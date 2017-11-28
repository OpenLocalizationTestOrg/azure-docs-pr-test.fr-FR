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
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="475f9-103">Créer une base de données Oracle dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="475f9-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="475f9-104">Ce guide décrit en détail à l’aide de hello CLI d’Azure toodeploy une machine virtuelle Azure à partir de hello [image de la galerie de marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) commander toocreate une base de données Oracle 12C.</span><span class="sxs-lookup"><span data-stu-id="475f9-104">This guide details using hello Azure CLI toodeploy an Azure virtual machine from hello [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order toocreate an Oracle 12c database.</span></span> <span data-ttu-id="475f9-105">Une fois que le serveur de hello est déployé, vous vous connectez via une connexion SSH dans la base de données Oracle ordre tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="475f9-105">Once hello server is deployed, you will connect via SSH in order tooconfigure hello Oracle database.</span></span> 

<span data-ttu-id="475f9-106">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="475f9-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="475f9-107">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="475f9-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="475f9-108">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="475f9-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="475f9-109">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="475f9-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="475f9-110">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="475f9-110">Create a resource group</span></span>

<span data-ttu-id="475f9-111">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="475f9-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="475f9-112">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="475f9-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="475f9-113">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="475f9-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="475f9-114">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="475f9-114">Create virtual machine</span></span>

<span data-ttu-id="475f9-115">toocreate un ordinateur virtuel (VM), utilisez hello [az vm créer](/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="475f9-115">toocreate a virtual machine (VM), use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="475f9-116">Hello exemple suivant crée un ordinateur virtuel nommé `myVM`.</span><span class="sxs-lookup"><span data-stu-id="475f9-116">hello following example creates a VM named `myVM`.</span></span> <span data-ttu-id="475f9-117">Il crée également des clés SSH si elles n’existent pas déjà à un emplacement de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="475f9-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="475f9-118">toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="475f9-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="475f9-119">Après avoir créé la machine virtuelle de hello, CLI d’Azure affiche des informations similaires toohello est l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="475f9-119">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="475f9-120">Notez la valeur hello pour `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="475f9-120">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="475f9-121">Vous utilisez cette hello de tooaccess adresse machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="475f9-121">You use this address tooaccess hello VM.</span></span>

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

## <a name="connect-toohello-vm"></a><span data-ttu-id="475f9-122">Se connecter toohello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="475f9-122">Connect toohello VM</span></span>

<span data-ttu-id="475f9-123">toocreate une session SSH avec hello machine virtuelle, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="475f9-123">toocreate an SSH session with hello VM, use hello following command.</span></span> <span data-ttu-id="475f9-124">Remplacer l’adresse IP de hello avec hello `publicIpAddress` valeur pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="475f9-124">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a><span data-ttu-id="475f9-125">Créer la base de données hello</span><span class="sxs-lookup"><span data-stu-id="475f9-125">Create hello database</span></span>

<span data-ttu-id="475f9-126">Hello logiciels Oracle est déjà installé sur une image Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="475f9-126">hello Oracle software is already installed on hello Marketplace image.</span></span> <span data-ttu-id="475f9-127">Créer une base de données comme suit.</span><span class="sxs-lookup"><span data-stu-id="475f9-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="475f9-128">Commutateur toohello *oracle* super utilisateur, puis d’écouteur de hello d’initialisation pour la journalisation :</span><span class="sxs-lookup"><span data-stu-id="475f9-128">Switch toohello *oracle* superuser, then initialize hello listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="475f9-129">sortie de Hello est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="475f9-129">hello output is similar toohello following:</span></span>

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

2.  <span data-ttu-id="475f9-130">Créer la base de données hello :</span><span class="sxs-lookup"><span data-stu-id="475f9-130">Create hello database:</span></span>

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

    <span data-ttu-id="475f9-131">Base de données de quelques minutes toocreate hello nécessaire.</span><span class="sxs-lookup"><span data-stu-id="475f9-131">It takes a few minutes toocreate hello database.</span></span>

3. <span data-ttu-id="475f9-132">Fixer les variables oracle</span><span class="sxs-lookup"><span data-stu-id="475f9-132">Set Oracle variables</span></span>

<span data-ttu-id="475f9-133">Avant de vous connectez, vous devez tooset deux variables d’environnement : *ORACLE_HOME* et *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="475f9-133">Before you connect, you need tooset two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="475f9-134">Vous pouvez également ajouter ORACLE_HOME et ORACLE_SID variables toohello .bashrc le fichier.</span><span class="sxs-lookup"><span data-stu-id="475f9-134">You also can add ORACLE_HOME and ORACLE_SID variables toohello .bashrc file.</span></span> <span data-ttu-id="475f9-135">Cela permet d’enregistrer les variables d’environnement hello pour les connexions futures. Confirmer les éléments suivants de hello instructions ont été ajoutées toohello `~/.bashrc` fichier à l’aide de l’éditeur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="475f9-135">This would save hello environment variables for future sign-ins. Confirm hello following statements have been added toohello `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="475f9-136">Connectivité à Oracle EM Express</span><span class="sxs-lookup"><span data-stu-id="475f9-136">Oracle EM Express connectivity</span></span>

<span data-ttu-id="475f9-137">Pour un outil de gestion de l’interface graphique utilisateur que vous pouvez utiliser la base de données tooexplore hello, définissez Oracle EM Express.</span><span class="sxs-lookup"><span data-stu-id="475f9-137">For a GUI management tool that you can use tooexplore hello database, set up Oracle EM Express.</span></span> <span data-ttu-id="475f9-138">tooconnect tooOracle EM Express, vous devez tout d’abord configurer port hello dans Oracle.</span><span class="sxs-lookup"><span data-stu-id="475f9-138">tooconnect tooOracle EM Express, you must first set up hello port in Oracle.</span></span> 

1. <span data-ttu-id="475f9-139">Se connecter à l’aide de sqlplus de la base de données tooyour :</span><span class="sxs-lookup"><span data-stu-id="475f9-139">Connect tooyour database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="475f9-140">Une fois connecté, définissez le port hello 5502 pour EM Express</span><span class="sxs-lookup"><span data-stu-id="475f9-140">Once connected, set hello port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="475f9-141">Conteneur de hello ouvrir PDB1 si ce n’est pas déjà ouvert, mais tout d’abord vérifier le statut de hello :</span><span class="sxs-lookup"><span data-stu-id="475f9-141">Open hello container PDB1 if not already opened, but first check hello status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="475f9-142">sortie de Hello est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="475f9-142">hello output is similar toohello following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="475f9-143">Si hello OPEN_MODE pour `PDB1` n’est pas de lecture et écriture, puis exécutez les commandes tooopen PDB1 de hello ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="475f9-143">If hello OPEN_MODE for `PDB1` is not READ WRITE, then run hello followings commands tooopen PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="475f9-144">Vous devez tootype `quit` tooend hello sqlplus session et le type `exit` toologout de l’utilisateur d’oracle hello.</span><span class="sxs-lookup"><span data-stu-id="475f9-144">You need tootype `quit` tooend hello sqlplus session and type `exit` toologout of hello oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="475f9-145">Automatisation du démarrage et de l’arrêt de la base de données</span><span class="sxs-lookup"><span data-stu-id="475f9-145">Automate database startup and shutdown</span></span>

<span data-ttu-id="475f9-146">base de données Oracle Hello par défaut ne démarre pas automatiquement lorsque vous redémarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="475f9-146">hello Oracle database by default doesn't automatically start when you restart hello VM.</span></span> <span data-ttu-id="475f9-147">tooset des toostart de base de données Oracle hello automatiquement, tout d’abord vous connecter en tant que racine.</span><span class="sxs-lookup"><span data-stu-id="475f9-147">tooset up hello Oracle database toostart automatically, first sign in as root.</span></span> <span data-ttu-id="475f9-148">Puis, créez et mettez à jour des fichiers système.</span><span class="sxs-lookup"><span data-stu-id="475f9-148">Then, create and update some system files.</span></span>

1. <span data-ttu-id="475f9-149">Connexion en tant qu’utilisateur racine</span><span class="sxs-lookup"><span data-stu-id="475f9-149">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="475f9-150">À l’aide de votre éditeur favori, de modifier le fichier de hello `/etc/oratab` et modifiez la valeur par défaut hello `N` trop`Y`:</span><span class="sxs-lookup"><span data-stu-id="475f9-150">Using your favorite editor, edit hello file `/etc/oratab` and change hello default `N` too`Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="475f9-151">Créez un fichier nommé `/etc/init.d/dbora` et coller hello suivant contenu :</span><span class="sxs-lookup"><span data-stu-id="475f9-151">Create a file named `/etc/init.d/dbora` and paste hello following contents:</span></span>

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

4.  <span data-ttu-id="475f9-152">Modifiez les autorisations des fichiers *chmod* comme suit :</span><span class="sxs-lookup"><span data-stu-id="475f9-152">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="475f9-153">Créez des liens symboliques pour le démarrage et l’arrêt, comme suit :</span><span class="sxs-lookup"><span data-stu-id="475f9-153">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="475f9-154">tootest vos modifications, redémarrez hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="475f9-154">tootest your changes, restart hello VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="475f9-155">Ouverture des ports pour la connectivité</span><span class="sxs-lookup"><span data-stu-id="475f9-155">Open ports for connectivity</span></span>

<span data-ttu-id="475f9-156">tâche finale Hello est tooconfigure certains points de terminaison externes.</span><span class="sxs-lookup"><span data-stu-id="475f9-156">hello final task is tooconfigure some external endpoints.</span></span> <span data-ttu-id="475f9-157">tooset des hello du groupe de sécurité réseau Azure qui protège hello machine virtuelle, tout d’abord fermer votre session SSH Bonjour VM (doit avoir été exclu SSH lors du redémarrage de l’étape précédente).</span><span class="sxs-lookup"><span data-stu-id="475f9-157">tooset up hello Azure Network Security Group that protects hello VM, first exit your SSH session in hello VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="475f9-158">point de terminaison hello tooopen que vous utilisez base de données Oracle tooaccess hello à distance, créez une règle de groupe de sécurité réseau avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) comme suit :</span><span class="sxs-lookup"><span data-stu-id="475f9-158">tooopen hello endpoint that you use tooaccess hello Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="475f9-159">point de terminaison hello tooopen que vous utilisez tooaccess Oracle EM Express à distance, créez une règle de groupe de sécurité réseau avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) comme suit :</span><span class="sxs-lookup"><span data-stu-id="475f9-159">tooopen hello endpoint that you use tooaccess Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="475f9-160">Si nécessaire, obtenir hello adresse IP publique de votre machine virtuelle à l’aide de [az réseau public-ip afficher](/cli/azure/network/public-ip#show) comme suit :</span><span class="sxs-lookup"><span data-stu-id="475f9-160">If needed, obtain hello public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="475f9-161">Connectez-vous à EM Express à partir de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="475f9-161">Connect EM Express from your browser.</span></span> <span data-ttu-id="475f9-162">Assurez-vous que votre navigateur est compatible avec EM Express (l’installation de Flash est requise) :</span><span class="sxs-lookup"><span data-stu-id="475f9-162">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="475f9-163">Vous pouvez vous connecter à l’aide de hello **SYS** de compte, puis activez les hello **tant que sysdba** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="475f9-163">You can log in by using hello **SYS** account, and check hello **as sysdba** checkbox.</span></span> <span data-ttu-id="475f9-164">Mot de passe utilisation hello **OraPasswd1** que vous définissez lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="475f9-164">Use hello password **OraPasswd1** that you set during installation.</span></span> 

![Capture d’écran de la page de connexion Oracle OEM Express hello](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="475f9-166">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="475f9-166">Clean up resources</span></span>

<span data-ttu-id="475f9-167">Une fois que vous avez terminé d’exploration de votre première base de données Oracle sur Azure et hello VM n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, machine virtuelle et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="475f9-167">Once you have finished exploring your first Oracle database on Azure and hello VM is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="475f9-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="475f9-168">Next steps</span></span>

<span data-ttu-id="475f9-169">En savoir plus sur les autres [solutions Oracle sur Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="475f9-169">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="475f9-170">Essayez de hello [installation et configuration d’Oracle Automated Storage Management](configure-oracle-asm.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="475f9-170">Try hello [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>
