---
title: "aaaAzure exemple de Script PowerShell - déployer le modèle | Documents Microsoft"
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
ms.openlocfilehash: 536b8ccecad4ed8a4c4a4139c6bf4600e2eb9405
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="56909-103">Déploiement d’un modèle Azure Resource Manager - script PowerShell</span><span class="sxs-lookup"><span data-stu-id="56909-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="56909-104">Ce script déploie un groupe de ressources de gestionnaire de ressources du modèle tooa dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="56909-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="56909-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="56909-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template tooAzure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #hello subscription id where hello template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #hello resource group where hello template will be deployed. Can be hello name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try toocreate a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #hello deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path toohello template file. Defaults tootemplate.json.
    [string]$TemplateFilePath = "template.json",  

    #Path toohello parameters file. Defaults tooparameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login tooAzure and select subscription
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

# Start hello deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="56909-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="56909-106">Clean up deployment</span></span> 

<span data-ttu-id="56909-107">La commande suivante d’exécution hello groupe de ressources tooremove hello et toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="56909-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="56909-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="56909-108">Script explanation</span></span>

<span data-ttu-id="56909-109">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="56909-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="56909-110">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="56909-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="56909-111">Commande</span><span class="sxs-lookup"><span data-stu-id="56909-111">Command</span></span> | <span data-ttu-id="56909-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="56909-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="56909-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="56909-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="56909-114">Inscrit un fournisseur de ressources afin de ses types de ressources peuvent être déployé tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="56909-114">Registers a resource provider so its resource types can be deployed tooyour subscription.</span></span>  |
| [<span data-ttu-id="56909-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="56909-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="56909-116">Récupère le groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="56909-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="56909-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="56909-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="56909-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="56909-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="56909-119">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="56909-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="56909-120">Ajoute un groupe de ressources de déploiement Azure tooa.</span><span class="sxs-lookup"><span data-stu-id="56909-120">Adds an Azure deployment tooa resource group.</span></span>  |
| [<span data-ttu-id="56909-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="56909-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="56909-122">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="56909-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="56909-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56909-123">Next steps</span></span>
* <span data-ttu-id="56909-124">Pour une toodeploying des modèles de présentation, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et d’Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="56909-124">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="56909-125">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="56909-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="56909-126">paramètres de toodefine dans le modèle, consultez [création de modèles](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="56909-126">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="56909-127">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="56909-127">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

