---
title: "aaaAzure exemple de Script PowerShell - créer une application web avec un déploiement continu à partir de GitHub | Documents Microsoft"
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
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="3fe88-103">Créer une application web avec un déploiement continu à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="3fe88-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="3fe88-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis configure un déploiement continu à partir d’un dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="3fe88-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="3fe88-105">Pour le déploiement GitHub sans déploiement continu, consultez [Créer une application web et déployer du code à partir de GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="3fe88-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="3fe88-106">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3fe88-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="3fe88-107">Vérifiez également les points suivants :</span><span class="sxs-lookup"><span data-stu-id="3fe88-107">Also, ensure that:</span></span>

- <span data-ttu-id="3fe88-108">Une connexion avec Azure a été créée à l’aide de hello `az login` commande.</span><span class="sxs-lookup"><span data-stu-id="3fe88-108">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="3fe88-109">code de l’application Hello est dans un référentiel GitHub public ou privé dont vous êtes propriétaire.</span><span class="sxs-lookup"><span data-stu-id="3fe88-109">hello application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="3fe88-110">Vous avez [créé un jeton d’accès dans votre compte GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="3fe88-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="3fe88-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="3fe88-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3fe88-112">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="3fe88-112">Clean up deployment</span></span> 

<span data-ttu-id="3fe88-113">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="3fe88-113">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3fe88-114">Explication du script</span><span class="sxs-lookup"><span data-stu-id="3fe88-114">Script explanation</span></span>

<span data-ttu-id="3fe88-115">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="3fe88-115">This script uses hello following commands.</span></span> <span data-ttu-id="3fe88-116">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="3fe88-116">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3fe88-117">Commande</span><span class="sxs-lookup"><span data-stu-id="3fe88-117">Command</span></span> | <span data-ttu-id="3fe88-118">Remarques</span><span class="sxs-lookup"><span data-stu-id="3fe88-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3fe88-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3fe88-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3fe88-120">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="3fe88-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3fe88-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3fe88-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="3fe88-122">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="3fe88-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3fe88-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3fe88-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="3fe88-124">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="3fe88-124">Creates a web app.</span></span> |
| [<span data-ttu-id="3fe88-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="3fe88-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="3fe88-126">Modifie une ressource dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="3fe88-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3fe88-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3fe88-127">Next steps</span></span>

<span data-ttu-id="3fe88-128">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3fe88-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3fe88-129">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3fe88-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
