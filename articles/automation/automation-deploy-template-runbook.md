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
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Déployer un modèle Azure Resource Manager dans un runbook PowerShell Azure Automation

Vous pouvez écrire un [runbook PowerShell Azure Automation](automation-first-runbook-textual-powershell.md) qui déploie une ressource Azure en utilisant un [modèle Azure Resource Manager](../azure-resource-manager/resource-manager-create-first-template.md).

Ainsi, vous pouvez automatiser le déploiement de ressources Azure. Vous pouvez gérer vos modèles Resource Manager dans un emplacement central et sécurisé, tel que Stockage Azure.

Dans cette rubrique, nous créons un runbook PowerShell qui utilise un modèle de gestionnaire de ressources stocké dans [Azure Storage](../storage/common/storage-introduction.md) toodeploy un nouveau compte de stockage Azure.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, vous devez hello suivant :

* Abonnement Azure. Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[créer un compte gratuit](https://azure.microsoft.com/free/).
* [Compte Automation](automation-sec-configure-azure-runas-account.md) toohold hello runbook et authentifier les ressources tooAzure.  Ce compte doit avoir l’autorisation toostart et arrêter l’ordinateur virtuel de hello.
* [Compte de stockage Azure](../storage/common/storage-create-storage-account.md) dans le modèle de gestionnaire de ressources hello toostore
* Azure Powershell installé sur un ordinateur local. Consultez [installer et configurer Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) pour plus d’informations sur la façon tooget Azure PowerShell.

## <a name="create-hello-resource-manager-template"></a>Créer le modèle de gestionnaire de ressources hello

Pour cet exemple, nous utilisons un modèle Resource Manager qui déploie un nouveau compte de stockage Azure.

Dans un éditeur de texte, copiez hello suivant du texte :

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

Enregistrer le fichier de hello localement sous `TemplateTest.json`.

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Enregistrer le modèle de gestionnaire de ressources hello dans le stockage Azure

Maintenant, nous utiliser PowerShell toocreate un partage de fichiers de stockage Azure et télécharger hello `TemplateTest.json` fichier.
Pour obtenir des instructions sur le partage toocreate un fichier et télécharger un fichier Bonjour portail Azure, consultez [prise en main avec un stockage de fichier Azure sur Windows](../storage/files/storage-dotnet-how-to-use-files.md).

Lancez PowerShell sur votre ordinateur local et exécutez hello suivant de commandes toocreate un partage de fichiers et partage de fichiers toothat hello Gestionnaire de ressources du modèle.

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

## <a name="create-hello-powershell-runbook-script"></a>Créer le script du runbook PowerShell hello

Maintenant nous créons un script PowerShell qui obtient hello `TemplateTest.json` à partir du stockage Azure et déploie hello modèle toocreate un nouveau compte de stockage Azure.

Dans un éditeur de texte, collez hello suivant du texte :

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

Enregistrer le fichier de hello localement sous `DeployTemplate.ps1`.

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>Importer et publier le runbook de hello dans votre compte Azure Automation

Maintenant nous utiliser PowerShell tooimport hello runbook dans votre compte Azure Automation et puis publier hello runbook.
Pour plus d’informations sur la façon tooimport et publier un runbook Bonjour portail Azure, consultez [création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md).

tooimport `DeployTemplate.ps1` dans votre compte Automation en tant qu’un runbook PowerShell, exécutez hello suivant de commandes PowerShell :

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

## <a name="start-hello-runbook"></a>Démarrer hello runbook

Maintenant nous allons commencer hello runbook par appel hello [AzureRmAutomationRunbook de début](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) applet de commande.

Pour plus d’informations sur comment toostart un runbook dans hello portail Azure, consultez [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md).

Exécutez hello suivant les commandes dans la console PowerShell hello :

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

Hello s’exécute le runbook, et vous pouvez vérifier son état en exécutant `$job.Status`.

Hello runbook Obtient le modèle de gestionnaire de ressources hello et l’utilise toodeploy un nouveau compte de stockage Azure.
Vous pouvez voir que le nouveau compte de stockage hello a été créé en exécutant hello de commande suivante :
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>Résumé

Et voilà ! Maintenant vous pouvez utiliser Azure Automation et Azure Storage et Gestionnaire de ressources modèles toodeploy toutes vos ressources Azure.

## <a name="next-steps"></a>Étapes suivantes

* toolearn savoir plus sur les modèles du Gestionnaire de ressources, consultez [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md)
* tooget a démarré avec le stockage Azure, consultez [Introduction tooAzure stockage](../storage/common/storage-introduction.md).
* toofind autres runbooks Azure Automation utiles, consultez [Runbook et module galeries pour Azure Automation](automation-runbook-gallery.md).
* toofind autres modèles de gestionnaire de ressources utiles, consultez [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/)

