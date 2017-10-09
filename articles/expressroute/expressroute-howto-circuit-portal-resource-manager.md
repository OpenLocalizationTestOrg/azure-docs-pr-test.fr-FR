---
title: "Créer et modifier un circuit ExpressRoute à l’aide du portail Azure | Microsoft Docs"
description: "Cet article décrit comment toocreate, configurer, vérifier, mettre à jour, supprimer et annuler le déploiement d’un circuit ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="829ec-103">Création et modification d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="829ec-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="829ec-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="829ec-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="829ec-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="829ec-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="829ec-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="829ec-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="829ec-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="829ec-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="829ec-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="829ec-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="829ec-109">Cet article décrit comment un circuit ExpressRoute d’Azure à l’aide de toocreate hello Azure portal et hello Azure Resource Manager modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="829ec-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="829ec-110">Hello suit également vous montre l’état de hello toocheck du circuit de hello, mettre à jour, supprimer et ou annuler le déploiement.</span><span class="sxs-lookup"><span data-stu-id="829ec-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="829ec-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="829ec-111">Before you begin</span></span>
* <span data-ttu-id="829ec-112">Hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="829ec-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="829ec-113">Assurez-vous d’avoir accès toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="829ec-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="829ec-114">Assurez-vous que vous disposez d’autorisations des ressources mise en réseau nouvelle toocreate.</span><span class="sxs-lookup"><span data-stu-id="829ec-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="829ec-115">Contactez votre administrateur de compte si vous n’avez pas les autorisations appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="829ec-116">Vous pouvez [visualiser une vidéo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) avant de commencer par ordre toobetter comprendre les étapes hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="829ec-117">Création et approvisionnement d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="829ec-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="829ec-118">1. Se connecter toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="829ec-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="829ec-119">À partir d’un navigateur, accédez à toohello [portail Azure](http://portal.azure.com) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="829ec-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="829ec-120">2. Créez un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="829ec-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="829ec-121">Votre circuit ExpressRoute sera facturé dès hello, qu'une clé de service est émise.</span><span class="sxs-lookup"><span data-stu-id="829ec-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="829ec-122">Veillez à effectuer cette opération lorsque le fournisseur de connectivité hello est circuit de hello tooprovision prêt.</span><span class="sxs-lookup"><span data-stu-id="829ec-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="829ec-123">Vous pouvez créer un circuit ExpressRoute en sélectionnant hello option toocreate une nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="829ec-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="829ec-124">Cliquez sur **nouveau** > **réseau** > **ExpressRoute**, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="829ec-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![Création d’un circuit ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="829ec-126">Après avoir cliqué sur **ExpressRoute**, vous verrez hello **circuit ExpressRoute de créer** panneau.</span><span class="sxs-lookup"><span data-stu-id="829ec-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="829ec-127">Lorsque vous remplacez les valeurs hello sur ce panneau, assurez-vous que vous spécifiez un niveau de référence (SKU) hello approprié et le contrôle de données.</span><span class="sxs-lookup"><span data-stu-id="829ec-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="829ec-128">**niveau** détermine si ExpressRoute standard ou un module complémentaire ExpressRoute Premium est activé.</span><span class="sxs-lookup"><span data-stu-id="829ec-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="829ec-129">Vous pouvez spécifier **Standard** tooget hello référence (SKU) standard ou **Premium** pour le module complémentaire de hello premium.</span><span class="sxs-lookup"><span data-stu-id="829ec-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="829ec-130">**Contrôle de données** détermine le type de facturation hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="829ec-131">Vous pouvez spécifier **Limité** pour un forfait de données limité, et **Illimité** pour un forfait de données illimité.</span><span class="sxs-lookup"><span data-stu-id="829ec-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="829ec-132">Notez que vous pouvez modifier le type de facturation hello de **Metered** trop**illimité**, mais vous ne pouvez pas modifier le type hello de **illimité** trop**Metered**.</span><span class="sxs-lookup"><span data-stu-id="829ec-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![Configurer le niveau de référence (SKU) hello et les données de contrôle](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="829ec-134">Notez que cet emplacement d’homologation hello indique hello [emplacement physique](expressroute-locations.md) où vous sont d’homologation avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="829ec-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="829ec-135">Il s’agit de **pas** lié trop propriété « Location », ce qui fait référence geography toohello où se trouve hello fournisseur de ressources réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="829ec-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="829ec-136">Elles ne sont pas liées, mais il est un toochoose de bonnes pratiques un emplacement d’homologation du circuit de hello du fournisseur de ressources réseau géographiquement fermer toohello.</span><span class="sxs-lookup"><span data-stu-id="829ec-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="829ec-137">3. Affichage des circuits hello et propriétés</span><span class="sxs-lookup"><span data-stu-id="829ec-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="829ec-138">**Afficher tous les circuits hello**</span><span class="sxs-lookup"><span data-stu-id="829ec-138">**View all hello circuits**</span></span>

<span data-ttu-id="829ec-139">Vous pouvez afficher tous les circuits hello que vous avez créé en sélectionnant **toutes les ressources** sur le menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![Afficher les circuits](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="829ec-141">**Afficher les propriétés de hello**</span><span class="sxs-lookup"><span data-stu-id="829ec-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Afficher les propriétés](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="829ec-143">4. Envoyer le fournisseur de connectivité hello service tooyour clé pour la configuration</span><span class="sxs-lookup"><span data-stu-id="829ec-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="829ec-144">Dans ce panneau, **état du fournisseur** fournit des informations sur l’état actuel de mise en service sur le côté du fournisseur de services hello hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="829ec-145">**État de circuit** fournit l’état de hello sur hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="829ec-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="829ec-146">Pour plus d’informations sur les États de configuration de circuit, consultez hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) l’article.</span><span class="sxs-lookup"><span data-stu-id="829ec-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="829ec-147">Lorsque vous créez un nouveau circuit ExpressRoute, circuit de hello sera Bonjour suivant l’état :</span><span class="sxs-lookup"><span data-stu-id="829ec-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="829ec-148">Statu du fournisseur : Non approvisionné</span><span class="sxs-lookup"><span data-stu-id="829ec-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="829ec-149">Statut du circuit : Activé</span><span class="sxs-lookup"><span data-stu-id="829ec-149">Circuit status: Enabled</span></span>

![Lancer le processus d’approvisionnement](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="829ec-151">circuit de Hello modifiera toohello suivant l’état lorsque le fournisseur de connectivité hello est en cours de hello de l’activer pour vous :</span><span class="sxs-lookup"><span data-stu-id="829ec-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="829ec-152">Statut du fournisseur : En cours d’approvisionnement </span><span class="sxs-lookup"><span data-stu-id="829ec-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="829ec-153">Statut du circuit : Activé</span><span class="sxs-lookup"><span data-stu-id="829ec-153">Circuit status: Enabled</span></span>

<span data-ttu-id="829ec-154">Pour vous toobe en mesure de toouse un circuit ExpressRoute, il doit être Bonjour suivant l’état :</span><span class="sxs-lookup"><span data-stu-id="829ec-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="829ec-155">Statut du fournisseur : Approvisionné</span><span class="sxs-lookup"><span data-stu-id="829ec-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="829ec-156">Statut du circuit : Activé</span><span class="sxs-lookup"><span data-stu-id="829ec-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="829ec-157">5. Vérifier régulièrement le statut de hello et état hello de clé du circuit hello</span><span class="sxs-lookup"><span data-stu-id="829ec-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="829ec-158">Vous pouvez afficher les propriétés de hello du circuit hello qui vous intéresse en le sélectionnant.</span><span class="sxs-lookup"><span data-stu-id="829ec-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="829ec-159">Vérifiez hello **état du fournisseur** et assurez-vous qu’il a transféré trop**configuré** avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="829ec-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![Statut du circuit et du fournisseur](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="829ec-161">6. Créer votre configuration de routage</span><span class="sxs-lookup"><span data-stu-id="829ec-161">6. Create your routing configuration</span></span>
<span data-ttu-id="829ec-162">Pour obtenir des instructions, consultez toohello [circuit ExpressRoute de configuration de routage](expressroute-howto-routing-portal-resource-manager.md) toocreate de l’article et modifier des homologations de circuit.</span><span class="sxs-lookup"><span data-stu-id="829ec-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="829ec-163">Ces instructions s’appliquent uniquement à toocircuits qui sont créés avec des fournisseurs de services qui offrent des services de couche 2 de connectivité.</span><span class="sxs-lookup"><span data-stu-id="829ec-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="829ec-164">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="829ec-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="829ec-165">7. Lier un circuit ExpressRoute de tooan réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="829ec-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="829ec-166">Ensuite, lier un circuit ExpressRoute de tooyour réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="829ec-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="829ec-167">Hello d’utilisation [liaison virtuel réseaux tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article lorsque vous travaillez avec un modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="829ec-168">État de hello lors de l’obtention d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="829ec-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="829ec-169">Vous pouvez afficher l’état hello d’un circuit en la sélectionnant.</span><span class="sxs-lookup"><span data-stu-id="829ec-169">You can view hello status of a circuit by selecting it.</span></span> 

![Statut d’un circuit ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="829ec-171">Modification d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="829ec-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="829ec-172">Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.</span><span class="sxs-lookup"><span data-stu-id="829ec-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="829ec-173">Vous pouvez effectuer hello suivant sans interruption de service :</span><span class="sxs-lookup"><span data-stu-id="829ec-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="829ec-174">Activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="829ec-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="829ec-175">La bande passante de hello augmentation de votre circuit ExpressRoute fourni la capacité est disponible sur le port hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="829ec-176">Notez que la bande passante hello d’un circuit de rétrogradation n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="829ec-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="829ec-177">Modifier hello plan à partir de données de limitées tooUnlimited données de contrôle.</span><span class="sxs-lookup"><span data-stu-id="829ec-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="829ec-178">Notez ce plan de contrôle hello modification à partir de tooMetered données illimité que données ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="829ec-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="829ec-179">Vous pouvez activer et désactiver *Autoriser les opérations classiques*.</span><span class="sxs-lookup"><span data-stu-id="829ec-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="829ec-180">Pour plus d’informations sur les limites et limitations, consultez toohello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="829ec-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="829ec-181">toomodify un circuit ExpressRoute, cliquez sur hello **Configuration** comme indiqué dans la figure ci-dessous hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![Modifier le circuit](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="829ec-183">Vous pouvez modifier la bande passante hello, référence (SKU), modèle de facturation et autoriser des opérations classiques dans le panneau de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="829ec-184">Vous avez peut-être circuit ExpressRoute de hello toorecreate si la capacité inadéquate est sur le port existant hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="829ec-185">Vous ne peut pas mettre à niveau de circuit de hello si aucune capacité supplémentaire n’est disponible à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="829ec-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="829ec-186">Vous ne pouvez pas réduire la bande passante hello d’un circuit ExpressRoute sans interruption de service.</span><span class="sxs-lookup"><span data-stu-id="829ec-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="829ec-187">Rétrogradation de la bande passante vous oblige le circuit ExpressRoute de hello toodeprovision et puis reconfigurez un circuit ExpressRoute de nouveau.</span><span class="sxs-lookup"><span data-stu-id="829ec-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="829ec-188">Désactiver un module complémentaire premium opération peut échouer si vous utilisez des ressources qui sont supérieures à ce qui est autorisé pour le circuit de standard hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="829ec-189">Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="829ec-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="829ec-190">Vous pouvez supprimer votre circuit ExpressRoute en sélectionnant hello **supprimer** icône.</span><span class="sxs-lookup"><span data-stu-id="829ec-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="829ec-191">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="829ec-191">Note hello following:</span></span>

* <span data-ttu-id="829ec-192">Vous devez supprimer le lien de tous les réseaux virtuels à partir de hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="829ec-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="829ec-193">Si cette opération échoue, vérifiez si les réseaux virtuels sont liés toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="829ec-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="829ec-194">Si le fournisseur de service du circuit ExpressRoute hello état d’approvisionnement est **Provisioning** ou **configuré** vous devez collaborer avec votre circuit de hello toodeprovision service fournisseur de leur côté.</span><span class="sxs-lookup"><span data-stu-id="829ec-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="829ec-195">Nous allons continuer tooreserve ressources et vous facturer jusqu'à ce que le fournisseur de services hello termine de circuit de hello désaffectation et nous avertit.</span><span class="sxs-lookup"><span data-stu-id="829ec-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="829ec-196">Si le fournisseur de services hello a annulé le circuit de hello (fournisseur de services hello état d’approvisionnement est défini trop**non préparé**) vous pouvez ensuite supprimer le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="829ec-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="829ec-197">Cela arrêtera la facturation pour le circuit de hello</span><span class="sxs-lookup"><span data-stu-id="829ec-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="829ec-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="829ec-198">Next steps</span></span>
<span data-ttu-id="829ec-199">Après avoir créé votre circuit, assurez-vous que vous hello suivant :</span><span class="sxs-lookup"><span data-stu-id="829ec-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="829ec-200">Créer et modifier le routage le routage pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="829ec-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="829ec-201">Lier votre réseau virtuel de tooyour circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="829ec-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

