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
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="b8e50-103">Sauvegarder et récupérer une base de données de la base de données Oracle Database 12c sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="b8e50-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="b8e50-104">Vous pouvez utiliser Azure CLI toocreate et gérer des ressources Azure à l’invite de commande ou utiliser des scripts.</span><span class="sxs-lookup"><span data-stu-id="b8e50-104">You can use Azure CLI toocreate and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="b8e50-105">Dans cet article, nous utilisons toodeploy de scripts CLI d’Azure une base de données de 12c de base de données Oracle à partir d’une image de la galerie Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b8e50-105">In this article, we use Azure CLI scripts toodeploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="b8e50-106">Avant de commencer, vérifiez qu’Azure CLI est installé.</span><span class="sxs-lookup"><span data-stu-id="b8e50-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="b8e50-107">Pour plus d’informations, consultez hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b8e50-107">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="b8e50-108">Préparer l’environnement de hello</span><span class="sxs-lookup"><span data-stu-id="b8e50-108">Prepare hello environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="b8e50-109">Étape 1 : Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="b8e50-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="b8e50-110">processus sauvegarde et récupération de hello tooperform, vous devez d’abord créer un VM Linux qui a une instance installée de la base de données Oracle 12C.</span><span class="sxs-lookup"><span data-stu-id="b8e50-110">tooperform hello backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="b8e50-111">image de Marketplace Hello que vous utilisez hello toocreate machine virtuelle se nomme *Oracle : Oracle-base de données-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="b8e50-111">hello Marketplace image you use toocreate hello VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="b8e50-112">toolearn comment toocreate une base de données Oracle, consultez hello [Oracle créer démarrage rapide de base de données](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="b8e50-112">toolearn how toocreate an Oracle database, see hello [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-toohello-vm"></a><span data-ttu-id="b8e50-113">Étape 2 : Se connecter toohello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b8e50-113">Step 2: Connect toohello VM</span></span>

*   <span data-ttu-id="b8e50-114">toocreate une session SSH (Secure Shell) avec hello machine virtuelle, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="b8e50-114">toocreate a Secure Shell (SSH) session with hello VM, use hello following command.</span></span> <span data-ttu-id="b8e50-115">Remplacer l’adresse IP de hello et combinaison de nom d’hôte hello avec hello `publicIpAddress` valeur pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b8e50-115">Replace hello IP address and hello host name combination with hello `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a><span data-ttu-id="b8e50-116">Étape 3 : Préparer la base de données hello</span><span class="sxs-lookup"><span data-stu-id="b8e50-116">Step 3: Prepare hello database</span></span>

1.  <span data-ttu-id="b8e50-117">Cette étape suppose que vous disposiez d’une instance Oracle (cdb1) s’exécutant sur une machine virtuelle nommée *myVM*.</span><span class="sxs-lookup"><span data-stu-id="b8e50-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="b8e50-118">Exécutez hello *oracle* racine de super utilisateur, puis initialiser hello écouteur :</span><span class="sxs-lookup"><span data-stu-id="b8e50-118">Run hello *oracle* superuser root, and then initialize hello listener:</span></span>

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

2.  <span data-ttu-id="b8e50-119">(Facultatif) Vérifiez que hello est en mode de journal d’archivage :</span><span class="sxs-lookup"><span data-stu-id="b8e50-119">(Optional) Make sure hello database is in archive log mode:</span></span>

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
3.  <span data-ttu-id="b8e50-120">(Facultatif) Créer un tableau tootest hello de validation :</span><span class="sxs-lookup"><span data-stu-id="b8e50-120">(Optional) Create a table tootest hello commit:</span></span>

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
4.  <span data-ttu-id="b8e50-121">Vérifier ou modifier la taille et l’emplacement du fichier de sauvegarde hello :</span><span class="sxs-lookup"><span data-stu-id="b8e50-121">Verify or change hello backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="b8e50-122">Utilisez tooback Oracle Recovery Manager (RMAN) base de données hello :</span><span class="sxs-lookup"><span data-stu-id="b8e50-122">Use Oracle Recovery Manager (RMAN) tooback up hello database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="b8e50-123">Étape 4 : Sauvegarde cohérente avec les applications pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="b8e50-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="b8e50-124">La sauvegarde cohérente avec les applications est une nouvelle fonctionnalité de Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="b8e50-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="b8e50-125">Vous pouvez créer et sélectionnez tooexecute des scripts avant et après l’instantané d’ordinateur virtuel hello (instantané avant et après les captures instantanées).</span><span class="sxs-lookup"><span data-stu-id="b8e50-125">You can create and select scripts tooexecute before and after hello VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="b8e50-126">Téléchargez le fichier JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-126">Download hello JSON file.</span></span>

    <span data-ttu-id="b8e50-127">Téléchargez VMSnapshotScriptPluginConfig.json à partir de https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span><span class="sxs-lookup"><span data-stu-id="b8e50-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="b8e50-128">contenu du fichier Hello recherche similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="b8e50-128">hello file contents look similar toohello following:</span></span>

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

2. <span data-ttu-id="b8e50-129">Créez le dossier de /etc/azure de hello sur hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="b8e50-129">Create hello /etc/azure folder on hello VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="b8e50-130">Copier le fichier JSON hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-130">Copy hello JSON file.</span></span>

    <span data-ttu-id="b8e50-131">Copiez le dossier de /etc/azure VMSnapshotScriptPluginConfig.json toohello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-131">Copy VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span></span>

4. <span data-ttu-id="b8e50-132">Modifier le fichier JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-132">Edit hello JSON file.</span></span>

    <span data-ttu-id="b8e50-133">Modifier hello de hello VMSnapshotScriptPluginConfig.json fichier tooinclude `PreScriptLocation` et `PostScriptlocation` paramètres.</span><span class="sxs-lookup"><span data-stu-id="b8e50-133">Edit hello VMSnapshotScriptPluginConfig.json file tooinclude hello `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="b8e50-134">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b8e50-134">For example:</span></span>

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

5. <span data-ttu-id="b8e50-135">Créer des fichiers de script d’instantané avant et après les captures instantanées hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-135">Create hello pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="b8e50-136">Voici un exemple de script de pré-instantané et de post-instantané pour une « sauvegarde à froid » (sauvegarde hors connexion, avec arrêt et redémarrage) :</span><span class="sxs-lookup"><span data-stu-id="b8e50-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="b8e50-137">Pour /etc/azure/pre_script.sh :</span><span class="sxs-lookup"><span data-stu-id="b8e50-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="b8e50-138">Pour /etc/azure/post_script.sh :</span><span class="sxs-lookup"><span data-stu-id="b8e50-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="b8e50-139">Voici un exemple de script de pré-instantané et de post-instantané pour une « sauvegarde à chaud » (sauvegarde en ligne) :</span><span class="sxs-lookup"><span data-stu-id="b8e50-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="b8e50-140">Pour /etc/azure/post_script.sh :</span><span class="sxs-lookup"><span data-stu-id="b8e50-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="b8e50-141">Pour /etc/azure/pre_script.sql, modifier le contenu de hello du fichier hello selon vos besoins :</span><span class="sxs-lookup"><span data-stu-id="b8e50-141">For /etc/azure/pre_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="b8e50-142">Pour /etc/azure/post_script.sql, modifier le contenu de hello du fichier hello selon vos besoins :</span><span class="sxs-lookup"><span data-stu-id="b8e50-142">For /etc/azure/post_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="b8e50-143">Modifiez les autorisations des fichiers :</span><span class="sxs-lookup"><span data-stu-id="b8e50-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="b8e50-144">Tester des scripts de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-144">Test hello scripts.</span></span>

    <span data-ttu-id="b8e50-145">scripts de hello tootest, tout d’abord, connectez-vous en tant que racine.</span><span class="sxs-lookup"><span data-stu-id="b8e50-145">tootest hello scripts, first, sign in as root.</span></span> <span data-ttu-id="b8e50-146">Assurez-vous ensuite qu’il n’y a aucune erreur :</span><span class="sxs-lookup"><span data-stu-id="b8e50-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="b8e50-147">Pour plus d’informations, consultez [Sauvegarde cohérente avec les applications pour les machines virtuelles Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="b8e50-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a><span data-ttu-id="b8e50-148">Étape 5 : Utiliser les Services de récupération Azure coffres-forts tooback des hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b8e50-148">Step 5: Use Azure Recovery Services vaults tooback up hello VM</span></span>

1.  <span data-ttu-id="b8e50-149">Dans l’hello portail Azure, recherchez **les coffres de Services de récupération**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-149">In hello Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Page Coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="b8e50-151">Sur hello **les coffres de Services de récupération** panneau, tooadd un coffre, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-151">On hello **Recovery Services vaults** blade, tooadd a new vault, click **Add**.</span></span>

    ![Page d’ajout de coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="b8e50-153">toocontinue, cliquez sur **myVault**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-153">toocontinue, click **myVault**.</span></span>

    ![Page de détails de coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="b8e50-155">Sur hello **myVault** panneau, cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-155">On hello **myVault** blade, click **Backup**.</span></span>

    ![Page de sauvegarde des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="b8e50-157">Sur hello **sauvegarde objectif** panneau, utiliser hello des valeurs par défaut de **Azure** et **machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-157">On hello **Backup Goal** blade, use hello default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="b8e50-158">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-158">Click **OK**.</span></span>

    ![Page de détails de coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="b8e50-160">Pour **Stratégie de sauvegarde**, utilisez **DefaultPolicy** ou sélectionnez **Créer une stratégie**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="b8e50-161">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-161">Click **OK**.</span></span>

    ![Page de détails de la stratégie de sauvegarde des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="b8e50-163">Sur hello **sélectionner des machines virtuelles** panneau, sélectionnez hello **myVM1** case à cocher, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-163">On hello **Select virtual machines** blade, select hello **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="b8e50-164">Cliquez sur hello **Active la sauvegarde** bouton.</span><span class="sxs-lookup"><span data-stu-id="b8e50-164">Click hello **Enable backup** button.</span></span>

    ![Page de détail de sauvegarde de récupération Services coffres éléments toohello](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="b8e50-166">Après avoir cliqué sur **Active la sauvegarde**, processus de sauvegarde hello ne commence pas tant que hello planifiée arrive à expiration.</span><span class="sxs-lookup"><span data-stu-id="b8e50-166">After you click **Enable backup**, hello backup process doesn't start until hello scheduled time expires.</span></span> <span data-ttu-id="b8e50-167">tooset d’une sauvegarde immédiate, complète hello étape suivante.</span><span class="sxs-lookup"><span data-stu-id="b8e50-167">tooset up an immediate backup, complete hello next step.</span></span>

8.  <span data-ttu-id="b8e50-168">Sur hello **myVault - éléments de sauvegarde** panneau, sous **nombre d’éléments de sauvegarde**, sélectionnez le nombre d’éléments de sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-168">On hello **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select hello backup item count.</span></span>

    ![Page de détails myVault d’Archivages de Recovery Services](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="b8e50-170">Sur hello **des éléments de sauvegarde (Machine virtuelle de Azure)** panneau, sur le côté droit de hello de page de hello, cliquez sur les points de suspension hello (**...** ) bouton, puis cliquez sur **sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-170">On hello **Backup Items (Azure Virtual Machine)** blade, on hello right side of hello page, click hello ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Commande Sauvegarder maintenant des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="b8e50-172">Cliquez sur hello **sauvegarde** bouton.</span><span class="sxs-lookup"><span data-stu-id="b8e50-172">Click hello **Backup** button.</span></span> <span data-ttu-id="b8e50-173">Attendez que toofinish du processus de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-173">Wait for hello backup process toofinish.</span></span> <span data-ttu-id="b8e50-174">Ensuite, passez trop[étape 6 : supprimer les fichiers de base de données hello](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="b8e50-174">Then, go too[Step 6: Remove hello database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="b8e50-175">tooview hello le statut de tâche de sauvegarde hello, cliquez sur **travaux**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-175">tooview hello status of hello backup job, click **Jobs**.</span></span>

    ![Page de travail des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="b8e50-177">état de Hello du travail de sauvegarde hello apparaît dans hello suivant l’image :</span><span class="sxs-lookup"><span data-stu-id="b8e50-177">hello status of hello backup job appears in hello following image:</span></span>

    ![Page de travail d’Archivages de Recovery Services avec état](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="b8e50-179">Pour une sauvegarde cohérente avec les applications, résolvez les éventuelles erreurs dans le fichier journal de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-179">For an application-consistent backup, address any errors in hello log file.</span></span> <span data-ttu-id="b8e50-180">fichier de journal Hello se trouve dans /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span><span class="sxs-lookup"><span data-stu-id="b8e50-180">hello log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-hello-database-files"></a><span data-ttu-id="b8e50-181">Étape 6 : Supprimer les fichiers de base de données hello</span><span class="sxs-lookup"><span data-stu-id="b8e50-181">Step 6: Remove hello database files</span></span> 
<span data-ttu-id="b8e50-182">Plus loin dans cet article, vous allez apprendre comment tootest hello le processus de récupération.</span><span class="sxs-lookup"><span data-stu-id="b8e50-182">Later in this article, you'll learn how tootest hello recovery process.</span></span> <span data-ttu-id="b8e50-183">Avant de pouvoir tester les processus de récupération hello, vous disposez des fichiers de base de données tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-183">Before you can test hello recovery process, you have tooremove hello database files.</span></span>

1.  <span data-ttu-id="b8e50-184">Supprimer les fichiers de sauvegarde et d’espace disque logique hello :</span><span class="sxs-lookup"><span data-stu-id="b8e50-184">Remove hello tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="b8e50-185">(Facultatif) Arrêtez l’instance Oracle hello :</span><span class="sxs-lookup"><span data-stu-id="b8e50-185">(Optional) Shut down hello Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a><span data-ttu-id="b8e50-186">Restaurer les fichiers de hello supprimé à partir de hello que les coffres de Services de récupération</span><span class="sxs-lookup"><span data-stu-id="b8e50-186">Restore hello deleted files from hello Recovery Services vaults</span></span>
<span data-ttu-id="b8e50-187">toorestore hello supprimé des fichiers, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8e50-187">toorestore hello deleted files, complete hello following steps:</span></span>

1. <span data-ttu-id="b8e50-188">Bonjour portail Azure, recherchez hello *myVault* élément les coffres de Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="b8e50-188">In hello Azure portal, search for hello *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="b8e50-189">Sur hello **vue d’ensemble** panneau, sous **sauvegarde éléments**, sélectionnez nombre hello d’éléments.</span><span class="sxs-lookup"><span data-stu-id="b8e50-189">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Éléments de sauvegarde myVault des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="b8e50-191">Sous **nombre d’éléments de sauvegarde**, sélectionnez le nombre hello d’éléments.</span><span class="sxs-lookup"><span data-stu-id="b8e50-191">Under **BACKUP ITEM COUNT**, select hello number of items.</span></span>

    ![Nombre d’éléments de sauvegarde de machine virtuelle Azure des coffres Recovery Services](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="b8e50-193">Sur hello **myvm1** panneau, cliquez sur **récupération de fichier (version préliminaire)**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-193">On hello **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Capture d’écran de Services de récupération de hello les coffres de page de récupération du fichier](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="b8e50-195">Sur hello **récupération de fichier (version préliminaire)** volet, cliquez sur **télécharger le Script**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-195">On hello **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="b8e50-196">Enregistrez ensuite le fichier tooa dossier hello téléchargement (.sh) sur l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-196">Then, save hello download (.sh) file tooa folder on hello client computer.</span></span>

    ![Options d’enregistrement de fichier de script téléchargé](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="b8e50-198">Copiez hello .sh fichier toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b8e50-198">Copy hello .sh file toohello VM.</span></span>

    <span data-ttu-id="b8e50-199">Hello, l’exemple suivant montre comment vous toouse un toomove de commande de copie sécurisée (scp) hello fichier toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b8e50-199">hello following example shows how you toouse a secure copy (scp) command toomove hello file toohello VM.</span></span> <span data-ttu-id="b8e50-200">Vous pouvez également copier le Presse-papiers de toohello contenu hello, puis coller hello contenu dans un nouveau fichier qui est configuré sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-200">You also can copy hello contents toohello clipboard, and then paste hello contents in a new file that is set up on hello VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b8e50-201">Dans l’exemple suivant de hello, assurez-vous que vous mettez à jour les valeurs d’adresse et le dossier IP hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-201">In hello following example, ensure that you update hello IP address and folder values.</span></span> <span data-ttu-id="b8e50-202">les valeurs Hello doivent mapper toohello dossier où hello est enregistré.</span><span class="sxs-lookup"><span data-stu-id="b8e50-202">hello values must map toohello folder where hello file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="b8e50-203">Modifier le fichier de hello, afin qu’il appartient à la racine de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-203">Change hello file, so that it's owned by hello root.</span></span>

    <span data-ttu-id="b8e50-204">Dans l’exemple suivant de hello, remplacez le fichier de la hello afin qu’il appartient à la racine de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-204">In hello following example, change hello file so that it's owned by hello root.</span></span> <span data-ttu-id="b8e50-205">Modifiez ensuite les autorisations.</span><span class="sxs-lookup"><span data-stu-id="b8e50-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="b8e50-206">Hello suivant montre ce que vous devez voir après avoir exécuté hello précédant le script.</span><span class="sxs-lookup"><span data-stu-id="b8e50-206">hello following example shows what you should see after you run hello preceding script.</span></span> <span data-ttu-id="b8e50-207">Lorsque vous êtes invité à entrer toocontinue, entrez **Y**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-207">When you're prompted toocontinue, enter **Y**.</span></span>

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

7. <span data-ttu-id="b8e50-208">Accès toohello monté volumes est confirmée.</span><span class="sxs-lookup"><span data-stu-id="b8e50-208">Access toohello mounted volumes is confirmed.</span></span>

    <span data-ttu-id="b8e50-209">tooexit, entrez **q**, puis recherchez les volumes hello monté.</span><span class="sxs-lookup"><span data-stu-id="b8e50-209">tooexit, enter **q**, and then search for hello mounted volumes.</span></span> <span data-ttu-id="b8e50-210">toocreate une liste de hello ajoutée de volumes, à l’invite de commandes, entrez **df -k**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-210">toocreate a list of hello added volumes, at a command prompt, enter **df -k**.</span></span>

    ![commande Hello df-k](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="b8e50-212">Hello utilisation suivante du script toocopy hello manquant fichiers toohello arrière dossiers :</span><span class="sxs-lookup"><span data-stu-id="b8e50-212">Use hello following script toocopy hello missing files back toohello folders:</span></span>

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
9. <span data-ttu-id="b8e50-213">Bonjour le script suivant, utiliser de base de données RMAN toorecover hello :</span><span class="sxs-lookup"><span data-stu-id="b8e50-213">In hello following script, use RMAN toorecover hello database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="b8e50-214">Démontez le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-214">Unmount hello disk.</span></span>

    <span data-ttu-id="b8e50-215">Bonjour portail Azure, sur hello **récupération de fichier (version préliminaire)** panneau, cliquez sur **démontage de disques**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-215">In hello Azure portal, on hello **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Commande Démonter les disques](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a><span data-ttu-id="b8e50-217">Restaurer hello machine virtuelle entière</span><span class="sxs-lookup"><span data-stu-id="b8e50-217">Restore hello entire VM</span></span>

<span data-ttu-id="b8e50-218">Au lieu de restaurer les fichiers hello supprimé à partir des archivages de Recovery Services hello, vous pouvez restaurer hello machine virtuelle entière.</span><span class="sxs-lookup"><span data-stu-id="b8e50-218">Instead of restoring hello deleted files from hello Recovery Services vaults, you can restore hello entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="b8e50-219">Étape 1 : Supprimer myVM</span><span class="sxs-lookup"><span data-stu-id="b8e50-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="b8e50-220">Bonjour portail Azure, accédez à toohello **myVM1** coffre et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-220">In hello Azure portal, go toohello **myVM1** vault, and then select **Delete**.</span></span>

    ![Commande Supprimer du coffre](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a><span data-ttu-id="b8e50-222">Étape 2 : Récupération hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b8e50-222">Step 2: Recover hello VM</span></span>

1.  <span data-ttu-id="b8e50-223">Accédez trop**les coffres de Services de récupération**, puis sélectionnez **myVault**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-223">Go too**Recovery Services vaults**, and then select **myVault**.</span></span>

    ![Entrée myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="b8e50-225">Sur hello **vue d’ensemble** panneau, sous **sauvegarde éléments**, sélectionnez nombre hello d’éléments.</span><span class="sxs-lookup"><span data-stu-id="b8e50-225">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Éléments de sauvegarde myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="b8e50-227">Sur hello **des éléments de sauvegarde (Machine virtuelle de Azure)** panneau, sélectionnez **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-227">On hello **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![Page de récupération de machine virtuelle](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="b8e50-229">Sur hello **myvm1** panneau, cliquez sur les points de suspension hello (**...** ) bouton, puis cliquez sur **restaurer la machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-229">On hello **myvm1** blade, click hello ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![Commande Restaurer la machine virtuelle](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="b8e50-231">Sur hello **point de restauration** panneau, sélectionnez hello élément que vous souhaitez toorestore, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-231">On hello **Select restore point** blade, select hello item that you want toorestore, and then click **OK**.</span></span>

    ![Point de restauration hello SELECT](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="b8e50-233">Si vous avez activé la sauvegarde cohérente avec les applications, une barre bleue verticale apparaît.</span><span class="sxs-lookup"><span data-stu-id="b8e50-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="b8e50-234">Sur hello **restaurer la configuration** panneau, nom d’ordinateur virtuel, sélectionnez hello, sélectionnez le groupe de ressources hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-234">On hello **Restore configuration** blade, select hello virtual machine name, select hello resource group, and then click **OK**.</span></span>

    ![Restaurer les valeurs de configuration](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="b8e50-236">toorestore hello machine virtuelle, cliquez sur hello **restaurer** bouton.</span><span class="sxs-lookup"><span data-stu-id="b8e50-236">toorestore hello VM, click hello **Restore** button.</span></span>

8.  <span data-ttu-id="b8e50-237">état de hello tooview hello processus de restauration, cliquez sur **travaux**, puis cliquez sur **des tâches de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-237">tooview hello status of hello restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Commande d’état des travaux de sauvegarde](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="b8e50-239">Hello figure ci-dessous illustre état hello du processus de restauration hello :</span><span class="sxs-lookup"><span data-stu-id="b8e50-239">hello following figure shows hello status of hello restore process:</span></span>

    ![État du processus de restauration hello](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a><span data-ttu-id="b8e50-241">Étape 3 : Définir l’adresse IP publique de hello</span><span class="sxs-lookup"><span data-stu-id="b8e50-241">Step 3: Set hello public IP address</span></span>
<span data-ttu-id="b8e50-242">Après hello que machine virtuelle est restaurée, configurer l’adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-242">After hello VM is restored, set up hello public IP address.</span></span>

1.  <span data-ttu-id="b8e50-243">Dans la zone de recherche de hello, entrez **adresse IP publique**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-243">In hello search box, enter **public IP address**.</span></span>

    ![Liste d’adresses IP publiques](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="b8e50-245">Sur hello **des adresses IP publiques** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-245">On hello **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="b8e50-246">Sur hello **créer une adresse IP publique** panneau, pour **nom**, sélectionnez les nom IP public hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-246">On hello **Create public IP address** blade, for **Name**, select hello public IP name.</span></span> <span data-ttu-id="b8e50-247">Pour **Groupe de ressources**, sélectionnez **Use existing** (Utiliser existant).</span><span class="sxs-lookup"><span data-stu-id="b8e50-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="b8e50-248">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-248">Then, click **Create**.</span></span>

    ![Créer une adresse IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="b8e50-250">tooassociate hello adresse IP publique avec une interface réseau hello hello machine virtuelle, rechercher des et sélectionnez **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-250">tooassociate hello public IP address with hello network interface for hello VM, search for and select **myVMip**.</span></span> <span data-ttu-id="b8e50-251">Cliquez ensuite sur **Associer**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-251">Then, click **Associate**.</span></span>

    ![Associer une adresse IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="b8e50-253">Pour **Type de ressource**, sélectionnez **Interface réseau**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="b8e50-254">Sélectionnez l’interface réseau hello qui est utilisé par l’instance de myVM hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8e50-254">Select hello network interface that is used by hello myVM instance, and then click **OK**.</span></span>

    ![Sélectionner le type de ressource et les valeurs de carte réseau](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="b8e50-256">Recherchez et ouvrez l’instance hello de myVM est déplacée à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="b8e50-256">Search for and open hello instance of myVM that is ported from hello portal.</span></span> <span data-ttu-id="b8e50-257">Hello adresse IP associé à hello machine virtuelle apparaît sur hello myVM **vue d’ensemble** panneau.</span><span class="sxs-lookup"><span data-stu-id="b8e50-257">hello IP address that is associated with hello VM appears on hello myVM **Overview** blade.</span></span>

    ![Valeur d’adresse IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a><span data-ttu-id="b8e50-259">Étape 4 : Connecter toohello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b8e50-259">Step 4: Connect toohello VM</span></span>

*   <span data-ttu-id="b8e50-260">tooconnect toohello machine virtuelle, utilisez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="b8e50-260">tooconnect toohello VM, use hello following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a><span data-ttu-id="b8e50-261">Étape 5 : Tester si la base de données hello est accessible</span><span class="sxs-lookup"><span data-stu-id="b8e50-261">Step 5: Test whether hello database is accessible</span></span>
*   <span data-ttu-id="b8e50-262">tootest accessibilité, hello utilisez script suivant :</span><span class="sxs-lookup"><span data-stu-id="b8e50-262">tootest accessibility, use hello following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b8e50-263">Base de données si hello **démarrage** commande génère une erreur, la base de données toorecover hello, consultez [étape 6 : base de données utilisez RMAN toorecover hello](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="b8e50-263">If hello database **startup** command generates an error, toorecover hello database, see [Step 6: Use RMAN toorecover hello database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a><span data-ttu-id="b8e50-264">Étape 6 : Base de données (facultatif) utilisez RMAN toorecover hello</span><span class="sxs-lookup"><span data-stu-id="b8e50-264">Step 6: (Optional) Use RMAN toorecover hello database</span></span>
*   <span data-ttu-id="b8e50-265">toorecover hello base de données, hello utilisez script suivant :</span><span class="sxs-lookup"><span data-stu-id="b8e50-265">toorecover hello database, use hello following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="b8e50-266">sauvegarde de Hello et la récupération de base de données de 12c de base de données Oracle hello sur une machine virtuelle Linux de Azure est maintenant terminé.</span><span class="sxs-lookup"><span data-stu-id="b8e50-266">hello backup and recovery of hello Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="b8e50-267">Supprimer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b8e50-267">Delete hello VM</span></span>

<span data-ttu-id="b8e50-268">Lorsque vous avez besoin n’est plus hello machine virtuelle, vous pouvez utiliser hello suivant du groupe de ressources de commande tooremove hello, hello machine virtuelle et toutes les ressources :</span><span class="sxs-lookup"><span data-stu-id="b8e50-268">When you no longer need hello VM, you can use hello following command tooremove hello resource group, hello VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b8e50-269">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8e50-269">Next steps</span></span>

[<span data-ttu-id="b8e50-270">Didacticiel : créer des machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="b8e50-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="b8e50-271">Explorer des exemples Azure CLI de déploiement de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b8e50-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)



