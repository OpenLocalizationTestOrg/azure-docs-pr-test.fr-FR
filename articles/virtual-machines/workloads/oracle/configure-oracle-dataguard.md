---
title: aaaImplement Oracle Data Guard sur une machine virtuelle de Azure Linux | Documents Microsoft
description: "Configurez et exécutez rapidement Oracle Data Guard dans votre environnement Azure."
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
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a>Implémenter Oracle Data Guard sur une machine virtuelle Azure Linux 

CLI Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts. Cet article décrit comment toouse CLI d’Azure toodeploy une base de données Oracle 12C de base de données à partir de l’image d’Azure Marketplace hello. Cet article montre ensuite vous, étape par étape comment tooinstall et configurer Data Guard sur une machine virtuelle Azure (VM).

Avant de commencer, vérifiez qu’Azure CLI est installé. Pour plus d’informations, consultez hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Préparer l’environnement de hello
### <a name="assumptions"></a>Hypothèses

tooinstall Oracle Data Guard, vous devez toocreate deux machines virtuelles Azure hello même groupe à haute disponibilité :

- Hello ordinateur virtuel principal (myVM1) a une instance Oracle en cours d’exécution.
- Hello que machine virtuelle de secours (myVM2) dispose d’un hello Oracle logiciel uniquement.

image de Marketplace que vous utilisez toocreate hello machines virtuelles Hello est Oracle : Oracle-base de données-Ee:12.1.0.2:latest.

### <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure 

Se connecter à l’aide de hello tooyour abonnement Azure [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources à l’aide de hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westus` emplacement :

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Créer un groupe à haute disponibilité

La création d’un groupe à haute disponibilité est facultative, mais recommandée. Pour plus d’informations, consultez [Instructions pour les groupes à haute disponibilité Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle

Créer une machine virtuelle à l’aide de hello [az vm créer](/cli/azure/vm#create) commande. 

Hello exemple suivant crée deux ordinateurs virtuels nommés `myVM1` et `myVM2`. Il crée également des clés SSH si elles n’existent pas déjà à un emplacement de clé par défaut. toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.

Créez myVM1 (machine virtuelle principale) :
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

Après avoir créé la machine virtuelle de hello, CLI d’Azure affiche des informations similaires toohello est l’exemple suivant. Notez la valeur hello `publicIpAddress`. Vous utilisez cette hello de tooaccess adresse machine virtuelle.

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

Créez myVM2 (machine virtuelle de secours) :
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

Notez la valeur hello `publicIpAddress` après avoir créé le myVM2.

### <a name="open-hello-tcp-port-for-connectivity"></a>Ouvrez le port TCP hello pour la connectivité

Cette étape configure les points de terminaison externes, qui permettent la base de données Oracle de toohello l’accès à distance.

Ouvrez le port hello pour myVM1 :

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

résultat de Hello doit ressembler similaire toohello suivant la réponse :

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

Ouvrez le port hello pour myVM2 :

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Connecter l’ordinateur virtuel de toohello

La commande suivante de hello utilisation toocreate une session SSH avec l’ordinateur virtuel de hello. Remplacer l’adresse IP de hello avec hello `publicIpAddress` valeur pour votre machine virtuelle.

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Créer la base de données hello sur myVM1 (principal)

Hello logiciels Oracle est déjà installé sur une image Marketplace hello, afin de l’étape suivante de hello est la base de données tooinstall hello. 

Super utilisateur de commutateur toohello Oracle :

```bash
$ sudo su - oracle
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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

Définissez les variables ORACLE_SID et ORACLE_HOME hello :

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

Si vous le souhaitez, vous pouvez ajouter ORACLE_HOME et ORACLE_SID fichier /home/oracle/.bashrc toohello, afin que ces paramètres sont enregistrés pour les futures connexions :

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a>Configurer Data Guard

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
Activez la journalisation forcée et vérifiez qu’au moins un fichier journal est présent :

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

Créez des journaux de rétablissement de secours :

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

Activer la restauration (ce qui rend la beaucoup plus facile de récupération) et définir la mise en veille\_fichier\_tooauto de gestion. Quittez ensuite SQL* Plus.

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a>Configurer le service sur myVM1 (machine virtuelle principale)

Modifiez ou créez le fichier tnsnames.ora hello, qui se trouve dans le dossier de ORACLE_HOME\network\admin $ hello.

Ajoutez hello suivant entrées :

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

Modifiez ou créez le fichier listener.ora hello, qui se trouve dans le dossier de ORACLE_HOME\network\admin $ hello.

Ajoutez hello suivant entrées :

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Activez Data Guard Broker :
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
Démarrer l’écouteur de hello :

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a>Configurer le service sur myVM2 (machine virtuelle de secours)

SSH toomyVM2 :

```bash 
$ ssh azureuser@<publicIpAddress>
```

Connectez-vous en tant qu’Oracle :

```bash
$ sudo su - oracle
```

Modifiez ou créez le fichier tnsnames.ora hello, qui se trouve dans le dossier de ORACLE_HOME\network\admin $ hello.

Ajoutez hello suivant entrées :

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

Modifiez ou créez le fichier listener.ora hello, qui se trouve dans le dossier de ORACLE_HOME\network\admin $ hello.

Ajoutez hello suivant entrées :

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Démarrer l’écouteur de hello :

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a>Restaurer hello de base de données toomyVM2 (de secours)

Créer hello paramètre fichier /tmp/initcdb1_stby.ora avec hello suivant le contenu :
```bash
*.db_name='cdb1'
```

Créez les dossiers :

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

Créez un fichier de mot de passe :

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
Démarrer la base de données hello sur myVM2 :

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

Restaurer la base de données de hello en utilisant l’outil RMAN hello :

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

Exécutez hello suivant les commandes dans RMAN :
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

Vous devez voir s’afficher les messages similaires toohello lors de la commande hello est terminée. Quittez RMAN.
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

Si vous le souhaitez, vous pouvez ajouter ORACLE_HOME et ORACLE_SID fichier /home/oracle/.bashrc toohello, afin que ces paramètres sont enregistrés pour les futures connexions :

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

Activez Data Guard Broker :
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>Configurer Data Guard Broker sur myVM1 (machine virtuelle principale)

Démarrez Data Guard Manager et connectez-vous à l’aide de SYS et d’un mot de passe (n’utilisez pas d’authentification du système d’exploitation). Effectuez les opérations suivantes de hello :

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

Revoir la configuration hello :
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

Vous avez terminé le programme d’installation de hello Oracle Data Guard. section suivante de Hello vous montre comment tootest hello connectivité et basculer.

### <a name="connect-hello-database-from-hello-client-machine"></a>Connexion de base de données hello à partir de l’ordinateur client de hello

Mettre à jour ou de créer le fichier tnsnames.ora de hello sur votre ordinateur client. Ce fichier est généralement $ORACLE_HOME\network\admin.

Remplacer les adresses IP de hello avec votre `publicIpAddress` valeurs pour myVM1 et myVM2 :

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

Démarrez SQL* Plus :

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a>Configuration de test hello Data Guard

### <a name="switch-over-hello-database-on-myvm1-primary"></a>Basculer la base de données de hello sur myVM1 (principal)

tooswitch de toostandby principal (cdb1 toocdb1_stby) :

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

Vous pouvez maintenant vous connecter à la base de données de secours toohello.

Démarrez SQL* Plus :

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a>Basculer la base de données de hello sur myVM2 (en attente)

tooswitch, exécutez suivant de hello sur myVM2 :
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

Une fois encore, vous devez maintenant être en mesure de tooconnect toohello base de données primaire.

Démarrez SQL* Plus :

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

Vous avez fini d’installation de hello et la configuration de Data Guard sur Oracle Linux.


## <a name="delete-hello-virtual-machine"></a>Supprimer la machine virtuelle de hello

Lorsque vous avez besoin n’est plus hello machine virtuelle, vous pouvez utiliser hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources :

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

[Didacticiel : Créer des machines virtuelles à haute disponibilité](../../linux/create-cli-complete.md)

[Explorer des exemples Azure CLI de déploiement de machines virtuelles](../../linux/cli-samples.md)
