---
title: Configurer Oracle ASM sur une machine virtuelle Linux Azure | Microsoft Docs
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
ms.openlocfilehash: 117212a2e7e3da7c3e249798eec804a652e0ef58
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="554de-103">Configurer Oracle ASM sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="554de-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="554de-104">Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible.</span><span class="sxs-lookup"><span data-stu-id="554de-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="554de-105">Ce didacticiel décrit le déploiement de base d’une machine virtuelle Azure associé à l’installation et à la configuration d’Oracle Automated Storage Management (ASM).</span><span class="sxs-lookup"><span data-stu-id="554de-105">This tutorial covers basic Azure virtual machine deployment combined with the installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="554de-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="554de-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="554de-107">Créer une machine virtuelle Oracle Database et s’y connecter</span><span class="sxs-lookup"><span data-stu-id="554de-107">Create and connect to an Oracle Database VM</span></span>
> * <span data-ttu-id="554de-108">Installer et configurer Oracle Automated Storage Management</span><span class="sxs-lookup"><span data-stu-id="554de-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="554de-109">Installer et configurer Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="554de-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="554de-110">Initialiser une installation Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="554de-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="554de-111">Créer une base de données Oracle gérée par ASM</span><span class="sxs-lookup"><span data-stu-id="554de-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="554de-112">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="554de-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="554de-113">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="554de-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="554de-114">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="554de-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-the-environment"></a><span data-ttu-id="554de-115">Préparer l’environnement</span><span class="sxs-lookup"><span data-stu-id="554de-115">Prepare the environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="554de-116">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="554de-116">Create a resource group</span></span>

<span data-ttu-id="554de-117">Pour créer un groupe de ressources, utilisez la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="554de-117">To create a resource group, use the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="554de-118">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="554de-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="554de-119">Dans cet exemple, un groupe de ressources nommé *myResourceGroup* est créé dans la région *eastus*.</span><span class="sxs-lookup"><span data-stu-id="554de-119">In this example, a resource group named *myResourceGroup* in the *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="554de-120">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="554de-120">Create a VM</span></span>

<span data-ttu-id="554de-121">Pour créer une machine virtuelle basée sur l’image d’Oracle Database et la configurer pour utiliser Oracle ASM, exécutez la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="554de-121">To create a virtual machine based on the Oracle Database image and configure it to use Oracle ASM, use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="554de-122">L’exemple suivant crée une machine virtuelle nommée myVM qui a une taille Standard_DS2_v2 avec quatre disques de données associés de 50 Go.</span><span class="sxs-lookup"><span data-stu-id="554de-122">The following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="554de-123">Il crée également des clés SSH si elles n’existent pas encore à un emplacement de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="554de-123">If they do not already exist in the default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="554de-124">Pour utiliser un ensemble spécifique de clés, utilisez l’option `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="554de-124">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="554de-125">Une fois que vous avez créé la machine virtuelle, Azure CLI affiche des informations similaires à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="554de-125">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="554de-126">Notez la valeur pour `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="554de-126">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="554de-127">Vous utilisez cette adresse pour accéder à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="554de-127">You use this address to access the VM.</span></span>

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

### <a name="connect-to-the-vm"></a><span data-ttu-id="554de-128">Connexion à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="554de-128">Connect to the VM</span></span>

<span data-ttu-id="554de-129">Pour créer une session SSH avec la machine virtuelle et configurer des paramètres supplémentaires, utilisez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="554de-129">To create an SSH session with the VM and configure additional settings, use the following command.</span></span> <span data-ttu-id="554de-130">Remplacez l’adresse IP par la valeur de `publicIpAddress` pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="554de-130">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="554de-131">Installer Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="554de-131">Install Oracle ASM</span></span>

<span data-ttu-id="554de-132">Pour installer Oracle ASM, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="554de-132">To install Oracle ASM, complete the following steps.</span></span> 

<span data-ttu-id="554de-133">Pour plus d’informations sur l’installation d’Oracle ASM, consultez [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span><span class="sxs-lookup"><span data-stu-id="554de-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="554de-134">Vous devez ouvrir une session en tant qu’utilisateur ROOT afin de poursuivre l’installation d’ASM :</span><span class="sxs-lookup"><span data-stu-id="554de-134">You need to login as root in order to continue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="554de-135">Exécutez ces commandes supplémentaires pour installer les composants Oracle ASM :</span><span class="sxs-lookup"><span data-stu-id="554de-135">Run these additional commands to install Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="554de-136">Vérifiez qu’Oracle ASM est installé :</span><span class="sxs-lookup"><span data-stu-id="554de-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="554de-137">Le résultat de cette commande doit énumérer les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="554de-137">The output of this command should list the following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="554de-138">ASM requiert des rôles et des utilisateurs spécifiques afin de fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="554de-138">ASM requires specific users and roles in order to function correctly.</span></span> <span data-ttu-id="554de-139">Les commandes suivantes créent les comptes d’utilisateur et les groupes prérequis :</span><span class="sxs-lookup"><span data-stu-id="554de-139">The following commands create the pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="554de-140">Vérifiez que les utilisateurs et les groupes ont été créés correctement :</span><span class="sxs-lookup"><span data-stu-id="554de-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="554de-141">Le résultat de cette commande doit énumérer les utilisateurs et les groupes suivants :</span><span class="sxs-lookup"><span data-stu-id="554de-141">The output of this command should list the following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="554de-142">Créez un dossier pour l’utilisateur*grid* et changez son propriétaire :</span><span class="sxs-lookup"><span data-stu-id="554de-142">Create a folder for user *grid* and change the owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="554de-143">Configurer Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="554de-143">Set up Oracle ASM</span></span>

<span data-ttu-id="554de-144">Pour ce didacticiel, l’utilisateur par défaut est *grid* et le groupe par défaut est *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="554de-144">For this tutorial, the default user is *grid* and the default group is *asmadmin*.</span></span> <span data-ttu-id="554de-145">Vérifiez que l’utilisateur *oracle* fait partie du groupe asmadmin.</span><span class="sxs-lookup"><span data-stu-id="554de-145">Ensure that the *oracle* user is part of the asmadmin group.</span></span> <span data-ttu-id="554de-146">Pour configurer votre installation Oracle ASM, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="554de-146">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="554de-147">La configuration du pilote de la bibliothèque Oracle ASM implique la définition de l’utilisateur par défaut (grid) et du groupe par défaut (asmadmin), ainsi que la configuration du lecteur pour un lancement au démarrage (choisissez y) et l’analyse des disques au démarrage (choisissez y).</span><span class="sxs-lookup"><span data-stu-id="554de-147">Setting up the Oracle ASM library driver involves defining the default user (grid) and default group (asmadmin) as well as configuring the drive to start on boot (choose y) and to scan for disks on boot (choose y).</span></span> <span data-ttu-id="554de-148">Vous devez répondre aux invites de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="554de-148">You need to answer the prompts from the following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="554de-149">Le résultat de cette commande doit ressembler à ce qui suit, jusqu’aux invites.</span><span class="sxs-lookup"><span data-stu-id="554de-149">The output of this command should look similar to the following, stopping with prompts to be answered.</span></span>

    ```bash
   Configuring the Oracle ASM library driver.

   This will configure the on-boot properties of the Oracle ASM library
   driver. The following questions will determine whether the driver is
   loaded on boot and what permissions it will have. The current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user to own the driver interface []: grid
   Default group to own the driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="554de-150">Affichez la configuration du disque :</span><span class="sxs-lookup"><span data-stu-id="554de-150">View the disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="554de-151">Le résultat de cette commande doit ressembler à la liste suivante de disques disponibles.</span><span class="sxs-lookup"><span data-stu-id="554de-151">The output of this command should look similar to the following listing of available disks</span></span>

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

3. <span data-ttu-id="554de-152">Formatez le disque */dev/sdc* en exécutant la commande suivante et en répondant aux invites avec :</span><span class="sxs-lookup"><span data-stu-id="554de-152">Format disk */dev/sdc* by running the following command and answering the prompts with:</span></span>
   - <span data-ttu-id="554de-153">*n* pour la nouvelle partition</span><span class="sxs-lookup"><span data-stu-id="554de-153">*n* for new partition</span></span>
   - <span data-ttu-id="554de-154">*p* pour la partition principale</span><span class="sxs-lookup"><span data-stu-id="554de-154">*p* for primary partition</span></span>
   - <span data-ttu-id="554de-155">*1* pour sélectionner la première partition</span><span class="sxs-lookup"><span data-stu-id="554de-155">*1* to select the first partition</span></span>
   - <span data-ttu-id="554de-156">appuyez sur `enter` pour le premier cylindre de valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="554de-156">press `enter` for the default first cylinder</span></span>
   - <span data-ttu-id="554de-157">appuyez sur `enter` pour le dernier cylindre de valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="554de-157">press `enter` for the default last cylinder</span></span>
   - <span data-ttu-id="554de-158">appuyez sur *w* pour écrire les modifications dans la table de partition</span><span class="sxs-lookup"><span data-stu-id="554de-158">press *w* to write the changes to the partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="554de-159">À l’aide des réponses fournies ci-dessus, la sortie de la commande fdisk doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="554de-159">Using the answers provided above, the output for the fdisk command should look like the following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide to write them.
   After that, of course, the previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   The device presents a logical sector size that is smaller than
   the physical sector size. Aligning to a physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off the mode (command 'c') and change display units to
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
   The partition table has been altered!

   Calling ioctl() to re-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="554de-160">Répétez la commande fdisk précédente pour `/dev/sdd`, `/dev/sde` et `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="554de-160">Repeat the preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="554de-161">Vérifiez la configuration du disque :</span><span class="sxs-lookup"><span data-stu-id="554de-161">Check the disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="554de-162">La sortie de la commande doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="554de-162">The output of the command should look like the following:</span></span>

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

6. <span data-ttu-id="554de-163">Vérifiez l’état du service Oracle ASM et démarrez le service Oracle ASM :</span><span class="sxs-lookup"><span data-stu-id="554de-163">Check the Oracle ASM service status and start the Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="554de-164">La sortie de la commande doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="554de-164">The output of the command should look like the following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing the Oracle ASMLib driver:                     [  OK  ]
   Scanning the system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="554de-165">Créez les disques Oracle ASM :</span><span class="sxs-lookup"><span data-stu-id="554de-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="554de-166">La sortie de la commande doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="554de-166">The output of the command should look like the following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="554de-167">Répertoriez les disques Oracle ASM :</span><span class="sxs-lookup"><span data-stu-id="554de-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="554de-168">Le résultat de la commande doit énumérer les disques Oracle ASM suivants :</span><span class="sxs-lookup"><span data-stu-id="554de-168">The output of the command should list off the following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="554de-169">Modifiez les mots de passe pour les utilisateurs de la racine, d’Oracle et de Grid</span><span class="sxs-lookup"><span data-stu-id="554de-169">Change the passwords for the root, oracle, and grid users.</span></span> <span data-ttu-id="554de-170">**Prenez note de ces nouveaux mots de passe**, car vous les utiliserez plus tard pendant l’installation.</span><span class="sxs-lookup"><span data-stu-id="554de-170">**Make note of these new passwords** as you are using them later during the installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="554de-171">Changez l’autorisation du dossier :</span><span class="sxs-lookup"><span data-stu-id="554de-171">Change the folder permission:</span></span>

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

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="554de-172">Télécharger et préparer Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="554de-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="554de-173">Pour télécharger et préparer Oracle Grid Infrastructure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="554de-173">To download and prepare the Oracle Grid Infrastructure software, complete the following steps:</span></span>

1. <span data-ttu-id="554de-174">Téléchargez Oracle Grid Infrastructure à partir de la [page de téléchargement d’Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="554de-174">Download Oracle Grid Infrastructure from the [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="554de-175">Sous le téléchargement intitulé **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, téléchargez les deux fichiers .zip.</span><span class="sxs-lookup"><span data-stu-id="554de-175">Under the download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download the two .zip files.</span></span>

2. <span data-ttu-id="554de-176">Une fois que vous avez téléchargé les fichiers .zip sur votre ordinateur client, vous pouvez utiliser SCP (Secure Copy Protocol) pour les copier sur votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="554de-176">After you download the .zip files to your client computer, you can use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="554de-177">Revenez via SSH sur votre machine virtuelle Oracle dans Azure afin de déplacer les fichiers .zip dans le dossier /opt.</span><span class="sxs-lookup"><span data-stu-id="554de-177">SSH back into your Oracle VM in Azure in order to move the .zip files into the /opt folder.</span></span> <span data-ttu-id="554de-178">Ensuite, changez le propriétaire des fichiers :</span><span class="sxs-lookup"><span data-stu-id="554de-178">Then, change the owner of the files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="554de-179">Décompressez les fichiers</span><span class="sxs-lookup"><span data-stu-id="554de-179">Unzip the files.</span></span> <span data-ttu-id="554de-180">(installez l’outil de décompression Linux si ce n’est pas déjà fait).</span><span class="sxs-lookup"><span data-stu-id="554de-180">(Install the Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="554de-181">Changez l’autorisation :</span><span class="sxs-lookup"><span data-stu-id="554de-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="554de-182">Mettez à jour l’espace d’échange configuré.</span><span class="sxs-lookup"><span data-stu-id="554de-182">Update configured swap space.</span></span> <span data-ttu-id="554de-183">Les composants Oracle Grid ont besoin d’au moins 6,8 Go d’espace d’échange pour installer Grid.</span><span class="sxs-lookup"><span data-stu-id="554de-183">Oracle Grid components need at least 6.8 GB of swap space to install Grid.</span></span> <span data-ttu-id="554de-184">La taille du fichier d’échange par défaut pour les images Oracle Linux dans Azure est seulement de 2 048 Mo.</span><span class="sxs-lookup"><span data-stu-id="554de-184">The default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="554de-185">Vous devez augmenter `ResourceDisk.SwapSizeMB` dans le fichier `/etc/waagent.conf` et redémarrer le service WALinuxAgent afin que les paramètres mis à jour soient appliqués.</span><span class="sxs-lookup"><span data-stu-id="554de-185">You need to increase `ResourceDisk.SwapSizeMB` in the `/etc/waagent.conf` file and restart the WALinuxAgent service in order for the updated settings to take effect.</span></span> <span data-ttu-id="554de-186">S’agissant d’un fichier en lecture seule, vous devez modifier les autorisations de fichier pour permettre un accès en écriture.</span><span class="sxs-lookup"><span data-stu-id="554de-186">Because it is a read-only file, you need to change file permissions to enable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="554de-187">Recherchez `ResourceDisk.SwapSizeMB` et remplacez la valeur par **8192**.</span><span class="sxs-lookup"><span data-stu-id="554de-187">Search for `ResourceDisk.SwapSizeMB` and change the value to **8192**.</span></span> <span data-ttu-id="554de-188">Vous devez appuyer sur `insert` pour passer en mode d’insertion, saisir la valeur **8192**, puis appuyer sur `esc` pour revenir au mode de commande.</span><span class="sxs-lookup"><span data-stu-id="554de-188">You will need to press `insert` to enter insert mode, type in the value of **8192** and then press `esc` to return to command mode.</span></span> <span data-ttu-id="554de-189">Pour écrire les modifications et fermer le fichier, saisissez `:wq` et appuyez sur `enter`.</span><span class="sxs-lookup"><span data-stu-id="554de-189">To write the changes and quit the file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="554de-190">Nous vous recommandons vivement d’utiliser `WALinuxAgent` pour configurer l’espace d’échange afin qu’il soit toujours créé sur le disque éphémère local (temporaire). Vous bénéficierez ainsi de performances optimales.</span><span class="sxs-lookup"><span data-stu-id="554de-190">We highly recommend that you always use `WALinuxAgent` to configure swap space so that it's always created on the local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="554de-191">Pour plus d’informations, consultez [Comment faire pour ajouter un fichier d’échange dans des machines virtuelles Azure Linux](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="554de-191">For more information on, see [How to add a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-to-run-x11"></a><span data-ttu-id="554de-192">Préparer votre client local et la machine virtuelle pour exécuter x11</span><span class="sxs-lookup"><span data-stu-id="554de-192">Prepare your local client and VM to run x11</span></span>
<span data-ttu-id="554de-193">La configuration d’Oracle ASM nécessite une interface graphique pour mener à bien l’installation et la configuration.</span><span class="sxs-lookup"><span data-stu-id="554de-193">Configuring Oracle ASM requires a graphical interface to complete the install and configuration.</span></span> <span data-ttu-id="554de-194">Nous utilisons le protocole x11 pour faciliter cette installation.</span><span class="sxs-lookup"><span data-stu-id="554de-194">We are using the x11 protocol to facilitate this installation.</span></span> <span data-ttu-id="554de-195">Si vous utilisez un système client (Mac ou Linux) dont les fonctionnalités x11 sont déjà activées et configurées, vous pouvez ignorer cette installation et cette configuration propres aux ordinateurs Windows.</span><span class="sxs-lookup"><span data-stu-id="554de-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive to Windows machines.</span></span> 

1. <span data-ttu-id="554de-196">Téléchargez [PuTTY](http://www.putty.org/) et [Xming](https://xming.en.softonic.com/) sur votre ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="554de-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) to your Windows computer.</span></span> <span data-ttu-id="554de-197">Vous devez terminer l’installation de ces deux applications avec les valeurs par défaut avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="554de-197">You will need to complete the installation of both of these applications with the default values before proceeding.</span></span>

2. <span data-ttu-id="554de-198">Après avoir installé PuTTY, ouvrez une invite de commandes dans le dossier PuTTY (par exemple, C:\Program Files\PuTTY) et modifiez `puttygen.exe` afin de générer une clé.</span><span class="sxs-lookup"><span data-stu-id="554de-198">After you install PuTTY, open a command prompt, change into the PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order to generate a key.</span></span>

3. <span data-ttu-id="554de-199">Dans PuTTY Key Generator :</span><span class="sxs-lookup"><span data-stu-id="554de-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="554de-200">Générez une clé en sélectionnant le bouton `Generate`.</span><span class="sxs-lookup"><span data-stu-id="554de-200">Generate a key by selecting the `Generate` button.</span></span>
   2. <span data-ttu-id="554de-201">Copiez le contenu de la clé (Ctrl+C).</span><span class="sxs-lookup"><span data-stu-id="554de-201">Copy the contents of the key (Ctrl+C).</span></span>
   3. <span data-ttu-id="554de-202">Sélectionnez le bouton `Save private key`.</span><span class="sxs-lookup"><span data-stu-id="554de-202">Select the `Save private key` button.</span></span>
   4. <span data-ttu-id="554de-203">Ignorez l’avertissement sur la sécurisation de la clé avec une phrase secrète, puis sélectionnez `OK`.</span><span class="sxs-lookup"><span data-stu-id="554de-203">Ignore the warning about securing the key with a passphrase, and then select `OK`.</span></span>

   ![Capture d’écran du générateur de clé PuTTY](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="554de-205">Dans votre machine virtuelle, exécutez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="554de-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="554de-206">Créez un fichier appelé `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="554de-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="554de-207">Collez le contenu de la clé dans ce fichier, puis enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="554de-207">Paste the contents of the key in this file, and then save the file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="554de-208">La clé doit contenir la chaîne `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="554de-208">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="554de-209">En outre, le contenu de la clé doit être constitué d’une seule ligne de texte.</span><span class="sxs-lookup"><span data-stu-id="554de-209">Also, the contents of the key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="554de-210">Sur votre système client, démarrez PuTTY.</span><span class="sxs-lookup"><span data-stu-id="554de-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="554de-211">Dans le volet **Category** (Catégorie), accédez à **Connection** > **SSH** > **Auth** (Connexion > SSH > Authentification).</span><span class="sxs-lookup"><span data-stu-id="554de-211">In the **Category** pane, go to **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="554de-212">Dans la zone **Private key file for authentication** (Fichier de clé privée pour l’authentification), accédez à la clé que vous avez générée précédemment.</span><span class="sxs-lookup"><span data-stu-id="554de-212">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

   ![Capture d’écran des options d’authentification SSH](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="554de-214">Dans le volet **Category** (Catégorie), accédez à **Connection** > **SSH** > **X11** (Connexion > SSH > X11).</span><span class="sxs-lookup"><span data-stu-id="554de-214">In the **Category** pane, go to **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="554de-215">Activez la case à cocher **Enable X11 forwarding** (Activer le transfert X11).</span><span class="sxs-lookup"><span data-stu-id="554de-215">Select the **Enable X11 forwarding** check box.</span></span>

   ![Capture d’écran des options de transfert SSH X11](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="554de-217">Dans le volet **Category** (Catégorie), accédez à **Session**.</span><span class="sxs-lookup"><span data-stu-id="554de-217">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="554de-218">Indiquez votre machine virtuelle Oracle ASM `<publicIPaddress>` dans la boîte de dialogue du nom hôte, renseignez un nouveau nom `Saved Session`, puis cliquez sur `Save`.</span><span class="sxs-lookup"><span data-stu-id="554de-218">Enter your Oracle ASM VM `<publicIPaddress>` in the host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="554de-219">Une fois les modifications enregistrées, cliquez sur `open` pour vous connecter à votre machine virtuelle Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="554de-219">Once saved, click on `open` to connect to your Oracle ASM virtual machine.</span></span>  <span data-ttu-id="554de-220">Lors de la première connexion, vous êtes averti que le système distant n’est pas mis en cache dans le registre.</span><span class="sxs-lookup"><span data-stu-id="554de-220">The first time you connect you are warned  the remote system is not cached in your registry.</span></span> <span data-ttu-id="554de-221">Cliquez sur `yes` pour l’ajouter et continuer.</span><span class="sxs-lookup"><span data-stu-id="554de-221">Click on `yes` to add it and continue.</span></span>

   ![Capture d’écran des options de session PuTTY](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="554de-223">Installer Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="554de-223">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="554de-224">Pour installer Oracle Grid Infrastructure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="554de-224">To install Oracle Grid Infrastructure, complete the following steps:</span></span>

1. <span data-ttu-id="554de-225">Connectez-vous en tant que **grid**.</span><span class="sxs-lookup"><span data-stu-id="554de-225">Sign in as **grid**.</span></span> <span data-ttu-id="554de-226">(Vous devez pouvoir vous connecter sans avoir à saisir un mot de passe.)</span><span class="sxs-lookup"><span data-stu-id="554de-226">(You should be able to sign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="554de-227">Si vous exécutez Windows, vérifiez que vous avez démarré Xming avant de commencer l’installation.</span><span class="sxs-lookup"><span data-stu-id="554de-227">If you are running Windows, make sure you have started Xming before you begin the installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="554de-228">Le programme d’installation d’Oracle Grid Infrastructure 12c Release 1 s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="554de-228">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="554de-229">(Plusieurs minutes peuvent être nécessaires au démarrage du programme d’installation.)</span><span class="sxs-lookup"><span data-stu-id="554de-229">(It might take a few minutes for the  installer to start.)</span></span>

2. <span data-ttu-id="554de-230">Dans la page **Select Installation Option** (Sélectionner l’option d’installation), sélectionnez **Install and Configure Oracle Grid Infrastructure for a Standalone Server** (Installer et configurer Oracle Grid Infrastructure pour un serveur autonome).</span><span class="sxs-lookup"><span data-stu-id="554de-230">On the **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Capture d’écran de la page Select Installation Option (Sélectionner l’option d’installation)](./media/oracle-asm/install01.png)

3. <span data-ttu-id="554de-232">Sur la page **Select Product Languages** (Sélectionner les langues du produit), vérifiez que **English** (Anglais) ou la langue souhaitée est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="554de-232">On the **Select Product Languages** page, ensure **English** or the language that you want is selected.</span></span>  <span data-ttu-id="554de-233">Cliquez sur `next`.</span><span class="sxs-lookup"><span data-stu-id="554de-233">Click `next`.</span></span>

4. <span data-ttu-id="554de-234">Dans la page **Create ASM Disk Group** (Créer un groupe de disques ASM) :</span><span class="sxs-lookup"><span data-stu-id="554de-234">On the **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="554de-235">Entrez un nom pour le groupe de disques.</span><span class="sxs-lookup"><span data-stu-id="554de-235">Enter a name for the disk group.</span></span>
   - <span data-ttu-id="554de-236">Sous **Redundancy** (Redondance), sélectionnez **External** (Externe).</span><span class="sxs-lookup"><span data-stu-id="554de-236">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="554de-237">Sous **Allocation Unit Size** (Taille d’unité d’allocation), sélectionnez **4**.</span><span class="sxs-lookup"><span data-stu-id="554de-237">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="554de-238">Sous **Add Disks** (Ajouter des disques), sélectionnez **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="554de-238">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="554de-239">Cliquez sur `next`.</span><span class="sxs-lookup"><span data-stu-id="554de-239">Click `next`.</span></span>

5. <span data-ttu-id="554de-240">Dans la page **Specify ASM Password** (Spécifier le mot de passe ASM), sélectionnez l’option **Use same passwords for these accounts** (Utiliser les mêmes mots de passe pour ces comptes) et entrez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="554de-240">On the **Specify ASM Password** page, select the **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Capture d’écran de la page Specify ASM Password (Spécifier le mot de passe ASM) du programme d’installation](./media/oracle-asm/install04.png)

6. <span data-ttu-id="554de-242">Sur la page **Specify Management Options** (Spécifier les options de gestion), vous pouvez configurer EM Cloud Control.</span><span class="sxs-lookup"><span data-stu-id="554de-242">On the **Specify Management Options** page, you have the option to configure EM Cloud Control.</span></span> <span data-ttu-id="554de-243">Cette option est ignorée ; cliquez sur `next` pour continuer.</span><span class="sxs-lookup"><span data-stu-id="554de-243">We are skipping this option - click `next` to continue.</span></span> 

7. <span data-ttu-id="554de-244">Dans la page **Privileged Operating System Groups** (Groupes privilégiés du système d’exploitation), utilisez les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="554de-244">On the **Privileged Operating System Groups** page, use the default settings.</span></span> <span data-ttu-id="554de-245">Cliquez sur `next` pour continuer.</span><span class="sxs-lookup"><span data-stu-id="554de-245">Click `next` to continue.</span></span>

8. <span data-ttu-id="554de-246">Dans la page **Specify Installation Location** (Spécifier l’emplacement d’installation), utilisez les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="554de-246">On the **Specify Installation Location** page, use the default settings.</span></span> <span data-ttu-id="554de-247">Cliquez sur `next` pour continuer.</span><span class="sxs-lookup"><span data-stu-id="554de-247">Click `next` to continue.</span></span>

9. <span data-ttu-id="554de-248">Sur la page **Create Inventory** (Créer un inventaire), remplacez le répertoire de l’inventaire par `/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="554de-248">On the **Create Inventory** page, change the Inventory Directory to `/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="554de-249">Cliquez sur `next` pour continuer.</span><span class="sxs-lookup"><span data-stu-id="554de-249">Click `next` to continue.</span></span>

   ![Capture d’écran de la page Create Inventory (Créer un inventaire) du programme d’installation](./media/oracle-asm/install08.png)

10. <span data-ttu-id="554de-251">Dans la page **Root script execution configuration** (Configuration de l’exécution des scripts root), actualisez la case à cocher **Automatically run configuration scripts** (Exécuter automatiquement les scripts de configuration).</span><span class="sxs-lookup"><span data-stu-id="554de-251">On the **Root script execution configuration** page, select the **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="554de-252">Ensuite, sélectionnez l’option **Use "root" user credential** (Utiliser les informations d’identification de l’utilisateur « root »), puis entrez le mot de passe de l’utilisateur root.</span><span class="sxs-lookup"><span data-stu-id="554de-252">Then, select the **Use "root" user credential** option, and enter the root user password.</span></span>

    ![Capture d’écran de la page Use "root" user credential (Utiliser les informations d’identification de l’utilisateur « root ») du programme d’installation](./media/oracle-asm/install09.png)

11. <span data-ttu-id="554de-254">Sur la page **Perform Prerequisite Checks** (Effectuer les tests de prérequis), le programme d’installation en cours échoue avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="554de-254">On the **Perform Prerequisite Checks** page, the current setup will fail with errors.</span></span> <span data-ttu-id="554de-255">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="554de-255">This is an expected behavior.</span></span> <span data-ttu-id="554de-256">Sélectionnez `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="554de-256">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="554de-257">Dans la boîte de dialogue **Fixup Script** (Corriger le script), cliquez sur `OK`.</span><span class="sxs-lookup"><span data-stu-id="554de-257">In the **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="554de-258">Sur la page **Summary** (Récapitulatif), passez en revue les paramètres sélectionnés, puis cliquez sur `Install`.</span><span class="sxs-lookup"><span data-stu-id="554de-258">On the **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Capture d’écran de la page Summary (Récapitulatif) du programme d’installation](./media/oracle-asm/install12.png)

14. <span data-ttu-id="554de-260">Une boîte de dialogue d’avertissement apparaît. Elle vous informe que les scripts de configuration doivent être exécutés en tant qu’utilisateur doté de privilèges.</span><span class="sxs-lookup"><span data-stu-id="554de-260">A warning dialog box appears informing you configuration scripts need to be run as a privileged user.</span></span> <span data-ttu-id="554de-261">Cliquez sur `Yes` pour continuer.</span><span class="sxs-lookup"><span data-stu-id="554de-261">Click `Yes` to continue.</span></span>

15. <span data-ttu-id="554de-262">Sur la page **Finish** (Terminer), cliquez sur `Close` pour terminer l’installation.</span><span class="sxs-lookup"><span data-stu-id="554de-262">On the **Finish** page, click `Close` to finish the installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="554de-263">Configurer votre installation Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="554de-263">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="554de-264">Pour configurer votre installation Oracle ASM, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="554de-264">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="554de-265">Vérifiez que vous êtes toujours connecté en tant que **grid** à partir de votre session X11.</span><span class="sxs-lookup"><span data-stu-id="554de-265">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="554de-266">Vous devrez peut-être appuyer sur `enter` pour réactiver le terminal.</span><span class="sxs-lookup"><span data-stu-id="554de-266">You might need to hit `enter` to revive the terminal.</span></span> <span data-ttu-id="554de-267">Ensuite, lancez l’Assistant de configuration d’Oracle Automated Storage Management :</span><span class="sxs-lookup"><span data-stu-id="554de-267">Then launch the Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="554de-268">L’Assistant de configuration d’Oracle ASM s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="554de-268">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="554de-269">Dans la boîte de dialogue **Configure ASM: Disk Groups** (Configurer ASM : groupes de disques), cliquez sur le bouton `Create`, puis sur `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="554de-269">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="554de-270">Dans la boîte de dialogue **Create Disk Group** (Créer un groupe de disques) :</span><span class="sxs-lookup"><span data-stu-id="554de-270">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="554de-271">Entrez le nom de groupe de disques **DATA**.</span><span class="sxs-lookup"><span data-stu-id="554de-271">Enter the disk group name **DATA**.</span></span>
   - <span data-ttu-id="554de-272">Sous **Select Member Disks** (Sélectionner les disques membres), sélectionnez **ORCL_DATA** et **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="554de-272">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="554de-273">Sous **Allocation Unit Size** (Taille d’unité d’allocation), sélectionnez **4**.</span><span class="sxs-lookup"><span data-stu-id="554de-273">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="554de-274">Cliquez sur `ok` pour créer le groupe de disques.</span><span class="sxs-lookup"><span data-stu-id="554de-274">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="554de-275">Cliquez sur `ok` pour fermer la fenêtre de confirmation.</span><span class="sxs-lookup"><span data-stu-id="554de-275">Click `ok` to close the confirmation window.</span></span>

   ![Capture d’écran de la boîte de dialogue Create Disk Group (Créer un groupe de disques)](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="554de-277">Dans la boîte de dialogue **Configure ASM: Disk Groups** (Configurer ASM : groupes de disques), cliquez sur le bouton `Create`, puis sur `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="554de-277">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="554de-278">Dans la boîte de dialogue **Create Disk Group** (Créer un groupe de disques) :</span><span class="sxs-lookup"><span data-stu-id="554de-278">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="554de-279">Entrez le nom de groupe de disques **FRA**.</span><span class="sxs-lookup"><span data-stu-id="554de-279">Enter the disk group name **FRA**.</span></span>
   - <span data-ttu-id="554de-280">Sous **Redundancy** (Redondance), sélectionnez **External (none)** (Externe (aucun)).</span><span class="sxs-lookup"><span data-stu-id="554de-280">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="554de-281">Sous **Select Member Disks** (Sélectionner les disques membres), sélectionnez **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="554de-281">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="554de-282">Sous **Allocation Unit Size** (Taille d’unité d’allocation), sélectionnez **4**.</span><span class="sxs-lookup"><span data-stu-id="554de-282">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="554de-283">Cliquez sur `ok` pour créer le groupe de disques.</span><span class="sxs-lookup"><span data-stu-id="554de-283">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="554de-284">Cliquez sur `ok` pour fermer la fenêtre de confirmation.</span><span class="sxs-lookup"><span data-stu-id="554de-284">Click `ok` to close the confirmation window.</span></span>

   ![Capture d’écran de la boîte de dialogue Create Disk Group (Créer un groupe de disques)](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="554de-286">Sélectionnez **Exit** (Quitter) pour fermer l’Assistant de configuration d’ASM.</span><span class="sxs-lookup"><span data-stu-id="554de-286">Select **Exit** to close ASM Configuration Assistant.</span></span>

   ![Capture d’écran de la boîte de dialogue Configure ASM: Disk Groups (Configurer ASM : Groupes de disques) avec le bouton Exit (Quitter)](./media/oracle-asm/asm05.png)

## <a name="create-the-database"></a><span data-ttu-id="554de-288">Création de la base de données</span><span class="sxs-lookup"><span data-stu-id="554de-288">Create the database</span></span>

<span data-ttu-id="554de-289">Le logiciel de base de données Oracle est déjà installé sur l’image de la Place de marché Azure.</span><span class="sxs-lookup"><span data-stu-id="554de-289">The Oracle database software is already installed on the Azure Marketplace image.</span></span> <span data-ttu-id="554de-290">Pour créer une base de données, exécutez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="554de-290">To create a database, complete the following steps:</span></span>

1. <span data-ttu-id="554de-291">Changez l’utilisateur et passez au superutilisateur d’Oracle, puis initialisez l’écouteur pour la journalisation :</span><span class="sxs-lookup"><span data-stu-id="554de-291">Switch users to the Oracle superuser, and then initialize the listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="554de-292">L’Assistant de configuration de base de données s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="554de-292">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="554de-293">Sur la page **Database Operation** (Opération de base de données), cliquez sur `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="554de-293">On the **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="554de-294">Dans la page **Creation Mode** (Mode de création ) :</span><span class="sxs-lookup"><span data-stu-id="554de-294">On the **Creation Mode** page:</span></span>

   - <span data-ttu-id="554de-295">Entrez un nom pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="554de-295">Enter a name for the database.</span></span>
   - <span data-ttu-id="554de-296">Pour **Storage Type** (Type de stockage), assurez-vous que l’option **Automatic Storage Management (ASM)** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="554de-296">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="554de-297">Pour l’**emplacement des fichiers de base de données**, utilisez l’emplacement par défaut ASM suggéré.</span><span class="sxs-lookup"><span data-stu-id="554de-297">For **Database Files Location**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="554de-298">Pour la **zone de récupération rapide**, utilisez l’emplacement par défaut ASM suggéré.</span><span class="sxs-lookup"><span data-stu-id="554de-298">For **Fast Recovery Area**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="554de-299">Saisissez un **mot de passe administrateur** et **confirmez le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="554de-299">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="554de-300">Vérifiez que l’option `create as container database` est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="554de-300">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="554de-301">Saisissez une valeur pour `pluggable database name`.</span><span class="sxs-lookup"><span data-stu-id="554de-301">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="554de-302">Sur la page **Summary** (Récapitulatif), passez en revue les paramètres sélectionnés, puis cliquez sur `Finish` pour créer la base de données.</span><span class="sxs-lookup"><span data-stu-id="554de-302">On the **Summary** page, review your selected settings, and then click `Finish` to create the database.</span></span>

   ![Capture d’écran de la page Summary (Récapitulatif)](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="554de-304">La base de données a été créée.</span><span class="sxs-lookup"><span data-stu-id="554de-304">The Database has been created.</span></span> <span data-ttu-id="554de-305">Sur la page **Finish** (Terminer), vous pouvez déverrouiller des comptes supplémentaires pour utiliser cette base de données et modifier les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="554de-305">On the **Finish** page, you have the option to unlock additional accounts to use this database and change the passwords.</span></span> <span data-ttu-id="554de-306">Pour ce faire, sélectionnez **Password Management** (Gestion des mots de passe). Sinon, cliquez sur `close`.</span><span class="sxs-lookup"><span data-stu-id="554de-306">If you wish to do so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-the-vm"></a><span data-ttu-id="554de-307">Supprimer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="554de-307">Delete the VM</span></span>

<span data-ttu-id="554de-308">Vous avez correctement configuré Oracle Automated Storage Management sur l’image de base de données Oracle à partir de la Place de marché Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="554de-308">You have successfully configured Oracle Automated Storage Management on the Oracle DB image from the Azure Marketplace.</span></span>  <span data-ttu-id="554de-309">Si vous n’avez plus besoin de cette machine virtuelle, vous pouvez utiliser la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées :</span><span class="sxs-lookup"><span data-stu-id="554de-309">When you no longer need this VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="554de-310">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="554de-310">Next steps</span></span>

[<span data-ttu-id="554de-311">Didacticiel : Configurer Oracle DataGuard</span><span class="sxs-lookup"><span data-stu-id="554de-311">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="554de-312">Didacticiel : Configurer Oracle GoldenGate</span><span class="sxs-lookup"><span data-stu-id="554de-312">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="554de-313">Revoir [Créer l’architecture d’une base de données Oracle](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="554de-313">Review [Architect an Oracle DB](oracle-design.md)</span></span>
