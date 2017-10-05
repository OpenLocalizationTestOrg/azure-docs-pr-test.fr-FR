---
title: "Créer une règle Azure Load Balancer pour un cluster"
description: Configurez Azure Load Balancer pour ouvrir les ports pour votre cluster Azure Service Fabric.
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: c99c4d9f343ca97fd3cd363fb54feaf5507bb77c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="a7576-103">Ouvrir des ports pour un cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a7576-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="a7576-104">L’équilibreur de charge déployé avec votre cluster Azure Service Fabric dirige le trafic vers votre application en cours d’exécution sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="a7576-104">The load balancer deployed with your Azure Service Fabric cluster directs traffic to your app running on a node.</span></span> <span data-ttu-id="a7576-105">Si vous modifiez votre application pour utiliser un autre port, vous devez exposer ce port (ou acheminer un port différent) dans Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="a7576-105">If you change your app to use a different port, you must expose that port (or route a different port) in the Azure Load Balancer.</span></span>

<span data-ttu-id="a7576-106">Une fois votre cluster Service Fabric déployé vers Azure, un équilibreur de charge est créé automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="a7576-106">When you deployed your service fabric cluster to Azure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="a7576-107">Si vous ne disposez pas d’un équilibrage de charge, consultez [Configurer un équilibreur de charge connecté à Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a7576-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="a7576-108">Configurer Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a7576-108">Configure service fabric</span></span>

<span data-ttu-id="a7576-109">Le fichier de configuration de votre application Service Fabric **ServiceManifest.xml** définit les points de terminaison que votre application s’attend à utiliser.</span><span class="sxs-lookup"><span data-stu-id="a7576-109">Your Service Fabric application **ServiceManifest.xml** config file defines the endpoints your application expects to use.</span></span> <span data-ttu-id="a7576-110">Une fois le fichier de configuration mis à jour pour définir un point de terminaison, l’équilibreur de charge doit être mis à jour pour exposer ce port (ou un autre).</span><span class="sxs-lookup"><span data-stu-id="a7576-110">After the config file has been updated to define an endpoint, the load balancer must be updated to expose that (or a different) port.</span></span> <span data-ttu-id="a7576-111">Pour plus d’informations sur la façon de créer le point de terminaison Service Fabric, consultez [Configurer un point de terminaison](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="a7576-111">For more information on how to create the service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="a7576-112">Créer une règle d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="a7576-112">Create a load balancer rule</span></span>

<span data-ttu-id="a7576-113">Une règle d’équilibreur de charge ouvre un port connecté à internet et transfère le trafic vers le port du nœud interne utilisé par votre application.</span><span class="sxs-lookup"><span data-stu-id="a7576-113">A load balancer rule opens up an internet-facing port and forwards traffic to the internal node's port used by your application.</span></span> <span data-ttu-id="a7576-114">Si vous ne disposez pas d’un équilibrage de charge, consultez [Configurer un équilibreur de charge connecté à Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a7576-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="a7576-115">Pour créer une règle d’équilibreur de charge, vous devez collecter les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a7576-115">To create a load balancer rule, you need to collect the following information:</span></span>

- <span data-ttu-id="a7576-116">Nom de l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="a7576-116">Load balancer name.</span></span>
- <span data-ttu-id="a7576-117">Groupe de ressources de l’équilibreur de charge et du cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a7576-117">Resource group of the load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="a7576-118">Port externe.</span><span class="sxs-lookup"><span data-stu-id="a7576-118">External port.</span></span>
- <span data-ttu-id="a7576-119">Port interne.</span><span class="sxs-lookup"><span data-stu-id="a7576-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="a7576-120">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="a7576-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="a7576-121">Si vous avez besoin déterminer le nom de l’équilibreur de charge, utilisez cette commande pour obtenir rapidement une liste de tous les équilibreurs de charge et des groupes de ressources associés.</span><span class="sxs-lookup"><span data-stu-id="a7576-121">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and the associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="a7576-122">Il suffit d’une seule commande pour créer une règle d’équilibreur de charge avec l’interface **Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="a7576-122">It only takes a single command to create a load balancer rule with the **Azure CLI**.</span></span> <span data-ttu-id="a7576-123">Vous devez simplement connaître le nom de l’équilibreur de charge et du groupe de ressources pour créer une nouvelle règle.</span><span class="sxs-lookup"><span data-stu-id="a7576-123">You just need to know both the name of the load balancer and resource group to create a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="a7576-124">La commande Azure CLI dispose de quelques paramètres décrits dans le tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="a7576-124">The Azure CLI command has a few parameters that are described in the following table:</span></span>

| <span data-ttu-id="a7576-125">Paramètre</span><span class="sxs-lookup"><span data-stu-id="a7576-125">Parameter</span></span> | <span data-ttu-id="a7576-126">Description</span><span class="sxs-lookup"><span data-stu-id="a7576-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="a7576-127">Le port que l’application Service Fabric écoute.</span><span class="sxs-lookup"><span data-stu-id="a7576-127">The port the service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="a7576-128">Le port que l’équilibreur de charge expose aux connexions externes.</span><span class="sxs-lookup"><span data-stu-id="a7576-128">The port the load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="a7576-129">Le nom de l’équilibreur de charge à modifier.</span><span class="sxs-lookup"><span data-stu-id="a7576-129">The name of the load balancer to change.</span></span> |
| `-g`       | <span data-ttu-id="a7576-130">Le groupe de ressources qui dispose de l’équilibreur de charge et du cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a7576-130">The resource group that has both the load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="a7576-131">Le nom de la règle choisi.</span><span class="sxs-lookup"><span data-stu-id="a7576-131">The chosen name of the rule.</span></span> |


>[!NOTE]
><span data-ttu-id="a7576-132">Pour plus d’informations sur la création d’un équilibreur de charge avec l’interface Azure CLI, consultez [Créer un équilibreur de charge avec l’interface Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a7576-132">For more information on how to create a load balancer with the Azure CLI, see [Create a load balancer with the Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="a7576-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7576-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="a7576-134">Si vous devez déterminer le nom de l’équilibreur de charge, utilisez cette commande pour obtenir rapidement une liste de tous les équilibreurs de charge et des groupes de ressources associés.</span><span class="sxs-lookup"><span data-stu-id="a7576-134">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="a7576-135">PowerShell est un peu plus compliqué que l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a7576-135">PowerShell is a little more complicated than the Azure CLI.</span></span> <span data-ttu-id="a7576-136">Sur le plan conceptuel, procédez comme suit pour créer une règle.</span><span class="sxs-lookup"><span data-stu-id="a7576-136">Conceptually, do the following steps to create a rule.</span></span>

1. <span data-ttu-id="a7576-137">Récupérez l’équilibreur de charge d’Azure.</span><span class="sxs-lookup"><span data-stu-id="a7576-137">Get the load balancer from Azure.</span></span>
2. <span data-ttu-id="a7576-138">Créez une règle.</span><span class="sxs-lookup"><span data-stu-id="a7576-138">Create a rule.</span></span>
3. <span data-ttu-id="a7576-139">Ajoutez la règle pour l'équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="a7576-139">Add the rule to the load balancer.</span></span>
4. <span data-ttu-id="a7576-140">Mettez à jour l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="a7576-140">Update the load balancer.</span></span>

```powershell
# Get the load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create the rule based on information from the load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add the rule to the load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update the load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="a7576-141">En ce qui concerne la commande `New-AzureRmLoadBalancerRuleConfig`, le `-FrontendPort` représente le port que l’équilibrage de charge expose aux connexions externes, et le `-BackendPort` représente le port d’écoute de l’application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a7576-141">Regarding the `New-AzureRmLoadBalancerRuleConfig` command, the `-FrontendPort` represents the port the load balancer exposes for external connections, and the `-BackendPort` represents the port the service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="a7576-142">Pour plus d’informations sur la création d’un équilibreur de charge avec l’interface PowerShellI, consultez [Créer un équilibreur de charge avec PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a7576-142">For more information on how to create a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

