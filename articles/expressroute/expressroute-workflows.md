---
title: "aaaWorkflows pour la configuration d’un circuit ExpressRoute | Documents Microsoft"
description: Cette page vous guide tout au long des flux de travail hello pour la configuration des homologations et circuit ExpressRoute
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="64fed-103">Workflows ExpressRoute d’approvisionnement du circuit et états du circuit</span><span class="sxs-lookup"><span data-stu-id="64fed-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="64fed-104">Cette page vous guide de mise en service hello et routage des flux de travail de configuration à un niveau élevé.</span><span class="sxs-lookup"><span data-stu-id="64fed-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="64fed-105">Hello figure ci-dessous et les étapes correspondantes affichent hello tâches que vous devez suivre dans l’ordre toohave un ExpressRoute circuit approvisionné de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="64fed-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="64fed-106">Utilisez PowerShell tooconfigure un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="64fed-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="64fed-107">Suivez les instructions de hello Bonjour [des circuits ExpressRoute de créer](expressroute-howto-circuit-classic.md) article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="64fed-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="64fed-108">Connectivité de la commande de fournisseur de services hello.</span><span class="sxs-lookup"><span data-stu-id="64fed-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="64fed-109">Ce processus varie.</span><span class="sxs-lookup"><span data-stu-id="64fed-109">This process varies.</span></span> <span data-ttu-id="64fed-110">Contactez votre fournisseur de connectivité pour plus d’informations sur la connectivité de tooorder.</span><span class="sxs-lookup"><span data-stu-id="64fed-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="64fed-111">Assurez-vous que le circuit de hello a été configuré correctement en vérifiant le circuit ExpressRoute de hello état via PowerShell de configuration.</span><span class="sxs-lookup"><span data-stu-id="64fed-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="64fed-112">Configurez les domaines de routage.</span><span class="sxs-lookup"><span data-stu-id="64fed-112">Configure routing domains.</span></span> <span data-ttu-id="64fed-113">Si votre fournisseur de connectivité gère la couche 3 pour vous, il configurera le routage pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="64fed-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="64fed-114">Si votre fournisseur de connectivité propose uniquement les services de couche 2, vous devez configurer le routage par indications décrites dans hello [exigences routage](expressroute-routing.md) et [configuration de routage](expressroute-howto-routing-classic.md) pages.</span><span class="sxs-lookup"><span data-stu-id="64fed-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="64fed-115">Activer l’homologation privée Azure, vous devez activer cette tooVMs tooconnect d’homologation / cloud services déployés dans les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="64fed-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="64fed-116">Activer l’homologation publique Azure - vous devez activer l’homologation publique Azure si vous souhaitez que les services de tooAzure tooconnect hébergés sur des adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="64fed-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="64fed-117">Il s’agit d’une exigence de tooaccess ressources Azure si vous avez choisi de routage de tooenable par défaut pour l’homologation privée Azure.</span><span class="sxs-lookup"><span data-stu-id="64fed-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="64fed-118">Activer Microsoft d’homologation - vous devez activer cette tooaccess Office 365 et Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="64fed-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="64fed-119">Vous devez vous assurer que vous utilisez un proxy distinct / bord tooconnect tooMicrosoft que celui que vous utilisez pour hello hello Internet.</span><span class="sxs-lookup"><span data-stu-id="64fed-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="64fed-120">À l’aide de hello même bord pour ExpressRoute et hello Internet entraîne le routage asymétrique et provoquer des pannes de connexion pour votre réseau.</span><span class="sxs-lookup"><span data-stu-id="64fed-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="64fed-121">Liaison virtuel réseaux tooExpressRoute circuits - vous pouvez lier le circuit ExpressRoute de tooyour réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="64fed-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="64fed-122">Suivez les instructions [toolink des réseaux virtuels](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span><span class="sxs-lookup"><span data-stu-id="64fed-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="64fed-123">Ces réseaux virtuels peuvent être hello même abonnement Azure que le circuit ExpressRoute de hello ou peut être dans un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="64fed-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="64fed-124">États d’approvisionnement du circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="64fed-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="64fed-125">Chaque circuit ExpressRoute comporte deux états :</span><span class="sxs-lookup"><span data-stu-id="64fed-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="64fed-126">État d’approvisionnement du fournisseur de service</span><span class="sxs-lookup"><span data-stu-id="64fed-126">Service provider provisioning state</span></span>
* <span data-ttu-id="64fed-127">État</span><span class="sxs-lookup"><span data-stu-id="64fed-127">Status</span></span>

<span data-ttu-id="64fed-128">L'état représente l’état d'approvisionnement de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="64fed-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="64fed-129">Cette propriété a la valeur tooEnabled lorsque vous créez un circuit Expressroute</span><span class="sxs-lookup"><span data-stu-id="64fed-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="64fed-130">état d’approvisionnement Hello connectivité fournisseur représente l’état hello côté du fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="64fed-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="64fed-131">Il peut afficher *NotProvisioned*, *Provisioning* ou *Provisioned*.</span><span class="sxs-lookup"><span data-stu-id="64fed-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="64fed-132">Hello circuit ExpressRoute doit être configuré pour vous toouse en mesure de toobe il.</span><span class="sxs-lookup"><span data-stu-id="64fed-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="64fed-133">États possibles d'un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="64fed-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="64fed-134">Cette section répertorie les états possibles de hello pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="64fed-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="64fed-135">**Lors de la création**</span><span class="sxs-lookup"><span data-stu-id="64fed-135">**At creation time**</span></span>

<span data-ttu-id="64fed-136">Vous verrez le circuit ExpressRoute de hello Bonjour suivant état dès que vous exécutez circuit ExpressRoute de hello PowerShell applet de commande toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="64fed-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="64fed-137">**Lorsque ce dernier est en cours de hello d’approvisionnement du circuit de hello**</span><span class="sxs-lookup"><span data-stu-id="64fed-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="64fed-138">Vous verrez circuit ExpressRoute de hello Bonjour suivant état dès que vous passer de fournisseur de connectivité hello service toohello clé et qu’ils ont démarré hello processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="64fed-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="64fed-139">**Lorsque ce dernier a effectué l’hello processus d’approvisionnement**</span><span class="sxs-lookup"><span data-stu-id="64fed-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="64fed-140">Vous verrez hello circuit ExpressRoute Bonjour suivant état dès que le fournisseur de connectivité hello terminée hello processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="64fed-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="64fed-141">Configuré et activé est hello uniquement état hello circuit peut être dans pour vous toouse en mesure de toobe il.</span><span class="sxs-lookup"><span data-stu-id="64fed-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="64fed-142">Si vous utilisez un fournisseur de couche 2, vous pouvez configurer le routage pour votre circuit uniquement lorsqu'il est dans cet état.</span><span class="sxs-lookup"><span data-stu-id="64fed-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="64fed-143">**Lorsque ce dernier est mise hors service de circuit de hello**</span><span class="sxs-lookup"><span data-stu-id="64fed-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="64fed-144">Si vous avez demandé de circuit ExpressRoute de hello service fournisseur toodeprovision hello, vous verrez le circuit de hello définie toohello suivant état une fois fournisseur de services hello terminée hello mise hors service du processus.</span><span class="sxs-lookup"><span data-stu-id="64fed-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="64fed-145">Vous pouvez choisir d’activer toore si nécessaire, ou exécuter des applets de commande PowerShell circuit de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="64fed-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="64fed-146">Si vous exécutez hello PowerShell applet de commande toodelete circuit hello en hello ServiceProviderProvisioningState opération de hello approvisionnement ou configuré échoue.</span><span class="sxs-lookup"><span data-stu-id="64fed-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="64fed-147">Collaborez avec votre circuit ExpressRoute de connectivité fournisseur toodeprovision hello tout d’abord, puis supprimez les circuit hello.</span><span class="sxs-lookup"><span data-stu-id="64fed-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="64fed-148">Microsoft continuera de circuit de hello toobill jusqu'à ce que vous exécutez hello circuit de hello toodelete PowerShell applet de commande.</span><span class="sxs-lookup"><span data-stu-id="64fed-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="64fed-149">État de configuration d’une session de routage</span><span class="sxs-lookup"><span data-stu-id="64fed-149">Routing session configuration state</span></span>
<span data-ttu-id="64fed-150">Hello état d’approvisionnement BGP permet de savoir si la session BGP de hello a été activée sur hello Microsoft edge.</span><span class="sxs-lookup"><span data-stu-id="64fed-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="64fed-151">Hello état doit être activé pour vous toobe toouse en mesure de hello homologation.</span><span class="sxs-lookup"><span data-stu-id="64fed-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="64fed-152">Il est important de toocheck hello BGP en particulier pour l’homologation de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="64fed-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="64fed-153">Dans Ajout toohello BGP état d’approvisionnement, il existe un autre état appelé *publié l’état de préfixes publics*.</span><span class="sxs-lookup"><span data-stu-id="64fed-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="64fed-154">Hello publiés préfixes publics l’état doit être dans *configuré* état, à la fois pour hello BGP session toobe haut et pour votre routage toowork de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="64fed-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="64fed-155">Si hello publié préfixe publique état a la valeur tooa *validation nécessitée* d’état, session BGP hello n’est pas activée, hello annoncé préfixes ne correspondait pas hello en tant que nombre dans un des registres de routage hello.</span><span class="sxs-lookup"><span data-stu-id="64fed-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="64fed-156">Si hello publié l’état de préfixes publics est en *validation manuelle* d’état, vous devez ouvrir un ticket de support avec [prise en charge Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) et prouver que vous possédez des adresses IP hello publié le long hello associé numéro de système autonome.</span><span class="sxs-lookup"><span data-stu-id="64fed-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="64fed-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64fed-157">Next steps</span></span>
* <span data-ttu-id="64fed-158">Configurez votre connexion ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="64fed-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="64fed-159">Création d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="64fed-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="64fed-160">Configuration du routage</span><span class="sxs-lookup"><span data-stu-id="64fed-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="64fed-161">Lier un circuit ExpressRoute de tooan réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="64fed-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

