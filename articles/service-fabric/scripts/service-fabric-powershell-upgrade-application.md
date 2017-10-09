---
title: "aaaAzure exemple de Script PowerShell - mise à niveau une application de Service Fabric | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Mettre à niveau une application Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="fc343-103">Mettre à niveau une application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fc343-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="fc343-104">Cet exemple de script met à niveau une infrastructure de Service en cours d’exécution de tooversion d’instance application version 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="fc343-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="fc343-105">script de Hello copie hello nouveau package toohello cluster image Boutique d’applications, inscrit le type de l’application hello, démarre une mise à niveau analysée et vérifie en permanence l’état de mise à niveau hello jusqu'à ce que la mise à niveau hello se termine ou est restaurée.</span><span class="sxs-lookup"><span data-stu-id="fc343-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="fc343-106">Personnaliser les paramètres de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="fc343-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="fc343-107">Si nécessaire, installez le module PowerShell de l’infrastructure de Service de hello avec hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fc343-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fc343-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="fc343-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="fc343-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="fc343-109">Script explanation</span></span>

<span data-ttu-id="fc343-110">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="fc343-110">This script uses hello following commands.</span></span> <span data-ttu-id="fc343-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="fc343-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fc343-112">Commande</span><span class="sxs-lookup"><span data-stu-id="fc343-112">Command</span></span> | <span data-ttu-id="fc343-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="fc343-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc343-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="fc343-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="fc343-115">Obtient toutes les applications hello dans le cluster Service Fabric de hello ou une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="fc343-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="fc343-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="fc343-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="fc343-117">Obtient l’état hello d’une mise à niveau des applications de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fc343-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="fc343-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="fc343-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="fc343-119">Obtient les types d’applications de Service Fabric hello inscrits sur le cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="fc343-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="fc343-120">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="fc343-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="fc343-121">Annule l’enregistrement d’un type d’application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fc343-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="fc343-122">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="fc343-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="fc343-123">Copie une image de toohello du package d’application de Service Fabric magasin.</span><span class="sxs-lookup"><span data-stu-id="fc343-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="fc343-124">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="fc343-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="fc343-125">Enregistre un type d’application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fc343-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="fc343-126">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="fc343-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="fc343-127">Met à niveau une version de type de Service Fabric application toohello application spécifiée.</span><span class="sxs-lookup"><span data-stu-id="fc343-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="fc343-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc343-128">Next steps</span></span>

<span data-ttu-id="fc343-129">Pour plus d’informations sur le module PowerShell de l’infrastructure de Service de hello, consultez [documentation Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="fc343-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="fc343-130">Vous trouverez des exemples supplémentaires de Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fc343-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
