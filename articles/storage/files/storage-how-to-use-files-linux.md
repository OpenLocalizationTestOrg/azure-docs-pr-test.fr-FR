---
title: aaaUse stockage Azure files avec Linux | Documents Microsoft
description: "Découvrez comment toomount un fichier Azure partager sur SMB sur Linux."
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
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="3b1ff-103">Utilisation du stockage de fichiers Azure avec Linux</span><span class="sxs-lookup"><span data-stu-id="3b1ff-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="3b1ff-104">[Stockage de fichier Azure](../storage-dotnet-how-to-use-files.md) est le système de fichiers de cloud de Microsoft toouse facile.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="3b1ff-105">Les partages de fichiers Azure peuvent être montés dans des distributions de Linux à l’aide de hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) de hello [projet de Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="3b1ff-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="3b1ff-106">Cet article montre deux façons toomount un partage de fichiers Azure : flux de données à la demande avec hello `mount` de commande et de démarrage en créant une entrée dans `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="3b1ff-107">Dans l’ordre toomount un partage de fichiers Azure en dehors de hello région Azure, qu'il est hébergé dans, telles que localement ou dans une autre région Azure hello du système d’exploitation doit prendre en charge la fonctionnalité de chiffrement hello de SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="3b1ff-108">La fonctionnalité de chiffrement pour SMB 3.0 pour Linux a été introduite dans le noyau 4.11.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="3b1ff-109">Cette fonctionnalité permet le montage du partage de fichiers Azure en local ou à partir d’une autre région Azure.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="3b1ff-110">Au moment de hello du processus de publication, cette fonctionnalité a été tooUbuntu utilisées à partir de 16.04 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="3b1ff-111">Préalables pour le montage d’un partage de fichiers Azure avec Linux et hello package de cifs-utils</span><span class="sxs-lookup"><span data-stu-id="3b1ff-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="3b1ff-112">**Choisir une distribution Linux qui peut avoir des package de cifs-utils hello installé**: Microsoft vous recommande de hello suivant des distributions de Linux dans la galerie d’images Azure hello :</span><span class="sxs-lookup"><span data-stu-id="3b1ff-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="3b1ff-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="3b1ff-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="3b1ff-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="3b1ff-114">RHEL 7+</span></span>
    * <span data-ttu-id="3b1ff-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="3b1ff-115">CentOS 7+</span></span>
    * <span data-ttu-id="3b1ff-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="3b1ff-116">Debian 8</span></span>
    * <span data-ttu-id="3b1ff-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="3b1ff-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="3b1ff-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="3b1ff-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="3b1ff-119"><a id="install-cifs-utils"></a>**Hello cifs-utils installation**: hello cifs-utils peut être installé à l’aide du Gestionnaire de package hello sur la distribution de Linux hello de votre choix.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="3b1ff-120">Sur **Ubuntu** et **basée sur Debian** distributions, utilisez hello `apt-get` Gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="3b1ff-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="3b1ff-121">Sur **RHEL** et **CentOS**, utilisez hello `yum` Gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="3b1ff-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="3b1ff-122">Sur **openSUSE**, utilisez hello `zypper` Gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="3b1ff-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="3b1ff-123">Sur les autres distributions, utilisez le Gestionnaire de package approprié hello ou [une compilation à partir de la source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="3b1ff-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="3b1ff-124">**Décider des autorisations de répertoire/fichier hello du partage de monté hello**: dans les exemples de hello ci-dessous, nous utilisons 0777, toogive lire, écrire et exécuter des autorisations accordées aux utilisateurs de tooall.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="3b1ff-125">Vous pouvez les remplacer par d’autres [autorisations chmod](https://en.wikipedia.org/wiki/Chmod) comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="3b1ff-126">**Nom de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello nom hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="3b1ff-127">**Clé de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello la clé primaire (ou secondaire).</span><span class="sxs-lookup"><span data-stu-id="3b1ff-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="3b1ff-128">Actuellement, les clés SAS ne sont pas prises en charge pour le montage.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="3b1ff-129">**Assurez-vous que le port 445 est ouvert**: SMB communique via le port TCP 445 - Vérifiez toosee si votre pare-feu ne bloque pas les TCP ports 445 à partir de l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="3b1ff-130">Monter hello à la demande avec un partage de fichiers de Azure`mount`</span><span class="sxs-lookup"><span data-stu-id="3b1ff-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="3b1ff-131">**[Installer le package de cifs-utils hello pour votre distribution Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="3b1ff-132">**Créez un dossier pour le point de montage hello**: cela n’importe où sur le système de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="3b1ff-133">**Utilisez hello montage commande toomount hello Azure File share**: n’oubliez pas de tooreplace `<storage-account-name>`, `<share-name>`, et `<storage-account-key>` avec des informations correctes hello.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="3b1ff-134">Lorsque vous avez terminé à l’aide de hello le partage de fichiers Azure, vous pouvez utiliser `sudo umount ./mymountpoint` partage de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="3b1ff-135">Créer un point de montage persistant pour le partage de fichiers Azure hello avec`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="3b1ff-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="3b1ff-136">**[Installer le package de cifs-utils hello pour votre distribution Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="3b1ff-137">**Créez un dossier pour le point de montage hello**: cela n’importe où sur le système de fichiers hello, mais vous avez besoin de chemin d’accès absolu toonote hello du dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="3b1ff-138">Hello, l’exemple suivant crée un dossier sous la racine.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="3b1ff-139">**Hello tooappend suivant trop de ligne de commande de suivante de hello utilisation`/etc/fstab`**: n’oubliez pas de tooreplace `<storage-account-name>`, `<share-name>`, et `<storage-account-key>` avec des informations correctes hello.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="3b1ff-140">Vous pouvez utiliser `sudo mount -a` toomount partage de fichiers Azure hello après la modification `/etc/fstab` au lieu de redémarrer.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="3b1ff-141">Commentaires</span><span class="sxs-lookup"><span data-stu-id="3b1ff-141">Feedback</span></span>
<span data-ttu-id="3b1ff-142">Les utilisateurs Linux, nous souhaitons toohear vous !</span><span class="sxs-lookup"><span data-stu-id="3b1ff-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="3b1ff-143">Hello stockage de fichier Azure pour le groupe d’utilisateurs Linux propose un forum pour vous tooshare commentaires que vous évaluez et adoptez le stockage de fichier sur Linux.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="3b1ff-144">Messagerie [le stockage de fichiers Azure les utilisateurs Linux](mailto:azurefileslinuxusers@microsoft.com) groupe d’utilisateurs toojoin hello.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b1ff-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b1ff-145">Next steps</span></span>
<span data-ttu-id="3b1ff-146">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="3b1ff-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="3b1ff-147">Référence de l’API REST du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="3b1ff-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="3b1ff-148">Comment toouse AzCopy avec le stockage Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3b1ff-148">How toouse AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="3b1ff-149">À l’aide de hello CLI d’Azure avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="3b1ff-149">Using hello Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="3b1ff-150">FAQ</span><span class="sxs-lookup"><span data-stu-id="3b1ff-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="3b1ff-151">Dépannage</span><span class="sxs-lookup"><span data-stu-id="3b1ff-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
