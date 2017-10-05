---
title: "Exemple de script Azure PowerShell - Créer une application web avec un déploiement continu à partir de GitHub | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Créer une application web avec un déploiement continu à partir de GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: fc594a94bb64ceb88370be8617036a73402ade4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="a45ba-103">Créer une application web avec un déploiement continu à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="a45ba-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="a45ba-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis configure un déploiement continu à partir d’un dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="a45ba-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="a45ba-105">Pour le déploiement GitHub sans déploiement continu, consultez [Créer une application web et déployer du code à partir de GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="a45ba-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="a45ba-106">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [guide Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a45ba-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="a45ba-107">Vérifiez également les points suivants :</span><span class="sxs-lookup"><span data-stu-id="a45ba-107">Also, ensure that:</span></span>

- <span data-ttu-id="a45ba-108">Une connexion avec Azure a été créée à l’aide de la commande `az login`.</span><span class="sxs-lookup"><span data-stu-id="a45ba-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="a45ba-109">Le code d’application se trouve dans un référentiel GitHub public ou privé dont vous êtes propriétaire.</span><span class="sxs-lookup"><span data-stu-id="a45ba-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="a45ba-110">Vous avez [créé un jeton d’accès dans votre compte GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="a45ba-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="a45ba-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a45ba-111">Sample script</span></span>

<span data-ttu-id="a45ba-112">[!code-powershell[principal](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Créer une application web avec un déploiement continu à partir de GitHub")]</span><span class="sxs-lookup"><span data-stu-id="a45ba-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a45ba-113">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="a45ba-113">Clean up deployment</span></span> 

<span data-ttu-id="a45ba-114">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="a45ba-114">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="a45ba-115">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a45ba-115">Script explanation</span></span>

<span data-ttu-id="a45ba-116">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="a45ba-116">This script uses the following commands.</span></span> <span data-ttu-id="a45ba-117">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="a45ba-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a45ba-118">Commande</span><span class="sxs-lookup"><span data-stu-id="a45ba-118">Command</span></span> | <span data-ttu-id="a45ba-119">Remarques</span><span class="sxs-lookup"><span data-stu-id="a45ba-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a45ba-120">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a45ba-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a45ba-121">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="a45ba-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a45ba-122">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a45ba-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="a45ba-123">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="a45ba-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a45ba-124">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a45ba-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="a45ba-125">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="a45ba-125">Creates a web app.</span></span> |
| [<span data-ttu-id="a45ba-126">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="a45ba-126">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="a45ba-127">Modifie une ressource dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a45ba-127">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a45ba-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a45ba-128">Next steps</span></span>

<span data-ttu-id="a45ba-129">Pour plus d’informations sur le module Azure PowerShell, consultez la [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a45ba-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a45ba-130">Vous trouverez des exemples supplémentaires de scripts Azure PowerShell pour Azure App Service Web Apps sur la page [Azure PowerShell Samples](../app-service-powershell-samples.md) (Exemples Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a45ba-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
