---
title: "Télécharger un fichier de disque dur virtuel vers Azure DevTest Labs à l’aide d’AzCopy | Microsoft Docs"
description: "Télécharger un fichier de disque dur virtuel dans le compte de stockage d’un laboratoire avec AzCopy"
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
ms.openlocfilehash: a4f43354740d9f17570932b0b9c753f46d67dc33
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a><span data-ttu-id="a58dd-103">Télécharger un fichier de disque dur virtuel dans le compte de stockage d’un laboratoire avec AzCopy</span><span class="sxs-lookup"><span data-stu-id="a58dd-103">Upload VHD file to lab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="a58dd-104">Dans Azure DevTest Labs, les fichiers de disque dur virtuel peuvent être utilisés pour créer des images personnalisées, qui servent à approvisionner des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a58dd-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="a58dd-105">Les étapes suivantes vous guident lors de l’utilisation de l’utilitaire de ligne de commande AzCopy pour télécharger un fichier de disque dur virtuel pour le compte de stockage d’un laboratoire.</span><span class="sxs-lookup"><span data-stu-id="a58dd-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="a58dd-106">Une fois que vous avez téléchargé votre fichier de disque dur virtuel, consultez la [section Étapes suivantes](#next-steps) qui répertorie quelques articles qui expliquent comment créer une image personnalisée à partir du fichier de disque dur virtuel téléchargé.</span><span class="sxs-lookup"><span data-stu-id="a58dd-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="a58dd-107">Pour plus d’informations sur les disques et les disques durs virtuels dans Azure, consultez [À propos des disques et des VHD pour les machines virtuelles Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="a58dd-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="a58dd-108">L’utilitaire de ligne de commande AzCopy fonctionne exclusivement sur Windows.</span><span class="sxs-lookup"><span data-stu-id="a58dd-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="a58dd-109">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="a58dd-109">Step-by-step instructions</span></span>

<span data-ttu-id="a58dd-110">Les étapes suivantes vous guident lors du téléchargement d’un fichier de disque dur virtuel dans Azure DevTest Labs à l’aide d’[AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="a58dd-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="a58dd-111">Obtenez le nom du compte de stockage du laboratoire à l’aide du portail Azure :</span><span class="sxs-lookup"><span data-stu-id="a58dd-111">Get the name of the lab's storage account using the Azure portal:</span></span>

1. <span data-ttu-id="a58dd-112">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a58dd-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="a58dd-113">Sélectionnez **Plus de services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="a58dd-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="a58dd-114">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="a58dd-114">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="a58dd-115">Dans le panneau du laboratoire, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="a58dd-115">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="a58dd-116">Dans le panneau **Configuration** du laboratoire, sélectionnez **Custom images (VHDs)** (Images personnalisées (disques durs virtuels)).</span><span class="sxs-lookup"><span data-stu-id="a58dd-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="a58dd-117">Dans le panneau **Images personnalisées**, sélectionnez **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a58dd-117">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="a58dd-118">Dans le panneau **Image personnalisée**, sélectionnez **Disque dur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="a58dd-118">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="a58dd-119">Dans le panneau **Disque dur virtuel**, sélectionnez **Upload a VHD using PowerShell** (Télécharger un disque dur virtuel à l’aide de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a58dd-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Télécharger un disque dur virtuel à l’aide de PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="a58dd-121">Le panneau **Upload an image using PowerShell** (Télécharger une image à l’aide de PowerShell) affiche un appel à l’applet de commande **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="a58dd-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="a58dd-122">Le premier paramètre (*Destination*) contient l’URI d’un conteneur d’objets blob (*uploads*) au format suivant :</span><span class="sxs-lookup"><span data-stu-id="a58dd-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="a58dd-123">Prenez note de l’URI complet, car vous en aurez besoin dans des étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="a58dd-123">Make note of the full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="a58dd-124">Téléchargez le fichier de disque dur virtuel à l’aide d’AzCopy :</span><span class="sxs-lookup"><span data-stu-id="a58dd-124">Upload the VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="a58dd-125">[Téléchargez et installez la dernière version d’AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="a58dd-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="a58dd-126">Ouvrez une fenêtre Commande et naviguez jusqu’au répertoire d’installation d’AzCopy.</span><span class="sxs-lookup"><span data-stu-id="a58dd-126">Open a command window and navigate to the AzCopy installation directory.</span></span> <span data-ttu-id="a58dd-127">Si vous le souhaitez, vous pouvez ajouter l’emplacement d’installation d’AzCopy au chemin de votre système.</span><span class="sxs-lookup"><span data-stu-id="a58dd-127">Optionally, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="a58dd-128">Par défaut, AzCopy est installé dans le répertoire suivant :</span><span class="sxs-lookup"><span data-stu-id="a58dd-128">By default, AzCopy is installed to the following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="a58dd-129">À l’aide de la clé du compte de stockage et de l’URI du conteneur d’objets blob, exécutez la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="a58dd-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span></span> <span data-ttu-id="a58dd-130">La valeur *vhdFileName* doit être entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="a58dd-130">The *vhdFileName* value needs to be in quotes.</span></span> <span data-ttu-id="a58dd-131">Le processus de téléchargement d’un fichier de disque dur virtuel peut durer un certain temps en fonction de sa taille et de votre vitesse de connexion.</span><span class="sxs-lookup"><span data-stu-id="a58dd-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="a58dd-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a58dd-132">Next steps</span></span>

- [<span data-ttu-id="a58dd-133">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="a58dd-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="a58dd-134">Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a58dd-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)