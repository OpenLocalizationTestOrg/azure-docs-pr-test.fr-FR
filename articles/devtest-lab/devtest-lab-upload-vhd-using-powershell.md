---
title: "disque dur virtuel d’aaaUpload fichier tooAzure DevTest Labs, à l’aide de PowerShell | Documents Microsoft"
description: "Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide de PowerShell"
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="77668-103">Télécharger le compte de stockage de toolab du fichier de disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="77668-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="77668-104">Dans Azure DevTest Labs, les fichiers de disque dur virtuel peuvent être utilisé toocreate des images personnalisées, qui sont des ordinateurs virtuels tooprovision utilisé.</span><span class="sxs-lookup"><span data-stu-id="77668-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="77668-105">Hello étapes suivantes vous guident à l’aide de PowerShell tooupload compte de stockage d’un disque dur virtuel fichier tooa du laboratoire.</span><span class="sxs-lookup"><span data-stu-id="77668-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="77668-106">Une fois que vous avez téléchargé votre fichier de disque dur virtuel, hello [étapes section](#next-steps) répertorie certains articles qui expliquent comment toocreate une image personnalisée à partir de hello téléchargé le fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="77668-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="77668-107">Pour plus d’informations sur les disques et les disques durs virtuels dans Azure, consultez [À propos des disques et des VHD pour les machines virtuelles Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="77668-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="77668-108">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="77668-108">Step-by-step instructions</span></span>

<span data-ttu-id="77668-109">les étapes suivantes de Hello parcours vous aide à télécharger un disque dur virtuel du fichier tooAzure DevTest Labs, à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77668-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="77668-110">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="77668-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="77668-111">Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="77668-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="77668-112">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="77668-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="77668-113">Dans le panneau de hello lab, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="77668-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="77668-114">Atelier de hello **Configuration** panneau, sélectionnez **les images personnalisées (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="77668-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="77668-115">Sur hello **les images personnalisées** panneau, sélectionnez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="77668-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="77668-116">Sur hello **image personnalisée** panneau, sélectionnez **disque dur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="77668-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="77668-117">Sur hello **VHD** panneau, sélectionnez **télécharger un disque dur virtuel à l’aide de PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="77668-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Télécharger un disque dur virtuel à l’aide de PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="77668-119">Sur hello **télécharger une image à l’aide de PowerShell** panneau copie hello généré PowerShell script tooa et éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="77668-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="77668-120">Modifier hello **LocalFilePath** paramètre Hello **Add-AzureVhd** applet de commande toopoint toohello emplacement de fichier de disque dur virtuel souhaité tooupload de hello.</span><span class="sxs-lookup"><span data-stu-id="77668-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="77668-121">À l’invite de PowerShell, exécutez hello **Add-AzureVhd** applet de commande (avec hello modifié **LocalFilePath** paramètre).</span><span class="sxs-lookup"><span data-stu-id="77668-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="77668-122">processus Hello de téléchargement d’un fichier de disque dur virtuel peut être longue, en fonction de la taille de hello du fichier de disque dur virtuel hello et votre vitesse de connexion.</span><span class="sxs-lookup"><span data-stu-id="77668-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77668-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77668-123">Next steps</span></span>

- [<span data-ttu-id="77668-124">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="77668-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="77668-125">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="77668-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
