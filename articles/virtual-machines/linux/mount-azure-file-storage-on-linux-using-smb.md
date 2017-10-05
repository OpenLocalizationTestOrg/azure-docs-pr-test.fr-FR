---
title: "Montage du stockage de fichiers Azure sur les machines virtuelles Linux à l’aide de SMB | Microsoft Docs"
description: "Procédure de montage du stockage de fichiers Azure sur les machines virtuelles Linux à l’aide de SMB avec Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 9eae17b304f8a987b44ebed8906dabd8ff3a36a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="0f3cf-103">Monter le stockage de fichiers Azure sur les machines virtuelles Linux à l’aide de SMB</span><span class="sxs-lookup"><span data-stu-id="0f3cf-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="0f3cf-104">Cet article vous montre comment utiliser le service de stockage de fichiers Azure sur une machine virtuelle Linux à l’aide d’un montage SMB avec Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-104">This article shows you how to utilize the Azure File storage service on a Linux VM using an SMB mount with the Azure CLI 2.0.</span></span> <span data-ttu-id="0f3cf-105">Le stockage de fichiers Azure propose des partages de fichiers dans le cloud s’appuyant sur le protocole SMB standard.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-105">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span></span> <span data-ttu-id="0f3cf-106">Vous pouvez également effectuer ces étapes à l’aide [d’Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f3cf-106">You can also perform these steps with the [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0f3cf-107">Les conditions requises sont :</span><span class="sxs-lookup"><span data-stu-id="0f3cf-107">The requirements are:</span></span>

- [<span data-ttu-id="0f3cf-108">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="0f3cf-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="0f3cf-109">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="0f3cf-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="0f3cf-110">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="0f3cf-110">Quick Commands</span></span>

* <span data-ttu-id="0f3cf-111">Un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-111">A resource group</span></span>
* <span data-ttu-id="0f3cf-112">Un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-112">An Azure virtual network</span></span>
* <span data-ttu-id="0f3cf-113">Un groupe de sécurité réseau avec une connexion SSH entrante.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="0f3cf-114">Un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-114">A subnet</span></span>
* <span data-ttu-id="0f3cf-115">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-115">An Azure storage account</span></span>
* <span data-ttu-id="0f3cf-116">Des clés de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-116">Azure storage account keys</span></span>
* <span data-ttu-id="0f3cf-117">Un partage de stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-117">An Azure File storage share</span></span>
* <span data-ttu-id="0f3cf-118">Une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-118">A Linux VM</span></span>

<span data-ttu-id="0f3cf-119">Remplacez les exemples par vos propres paramètres.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-the-local-mount"></a><span data-ttu-id="0f3cf-120">Créez un répertoire pour le montage local</span><span class="sxs-lookup"><span data-stu-id="0f3cf-120">Create a directory for the local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-the-file-storage-smb-share-to-the-mount-point"></a><span data-ttu-id="0f3cf-121">Montez le partage SMB de stockage de fichiers sur le point de montage.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-121">Mount the File storage SMB share to the mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-the-mount-after-a-reboot"></a><span data-ttu-id="0f3cf-122">Conservez le montage après redémarrage.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-122">Persist the mount after a reboot</span></span>
<span data-ttu-id="0f3cf-123">Pour ce faire, ajoutez la ligne suivante à l’élément `/etc/fstab` :</span><span class="sxs-lookup"><span data-stu-id="0f3cf-123">To do so, add the following line to the `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0f3cf-124">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="0f3cf-124">Detailed walkthrough</span></span>

<span data-ttu-id="0f3cf-125">Le stockage de fichiers propose des partages de fichiers dans le cloud qui utilisent le protocole SMB standard.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-125">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="0f3cf-126">Avec la dernière version du Stockage Fichier, vous pouvez également monter un partage de fichiers à partir d’un système d’exploitation prenant en charge SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-126">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="0f3cf-127">Un montage SMB sur Linux permet d’effectuer facilement une sauvegarde vers un emplacement de stockage d’archivage robuste et permanent pris en charge par un contrat de niveau de service.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-127">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="0f3cf-128">Un bon moyen de déboguer les journaux consiste à déplacer les fichiers vers un montage SMB hébergé sur le stockage de fichiers à partir d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-128">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="0f3cf-129">En effet, un même partage SMB peut être monté localement sur votre station de travail Windows, Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-129">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="0f3cf-130">SMB ne constitue pas la meilleure solution pour transmettre en continu des journaux d’applications ou Linux en temps réel, car le protocole SMB n’est pas conçu pour gérer des tâches de journalisation aussi lourdes.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-130">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="0f3cf-131">Un outil de couche de journalisation unifié et dédié comme Fluentd resprésente un meilleur choix que SMB pour collecter la sortie de journalisation d’applications et Linux.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="0f3cf-132">Pour cette procédure pas à pas détaillée, nous créons la configuration requise pour d’abord créer le partage de Stockage Fichier, puis le monter via SMB sur une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-132">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="0f3cf-133">Créez un groupe de ressource avec la commande [az group create](/cli/azure/group#create) pour contenir le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-133">Create a resource group with [az group create](/cli/azure/group#create) to hold the file share.</span></span>

    <span data-ttu-id="0f3cf-134">Créez un groupe de ressources nommé `myResourceGroup` dans la région États-Unis de l’Ouest en suivant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0f3cf-134">To create a resource group named `myResourceGroup` in the "West US" location, use the following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="0f3cf-135">Créez un compte de stockage Azure avec [az storage account create](/cli/azure/storage/account#create) pour stocker les fichiers.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) to store the actual files.</span></span>

    <span data-ttu-id="0f3cf-136">Pour créer un compte de stockage nommé mystorageaccount à l’aide de la référence de stockage Standard_LRS, suivez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0f3cf-136">To create a storage account named mystorageaccount by using the Standard_LRS storage SKU, use the following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="0f3cf-137">Affichez les clés de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-137">Show the storage account keys.</span></span>

    <span data-ttu-id="0f3cf-138">Quand vous créez un compte de stockage, les clés du compte sont créées par paires afin qu’elles puissent faire l’objet d’une rotation sans interruption du service.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-138">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="0f3cf-139">Lorsque vous basculez vers la deuxième clé de la paire, vous créez une nouvelle paire de clés.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-139">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="0f3cf-140">Les nouvelles clés de compte de stockage sont toujours créées par paires, pour garantir que vous disposiez toujours d’au moins une clé de stockage inutilisée prête au basculement.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready to switch to.</span></span>

    <span data-ttu-id="0f3cf-141">Utilisez [az storage account keys list](/cli/azure/storage/account/keys#list) pour afficher les clés du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-141">View the storage account keys with the [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="0f3cf-142">Les clés de compte de stockage pour l’élément nommé `mystorageaccount` sont répertoriées dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0f3cf-142">The storage account keys for the named `mystorageaccount` are listed in the following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="0f3cf-143">Pour extraire une clé unique, utilisez l’indicateur `--query`.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-143">To extract a single key, use the `--query` flag.</span></span> <span data-ttu-id="0f3cf-144">L’exemple suivant extrait la première clé (`[0]`) :</span><span class="sxs-lookup"><span data-stu-id="0f3cf-144">The following example extracts the first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="0f3cf-145">Créez le partage de stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-145">Create the File storage share.</span></span>

    <span data-ttu-id="0f3cf-146">Créez le partage de stockage de fichiers qui contient le partage SMB avec [az storage share create](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="0f3cf-146">The File storage share contains the SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="0f3cf-147">Le quota est toujours exprimé en gigaoctets (Go).</span><span class="sxs-lookup"><span data-stu-id="0f3cf-147">The quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="0f3cf-148">Passez l’une des clés de la commande `az storage account keys list` précédente.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-148">Pass in one of the keys from the preceding `az storage account keys list` command.</span></span> <span data-ttu-id="0f3cf-149">Créez un partage nommé mystorageshare avec un quota de 10 Go en appliquant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0f3cf-149">Create a share named mystorageshare with a 10-GB quota by using the following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="0f3cf-150">Créez un répertoire de point de montage.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="0f3cf-151">Créez un répertoire local sur le système de fichiers Linux pour monter le partage SMB.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-151">Create a local directory in the Linux file system to mount the SMB share to.</span></span> <span data-ttu-id="0f3cf-152">Tout ce qui est écrit ou lu à partir du répertoire de montage local est transféré au partage SMB hébergé sur le stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-152">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span></span> <span data-ttu-id="0f3cf-153">Pour créer un répertoire local à l’emplacement /mnt/mymountdirectory, appliquez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0f3cf-153">To create a local directory at /mnt/mymountdirectory, use the following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="0f3cf-154">Montez le partage SMB sur le répertoire local.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-154">Mount the SMB share to the local directory.</span></span>

    <span data-ttu-id="0f3cf-155">Fournissez votre propre nom d’utilisateur de compte de stockage et la clé de compte de stockage pour les informations d’identification de montage comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f3cf-155">Provide your own storage account username and storage account key for the mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="0f3cf-156">Conservez le montage SMB au cours des redémarrages.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-156">Persist the SMB mount through reboots.</span></span>

    <span data-ttu-id="0f3cf-157">Lorsque vous redémarrez la machine virtuelle Linux, le partage SMB monté est démonté lors de l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-157">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="0f3cf-158">Pour remonter le partage SMB au démarrage, ajoutez une ligne à /etc/fstab dans Linux.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-158">To remount the SMB share on boot, add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="0f3cf-159">Linux utilise le fichier fstab pour lister les systèmes de fichiers à monter pendant le processus de démarrage.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-159">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="0f3cf-160">L’ajout du partage SMB garantit que le partage de stockage de fichiers est un système de fichiers monté définitivement pour la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-160">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="0f3cf-161">Il est possible d’ajouter le partage SMB du Stockage Fichier sur une nouvelle machine virtuelle si vous utilisez cloud-init.</span><span class="sxs-lookup"><span data-stu-id="0f3cf-161">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="0f3cf-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f3cf-162">Next steps</span></span>

- [<span data-ttu-id="0f3cf-163">Utilisation de cloud-init pour personnaliser une machine virtuelle Linux lors de la création</span><span class="sxs-lookup"><span data-stu-id="0f3cf-163">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="0f3cf-164">Ajouter un disque à une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="0f3cf-164">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="0f3cf-165">Chiffrer des disques sur une machine virtuelle Linux à l’aide de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="0f3cf-165">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
