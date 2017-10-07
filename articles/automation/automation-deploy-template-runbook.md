---
title: "aaaDeploy un modèle Azure Resource Manager dans un runbook Azure Automation | Documents Microsoft"
description: "Comment toodeploy un modèle de gestionnaire de ressources Azure stockée dans le stockage Azure à partir d’un runbook"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powerShell, runbook, json, azure automation
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="59bee-104">Déployer un modèle Azure Resource Manager dans un runbook PowerShell Azure Automation</span><span class="sxs-lookup"><span data-stu-id="59bee-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="59bee-105">Vous pouvez écrire un [runbook PowerShell Azure Automation](automation-first-runbook-textual-powershell.md) qui déploie une ressource Azure en utilisant un [modèle Azure Resource Manager](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="59bee-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="59bee-106">Ainsi, vous pouvez automatiser le déploiement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="59bee-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="59bee-107">Vous pouvez gérer vos modèles Resource Manager dans un emplacement central et sécurisé, tel que Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="59bee-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="59bee-108">Dans cette rubrique, nous créons un runbook PowerShell qui utilise un modèle de gestionnaire de ressources stocké dans [Azure Storage](../storage/common/storage-introduction.md) toodeploy un nouveau compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="59bee-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) toodeploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59bee-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="59bee-109">Prerequisites</span></span>

<span data-ttu-id="59bee-110">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="59bee-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="59bee-111">Abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="59bee-111">Azure subscription.</span></span> <span data-ttu-id="59bee-112">Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[créer un compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="59bee-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="59bee-113">[Compte Automation](automation-sec-configure-azure-runas-account.md) toohold hello runbook et authentifier les ressources tooAzure.</span><span class="sxs-lookup"><span data-stu-id="59bee-113">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="59bee-114">Ce compte doit avoir l’autorisation toostart et arrêter l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="59bee-114">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="59bee-115">[Compte de stockage Azure](../storage/common/storage-create-storage-account.md) dans le modèle de gestionnaire de ressources hello toostore</span><span class="sxs-lookup"><span data-stu-id="59bee-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which toostore hello Resource Manager template</span></span>
* <span data-ttu-id="59bee-116">Azure Powershell installé sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="59bee-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="59bee-117">Consultez [installer et configurer Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) pour plus d’informations sur la façon tooget Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59bee-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-resource-manager-template"></a><span data-ttu-id="59bee-118">Créer le modèle de gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="59bee-118">Create hello Resource Manager template</span></span>

<span data-ttu-id="59bee-119">Pour cet exemple, nous utilisons un modèle Resource Manager qui déploie un nouveau compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="59bee-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="59bee-120">Dans un éditeur de texte, copiez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="59bee-120">In a text editor, copy hello following text:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

<span data-ttu-id="59bee-121">Enregistrer le fichier de hello localement sous `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="59bee-121">Save hello file locally as `TemplateTest.json`.</span></span>

## <a name="save-hello-resource-manager-template-in-azure-storage"></a><span data-ttu-id="59bee-122">Enregistrer le modèle de gestionnaire de ressources hello dans le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="59bee-122">Save hello Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="59bee-123">Maintenant, nous utiliser PowerShell toocreate un partage de fichiers de stockage Azure et télécharger hello `TemplateTest.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="59bee-123">Now we use PowerShell toocreate an Azure Storage file share and upload hello `TemplateTest.json` file.</span></span>
<span data-ttu-id="59bee-124">Pour obtenir des instructions sur le partage toocreate un fichier et télécharger un fichier Bonjour portail Azure, consultez [prise en main avec un stockage de fichier Azure sur Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="59bee-124">For instructions on how toocreate a file share and upload a file in hello Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="59bee-125">Lancez PowerShell sur votre ordinateur local et exécutez hello suivant de commandes toocreate un partage de fichiers et partage de fichiers toothat hello Gestionnaire de ressources du modèle.</span><span class="sxs-lookup"><span data-stu-id="59bee-125">Launch PowerShell on your local machine, and run hello following commands toocreate a file share and upload hello Resource Manager template toothat file share.</span></span>

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a><span data-ttu-id="59bee-126">Créer le script du runbook PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="59bee-126">Create hello PowerShell runbook script</span></span>

<span data-ttu-id="59bee-127">Maintenant nous créons un script PowerShell qui obtient hello `TemplateTest.json` à partir du stockage Azure et déploie hello modèle toocreate un nouveau compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="59bee-127">Now we create a PowerShell script that gets hello `TemplateTest.json` file from Azure Storage and deploys hello template toocreate a new Azure Storage account.</span></span>

<span data-ttu-id="59bee-128">Dans un éditeur de texte, collez hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="59bee-128">In a text editor, paste hello following text:</span></span>

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="59bee-129">Enregistrer le fichier de hello localement sous `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="59bee-129">Save hello file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a><span data-ttu-id="59bee-130">Importer et publier le runbook de hello dans votre compte Azure Automation</span><span class="sxs-lookup"><span data-stu-id="59bee-130">Import and publish hello runbook into your Azure Automation account</span></span>

<span data-ttu-id="59bee-131">Maintenant nous utiliser PowerShell tooimport hello runbook dans votre compte Azure Automation et puis publier hello runbook.</span><span class="sxs-lookup"><span data-stu-id="59bee-131">Now we use PowerShell tooimport hello runbook into your Azure Automation account, and then publish hello runbook.</span></span>
<span data-ttu-id="59bee-132">Pour plus d’informations sur la façon tooimport et publier un runbook Bonjour portail Azure, consultez [création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="59bee-132">For information about how tooimport and publish a runbook in hello Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="59bee-133">tooimport `DeployTemplate.ps1` dans votre compte Automation en tant qu’un runbook PowerShell, exécutez hello suivant de commandes PowerShell :</span><span class="sxs-lookup"><span data-stu-id="59bee-133">tooimport `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run hello following PowerShell commands:</span></span>

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a><span data-ttu-id="59bee-134">Démarrer hello runbook</span><span class="sxs-lookup"><span data-stu-id="59bee-134">Start hello runbook</span></span>

<span data-ttu-id="59bee-135">Maintenant nous allons commencer hello runbook par appel hello [AzureRmAutomationRunbook de début](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="59bee-135">Now we start hello runbook by calling hello [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="59bee-136">Pour plus d’informations sur comment toostart un runbook dans hello portail Azure, consultez [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="59bee-136">For information about how toostart a runbook in hello Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="59bee-137">Exécutez hello suivant les commandes dans la console PowerShell hello :</span><span class="sxs-lookup"><span data-stu-id="59bee-137">Run hello following commands in hello PowerShell console:</span></span>

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="59bee-138">Hello s’exécute le runbook, et vous pouvez vérifier son état en exécutant `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="59bee-138">hello runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="59bee-139">Hello runbook Obtient le modèle de gestionnaire de ressources hello et l’utilise toodeploy un nouveau compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="59bee-139">hello runbook gets hello Resource Manager template and uses it toodeploy a new Azure Storage account.</span></span>
<span data-ttu-id="59bee-140">Vous pouvez voir que le nouveau compte de stockage hello a été créé en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="59bee-140">You can see that hello new storage account was created by running hello following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="59bee-141">Résumé</span><span class="sxs-lookup"><span data-stu-id="59bee-141">Summary</span></span>

<span data-ttu-id="59bee-142">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="59bee-142">That's it!</span></span> <span data-ttu-id="59bee-143">Maintenant vous pouvez utiliser Azure Automation et Azure Storage et Gestionnaire de ressources modèles toodeploy toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="59bee-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates toodeploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59bee-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59bee-144">Next steps</span></span>

* <span data-ttu-id="59bee-145">toolearn savoir plus sur les modèles du Gestionnaire de ressources, consultez [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="59bee-145">toolearn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="59bee-146">tooget a démarré avec le stockage Azure, consultez [Introduction tooAzure stockage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59bee-146">tooget started with Azure Storage, see [Introduction tooAzure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="59bee-147">toofind autres runbooks Azure Automation utiles, consultez [Runbook et module galeries pour Azure Automation](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="59bee-147">toofind other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="59bee-148">toofind autres modèles de gestionnaire de ressources utiles, consultez [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="59bee-148">toofind other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

