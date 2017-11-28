---
title: "Suppression d’une passerelle de réseau virtuel : portail Azure : Resource Manager | Microsoft Docs"
description: "Supprimez une passerelle de réseau virtuel à l’aide du portail Azure dans le modèle de déploiement Gestionnaire des ressources."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="56c91-103">Supprimer une passerelle de réseau virtuel à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="56c91-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="56c91-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="56c91-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="56c91-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56c91-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="56c91-106">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="56c91-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="56c91-107">Deux approches sont possibles afin de supprimer une passerelle de réseau virtuel pour une configuration de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="56c91-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="56c91-108">Si vous voulez tout supprimer et recommencer, comme dans le cas d’un environnement de test, vous pouvez supprimer le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="56c91-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="56c91-109">Supprimer un groupe de ressources supprime toutes les ressources du groupe.</span><span class="sxs-lookup"><span data-stu-id="56c91-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="56c91-110">Cette méthode est recommandée seulement si vous ne voulez conserver aucune des ressources du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="56c91-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="56c91-111">Vous ne pouvez pas choisir de supprimer uniquement certaines ressources avec cette approche.</span><span class="sxs-lookup"><span data-stu-id="56c91-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="56c91-112">Si vous souhaitez conserver certaines ressources de votre groupe de ressources, la suppression d’une passerelle de réseau virtuel devient légèrement plus complexe.</span><span class="sxs-lookup"><span data-stu-id="56c91-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="56c91-113">Avant de supprimer la passerelle de réseau virtuel, vous devez commencer par supprimer toutes les ressources qui dépendent de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="56c91-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="56c91-114">Les étapes à suivre dépendent du type de connexions que vous avez créées et des ressources dépendantes de chaque connexion.</span><span class="sxs-lookup"><span data-stu-id="56c91-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="56c91-115">Supprimer une passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="56c91-115">Delete a VPN gateway</span></span>

<span data-ttu-id="56c91-116">Si vous souhaitez supprimer une passerelle de réseau virtuel, vous devez d’abord supprimer chaque ressource liée à la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="56c91-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="56c91-117">Les ressources doivent être supprimées dans un certain ordre en raison des dépendances.</span><span class="sxs-lookup"><span data-stu-id="56c91-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="56c91-118">À ce stade, la passerelle de réseau virtuel est supprimée.</span><span class="sxs-lookup"><span data-stu-id="56c91-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="56c91-119">Les étapes suivantes vous permettent de supprimer toutes les ressources qui ne sont plus utilisées.</span><span class="sxs-lookup"><span data-stu-id="56c91-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="56c91-120">Pour supprimer la passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="56c91-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="56c91-121">Sous **Toutes les ressources**, recherchez les passerelles de réseau local associées à chaque connexion.</span><span class="sxs-lookup"><span data-stu-id="56c91-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="56c91-122">Dans le panneau **Vue d’ensemble** de la passerelle de réseau local, cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="56c91-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="56c91-123">Pour supprimer la ressource de l’adresse IP publique de la passerelle</span><span class="sxs-lookup"><span data-stu-id="56c91-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="56c91-124">Sous **Toutes les ressources**, recherchez la ressource d’adresse IP publique qui a été associée à la passerelle.</span><span class="sxs-lookup"><span data-stu-id="56c91-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="56c91-125">Si la passerelle de réseau virtuel était active-active, vous verrez deux adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="56c91-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="56c91-126">Sur la page **Vue d’ensemble** de l’adresse IP publique, cliquez sur **Supprimer**, puis sur **Oui** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="56c91-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="56c91-127">Pour supprimer le sous-réseau de la passerelle</span><span class="sxs-lookup"><span data-stu-id="56c91-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="56c91-128">Sous **Toutes les ressources**, recherchez le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="56c91-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="56c91-129">Dans le panneau **Sous-réseaux**, cliquez sur **Sous-réseau de passerelle**, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="56c91-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="56c91-130">Cliquez sur **Oui** pour confirmer que vous souhaitez supprimer le sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="56c91-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="56c91-131"><a name="deleterg"></a>Supprimer une passerelle VPN en supprimant le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="56c91-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="56c91-132">Si vous n’avez pas besoin de conserver de ressources dans le groupe de ressources et que vous voulez simplement recommencer à zéro, vous pouvez supprimer tout un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="56c91-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="56c91-133">Il s’agit d’un moyen rapide de tout supprimer.</span><span class="sxs-lookup"><span data-stu-id="56c91-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="56c91-134">Les étapes suivantes s’appliquent uniquement au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="56c91-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="56c91-135">Sous **Toutes les ressources**, recherchez le groupe de ressources et cliquez pour ouvrir le panneau.</span><span class="sxs-lookup"><span data-stu-id="56c91-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="56c91-136">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="56c91-136">Click **Delete**.</span></span> <span data-ttu-id="56c91-137">Dans le panneau Supprimer, affichez les ressources affectées.</span><span class="sxs-lookup"><span data-stu-id="56c91-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="56c91-138">Vérifiez que vous voulez supprimer toutes ces ressources.</span><span class="sxs-lookup"><span data-stu-id="56c91-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="56c91-139">Dans le cas contraire, utilisez les étapes sous [Supprimer une passerelle VPN](#deletegw) en haut de cet article.</span><span class="sxs-lookup"><span data-stu-id="56c91-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="56c91-140">Pour continuer, saisissez le nom du groupe de ressources que vous souhaitez supprimer, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="56c91-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>