---
title: "Télécharger un fichier de disque dur virtuel vers Azure DevTest Labs avec PowerShell | Microsoft Docs"
description: "Télécharger le fichier de disque dur virtuel dans le compte de stockage du laboratoire avec PowerShell"
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
ms.openlocfilehash: 3c43ef77b8fa10cd6dbd726968264f32f7a3dd0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-powershell"></a><span data-ttu-id="d0c79-103">Télécharger le fichier de disque dur virtuel dans le compte de stockage du laboratoire avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0c79-103">Upload VHD file to lab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="d0c79-104">Dans Azure DevTest Labs, les fichiers de disque dur virtuel peuvent être utilisés pour créer des images personnalisées, qui servent à approvisionner des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d0c79-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="d0c79-105">Les étapes suivantes vous guident lors de l’utilisation de PowerShell pour charger un fichier de disque dur virtuel sur le compte de stockage d’un laboratoire.</span><span class="sxs-lookup"><span data-stu-id="d0c79-105">The following steps walk you through using PowerShell to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="d0c79-106">Une fois que vous avez téléchargé votre fichier de disque dur virtuel, consultez la [section Étapes suivantes](#next-steps) qui répertorie quelques articles qui expliquent comment créer une image personnalisée à partir du fichier de disque dur virtuel téléchargé.</span><span class="sxs-lookup"><span data-stu-id="d0c79-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="d0c79-107">Pour plus d’informations sur les disques et les disques durs virtuels dans Azure, consultez [À propos des disques et des VHD pour les machines virtuelles Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="d0c79-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="d0c79-108">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="d0c79-108">Step-by-step instructions</span></span>

<span data-ttu-id="d0c79-109">Les étapes suivantes vous guident lors du téléchargement d’un fichier de disque dur virtuel dans Azure DevTest Labs avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0c79-109">The following steps walk you through uploading a VHD file to Azure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="d0c79-110">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0c79-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="d0c79-111">Sélectionnez **Plus de services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="d0c79-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="d0c79-112">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="d0c79-112">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="d0c79-113">Dans le panneau du laboratoire, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="d0c79-113">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="d0c79-114">Dans le panneau **Configuration** du laboratoire, sélectionnez **Custom images (VHDs)** (Images personnalisées (disques durs virtuels)).</span><span class="sxs-lookup"><span data-stu-id="d0c79-114">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="d0c79-115">Dans le panneau **Images personnalisées**, sélectionnez **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d0c79-115">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="d0c79-116">Dans le panneau **Image personnalisée**, sélectionnez **Disque dur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="d0c79-116">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="d0c79-117">Dans le panneau **Disque dur virtuel**, sélectionnez **Upload a VHD using PowerShell** (Télécharger un disque dur virtuel à l’aide de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d0c79-117">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Télécharger un disque dur virtuel à l’aide de PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="d0c79-119">Dans le panneau **Charger un disque dur virtuel avec PowerShell**, copiez le script PowerShell généré dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="d0c79-119">On the **Upload an image using PowerShell** blade, copy the generated PowerShell script to a text editor.</span></span>

1. <span data-ttu-id="d0c79-120">Modifiez le paramètre **LocalFilePath** de l’applet de commande **Add-AzureVhd** pour pointer vers l’emplacement du fichier VHD à télécharger.</span><span class="sxs-lookup"><span data-stu-id="d0c79-120">Modify the **LocalFilePath** parameter of the **Add-AzureVhd** cmdlet to point to the location of the VHD file you want to upload.</span></span>

1. <span data-ttu-id="d0c79-121">À l’invite de PowerShell, exécutez l’applet de commande **Add-AzureVhd** (avec le paramètre **LocalFilePath** modifié).</span><span class="sxs-lookup"><span data-stu-id="d0c79-121">At a PowerShell prompt, run the **Add-AzureVhd** cmdlet (with the modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="d0c79-122">Le processus de téléchargement d’un fichier de disque dur virtuel peut durer un certain temps en fonction de sa taille et de votre vitesse de connexion.</span><span class="sxs-lookup"><span data-stu-id="d0c79-122">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0c79-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0c79-123">Next steps</span></span>

- [<span data-ttu-id="d0c79-124">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d0c79-124">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="d0c79-125">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0c79-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
