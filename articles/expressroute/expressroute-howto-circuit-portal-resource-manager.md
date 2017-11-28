---
title: "Créer et modifier un circuit ExpressRoute à l’aide du portail Azure | Microsoft Docs"
description: "Cet article explique comment créer, approvisionner, vérifier, mettre à jour, supprimer et déprovisionner un circuit ExpressRoute."
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
ms.openlocfilehash: e3721cd3c031622788f553e71a6555b844f3f7dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="16c5a-103">Création et modification d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="16c5a-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16c5a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="16c5a-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="16c5a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="16c5a-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="16c5a-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="16c5a-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="16c5a-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="16c5a-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="16c5a-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="16c5a-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="16c5a-109">Cet article explique comment créer un circuit ExpressRoute à l’aide du portail Azure et du modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="16c5a-109">This article describes how to create an Azure ExpressRoute circuit by using the Azure portal and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="16c5a-110">Les étapes suivantes vous montreront également comment vérifier l’état du circuit, mettre à jour celui-ci, le supprimer et annuler son approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="16c5a-110">The following steps also show you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="16c5a-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="16c5a-111">Before you begin</span></span>
* <span data-ttu-id="16c5a-112">Examinez les [conditions préalables](expressroute-prerequisites.md) et les [flux de travail](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="16c5a-112">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="16c5a-113">Vérifiez que vous avez accès au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16c5a-113">Ensure that you have access to the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="16c5a-114">Assurez-vous que vous disposez des autorisations nécessaires pour créer des ressources réseau.</span><span class="sxs-lookup"><span data-stu-id="16c5a-114">Ensure that you have permissions to create new networking resources.</span></span> <span data-ttu-id="16c5a-115">Contactez votre administrateur de compte si vous n'avez pas les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="16c5a-115">Contact your account administrator if you do not have the right permissions.</span></span>
* <span data-ttu-id="16c5a-116">Vous pouvez [visualiser une vidéo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) avant de commencer afin de mieux comprendre les étapes.</span><span class="sxs-lookup"><span data-stu-id="16c5a-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order to better understand the steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="16c5a-117">Création et approvisionnement d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="16c5a-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-the-azure-portal"></a><span data-ttu-id="16c5a-118">1. Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16c5a-118">1. Sign in to the Azure portal</span></span>
<span data-ttu-id="16c5a-119">Dans un navigateur, accédez au [portail Azure](http://portal.azure.com) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="16c5a-119">From a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="16c5a-120">2. Créez un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="16c5a-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="16c5a-121">Votre circuit ExpressRoute sera facturé à partir de l’émission d'une clé de service.</span><span class="sxs-lookup"><span data-stu-id="16c5a-121">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="16c5a-122">Effectuez cette opération seulement quand le fournisseur de connectivité prêt à approvisionner le circuit.</span><span class="sxs-lookup"><span data-stu-id="16c5a-122">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

1. <span data-ttu-id="16c5a-123">Vous pouvez créer un circuit ExpressRoute en sélectionnant l'option permettant de créer une ressource.</span><span class="sxs-lookup"><span data-stu-id="16c5a-123">You can create an ExpressRoute circuit by selecting the option to create a new resource.</span></span> <span data-ttu-id="16c5a-124">Cliquez sur **Nouveau** > **Mise en réseau** > **ExpressRoute**, comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="16c5a-124">Click **New** > **Networking** > **ExpressRoute**, as shown in the following image:</span></span>
   
    ![Création d’un circuit ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="16c5a-126">Après avoir cliqué sur **ExpressRoute**, vous voyez s’afficher le panneau **Créer un circuit ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="16c5a-126">After you click **ExpressRoute**, you'll see the **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="16c5a-127">Quand vous remplissez les valeurs de ce panneau, veillez à spécifier le bon niveau de référence (SKU) et la bonne limitation des données.</span><span class="sxs-lookup"><span data-stu-id="16c5a-127">When you're filling in the values on this blade, make sure that you specify the correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="16c5a-128">**niveau** détermine si ExpressRoute standard ou un module complémentaire ExpressRoute Premium est activé.</span><span class="sxs-lookup"><span data-stu-id="16c5a-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="16c5a-129">Vous pouvez spécifier **Standard** pour obtenir la référence (SKU) standard ou **Premium** pour le module complémentaire Premium.</span><span class="sxs-lookup"><span data-stu-id="16c5a-129">You can specify **Standard** to get the standard SKU or **Premium** for the premium add-on.</span></span>
   * <span data-ttu-id="16c5a-130">**Limitation des données** détermine le type de facturation.</span><span class="sxs-lookup"><span data-stu-id="16c5a-130">**Data metering** determines the billing type.</span></span> <span data-ttu-id="16c5a-131">Vous pouvez spécifier **Limité** pour un forfait de données limité, et **Illimité** pour un forfait de données illimité.</span><span class="sxs-lookup"><span data-stu-id="16c5a-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="16c5a-132">Notez que vous pouvez changer le type de facturation de **Limité** en **Illimité**, mais que vous ne pouvez pas le changer de **Illimité** en **Limité**.</span><span class="sxs-lookup"><span data-stu-id="16c5a-132">Note that you can change the billing type from **Metered** to **Unlimited**, but you can't change the type from **Unlimited** to **Metered**.</span></span>
     
     ![Configurer le niveau de référence (SKU) et la limitation des données](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="16c5a-134">N’oubliez pas que l’emplacement d’homologation indique [l’emplacement physique](expressroute-locations.md) où vous vous homologuez auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="16c5a-134">Please be aware that the Peering Location indicates the [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="16c5a-135">Cet emplacement n’est **pas** lié à la propriété « Emplacement », qui fait référence à la zone géographique où se trouve le fournisseur de ressources réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="16c5a-135">This is **not** linked to "Location" property, which refers to the geography where the Azure Network Resource Provider is located.</span></span> <span data-ttu-id="16c5a-136">Bien que ces éléments ne soient pas liés, nous vous conseillons de choisir un fournisseur de ressources réseau géographiquement proche de l’emplacement d’homologation du circuit.</span><span class="sxs-lookup"><span data-stu-id="16c5a-136">While they are not related, it is a good practice to choose a Network Resource Provider geographically close to the Peering Location of the circuit.</span></span> 
> 
> 

### <a name="3-view-the-circuits-and-properties"></a><span data-ttu-id="16c5a-137">3. Afficher les circuits et les propriétés</span><span class="sxs-lookup"><span data-stu-id="16c5a-137">3. View the circuits and properties</span></span>
<span data-ttu-id="16c5a-138">**Afficher tous les circuits**</span><span class="sxs-lookup"><span data-stu-id="16c5a-138">**View all the circuits**</span></span>

<span data-ttu-id="16c5a-139">Vous pouvez afficher tous les circuits que vous avez créés en sélectionnant **Toutes les ressources** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="16c5a-139">You can view all the circuits that you created by selecting **All resources** on the left-side menu.</span></span>

![Afficher les circuits](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="16c5a-141">**Afficher les propriétés**</span><span class="sxs-lookup"><span data-stu-id="16c5a-141">**View the properties**</span></span>

    You can view the properties of the circuit by selecting it. On this blade, note the service key for the circuit. You must copy the circuit key for your circuit and pass it down to the service provider to complete the provisioning process. The circuit key is specific to your circuit.

![Afficher les propriétés](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="16c5a-143">4. Envoyer la clé de service à votre fournisseur de connectivité pour l’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="16c5a-143">4. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="16c5a-144">Dans ce panneau, **Statut du fournisseur** fournit des informations sur l’état actuel de l’approvisionnement du côté du fournisseur de service.</span><span class="sxs-lookup"><span data-stu-id="16c5a-144">On this blade, **Provider status** provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="16c5a-145">**Statut du circuit** indique l’état du côté Microsoft.</span><span class="sxs-lookup"><span data-stu-id="16c5a-145">**Circuit status** provides the state on the Microsoft side.</span></span> <span data-ttu-id="16c5a-146">Pour plus d’informations sur les états d’approvisionnement des circuits, consultez l’article [Flux de travail](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="16c5a-146">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="16c5a-147">Quand vous créez un circuit ExpressRoute, ce circuit affiche l’état suivant :</span><span class="sxs-lookup"><span data-stu-id="16c5a-147">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

<span data-ttu-id="16c5a-148">Statu du fournisseur : Non approvisionné</span><span class="sxs-lookup"><span data-stu-id="16c5a-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="16c5a-149">Statut du circuit : Activé</span><span class="sxs-lookup"><span data-stu-id="16c5a-149">Circuit status: Enabled</span></span>

![Lancer le processus d’approvisionnement](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="16c5a-151">Le circuit passe à l’état suivant quand le fournisseur de connectivité est sur le point de l’activer pour vous.</span><span class="sxs-lookup"><span data-stu-id="16c5a-151">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

<span data-ttu-id="16c5a-152">Statut du fournisseur : En cours d’approvisionnement </span><span class="sxs-lookup"><span data-stu-id="16c5a-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="16c5a-153">Statut du circuit : Activé</span><span class="sxs-lookup"><span data-stu-id="16c5a-153">Circuit status: Enabled</span></span>

<span data-ttu-id="16c5a-154">Pour pouvoir être utilisé, un circuit ExpressRoute doit être dans l’état suivant :</span><span class="sxs-lookup"><span data-stu-id="16c5a-154">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

<span data-ttu-id="16c5a-155">Statut du fournisseur : Approvisionné</span><span class="sxs-lookup"><span data-stu-id="16c5a-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="16c5a-156">Statut du circuit : Activé</span><span class="sxs-lookup"><span data-stu-id="16c5a-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="16c5a-157">5. Vérifier régulièrement le statut et l’état de la clé du circuit</span><span class="sxs-lookup"><span data-stu-id="16c5a-157">5. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="16c5a-158">Vous pouvez afficher les propriétés du circuit qui vous intéressent en le sélectionnant.</span><span class="sxs-lookup"><span data-stu-id="16c5a-158">You can view the properties of the circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="16c5a-159">Vérifiez le **Statut du fournisseur** et vérifiez qu’il est passé à **Approvisionné** avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="16c5a-159">Check the **Provider status** and ensure that it has moved to **Provisioned** before you continue.</span></span>

![Statut du circuit et du fournisseur](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="16c5a-161">6. Créer votre configuration de routage</span><span class="sxs-lookup"><span data-stu-id="16c5a-161">6. Create your routing configuration</span></span>
<span data-ttu-id="16c5a-162">Pour obtenir des instructions pas à pas, consultez l’article [Configuration du routage des circuits ExpressRoute](expressroute-howto-routing-portal-resource-manager.md) pour créer et modifier des homologations de circuit.</span><span class="sxs-lookup"><span data-stu-id="16c5a-162">For step-by-step instructions, refer to the [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16c5a-163">Ces instructions s’appliquent seulement aux circuits créés avec des fournisseurs de services proposant des services de connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="16c5a-163">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="16c5a-164">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="16c5a-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="16c5a-165">7. Lier un réseau virtuel à un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="16c5a-165">7. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="16c5a-166">Maintenant, vous devez lier un réseau virtuel à votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="16c5a-166">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="16c5a-167">Utilisez l’article [Liaison de réseaux virtuels à des circuits ExpressRoute](expressroute-howto-linkvnet-arm.md) quand vous travaillez avec le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="16c5a-167">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="16c5a-168">Récupération de l’état d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="16c5a-168">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="16c5a-169">Vous pouvez afficher l’état d’un circuit en le sélectionnant.</span><span class="sxs-lookup"><span data-stu-id="16c5a-169">You can view the status of a circuit by selecting it.</span></span> 

![Statut d’un circuit ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="16c5a-171">Modification d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="16c5a-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="16c5a-172">Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.</span><span class="sxs-lookup"><span data-stu-id="16c5a-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="16c5a-173">Vous pouvez effectuer les opérations suivantes sans entraîner d’interruption de service :</span><span class="sxs-lookup"><span data-stu-id="16c5a-173">You can do the following with no downtime:</span></span>

* <span data-ttu-id="16c5a-174">Activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="16c5a-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="16c5a-175">Augmenter la bande passante de votre circuit ExpressRoute à condition que la capacité disponible sur le port le permette.</span><span class="sxs-lookup"><span data-stu-id="16c5a-175">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="16c5a-176">Notez que la rétrogradation de la bande passante d'un circuit n'est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="16c5a-176">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="16c5a-177">Modifiez le plan de mesure de Données limitées à Données illimitées.</span><span class="sxs-lookup"><span data-stu-id="16c5a-177">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="16c5a-178">Notez que la modification du plan de limitation de Données illimitées à Données limitées n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="16c5a-178">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="16c5a-179">Vous pouvez activer et désactiver *Autoriser les opérations classiques*.</span><span class="sxs-lookup"><span data-stu-id="16c5a-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="16c5a-180">Pour plus d’informations sur les limites et les limitations, reportez-vous au [FAQ ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="16c5a-180">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="16c5a-181">Pour modifier un circuit ExpressRoute, cliquez sur la **Configuration** comme illustré dans la figure ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="16c5a-181">To modify an ExpressRoute circuit, click on the **Configuration** as shown in the figure below.</span></span>

![Modifier le circuit](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="16c5a-183">Vous pouvez modifier la bande passante, la référence (SKU), le modèle de facturation et autoriser les opérations classiques dans le panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="16c5a-183">You can modify the bandwidth, SKU, billing model and allow classic operations within the configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16c5a-184">Vous devrez peut-être recréer le circuit ExpressRoute si la capacité sur le port existant est inappropriée.</span><span class="sxs-lookup"><span data-stu-id="16c5a-184">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="16c5a-185">Vous ne pouvez pas mettre le circuit à niveau si aucune capacité supplémentaire n’est disponible à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="16c5a-185">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="16c5a-186">Vous ne pouvez pas réduire la bande passante d’un circuit ExpressRoute sans interrompre le service.</span><span class="sxs-lookup"><span data-stu-id="16c5a-186">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="16c5a-187">Le fait de passer à un niveau inférieur de bande passante vous oblige à annuler l’approvisionnement du circuit ExpressRoute, puis à réapprovisionner un nouveau circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="16c5a-187">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="16c5a-188">L’opération de désactivation du module complémentaire Premium peut échouer si vous utilisez des ressources supérieures à ce qui est autorisé pour le circuit standard.</span><span class="sxs-lookup"><span data-stu-id="16c5a-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="16c5a-189">Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="16c5a-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="16c5a-190">Vous pouvez supprimer votre circuit ExpressRoute en sélectionnant l’icône **Supprimer** .</span><span class="sxs-lookup"><span data-stu-id="16c5a-190">You can delete your ExpressRoute circuit by selecting the **delete** icon.</span></span> <span data-ttu-id="16c5a-191">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="16c5a-191">Note the following:</span></span>

* <span data-ttu-id="16c5a-192">Vous devez dissocier tous les réseaux virtuels du circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="16c5a-192">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="16c5a-193">Si cette opération échoue, vérifiez si certains de vos réseaux virtuels sont liés au circuit.</span><span class="sxs-lookup"><span data-stu-id="16c5a-193">If this operation fails, check whether any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="16c5a-194">Si l’état d’approvisionnement du fournisseur de services du circuit ExpressRoute est **En cours d’approvisionnement** ou **Approvisionné**, vous devez vous mettre en relation avec votre fournisseur de services pour annuler l’approvisionnement du circuit de son côté.</span><span class="sxs-lookup"><span data-stu-id="16c5a-194">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="16c5a-195">Nous continuerons à réserver des ressources et à vous facturer jusqu’à ce que le fournisseur de services termine le désapprovisionnement du circuit et nous en avertisse.</span><span class="sxs-lookup"><span data-stu-id="16c5a-195">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="16c5a-196">Si le fournisseur de services a annulé l’approvisionnement du circuit (l’état d’approvisionnement du fournisseur de services affiche la valeur **Non approvisionné**), vous pouvez supprimer le circuit.</span><span class="sxs-lookup"><span data-stu-id="16c5a-196">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="16c5a-197">Cette opération arrêtera la facturation du circuit</span><span class="sxs-lookup"><span data-stu-id="16c5a-197">This will stop billing for the circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c5a-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="16c5a-198">Next steps</span></span>
<span data-ttu-id="16c5a-199">Après avoir créé votre circuit, effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="16c5a-199">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="16c5a-200">Créer et modifier le routage le routage pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="16c5a-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="16c5a-201">Lier votre réseau virtuel à votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="16c5a-201">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

