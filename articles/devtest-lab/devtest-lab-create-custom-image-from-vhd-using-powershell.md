---
title: "aaaCreate une image personnalisée de Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de PowerShell | Documents Microsoft"
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
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="f3dba-103">Créer une image personnalisée à partir d’un fichier de disque dur virtuel avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3dba-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="f3dba-104">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="f3dba-104">Step-by-step instructions</span></span>

<span data-ttu-id="f3dba-105">Hello étapes suivantes vous aider à créer une image personnalisée à partir d’un fichier de disque dur virtuel à l’aide de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f3dba-105">hello following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="f3dba-106">À l’invite de PowerShell, ouvrez une session dans tooyour compte Azure avec hello après appel toohello **AzureRmAccount de connexion** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f3dba-106">At a PowerShell prompt, log in tooyour Azure account with hello following call toohello **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="f3dba-107">Sélectionnez hello souhaité d’abonnement Azure en appelant hello **sélectionnez-AzureRmSubscription** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f3dba-107">Select hello desired Azure subscription by calling hello **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="f3dba-108">Remplacez hello suivant l’espace réservé pour hello **$subscriptionId** variable avec un ID d’abonnement Azure valide.</span><span class="sxs-lookup"><span data-stu-id="f3dba-108">Replace hello following placeholder for hello **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="f3dba-109">Obtenir un objet lab de hello en appelant hello **Get-AzureRmResource** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f3dba-109">Get hello lab object by calling hello **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="f3dba-110">Remplacez hello suivant des espaces réservés pour hello **$labRg** et **$labName** variables avec hello appropriées des valeurs pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="f3dba-110">Replace hello following placeholders for hello **$labRg** and **$labName** variables with hello appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="f3dba-111">Obtenir compte de stockage lab hello et compte de stockage lab valeurs de clés à partir de l’objet de laboratoire hello.</span><span class="sxs-lookup"><span data-stu-id="f3dba-111">Get hello lab storage account and lab storage account key values from hello lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="f3dba-112">Remplacez hello suivant l’espace réservé pour hello **$vhdUri** variable avec hello URI tooyour téléchargé le fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="f3dba-112">Replace hello following placeholder for hello **$vhdUri** variable with hello URI tooyour uploaded VHD file.</span></span> <span data-ttu-id="f3dba-113">Vous pouvez obtenir l’URI du fichier de disque dur virtuel hello à partir du panneau d’objets blob du compte de stockage hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f3dba-113">You can get hello VHD file's URI from hello storage account's blob blade in hello Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  <span data-ttu-id="f3dba-114">Créer à l’aide de hello personnalisée hello **New-AzureRmResourceGroupDeployment** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f3dba-114">Create hello custom image using hello **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="f3dba-115">Remplacez hello suivant des espaces réservés pour hello **$customImageName** et **$customImageDescription** noms toomeaningful de variables pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="f3dba-115">Replace hello following placeholders for hello **$customImageName** and **$customImageDescription** variables toomeaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="f3dba-116">PowerShell script toocreate une image personnalisée à partir d’un fichier de disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="f3dba-116">PowerShell script toocreate a custom image from a VHD file</span></span>

<span data-ttu-id="f3dba-117">Hello PowerShell script suivant peut être utilisé toocreate une image personnalisée à partir d’un fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="f3dba-117">hello following PowerShell script can be used toocreate a custom image from a VHD file.</span></span> <span data-ttu-id="f3dba-118">Remplacer les espaces réservés de hello (début et de fin avec crochets pointus) avec les valeurs appropriées hello à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="f3dba-118">Replace hello placeholders (starting and ending with angle brackets) with hello appropriate values for your needs.</span></span> 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="f3dba-119">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="f3dba-119">Related blog posts</span></span>

- [<span data-ttu-id="f3dba-120">Custom images or formulas? (Images personnalisées ou formules ?)</span><span class="sxs-lookup"><span data-stu-id="f3dba-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="f3dba-121">Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="f3dba-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="f3dba-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3dba-122">Next steps</span></span>

- [<span data-ttu-id="f3dba-123">Ajouter un laboratoire tooyour de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f3dba-123">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
