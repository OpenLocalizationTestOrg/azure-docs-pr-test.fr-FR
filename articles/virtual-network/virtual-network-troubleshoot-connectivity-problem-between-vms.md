---
title: "Résolution des problèmes de connectivité entre machines virtuelles Azure | Microsoft Docs"
description: "Découvrez comment résoudre les problèmes de connectivité entre machines virtuelles Azure."
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
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="dcdb7-103">Résolution des problèmes de connectivité entre machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="dcdb7-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="dcdb7-104">Vous pouvez rencontrer des problèmes de connectivité entre machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="dcdb7-105">Cet article fournit les étapes requises pour vous aider à résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="dcdb7-106">Symptôme</span><span class="sxs-lookup"><span data-stu-id="dcdb7-106">Symptom</span></span>

<span data-ttu-id="dcdb7-107">Une machine virtuelle Azure ne peut pas se connecter à une autre machine virtuelle de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-107">An Azure VM cannot connect to another Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="dcdb7-108">Instructions pour la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="dcdb7-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="dcdb7-109">Vérifiez si la carte réseau est mal configuré</span><span class="sxs-lookup"><span data-stu-id="dcdb7-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="dcdb7-110">Vérifiez si le trafic réseau est bloqué par le groupe de sécurité réseau ou UDR</span><span class="sxs-lookup"><span data-stu-id="dcdb7-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="dcdb7-111">Vérifiez si le trafic réseau est bloqué par un pare-feu de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="dcdb7-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="dcdb7-112">Vérifiez si une application ou un service de la machine virtuelle écoute sur le port</span><span class="sxs-lookup"><span data-stu-id="dcdb7-112">Check whether VM app or service is listening on the port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="dcdb7-113">Vérifiez si le problème est causé par SNAT</span><span class="sxs-lookup"><span data-stu-id="dcdb7-113">Check whether the problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="dcdb7-114">Vérifiez si le trafic est bloqué par des ACL pour la machine virtuelle classique</span><span class="sxs-lookup"><span data-stu-id="dcdb7-114">Check whether traffic is blocked by ACLs for the classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="dcdb7-115">Vérifiez si le point de terminaison est créé pour la machine virtuelle classique</span><span class="sxs-lookup"><span data-stu-id="dcdb7-115">Check whether the endpoint is created for the classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="dcdb7-116">Impossible de se connecter à un partage réseau de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="dcdb7-116">Unable to connect to a VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="dcdb7-117">Connectivité de réseau virtuel entre réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="dcdb7-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="dcdb7-118">Étapes de dépannage</span><span class="sxs-lookup"><span data-stu-id="dcdb7-118">Troubleshooting steps</span></span>

<span data-ttu-id="dcdb7-119">Suivez ces étapes pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-119">Follow these steps to troubleshoot the problem.</span></span> <span data-ttu-id="dcdb7-120">Vérifiez si le problème est résolu après chaque étape.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-120">Check whether the problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="dcdb7-121">Étape 1 : Vérifier si la carte réseau est mal configuré</span><span class="sxs-lookup"><span data-stu-id="dcdb7-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="dcdb7-122">Suivez [comment réinitialiser l’interface réseau pour Windows Azure VM](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="dcdb7-122">Follow [How to reset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="dcdb7-123">Si le problème se produit après la modification de l’interface réseau (NIC), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dcdb7-123">If the problem occurs after you modify the network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="dcdb7-124">**Machines virtuelles mulit-NIC**</span><span class="sxs-lookup"><span data-stu-id="dcdb7-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="dcdb7-125">Ajoutez une carte réseau.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-125">Add a NIC.</span></span>
2. <span data-ttu-id="dcdb7-126">Résoudre les problèmes dans la carte réseau défectueux ou supprimer des mauvais NIC.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-126">Fix the problems in the bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="dcdb7-127">Puis readd la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-127">Then readd the NIC.</span></span>

<span data-ttu-id="dcdb7-128">Pour plus d’informations, consultez [Ajouter ou supprimer des cartes réseau de machines virtuelles](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="dcdb7-128">For more information, see [Add network interfaces to or remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="dcdb7-129">**Machine virtuelle à carte réseau unique**</span><span class="sxs-lookup"><span data-stu-id="dcdb7-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="dcdb7-130">Redéployez la machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="dcdb7-131">Redéployer la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="dcdb7-132">Étape 2 : Vérifier si le trafic réseau est bloqué par le groupe de sécurité réseau ou UDR</span><span class="sxs-lookup"><span data-stu-id="dcdb7-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="dcdb7-133">Utiliser [Vérifiez que les flux IP de l’Observateur réseau](../network-watcher/network-watcher-ip-flow-verify-overview.md) et [l’enregistrement de flux de groupe de sécurité réseau](../network-watcher/network-watcher-nsg-flow-logging-overview.md) pour déterminer s’il existe un groupe de sécurité réseau ou un itinéraire défini par l’utilisateur qui interfère avec le flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="dcdb7-134">Étape 3 : Vérifier si le trafic réseau est bloqué par un pare-feu de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="dcdb7-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="dcdb7-135">Désactivez le pare-feu, puis testez le résultat.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-135">Disable the firewall, and then test the result.</span></span> <span data-ttu-id="dcdb7-136">Si le problème est résolu, vérifiez les paramètres dans le pare-feu et activer de nouveau.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-136">If the problem is resolved, validate the settings in the firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a><span data-ttu-id="dcdb7-137">Étape 4 : Vérifiez si une application ou un service de la machine virtuelle écoute sur le port</span><span class="sxs-lookup"><span data-stu-id="dcdb7-137">Step 4: Check whether VM app or service is listening on the port</span></span>

<span data-ttu-id="dcdb7-138">Vous pouvez utiliser une des méthodes suivantes pour vérifier si les Application de la machine virtuelle ou un Service est à l’écoute sur le port</span><span class="sxs-lookup"><span data-stu-id="dcdb7-138">You can use one of the following methods to check whether VM Application or Service is listening on the port</span></span>

- <span data-ttu-id="dcdb7-139">Exécutez les commandes suivantes pour vérifier si le serveur écoute sur ce port.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-139">Run the following commands to check whether the server is listening on that port.</span></span>

<span data-ttu-id="dcdb7-140">**Machine virtuelle Windows**</span><span class="sxs-lookup"><span data-stu-id="dcdb7-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="dcdb7-141">**Machine virtuelle Linux**</span><span class="sxs-lookup"><span data-stu-id="dcdb7-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="dcdb7-142">Exécutez le **Telnet** commande sur la machine virtuelle à elle-même pour tester le port.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-142">Run the **Telnet** command on the VM to itself to test the port.</span></span> <span data-ttu-id="dcdb7-143">Si le test échoue, application ou service n’est pas configuré pour écouter sur le port.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-143">If the test fails, application or service is not configured to listen on the port.</span></span>

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a><span data-ttu-id="dcdb7-144">Étape 5 : Vérifiez si le problème est causé par SNAT</span><span class="sxs-lookup"><span data-stu-id="dcdb7-144">Step 5: Check whether the problem is caused by SNAT</span></span>

<span data-ttu-id="dcdb7-145">Dans certains scénarios, l’ordinateur virtuel est placé derrière une solution d’équilibrer la charge qui a une dépendance sur les ressources en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-145">In some scenarios, the VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="dcdb7-146">Dans ces scénarios, si vous rencontrez des problèmes de connexion intermittents, le problème peut être dû à [l’épuisement du port SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="dcdb7-146">In these scenarios, if you experience intermittent connection problems, the problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="dcdb7-147">Pour résoudre ce problème, créez une adresse IP virtuelle (ou ILPIP pour classique) pour chaque ordinateur virtuel qui se trouve derrière l’équilibrage de charge et sécurisé avec le groupe de sécurité réseau ou de la liste ACL.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-147">To resolve the issue, create a VIP (or ILPIP for classic) for each VM that is behind the Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a><span data-ttu-id="dcdb7-148">Étape 6 : Vérifiez si le trafic est bloqué par des ACL pour la machine virtuelle classique</span><span class="sxs-lookup"><span data-stu-id="dcdb7-148">Step 6: Check whether traffic is blocked by ACLs for the classic VM</span></span>

<span data-ttu-id="dcdb7-149">Une liste ACL permet d’autoriser ou refuser le trafic de manière sélective pour un point de terminaison de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-149">An ACL provides the ability to selectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="dcdb7-150">Pour plus d’informations, consultez la page [Gestion de l’ACL sur un point de terminaison](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="dcdb7-150">For more information, see [Manage the ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a><span data-ttu-id="dcdb7-151">Étape 7 : Vérifiez si le point de terminaison est créé pour la machine virtuelle classique</span><span class="sxs-lookup"><span data-stu-id="dcdb7-151">Step 7: Check whether the endpoint is created for the classic VM</span></span>

<span data-ttu-id="dcdb7-152">Tous les ordinateurs virtuels que vous créez dans Azure à l’aide du modèle de déploiement classique peuvent communiquer automatiquement via un canal réseau privé avec d’autres machines virtuelles dans le même service cloud ou d’un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-152">All VMs that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="dcdb7-153">Toutefois, les ordinateurs sur d'autres réseaux virtuels requièrent des points de terminaison pour diriger le trafic réseau entrant vers une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-153">However, computers on other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="dcdb7-154">Pour plus d’informations, consultez [Configuration de points de terminaison](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="dcdb7-154">For more information, see [How to set up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a><span data-ttu-id="dcdb7-155">Étape 8 : Impossible de se connecter à un partage réseau de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="dcdb7-155">Step 8: Unable to connect to a VM network share</span></span>

<span data-ttu-id="dcdb7-156">Si vous ne parvenez pas à se connecter à un partage réseau de machine virtuelle, le problème peut résulter de cartes d’interface réseau non disponibles dans la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-156">If you are unable to connect to a VM network share, the problem can be caused by unavailable NICs in the VM.</span></span> <span data-ttu-id="dcdb7-157">Pour supprimer les cartes réseau non disponibles, consultez [Supprimer les cartes réseau non disponibles](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="dcdb7-157">To delete the unavailable NICs, see [How to delete the unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="dcdb7-158">Étape 9 : La connectivité réseau virtuel entre réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="dcdb7-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="dcdb7-159">Utiliser [Vérifiez que les flux IP de l’Observateur réseau](../network-watcher/network-watcher-ip-flow-verify-overview.md) et [l’enregistrement de flux de groupe de sécurité réseau](../network-watcher/network-watcher-nsg-flow-logging-overview.md) pour déterminer s’il existe un groupe de sécurité réseau ou un itinéraire défini par l’utilisateur qui interfère avec le flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="dcdb7-160">Vous pouvez également valider votre configuration de réseau virtuel Inter [ici](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="dcdb7-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="dcdb7-161">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="dcdb7-161">Need help?</span></span> <span data-ttu-id="dcdb7-162">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-162">Contact support.</span></span>
<span data-ttu-id="dcdb7-163">Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour obtenir une prise en charge rapide de votre problème.</span><span class="sxs-lookup"><span data-stu-id="dcdb7-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>