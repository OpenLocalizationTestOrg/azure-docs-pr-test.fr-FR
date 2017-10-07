---
title: "Exemple de Script PowerShell - port application ouverte dans l’équilibrage de charge d’aaaAzure | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - ouvrir un port de l’équilibrage de charge Azure hello pour une application de Service Fabric."
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
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a><span data-ttu-id="38795-103">Ouvrir un port de l’application dans l’équilibrage de charge Azure hello</span><span class="sxs-lookup"><span data-stu-id="38795-103">Open an application port in hello Azure load balancer</span></span>

<span data-ttu-id="38795-104">Une application de Service Fabric s’exécutant dans Azure se trouve derrière l’équilibrage de charge Azure hello.</span><span class="sxs-lookup"><span data-stu-id="38795-104">A Service Fabric application running in Azure sits behind hello Azure load balancer.</span></span> <span data-ttu-id="38795-105">Cet exemple de script ouvre un port dans un équilibreur de charge Azure pour qu’une application Service Fabric puisse communiquer avec des clients externes.</span><span class="sxs-lookup"><span data-stu-id="38795-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="38795-106">Personnaliser les paramètres de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="38795-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="38795-107">Si nécessaire, installez le module PowerShell de l’infrastructure de Service de hello avec hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="38795-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="38795-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="38795-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a><span data-ttu-id="38795-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="38795-109">Script explanation</span></span>

<span data-ttu-id="38795-110">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="38795-110">This script uses hello following commands.</span></span> <span data-ttu-id="38795-111">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="38795-111">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="38795-112">Commande</span><span class="sxs-lookup"><span data-stu-id="38795-112">Command</span></span> | <span data-ttu-id="38795-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="38795-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="38795-114">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="38795-114">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="38795-115">Obtient une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="38795-115">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="38795-116">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="38795-116">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="38795-117">Obtient l’équilibrage de charge Azure hello.</span><span class="sxs-lookup"><span data-stu-id="38795-117">Gets hello Azure load balancer.</span></span> |
| [<span data-ttu-id="38795-118">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="38795-118">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="38795-119">Ajoute un équilibrage de charge de sonde configuration tooa.</span><span class="sxs-lookup"><span data-stu-id="38795-119">Adds a probe configuration tooa load balancer.</span></span>|
| [<span data-ttu-id="38795-120">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="38795-120">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="38795-121">Obtient une configuration de sonde pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="38795-121">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="38795-122">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="38795-122">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="38795-123">Ajoute un équilibrage de charge de règle configuration tooa.</span><span class="sxs-lookup"><span data-stu-id="38795-123">Adds a rule configuration tooa load balancer.</span></span> |
| [<span data-ttu-id="38795-124">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="38795-124">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="38795-125">Jeux de hello état objectif d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="38795-125">Sets hello goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="38795-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38795-126">Next steps</span></span>

<span data-ttu-id="38795-127">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="38795-127">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="38795-128">Vous trouverez des exemples supplémentaires de Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="38795-128">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
