---
title: "aaaUpload disque dur virtuel du fichier tooAzure DevTest Labs, à l’aide de AzCopy | Documents Microsoft"
description: "Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide d’AzCopy"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="cdf92-103">Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide d’AzCopy</span><span class="sxs-lookup"><span data-stu-id="cdf92-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="cdf92-104">Dans Azure DevTest Labs, les fichiers de disque dur virtuel peuvent être utilisé toocreate des images personnalisées, qui sont des ordinateurs virtuels tooprovision utilisé.</span><span class="sxs-lookup"><span data-stu-id="cdf92-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="cdf92-105">Hello suit vous guide à l’aide de tooupload d’utilitaire de ligne de commande hello AzCopy compte de stockage d’un disque dur virtuel fichier tooa du laboratoire.</span><span class="sxs-lookup"><span data-stu-id="cdf92-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="cdf92-106">Une fois que vous avez téléchargé votre fichier de disque dur virtuel, hello [étapes section](#next-steps) répertorie certains articles qui expliquent comment toocreate une image personnalisée à partir de hello téléchargé le fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="cdf92-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="cdf92-107">Pour plus d’informations sur les disques et les disques durs virtuels dans Azure, consultez [À propos des disques et des VHD pour les machines virtuelles Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="cdf92-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="cdf92-108">L’utilitaire de ligne de commande AzCopy fonctionne exclusivement sur Windows.</span><span class="sxs-lookup"><span data-stu-id="cdf92-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="cdf92-109">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="cdf92-109">Step-by-step instructions</span></span>

<span data-ttu-id="cdf92-110">Hello après le parcours des étapes vous aide à télécharger un disque dur virtuel du fichier à l’aide de tooAzure DevTest Labs [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="cdf92-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="cdf92-111">Obtenir le nom de hello de du laboratoire hello compte de stockage à l’aide de hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="cdf92-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="cdf92-112">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="cdf92-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="cdf92-113">Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="cdf92-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="cdf92-114">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="cdf92-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="cdf92-115">Dans le panneau de hello lab, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="cdf92-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="cdf92-116">Atelier de hello **Configuration** panneau, sélectionnez **les images personnalisées (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="cdf92-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="cdf92-117">Sur hello **les images personnalisées** panneau, sélectionnez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cdf92-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="cdf92-118">Sur hello **image personnalisée** panneau, sélectionnez **disque dur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="cdf92-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="cdf92-119">Sur hello **VHD** panneau, sélectionnez **télécharger un disque dur virtuel à l’aide de PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="cdf92-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Télécharger un disque dur virtuel à l’aide de PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="cdf92-121">Hello **télécharger une image à l’aide de PowerShell** panneau affiche un appel toohello **Add-AzureVhd** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cdf92-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="cdf92-122">Hello du premier paramètre (*Destination*) contient hello URI pour un conteneur d’objets blob (*télécharge*) Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="cdf92-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="cdf92-123">Prenez note de hello complet des URI qu’il est utilisé dans les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="cdf92-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="cdf92-124">Téléchargez le fichier de disque dur virtuel de hello à l’aide de AzCopy :</span><span class="sxs-lookup"><span data-stu-id="cdf92-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="cdf92-125">[Téléchargez et installez la version la plus récente de AzCopy hello](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="cdf92-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="cdf92-126">Ouvrez une fenêtre de commande et accédez de répertoire d’installation toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="cdf92-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="cdf92-127">Si vous le souhaitez, vous pouvez ajouter le chemin d’accès de hello AzCopy installation emplacement tooyour système.</span><span class="sxs-lookup"><span data-stu-id="cdf92-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="cdf92-128">Par défaut, AzCopy est installé toohello suivant active :</span><span class="sxs-lookup"><span data-stu-id="cdf92-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="cdf92-129">À l’aide de hello conteneur compte de stockage blob et de clé URI, exécutez hello suivant de commande à l’invite de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="cdf92-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="cdf92-130">Hello *vhdFileName* valeur doit toobe entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="cdf92-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="cdf92-131">processus Hello de téléchargement d’un fichier de disque dur virtuel peut être longue, en fonction de la taille de hello du fichier de disque dur virtuel hello et votre vitesse de connexion.</span><span class="sxs-lookup"><span data-stu-id="cdf92-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="cdf92-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cdf92-132">Next steps</span></span>

- [<span data-ttu-id="cdf92-133">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="cdf92-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="cdf92-134">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdf92-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)