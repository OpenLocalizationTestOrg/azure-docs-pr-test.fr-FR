---
title: "Exemple de script Azure PowerShell - Créer une application web et déployer du code à partir d’un référentiel Git local | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Créer une application web et déployer du code à partir d’un référentiel Git local"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 855b8c643bf2a742e763bda2e2c21c6a86331aac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="44852-103">Créer une application web et déployer du code à partir d’un référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="44852-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="44852-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis déploie votre code d’application web dans un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="44852-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="44852-105">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="44852-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="44852-106">En outre, votre code d’application doit être validé dans un dépôt Git local.</span><span class="sxs-lookup"><span data-stu-id="44852-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="44852-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="44852-107">Sample script</span></span>

<span data-ttu-id="44852-108">[!code-powershell[principal](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Créer une application web et déployer du code à partir d’un référentiel Git")]</span><span class="sxs-lookup"><span data-stu-id="44852-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="44852-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="44852-109">Clean up deployment</span></span> 

<span data-ttu-id="44852-110">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="44852-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="44852-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="44852-111">Script explanation</span></span>

<span data-ttu-id="44852-112">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="44852-112">This script uses the following commands.</span></span> <span data-ttu-id="44852-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="44852-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="44852-114">Commande</span><span class="sxs-lookup"><span data-stu-id="44852-114">Command</span></span> | <span data-ttu-id="44852-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="44852-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="44852-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="44852-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="44852-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="44852-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="44852-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="44852-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="44852-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="44852-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="44852-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="44852-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="44852-121">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="44852-121">Creates a web app.</span></span> |
| [<span data-ttu-id="44852-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="44852-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="44852-123">Modifie une ressource dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="44852-123">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="44852-124">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="44852-124">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="44852-125">Obtient un profil de publication d’application web.</span><span class="sxs-lookup"><span data-stu-id="44852-125">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="44852-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44852-126">Next steps</span></span>

<span data-ttu-id="44852-127">Pour plus d’informations sur le module Azure PowerShell, consultez la [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="44852-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="44852-128">Vous trouverez des exemples supplémentaires de scripts Azure PowerShell pour Azure App Service Web Apps sur la page [Azure PowerShell Samples](../app-service-powershell-samples.md) (Exemples Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="44852-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
