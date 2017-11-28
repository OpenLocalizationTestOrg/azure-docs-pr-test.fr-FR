---
title: "aaaAzure exemple de Script PowerShell - créer une application web et déployer le code à partir d’un référentiel Git local | Documents Microsoft"
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
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="6a416-103">Créer une application web et déployer du code à partir d’un référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="6a416-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="6a416-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis déploie votre code d’application web dans un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="6a416-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="6a416-105">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="6a416-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="6a416-106">En outre, votre code d’application doit toobe validée dans un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="6a416-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6a416-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="6a416-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6a416-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="6a416-108">Clean up deployment</span></span> 

<span data-ttu-id="6a416-109">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="6a416-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6a416-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="6a416-110">Script explanation</span></span>

<span data-ttu-id="6a416-111">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="6a416-111">This script uses hello following commands.</span></span> <span data-ttu-id="6a416-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="6a416-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6a416-113">Commande</span><span class="sxs-lookup"><span data-stu-id="6a416-113">Command</span></span> | <span data-ttu-id="6a416-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="6a416-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6a416-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6a416-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6a416-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="6a416-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6a416-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6a416-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6a416-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="6a416-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6a416-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6a416-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6a416-120">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="6a416-120">Creates a web app.</span></span> |
| [<span data-ttu-id="6a416-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="6a416-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="6a416-122">Modifie une ressource dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6a416-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="6a416-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="6a416-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="6a416-124">Obtient un profil de publication d’application web.</span><span class="sxs-lookup"><span data-stu-id="6a416-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6a416-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6a416-125">Next steps</span></span>

<span data-ttu-id="6a416-126">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6a416-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6a416-127">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6a416-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
