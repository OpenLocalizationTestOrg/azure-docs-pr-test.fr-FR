---
title: "aaaCreate une règle d’équilibrage de charge Azure pour un cluster"
description: "Configurer un équilibrage de charge Azure tooopen des ports pour votre cluster Azure Service Fabric."
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
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="68155-103">Ouvrir des ports pour un cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="68155-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="68155-104">équilibrage de charge Hello déployé avec votre cluster Azure Service Fabric dirige le trafic tooyour application est en cours d’exécution sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="68155-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="68155-105">Si vous modifiez votre application de toouse un autre port, vous devez exposer ce port (ou acheminer un autre port) Bonjour équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="68155-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="68155-106">Lorsque vous avez déployé votre tooAzure de cluster service fabric, un équilibreur de charge a été créé automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="68155-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="68155-107">Si vous ne disposez pas d’un équilibrage de charge, consultez [Configurer un équilibreur de charge connecté à Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68155-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="68155-108">Configurer Service Fabric</span><span class="sxs-lookup"><span data-stu-id="68155-108">Configure service fabric</span></span>

<span data-ttu-id="68155-109">Votre application de Service Fabric **ServiceManifest.xml** le fichier de configuration définit les points de terminaison hello toouse que votre application attend.</span><span class="sxs-lookup"><span data-stu-id="68155-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="68155-110">Une fois que le fichier de configuration hello a été mis à jour toodefine un point de terminaison, équilibrage de charge hello doit être mis à jour tooexpose que (ou une autre) port.</span><span class="sxs-lookup"><span data-stu-id="68155-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="68155-111">Pour plus d’informations sur la façon dont toocreate hello point de terminaison de service fabric, consultez [le programme d’installation d’un point de terminaison](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="68155-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="68155-112">Créer une règle d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="68155-112">Create a load balancer rule</span></span>

<span data-ttu-id="68155-113">Une règle d’équilibreur de charge s’ouvre un port connecté à internet et transmet le port du nœud de l’intérieur du trafic toohello utilisé par votre application.</span><span class="sxs-lookup"><span data-stu-id="68155-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="68155-114">Si vous ne disposez pas d’un équilibrage de charge, consultez [Configurer un équilibreur de charge connecté à Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68155-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="68155-115">règle de toocreate un équilibreur de charge, vous devez hello toocollect informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="68155-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="68155-116">Nom de l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="68155-116">Load balancer name.</span></span>
- <span data-ttu-id="68155-117">Groupe de ressources de hello équilibreur de charge et cluster service fabric.</span><span class="sxs-lookup"><span data-stu-id="68155-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="68155-118">Port externe.</span><span class="sxs-lookup"><span data-stu-id="68155-118">External port.</span></span>
- <span data-ttu-id="68155-119">Port interne.</span><span class="sxs-lookup"><span data-stu-id="68155-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="68155-120">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="68155-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="68155-121">Si vous avez besoin de nom de hello toodetermine d’équilibrage de charge hello, vous pouvez utiliser cette get tooquickly de commande une liste de tous les équilibreurs de charge et les groupes de ressources hello associé.</span><span class="sxs-lookup"><span data-stu-id="68155-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="68155-122">Il n’accepte qu’une commande unique de toocreate une règle d’équilibreur de charge avec hello **CLI d’Azure**.</span><span class="sxs-lookup"><span data-stu-id="68155-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="68155-123">Vous devez simplement tooknow à la fois nom hello de hello charge équilibrage et ressource groupe toocreate une nouvelle règle.</span><span class="sxs-lookup"><span data-stu-id="68155-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="68155-124">Hello commande CLI d’Azure a quelques paramètres décrits dans hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="68155-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="68155-125">Paramètre</span><span class="sxs-lookup"><span data-stu-id="68155-125">Parameter</span></span> | <span data-ttu-id="68155-126">Description</span><span class="sxs-lookup"><span data-stu-id="68155-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="68155-127">application de l’ensemble fibre optique Hello port hello service écoute.</span><span class="sxs-lookup"><span data-stu-id="68155-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="68155-128">Bonjour Bonjour de port de charge expose équilibrage pour les connexions externes.</span><span class="sxs-lookup"><span data-stu-id="68155-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="68155-129">toochange d’équilibrage de charge nom Hello Hello.</span><span class="sxs-lookup"><span data-stu-id="68155-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="68155-130">groupe de ressources Hello qui a l’équilibrage de charge hello et cluster service fabric.</span><span class="sxs-lookup"><span data-stu-id="68155-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="68155-131">Hello choisi le nom de règle de hello.</span><span class="sxs-lookup"><span data-stu-id="68155-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="68155-132">Pour plus d’informations sur comment toocreate un équilibreur de charge avec hello CLI d’Azure, consultez [créer un équilibreur de charge avec hello CLI d’Azure](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="68155-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="68155-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68155-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="68155-134">Si vous avez besoin de nom de hello toodetermine d’équilibrage de charge hello, utilisez cette get tooquickly de commandes une liste de tous les équilibrages de charge et les groupes de ressources associé.</span><span class="sxs-lookup"><span data-stu-id="68155-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="68155-135">PowerShell est un peu plus compliqué que hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="68155-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="68155-136">Point de vue conceptuel, faire hello suivant les étapes toocreate une règle.</span><span class="sxs-lookup"><span data-stu-id="68155-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="68155-137">Obtenir l’équilibrage de charge hello à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="68155-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="68155-138">Créez une règle.</span><span class="sxs-lookup"><span data-stu-id="68155-138">Create a rule.</span></span>
3. <span data-ttu-id="68155-139">Ajouter un équilibrage de charge hello règle toohello.</span><span class="sxs-lookup"><span data-stu-id="68155-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="68155-140">Mettre à jour d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="68155-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="68155-141">En ce qui concerne les hello `New-AzureRmLoadBalancerRuleConfig` commande hello `-FrontendPort` équilibrage de charge représente hello port hello expose pour les connexions externes et hello `-BackendPort` représente hello port hello service fabric application écoute.</span><span class="sxs-lookup"><span data-stu-id="68155-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="68155-142">Pour plus d’informations sur comment toocreate un équilibreur de charge avec PowerShell, consultez [créer un équilibreur de charge avec PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="68155-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

