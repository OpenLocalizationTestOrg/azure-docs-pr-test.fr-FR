---
title: "Exemple de script Azure PowerShell - Déploiement de modèle | Microsoft Docs"
description: "Exemple de script pour le déploiement d’un modèle Azure Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b7a7dda1da653d084e02e6724d2f0cb5aa76807a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="f8767-103">Déploiement d’un modèle Azure Resource Manager - script PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8767-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="f8767-104">Ce script déploie un modèle Resource Manager sur un groupe de ressources de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f8767-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f8767-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="f8767-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template to Azure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #The subscription id where the template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #The resource group where the template will be deployed. Can be the name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try to create a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #The deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path to the template file. Defaults to template.json.
    [string]$TemplateFilePath = "template.json",  

    #Path to the parameters file. Defaults to parameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login to Azure and select subscription
Write-Output "Logging in"
Login-AzureRmAccount
Write-Output "Selecting subscription '$SubscriptionId'"
Select-AzureRmSubscription -SubscriptionID $SubscriptionId

# Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $ResourceGroupName -ErrorAction SilentlyContinue
if ( -not $ResourceGroup ) {
    Write-Output "Could not find resource group '$ResourceGroupName' - will create it"
    if ( -not $ResourceGroupLocation ) {
        $ResourceGroupLocation = Read-Host -Prompt 'Enter location for resource group'
    }
    Write-Output "Creating resource group '$ResourceGroupName' in location '$ResourceGroupLocation'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else {
    Write-Output "Using existing resource group '$ResourceGroupName'"
}

# Start the deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="f8767-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="f8767-106">Clean up deployment</span></span> 

<span data-ttu-id="f8767-107">Exécutez la commande suivante pour supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="f8767-107">Run the following command to remove the resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f8767-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="f8767-108">Script explanation</span></span>

<span data-ttu-id="f8767-109">Ce script a recours aux commandes suivantes pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f8767-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="f8767-110">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="f8767-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f8767-111">Commande</span><span class="sxs-lookup"><span data-stu-id="f8767-111">Command</span></span> | <span data-ttu-id="f8767-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="f8767-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f8767-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="f8767-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="f8767-114">Inscrit un fournisseur de ressources pour que ses types de ressources puissent être déployés dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f8767-114">Registers a resource provider so its resource types can be deployed to your subscription.</span></span>  |
| [<span data-ttu-id="f8767-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f8767-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="f8767-116">Récupère le groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="f8767-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="f8767-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f8767-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f8767-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="f8767-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f8767-119">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="f8767-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="f8767-120">Ajoute un déploiement Azure à un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f8767-120">Adds an Azure deployment to a resource group.</span></span>  |
| [<span data-ttu-id="f8767-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f8767-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f8767-122">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="f8767-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="f8767-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f8767-123">Next steps</span></span>
* <span data-ttu-id="f8767-124">Pour une introduction au déploiement de modèles, voir [Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f8767-124">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="f8767-125">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="f8767-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="f8767-126">Pour définir des paramètres dans le modèle, consultez [Création de modèles](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="f8767-126">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="f8767-127">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f8767-127">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

