---
title: Utilisation du stockage de fichiers Azure avec Linux | Microsoft Docs
description: "Découvrez comment monter un partage de fichiers Azure via SMB sur Linux."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: 27b393a899c60a3a0393619f338a396dff659498
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="8475d-103">Utilisation du stockage de fichiers Azure avec Linux</span><span class="sxs-lookup"><span data-stu-id="8475d-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="8475d-104">Le [Stockage Fichier Azure](storage-dotnet-how-to-use-files.md) est le système de fichiers dans le cloud, facile à utiliser, de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8475d-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="8475d-105">Les partages de fichiers Azure peuvent être montés dans des distributions Linux à l’aide du [package cifs-utils](https://wiki.samba.org/index.php/LinuxCIFS_utils) à partir du [projet Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="8475d-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="8475d-106">Cet article présente deux méthodes de montage d’un partage de fichiers Azure : à la demande avec la commande `mount` et au démarrage en créant une entrée dans `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="8475d-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="8475d-107">Pour monter un partage de fichiers Azure en dehors de la région Azure dans laquelle il est hébergé, par exemple en local ou dans une région Azure différente, le système d’exploitation doit prendre en charge la fonctionnalité de chiffrement de SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="8475d-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="8475d-108">La fonctionnalité de chiffrement pour SMB 3.0 pour Linux a été introduite dans le noyau 4.11.</span><span class="sxs-lookup"><span data-stu-id="8475d-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="8475d-109">Cette fonctionnalité permet le montage du partage de fichiers Azure en local ou à partir d’une autre région Azure.</span><span class="sxs-lookup"><span data-stu-id="8475d-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="8475d-110">Quand nous avons publié cet article, cette fonctionnalité a été rétroportée dans Ubuntu à partir de 16.04 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="8475d-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="8475d-111">Conditions préalables au montage d’un partage de fichiers Azure avec Linux et le package cifs-utils</span><span class="sxs-lookup"><span data-stu-id="8475d-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="8475d-112">**Choisissez une distribution Linux pour laquelle le package cifs-utils peut être installé** : Microsoft recommande les distributions Linux suivantes dans la galerie d’images Azure :</span><span class="sxs-lookup"><span data-stu-id="8475d-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="8475d-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="8475d-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="8475d-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="8475d-114">RHEL 7+</span></span>
    * <span data-ttu-id="8475d-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="8475d-115">CentOS 7+</span></span>
    * <span data-ttu-id="8475d-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="8475d-116">Debian 8</span></span>
    * <span data-ttu-id="8475d-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="8475d-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="8475d-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="8475d-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="8475d-119"><a id="install-cifs-utils"></a>**Le package cifs-utils est installé** : le package cifs-utils peut être installé à l’aide du gestionnaire de packages sur la distribution Linux de votre choix.</span><span class="sxs-lookup"><span data-stu-id="8475d-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="8475d-120">Sur les distributions **Ubuntu** et **basées sur Debian**, utilisez le gestionnaire de packages `apt-get` :</span><span class="sxs-lookup"><span data-stu-id="8475d-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="8475d-121">Sur **RHEL** et **CentOS**, utilisez le gestionnaire de packages `yum` :</span><span class="sxs-lookup"><span data-stu-id="8475d-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="8475d-122">Sur **openSUSE**, utilisez le gestionnaire de packages `zypper` :</span><span class="sxs-lookup"><span data-stu-id="8475d-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="8475d-123">Sur les autres distributions, utilisez le gestionnaire de packages approprié ou effectuez une [compilation à partir de la source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="8475d-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="8475d-124">**Déterminez les autorisations de fichier/répertoire du partage monté** : dans les exemples ci-dessous, nous utilisons 0777 pour accorder des autorisations de lecture, d’écriture et d’exécution à tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8475d-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="8475d-125">Vous pouvez les remplacer par d’autres [autorisations chmod](https://en.wikipedia.org/wiki/Chmod) comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="8475d-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="8475d-126">**Nom de compte de stockage** : pour monter un partage de fichiers Azure, vous avez besoin du nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8475d-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="8475d-127">**Clé du compte de stockage** : pour monter un partage de fichiers Azure, vous avez besoin de la clé de stockage primaire (ou secondaire).</span><span class="sxs-lookup"><span data-stu-id="8475d-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="8475d-128">Actuellement, les clés SAS ne sont pas prises en charge pour le montage.</span><span class="sxs-lookup"><span data-stu-id="8475d-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="8475d-129">**Vérifiez que le port 445 est ouvert** : SMB communique via le port TCP 445. Assurez-vous que votre pare-feu ne bloque pas les ports TCP 445 de la machine cliente.</span><span class="sxs-lookup"><span data-stu-id="8475d-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="8475d-130">Montage du partage de fichiers Azure à la demande avec `mount`</span><span class="sxs-lookup"><span data-stu-id="8475d-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="8475d-131">**[Installez le package cifs-utils pour votre distribution Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="8475d-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="8475d-132">**Créez un dossier pour le point de montage** : cela peut être fait n’importe où sur le système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="8475d-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="8475d-133">**Utilisez la commande de montage pour monter le partage de fichiers Azure** : n’oubliez pas de remplacer `<storage-account-name>`, `<share-name>` et `<storage-account-key>` par les informations appropriées.</span><span class="sxs-lookup"><span data-stu-id="8475d-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="8475d-134">Lorsque vous avez terminé d’utiliser le partage de fichiers Azure, vous pouvez utiliser `sudo umount ./mymountpoint` pour démonter le partage.</span><span class="sxs-lookup"><span data-stu-id="8475d-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="8475d-135">Création d’un point de montage persistant pour le partage de fichiers Azure avec `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="8475d-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="8475d-136">**[Installez le package cifs-utils pour votre distribution Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="8475d-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="8475d-137">**Créez un dossier pour le point de montage** : cela peut être fait n’importe où sur le système de fichiers, mais vous devez noter le chemin d’accès absolu du dossier.</span><span class="sxs-lookup"><span data-stu-id="8475d-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="8475d-138">L’exemple suivant permet de créer un dossier à la racine.</span><span class="sxs-lookup"><span data-stu-id="8475d-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="8475d-139">**Utilisez la commande suivante pour ajouter la ligne suivante à `/etc/fstab`** : n’oubliez pas de remplacer `<storage-account-name>`, `<share-name>` et `<storage-account-key>` par les informations appropriées.</span><span class="sxs-lookup"><span data-stu-id="8475d-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="8475d-140">Vous pouvez utiliser `sudo mount -a` pour monter le partage de fichiers Azure après la modification de `/etc/fstab` plutôt que de redémarrer.</span><span class="sxs-lookup"><span data-stu-id="8475d-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="8475d-141">Commentaires</span><span class="sxs-lookup"><span data-stu-id="8475d-141">Feedback</span></span>
<span data-ttu-id="8475d-142">Utilisateurs de Linux, nous attendons votre avis !</span><span class="sxs-lookup"><span data-stu-id="8475d-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="8475d-143">Le stockage de fichiers Azure pour le groupe d'utilisateurs Linux propose un forum vous permettant de partager vos commentaires lorsque vous évaluez et adoptez le stockage de fichiers sur Linux.</span><span class="sxs-lookup"><span data-stu-id="8475d-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="8475d-144">Envoyez un courrier électronique aux [utilisateurs Linux du partage de fichiers Azure ](mailto:azurefileslinuxusers@microsoft.com) pour rejoindre le groupe d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8475d-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8475d-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8475d-145">Next steps</span></span>
<span data-ttu-id="8475d-146">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="8475d-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="8475d-147">Référence de l’API REST du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="8475d-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="8475d-148">Utilisation d’Azure PowerShell avec Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8475d-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="8475d-149">Transférer des données avec AzCopy sur Windows</span><span class="sxs-lookup"><span data-stu-id="8475d-149">How to use AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="8475d-150">Utilisation d’Azure CLI 2.0 avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8475d-150">Using the Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="8475d-151">FAQ</span><span class="sxs-lookup"><span data-stu-id="8475d-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="8475d-152">Dépannage</span><span class="sxs-lookup"><span data-stu-id="8475d-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
