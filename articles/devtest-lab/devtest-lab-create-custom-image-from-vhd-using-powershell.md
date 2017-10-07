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
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a>Créer une image personnalisée à partir d’un fichier de disque dur virtuel avec PowerShell

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Instructions pas à pas

Hello étapes suivantes vous aider à créer une image personnalisée à partir d’un fichier de disque dur virtuel à l’aide de PowerShell :

1. À l’invite de PowerShell, ouvrez une session dans tooyour compte Azure avec hello après appel toohello **AzureRmAccount de connexion** applet de commande.  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  Sélectionnez hello souhaité d’abonnement Azure en appelant hello **sélectionnez-AzureRmSubscription** applet de commande. Remplacez hello suivant l’espace réservé pour hello **$subscriptionId** variable avec un ID d’abonnement Azure valide. 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  Obtenir un objet lab de hello en appelant hello **Get-AzureRmResource** applet de commande. Remplacez hello suivant des espaces réservés pour hello **$labRg** et **$labName** variables avec hello appropriées des valeurs pour votre environnement. 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  Obtenir compte de stockage lab hello et compte de stockage lab valeurs de clés à partir de l’objet de laboratoire hello. 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  Remplacez hello suivant l’espace réservé pour hello **$vhdUri** variable avec hello URI tooyour téléchargé le fichier de disque dur virtuel. Vous pouvez obtenir l’URI du fichier de disque dur virtuel hello à partir du panneau d’objets blob du compte de stockage hello Bonjour portail Azure.

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  Créer à l’aide de hello personnalisée hello **New-AzureRmResourceGroupDeployment** applet de commande. Remplacez hello suivant des espaces réservés pour hello **$customImageName** et **$customImageDescription** noms toomeaningful de variables pour votre environnement.

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a>PowerShell script toocreate une image personnalisée à partir d’un fichier de disque dur virtuel

Hello PowerShell script suivant peut être utilisé toocreate une image personnalisée à partir d’un fichier de disque dur virtuel. Remplacer les espaces réservés de hello (début et de fin avec crochets pointus) avec les valeurs appropriées hello à vos besoins. 

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

## <a name="related-blog-posts"></a>Billets de blog connexes

- [Custom images or formulas? (Images personnalisées ou formules ?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Étapes suivantes

- [Ajouter un laboratoire tooyour de machine virtuelle](./devtest-lab-add-vm-with-artifacts.md)
