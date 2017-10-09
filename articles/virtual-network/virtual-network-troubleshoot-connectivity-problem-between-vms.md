---
title: "aaaTroubleshooting des problèmes de connectivité entre machines virtuelles Azure | Documents Microsoft"
description: "Découvrez comment tooTroubleshoot hello des problèmes de connectivité entre machines virtuelles Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="a533e-103">Résolution des problèmes de connectivité entre machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="a533e-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="a533e-104">Vous pouvez rencontrer des problèmes de connectivité entre machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="a533e-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="a533e-105">Cet article fournit la résolution des problèmes étapes toohelp vous résolvez ce problème.</span><span class="sxs-lookup"><span data-stu-id="a533e-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="a533e-106">Symptôme</span><span class="sxs-lookup"><span data-stu-id="a533e-106">Symptom</span></span>

<span data-ttu-id="a533e-107">Une machine virtuelle Azure ne peut pas se connecter à tooanother machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="a533e-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="a533e-108">Instructions pour la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a533e-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="a533e-109">Vérifiez si la carte réseau est mal configuré</span><span class="sxs-lookup"><span data-stu-id="a533e-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="a533e-110">Vérifiez si le trafic réseau est bloqué par le groupe de sécurité réseau ou UDR</span><span class="sxs-lookup"><span data-stu-id="a533e-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="a533e-111">Vérifiez si le trafic réseau est bloqué par un pare-feu de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a533e-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="a533e-112">Vérifiez si l’option application de la machine virtuelle ou un service écoute sur le port de hello</span><span class="sxs-lookup"><span data-stu-id="a533e-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="a533e-113">Vérifiez si le problème de hello est causée par SNAT</span><span class="sxs-lookup"><span data-stu-id="a533e-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="a533e-114">Vérifiez si le trafic est bloqué par des listes ACL pour hello VM classique</span><span class="sxs-lookup"><span data-stu-id="a533e-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="a533e-115">Vérifiez si le point de terminaison hello est créé pour hello VM classique</span><span class="sxs-lookup"><span data-stu-id="a533e-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="a533e-116">Partage de réseau de machine virtuelle tooa tooconnect Impossible</span><span class="sxs-lookup"><span data-stu-id="a533e-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="a533e-117">Connectivité de réseau virtuel entre réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="a533e-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="a533e-118">Étapes de dépannage</span><span class="sxs-lookup"><span data-stu-id="a533e-118">Troubleshooting steps</span></span>

<span data-ttu-id="a533e-119">Suivez ces problèmes de hello tootroubleshoot étapes.</span><span class="sxs-lookup"><span data-stu-id="a533e-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="a533e-120">Vérifiez si le problème de hello est résolu après chaque étape.</span><span class="sxs-lookup"><span data-stu-id="a533e-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="a533e-121">Étape 1 : Vérifier si la carte réseau est mal configuré</span><span class="sxs-lookup"><span data-stu-id="a533e-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="a533e-122">Suivez [comment tooreset interface réseau pour Windows Azure VM](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="a533e-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="a533e-123">Si le problème de hello se produit après avoir modifié l’interface de réseau hello (NIC), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a533e-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="a533e-124">**Machines virtuelles mulit-NIC**</span><span class="sxs-lookup"><span data-stu-id="a533e-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="a533e-125">Ajoutez une carte réseau.</span><span class="sxs-lookup"><span data-stu-id="a533e-125">Add a NIC.</span></span>
2. <span data-ttu-id="a533e-126">Résoudre les problèmes de hello dans hello incorrect supprimer ou carte réseau défectueux carte réseau.</span><span class="sxs-lookup"><span data-stu-id="a533e-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="a533e-127">Puis readd NIC de hello.</span><span class="sxs-lookup"><span data-stu-id="a533e-127">Then readd hello NIC.</span></span>

<span data-ttu-id="a533e-128">Pour plus d’informations, consultez [ajouter réseau interfaces tooor supprimer des machines virtuelles](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a533e-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="a533e-129">**Machine virtuelle à carte réseau unique**</span><span class="sxs-lookup"><span data-stu-id="a533e-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="a533e-130">Redéployez la machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="a533e-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="a533e-131">Redéployer la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="a533e-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="a533e-132">Étape 2 : Vérifier si le trafic réseau est bloqué par le groupe de sécurité réseau ou UDR</span><span class="sxs-lookup"><span data-stu-id="a533e-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="a533e-133">Utiliser [Vérifiez que les flux IP de l’Observateur réseau](../network-watcher/network-watcher-ip-flow-verify-overview.md) et [l’enregistrement de flux de groupe de sécurité réseau](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify s’il existe un groupe de sécurité réseau ou un itinéraire défini par l’utilisateur qui interfère avec le flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="a533e-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="a533e-134">Étape 3 : Vérifier si le trafic réseau est bloqué par un pare-feu de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a533e-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="a533e-135">Désactiver le pare-feu hello et testez les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="a533e-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="a533e-136">Si hello problème est résolu, vérifiez les paramètres de hello dans le pare-feu hello et réactiver.</span><span class="sxs-lookup"><span data-stu-id="a533e-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="a533e-137">Étape 4 : Vérifier si l’option application de la machine virtuelle ou un service écoute sur le port de hello</span><span class="sxs-lookup"><span data-stu-id="a533e-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="a533e-138">Vous pouvez utiliser une des hello suivant les méthodes toocheck si l’Application de la machine virtuelle ou un Service écoute sur le port de hello</span><span class="sxs-lookup"><span data-stu-id="a533e-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="a533e-139">Exécutez hello suivant de commandes toocheck si hello serveur écoute sur ce port.</span><span class="sxs-lookup"><span data-stu-id="a533e-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="a533e-140">**Machine virtuelle Windows**</span><span class="sxs-lookup"><span data-stu-id="a533e-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="a533e-141">**Machine virtuelle Linux**</span><span class="sxs-lookup"><span data-stu-id="a533e-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="a533e-142">Exécutez hello **Telnet** commande hello port de machine virtuelle tooitself tootest hello.</span><span class="sxs-lookup"><span data-stu-id="a533e-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="a533e-143">En cas de test de hello, application ou service n’est pas toolisten configuré sur le port hello.</span><span class="sxs-lookup"><span data-stu-id="a533e-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="a533e-144">Étape 5 : Vérifier si le problème de hello est causée par SNAT</span><span class="sxs-lookup"><span data-stu-id="a533e-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="a533e-145">Dans certains scénarios, hello machine virtuelle est placé derrière une solution d’équilibrer la charge qui a une dépendance sur les ressources en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="a533e-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="a533e-146">Dans ces scénarios, si vous rencontrez des problèmes de connexion intermittents, hello problème peut être dû [épuisement du port SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="a533e-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="a533e-147">problème de hello tooresolve, créer une adresse IP virtuelle (ou ILPIP pour classique) pour chaque ordinateur virtuel qui est derrière un équilibreur de charge hello et sécurisé avec le groupe de sécurité réseau ou de la liste ACL.</span><span class="sxs-lookup"><span data-stu-id="a533e-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="a533e-148">Étape 6 : Vérification si le trafic est bloqué par des listes ACL pour hello VM classique</span><span class="sxs-lookup"><span data-stu-id="a533e-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="a533e-149">Une liste ACL fournit hello capacité tooselectively autoriser ou refuser le trafic pour un point de terminaison de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a533e-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="a533e-150">Pour plus d’informations, consultez [gérer hello ACL sur un point de terminaison](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="a533e-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="a533e-151">Étape 7 : Vérification si le point de terminaison hello est créé pour hello VM classique</span><span class="sxs-lookup"><span data-stu-id="a533e-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="a533e-152">Tous les ordinateurs virtuels que vous créez dans Azure à l’aide du modèle de déploiement classique hello peuvent communiquer automatiquement via un canal réseau privé avec d’autres ordinateurs virtuels de hello que même service ou de réseau virtuel de cloud.</span><span class="sxs-lookup"><span data-stu-id="a533e-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="a533e-153">Toutefois, les ordinateurs sur d’autres réseaux virtuels nécessitent des points de terminaison toodirect hello réseau entrant trafic tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a533e-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="a533e-154">Pour plus d’informations, consultez [comment tooset des points de terminaison](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="a533e-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="a533e-155">Étape 8 : Le partage réseau VM Impossible de tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="a533e-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="a533e-156">Si vous êtes le partage de réseau de machine virtuelle tooa tooconnect impossible, problème de hello peut résulter de cartes d’interface réseau non disponibles dans hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a533e-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="a533e-157">toodelete hello indisponible cartes réseau, consultez [comment toodelete hello cartes réseau non disponible](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="a533e-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="a533e-158">Étape 9 : La connectivité réseau virtuel entre réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="a533e-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="a533e-159">Utiliser [Vérifiez que les flux IP de l’Observateur réseau](../network-watcher/network-watcher-ip-flow-verify-overview.md) et [l’enregistrement de flux de groupe de sécurité réseau](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify s’il existe un groupe de sécurité réseau ou un itinéraire défini par l’utilisateur qui interfère avec le flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="a533e-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="a533e-160">Vous pouvez également valider votre configuration de réseau virtuel Inter [ici](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="a533e-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="a533e-161">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="a533e-161">Need help?</span></span> <span data-ttu-id="a533e-162">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="a533e-162">Contact support.</span></span>
<span data-ttu-id="a533e-163">Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.</span><span class="sxs-lookup"><span data-stu-id="a533e-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
