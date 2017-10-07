---
title: "aaaBack haut et récupérer une base de données Oracle 12C de base de données sur une machine virtuelle de Azure Linux | Documents Microsoft"
description: "Découvrez comment tooback haut et récupérer une base de données Oracle 12C base de données dans votre environnement Windows Azure."
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
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Sauvegarder et récupérer une base de données de la base de données Oracle Database 12c sur une machine virtuelle Linux Azure

Vous pouvez utiliser Azure CLI toocreate et gérer des ressources Azure à l’invite de commande ou utiliser des scripts. Dans cet article, nous utilisons toodeploy de scripts CLI d’Azure une base de données de 12c de base de données Oracle à partir d’une image de la galerie Azure Marketplace.

Avant de commencer, vérifiez qu’Azure CLI est installé. Pour plus d’informations, consultez hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Préparer l’environnement de hello

### <a name="step-1-prerequisites"></a>Étape 1 : Conditions préalables

*   processus sauvegarde et récupération de hello tooperform, vous devez d’abord créer un VM Linux qui a une instance installée de la base de données Oracle 12C. image de Marketplace Hello que vous utilisez hello toocreate machine virtuelle se nomme *Oracle : Oracle-base de données-Ee:12.1.0.2:latest*.

    toolearn comment toocreate une base de données Oracle, consultez hello [Oracle créer démarrage rapide de base de données](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).


### <a name="step-2-connect-toohello-vm"></a>Étape 2 : Se connecter toohello machine virtuelle

*   toocreate une session SSH (Secure Shell) avec hello machine virtuelle, utilisez hello commande suivante. Remplacer l’adresse IP de hello et combinaison de nom d’hôte hello avec hello `publicIpAddress` valeur pour votre machine virtuelle.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>Étape 3 : Préparer la base de données hello

1.  Cette étape suppose que vous disposiez d’une instance Oracle (cdb1) s’exécutant sur une machine virtuelle nommée *myVM*.

    Exécutez hello *oracle* racine de super utilisateur, puis initialiser hello écouteur :

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
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

2.  (Facultatif) Vérifiez que hello est en mode de journal d’archivage :

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
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  (Facultatif) Créer un tableau tootest hello de validation :

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  Vérifier ou modifier la taille et l’emplacement du fichier de sauvegarde hello :

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Utilisez tooback Oracle Recovery Manager (RMAN) base de données hello :

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>Étape 4 : Sauvegarde cohérente avec les applications pour les machines virtuelles Linux

La sauvegarde cohérente avec les applications est une nouvelle fonctionnalité de Sauvegarde Azure. Vous pouvez créer et sélectionnez tooexecute des scripts avant et après l’instantané d’ordinateur virtuel hello (instantané avant et après les captures instantanées).

1. Téléchargez le fichier JSON de hello.

    Téléchargez VMSnapshotScriptPluginConfig.json à partir de https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig. contenu du fichier Hello recherche similaire toohello suivantes :

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. Créez le dossier de /etc/azure de hello sur hello machine virtuelle :

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. Copier le fichier JSON hello.

    Copiez le dossier de /etc/azure VMSnapshotScriptPluginConfig.json toohello.

4. Modifier le fichier JSON de hello.

    Modifier hello de hello VMSnapshotScriptPluginConfig.json fichier tooinclude `PreScriptLocation` et `PostScriptlocation` paramètres. Par exemple :

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. Créer des fichiers de script d’instantané avant et après les captures instantanées hello.

    Voici un exemple de script de pré-instantané et de post-instantané pour une « sauvegarde à froid » (sauvegarde hors connexion, avec arrêt et redémarrage) :

    Pour /etc/azure/pre_script.sh :

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    Pour /etc/azure/post_script.sh :

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    Voici un exemple de script de pré-instantané et de post-instantané pour une « sauvegarde à chaud » (sauvegarde en ligne) :

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Pour /etc/azure/post_script.sh :

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Pour /etc/azure/pre_script.sql, modifier le contenu de hello du fichier hello selon vos besoins :

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    Pour /etc/azure/post_script.sql, modifier le contenu de hello du fichier hello selon vos besoins :

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. Modifiez les autorisations des fichiers :

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. Tester des scripts de hello.

    scripts de hello tootest, tout d’abord, connectez-vous en tant que racine. Assurez-vous ensuite qu’il n’y a aucune erreur :

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

Pour plus d’informations, consultez [Sauvegarde cohérente avec les applications pour les machines virtuelles Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>Étape 5 : Utiliser les Services de récupération Azure coffres-forts tooback des hello machine virtuelle

1.  Dans l’hello portail Azure, recherchez **les coffres de Services de récupération**.

    ![Page Coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_01.png)

2.  Sur hello **les coffres de Services de récupération** panneau, tooadd un coffre, cliquez sur **ajouter**.

    ![Page d’ajout de coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue, cliquez sur **myVault**.

    ![Page de détails de coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_03.png)

4.  Sur hello **myVault** panneau, cliquez sur **sauvegarde**.

    ![Page de sauvegarde des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_04.png)

5.  Sur hello **sauvegarde objectif** panneau, utiliser hello des valeurs par défaut de **Azure** et **machine virtuelle**. Cliquez sur **OK**.

    ![Page de détails de coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_05.png)

6.  Pour **Stratégie de sauvegarde**, utilisez **DefaultPolicy** ou sélectionnez **Créer une stratégie**. Cliquez sur **OK**.

    ![Page de détails de la stratégie de sauvegarde des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_06.png)

7.  Sur hello **sélectionner des machines virtuelles** panneau, sélectionnez hello **myVM1** case à cocher, puis cliquez sur **OK**. Cliquez sur hello **Active la sauvegarde** bouton.

    ![Page de détail de sauvegarde de récupération Services coffres éléments toohello](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > Après avoir cliqué sur **Active la sauvegarde**, processus de sauvegarde hello ne commence pas tant que hello planifiée arrive à expiration. tooset d’une sauvegarde immédiate, complète hello étape suivante.

8.  Sur hello **myVault - éléments de sauvegarde** panneau, sous **nombre d’éléments de sauvegarde**, sélectionnez le nombre d’éléments de sauvegarde de hello.

    ![Page de détails myVault d’Archivages de Recovery Services](./media/oracle-backup-recovery/recovery_service_08.png)

9.  Sur hello **des éléments de sauvegarde (Machine virtuelle de Azure)** panneau, sur le côté droit de hello de page de hello, cliquez sur les points de suspension hello (**...** ) bouton, puis cliquez sur **sauvegarder maintenant**.

    ![Commande Sauvegarder maintenant des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_09.png)

10. Cliquez sur hello **sauvegarde** bouton. Attendez que toofinish du processus de sauvegarde hello. Ensuite, passez trop[étape 6 : supprimer les fichiers de base de données hello](#step-6-remove-the-database-files).

    tooview hello le statut de tâche de sauvegarde hello, cliquez sur **travaux**.

    ![Page de travail des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_10.png)

    état de Hello du travail de sauvegarde hello apparaît dans hello suivant l’image :

    ![Page de travail d’Archivages de Recovery Services avec état](./media/oracle-backup-recovery/recovery_service_11.png)

11. Pour une sauvegarde cohérente avec les applications, résolvez les éventuelles erreurs dans le fichier journal de hello. fichier de journal Hello se trouve dans /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.

### <a name="step-6-remove-hello-database-files"></a>Étape 6 : Supprimer les fichiers de base de données hello 
Plus loin dans cet article, vous allez apprendre comment tootest hello le processus de récupération. Avant de pouvoir tester les processus de récupération hello, vous disposez des fichiers de base de données tooremove hello.

1.  Supprimer les fichiers de sauvegarde et d’espace disque logique hello :

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (Facultatif) Arrêtez l’instance Oracle hello :

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>Restaurer les fichiers de hello supprimé à partir de hello que les coffres de Services de récupération
toorestore hello supprimé des fichiers, hello complète comme suit :

1. Bonjour portail Azure, recherchez hello *myVault* élément les coffres de Services de récupération. Sur hello **vue d’ensemble** panneau, sous **sauvegarde éléments**, sélectionnez nombre hello d’éléments.

    ![Éléments de sauvegarde myVault des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_12.png)

2. Sous **nombre d’éléments de sauvegarde**, sélectionnez le nombre hello d’éléments.

    ![Nombre d’éléments de sauvegarde de machine virtuelle Azure des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_13.png)

3. Sur hello **myvm1** panneau, cliquez sur **récupération de fichier (version préliminaire)**.

    ![Capture d’écran de Services de récupération de hello les coffres de page de récupération du fichier](./media/oracle-backup-recovery/recovery_service_14.png)

4. Sur hello **récupération de fichier (version préliminaire)** volet, cliquez sur **télécharger le Script**. Enregistrez ensuite le fichier tooa dossier hello téléchargement (.sh) sur l’ordinateur client de hello.

    ![Options d’enregistrement de fichier de script téléchargé](./media/oracle-backup-recovery/recovery_service_15.png)

5. Copiez hello .sh fichier toohello machine virtuelle.

    Hello, l’exemple suivant montre comment vous toouse un toomove de commande de copie sécurisée (scp) hello fichier toohello machine virtuelle. Vous pouvez également copier le Presse-papiers de toohello contenu hello, puis coller hello contenu dans un nouveau fichier qui est configuré sur la machine virtuelle de hello.

    > [!IMPORTANT]
    > Dans l’exemple suivant de hello, assurez-vous que vous mettez à jour les valeurs d’adresse et le dossier IP hello. les valeurs Hello doivent mapper toohello dossier où hello est enregistré.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Modifier le fichier de hello, afin qu’il appartient à la racine de hello.

    Dans l’exemple suivant de hello, remplacez le fichier de la hello afin qu’il appartient à la racine de hello. Modifiez ensuite les autorisations.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    Hello suivant montre ce que vous devez voir après avoir exécuté hello précédant le script. Lorsque vous êtes invité à entrer toocontinue, entrez **Y**.

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. Accès toohello monté volumes est confirmée.

    tooexit, entrez **q**, puis recherchez les volumes hello monté. toocreate une liste de hello ajoutée de volumes, à l’invite de commandes, entrez **df -k**.

    ![commande Hello df-k](./media/oracle-backup-recovery/recovery_service_16.png)

8. Hello utilisation suivante du script toocopy hello manquant fichiers toohello arrière dossiers :

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. Bonjour le script suivant, utiliser de base de données RMAN toorecover hello :

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Démontez le disque de hello.

    Bonjour portail Azure, sur hello **récupération de fichier (version préliminaire)** panneau, cliquez sur **démontage de disques**.

    ![Commande Démonter les disques](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>Restaurer hello machine virtuelle entière

Au lieu de restaurer les fichiers hello supprimé à partir des archivages de Recovery Services hello, vous pouvez restaurer hello machine virtuelle entière.

### <a name="step-1-delete-myvm"></a>Étape 1 : Supprimer myVM

*   Bonjour portail Azure, accédez à toohello **myVM1** coffre et sélectionnez **supprimer**.

    ![Commande Supprimer du coffre](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>Étape 2 : Récupération hello machine virtuelle

1.  Accédez trop**les coffres de Services de récupération**, puis sélectionnez **myVault**.

    ![Entrée myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  Sur hello **vue d’ensemble** panneau, sous **sauvegarde éléments**, sélectionnez nombre hello d’éléments.

    ![Éléments de sauvegarde myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  Sur hello **des éléments de sauvegarde (Machine virtuelle de Azure)** panneau, sélectionnez **myvm1**.

    ![Page de récupération de machine virtuelle](./media/oracle-backup-recovery/recover_vm_04.png)

4.  Sur hello **myvm1** panneau, cliquez sur les points de suspension hello (**...** ) bouton, puis cliquez sur **restaurer la machine virtuelle**.

    ![Commande Restaurer la machine virtuelle](./media/oracle-backup-recovery/recover_vm_05.png)

5.  Sur hello **point de restauration** panneau, sélectionnez hello élément que vous souhaitez toorestore, puis cliquez sur **OK**.

    ![Point de restauration hello SELECT](./media/oracle-backup-recovery/recover_vm_06.png)

    Si vous avez activé la sauvegarde cohérente avec les applications, une barre bleue verticale apparaît.

6.  Sur hello **restaurer la configuration** panneau, nom d’ordinateur virtuel, sélectionnez hello, sélectionnez le groupe de ressources hello, puis cliquez sur **OK**.

    ![Restaurer les valeurs de configuration](./media/oracle-backup-recovery/recover_vm_07.png)

7.  toorestore hello machine virtuelle, cliquez sur hello **restaurer** bouton.

8.  état de hello tooview hello processus de restauration, cliquez sur **travaux**, puis cliquez sur **des tâches de sauvegarde**.

    ![Commande d’état des travaux de sauvegarde](./media/oracle-backup-recovery/recover_vm_08.png)

    Hello figure ci-dessous illustre état hello du processus de restauration hello :

    ![État du processus de restauration hello](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>Étape 3 : Définir l’adresse IP publique de hello
Après hello que machine virtuelle est restaurée, configurer l’adresse IP publique de hello.

1.  Dans la zone de recherche de hello, entrez **adresse IP publique**.

    ![Liste d’adresses IP publiques](./media/oracle-backup-recovery/create_ip_00.png)

2.  Sur hello **des adresses IP publiques** panneau, cliquez sur **ajouter**. Sur hello **créer une adresse IP publique** panneau, pour **nom**, sélectionnez les nom IP public hello. Pour **Groupe de ressources**, sélectionnez **Use existing** (Utiliser existant). Cliquez sur **Créer**.

    ![Créer une adresse IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  tooassociate hello adresse IP publique avec une interface réseau hello hello machine virtuelle, rechercher des et sélectionnez **myVMip**. Cliquez ensuite sur **Associer**.

    ![Associer une adresse IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  Pour **Type de ressource**, sélectionnez **Interface réseau**. Sélectionnez l’interface réseau hello qui est utilisé par l’instance de myVM hello, puis cliquez sur **OK**.

    ![Sélectionner le type de ressource et les valeurs de carte réseau](./media/oracle-backup-recovery/create_ip_03.png)

5.  Recherchez et ouvrez l’instance hello de myVM est déplacée à partir du portail de hello. Hello adresse IP associé à hello machine virtuelle apparaît sur hello myVM **vue d’ensemble** panneau.

    ![Valeur d’adresse IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>Étape 4 : Connecter toohello machine virtuelle

*   tooconnect toohello machine virtuelle, utilisez hello script suivant :

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>Étape 5 : Tester si la base de données hello est accessible
*   tootest accessibilité, hello utilisez script suivant :

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > Base de données si hello **démarrage** commande génère une erreur, la base de données toorecover hello, consultez [étape 6 : base de données utilisez RMAN toorecover hello](#step-6-optional-use-rman-to-recover-the-database).

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>Étape 6 : Base de données (facultatif) utilisez RMAN toorecover hello
*   toorecover hello base de données, hello utilisez script suivant :

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

sauvegarde de Hello et la récupération de base de données de 12c de base de données Oracle hello sur une machine virtuelle Linux de Azure est maintenant terminé.

## <a name="delete-hello-vm"></a>Supprimer hello machine virtuelle

Lorsque vous avez besoin n’est plus hello machine virtuelle, vous pouvez utiliser hello suivant du groupe de ressources de commande tooremove hello, hello machine virtuelle et toutes les ressources :

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

[Didacticiel : créer des machines virtuelles hautement disponibles](../../linux/create-cli-complete.md)

[Explorer des exemples Azure CLI de déploiement de machines virtuelles](../../linux/cli-samples.md)



