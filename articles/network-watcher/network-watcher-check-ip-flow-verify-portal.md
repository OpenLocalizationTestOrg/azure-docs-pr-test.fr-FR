---
title: "Vérifier le trafic avec la vérification des flux IP Azure Network Watcher - Portail Azure | Microsoft Docs"
description: "Cet article explique comment savoir si le trafic en direction ou en provenance d’une machine virtuelle est autorisé ou refusé"
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
ms.openlocfilehash: 7db29c186cf6e6f3b40a680ab76f1d2763f806ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="459db-103">Vérifiez si le trafic est autorisé ou refusé en direction ou en provenance d’une machine virtuelle avec le composant de vérification des flux IP d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="459db-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="459db-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="459db-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="459db-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="459db-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="459db-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="459db-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="459db-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="459db-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="459db-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="459db-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="459db-109">La vérification des flux IP est une fonctionnalité de Network Watcher qui vous permet de vérifier si le trafic en direction ou en provenance d’une machine virtuelle est autorisé.</span><span class="sxs-lookup"><span data-stu-id="459db-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="459db-110">La validation peut être exécutée pour le trafic entrant ou sortant.</span><span class="sxs-lookup"><span data-stu-id="459db-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="459db-111">Cette fonctionnalité est très utile pour définir si une machine virtuelle peut actuellement communiquer avec une ressource externe ou une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="459db-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="459db-112">La vérification des flux IP peut être utilisée pour vérifier si les règles de votre groupe de sécurité réseau sont correctement configurées et pour résoudre les problèmes de flux bloqués par les règles de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="459db-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="459db-113">La vérification des flux IP permet aussi de s’assurer que le trafic que vous souhaitez bloquer est correctement bloqué par le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="459db-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="459db-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="459db-114">Before you begin</span></span>

<span data-ttu-id="459db-115">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Créer une instance d’Azure Network Watcher](network-watcher-create.md) pour créer un Network Watcher ou que vous disposez d’une instance existante de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="459db-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="459db-116">Ce scénario suppose également qu’un groupe de ressources avec une machine virtuelle valide existe et peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="459db-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="459db-117">Scénario</span><span class="sxs-lookup"><span data-stu-id="459db-117">Scenario</span></span>

<span data-ttu-id="459db-118">Ce scénario utilise la vérification des flux IP pour vérifier si une machine virtuelle peut communiquer avec une autre machine via le port 443.</span><span class="sxs-lookup"><span data-stu-id="459db-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="459db-119">Si le trafic est refusé, la règle de sécurité refusant ce trafic est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="459db-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="459db-120">Pour plus d’informations sur la vérification des flux IP, consultez la page [IP Flow Verify Overview (Vue d’ensemble de la fonction de vérification des flux IP)](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="459db-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="459db-121">Exécuter la vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="459db-121">Run IP flow verify</span></span>

<span data-ttu-id="459db-122">Accédez à Network Watcher et cliquez sur **Vérification du flux IP**.</span><span class="sxs-lookup"><span data-stu-id="459db-122">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="459db-123">Sélectionnez la machine virtuelle et l’interface réseau à partir desquelles vous souhaitez vérifier le trafic.</span><span class="sxs-lookup"><span data-stu-id="459db-123">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="459db-124">Entrez les informations de filtrage supplémentaires, puis cliquez sur **Vérifier**.</span><span class="sxs-lookup"><span data-stu-id="459db-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="459db-125">Une fois que vous cliquez sur **Vérifier**, le flux basé sur les critères que vous avez fournis est vérifié.</span><span class="sxs-lookup"><span data-stu-id="459db-125">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="459db-126">Le résultat est **Accès autorisé** ou **Accès refusé**.</span><span class="sxs-lookup"><span data-stu-id="459db-126">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="459db-127">Si l’accès est refusé, le groupe de sécurité réseau (NSG) et la règle de sécurité qui bloquent le trafic sont indiqués.</span><span class="sxs-lookup"><span data-stu-id="459db-127">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="459db-128">Si le refus du trafic correspond au comportement attendu, cela signifie que la règle a réussi.</span><span class="sxs-lookup"><span data-stu-id="459db-128">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="459db-129">La vérification des flux IP nécessite l’attribution de la ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="459db-129">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="459db-130">Comme vous pouvez le constater dans l’image suivante, le trafic HTTP sortant a été autorisé.</span><span class="sxs-lookup"><span data-stu-id="459db-130">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![vue d’ensemble Vérification du flux IP][1]

<span data-ttu-id="459db-132">Comme indiqué dans l’image suivante, le trafic est défini sur entrant et le port d’entrée est remplacé par 123.</span><span class="sxs-lookup"><span data-stu-id="459db-132">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="459db-133">Le trafic est maintenant refusé : le message « Accès refusé » est indiqué avec le groupe de sécurité réseau et la règle de sécurité qui refusent le trafic.</span><span class="sxs-lookup"><span data-stu-id="459db-133">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![résultats du flux IP][2]

## <a name="next-steps"></a><span data-ttu-id="459db-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="459db-135">Next steps</span></span>

<span data-ttu-id="459db-136">Si le trafic est bloqué alors qu’il ne devrait pas l’être, consultez [Gérer les groupes de sécurité réseau à partir du portail](../virtual-network/virtual-network-manage-nsg-arm-portal.md) afin de surveiller le groupe de sécurité réseau et les règles de sécurité définis.</span><span class="sxs-lookup"><span data-stu-id="459db-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













