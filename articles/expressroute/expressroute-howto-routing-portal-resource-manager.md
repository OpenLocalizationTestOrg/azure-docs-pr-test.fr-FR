---
title: "Comment tooconfigure routage (homologation) pour un circuit ExpressRoute : le Gestionnaire de ressources : Azure | Documents Microsoft"
description: "Cet article vous guide tout au long des étapes hello pour la création et l’approvisionnement hello privés, publics et homologation Microsoft d’un circuit ExpressRoute. Cet article vous explique également comment toocheck état de hello, mettre à jour ou supprimer des homologations pour votre circuit."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="74549-104">Créer et modifier l’homologation pour un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="74549-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="74549-105">Cet article vous aide à créer et gérer la configuration de routage pour un circuit ExpressRoute de modèle de déploiement de gestionnaire de ressources hello à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="74549-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="74549-106">Vous pouvez également vérifier l’état de hello, update ou delete et annuler le déploiement homologations pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74549-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="74549-107">Si vous souhaitez toouse une autre méthode de toowork avec votre circuit, sélectionnez un article à partir de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="74549-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="74549-108">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="74549-108">Configuration prerequisites</span></span>

* <span data-ttu-id="74549-109">Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md) page hello [exigences routage](expressroute-routing.md) page et hello [workflows](expressroute-workflows.md) page avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="74549-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="74549-110">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="74549-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="74549-111">Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="74549-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="74549-112">Hello circuit ExpressRoute doit être dans un état configuré et activé pour vous toobe toorun en mesure des applets de commande hello dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="74549-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="74549-113">Si vous envisagez de toouse un hachage de clé/MD5 partagé, être toouse que cela des deux côtés de hello tunnel et limite hello le nombre de caractères au maximum de 25 tooa.</span><span class="sxs-lookup"><span data-stu-id="74549-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="74549-114">Ces instructions s’appliquent uniquement à toocircuits créé avec les fournisseurs de services offrant des services de connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="74549-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="74549-115">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="74549-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="74549-116">Nous n’effectuent pas homologations configurées par les fournisseurs de services via le portail de gestion des services hello.</span><span class="sxs-lookup"><span data-stu-id="74549-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="74549-117">Nous travaillons sur la prochaine activation de cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="74549-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="74549-118">Contactez votre fournisseur de services avant de configurer des homologations BGP.</span><span class="sxs-lookup"><span data-stu-id="74549-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="74549-119">Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74549-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="74549-120">Vous pouvez configurer les homologations dans l’ordre de votre choix.</span><span class="sxs-lookup"><span data-stu-id="74549-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="74549-121">Toutefois, il se peut que vous devez vous assurer que vous terminez configuration hello de chacun d’eux à la fois d’homologation.</span><span class="sxs-lookup"><span data-stu-id="74549-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="74549-122">Homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="74549-122">Azure private peering</span></span>

<span data-ttu-id="74549-123">Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello Azure configuration d’homologation privée pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74549-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="74549-124">toocreate l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="74549-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="74549-125">Configurer le circuit ExpressRoute de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="74549-126">Vous assurer que circuit de hello est entièrement configuré par le fournisseur de connectivité hello avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="74549-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="74549-128">Configurer une homologation privée Azure pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="74549-129">Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="74549-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="74549-130">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="74549-131">sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="74549-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="74549-132">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="74549-133">sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="74549-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="74549-134">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="74549-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="74549-135">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="74549-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="74549-136">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="74549-136">AS number for peering.</span></span> <span data-ttu-id="74549-137">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="74549-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="74549-138">Vous pouvez utiliser un numéro AS privé pour cette homologation.</span><span class="sxs-lookup"><span data-stu-id="74549-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="74549-139">Veillez à ne pas utiliser le numéro 65515.</span><span class="sxs-lookup"><span data-stu-id="74549-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="74549-140">**Facultatif :** un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="74549-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="74549-141">Sélectionnez la ligne de d’homologation privée Azure hello, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="74549-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![private](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="74549-143">Configurer l’homologation privée Azure.</span><span class="sxs-lookup"><span data-stu-id="74549-143">Configure private peering.</span></span> <span data-ttu-id="74549-144">Hello suivant image montre un exemple de configuration :</span><span class="sxs-lookup"><span data-stu-id="74549-144">hello following image shows a configuration example:</span></span>

  ![configurer l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="74549-146">Enregistrer la configuration de hello après avoir spécifié tous les paramètres.</span><span class="sxs-lookup"><span data-stu-id="74549-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="74549-147">Une fois la configuration de hello a été acceptée avec succès, vous voyez quelque chose de similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="74549-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![enregistrer l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="74549-149">tooview Azure privé d’homologation détails</span><span class="sxs-lookup"><span data-stu-id="74549-149">tooview Azure private peering details</span></span>

<span data-ttu-id="74549-150">Vous pouvez afficher les propriétés de hello d’une homologation privée Azure en sélectionnant hello d’homologation.</span><span class="sxs-lookup"><span data-stu-id="74549-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![afficher l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="74549-152">tooupdate configuration d’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="74549-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="74549-153">Vous pouvez sélectionner la ligne hello pour l’homologation et modifier les propriétés d’homologation hello.</span><span class="sxs-lookup"><span data-stu-id="74549-153">You can select hello row for peering and modify hello peering properties.</span></span>

![mettre à jour l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="74549-155">toodelete l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="74549-155">toodelete Azure private peering</span></span>

<span data-ttu-id="74549-156">Vous pouvez supprimer votre configuration d’homologation en sélectionnant l’icône de suppression hello, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="74549-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![supprimer l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="74549-158">Homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="74549-158">Azure public peering</span></span>

<span data-ttu-id="74549-159">Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello configuration d’homologation publique Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74549-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="74549-160">toocreate l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="74549-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="74549-161">Configurer le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74549-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="74549-162">Garantissent que circuit de hello est entièrement par le fournisseur de connectivité hello avant de continuer à obtenir.</span><span class="sxs-lookup"><span data-stu-id="74549-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![énumérer l’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="74549-164">Configurer l’homologation publique Azure pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="74549-165">Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="74549-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="74549-166">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="74549-167">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="74549-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="74549-168">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="74549-169">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="74549-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="74549-170">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="74549-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="74549-171">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="74549-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="74549-172">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="74549-172">AS number for peering.</span></span> <span data-ttu-id="74549-173">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="74549-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="74549-174">**Facultatif :** un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="74549-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="74549-175">Sélectionnez hello des lignes d’homologation publique Azure, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="74549-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![sélectionner la ligne d’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="74549-177">Configurez l’homologation publique.</span><span class="sxs-lookup"><span data-stu-id="74549-177">Configure public peering.</span></span> <span data-ttu-id="74549-178">Hello suivant image montre un exemple de configuration :</span><span class="sxs-lookup"><span data-stu-id="74549-178">hello following image shows a configuration example:</span></span>

  ![Configurer l’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="74549-180">Enregistrer la configuration de hello après avoir spécifié tous les paramètres.</span><span class="sxs-lookup"><span data-stu-id="74549-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="74549-181">Une fois la configuration de hello a été acceptée avec succès, vous voyez quelque chose de similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="74549-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Enregistrer la configuration d’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="74549-183">tooview Azure public d’homologation détails</span><span class="sxs-lookup"><span data-stu-id="74549-183">tooview Azure public peering details</span></span>

<span data-ttu-id="74549-184">Vous pouvez afficher les propriétés de hello d’homologation publique Azure en sélectionnant hello d’homologation.</span><span class="sxs-lookup"><span data-stu-id="74549-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![afficher les propriétés d’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="74549-186">tooupdate configuration d’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="74549-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="74549-187">Vous pouvez sélectionner la ligne hello pour l’homologation et modifier les propriétés d’homologation hello.</span><span class="sxs-lookup"><span data-stu-id="74549-187">You can select hello row for peering and modify hello peering properties.</span></span>

![sélectionner la ligne d’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="74549-189">toodelete l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="74549-189">toodelete Azure public peering</span></span>

<span data-ttu-id="74549-190">Vous pouvez supprimer votre configuration d’homologation en sélectionnant l’icône de suppression hello, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="74549-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![supprimer l’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="74549-192">Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="74549-192">Microsoft peering</span></span>

<span data-ttu-id="74549-193">Cette section vous permet de créer, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft hello pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74549-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74549-194">Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés par le biais d’homologation de Microsoft hello, même si les filtres de routage ne sont pas définis.</span><span class="sxs-lookup"><span data-stu-id="74549-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="74549-195">Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="74549-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="74549-196">Pour plus d’informations, consultez [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurer un filtre d’itinéraire pour l’homologation Microsoft).</span><span class="sxs-lookup"><span data-stu-id="74549-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="74549-197">l’homologation de Microsoft toocreate</span><span class="sxs-lookup"><span data-stu-id="74549-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="74549-198">Configurer le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74549-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="74549-199">Garantissent que circuit de hello est entièrement par le fournisseur de connectivité hello avant de continuer à obtenir.</span><span class="sxs-lookup"><span data-stu-id="74549-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![énumérer l’homologation Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="74549-201">Configurez Microsoft d’homologation pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="74549-202">Assurez-vous que vous avez hello suivant informations avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="74549-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="74549-203">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="74549-204">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="74549-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="74549-205">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="74549-206">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="74549-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="74549-207">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="74549-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="74549-208">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="74549-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="74549-209">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="74549-209">AS number for peering.</span></span> <span data-ttu-id="74549-210">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="74549-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="74549-211">Publié préfixes : vous devez fournir une liste de tous les préfixes que vous prévoyez tooadvertise sur la session BGP de hello.</span><span class="sxs-lookup"><span data-stu-id="74549-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="74549-212">Seuls les préfixes d'adresses IP publiques sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="74549-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="74549-213">Si vous envisagez un jeu de préfixes de toosend, vous pouvez envoyer une liste séparée par des virgules.</span><span class="sxs-lookup"><span data-stu-id="74549-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="74549-214">Ces préfixes doivent être inscrit tooyou dans un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="74549-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="74549-215">**Facultatif :** client ASN : Si vous ne les préfixes de publicité qui ne sont pas inscrit toohello d’homologation en tant que nombre, vous pouvez spécifier hello en tant que nombre toowhich ils sont inscrits.</span><span class="sxs-lookup"><span data-stu-id="74549-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="74549-216">Nom de Registre de routage : Vous pouvez spécifier hello RIR / IRR contre le hello comme nombre et les préfixes sont inscrits.</span><span class="sxs-lookup"><span data-stu-id="74549-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="74549-217">**Facultatif :** un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="74549-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="74549-218">Vous pouvez sélectionner hello homologation vous souhaitez tooconfigure, comme indiqué dans hello suivant exemple.</span><span class="sxs-lookup"><span data-stu-id="74549-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="74549-219">Sélectionnez la ligne de d’homologation Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="74549-219">Select hello Microsoft peering row.</span></span>

  ![sélectionner la ligne d’homologation Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="74549-221">Configurez l’homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74549-221">Configure Microsoft peering.</span></span> <span data-ttu-id="74549-222">Hello suivant image montre un exemple de configuration :</span><span class="sxs-lookup"><span data-stu-id="74549-222">hello following image shows a configuration example:</span></span>

  ![configurer l’homologation Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="74549-224">Enregistrer la configuration de hello après avoir spécifié tous les paramètres.</span><span class="sxs-lookup"><span data-stu-id="74549-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="74549-225">Si votre circuit obtient tooa 'Validation nécessaire' (comme indiqué dans l’image de hello) de l’état, vous devez ouvrir une tooshow de ticket de support preuve de possession de l’équipe de support tooour hello préfixes.</span><span class="sxs-lookup"><span data-stu-id="74549-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![Enregistrer la configuration d’homologation Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="74549-227">Vous pouvez ouvrir un ticket de support directement à partir de portail de hello, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="74549-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="74549-228">Une fois la configuration de hello a été acceptée avec succès, vous voyez quelque chose de similaire toohello suivant l’image :</span><span class="sxs-lookup"><span data-stu-id="74549-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="74549-229">informations d’homologation de tooview Microsoft</span><span class="sxs-lookup"><span data-stu-id="74549-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="74549-230">Vous pouvez afficher les propriétés de hello d’homologation publique Azure en sélectionnant hello d’homologation.</span><span class="sxs-lookup"><span data-stu-id="74549-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="74549-231">configuration d’homologation de tooupdate Microsoft</span><span class="sxs-lookup"><span data-stu-id="74549-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="74549-232">Vous pouvez sélectionner la ligne hello pour l’homologation et modifier les propriétés d’homologation hello.</span><span class="sxs-lookup"><span data-stu-id="74549-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="74549-233">l’homologation de Microsoft toodelete</span><span class="sxs-lookup"><span data-stu-id="74549-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="74549-234">Vous pouvez supprimer votre configuration d’homologation en sélectionnant l’icône de suppression hello, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="74549-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="74549-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74549-235">Next steps</span></span>

<span data-ttu-id="74549-236">Étape suivante, [lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="74549-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="74549-237">Pour plus d'informations sur les workflows ExpressRoute, consultez [Workflows ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="74549-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="74549-238">Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="74549-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="74549-239">Pour plus d’informations sur l’utilisation des réseaux virtuels, consultez la page [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74549-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
