---
title: "Configurer des filtres de routage pour l’homologation d’Azure ExpressRoute Microsoft : Portail | Microsoft Docs"
description: "Cet article décrit la façon dont les filtres de routage tooconfigure pour l’utilisation de Microsoft Peering hello portail Azure"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="76d28-103">Configurer des filtres de routage pour l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="76d28-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="76d28-104">Filtres de routage sont un moyen de tooconsume un sous-ensemble de services pris en charge via l’homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76d28-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="76d28-105">les étapes dans cette article vous aident à configurez et gérez des filtres de routage pour les circuits ExpressRoute Hello.</span><span class="sxs-lookup"><span data-stu-id="76d28-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="76d28-106">Dynamics 365 services et les services Office 365 comme Exchange Online, SharePoint Online et Skype pour entreprises, sont accessibles via l’homologation de Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="76d28-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="76d28-107">Lors de l’homologation Microsoft est configuré dans un circuit ExpressRoute, tous les services connexes toothese de préfixes sont publiés via des sessions BGP hello établies.</span><span class="sxs-lookup"><span data-stu-id="76d28-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="76d28-108">Une BGP Communauté valeur est attaché tooevery préfixe tooidentify hello du service qui vous est proposé via le préfixe de hello.</span><span class="sxs-lookup"><span data-stu-id="76d28-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="76d28-109">Pour obtenir la liste des valeurs de communauté BGP hello et services hello auxquels elles sont mappées à, consultez [les Communautés BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="76d28-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="76d28-110">Si vous avez besoin des services de connectivité de tooall, un grand nombre de préfixes est publié via BGP.</span><span class="sxs-lookup"><span data-stu-id="76d28-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="76d28-111">Cela augmente considérablement la taille de hello hello de tables d’itinéraires gérées par les routeurs au sein de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="76d28-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="76d28-112">Si vous envisagez tooconsume uniquement un sous-ensemble des services offerts via l’homologation Microsoft, vous pouvez réduire la taille hello de vos tables d’itinéraires de deux manières.</span><span class="sxs-lookup"><span data-stu-id="76d28-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="76d28-113">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="76d28-113">You can:</span></span>

- <span data-ttu-id="76d28-114">Filtrer les préfixes indésirables en appliquant des filtres de routage sur les communautés BGP.</span><span class="sxs-lookup"><span data-stu-id="76d28-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="76d28-115">Ceci est une pratique standard et très courante de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="76d28-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="76d28-116">Définir des filtres de routage et de les appliquer de circuit ExpressRoute de tooyour.</span><span class="sxs-lookup"><span data-stu-id="76d28-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="76d28-117">Un filtre d’itinéraire est une ressource que vous permet de sélectionner la liste hello des services que vous prévoyez tooconsume via l’homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76d28-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="76d28-118">ExpressRoute les routeurs n’envoient liste hello de préfixes qui font partie des services de toohello identifiés dans le filtre de routage hello.</span><span class="sxs-lookup"><span data-stu-id="76d28-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="76d28-119"><a name="about"></a>À propos des filtres de routage</span><span class="sxs-lookup"><span data-stu-id="76d28-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="76d28-120">Lors de l’homologation Microsoft est configuré sur votre circuit ExpressRoute, routeurs de bord Microsoft hello établissent une paire de sessions BGP avec les routeurs de périphérie hello (la vôtre ou votre fournisseur de connectivité).</span><span class="sxs-lookup"><span data-stu-id="76d28-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="76d28-121">Aucun itinéraire n’est publiés tooyour réseau.</span><span class="sxs-lookup"><span data-stu-id="76d28-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="76d28-122">réseau de tooyour tooenable itinéraire publications, vous devez associer un filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="76d28-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="76d28-123">Un filtre de routage vous permet d’identifier les services auxquels vous souhaitez tooconsume via votre circuit ExpressRoute homologation de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76d28-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="76d28-124">Il est essentiellement une liste blanche de toutes les valeurs de communauté hello BGP.</span><span class="sxs-lookup"><span data-stu-id="76d28-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="76d28-125">Une fois qu’une ressource de filtre d’itinéraire est définie et attaché tooan circuit ExpressRoute, tous les préfixes qui mappent les valeurs de communauté toohello BGP sont publiés tooyour réseau.</span><span class="sxs-lookup"><span data-stu-id="76d28-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="76d28-126">toobe tooattach en mesure des filtres de routage avec les services Office 365, vous devez disposer de services d’Office 365 tooconsume d’autorisation via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="76d28-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="76d28-127">Si vous n’êtes pas autorisé tooconsume Office 365 des services via ExpressRoute, filtres de routage tooattach hello opération échoue.</span><span class="sxs-lookup"><span data-stu-id="76d28-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="76d28-128">Pour plus d’informations sur le processus d’autorisation de hello, consultez [Azure ExpressRoute pour Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="76d28-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="76d28-129">Services de connectivité de 365 tooDynamics ne nécessite pas l’autorisation préalable.</span><span class="sxs-lookup"><span data-stu-id="76d28-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76d28-130">Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés via l’homologation Microsoft, même si les filtres de routage ne sont pas définis.</span><span class="sxs-lookup"><span data-stu-id="76d28-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="76d28-131">Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="76d28-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="76d28-132"><a name="workflow"></a>Flux de travail</span><span class="sxs-lookup"><span data-stu-id="76d28-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="76d28-133">toobe les toosuccessfully en mesure de se connecter à tooservices via l’homologation Microsoft, vous devez effectuer les hello configuration comme suit :</span><span class="sxs-lookup"><span data-stu-id="76d28-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="76d28-134">Vous devez disposer d’un circuit ExpressRoute actif où l’homologation Microsoft est approvisionnée.</span><span class="sxs-lookup"><span data-stu-id="76d28-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="76d28-135">Vous pouvez utiliser hello suivant les instructions tooaccomplish ces tâches :</span><span class="sxs-lookup"><span data-stu-id="76d28-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="76d28-136">[Créer un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="76d28-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="76d28-137">Hello circuit ExpressRoute doit être dans un état configuré et activé.</span><span class="sxs-lookup"><span data-stu-id="76d28-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="76d28-138">[Créer l’homologation Microsoft](expressroute-howto-routing-portal-resource-manager.md) si vous gérez la session BGP hello directement.</span><span class="sxs-lookup"><span data-stu-id="76d28-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="76d28-139">Sinon, demandez à votre fournisseur de connectivité de configurer l’homologation Microsoft pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="76d28-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="76d28-140">Vous devez créer et configurer un filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="76d28-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="76d28-141">Identifier hello services vous avec tooconsume via l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="76d28-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="76d28-142">Identifier la liste des valeurs de communauté BGP associés aux services de hello de hello</span><span class="sxs-lookup"><span data-stu-id="76d28-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="76d28-143">Créer une règle tooallow hello préfixe liste correspondance hello valeurs de communauté BGP</span><span class="sxs-lookup"><span data-stu-id="76d28-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="76d28-144">Vous devez joindre le circuit ExpressRoute toohello hello itinéraire filtre.</span><span class="sxs-lookup"><span data-stu-id="76d28-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="76d28-145">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="76d28-145">Before you begin</span></span>

<span data-ttu-id="76d28-146">Avant de commencer la configuration, assurez-vous que vous remplissez hello suivant des critères :</span><span class="sxs-lookup"><span data-stu-id="76d28-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="76d28-147">Hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="76d28-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="76d28-148">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="76d28-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="76d28-149">Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="76d28-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="76d28-150">Hello circuit ExpressRoute doit être dans un état configuré et activé.</span><span class="sxs-lookup"><span data-stu-id="76d28-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="76d28-151">Vous devez disposer d’une homologation Microsoft active.</span><span class="sxs-lookup"><span data-stu-id="76d28-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="76d28-152">Suivez les instructions de [création et modification de la configuration d’homologation](expressroute-howto-routing-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="76d28-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="76d28-153"><a name="prefixes"></a>Étape 1.</span><span class="sxs-lookup"><span data-stu-id="76d28-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="76d28-154">Obtenir la liste des préfixes et des valeurs de communauté BGP</span><span class="sxs-lookup"><span data-stu-id="76d28-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="76d28-155">1. Obtenir la liste des valeurs de communauté BGP</span><span class="sxs-lookup"><span data-stu-id="76d28-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="76d28-156">Les valeurs de communauté BGP associés aux services accessibles via l’homologation Microsoft n’est disponible dans hello [conditions de routage ExpressRoute](expressroute-routing.md) page.</span><span class="sxs-lookup"><span data-stu-id="76d28-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="76d28-157">2. Dressez la liste des valeurs de hello que vous souhaitez toouse</span><span class="sxs-lookup"><span data-stu-id="76d28-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="76d28-158">Dressez la liste des valeurs de communauté BGP souhaité toouse dans un filtre d’itinéraire hello.</span><span class="sxs-lookup"><span data-stu-id="76d28-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="76d28-159">Par exemple, hello valeur communautaire BGP pour les services de Dynamics 365 est 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="76d28-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="76d28-160"><a name="filter"></a>Étape 2.</span><span class="sxs-lookup"><span data-stu-id="76d28-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="76d28-161">Créer un filtre de routage et une règle de filtre</span><span class="sxs-lookup"><span data-stu-id="76d28-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="76d28-162">Un filtre de routage peut avoir qu’une seule règle, et la règle de hello doit être de type « Autoriser ».</span><span class="sxs-lookup"><span data-stu-id="76d28-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="76d28-163">Cette règle peut être associée à une liste des valeurs de communauté BGP.</span><span class="sxs-lookup"><span data-stu-id="76d28-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="76d28-164">1. Créer un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="76d28-164">1. Create a route filter</span></span>
<span data-ttu-id="76d28-165">Vous pouvez créer un filtre de routage en sélectionnant hello option toocreate une nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="76d28-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="76d28-166">Cliquez sur **nouveau** > **réseau** > **RouteFilter**, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="76d28-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![Créer un filtre de routage](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="76d28-168">Vous devez placer le filtre de routage hello dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="76d28-168">You must place hello route filter in a resource group.</span></span> 

![Créer un filtre de routage](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="76d28-170">2. Créer une règle de filtre</span><span class="sxs-lookup"><span data-stu-id="76d28-170">2. Create a filter rule</span></span>

<span data-ttu-id="76d28-171">Vous pouvez ajouter et gérer les règles de mise à jour en sélectionnant hello onglet règle votre filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="76d28-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![Créer un filtre de routage](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="76d28-173">Vous pouvez sélectionner hello services souhaités tooconnect toofrom hello liste déroulant et enregistrement la règle hello lorsqu’il est terminé.</span><span class="sxs-lookup"><span data-stu-id="76d28-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![Créer un filtre de routage](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="76d28-175"><a name="attach"></a>Étape 3.</span><span class="sxs-lookup"><span data-stu-id="76d28-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="76d28-176">Attacher le circuit ExpressRoute tooan hello itinéraire filtre</span><span class="sxs-lookup"><span data-stu-id="76d28-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="76d28-177">Vous pouvez attacher le circuit de tooa hello route filtre en sélectionnant le bouton « Ajouter un Circuit » de hello, circuit ExpressRoute de hello à partir de la liste déroulante hello.</span><span class="sxs-lookup"><span data-stu-id="76d28-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![Créer un filtre de routage](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="76d28-179"><a name="getproperties"></a>propriétés de hello tooget d’un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="76d28-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="76d28-180">Vous pouvez afficher les propriétés d’un filtre de routage lorsque vous ouvrez des ressources de hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="76d28-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![Créer un filtre de routage](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="76d28-182"><a name="updateproperties"></a>propriétés de hello tooupdate d’un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="76d28-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="76d28-183">Vous pouvez mettre à jour liste hello du circuit BGP Communauté valeurs tooa attaché en sélectionnant le bouton de hello « gérer les règles ».</span><span class="sxs-lookup"><span data-stu-id="76d28-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![Créer un filtre de routage](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Créer un filtre de routage](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="76d28-186"><a name="detach"></a>toodetach un filtre d’itinéraire à partir d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="76d28-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="76d28-187">toodetach un circuit de filtre de routage hello, cliquez avec le bouton droit sur le circuit de hello et cliquez sur « Dissocier ».</span><span class="sxs-lookup"><span data-stu-id="76d28-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![Créer un filtre de routage](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="76d28-189"><a name="delete"></a>toodelete un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="76d28-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="76d28-190">Vous pouvez supprimer un filtre de routage en sélectionnant le bouton de suppression hello.</span><span class="sxs-lookup"><span data-stu-id="76d28-190">You can delete a route filter by selecting hello delete button.</span></span> 

![Créer un filtre de routage](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="76d28-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76d28-192">Next steps</span></span>

<span data-ttu-id="76d28-193">Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="76d28-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
