---
title: "Déployer un modèle Azure Resource Manager dans un runbook Azure Automation | Microsoft Docs"
description: "Comment déployer un modèle Azure Resource Manager stocké dans Stockage Azure à partir d’un runbook"
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
ms.openlocfilehash: e511eee2f9eac3969b15ad3d45558dc7034f330a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="4c9ee-104">Déployer un modèle Azure Resource Manager dans un runbook PowerShell Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4c9ee-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="4c9ee-105">Vous pouvez écrire un [runbook PowerShell Azure Automation](automation-first-runbook-textual-powershell.md) qui déploie une ressource Azure en utilisant un [modèle Azure Resource Manager](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="4c9ee-106">Ainsi, vous pouvez automatiser le déploiement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="4c9ee-107">Vous pouvez gérer vos modèles Resource Manager dans un emplacement central et sécurisé, tel que Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="4c9ee-108">Dans cette rubrique, nous créons un runbook PowerShell qui utilise un modèle Resource Manager stocké dans [Stockage Azure](../storage/common/storage-introduction.md) pour déployer un nouveau compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) to deploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c9ee-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4c9ee-109">Prerequisites</span></span>

<span data-ttu-id="4c9ee-110">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4c9ee-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="4c9ee-111">Abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-111">Azure subscription.</span></span> <span data-ttu-id="4c9ee-112">Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[créer un compte gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="4c9ee-113">[compte Automation](automation-sec-configure-azure-runas-account.md) pour le stockage du Runbook et l’authentification auprès des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-113">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="4c9ee-114">Ce compte doit avoir l’autorisation de démarrer et d’arrêter la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-114">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="4c9ee-115">[Compte de stockage Azure](../storage/common/storage-create-storage-account.md) dans lequel stocker le modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c9ee-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which to store the Resource Manager template</span></span>
* <span data-ttu-id="4c9ee-116">Azure Powershell installé sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="4c9ee-117">Pour plus d'informations sur l’obtention d’Azure PowerShell, consultez la section [Installation et configuration d'Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-resource-manager-template"></a><span data-ttu-id="4c9ee-118">Créer le modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c9ee-118">Create the Resource Manager template</span></span>

<span data-ttu-id="4c9ee-119">Pour cet exemple, nous utilisons un modèle Resource Manager qui déploie un nouveau compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="4c9ee-120">Dans un éditeur de texte, copiez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="4c9ee-120">In a text editor, copy the following text:</span></span>

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

<span data-ttu-id="4c9ee-121">Enregistrez le fichier localement sous le nom `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-121">Save the file locally as `TemplateTest.json`.</span></span>

## <a name="save-the-resource-manager-template-in-azure-storage"></a><span data-ttu-id="4c9ee-122">Enregistrer le modèle Resource Manager dans Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="4c9ee-122">Save the Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="4c9ee-123">Maintenant, nous allons utiliser PowerShell pour créer un partage de fichiers Stockage Azure et charger le fichier `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-123">Now we use PowerShell to create an Azure Storage file share and upload the `TemplateTest.json` file.</span></span>
<span data-ttu-id="4c9ee-124">Pour obtenir des instructions sur la création d’un partage de fichier et sur le chargement d’un fichier sur le portail Azure, consultez [Bien démarrer avec le stockage de fichiers Azure sur Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-124">For instructions on how to create a file share and upload a file in the Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="4c9ee-125">Lancez PowerShell sur votre ordinateur local et exécutez les commandes suivantes pour créer un partage de fichiers et y charger le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-125">Launch PowerShell on your local machine, and run the following commands to create a file share and upload the Resource Manager template to that file share.</span></span>

```powershell
# Login to Azure
Login-AzureRmAccount

# Get the access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using the first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add the TemplateTest.json file to the new file share
# "TemplatePath" is the path where you saved the TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-the-powershell-runbook-script"></a><span data-ttu-id="4c9ee-126">Créer le script de runbook PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c9ee-126">Create the PowerShell runbook script</span></span>

<span data-ttu-id="4c9ee-127">Nous allons maintenant créer un script PowerShell qui récupère le fichier `TemplateTest.json` de Stockage Azure et déploie le modèle pour créer un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-127">Now we create a PowerShell script that gets the `TemplateTest.json` file from Azure Storage and deploys the template to create a new Azure Storage account.</span></span>

<span data-ttu-id="4c9ee-128">Dans un éditeur de texte, collez le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="4c9ee-128">In a text editor, paste the following text:</span></span>

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



# Authenticate to Azure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set the parameter values for the Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy the storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="4c9ee-129">Enregistrez le fichier localement sous le nom `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-129">Save the file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-the-runbook-into-your-azure-automation-account"></a><span data-ttu-id="4c9ee-130">Importer et publier le runbook dans votre compte Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4c9ee-130">Import and publish the runbook into your Azure Automation account</span></span>

<span data-ttu-id="4c9ee-131">Nous allons maintenant utiliser PowerShell pour importer le runbook dans votre compte Azure Automation, puis publier le runbook.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-131">Now we use PowerShell to import the runbook into your Azure Automation account, and then publish the runbook.</span></span>
<span data-ttu-id="4c9ee-132">Pour plus d’informations sur la façon d’importer et de publier un runbook dans le portail Azure, consultez [Création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-132">For information about how to import and publish a runbook in the Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="4c9ee-133">Pour importer `DeployTemplate.ps1` dans votre compte Automation en tant que runbook PowerShell, exécutez les commandes PowerShell suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c9ee-133">To import `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run the following PowerShell commands:</span></span>

```powershell
# MyPath is the path where you saved DeployTemplate.ps1
# MyResourceGroup is the name of the Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is the name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish the runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-the-runbook"></a><span data-ttu-id="4c9ee-134">Démarrer le runbook</span><span class="sxs-lookup"><span data-stu-id="4c9ee-134">Start the runbook</span></span>

<span data-ttu-id="4c9ee-135">Maintenant, nous démarrons le runbook en appelant l’applet de commande [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-135">Now we start the runbook by calling the [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="4c9ee-136">Pour plus d’informations sur la façon de démarrer un runbook dans le portail Azure, consultez [Démarrage d’un Runbook dans Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-136">For information about how to start a runbook in the Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="4c9ee-137">Dans la console PowerShell, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c9ee-137">Run the following commands in the PowerShell console:</span></span>

```powershell
# Set up the parameters for the runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for the Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start the runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="4c9ee-138">Le runbook s’exécute, et vous pouvez vérifier son état en exécutant `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-138">The runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="4c9ee-139">Le runbook récupère le modèle Resource Manager et l’utilise pour déployer un nouveau compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-139">The runbook gets the Resource Manager template and uses it to deploy a new Azure Storage account.</span></span>
<span data-ttu-id="4c9ee-140">Vous pouvez voir que le nouveau compte de stockage a été créé en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4c9ee-140">You can see that the new storage account was created by running the following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="4c9ee-141">Résumé</span><span class="sxs-lookup"><span data-stu-id="4c9ee-141">Summary</span></span>

<span data-ttu-id="4c9ee-142">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="4c9ee-142">That's it!</span></span> <span data-ttu-id="4c9ee-143">Maintenant, vous pouvez utiliser Azure Automation, Stockage Azure et des modèles Resource Manager pour déployer toutes vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4c9ee-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates to deploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c9ee-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c9ee-144">Next steps</span></span>

* <span data-ttu-id="4c9ee-145">Pour en savoir plus sur les modèles Resource Manager, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-145">To learn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="4c9ee-146">Pour démarrer avec Stockage Azure, consultez [Introduction à Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-146">To get started with Azure Storage, see [Introduction to Azure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="4c9ee-147">Pour rechercher d’autres runbooks Azure Automation utiles, consultez [Galeries de runbooks et de modules pour Azure Automation](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-147">To find other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="4c9ee-148">Pour rechercher d’autres modèles Resource Manager utiles, consultez [Modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/).</span><span class="sxs-lookup"><span data-stu-id="4c9ee-148">To find other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

