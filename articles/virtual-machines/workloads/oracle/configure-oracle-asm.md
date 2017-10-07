---
title: "aaaSet d’Oracle ASM sur une machine virtuelle de Azure Linux | Documents Microsoft"
description: "Rendez Oracle ASM opérationnel rapidement dans votre environnement Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="c464c-103">Configurer Oracle ASM sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="c464c-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="c464c-104">Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible.</span><span class="sxs-lookup"><span data-stu-id="c464c-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="c464c-105">Ce didacticiel décrit le déploiement de base de machine virtuelle Azure combiné avec l’installation de hello et la configuration d’Oracle Automated Storage Management (ASM).</span><span class="sxs-lookup"><span data-stu-id="c464c-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="c464c-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c464c-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c464c-107">Créer et connecter tooan machine virtuelle de base de données Oracle</span><span class="sxs-lookup"><span data-stu-id="c464c-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="c464c-108">Installer et configurer Oracle Automated Storage Management</span><span class="sxs-lookup"><span data-stu-id="c464c-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="c464c-109">Installer et configurer Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="c464c-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="c464c-110">Initialiser une installation Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="c464c-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="c464c-111">Créer une base de données Oracle gérée par ASM</span><span class="sxs-lookup"><span data-stu-id="c464c-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c464c-112">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c464c-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c464c-113">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c464c-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c464c-114">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c464c-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="c464c-115">Préparer l’environnement de hello</span><span class="sxs-lookup"><span data-stu-id="c464c-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="c464c-116">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="c464c-116">Create a resource group</span></span>

<span data-ttu-id="c464c-117">toocreate un groupe de ressources, utilisez hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="c464c-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c464c-118">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="c464c-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="c464c-119">Dans cet exemple, un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* région.</span><span class="sxs-lookup"><span data-stu-id="c464c-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="c464c-120">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c464c-120">Create a VM</span></span>

<span data-ttu-id="c464c-121">toocreate un ordinateur virtuel basé sur l’image de base de données Oracle hello et configurez-le toouse Oracle ASM, utilisez hello [az vm créer](/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="c464c-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="c464c-122">Hello exemple suivant crée un ordinateur virtuel nommé myVM qui a une taille Standard_DS2_v2 avec quatre disques de données associés de 50 Go.</span><span class="sxs-lookup"><span data-stu-id="c464c-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="c464c-123">Si elles n’existent pas déjà dans l’emplacement de la clé hello par défaut, il crée également des clés SSH.</span><span class="sxs-lookup"><span data-stu-id="c464c-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="c464c-124">toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="c464c-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="c464c-125">Après avoir créé la machine virtuelle de hello, CLI d’Azure affiche des informations similaires toohello est l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c464c-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="c464c-126">Notez la valeur hello pour `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="c464c-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="c464c-127">Vous utilisez cette hello de tooaccess adresse machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c464c-127">You use this address tooaccess hello VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a><span data-ttu-id="c464c-128">Se connecter toohello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c464c-128">Connect toohello VM</span></span>

<span data-ttu-id="c464c-129">toocreate une session SSH avec hello de machine virtuelle et configurer des paramètres supplémentaires, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="c464c-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="c464c-130">Remplacer l’adresse IP de hello avec hello `publicIpAddress` valeur pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c464c-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="c464c-131">Installer Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="c464c-131">Install Oracle ASM</span></span>

<span data-ttu-id="c464c-132">tooinstall Oracle ASM, hello complète comme suit.</span><span class="sxs-lookup"><span data-stu-id="c464c-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="c464c-133">Pour plus d’informations sur l’installation d’Oracle ASM, consultez [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span><span class="sxs-lookup"><span data-stu-id="c464c-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="c464c-134">Vous devez toologin en tant que racine dans toocontinue d’ordre d’installation de ASM :</span><span class="sxs-lookup"><span data-stu-id="c464c-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="c464c-135">Exécutez ces commandes supplémentaires des composants Oracle ASM tooinstall :</span><span class="sxs-lookup"><span data-stu-id="c464c-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="c464c-136">Vérifiez qu’Oracle ASM est installé :</span><span class="sxs-lookup"><span data-stu-id="c464c-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="c464c-137">sortie Hello de cette commande doit répertorier hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="c464c-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="c464c-138">ASM requiert des utilisateurs spécifiques et les rôles dans l’ordre toofunction correctement.</span><span class="sxs-lookup"><span data-stu-id="c464c-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="c464c-139">Hello suivant les commandes créer des groupes et comptes d’utilisateur requis hello :</span><span class="sxs-lookup"><span data-stu-id="c464c-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="c464c-140">Vérifiez que les utilisateurs et les groupes ont été créés correctement :</span><span class="sxs-lookup"><span data-stu-id="c464c-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="c464c-141">Hello sortie de cette commande doit répertorier les suivant hello utilisateurs et groupes :</span><span class="sxs-lookup"><span data-stu-id="c464c-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="c464c-142">Créez un dossier pour l’utilisateur *grille* et changer le propriétaire de hello :</span><span class="sxs-lookup"><span data-stu-id="c464c-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="c464c-143">Configurer Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="c464c-143">Set up Oracle ASM</span></span>

<span data-ttu-id="c464c-144">Pour ce didacticiel, hello utilisateur par défaut est *grille* et le groupe par défaut hello est *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="c464c-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="c464c-145">Vérifiez que hello *oracle* utilisateur fait partie du groupe d’asmadmin hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="c464c-146">tooset votre installation Oracle ASM, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="c464c-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="c464c-147">Configuration d’un pilote de bibliothèque Oracle ASM hello implique la définition d’utilisateur par défaut de hello (grille) et le groupe par défaut (asmadmin), ainsi que la configuration hello lecteur toostart au démarrage du système (choisissez y) et tooscan de disques de démarrage (choisissez y).</span><span class="sxs-lookup"><span data-stu-id="c464c-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="c464c-148">Vous avez besoin d’invites de hello tooanswer de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c464c-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="c464c-149">sortie Hello de cette commande doit se présenter comme toohello suivant, l’arrêt avec toobe invites ayant obtenu une réponse.</span><span class="sxs-lookup"><span data-stu-id="c464c-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="c464c-150">Afficher la configuration disque hello :</span><span class="sxs-lookup"><span data-stu-id="c464c-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="c464c-151">sortie Hello de cette commande doit ressembler similaire toohello suivant de la liste des disques disponibles</span><span class="sxs-lookup"><span data-stu-id="c464c-151">hello output of this command should look similar toohello following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="c464c-152">Disque au format *sdc/dev/* en exécutant hello commande suivante et répondre aux hello invite avec :</span><span class="sxs-lookup"><span data-stu-id="c464c-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="c464c-153">*n* pour la nouvelle partition</span><span class="sxs-lookup"><span data-stu-id="c464c-153">*n* for new partition</span></span>
   - <span data-ttu-id="c464c-154">*p* pour la partition principale</span><span class="sxs-lookup"><span data-stu-id="c464c-154">*p* for primary partition</span></span>
   - <span data-ttu-id="c464c-155">*1* première partition de hello tooselect</span><span class="sxs-lookup"><span data-stu-id="c464c-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="c464c-156">Appuyez sur `enter` pour le premier cylindre de hello par défaut</span><span class="sxs-lookup"><span data-stu-id="c464c-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="c464c-157">Appuyez sur `enter` pour le dernier cylindre de hello par défaut</span><span class="sxs-lookup"><span data-stu-id="c464c-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="c464c-158">Appuyez sur *w* table de partition toowrite hello modifications toohello</span><span class="sxs-lookup"><span data-stu-id="c464c-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="c464c-159">Réponses hello fournis ci-dessus, sortie hello pour la commande de fdisk hello doit ressembler à celle de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="c464c-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="c464c-160">Répétition hello précédant la commande fdisk pour `/dev/sdd`, `/dev/sde`, et `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="c464c-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="c464c-161">Vérifier la configuration de disque hello :</span><span class="sxs-lookup"><span data-stu-id="c464c-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="c464c-162">sortie Hello de commande hello doit ressembler à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="c464c-162">hello output of hello command should look like hello following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="c464c-163">Vérifiez l’état du service Oracle ASM hello et démarrer le service Oracle ASM hello :</span><span class="sxs-lookup"><span data-stu-id="c464c-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="c464c-164">sortie Hello de commande hello doit ressembler à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="c464c-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="c464c-165">Créez les disques Oracle ASM :</span><span class="sxs-lookup"><span data-stu-id="c464c-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="c464c-166">sortie Hello de commande hello doit ressembler à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="c464c-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="c464c-167">Répertoriez les disques Oracle ASM :</span><span class="sxs-lookup"><span data-stu-id="c464c-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="c464c-168">sortie Hello de commande hello doit répertorier off hello Oracle ASM disques suivants :</span><span class="sxs-lookup"><span data-stu-id="c464c-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="c464c-169">Modifier les mots de passe hello pour les utilisateurs racine, oracle et grille hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="c464c-170">**Prenez note de ces nouveaux mots de passe** comme vous les utilisez plus tard pendant l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="c464c-171">Modifier les autorisations de dossier hello :</span><span class="sxs-lookup"><span data-stu-id="c464c-171">Change hello folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="c464c-172">Télécharger et préparer Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="c464c-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="c464c-173">toodownload et préparer des logiciels d’Infrastructure de grille Oracle hello, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="c464c-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="c464c-174">Télécharger l’Infrastructure de grille Oracle à partir de hello [page de téléchargement Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="c464c-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="c464c-175">Sous Télécharger hello intitulée **Oracle Database 12C version 1 grille Infrastructure (12.1.0.2.0) pour Linux x86-64**, téléchargez les fichiers .zip hello deux.</span><span class="sxs-lookup"><span data-stu-id="c464c-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="c464c-176">Après avoir téléchargé hello .zip fichiers tooyour client ordinateur, vous pouvez utiliser Secure copie Protocol (SCP) toocopy hello fichiers tooyour machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="c464c-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="c464c-177">SSH précédent dans votre machine virtuelle d’Oracle dans Azure dans les fichiers de commande toomove hello .zip dans hello / opt dossier.</span><span class="sxs-lookup"><span data-stu-id="c464c-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="c464c-178">Ensuite, modifiez le propriétaire hello des fichiers de hello :</span><span class="sxs-lookup"><span data-stu-id="c464c-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="c464c-179">Décompressez les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-179">Unzip hello files.</span></span> <span data-ttu-id="c464c-180">(Installation hello Linux décompressez outil s’il n’est pas déjà installé).</span><span class="sxs-lookup"><span data-stu-id="c464c-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="c464c-181">Changez l’autorisation :</span><span class="sxs-lookup"><span data-stu-id="c464c-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="c464c-182">Mettez à jour l’espace d’échange configuré.</span><span class="sxs-lookup"><span data-stu-id="c464c-182">Update configured swap space.</span></span> <span data-ttu-id="c464c-183">Les composants de grille Oracle doivent au moins 6,8 Go d’espace de permutation tooinstall grille.</span><span class="sxs-lookup"><span data-stu-id="c464c-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="c464c-184">taille de fichier d’échange Hello par défaut pour les images Oracle Linux dans Azure est uniquement 2 048 Mo.</span><span class="sxs-lookup"><span data-stu-id="c464c-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="c464c-185">Vous devez tooincrease `ResourceDisk.SwapSizeMB` Bonjour `/etc/waagent.conf` de fichiers et de redémarrer hello WALinuxAgent service pour effet de tootake hello mis à jour les paramètres.</span><span class="sxs-lookup"><span data-stu-id="c464c-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="c464c-186">S’agissant d’un fichier en lecture seule, vous avez besoin d’autorisations fichier toochange tooenable un accès en écriture.</span><span class="sxs-lookup"><span data-stu-id="c464c-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="c464c-187">Recherchez `ResourceDisk.SwapSizeMB` et également de modifier la valeur de hello**8192**.</span><span class="sxs-lookup"><span data-stu-id="c464c-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="c464c-188">Vous devez toopress `insert` tooenter en mode d’insertion, le type de valeur hello de **8192** , puis appuyez sur `esc` tooreturn toocommand mode.</span><span class="sxs-lookup"><span data-stu-id="c464c-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="c464c-189">modifications de hello toowrite et quittez hello, type de fichier `:wq` et appuyez sur `enter`.</span><span class="sxs-lookup"><span data-stu-id="c464c-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c464c-190">Il est vivement recommandé de toujours utiliser `WALinuxAgent` tooconfigure espace d’échange afin qu’il est toujours créé sur hello local éphémère disque temporaire pour de meilleures performances.</span><span class="sxs-lookup"><span data-stu-id="c464c-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="c464c-191">Pour plus d’informations, consultez [comment tooadd un échange de fichiers dans des machines virtuelles Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="c464c-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="c464c-192">Préparer votre client local et la machine virtuelle toorun x11</span><span class="sxs-lookup"><span data-stu-id="c464c-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="c464c-193">Configuration d’Oracle ASM nécessite une interface graphique toocomplete hello installation et la configuration.</span><span class="sxs-lookup"><span data-stu-id="c464c-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="c464c-194">Nous utilisons hello x11 protocole toofacilitate cette installation.</span><span class="sxs-lookup"><span data-stu-id="c464c-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="c464c-195">Si vous utilisez un système client (Mac ou Linux) qui a déjà X11 fonctionnalités activé et configuré - vous pouvez ignorer cette configuration et le programme d’installation tooWindows exclusif machines.</span><span class="sxs-lookup"><span data-stu-id="c464c-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="c464c-196">[Télécharger PuTTY](http://www.putty.org/) et [télécharger Xming](https://xming.en.softonic.com/) tooyour l’ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="c464c-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="c464c-197">Installation vous devez toocomplete hello de ces deux applications hello valeurs par défaut avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="c464c-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="c464c-198">Après avoir installé PuTTY, ouvrez une invite de commandes en hello PuTTY dossier (par exemple, C:\Program Files\PuTTY) et modifier `puttygen.exe` commander toogenerate une clé.</span><span class="sxs-lookup"><span data-stu-id="c464c-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="c464c-199">Dans PuTTY Key Generator :</span><span class="sxs-lookup"><span data-stu-id="c464c-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="c464c-200">Générer une clé en sélectionnant hello `Generate` bouton.</span><span class="sxs-lookup"><span data-stu-id="c464c-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="c464c-201">Copier le contenu de hello de clé de hello (Ctrl + C).</span><span class="sxs-lookup"><span data-stu-id="c464c-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="c464c-202">Sélectionnez hello `Save private key` bouton.</span><span class="sxs-lookup"><span data-stu-id="c464c-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="c464c-203">Ignorer l’avertissement hello sur la sécurisation de clé hello avec un mot de passe, puis sélectionnez `OK`.</span><span class="sxs-lookup"><span data-stu-id="c464c-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![Capture d’écran du générateur de clé PuTTY](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="c464c-205">Dans votre machine virtuelle, exécutez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="c464c-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="c464c-206">Créez un fichier appelé `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="c464c-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="c464c-207">Collez le contenu hello de clé de hello dans ce fichier, puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c464c-208">clé de Hello doit contenir la chaîne de hello `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="c464c-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="c464c-209">En outre, le contenu hello de clé de hello doit être une seule ligne de texte.</span><span class="sxs-lookup"><span data-stu-id="c464c-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="c464c-210">Sur votre système client, démarrez PuTTY.</span><span class="sxs-lookup"><span data-stu-id="c464c-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="c464c-211">Bonjour **catégorie** volet, accédez trop**connexion** > **SSH** > **Auth**. Bonjour **fichier de clé privée pour l’authentification** , naviguez jusque toohello clé que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c464c-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Capture d’écran des options d’authentification SSH hello](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="c464c-213">Bonjour **catégorie** volet, accédez trop**connexion** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="c464c-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="c464c-214">Sélectionnez hello **X11 d’activer le transfert** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c464c-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![Capture d’écran de hello SSH X11 options de transfert](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="c464c-216">Bonjour **catégorie** volet, accédez trop**Session**.</span><span class="sxs-lookup"><span data-stu-id="c464c-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="c464c-217">Entrez votre machine virtuelle ASM de Oracle `<publicIPaddress>` dans la boîte de dialogue Nom hôte hello renseigner un nouvel `Saved Session` nom, puis cliquez sur `Save`.</span><span class="sxs-lookup"><span data-stu-id="c464c-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="c464c-218">Une fois enregistré, cliquez sur `open` tooconnect tooyour Oracle ASM virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c464c-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="c464c-219">Hello première connexion, vous recevez un avertissement système à distance de hello n’est pas mis en cache dans le Registre.</span><span class="sxs-lookup"><span data-stu-id="c464c-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="c464c-220">Cliquez sur `yes` tooadd il et continuer.</span><span class="sxs-lookup"><span data-stu-id="c464c-220">Click on `yes` tooadd it and continue.</span></span>

   ![Capture d’écran des options de session PuTTY hello](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="c464c-222">Installer Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="c464c-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="c464c-223">tooinstall Infrastructure de grille Oracle, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="c464c-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="c464c-224">Connectez-vous en tant que **grid**.</span><span class="sxs-lookup"><span data-stu-id="c464c-224">Sign in as **grid**.</span></span> <span data-ttu-id="c464c-225">(Vous devez être en mesure de toosign dans sans être invité à entrer un mot de passe.)</span><span class="sxs-lookup"><span data-stu-id="c464c-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="c464c-226">Si vous exécutez Windows, assurez-vous que vous avez démarré Xming avant de commencer l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="c464c-227">Le programme d’installation d’Oracle Grid Infrastructure 12c Release 1 s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c464c-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="c464c-228">(Il peut prendre quelques minutes pour toostart du programme d’installation hello.)</span><span class="sxs-lookup"><span data-stu-id="c464c-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="c464c-229">Sur hello **sélectionner l’Option Installation** , sélectionnez **installez et configurez l’Infrastructure de grille Oracle pour un serveur autonome**.</span><span class="sxs-lookup"><span data-stu-id="c464c-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Capture d’écran de la page de sélectionner l’Option Installation hello du programme d’installation](./media/oracle-asm/install01.png)

3. <span data-ttu-id="c464c-231">Sur hello **sélectionner les langues de produits** , vérifiez **anglais** ou langue hello de votre choix est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c464c-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="c464c-232">Cliquez sur `next`.</span><span class="sxs-lookup"><span data-stu-id="c464c-232">Click `next`.</span></span>

4. <span data-ttu-id="c464c-233">Sur hello **créer un groupe de disques ASM** page :</span><span class="sxs-lookup"><span data-stu-id="c464c-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="c464c-234">Entrez un nom pour le groupe de disques hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="c464c-235">Sous **Redundancy** (Redondance), sélectionnez **External** (Externe).</span><span class="sxs-lookup"><span data-stu-id="c464c-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="c464c-236">Sous **Allocation Unit Size** (Taille d’unité d’allocation), sélectionnez **4**.</span><span class="sxs-lookup"><span data-stu-id="c464c-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="c464c-237">Sous **Add Disks** (Ajouter des disques), sélectionnez **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="c464c-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="c464c-238">Cliquez sur `next`.</span><span class="sxs-lookup"><span data-stu-id="c464c-238">Click `next`.</span></span>

5. <span data-ttu-id="c464c-239">Sur hello **spécifier le mot de passe ASM** page, sélectionnez hello **utiliser les mêmes mots de passe pour ces comptes** , puis entrez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c464c-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Capture d’écran de la page de spécifier le mot de passe ASM hello du programme d’installation](./media/oracle-asm/install04.png)

6. <span data-ttu-id="c464c-241">Sur hello **spécifier les Options de gestion** page, vous avez hello option tooconfigure EM Cloud contrôle.</span><span class="sxs-lookup"><span data-stu-id="c464c-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="c464c-242">Cette option est ignorée, cliquez `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c464c-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="c464c-243">Sur hello **groupes privilégiés de système d’exploitation** page, les paramètres par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="c464c-244">Cliquez sur `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c464c-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="c464c-245">Sur hello **spécifier l’emplacement d’Installation** page, les paramètres par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="c464c-246">Cliquez sur `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c464c-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="c464c-247">Sur hello **créer un inventaire** , changez hello inventaire active trop`/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="c464c-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="c464c-248">Cliquez sur `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c464c-248">Click `next` toocontinue.</span></span>

   ![Capture d’écran de la page Créer un inventaire de hello du programme d’installation](./media/oracle-asm/install08.png)

10. <span data-ttu-id="c464c-250">Sur hello **configuration de l’exécution de script racine** page, sélectionnez hello **exécuter automatiquement les scripts de configuration** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c464c-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="c464c-251">Ensuite, sélectionnez hello **utiliser les informations d’identification utilisateur de « root »** , puis entrez le mot de passe utilisateur hello racine.</span><span class="sxs-lookup"><span data-stu-id="c464c-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Capture d’écran de la page de configuration de l’exécution du programme d’installation hello racine script](./media/oracle-asm/install09.png)

11. <span data-ttu-id="c464c-253">Sur hello **effectuer Prerequisite Checks** la page, le programme d’installation en cours de hello échouera avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="c464c-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="c464c-254">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="c464c-254">This is an expected behavior.</span></span> <span data-ttu-id="c464c-255">Sélectionnez `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="c464c-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="c464c-256">Bonjour **Script de correction** boîte de dialogue, cliquez sur `OK`.</span><span class="sxs-lookup"><span data-stu-id="c464c-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="c464c-257">Sur hello **Résumé** page, passez en revue les paramètres sélectionnés, puis cliquez sur `Install`.</span><span class="sxs-lookup"><span data-stu-id="c464c-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Capture d’écran de la page de résumé hello du programme d’installation](./media/oracle-asm/install12.png)

14. <span data-ttu-id="c464c-259">Une boîte de dialogue d’avertissement s’affiche pour signaler les scripts de configuration vous devez toobe exécuter en tant qu’un utilisateur doté de privilèges.</span><span class="sxs-lookup"><span data-stu-id="c464c-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="c464c-260">Cliquez sur `Yes` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c464c-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="c464c-261">Sur hello **Terminer** , cliquez sur `Close` installation de hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="c464c-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="c464c-262">Configurer votre installation Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="c464c-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="c464c-263">tooset votre installation Oracle ASM, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="c464c-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="c464c-264">Vérifiez que vous êtes toujours connecté en tant que **grid** à partir de votre session X11.</span><span class="sxs-lookup"><span data-stu-id="c464c-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="c464c-265">Vous devrez peut-être toohit `enter` hello toorevive Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="c464c-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="c464c-266">Puis lancez hello Oracle automatisée stockage gestion Assistant de Configuration :</span><span class="sxs-lookup"><span data-stu-id="c464c-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="c464c-267">L’Assistant de configuration d’Oracle ASM s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c464c-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="c464c-268">Bonjour **configurer un ASM : groupes de disques** boîte de dialogue, cliquez sur hello `Create` bouton, puis cliquez sur `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="c464c-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="c464c-269">Bonjour **créer un groupe de disques** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="c464c-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="c464c-270">Entrez le nom du groupe hello disque **données**.</span><span class="sxs-lookup"><span data-stu-id="c464c-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="c464c-271">Sous **Select Member Disks** (Sélectionner les disques membres), sélectionnez **ORCL_DATA** et **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="c464c-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="c464c-272">Sous **Allocation Unit Size** (Taille d’unité d’allocation), sélectionnez **4**.</span><span class="sxs-lookup"><span data-stu-id="c464c-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="c464c-273">Cliquez sur `ok` le groupe de disques toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="c464c-274">Cliquez sur `ok` fenêtre de confirmation tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Capture d’écran de la boîte de dialogue Créer un groupe de disques hello](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="c464c-276">Bonjour **configurer un ASM : groupes de disques** boîte de dialogue, cliquez sur hello `Create` bouton, puis cliquez sur `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="c464c-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="c464c-277">Bonjour **créer un groupe de disques** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="c464c-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="c464c-278">Entrez le nom du groupe hello disque **FRA**.</span><span class="sxs-lookup"><span data-stu-id="c464c-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="c464c-279">Sous **Redundancy** (Redondance), sélectionnez **External (none)** (Externe (aucun)).</span><span class="sxs-lookup"><span data-stu-id="c464c-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="c464c-280">Sous **Select Member Disks** (Sélectionner les disques membres), sélectionnez **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="c464c-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="c464c-281">Sous **Allocation Unit Size** (Taille d’unité d’allocation), sélectionnez **4**.</span><span class="sxs-lookup"><span data-stu-id="c464c-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="c464c-282">Cliquez sur `ok` le groupe de disques toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="c464c-283">Cliquez sur `ok` fenêtre de confirmation tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Capture d’écran de la boîte de dialogue Créer un groupe de disques hello](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="c464c-285">Sélectionnez **Exit** tooclose ASM l’Assistant Configuration.</span><span class="sxs-lookup"><span data-stu-id="c464c-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![Capture d’écran de hello ASM de configurer : boîte de dialogue de groupes de disques avec le bouton Quitter](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="c464c-287">Créer la base de données hello</span><span class="sxs-lookup"><span data-stu-id="c464c-287">Create hello database</span></span>

<span data-ttu-id="c464c-288">Hello logiciel de base de données Oracle est déjà installé sur l’image d’Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="c464c-289">toocreate une base de données, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="c464c-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="c464c-290">Basculez superutilisateur de Oracle toohello utilisateurs et puis initialisez écouteur hello pour l’enregistrement :</span><span class="sxs-lookup"><span data-stu-id="c464c-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="c464c-291">L’Assistant de configuration de base de données s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c464c-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="c464c-292">Sur hello **opération de base de données** , cliquez sur `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="c464c-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="c464c-293">Sur hello **Mode de création de** page :</span><span class="sxs-lookup"><span data-stu-id="c464c-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="c464c-294">Entrez un nom pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="c464c-295">Pour **Storage Type** (Type de stockage), assurez-vous que l’option **Automatic Storage Management (ASM)** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="c464c-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="c464c-296">Pour **emplacement des fichiers de base de données**, utiliser la valeur par défaut hello ASM suggéré emplacement.</span><span class="sxs-lookup"><span data-stu-id="c464c-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="c464c-297">Pour **zone de récupération rapide**, utiliser la valeur par défaut hello ASM suggéré emplacement.</span><span class="sxs-lookup"><span data-stu-id="c464c-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="c464c-298">Saisissez un **mot de passe administrateur** et **confirmez le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c464c-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="c464c-299">Vérifiez que l’option `create as container database` est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="c464c-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="c464c-300">Saisissez une valeur pour `pluggable database name`.</span><span class="sxs-lookup"><span data-stu-id="c464c-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="c464c-301">Sur hello **Résumé** page, passez en revue les paramètres sélectionnés, puis cliquez sur `Finish` base de données toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Capture d’écran de la page de résumé hello](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="c464c-303">Hello de base de données a été créé.</span><span class="sxs-lookup"><span data-stu-id="c464c-303">hello Database has been created.</span></span> <span data-ttu-id="c464c-304">Sur hello **Terminer** page, vous avez hello option toounlock des comptes supplémentaires toouse cette base de données et modifier les mots de passe hello.</span><span class="sxs-lookup"><span data-stu-id="c464c-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="c464c-305">Si vous souhaitez donc toodo, sélectionnez **gestion de mot de passe** -Cliquez sinon sur `close`.</span><span class="sxs-lookup"><span data-stu-id="c464c-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="c464c-306">Supprimer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c464c-306">Delete hello VM</span></span>

<span data-ttu-id="c464c-307">Vous avez correctement configuré la gestion du stockage automatisé Oracle sur l’image de base de données Oracle hello de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c464c-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="c464c-308">Lorsque vous ne devez plus cet ordinateur virtuel, vous pouvez utiliser hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources :</span><span class="sxs-lookup"><span data-stu-id="c464c-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c464c-309">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c464c-309">Next steps</span></span>

[<span data-ttu-id="c464c-310">Didacticiel : Configurer Oracle DataGuard</span><span class="sxs-lookup"><span data-stu-id="c464c-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="c464c-311">Didacticiel : Configurer Oracle GoldenGate</span><span class="sxs-lookup"><span data-stu-id="c464c-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="c464c-312">Revoir [Créer l’architecture d’une base de données Oracle](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="c464c-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>
