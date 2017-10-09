---
title: partage de fichiers Azure aaaMount sur SMB avec macOS | Documents Microsoft
description: "Découvrez comment partager des toomount un fichier Azure sur SMB avec macOS."
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
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="168ee-103">Montage du partage de fichiers Azure via SMB avec MacOS</span><span class="sxs-lookup"><span data-stu-id="168ee-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="168ee-104">[Stockage de fichier Azure](../storage-dotnet-how-to-use-files.md) est service de Microsoft qui vous permet de partages de fichiers réseau toocreate et utilisez Bonjour Azure à l’aide de norme industrielle de hello.</span><span class="sxs-lookup"><span data-stu-id="168ee-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="168ee-105">Les partages de fichiers Azure peuvent être montés dans MacOS Sierra (10.12) et El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="168ee-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="168ee-106">Cet article montre deux façons différentes toomount un partage de fichiers Azure sur macOS avec hello l’interface utilisateur de la recherche et à l’aide de hello Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="168ee-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="168ee-107">Avant de monter un partage de fichiers Azure via SMB, il est recommandé de désactiver la signature de paquet SMB.</span><span class="sxs-lookup"><span data-stu-id="168ee-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="168ee-108">Sinon, peut entraîner des performances médiocres lors de l’accès de partage de fichiers Azure hello de macOS.</span><span class="sxs-lookup"><span data-stu-id="168ee-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="168ee-109">Votre connexion SMB est chiffrée, donc cela n’affecte pas la sécurité hello de votre connexion.</span><span class="sxs-lookup"><span data-stu-id="168ee-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="168ee-110">À partir de hello Terminal Server, hello commandes suivantes désactivera la signature des paquets SMB, comme décrit par cet [article du support technique Apple sur la désactivation de la signature de paquet SMB](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="168ee-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="168ee-111">Conditions préalables pour le montage d’un partage de fichiers Azure sous MacOS</span><span class="sxs-lookup"><span data-stu-id="168ee-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="168ee-112">**Nom de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello nom hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="168ee-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="168ee-113">**Clé de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello la clé primaire (ou secondaire).</span><span class="sxs-lookup"><span data-stu-id="168ee-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="168ee-114">Actuellement, les clés SAS ne sont pas prises en charge pour le montage.</span><span class="sxs-lookup"><span data-stu-id="168ee-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="168ee-115">**Assurez-vous que le port 445 est ouvert** : SMB communique via le port TCP 445.</span><span class="sxs-lookup"><span data-stu-id="168ee-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="168ee-116">Sur votre ordinateur client (hello Mac), vérifiez que votre pare-feu ne bloque pas le port TCP 445 de toomake.</span><span class="sxs-lookup"><span data-stu-id="168ee-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="168ee-117">Montage d’un partage de fichiers Azure via Finder</span><span class="sxs-lookup"><span data-stu-id="168ee-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="168ee-118">**Ouvrir le Finder**: Finder est ouvert sur macOS par défaut, mais vous pouvez vous assurer qu’il est hello sélectionné actuellement application en cliquant sur hello « macOS accessibles icône » sur la station d’accueil hello :</span><span class="sxs-lookup"><span data-stu-id="168ee-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="168ee-119">![Hello macOS accessibles icône](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="168ee-119">![hello macOS face icon](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="168ee-120">**Sélectionnez « Se connecter tooServer » à partir de hello « Go » Menu**: à l’aide du chemin d’accès UNC de hello de hello [conditions préalables](#preq), convertir hello début double barre oblique inverse (`\\`) trop`smb://` et toutes les autres barres obliques inverses (`\`) les barres obliques tooforwards (`/`).</span><span class="sxs-lookup"><span data-stu-id="168ee-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="168ee-121">Votre lien doit ressembler à hello suivant : ![boîte de dialogue « Se connecter tooServer » hello](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="168ee-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="168ee-122">**Utilisation hello partage stockage et le nom de clé de compte lorsque vous y êtes invité pour un nom d’utilisateur et un mot de passe**: lorsque vous cliquez sur « Se connecter » sur la boîte de dialogue « Se connecter tooServer » hello, vous demandera d’utilisateur de hello et le mot de passe (il s’agira autopopulated avec votre macOS nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="168ee-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="168ee-123">Vous pouvez hello de placer la clé de compte/nom du stockage hello partage dans votre trousseau Mac OS.</span><span class="sxs-lookup"><span data-stu-id="168ee-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="168ee-124">**Partage de fichiers Azure hello utilisation comme vous le souhaitez**: après la substitution hello partage de stockage et le nom de clé de compte dans pour hello username et password, partage de hello est monté.</span><span class="sxs-lookup"><span data-stu-id="168ee-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="168ee-125">Vous pouvez utiliser cette option comme vous utiliseriez normalement un partage de dossier ou fichier local, y compris le glisser -déplacer des fichiers dans le partage de fichiers hello :</span><span class="sxs-lookup"><span data-stu-id="168ee-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![Une capture instantanée d’un partage de fichiers Azure monté](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="168ee-127">Montage d’un partage de fichiers Azure via Terminal</span><span class="sxs-lookup"><span data-stu-id="168ee-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="168ee-128">Remplacez `<storage-account-name>` par nom de hello de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="168ee-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="168ee-129">Lorsque vous y êtes invité, entrez la clé du compte de stockage comme mot de passe.</span><span class="sxs-lookup"><span data-stu-id="168ee-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="168ee-130">**Partage de fichiers Azure hello utilisation comme vous le souhaitez**: partage de fichiers Azure hello est monté au point de montage hello spécifié par la commande précédente hello.</span><span class="sxs-lookup"><span data-stu-id="168ee-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Un instantané du partage de fichiers Azure hello monté](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="168ee-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="168ee-132">Next steps</span></span>
<span data-ttu-id="168ee-133">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="168ee-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="168ee-134">Article du support technique Apple - comment tooconnect avec partage de fichiers sur votre Mac</span><span class="sxs-lookup"><span data-stu-id="168ee-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="168ee-135">FAQ</span><span class="sxs-lookup"><span data-stu-id="168ee-135">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="168ee-136">Résolution des problèmes sur Windows</span><span class="sxs-lookup"><span data-stu-id="168ee-136">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="168ee-137">Résolution des problèmes sur Linux</span><span class="sxs-lookup"><span data-stu-id="168ee-137">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    