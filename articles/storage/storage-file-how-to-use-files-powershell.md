---
title: aaaHow toouse PowerShell toomanage stockage de fichier Azure | Documents Microsoft
description: "Découvrez le stockage de fichiers Azure toomanage toouse PowerShell."
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
ms.openlocfilehash: 0e30e8796cf8bbf5f9249b26179d5e0f9077c8fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="24e90-103">Comment toouse PowerShell toomanage stockage Azure</span><span class="sxs-lookup"><span data-stu-id="24e90-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="24e90-104">Vous pouvez utiliser Azure PowerShell toocreate et gérer des partages de fichiers.</span><span class="sxs-lookup"><span data-stu-id="24e90-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="24e90-105">Installer les applets de commande PowerShell hello pour le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="24e90-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="24e90-106">tooprepare toouse PowerShell, téléchargez et installez les applets de commande PowerShell Azure hello.</span><span class="sxs-lookup"><span data-stu-id="24e90-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="24e90-107">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) Pourquoi installer instructions d’installation et de point.</span><span class="sxs-lookup"><span data-stu-id="24e90-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="24e90-108">Il est recommandé de télécharger et installer ou mettre à niveau du module Azure PowerShell toohello plus récent.</span><span class="sxs-lookup"><span data-stu-id="24e90-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="24e90-109">Ouvrez une fenêtre Azure PowerShell en cliquant sur **Démarrer** et en saisissant **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="24e90-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="24e90-110">fenêtre de PowerShell Hello charge module Azure Powershell de hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="24e90-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="24e90-111">Création d'un contexte pour votre compte de stockage et votre clé</span><span class="sxs-lookup"><span data-stu-id="24e90-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="24e90-112">Créer un contexte de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="24e90-112">Create hello storage account context.</span></span> <span data-ttu-id="24e90-113">contexte de Hello encapsule la clé de compte et le nom du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="24e90-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="24e90-114">Pour obtenir des instructions sur la copie de votre clé de compte à partir de hello [portail Azure](https://portal.azure.com), consultez [clés d’accès afficher et copier](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="24e90-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="24e90-115">Remplacez `storage-account-name` et `storage-account-key` avec votre nom de compte de stockage et de la clé Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="24e90-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="24e90-116">Création d’un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="24e90-116">Create a new file share</span></span>
<span data-ttu-id="24e90-117">Créer un nouveau partage hello, nommé `logs`.</span><span class="sxs-lookup"><span data-stu-id="24e90-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="24e90-118">Vous disposez désormais d’un partage de fichier dans le stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="24e90-118">You now have a file share in File storage.</span></span> <span data-ttu-id="24e90-119">Nous allons maintenant ajouter un répertoire et un fichier.</span><span class="sxs-lookup"><span data-stu-id="24e90-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24e90-120">nom de Hello de votre partage de fichiers doit être tout en minuscules.</span><span class="sxs-lookup"><span data-stu-id="24e90-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="24e90-121">Pour plus d’informations sur la façon de nommer des partages de fichiers et des fichiers, consultez la rubrique [Affectation de noms et références aux partages, répertoires, fichiers et métadonnées](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="24e90-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="24e90-122">Créez un répertoire dans le partage de fichiers hello</span><span class="sxs-lookup"><span data-stu-id="24e90-122">Create a directory in hello file share</span></span>
<span data-ttu-id="24e90-123">Créez un répertoire dans le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="24e90-123">Create a directory in hello share.</span></span> <span data-ttu-id="24e90-124">Dans l’exemple suivant de hello, hello se nomme `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="24e90-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="24e90-125">Télécharger un répertoire toohello de fichier local</span><span class="sxs-lookup"><span data-stu-id="24e90-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="24e90-126">Télécharger un répertoire toohello de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="24e90-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="24e90-127">exemple Hello télécharge un fichier à partir de `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="24e90-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="24e90-128">Modifier le chemin d’accès du fichier hello pour qu’il pointe tooa de fichier valide sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="24e90-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="24e90-129">Liste des fichiers dans le répertoire de hello hello</span><span class="sxs-lookup"><span data-stu-id="24e90-129">List hello files in hello directory</span></span>
<span data-ttu-id="24e90-130">fichier hello toosee répertoire de hello, vous pouvez répertorier tous les fichiers du répertoire hello.</span><span class="sxs-lookup"><span data-stu-id="24e90-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="24e90-131">Cette commande retourne des sous-répertoires et fichiers de hello (le cas échéant) dans le répertoire de CustomLogs hello.</span><span class="sxs-lookup"><span data-stu-id="24e90-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="24e90-132">Get-AzureStorageFile renvoie une liste de fichiers et de répertoires pour répertoire vers lequel l’objet est transmis.</span><span class="sxs-lookup"><span data-stu-id="24e90-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="24e90-133">« Get-AzureStorageFile-partager $s » retourne une liste de fichiers et de répertoires dans le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="24e90-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="24e90-134">tooget une liste de fichiers dans un sous-répertoire, vous avez toopass hello sous-répertoire tooGet-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="24e90-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="24e90-135">C’est ce que cela fait : hello première partie de commande hello toohello canal retourne une instance de répertoire du sous-répertoire de hello CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="24e90-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="24e90-136">Puis, qui est passée à Get-AzureStorageFile, qui retourne les fichiers hello et des répertoires dans CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="24e90-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="24e90-137">Copie des fichiers</span><span class="sxs-lookup"><span data-stu-id="24e90-137">Copy files</span></span>
<span data-ttu-id="24e90-138">Depuis la version 0.9.7 d’Azure PowerShell, vous pouvez copier un fichier de tooanother, un objet blob tooa de fichier ou un objet blob tooa fichier.</span><span class="sxs-lookup"><span data-stu-id="24e90-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="24e90-139">Ci-dessous, nous allons montrer comment tooperform ces copier opérations à l’aide des applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24e90-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="24e90-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24e90-140">Next steps</span></span>
<span data-ttu-id="24e90-141">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="24e90-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="24e90-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="24e90-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="24e90-143">Dépannage</span><span class="sxs-lookup"><span data-stu-id="24e90-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)