---
title: "aaaCannot supprimer un réseau virtuel dans Azure | Documents Microsoft"
description: "Découvrez comment tootroubleshoot hello problème dans lequel vous ne pouvez pas supprimer un réseau virtuel dans Azure."
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
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="530ed-103">Résolution des problèmes : Échec de la toodelete un réseau virtuel dans Azure</span><span class="sxs-lookup"><span data-stu-id="530ed-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="530ed-104">Vous pouvez recevoir des erreurs lorsque vous essayez de toodelete un réseau virtuel dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="530ed-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="530ed-105">Cet article fournit la résolution des problèmes étapes toohelp vous résolvez ce problème.</span><span class="sxs-lookup"><span data-stu-id="530ed-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="530ed-106">Instructions pour la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="530ed-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="530ed-107">[Vérifiez si une passerelle de réseau virtuel s’exécute dans le réseau virtuel de hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="530ed-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="530ed-108">[Vérifiez si une passerelle d’application s’exécute dans le réseau virtuel de hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="530ed-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="530ed-109">[Vérifier si le Service de domaine Azure Active Directory est activée dans le réseau virtuel de hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="530ed-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="530ed-110">[Vérifiez si le réseau virtuel de hello est connecté tooother ressources](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="530ed-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="530ed-111">[Vérifiez si un ordinateur virtuel est en cours d’exécution dans le réseau virtuel de hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="530ed-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="530ed-112">[Vérifiez si le réseau virtuel de hello est bloquée dans la migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="530ed-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="530ed-113">Étapes de dépannage</span><span class="sxs-lookup"><span data-stu-id="530ed-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="530ed-114">Vérifiez si une passerelle de réseau virtuel s’exécute dans le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="530ed-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="530ed-115">réseau virtuel de hello tooremove, vous devez d’abord supprimer passerelle de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="530ed-116">Pour les réseaux virtuels classiques, accédez à toohello **vue d’ensemble** page de réseau virtuel classique de hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="530ed-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="530ed-117">Bonjour **connexions VPN** section, si hello est en cours d’exécution dans le réseau virtuel de hello, vous verrez hello IP adresse de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![Vérifier si la passerelle est en cours d’exécution](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="530ed-119">Pour les réseaux virtuels, accédez à toohello **vue d’ensemble** page de réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="530ed-120">Vérifiez **périphériques connectés** pour la passerelle de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Hello du périphérique connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="530ed-122">Vous pouvez supprimer la passerelle de hello, avant de supprimer les **connexion** objets dans la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="530ed-123">Vérifiez si une passerelle d’application s’exécute dans le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="530ed-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="530ed-124">Accédez toohello **vue d’ensemble** page de réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="530ed-125">Vérifiez hello **périphériques connectés** pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Hello du périphérique connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="530ed-127">S’il existe une passerelle d’application, vous devez le supprimer avant de pouvoir supprimer les réseaux virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="530ed-128">Vérifier si le Service de domaine Azure Active Directory est activée dans le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="530ed-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="530ed-129">Si hello des services de domaine Active Directory est activée et connectée toohello des réseaux virtuels, vous ne pouvez pas supprimer ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="530ed-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Hello du périphérique connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="530ed-131">toodisable hello service, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="530ed-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="530ed-132">Accédez toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="530ed-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="530ed-133">Dans le volet gauche de hello, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="530ed-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="530ed-134">Sélectionnez répertoire Azure Active Directory (Azure AD) hello qui a des services de domaine Active Directory activée.</span><span class="sxs-lookup"><span data-stu-id="530ed-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="530ed-135">Sélectionnez hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="530ed-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="530ed-136">Sous **services de domaine**, modifiez hello **activer les services de domaine pour ce répertoire** option trop**non**.</span><span class="sxs-lookup"><span data-stu-id="530ed-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="530ed-137">Vérifiez si le réseau virtuel de hello est connecté tooother ressource</span><span class="sxs-lookup"><span data-stu-id="530ed-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="530ed-138">Recherchez les liaisons de circuit, les connexions et les homologations de réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="530ed-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="530ed-139">Une de ces peut entraîner un toofail de suppression du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="530ed-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="530ed-140">Hello ordre de suppression recommandée est la suivante :</span><span class="sxs-lookup"><span data-stu-id="530ed-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="530ed-141">Connexions de passerelle</span><span class="sxs-lookup"><span data-stu-id="530ed-141">Gateway connections</span></span>
2. <span data-ttu-id="530ed-142">Passerelles</span><span class="sxs-lookup"><span data-stu-id="530ed-142">Gateways</span></span>
3. <span data-ttu-id="530ed-143">Adresses IP</span><span class="sxs-lookup"><span data-stu-id="530ed-143">IPs</span></span>
4. <span data-ttu-id="530ed-144">Homologations de réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="530ed-144">Virtual network peerings</span></span>
5. <span data-ttu-id="530ed-145">App Service Environment (ASE)</span><span class="sxs-lookup"><span data-stu-id="530ed-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="530ed-146">Vérifiez si un ordinateur virtuel est en cours d’exécution dans le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="530ed-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="530ed-147">Assurez-vous qu’aucun ordinateur virtuel n’est dans un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="530ed-148">Vérifiez si le réseau virtuel de hello est bloquée dans la migration</span><span class="sxs-lookup"><span data-stu-id="530ed-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="530ed-149">Si le réseau virtuel de hello est bloquée dans un état de migration, il ne peut pas être supprimé.</span><span class="sxs-lookup"><span data-stu-id="530ed-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="530ed-150">Exécutez hello après la migration de commande tooabort hello et ensuite supprimer le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="530ed-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="530ed-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="530ed-151">Next steps</span></span>

- [<span data-ttu-id="530ed-152">Réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="530ed-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="530ed-153">FAQ sur les réseaux virtuels Azure</span><span class="sxs-lookup"><span data-stu-id="530ed-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)