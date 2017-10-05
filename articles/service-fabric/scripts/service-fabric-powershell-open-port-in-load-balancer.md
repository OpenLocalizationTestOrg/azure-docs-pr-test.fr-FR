---
title: "Exemple de script Azure PowerShell - Ouvrir le port d’application dans l’équilibrage de charge | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Ouvrir un port dans l’équilibrage de charge Azure pour une application de Service Fabric."
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
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 2958bdef0889076249918608c04c66678fa80b97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="open-an-application-port-in-the-azure-load-balancer"></a><span data-ttu-id="a3efa-103">Ouvrir un port d’application dans l’équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="a3efa-103">Open an application port in the Azure load balancer</span></span>

<span data-ttu-id="a3efa-104">Une application Service Fabric s’exécutant dans Azure se trouve derrière l’équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="a3efa-104">A Service Fabric application running in Azure sits behind the Azure load balancer.</span></span> <span data-ttu-id="a3efa-105">Cet exemple de script ouvre un port dans un équilibreur de charge Azure pour qu’une application Service Fabric puisse communiquer avec des clients externes.</span><span class="sxs-lookup"><span data-stu-id="a3efa-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="a3efa-106">Personnalisez les paramètres selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="a3efa-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="a3efa-107">Si nécessaire, installez le module Service Fabric PowerShell avec le [Kit de développement logiciel (SDK) Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a3efa-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a3efa-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a3efa-108">Sample script</span></span>

<span data-ttu-id="a3efa-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Ouvrir un port dans l’équilibreur de charge")]</span><span class="sxs-lookup"><span data-stu-id="a3efa-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="a3efa-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a3efa-110">Script explanation</span></span>

<span data-ttu-id="a3efa-111">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="a3efa-111">This script uses the following commands.</span></span> <span data-ttu-id="a3efa-112">Chaque commande de la table renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="a3efa-112">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="a3efa-113">Commande</span><span class="sxs-lookup"><span data-stu-id="a3efa-113">Command</span></span> | <span data-ttu-id="a3efa-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="a3efa-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a3efa-115">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="a3efa-115">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="a3efa-116">Obtient une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="a3efa-116">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="a3efa-117">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="a3efa-117">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="a3efa-118">Obtient l’équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="a3efa-118">Gets the Azure load balancer.</span></span> |
| [<span data-ttu-id="a3efa-119">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="a3efa-119">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="a3efa-120">Ajoute une configuration de sonde pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="a3efa-120">Adds a probe configuration to a load balancer.</span></span>|
| [<span data-ttu-id="a3efa-121">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="a3efa-121">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="a3efa-122">Obtient une configuration de sonde pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="a3efa-122">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="a3efa-123">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="a3efa-123">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="a3efa-124">Ajoute une configuration de règle pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="a3efa-124">Adds a rule configuration to a load balancer.</span></span> |
| [<span data-ttu-id="a3efa-125">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="a3efa-125">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="a3efa-126">Définit l’état visé d’un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="a3efa-126">Sets the goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a3efa-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3efa-127">Next steps</span></span>

<span data-ttu-id="a3efa-128">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a3efa-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a3efa-129">Vous trouverez des exemples supplémentaires de scripts PowerShell pour Azure Service Fabric sur la page [Exemples Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a3efa-129">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
