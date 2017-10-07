---
title: "aaaCreate une base de données Oracle dans une machine virtuelle Azure | Documents Microsoft"
description: "Configurez et exécutez rapidement une base de données Oracle Database 12c dans votre environnement Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a>Créer une base de données Oracle dans une machine virtuelle Azure

Ce guide décrit en détail à l’aide de hello CLI d’Azure toodeploy une machine virtuelle Azure à partir de hello [image de la galerie de marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) commander toocreate une base de données Oracle 12C. Une fois que le serveur de hello est déployé, vous vous connectez via une connexion SSH dans la base de données Oracle ordre tooconfigure hello. 

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>Create virtual machine

toocreate un ordinateur virtuel (VM), utilisez hello [az vm créer](/cli/azure/vm#create) commande. 

Hello exemple suivant crée un ordinateur virtuel nommé `myVM`. Il crée également des clés SSH si elles n’existent pas déjà à un emplacement de clé par défaut. toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

Après avoir créé la machine virtuelle de hello, CLI d’Azure affiche des informations similaires toohello est l’exemple suivant. Notez la valeur hello pour `publicIpAddress`. Vous utilisez cette hello de tooaccess adresse machine virtuelle.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a>Se connecter toohello machine virtuelle

toocreate une session SSH avec hello machine virtuelle, utilisez hello commande suivante. Remplacer l’adresse IP de hello avec hello `publicIpAddress` valeur pour votre machine virtuelle.

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>Créer la base de données hello

Hello logiciels Oracle est déjà installé sur une image Marketplace hello. Créer une base de données comme suit. 

1.  Commutateur toohello *oracle* super utilisateur, puis d’écouteur de hello d’initialisation pour la journalisation :

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    sortie de Hello est similaire toohello suivantes :

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  Créer la base de données hello :

    ```bash
    dbca -silent \
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

    Base de données de quelques minutes toocreate hello nécessaire.

3. Fixer les variables oracle

Avant de vous connectez, vous devez tooset deux variables d’environnement : *ORACLE_HOME* et *ORACLE_SID*.

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
Vous pouvez également ajouter ORACLE_HOME et ORACLE_SID variables toohello .bashrc le fichier. Cela permet d’enregistrer les variables d’environnement hello pour les connexions futures. Confirmer les éléments suivants de hello instructions ont été ajoutées toohello `~/.bashrc` fichier à l’aide de l’éditeur de votre choix.

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Connectivité à Oracle EM Express

Pour un outil de gestion de l’interface graphique utilisateur que vous pouvez utiliser la base de données tooexplore hello, définissez Oracle EM Express. tooconnect tooOracle EM Express, vous devez tout d’abord configurer port hello dans Oracle. 

1. Se connecter à l’aide de sqlplus de la base de données tooyour :

    ```bash
    sqlplus / as sysdba
    ```

2. Une fois connecté, définissez le port hello 5502 pour EM Express

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. Conteneur de hello ouvrir PDB1 si ce n’est pas déjà ouvert, mais tout d’abord vérifier le statut de hello :

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    sortie de Hello est similaire toohello suivantes :

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. Si hello OPEN_MODE pour `PDB1` n’est pas de lecture et écriture, puis exécutez les commandes tooopen PDB1 de hello ce qui suit :

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

Vous devez tootype `quit` tooend hello sqlplus session et le type `exit` toologout de l’utilisateur d’oracle hello.

## <a name="automate-database-startup-and-shutdown"></a>Automatisation du démarrage et de l’arrêt de la base de données

base de données Oracle Hello par défaut ne démarre pas automatiquement lorsque vous redémarrez hello machine virtuelle. tooset des toostart de base de données Oracle hello automatiquement, tout d’abord vous connecter en tant que racine. Puis, créez et mettez à jour des fichiers système.

1. Connexion en tant qu’utilisateur racine
    ```bash
    sudo su -
    ```

2.  À l’aide de votre éditeur favori, de modifier le fichier de hello `/etc/oratab` et modifiez la valeur par défaut hello `N` trop`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  Créez un fichier nommé `/etc/init.d/dbora` et coller hello suivant contenu :

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  Modifiez les autorisations des fichiers *chmod* comme suit :

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  Créez des liens symboliques pour le démarrage et l’arrêt, comme suit :

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest vos modifications, redémarrez hello machine virtuelle :

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>Ouverture des ports pour la connectivité

tâche finale Hello est tooconfigure certains points de terminaison externes. tooset des hello du groupe de sécurité réseau Azure qui protège hello machine virtuelle, tout d’abord fermer votre session SSH Bonjour VM (doit avoir été exclu SSH lors du redémarrage de l’étape précédente). 

1.  point de terminaison hello tooopen que vous utilisez base de données Oracle tooaccess hello à distance, créez une règle de groupe de sécurité réseau avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) comme suit : 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  point de terminaison hello tooopen que vous utilisez tooaccess Oracle EM Express à distance, créez une règle de groupe de sécurité réseau avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) comme suit :

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. Si nécessaire, obtenir hello adresse IP publique de votre machine virtuelle à l’aide de [az réseau public-ip afficher](/cli/azure/network/public-ip#show) comme suit :

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  Connectez-vous à EM Express à partir de votre navigateur. Assurez-vous que votre navigateur est compatible avec EM Express (l’installation de Flash est requise) : 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

Vous pouvez vous connecter à l’aide de hello **SYS** de compte, puis activez les hello **tant que sysdba** case à cocher. Mot de passe utilisation hello **OraPasswd1** que vous définissez lors de l’installation. 

![Capture d’écran de la page de connexion Oracle OEM Express hello](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>Supprimer des ressources

Une fois que vous avez terminé d’exploration de votre première base de données Oracle sur Azure et hello VM n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, machine virtuelle et toutes les ressources de la commande.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur les autres [solutions Oracle sur Azure](oracle-considerations.md). 

Essayez de hello [installation et configuration d’Oracle Automated Storage Management](configure-oracle-asm.md) didacticiel.
