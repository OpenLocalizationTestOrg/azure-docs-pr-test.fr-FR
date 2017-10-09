---
title: "aaaAzure exemple de Script PowerShell - supprimer une application à partir d’un cluster | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Supprimer une application d’un cluster Service Fabric"
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="6be13-103">Supprimer une application d’un cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6be13-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="6be13-104">Cet exemple de script supprime une instance en cours d’exécution de l’application Service Fabric, annule l’inscription d’un type d’application et la version du cluster de hello et supprime le package d’application hello à partir du magasin d’images hello cluster.</span><span class="sxs-lookup"><span data-stu-id="6be13-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="6be13-105">Instance de l’application hello suppression supprime également hello toutes les instances de service associés à cette application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6be13-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="6be13-106">Personnaliser les paramètres de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="6be13-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="6be13-107">Si nécessaire, installez le module PowerShell de l’infrastructure de Service de hello avec hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6be13-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6be13-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="6be13-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="6be13-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="6be13-109">Script explanation</span></span>

<span data-ttu-id="6be13-110">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="6be13-110">This script uses hello following commands.</span></span> <span data-ttu-id="6be13-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="6be13-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6be13-112">Commande</span><span class="sxs-lookup"><span data-stu-id="6be13-112">Command</span></span> | <span data-ttu-id="6be13-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="6be13-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6be13-114">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="6be13-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="6be13-115">Supprime une instance d’application en cours d’exécution de l’infrastructure de Service de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6be13-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="6be13-116">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="6be13-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="6be13-117">Annule l’inscription d’un type d’application Service Fabric et une version à partir du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6be13-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="6be13-118">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="6be13-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="6be13-119">Supprime un package d’application Service Fabric de magasin d’images hello.</span><span class="sxs-lookup"><span data-stu-id="6be13-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="6be13-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6be13-120">Next steps</span></span>

<span data-ttu-id="6be13-121">Pour plus d’informations sur le module PowerShell de l’infrastructure de Service de hello, consultez [documentation Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="6be13-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="6be13-122">Vous trouverez des exemples supplémentaires de Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6be13-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
