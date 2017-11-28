---
title: "Vérifiez que le trafic d’aaaVerify le transfert IP de l’Observateur réseau Azure - portail Azure | Documents Microsoft"
description: "Cet article décrit comment toocheck si tooor le trafic à partir d’un ordinateur virtuel est autorisé ou refusé"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="3a997-103">Vérifiez si le trafic est autorisé ou refusé tooor à partir d’une machine virtuelle avec IP flux vérifier un composant de l’Observateur de réseau Azure</span><span class="sxs-lookup"><span data-stu-id="3a997-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3a997-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3a997-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="3a997-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a997-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="3a997-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3a997-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="3a997-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3a997-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="3a997-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="3a997-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="3a997-109">Vérifiez que les flux IP est une fonctionnalité de l’Observateur réseau qui vous permet de tooverify si le trafic est autorisé à tooor à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="3a997-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="3a997-110">la validation de Hello peut être exécutée pour le trafic entrant ou sortant.</span><span class="sxs-lookup"><span data-stu-id="3a997-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="3a997-111">Ce scénario est utile tooget un état actuel de si un ordinateur virtuel peut communiquer avec les ressources externes tooan ou une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="3a997-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="3a997-112">Les flux IP vérifier peut être utilisé tooverify si vos règles de groupe de sécurité réseau (NSG) sont correctement configurés et résoudre les problèmes de flux qui sont bloqués par les règles du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="3a997-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="3a997-113">Une autre raison de l’utilisation de IP flux Vérifiez à bloquer le trafic de tooensure est bloqué correctement par hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="3a997-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3a997-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3a997-114">Before you begin</span></span>

<span data-ttu-id="3a997-115">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau ou une instance existante de l’Observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="3a997-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="3a997-116">scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.</span><span class="sxs-lookup"><span data-stu-id="3a997-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="3a997-117">Scénario</span><span class="sxs-lookup"><span data-stu-id="3a997-117">Scenario</span></span>

<span data-ttu-id="3a997-118">Ce scénario utilise tooverify d’IP de flux de vérifier si un ordinateur virtuel peut communiquer avec l’ordinateur de tooanother sur le port 443.</span><span class="sxs-lookup"><span data-stu-id="3a997-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="3a997-119">Si le trafic de hello est refusé, elle retourne la règle de sécurité hello refuse ce trafic.</span><span class="sxs-lookup"><span data-stu-id="3a997-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="3a997-120">toolearn en savoir plus sur l’IP de flux de vérifier, visitez [flux vérifier la vue d’ensemble IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3a997-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="3a997-121">Exécuter la vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="3a997-121">Run IP flow verify</span></span>

<span data-ttu-id="3a997-122">Accédez tooyour Observateur réseau et cliquez sur **les flux IP vérifier**.</span><span class="sxs-lookup"><span data-stu-id="3a997-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="3a997-123">Sélectionnez hello virtual machine et l’interface réseau du trafic tooverify à partir de.</span><span class="sxs-lookup"><span data-stu-id="3a997-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="3a997-124">Entrez les informations de filtrage supplémentaires, puis cliquez sur **Vérifier**.</span><span class="sxs-lookup"><span data-stu-id="3a997-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="3a997-125">Une fois que vous cliquez sur **vérifier**, flux hello en fonction de critères hello vous avez fourni est activée.</span><span class="sxs-lookup"><span data-stu-id="3a997-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="3a997-126">résultat de Hello est **accès autorisé** ou **accès refusé**.</span><span class="sxs-lookup"><span data-stu-id="3a997-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="3a997-127">Si l’accès est refusé, hello du groupe de sécurité réseau (NSG) et règle de sécurité qui bloquent le trafic est fournie.</span><span class="sxs-lookup"><span data-stu-id="3a997-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="3a997-128">Si le refus hello du trafic est le comportement attendu, règle de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="3a997-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="3a997-129">Les flux IP vérifier requiert que la ressource de machine virtuelle hello est allouée.</span><span class="sxs-lookup"><span data-stu-id="3a997-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="3a997-130">Comme vous pouvez voir à partir de hello suivant l’image, le trafic HTTPS hello a été autorisé.</span><span class="sxs-lookup"><span data-stu-id="3a997-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![vue d’ensemble Vérification du flux IP][1]

<span data-ttu-id="3a997-132">Comme indiqué dans hello suivant l’image, le trafic est modifié tooinbound et hello entrant too123 de port modifié.</span><span class="sxs-lookup"><span data-stu-id="3a997-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="3a997-133">Le trafic est maintenant refusé, le message de salutation « Accès refusé » est fourni avec hello groupe et sécurité règle de sécurité réseau qui refusent le trafic de hello.</span><span class="sxs-lookup"><span data-stu-id="3a997-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![résultats du flux IP][2]

## <a name="next-steps"></a><span data-ttu-id="3a997-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a997-135">Next steps</span></span>

<span data-ttu-id="3a997-136">Si le trafic est bloqué et ne doit pas être, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui sont définis.</span><span class="sxs-lookup"><span data-stu-id="3a997-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













