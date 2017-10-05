---
title: "Impossible de supprimer un réseau virtuel dans Azure | Microsoft Docs"
description: "Découvrez comment résoudre le problème de suppression impossible d’un réseau virtuel dans Azure."
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
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: 55c42a91bb1c5fad289b975ffae8ce4d6e7343dd
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a><span data-ttu-id="83471-103">Résolution de problème : impossible de supprimer un réseau virtuel dans Azure</span><span class="sxs-lookup"><span data-stu-id="83471-103">Troubleshooting: Failed to delete a virtual network in Azure</span></span>

<span data-ttu-id="83471-104">Vous rencontrez peut-être des erreurs lors de vos tentatives de suppression de réseau virtuel dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="83471-104">You might receive errors when you try to delete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="83471-105">Cet article fournit les étapes requises pour vous aider à résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="83471-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="83471-106">Instructions pour la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="83471-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="83471-107">[Vérifiez si une passerelle de réseau virtuel s’exécute dans le réseau virtuel](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="83471-107">[Check whether a virtual network gateway is running in the virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="83471-108">[Vérifiez si une passerelle d’application s’exécute dans le réseau virtuel](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="83471-108">[Check whether an application gateway is running in the virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="83471-109">[Vérifiez si Azure Active Directory Domain Services est activé dans le réseau virtuel](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="83471-109">[Check whether Azure Active Directory Domain Service is enabled in the virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="83471-110">[Vérifiez si le réseau virtuel est connecté à d’autres ressources](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="83471-110">[Check whether the virtual network is connected to other resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="83471-111">[Vérifiez si une machine virtuelle s’exécute toujours dans le réseau virtuel](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="83471-111">[Check whether a virtual machine is still running in the virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="83471-112">[Vérifiez si le réseau virtuel est bloqué en cours de migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="83471-112">[Check whether the virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="83471-113">Étapes de dépannage</span><span class="sxs-lookup"><span data-stu-id="83471-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="83471-114">Vérifier si une passerelle de réseau virtuel s’exécute dans le réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="83471-114">Check whether a virtual network gateway is running in the virtual network</span></span>

<span data-ttu-id="83471-115">Pour supprimer le réseau virtuel, vous devez d’abord supprimer la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="83471-115">To remove the virtual network, you must first remove the virtual network gateway.</span></span>

<span data-ttu-id="83471-116">Pour les réseaux virtuels classiques, accédez à la **Vue d’ensemble** du réseau virtuel classique dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="83471-116">For classic virtual networks, go to the **Overview** page of the classic virtual network in the Azure portal.</span></span> <span data-ttu-id="83471-117">Si la passerelle est en cours d’exécution dans le réseau virtuel, vous verrez son adresse IP dans la section **Connexions VPN**.</span><span class="sxs-lookup"><span data-stu-id="83471-117">In the **VPN connections** section, if the gateway is running in the virtual network, you will see the IP address of the gateway.</span></span> 

![Vérifier si la passerelle est en cours d’exécution](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="83471-119">Pour les réseaux virtuels, accédez à la page **Vue d’ensemble** du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="83471-119">For virtual networks, go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="83471-120">Recherchez la passerelle de réseau virtuel dans les **Appareils connectés**.</span><span class="sxs-lookup"><span data-stu-id="83471-120">Check **Connected devices** for the virtual network gateway.</span></span>

![Vérifier l’appareil connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="83471-122">Avant de pouvoir supprimer la passerelle, supprimez d’abord les objets de **connexion** de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="83471-122">Before you can remove the gateway, first remove any **Connection** objects in the gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="83471-123">Vérifier si une passerelle d’application s’exécute dans le réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="83471-123">Check whether an application gateway is running in the virtual network</span></span>

<span data-ttu-id="83471-124">Accédez à la page **Vue d’ensemble** du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="83471-124">Go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="83471-125">Vérifiez les **Appareils connectés** dans la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="83471-125">Check the **Connected devices** for the application gateway.</span></span>

![Vérifier l’appareil connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="83471-127">S’il existe une passerelle d’application, vous devez la supprimer avant de pouvoir supprimer le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="83471-127">If there is an application gateway, you must remove it before you can delete the virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a><span data-ttu-id="83471-128">Vérifier si Azure Active Directory Domain Services est activé dans le réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="83471-128">Check whether Azure Active Directory Domain Service is enabled in the virtual network</span></span>

<span data-ttu-id="83471-129">Si Active Directory Domain Services est activé et connecté au réseau virtuel, vous ne pouvez pas supprimer ce dernier.</span><span class="sxs-lookup"><span data-stu-id="83471-129">If the Active Directory Domain Service is enabled and connected to the virtual network, you cannot delete this virtual network.</span></span> 

![Vérifier l’appareil connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="83471-131">Pour désactiver le service, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="83471-131">To disable the service, follow these steps:</span></span>

1. <span data-ttu-id="83471-132">Connectez-vous au [Portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="83471-132">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="83471-133">Dans le volet gauche, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83471-133">In the left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="83471-134">Sélectionnez le répertoire Azure Active Directory (Azure AD) où Active Directory Domain Services est activé.</span><span class="sxs-lookup"><span data-stu-id="83471-134">Select the Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="83471-135">Sélectionnez l’onglet **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="83471-135">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="83471-136">Sous **Services de domaine**, affectez à l’option **Activer les services de domaine pour cet annuaire** la valeur **Non**.</span><span class="sxs-lookup"><span data-stu-id="83471-136">Under **domain services**, change the **Enable domain services for this directory** option to **No**.</span></span>  

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a><span data-ttu-id="83471-137">Vérifier si le réseau virtuel est connecté à d’autres ressources</span><span class="sxs-lookup"><span data-stu-id="83471-137">Check whether the virtual network is connected to other resource</span></span>

<span data-ttu-id="83471-138">Recherchez les liaisons de circuit, les connexions et les homologations de réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="83471-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="83471-139">Tous ces éléments peuvent empêcher la suppression d’un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="83471-139">Any of these can cause a virtual network deletion to fail.</span></span> 

<span data-ttu-id="83471-140">Voici la séquence de suppression recommandée :</span><span class="sxs-lookup"><span data-stu-id="83471-140">The recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="83471-141">Connexions de passerelle</span><span class="sxs-lookup"><span data-stu-id="83471-141">Gateway connections</span></span>
2. <span data-ttu-id="83471-142">Passerelles</span><span class="sxs-lookup"><span data-stu-id="83471-142">Gateways</span></span>
3. <span data-ttu-id="83471-143">Adresses IP</span><span class="sxs-lookup"><span data-stu-id="83471-143">IPs</span></span>
4. <span data-ttu-id="83471-144">Homologations de réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="83471-144">Virtual network peerings</span></span>
5. <span data-ttu-id="83471-145">App Service Environment (ASE)</span><span class="sxs-lookup"><span data-stu-id="83471-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a><span data-ttu-id="83471-146">Vérifier si une machine virtuelle s’exécute toujours dans le réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="83471-146">Check whether a virtual machine is still running in the virtual network</span></span>

<span data-ttu-id="83471-147">Vérifiez qu’aucune machine virtuelle ne s’exécute dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="83471-147">Make sure that no virtual machine is in the virtual network.</span></span>

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="83471-148">Vérifier si le réseau virtuel est bloqué en cours de migration</span><span class="sxs-lookup"><span data-stu-id="83471-148">Check whether the virtual network is stuck in migration</span></span>

<span data-ttu-id="83471-149">Si le réseau virtuel est bloqué dans un état de migration, il ne peut pas être supprimé.</span><span class="sxs-lookup"><span data-stu-id="83471-149">If the virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="83471-150">Exécutez la commande suivante pour annuler la migration, puis supprimez le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="83471-150">Run the following command to abort the migration, and then delete the virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="83471-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="83471-151">Next steps</span></span>

- [<span data-ttu-id="83471-152">Réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="83471-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="83471-153">FAQ sur les réseaux virtuels Azure</span><span class="sxs-lookup"><span data-stu-id="83471-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)