---
title: "Vérifier le trafic avec la vérification des flux IP Azure Network Watcher - Azure CLI | Microsoft Docs"
description: "Cet article explique comment savoir si le trafic en direction ou en provenance d’une machine virtuelle est autorisé ou refusé à l’aide de la ligne de commande Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c5fe6c662b3ee2a443904b0f12cbfd495d9bc85e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="56da6-103">Vérifiez si le trafic est autorisé ou refusé en direction ou en provenance d’une machine virtuelle avec le composant de vérification des flux IP d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="56da6-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="56da6-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="56da6-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="56da6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56da6-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="56da6-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="56da6-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="56da6-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="56da6-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="56da6-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="56da6-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="56da6-109">La vérification des flux IP est une fonctionnalité de Network Watcher qui vous permet de vérifier si le trafic en direction ou en provenance d’une machine virtuelle est autorisé.</span><span class="sxs-lookup"><span data-stu-id="56da6-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="56da6-110">Cette fonctionnalité est très utile pour définir si une machine virtuelle peut actuellement communiquer avec une ressource externe ou un serveur back-end.</span><span class="sxs-lookup"><span data-stu-id="56da6-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="56da6-111">La vérification des flux IP peut être utilisée pour vérifier si les règles de votre groupe de sécurité réseau sont correctement configurées et pour résoudre les problèmes de flux bloqués par les règles de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="56da6-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="56da6-112">La vérification des flux IP permet aussi de s’assurer que le trafic que vous souhaitez bloquer est correctement bloqué par le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="56da6-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="56da6-113">Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="56da6-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="56da6-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="56da6-114">Before you begin</span></span>

<span data-ttu-id="56da6-115">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Créer une instance d’Azure Network Watcher](network-watcher-create.md) pour créer un Network Watcher ou que vous disposez d’une instance existante de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="56da6-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="56da6-116">Ce scénario suppose également qu’un groupe de ressources avec une machine virtuelle valide existe et peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="56da6-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="56da6-117">Scénario</span><span class="sxs-lookup"><span data-stu-id="56da6-117">Scenario</span></span>

<span data-ttu-id="56da6-118">Ce scénario utilise la vérification des flux IP pour savoir si une machine virtuelle peut communiquer avec une adresse IP Bing connue.</span><span class="sxs-lookup"><span data-stu-id="56da6-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="56da6-119">Si le trafic est refusé, la règle de sécurité refusant ce trafic est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="56da6-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="56da6-120">Pour plus d’informations sur la vérification des flux IP, consultez la page [IP Flow Verify Overview (Vue d’ensemble de la fonction de vérification des flux IP)](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="56da6-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="56da6-121">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="56da6-121">Get a VM</span></span>

<span data-ttu-id="56da6-122">La vérification des flux IP permet de tester le trafic en direction ou en provenance d’une adresse IP sur une machine virtuelle en direction ou en provenance d’une destination distante.</span><span class="sxs-lookup"><span data-stu-id="56da6-122">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="56da6-123">Un identifiant de machine virtuelle est requis pour l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="56da6-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="56da6-124">Si vous connaissez déjà l’identifiant de la machine virtuelle à utiliser, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="56da6-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-the-nics"></a><span data-ttu-id="56da6-125">Obtenir les cartes réseau</span><span class="sxs-lookup"><span data-stu-id="56da6-125">Get the NICS</span></span>

<span data-ttu-id="56da6-126">L’adresse IP d’une carte réseau sur la machine virtuelle est requise. Dans cet exemple, nous récupérons les cartes réseau sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="56da6-126">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="56da6-127">Si vous connaissez déjà l’adresse IP que vous souhaitez tester sur la machine virtuelle, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="56da6-127">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="56da6-128">Exécuter la vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="56da6-128">Run IP flow verify</span></span>

<span data-ttu-id="56da6-129">Maintenant que nous disposons des informations nécessaires pour exécuter l’applet de commande, nous pouvons exécuter l’applet de commande `network watcher ip-flow-verify` pour tester le trafic.</span><span class="sxs-lookup"><span data-stu-id="56da6-129">Now that we have the information needed to run the cmdlet, we run the `network watcher ip-flow-verify` cmdlet to test the traffic.</span></span> <span data-ttu-id="56da6-130">Dans cet exemple, nous utilisons la première adresse IP sur la première carte réseau.</span><span class="sxs-lookup"><span data-stu-id="56da6-130">In this example, we are using the first IP address on the first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="56da6-131">La vérification des flux IP nécessite l’attribution de la ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="56da6-131">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="56da6-132">Analyser les résultats</span><span class="sxs-lookup"><span data-stu-id="56da6-132">Review Results</span></span>

<span data-ttu-id="56da6-133">Après l’exécution de `network watcher ip-flow-verify`, les résultats sont renvoyés. L’exemple suivant présente les résultats renvoyés à partir de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="56da6-133">After running `network watcher ip-flow-verify` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="56da6-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56da6-134">Next steps</span></span>

<span data-ttu-id="56da6-135">Si le trafic est bloqué alors qu’il ne devrait pas l’être, consultez [Gérer les groupes de sécurité réseau à partir du portail](../virtual-network/virtual-network-manage-nsg-arm-portal.md) afin de surveiller le groupe de sécurité réseau et les règles de sécurité définis.</span><span class="sxs-lookup"><span data-stu-id="56da6-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="56da6-136">Pour savoir comment auditer les paramètres de votre groupe de sécurité réseau, consultez [Auditing Network Security Groups (NSG) with Network Watcher (Audit des groupes de sécurité réseau avec Network Watcher)](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="56da6-136">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
