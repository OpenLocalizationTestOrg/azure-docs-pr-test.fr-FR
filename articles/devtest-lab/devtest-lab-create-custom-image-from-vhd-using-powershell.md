---
title: "Créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell | Microsoft Docs"
description: "Automatiser la création d’une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel avec PowerShell"
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
ms.openlocfilehash: a4729f70aae80a13233fbe96a5d8a56c0c9d01d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="4c143-103">Créer une image personnalisée à partir d’un fichier de disque dur virtuel avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c143-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="4c143-104">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="4c143-104">Step-by-step instructions</span></span>

<span data-ttu-id="4c143-105">La procédure suivante décrit comment créer une image personnalisée à partir d’un fichier de disque dur virtuel avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="4c143-105">The following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="4c143-106">À l’invite de PowerShell, connectez-vous à votre compte Azure avec l’appel suivant à l’applet de commande **Login-AzureRmAccount**.</span><span class="sxs-lookup"><span data-stu-id="4c143-106">At a PowerShell prompt, log in to your Azure account with the following call to the **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="4c143-107">Sélectionnez l’abonnement Azure souhaité en appelant l’applet de commande **Select-AzureRmSubscription**.</span><span class="sxs-lookup"><span data-stu-id="4c143-107">Select the desired Azure subscription by calling the **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="4c143-108">Remplacez l’espace suivant réservé à la variable **$subscriptionId** par un ID d’abonnement Azure valide.</span><span class="sxs-lookup"><span data-stu-id="4c143-108">Replace the following placeholder for the **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="4c143-109">Récupérez l’objet de laboratoire en appelant l’applet de commande **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="4c143-109">Get the lab object by calling the **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="4c143-110">Remplacez les espaces suivants réservés aux variables **$labRg** et **$labName** par les valeurs appropriées pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="4c143-110">Replace the following placeholders for the **$labRg** and **$labName** variables with the appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="4c143-111">Récupérez les valeurs de clé du compte de stockage et du compte de stockage du laboratoire dans l’objet de laboratoire.</span><span class="sxs-lookup"><span data-stu-id="4c143-111">Get the lab storage account and lab storage account key values from the lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="4c143-112">Remplacez l’espace suivant réservé à la variable **$vhdUri** par l’URI vers le fichier VHD chargé.</span><span class="sxs-lookup"><span data-stu-id="4c143-112">Replace the following placeholder for the **$vhdUri** variable with the URI to your uploaded VHD file.</span></span> <span data-ttu-id="4c143-113">Vous pouvez obtenir l’URI du fichier de disque dur virtuel dans le panneau d’objet blob du compte de stockage, dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4c143-113">You can get the VHD file's URI from the storage account's blob blade in the Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify the VHD URI here>'
    ```

1.  <span data-ttu-id="4c143-114">Créez l’image personnalisée avec l’applet de commande **New-AzureRmResourceGroupDeployment**.</span><span class="sxs-lookup"><span data-stu-id="4c143-114">Create the custom image using the **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="4c143-115">Remplacez les espaces suivants réservés aux variables **$customImageName** et **$customImageDescription** par des noms significatifs pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="4c143-115">Replace the following placeholders for the **$customImageName** and **$customImageDescription** variables to meaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify the custom image name>'
    $customImageDescription = '<Specify the custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-to-create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="4c143-116">Script PowerShell pour créer une image personnalisée à partir d’un fichier de disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="4c143-116">PowerShell script to create a custom image from a VHD file</span></span>

<span data-ttu-id="4c143-117">Le script PowerShell suivant peut être utilisé pour créer une image personnalisée à partir d’un fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="4c143-117">The following PowerShell script can be used to create a custom image from a VHD file.</span></span> <span data-ttu-id="4c143-118">Remplacez les espaces réservés (entre crochets) par les valeurs adaptées à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="4c143-118">Replace the placeholders (starting and ending with angle brackets) with the appropriate values for your needs.</span></span> 

```PowerShell
# Log in to your Azure account.  
Login-AzureRmAccount

# Select the desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get the lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get the lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set the URI of the VHD file.  
$vhdUri = '<Specify the VHD URI here>'

# Set the custom image name and description values.
$customImageName = '<Specify the custom image name>'
$customImageDescription = '<Specify the custom image description>'

# Set up the parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create the custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="4c143-119">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="4c143-119">Related blog posts</span></span>

- [<span data-ttu-id="4c143-120">Custom images or formulas? (Images personnalisées ou formules ?)</span><span class="sxs-lookup"><span data-stu-id="4c143-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="4c143-121">Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="4c143-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="4c143-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c143-122">Next steps</span></span>

- [<span data-ttu-id="4c143-123">Ajout d’une machine virtuelle à votre laboratoire</span><span class="sxs-lookup"><span data-stu-id="4c143-123">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
