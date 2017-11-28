---
title: "Ajouter plusieurs tooa connexions de passerelle Site-à-Site VPN réseau virtuel : portail Azure : le Gestionnaire de ressources | Documents Microsoft"
description: "Ajouter plusieurs S2S connexions tooa passerelle VPN de site qui dispose d’une connexion existante"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="3bb2b-103">Ajouter un tooa de connexion de Site à Site réseau virtuel avec une connexion de passerelle VPN existante</span><span class="sxs-lookup"><span data-stu-id="3bb2b-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3bb2b-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3bb2b-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="3bb2b-105">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="3bb2b-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="3bb2b-106">Cet article vous guide tout au long de l’aide de hello tooadd portail Azure Site à Site (S2S) connexions tooa passerelle VPN qui dispose d’une connexion existante.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="3bb2b-107">Ce type de connexion est souvent tooas auxquels une configuration de « multisite ».</span><span class="sxs-lookup"><span data-stu-id="3bb2b-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="3bb2b-108">Vous pouvez ajouter un tooa de connexion réseau virtuel qui possède déjà un S2S connexion, une connexion Point à Site ou un réseau à connexion S2S.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="3bb2b-109">L’ajout de connexions est soumis à certaines limitations.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="3bb2b-110">Vérifiez hello [avant de commencer](#before) section dans cette tooverify article avant de commencer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="3bb2b-111">Cet article s’applique tooVNets créé à l’aide du modèle de déploiement du Gestionnaire de ressources hello qui ont une passerelle VPN de RouteBased.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="3bb2b-112">Ces étapes ne s’appliquent pas à la configuration des connexions coexistence tooExpressRoute/Site à Site.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="3bb2b-113">Consultez l’article [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) (Connexions coexistantes ExpressRoute/S2S) pour en savoir plus sur les connexions coexistantes.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="3bb2b-114">Outils et modèles de déploiement</span><span class="sxs-lookup"><span data-stu-id="3bb2b-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="3bb2b-115">Nous mettons à jour ce tableau à mesure que de nouveaux articles et des outils supplémentaires sont disponibles pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="3bb2b-116">Quand un article est disponible, nous lier directement tooit à partir de cette table.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="3bb2b-117"><a name="before"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3bb2b-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="3bb2b-118">Vérifiez que hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3bb2b-118">Verify hello following items:</span></span>

* <span data-ttu-id="3bb2b-119">Vous ne créez pas de connexion coexistante ExpressRoute/S2S.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="3bb2b-120">Vous avez un réseau virtuel qui a été créé à l’aide du modèle de déploiement du Gestionnaire de ressources hello avec une connexion existante.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="3bb2b-121">passerelle de réseau virtuel Hello pour votre réseau virtuel est RouteBased.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="3bb2b-122">Si vous avez une passerelle VPN de PolicyBased, vous devez supprimer la passerelle de réseau virtuel hello et créer une passerelle VPN en tant que RouteBased.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="3bb2b-123">Aucune des plages d’adresses hello se chevauchent pour une des hello ce réseau virtuel se connecte à des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="3bb2b-124">Vous avez le périphérique VPN compatible et une personne qui est en mesure de tooconfigure il.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="3bb2b-125">Consultez [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="3bb2b-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="3bb2b-126">Si vous n’êtes pas familiarisé avec la configuration de votre périphérique VPN, ou vous n’êtes pas familiarisé avec les plages d’adresses IP hello situés dans la configuration de votre réseau local, vous devez toocoordinate avec une personne qui peut fournir ces informations pour vous.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="3bb2b-127">Vous disposez d’une adresse IP publique exposée en externe pour votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="3bb2b-128">Cette adresse IP ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="3bb2b-129"><a name="part1"></a>Partie 1 - Configuration d’une connexion</span><span class="sxs-lookup"><span data-stu-id="3bb2b-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="3bb2b-130">À partir d’un navigateur, accédez à toohello [portail Azure](http://portal.azure.com) et, si nécessaire, connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="3bb2b-131">Cliquez sur **toutes les ressources** et recherchez votre **passerelle de réseau virtuel** à partir de la liste de hello des ressources, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="3bb2b-132">Sur hello **passerelle de réseau virtuel** panneau, cliquez sur **connexions**.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="3bb2b-133">![Panneau Connexions](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Panneau Connexions")</span><span class="sxs-lookup"><span data-stu-id="3bb2b-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="3bb2b-134">Sur hello **connexions** panneau, cliquez sur **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="3bb2b-135">![Bouton de connexion ajouter](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "bouton Ajouter la connexion")</span><span class="sxs-lookup"><span data-stu-id="3bb2b-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="3bb2b-136">Sur hello **ajouter une connexion** panneau, remplissez hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="3bb2b-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="3bb2b-137">**Nom :** nom hello toogive toohello site que vous créez connexion hello.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="3bb2b-138">**Type de connexion** : sélectionnez **Site à site (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="3bb2b-139">![Panneau de connexion ajouter](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Panneau de connexion ajouter")</span><span class="sxs-lookup"><span data-stu-id="3bb2b-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="3bb2b-140"><a name="part2"></a>Partie 2 - Ajout d’une passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="3bb2b-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="3bb2b-141">Cliquez sur **Passerelle de réseau local** ***Choisir une passerelle de réseau local***.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="3bb2b-142">Cela ouvre hello **passerelle de réseau local choisir** panneau.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="3bb2b-143">![Passerelle de réseau local choisir](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "passerelle de réseau local choisir")</span><span class="sxs-lookup"><span data-stu-id="3bb2b-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="3bb2b-144">Cliquez sur **nouvel** tooopen hello **créer une passerelle réseau local** panneau.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="3bb2b-145">![Panneau de passerelle de réseau local de créer](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "créer une passerelle réseau local")</span><span class="sxs-lookup"><span data-stu-id="3bb2b-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="3bb2b-146">Sur hello **créer une passerelle réseau local** panneau, remplissez hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="3bb2b-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="3bb2b-147">**Nom :** hello nom de ressource de la passerelle toogive toohello réseau local.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="3bb2b-148">**Adresse IP :** hello adresse IP publique du périphérique VPN de hello sur site hello que vous souhaitez tooconnect à.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="3bb2b-149">**L’espace d’adressage :** l’espace d’adressage que vous souhaitez toobe hello routé toohello nouveau site de réseau local.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="3bb2b-150">Cliquez sur **OK** sur hello **créer une passerelle réseau local** modifications de panneau toosave hello.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="3bb2b-151"><a name="part3"></a>Partie 3 : ajouter la clé partagée de hello et créer la connexion de hello</span><span class="sxs-lookup"><span data-stu-id="3bb2b-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="3bb2b-152">Sur hello **ajouter une connexion** panneau, ajouter la clé partagée de hello que vous souhaitez toouse toocreate votre connexion.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="3bb2b-153">Vous pouvez soit obtenir la clé partagée de hello à partir de votre périphérique VPN, ou créer un ici, puis configurer votre hello toouse du périphérique VPN même clé partagée.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="3bb2b-154">Hello important est que les clés de hello sont exactement hello identiques.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="3bb2b-155">![Clé partagée](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Clé partagée")</span><span class="sxs-lookup"><span data-stu-id="3bb2b-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="3bb2b-156">Au bas de hello du Panneau de hello, cliquez sur **OK** connexion de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="3bb2b-157"><a name="part4"></a>Partie 4 : vérifier la connexion VPN hello</span><span class="sxs-lookup"><span data-stu-id="3bb2b-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3bb2b-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3bb2b-158">Next steps</span></span>

<span data-ttu-id="3bb2b-159">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="3bb2b-160">Consultez les machines virtuelles de hello [cursus](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3bb2b-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
