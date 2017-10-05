---
title: Montage du partage de fichiers Azure via SMB avec MacOS | Microsoft Docs
description: "Découvrez comment monter un partage de fichiers Azure via SMB avec Mac OS."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: bc3d67745afb8bbffe7ec3462e995104daff9632
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="d7524-103">Montage du partage de fichiers Azure via SMB avec MacOS</span><span class="sxs-lookup"><span data-stu-id="d7524-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="d7524-104">[Stockage Fichier Azure](../storage-dotnet-how-to-use-files.md) est un service de Microsoft qui vous permet de créer et d’utiliser des partages de fichiers réseau dans Azure en utilisant la norme industrielle.</span><span class="sxs-lookup"><span data-stu-id="d7524-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="d7524-105">Les partages de fichiers Azure peuvent être montés dans MacOS Sierra (10.12) et El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="d7524-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="d7524-106">Cet article expose deux méthodes de montage d’un partage de fichiers Azure sur MacOS avec l’interface utilisateur Finder et à l’aide de Terminal.</span><span class="sxs-lookup"><span data-stu-id="d7524-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="d7524-107">Avant de monter un partage de fichiers Azure via SMB, il est recommandé de désactiver la signature de paquet SMB.</span><span class="sxs-lookup"><span data-stu-id="d7524-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="d7524-108">Dans le cas contraire, cela risque d’entraîner des dysfonctionnements lors de l’accès au partage de fichiers Azure depuis MacOS.</span><span class="sxs-lookup"><span data-stu-id="d7524-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="d7524-109">Votre connexion SMB est chiffrée. Cela n’affecte donc pas la sécurité de votre connexion.</span><span class="sxs-lookup"><span data-stu-id="d7524-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="d7524-110">À partir du terminal, utilisez les commandes suivantes pour désactiver la signature de paquet SMB, conformément à la[rubrique d’aide Apple sur la désactivation de la signature des paquets SMB](https://support.apple.com/HT205926) :</span><span class="sxs-lookup"><span data-stu-id="d7524-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="d7524-111">Conditions préalables pour le montage d’un partage de fichiers Azure sous MacOS</span><span class="sxs-lookup"><span data-stu-id="d7524-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="d7524-112">**Nom de compte de stockage** : pour monter un partage de fichiers Azure, vous avez besoin du nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d7524-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="d7524-113">**Clé du compte de stockage** : pour monter un partage de fichiers Azure, vous avez besoin de la clé de stockage primaire (ou secondaire).</span><span class="sxs-lookup"><span data-stu-id="d7524-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="d7524-114">Actuellement, les clés SAS ne sont pas prises en charge pour le montage.</span><span class="sxs-lookup"><span data-stu-id="d7524-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="d7524-115">**Assurez-vous que le port 445 est ouvert** : SMB communique via le port TCP 445.</span><span class="sxs-lookup"><span data-stu-id="d7524-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="d7524-116">Sur votre machine client (Mac), vérifiez que votre pare-feu ne bloque pas le port TCP 445.</span><span class="sxs-lookup"><span data-stu-id="d7524-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="d7524-117">Montage d’un partage de fichiers Azure via Finder</span><span class="sxs-lookup"><span data-stu-id="d7524-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="d7524-118">**Ouvrez Finder** : Finder est ouvert par défaut sous MacOS, mais vous pouvez vérifier qu’il s’agit bien de l’application par défaut en cliquant sur l’icône MacOS (illustrée par un visage), dans la barre :</span><span class="sxs-lookup"><span data-stu-id="d7524-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="d7524-119">![L’icône MacOS (visage)](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="d7524-119">![The macOS face icon](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="d7524-120">**Sélectionnez « Se connecter au serveur » dans le Menu « Aller »** : à l’aide du chemin d’accès UNC requis dans les [conditions préalables](#preq), remplacez la double barre oblique inverse (`\\`) par `smb://` et toutes les autres barres obliques inverses (`\`) par des barres obliques normales (`/`).</span><span class="sxs-lookup"><span data-stu-id="d7524-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="d7524-121">Votre lien doit se présenter comme suit : ![la boîte de dialogue « Se connecter au serveur »](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="d7524-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="d7524-122">**Lorsque vous y êtes invité, utilisez le nom du partage et la clé du compte de stockage comme nom d’utilisateur et comme mot de passe** : lorsque vous cliquez sur « Connexion », dans la boîte de dialogue « Se connecter au serveur », vous êtes invité à entrer le nom d’utilisateur et le mot de passe (votre nom d’utilisateur MacOS est automatiquement prérempli).</span><span class="sxs-lookup"><span data-stu-id="d7524-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="d7524-123">Vous avez la possibilité de placer le nom de partage / la clé du compte de stockage dans votre trousseau MacOS.</span><span class="sxs-lookup"><span data-stu-id="d7524-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="d7524-124">**Utilisez le partage de fichiers Azure à votre guise** : après avoir remplacé le nom de partage et la clé du compte de stockage par le nom d’utilisateur et le mot de passe, vous pouvez monter le partage.</span><span class="sxs-lookup"><span data-stu-id="d7524-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="d7524-125">Vous pouvez l’utiliser comme un partage de fichiers / un dossier local normal. Vous pouvez notamment faire glisser et déposer des fichiers dans le partage :</span><span class="sxs-lookup"><span data-stu-id="d7524-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![Une capture instantanée d’un partage de fichiers Azure monté](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="d7524-127">Montage d’un partage de fichiers Azure via Terminal</span><span class="sxs-lookup"><span data-stu-id="d7524-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="d7524-128">Remplacez `<storage-account-name>` par le nom de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d7524-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="d7524-129">Lorsque vous y êtes invité, entrez la clé du compte de stockage comme mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d7524-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="d7524-130">**Utilisez le partage de fichiers Azure à votre guise** : le partage de fichiers Azure est monté sur le point de montage spécifié par la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="d7524-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![Une capture instantanée du partage de fichiers Azure monté](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="d7524-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7524-132">Next steps</span></span>
<span data-ttu-id="d7524-133">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="d7524-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="d7524-134">Rubrique d’aide Apple : connexion au partage de fichiers sur Mac</span><span class="sxs-lookup"><span data-stu-id="d7524-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="d7524-135">FAQ</span><span class="sxs-lookup"><span data-stu-id="d7524-135">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="d7524-136">Résolution des problèmes sur Windows</span><span class="sxs-lookup"><span data-stu-id="d7524-136">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="d7524-137">Résolution des problèmes sur Linux</span><span class="sxs-lookup"><span data-stu-id="d7524-137">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    