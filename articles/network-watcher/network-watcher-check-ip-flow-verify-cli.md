---
title: "trafic aaaVerify avec Azure réseau Observateur IP flux vérifier - CLI d’Azure | Documents Microsoft"
description: "Cet article décrit comment toocheck si tooor le trafic à partir d’un ordinateur virtuel est autorisé ou refusé à l’aide de CLI d’Azure"
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
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="d713e-103">Vérifiez si le trafic est autorisé ou refusé tooor à partir d’une machine virtuelle avec IP flux vérifier un composant de l’Observateur de réseau Azure</span><span class="sxs-lookup"><span data-stu-id="d713e-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d713e-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d713e-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="d713e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d713e-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="d713e-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d713e-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="d713e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d713e-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="d713e-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="d713e-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="d713e-109">Flux d’IP Vérifiez est une fonctionnalité de l’Observateur réseau qui vous permet de tooverify si le trafic est autorisé à tooor à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="d713e-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="d713e-110">Ce scénario est utile tooget un état actuel de si un ordinateur virtuel peut communiquer avec les ressources externes tooan ou principal.</span><span class="sxs-lookup"><span data-stu-id="d713e-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="d713e-111">Les flux IP vérifier peut être utilisé tooverify si vos règles de groupe de sécurité réseau (NSG) sont correctement configurés et résoudre les problèmes de flux qui sont bloqués par les règles du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d713e-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="d713e-112">Une autre raison de l’utilisation de IP flux Vérifiez à bloquer le trafic de tooensure est bloqué correctement par hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d713e-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="d713e-113">Cet article utilise notre prochaine génération CLI pour le modèle de déploiement de la gestion des ressources d’hello, Azure CLI 2.0, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="d713e-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="d713e-114">les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="d713e-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d713e-115">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d713e-115">Before you begin</span></span>

<span data-ttu-id="d713e-116">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau ou une instance existante de l’Observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="d713e-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="d713e-117">scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.</span><span class="sxs-lookup"><span data-stu-id="d713e-117">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="d713e-118">Scénario</span><span class="sxs-lookup"><span data-stu-id="d713e-118">Scenario</span></span>

<span data-ttu-id="d713e-119">Ce scénario utilise tooverify d’IP de flux de vérifier si un ordinateur virtuel peuvent communiquer avec les tooa connus adresse IP de Bing.</span><span class="sxs-lookup"><span data-stu-id="d713e-119">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="d713e-120">Si le trafic de hello est refusé, elle retourne la règle de sécurité hello refuse ce trafic.</span><span class="sxs-lookup"><span data-stu-id="d713e-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="d713e-121">toolearn en savoir plus sur l’IP de flux de vérifier, visitez [flux vérifier la vue d’ensemble IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d713e-121">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="d713e-122">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d713e-122">Get a VM</span></span>

<span data-ttu-id="d713e-123">Les flux IP vérifier tooor le trafic de tests à partir d’une adresse IP sur un tooor de l’ordinateur virtuel à partir d’une destination à distance.</span><span class="sxs-lookup"><span data-stu-id="d713e-123">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="d713e-124">Un Id d’un ordinateur virtuel est requis pour l’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="d713e-124">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="d713e-125">Si vous connaissez déjà les ID hello de hello machine virtuelle toouse, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="d713e-125">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a><span data-ttu-id="d713e-126">Obtenir hello cartes réseau</span><span class="sxs-lookup"><span data-stu-id="d713e-126">Get hello NICS</span></span>

<span data-ttu-id="d713e-127">adresse IP de Hello d’une carte réseau sur l’ordinateur virtuel de hello est nécessaire, dans cet exemple, nous récupérons hello cartes d’interface réseau sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="d713e-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="d713e-128">Si vous connaissez déjà hello IP d’adresses que vous souhaitez tootest sur l’ordinateur virtuel de hello, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="d713e-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="d713e-129">Exécuter la vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="d713e-129">Run IP flow verify</span></span>

<span data-ttu-id="d713e-130">Maintenant que nous avons des informations hello nécessaire toorun hello applet de commande, nous exécutons hello `az network watcher test-ip-flow` trafic de hello tootest applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d713e-130">Now that we have hello information needed toorun hello cmdlet, we run hello `az network watcher test-ip-flow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="d713e-131">Dans cet exemple, nous utilisons la première adresse IP de hello sur la carte réseau de première hello.</span><span class="sxs-lookup"><span data-stu-id="d713e-131">In this example, we are using hello first IP address on hello first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="d713e-132">Flux d’IP vérifier requiert que les ressources d’ordinateur virtuel hello est allouée toorun.</span><span class="sxs-lookup"><span data-stu-id="d713e-132">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="d713e-133">Analyser les résultats</span><span class="sxs-lookup"><span data-stu-id="d713e-133">Review Results</span></span>

<span data-ttu-id="d713e-134">Après l’exécution `az network watcher test-ip-flow` hello résultats sont retournés, exemple hello est résultats hello retournés à partir de hello précédant l’étape.</span><span class="sxs-lookup"><span data-stu-id="d713e-134">After running `az network watcher test-ip-flow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="d713e-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d713e-135">Next steps</span></span>

<span data-ttu-id="d713e-136">Si le trafic est bloqué et ne doit pas être, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui sont définis.</span><span class="sxs-lookup"><span data-stu-id="d713e-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="d713e-137">En savoir tooaudit vos paramètres de groupe de sécurité réseau, consultez [audit réseau sécurité groupes (NSG) avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d713e-137">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
