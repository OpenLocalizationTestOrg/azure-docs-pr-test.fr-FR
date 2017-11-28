---
title: "aaaMount stockage de fichier Azure à partir d’une machine virtuelle de Windows Azure | Documents Microsoft"
description: "Stockez le fichier dans le cloud hello avec stockage de fichiers Azure et monter votre partage de fichiers de cloud à partir d’une machine virtuelle Azure (VM)."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="45432-103">Utiliser des partages de fichiers Azure avec des machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="45432-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="45432-104">Vous pouvez utiliser des partages de fichiers Azure comme un moyen toostore et accèdent aux fichiers à partir de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="45432-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="45432-105">Par exemple, vous pouvez stocker un script ou un fichier de configuration que vous souhaitez toutes les tooshare de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="45432-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="45432-106">Dans cette rubrique, nous vous indiquons comment toocreate et montez Azure de partage de fichiers et tooupload et téléchargez des fichiers.</span><span class="sxs-lookup"><span data-stu-id="45432-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="45432-107">Connecter le partage de fichiers tooa d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="45432-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="45432-108">Cette section suppose que vous avez déjà un fichier que vous souhaitez tooconnect à du partage.</span><span class="sxs-lookup"><span data-stu-id="45432-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="45432-109">Si vous devez toocreate une, consultez [créer un partage de fichiers](#create-a-file-share) plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="45432-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="45432-110">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45432-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="45432-111">Dans le menu de gauche hello, cliquez sur **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="45432-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="45432-112">Choisissez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="45432-112">Choose your storage account.</span></span>
4. <span data-ttu-id="45432-113">Bonjour **vue d’ensemble** sous **Services**, sélectionnez **fichiers**.</span><span class="sxs-lookup"><span data-stu-id="45432-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="45432-114">Sélectionnez un partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="45432-114">Select a file share.</span></span>
6. <span data-ttu-id="45432-115">Cliquez sur **Connect** tooopen une page qui affiche la syntaxe de ligne de commande de hello montage hello partage de fichiers Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="45432-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="45432-116">Mettez en surbrillance la syntaxe hello de commande hello et collez-le dans le bloc-notes ou un autre endroit où vous pouvez y accéder facilement.</span><span class="sxs-lookup"><span data-stu-id="45432-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="45432-117">Modifier la valeur principale de hello syntaxe tooremove hello ** > ** et remplacez *[lettre de lecteur]* avec la lettre de lecteur hello (par exemple, **Y:**) où vous souhaitez que le partage de fichiers toomount hello.</span><span class="sxs-lookup"><span data-stu-id="45432-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="45432-118">Se connecter tooyour machine virtuelle et ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="45432-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="45432-119">Coller dans hello modifié la syntaxe de connexion et d’accès **entrée**.</span><span class="sxs-lookup"><span data-stu-id="45432-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="45432-120">Lors de la connexion de hello a été créée, vous obtenez le message de type hello **hello commande s’est terminée avec succès.**</span><span class="sxs-lookup"><span data-stu-id="45432-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="45432-121">Vérifiez la connexion de hello en tapant dans hello lettre tooswitch toothat lecteur et tapez **dir** contenu de hello toosee hello du partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="45432-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="45432-122">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="45432-122">Create a file share</span></span> 
1. <span data-ttu-id="45432-123">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45432-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="45432-124">Dans le menu de gauche hello, cliquez sur **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="45432-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="45432-125">Choisissez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="45432-125">Choose your storage account.</span></span>
4. <span data-ttu-id="45432-126">Bonjour **vue d’ensemble** sous **Services**, sélectionnez **fichiers**.</span><span class="sxs-lookup"><span data-stu-id="45432-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="45432-127">Dans la page du Service de fichiers hello, cliquez sur **+ partage de fichiers** toocreate votre premier fichier partager. \\</span><span class="sxs-lookup"><span data-stu-id="45432-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="45432-128">Renseignez le nom de partage de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="45432-128">Fill in hello file share name.</span></span> <span data-ttu-id="45432-129">Le nom des partages de fichiers peut inclure des lettres minuscules, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="45432-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="45432-130">nom de Hello ne peut pas commencer par un trait d’union, et vous ne pouvez pas utiliser plusieurs traits d’union consécutifs.</span><span class="sxs-lookup"><span data-stu-id="45432-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="45432-131">Remplissage dans une limite sur le fichier de hello quelle taille possible, too5120 go.</span><span class="sxs-lookup"><span data-stu-id="45432-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="45432-132">Cliquez sur **OK** partage de fichiers toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="45432-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="45432-133">Charger des fichiers</span><span class="sxs-lookup"><span data-stu-id="45432-133">Upload files</span></span>
1. <span data-ttu-id="45432-134">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45432-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="45432-135">Dans le menu de gauche hello, cliquez sur **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="45432-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="45432-136">Choisissez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="45432-136">Choose your storage account.</span></span>
4. <span data-ttu-id="45432-137">Bonjour **vue d’ensemble** sous **Services**, sélectionnez **fichiers**.</span><span class="sxs-lookup"><span data-stu-id="45432-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="45432-138">Sélectionnez un partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="45432-138">Select a file share.</span></span>
6. <span data-ttu-id="45432-139">Cliquez sur **télécharger** tooopen hello **télécharger des fichiers** page.</span><span class="sxs-lookup"><span data-stu-id="45432-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="45432-140">Cliquez sur hello dossier icône toobrowse le système de fichiers local pour un tooupload de fichier.</span><span class="sxs-lookup"><span data-stu-id="45432-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="45432-141">Cliquez sur **télécharger** partage de fichiers toohello tooupload hello fichier.</span><span class="sxs-lookup"><span data-stu-id="45432-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="45432-142">Téléchargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="45432-142">Download files</span></span>
1. <span data-ttu-id="45432-143">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45432-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="45432-144">Dans le menu de gauche hello, cliquez sur **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="45432-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="45432-145">Choisissez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="45432-145">Choose your storage account.</span></span>
4. <span data-ttu-id="45432-146">Bonjour **vue d’ensemble** sous **Services**, sélectionnez **fichiers**.</span><span class="sxs-lookup"><span data-stu-id="45432-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="45432-147">Sélectionnez un partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="45432-147">Select a file share.</span></span>
6. <span data-ttu-id="45432-148">Avec le bouton droit sur le fichier de hello et choisissez **télécharger** toodownload il tooyour les ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="45432-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="45432-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45432-149">Next steps</span></span>

<span data-ttu-id="45432-150">Vous pouvez également créer et gérer des partages de fichiers à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45432-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="45432-151">Pour plus d’informations, consultez [Prise en main du stockage de fichiers Azure sur Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="45432-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
