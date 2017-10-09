---
title: "aaaAzure exemple de Script PowerShell - mise à l’échelle une application web manuellement | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Mettre manuellement à l’échelle une application"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="94cc9-103">Mettre manuellement à l’échelle une application web</span><span class="sxs-lookup"><span data-stu-id="94cc9-103">Scale a web app manually</span></span>

<span data-ttu-id="94cc9-104">Dans ce scénario, vous allez apprendre toocreate un groupe de ressources, application de service web et le plan d’applications.</span><span class="sxs-lookup"><span data-stu-id="94cc9-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="94cc9-105">Vous allez ensuite échelonner hello du Plan App Service à partir d’une instance de toomultiple d’instance unique.</span><span class="sxs-lookup"><span data-stu-id="94cc9-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="94cc9-106">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="94cc9-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="94cc9-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="94cc9-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="94cc9-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="94cc9-108">Clean up deployment</span></span> 

<span data-ttu-id="94cc9-109">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="94cc9-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="94cc9-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="94cc9-110">Script explanation</span></span>

<span data-ttu-id="94cc9-111">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="94cc9-111">This script uses hello following commands.</span></span> <span data-ttu-id="94cc9-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="94cc9-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="94cc9-113">Commande</span><span class="sxs-lookup"><span data-stu-id="94cc9-113">Command</span></span> | <span data-ttu-id="94cc9-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="94cc9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="94cc9-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="94cc9-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="94cc9-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="94cc9-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="94cc9-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="94cc9-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="94cc9-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="94cc9-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="94cc9-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="94cc9-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="94cc9-120">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="94cc9-120">Creates a web app.</span></span> |
| [<span data-ttu-id="94cc9-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="94cc9-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="94cc9-122">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="94cc9-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="94cc9-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94cc9-123">Next steps</span></span>

<span data-ttu-id="94cc9-124">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="94cc9-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="94cc9-125">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="94cc9-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
