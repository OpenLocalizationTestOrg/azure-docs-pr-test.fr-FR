---
title: aaaImplement Oracle Golden la porte sur une machine virtuelle Linux de Azure | Documents Microsoft
description: "Configurez et exécutez rapidement une base de données Oracle Golden Gate dans votre environnement Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a>Implémenter Oracle Golden Gate sur une machine virtuelle Linux Azure 

Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts. Ce guide décrit en détail comment toouse hello CLI d’Azure toodeploy Oracle 12C de base de données à partir de l’image de la galerie Azure Marketplace hello. 

Ce document explique comment toocreate, installer et configurer Oracle Golden porte sur une machine virtuelle Azure.

Avant de commencer, assurez-vous que hello que CLI d’Azure a été installé. Pour plus d’informations, consultez le [Guide d’installation de l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Préparer l’environnement de hello

installation de Oracle Golden porte tooperform hello, vous devez toocreate deux machines virtuelles Azure hello même groupe à haute disponibilité. image de Marketplace Hello vous utilisez toocreate hello machines virtuelles est **Oracle : Oracle-base de données-Ee:12.1.0.2:latest**.

Également, vous devez toobe familiarisé avec Unix éditeur vi et que vous avez une connaissance élémentaire de x11 (X Windows).

Hello Voici un résumé de la configuration de l’environnement hello :
> 
> |  | **Site principal** | **Site de réplication** |
> | --- | --- | --- |
> | **Version d’Oracle** |Oracle 12c Version 2 – (12.1.0.2) |Oracle 12c Version 2 – (12.1.0.2)|
> | **Nom de la machine** |myVM1 |myVM2 |
> | **Système d’exploitation** |Oracle Linux 6.x |Oracle Linux 6.x |
> | **SID Oracle** |CDB1 |CDB1 |
> | **Schéma de réplication** |TEST|TEST |
> | **Propriétaire Golden Gate/réplication** |C##GGADMIN |REPUSER |
> | **Processus Golden Gate** |EXTORA |REPORA|


### <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure 

Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande. Puis suivez hello à l’écran.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et à partir duquel elles peuvent être gérées. 

Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westus` emplacement.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Créer un groupe à haute disponibilité

Hello suivant l’étape est facultative mais recommandée. Pour plus d’informations, consultez [Instructions pour les groupes à haute disponibilité Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle

Créer une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) commande. 

Hello exemple suivant crée deux ordinateurs virtuels nommés `myVM1` et `myVM2`. Créez les clés SSH si elles n’existent pas déjà dans un emplacement de clé par défaut. toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.

#### <a name="create-myvm1-primary"></a>Créez myVM1 (machine virtuelle principale) :
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Après l’hello que machine virtuelle a été créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant. (Notez hello `publicIpAddress`. Cette adresse est utilisée tooaccess hello machine virtuelle).

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

#### <a name="create-myvm2-replicate"></a>Créez myVM2 (machine virtuelle de réplication) :
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Prenez note de hello `publicIpAddress` ainsi une fois qu’elle a été créée.

### <a name="open-hello-tcp-port-for-connectivity"></a>Ouvrez le port TCP hello pour la connectivité

étape suivante de Hello est tooconfigure points de terminaison externes, qui permettent de base de données Oracle tooaccess hello à distance. tooconfigure hello points de terminaison externes, exécutez hello suivant les commandes.

#### <a name="open-hello-port-for-myvm1"></a>Ouvrez le port hello pour myVM1 :

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

les résultats de Hello doivent ressembler similaire toohello suivant la réponse :

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

#### <a name="open-hello-port-for-myvm2"></a>Ouvrez le port hello pour myVM2 :

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Connecter l’ordinateur virtuel de toohello

La commande suivante de hello utilisation toocreate une session SSH avec l’ordinateur virtuel de hello. Remplacer l’adresse IP de hello avec hello `publicIpAddress` de votre machine virtuelle.

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Créer la base de données hello sur myVM1 (principal)

Hello logiciels Oracle est déjà installé sur une image Marketplace hello, afin de l’étape suivante de hello est la base de données tooinstall hello. 

Identification des logiciels de hello superutilisateur « oracle » de hello :

```bash
sudo su - oracle
```

Créer la base de données hello :

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Sorties doivent être similaire toohello suivant la réponse :

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

Définir les variables ORACLE_SID et ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Si vous le souhaitez, vous pouvez ajouter ORACLE_HOME et ORACLE_SID fichier .bashrc toohello, afin que ces paramètres sont enregistrés pour les futures connexions :

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Démarrer l’écouteur d’Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a>Créer la base de données hello sur myVM2 (réplication)

```bash
sudo su - oracle
```
Créer la base de données hello :

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Définir les variables ORACLE_SID et ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Si vous le souhaitez, vous pouvez ajouté ORACLE_HOME et ORACLE_SID toohello .bashrc de fichier, afin que ces paramètres sont enregistrés pour les futures connexions.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Démarrer l’écouteur d’Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a>Configurer Golden Gate 
tooconfigure Golden porte, prendre des mesures de hello dans cette section.

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>Activer le mode de journalisation d’archive sur myVM1 (machine virtuelle principale)

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
Activez la journalisation forcée et assurez-vous qu’au moins un fichier journal est présent.

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a>Télécharger le logiciel Golden Gate
toodownload et préparer un logiciel Oracle Golden porte hello, hello complète comme suit :

1. Télécharger hello **fbo_ggs_Linux_x64_shiphome.zip** fichier hello [page de téléchargement Oracle Golden porte](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html). Sous hello télécharger titre **12.x.x.x GoldenGate Oracle pour Oracle Linux x86-64**, il doit y avoir un ensemble de toodownload de fichiers .zip.

2. Après avoir téléchargé hello .zip fichiers tooyour client ordinateur, utilisez Secure copie Protocol (SCP) toocopy hello fichiers tooyour machine virtuelle :

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. Déplacer hello .zip fichiers toohello **/ opt** dossier. Puis modifiez le propriétaire hello des fichiers de hello comme suit :

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. Décompresser les fichiers de hello (installation hello Linux décompresser utilitaire s’il n’est pas déjà installé) :

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. Changez l’autorisation :

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a>Préparer le client de hello et de la machine virtuelle toorun x11 (pour les clients Windows uniquement)
Il s’agit d’une étape facultative. Vous pouvez l’ignorer si vous utilisez un client Linux ou si x11 est déjà configuré.

1. Vous pouvez télécharger PuTTY et Xming ordinateur Windows de tooyour :

  * [Télécharger PuTTY](http://www.putty.org/)
  * [Télécharger Xming](https://xming.en.softonic.com/)

2.  Après avoir installé PuTTY, en hello PuTTY dossier (par exemple, C:\Program Files\PuTTY), exécutez puttygen.exe (Générateur de clé PuTTY).

3.  Dans PuTTY Key Generator :

  - toogenerate un Bonjour clé, sélectionnez **générer** bouton.
  - Copier le contenu de hello de clé de hello (**Ctrl + C**).
  - Sélectionnez hello **clé privée d’enregistrement** bouton.
  - Ignorer l’avertissement hello qui s’affiche, puis sélectionnez **OK**.

    ![Capture d’écran de la page de générateur de clé PuTTY hello](./media/oracle-golden-gate/puttykeygen.png)

4.  Dans votre machine virtuelle, exécutez ces commandes :

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. Créez un fichier nommé **authorized_keys**. Collez le contenu hello de clé de hello dans ce fichier, puis enregistrez le fichier de hello.

  > [!NOTE]
  > clé de Hello doit contenir la chaîne de hello `ssh-rsa`. En outre, le contenu hello de clé de hello doit être une seule ligne de texte.
  >  

6. Démarrez PuTTY. Bonjour **catégorie** volet, sélectionnez **connexion** > **SSH** > **Auth**. Bonjour **fichier de clé privée pour l’authentification** , naviguez jusque toohello clé que vous avez créé précédemment.

  ![Capture d’écran de la page Définir la clé privée de hello](./media/oracle-golden-gate/setprivatekey.png)

7. Bonjour **catégorie** volet, sélectionnez **connexion** > **SSH** > **X11**. Puis sélectionnez hello **X11 d’activer le transfert** boîte.

  ![Capture d’écran de la page d’activation X11 hello](./media/oracle-golden-gate/enablex11.png)

8. Bonjour **catégorie** volet, accédez trop**Session**. Entrez les informations sur l’hôte hello et sélectionnez **ouvrir**.

  ![Capture d’écran de la page de session hello](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a>Installer le logiciel Golden Gate

tooinstall Oracle Golden porte, hello complète comme suit :

1. Connectez-vous en tant qu’oracle. (Vous devez être en mesure de toosign dans sans être invité à entrer un mot de passe.) Assurez-vous que Xming est en cours d’exécution avant de commencer l’installation de hello.
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. Sélectionnez « Oracle GoldenGate for Oracle Database 12c ». Puis sélectionnez **suivant** toocontinue.

  ![Capture d’écran de la page de sélectionner l’Installation de programme d’installation de hello](./media/oracle-golden-gate/golden_gate_install_01.png)

3. Modifier l’emplacement du logiciel hello. Puis sélectionnez hello **démarrer le Gestionnaire de** zone, puis entrez l’emplacement de base de données hello. Sélectionnez **suivant** toocontinue.

  ![Capture d’écran de la page Sélectionnez une Installation de hello](./media/oracle-golden-gate/golden_gate_install_02.png)

4. Basculez hello d’inventaire, puis **suivant** toocontinue.

  ![Capture d’écran de la page Sélectionnez une Installation de hello](./media/oracle-golden-gate/golden_gate_install_03.png)

5. Sur hello **Résumé** écran, sélectionnez **installer** toocontinue.

  ![Capture d’écran de la page de sélectionner l’Installation de programme d’installation de hello](./media/oracle-golden-gate/golden_gate_install_04.png)

6. Vous pouvez être invité à toorun un script en tant que « root ». Dans ce cas, d’ouvrir une session distincte, ssh toohello machine virtuelle, sudo tooroot et puis exécutez le script de hello. Sélectionnez **OK** pour continuer.

  ![Capture d’écran de la page Sélectionnez une Installation de hello](./media/oracle-golden-gate/golden_gate_install_05.png)

7. Lors de l’installation de hello est terminée, sélectionnez **fermer** processus de hello toocomplete.

  ![Capture d’écran de la page Sélectionnez une Installation de hello](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a>Configurer le service sur myVM1 (machine virtuelle principale)

1. Créer ou mettre à jour le fichier tnsnames.ora de hello :

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Permet de créer des comptes de propriétaire et utilisateur Golden porte de hello.

  > [!NOTE]
  > compte de propriétaire de Hello doit avoir le préfixe C ##.
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. Créer un compte d’utilisateur test hello Golden porte :

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. Configurer le fichier de paramètres d’extraction hello.

 Démarrer une interface de ligne hello porte finale (ggsci) :

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. Ajoutez hello suivant du fichier de paramètres d’extraction toohello (à l’aide des commandes de vi). Appuyez sur la touche ÉCHAP, ':wq!' fichier de toosave. 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. Extrait de registre--extrait intégré :

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. Configurer des points de contrôle d’extraction et démarrer l’extraction en temps réel :

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
Dans cette étape, vous trouver hello SCN, qui sera utilisée ultérieurement, dans une autre section de démarrage :

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a>Configurer le service sur myVM2 (machine virtuelle de réplication)


1. Créer ou mettre à jour le fichier tnsnames.ora de hello :

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Créez un compte de réplication :

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. Créez un compte d’utilisateur de test de Golden Gate :

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. Modifications de tooreplicate paramètre fichier REPLICAT : 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  Contenu du fichier de paramètres REPORA :

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. Configurez un point de contrôle de réplication :

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a>Configurer la réplication hello (myVM1 et myVM2)

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a>1. Configurer la réplication hello sur myVM2 (réplication)

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
Mettre à jour les fichiers hello avec les éléments suivants de hello :

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
Puis redémarrez le service Manager hello :

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a>2. Configurer la réplication hello sur myVM1 (principal)

Démarrez la charge initiale hello et recherchez les erreurs :

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a>3. Configurer la réplication hello sur myVM2 (réplication)

Modifier hello numéro SCN avec le nombre de hello que vous avez obtenus avant :

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
la réplication Hello a commencé, et vous pouvez le tester en insérant de nouvelles tables de tooTEST d’enregistrements.


### <a name="view-job-status-and-troubleshooting"></a>Afficher l’état du travail et la résolution des problèmes

#### <a name="view-reports"></a>Afficher des rapports
tooview signale myVM1, exécutez hello suivant de commandes :

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
tooview signale myVM2, exécutez hello suivant de commandes :

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a>Afficher l’état et l’historique
tooview état et l’historique sur myVM1, exécutez hello suivant de commandes :

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

tooview état et l’historique sur myVM2, exécutez hello suivant de commandes :

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
Cela termine l’installation de hello et la configuration de Golden porte sur Oracle linux.


## <a name="delete-hello-virtual-machine"></a>Supprimer la machine virtuelle de hello

Lorsqu’il n’est plus nécessaire, hello commande suivante peut être groupe de ressources utilisé tooremove hello, machine virtuelle et toutes les ressources.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

[Didacticiel de création de machines virtuelles hautement disponibles](../../linux/create-cli-complete.md)

[Découvrir des exemples de commande de déploiement de machine virtuelle](../../linux/cli-samples.md)
