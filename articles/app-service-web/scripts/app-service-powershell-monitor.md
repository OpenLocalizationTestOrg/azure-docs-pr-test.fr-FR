---
title: aaaAzure exemple de Script PowerShell - analyser une application web avec les journaux du serveur web | Documents Microsoft
description: Exemple de script Azure PowerShell - Surveiller une application web avec les journaux de serveur web
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="67575-103">Surveiller une application web avec les journaux de serveur web</span><span class="sxs-lookup"><span data-stu-id="67575-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="67575-104">Dans ce scénario, vous créez un groupe de ressources, le plan de service d’application, l’application web et configurer les journaux du serveur web tooenable hello web app.</span><span class="sxs-lookup"><span data-stu-id="67575-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="67575-105">Vous télécharge alors les fichiers de journaux hello pour révision.</span><span class="sxs-lookup"><span data-stu-id="67575-105">You will then download hello log files for review.</span></span>

<span data-ttu-id="67575-106">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="67575-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="67575-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="67575-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="67575-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="67575-108">Clean up deployment</span></span> 

<span data-ttu-id="67575-109">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="67575-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="67575-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="67575-110">Script explanation</span></span>

<span data-ttu-id="67575-111">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="67575-111">This script uses hello following commands.</span></span> <span data-ttu-id="67575-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="67575-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="67575-113">Commande</span><span class="sxs-lookup"><span data-stu-id="67575-113">Command</span></span> | <span data-ttu-id="67575-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="67575-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="67575-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="67575-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="67575-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="67575-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="67575-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="67575-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="67575-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="67575-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="67575-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="67575-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="67575-120">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="67575-120">Creates a web app.</span></span> |
| [<span data-ttu-id="67575-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="67575-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="67575-122">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="67575-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="67575-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="67575-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="67575-124">Obtient les mesures de l’application web.</span><span class="sxs-lookup"><span data-stu-id="67575-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="67575-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="67575-125">Next steps</span></span>

<span data-ttu-id="67575-126">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="67575-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="67575-127">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="67575-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
