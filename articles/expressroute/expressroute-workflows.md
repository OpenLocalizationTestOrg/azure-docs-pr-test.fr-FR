---
title: "Workflows de configuration d’un circuit ExpressRoute | Microsoft Docs"
description: Cette page vous guide tout au long des workflows pour la configuration du circuit ExpressRoute et des homologations
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
ms.openlocfilehash: cba1b2cfee379e7d2b079bcb3089981ef1044d66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="af02b-103">Workflows ExpressRoute d’approvisionnement du circuit et états du circuit</span><span class="sxs-lookup"><span data-stu-id="af02b-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="af02b-104">Cette page vous guide de façon sommaire tout au long des workflows d’approvisionnement du service et de configuration du routage.</span><span class="sxs-lookup"><span data-stu-id="af02b-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="af02b-105">L'illustration et les étapes correspondantes suivantes montrent les tâches que vous devez effectuer pour approvisionner un circuit ExpressRoute de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="af02b-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="af02b-106">Utilisez PowerShell pour configurer un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af02b-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="af02b-107">Suivez les instructions de l’article [Création de circuits ExpressRoute](expressroute-howto-circuit-classic.md) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="af02b-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="af02b-108">Commandez la connectivité auprès du fournisseur de services.</span><span class="sxs-lookup"><span data-stu-id="af02b-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="af02b-109">Ce processus varie.</span><span class="sxs-lookup"><span data-stu-id="af02b-109">This process varies.</span></span> <span data-ttu-id="af02b-110">Contactez votre fournisseur de connectivité pour plus d’informations sur la commande de connectivité.</span><span class="sxs-lookup"><span data-stu-id="af02b-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="af02b-111">Assurez-vous que le circuit a été correctement approvisionné en vérifiant l’état approvisionnement du circuit ExpressRoute via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af02b-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="af02b-112">Configurez les domaines de routage.</span><span class="sxs-lookup"><span data-stu-id="af02b-112">Configure routing domains.</span></span> <span data-ttu-id="af02b-113">Si votre fournisseur de connectivité gère la couche 3 pour vous, il configurera le routage pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="af02b-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="af02b-114">Si votre fournisseur de connectivité offre uniquement des services de couche 2, vous devez configurer le routage conformément aux instructions décrites dans les pages [Conditions requises pour le routage](expressroute-routing.md) et [Configuration du routage](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="af02b-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="af02b-115">Activer l'homologation privée Azure : vous devez activer cette homologation pour vous connecter aux machines virtuelles/services de cloud déployés au sein de réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="af02b-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="af02b-116">Activer l'homologation publique Azure : vous devez activer l'homologation publique Azure si vous souhaitez vous connecter à des services Azure hébergés sur des adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="af02b-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="af02b-117">Cette étape est nécessaire pour accéder aux ressources Azure si vous avez choisi d'activer le routage par défaut pour l'homologation privée Azure.</span><span class="sxs-lookup"><span data-stu-id="af02b-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="af02b-118">Activer l’homologation Microsoft : vous devez activer cette option pour accéder aux services Office 365 et Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="af02b-118">Enable Microsoft peering - You must enable this to access Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="af02b-119">Pour vous connecter à Microsoft, vous devez veiller à utiliser un proxy/appareil edge différent de celui que vous utilisez pour Internet.</span><span class="sxs-lookup"><span data-stu-id="af02b-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="af02b-120">L’utilisation du même appareil edge à la fois pour ExpressRoute et Internet entraîne un routage asymétrique et provoque des pertes de connectivité sur votre réseau.</span><span class="sxs-lookup"><span data-stu-id="af02b-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="af02b-121">Liaison de réseaux virtuels à des circuits ExpressRoute - vous pouvez lier des réseaux virtuels à votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af02b-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="af02b-122">Suivez les instructions [pour lier des réseaux virtuels](expressroute-howto-linkvnet-arm.md) à votre circuit.</span><span class="sxs-lookup"><span data-stu-id="af02b-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="af02b-123">Ces réseaux virtuels peuvent figurer dans le même abonnement Azure que le circuit ExpressRoute, ou dans un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="af02b-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="af02b-124">États d’approvisionnement du circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="af02b-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="af02b-125">Chaque circuit ExpressRoute comporte deux états :</span><span class="sxs-lookup"><span data-stu-id="af02b-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="af02b-126">État d’approvisionnement du fournisseur de service</span><span class="sxs-lookup"><span data-stu-id="af02b-126">Service provider provisioning state</span></span>
* <span data-ttu-id="af02b-127">État</span><span class="sxs-lookup"><span data-stu-id="af02b-127">Status</span></span>

<span data-ttu-id="af02b-128">L'état représente l’état d'approvisionnement de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="af02b-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="af02b-129">Cette propriété est définie sur Activée lorsque vous créez un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="af02b-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="af02b-130">L'état d’approvisionnement du fournisseur de connectivité représente l'état du côté du fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="af02b-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="af02b-131">Il peut afficher *NotProvisioned*, *Provisioning* ou *Provisioned*.</span><span class="sxs-lookup"><span data-stu-id="af02b-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="af02b-132">Le circuit ExpressRoute doit être dans l'état Provisioned pour pouvoir être utilisé.</span><span class="sxs-lookup"><span data-stu-id="af02b-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="af02b-133">États possibles d'un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="af02b-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="af02b-134">Cette section répertorie les états possibles d’un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af02b-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="af02b-135">**Lors de la création**</span><span class="sxs-lookup"><span data-stu-id="af02b-135">**At creation time**</span></span>

<span data-ttu-id="af02b-136">Le circuit ExpressRoute affiche l'état suivant dès que vous exécutez l'applet de commande PowerShell pour créer le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af02b-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="af02b-137">**Quand le fournisseur de connectivité est en cours d’approvisionnement du circuit**</span><span class="sxs-lookup"><span data-stu-id="af02b-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="af02b-138">Le circuit ExpressRoute affiche l'état suivant dès que vous passez la clé de service au fournisseur de connectivité et qu’il démarre le processus d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="af02b-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="af02b-139">**Quand fournisseur de connectivité a terminé le processus d’approvisionnement**</span><span class="sxs-lookup"><span data-stu-id="af02b-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="af02b-140">Le circuit ExpressRoute affiche l'état suivant dès que le fournisseur de connectivité a terminé le processus d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="af02b-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="af02b-141">Provisioned et Enabled sont les seuls états dans lesquels le circuit peut se trouver pour pouvoir être utilisé.</span><span class="sxs-lookup"><span data-stu-id="af02b-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="af02b-142">Si vous utilisez un fournisseur de couche 2, vous pouvez configurer le routage pour votre circuit uniquement lorsqu'il est dans cet état.</span><span class="sxs-lookup"><span data-stu-id="af02b-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="af02b-143">**Quand le fournisseur de connectivité est en train d’annuler l’approvisionnement du circuit**</span><span class="sxs-lookup"><span data-stu-id="af02b-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="af02b-144">Si vous avez demandé au fournisseur de services d’annuler l’approvisionnement du circuit ExpressRoute, le circuit affichera l’état suivant une fois que le fournisseur de services aura terminé le processus d’annulation de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="af02b-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="af02b-145">Vous pouvez choisir de le réactiver si nécessaire, ou exécuter des applets de commande PowerShell pour supprimer le circuit.</span><span class="sxs-lookup"><span data-stu-id="af02b-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="af02b-146">Si vous exécutez l’applet de commande PowerShell pour supprimer le circuit alors que ServiceProviderProvisioningState a la valeur En cours d’approvisionnement ou Approvisionné, l’opération échoue.</span><span class="sxs-lookup"><span data-stu-id="af02b-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="af02b-147">Veuillez au préalable contacter votre fournisseur de connectivité pour annuler l’approvisionnement du circuit ExpressRoute, puis supprimer le circuit.</span><span class="sxs-lookup"><span data-stu-id="af02b-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="af02b-148">Microsoft continuera à facturer le circuit jusqu’à ce que vous exécutiez l’applet de commande PowerShell pour supprimer le circuit.</span><span class="sxs-lookup"><span data-stu-id="af02b-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="af02b-149">État de configuration d’une session de routage</span><span class="sxs-lookup"><span data-stu-id="af02b-149">Routing session configuration state</span></span>
<span data-ttu-id="af02b-150">Le protocole d’approvisionnement BGP vous indique si la session BGP a été activée sur le matériel edge Microsoft.</span><span class="sxs-lookup"><span data-stu-id="af02b-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="af02b-151">L'état doit être activé pour que vous puissiez utiliser l'homologation.</span><span class="sxs-lookup"><span data-stu-id="af02b-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="af02b-152">Il est important de vérifier l'état de la session BGP, en particulier pour l'homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="af02b-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="af02b-153">En plus de l'état d’approvisionnement BGP, il existe un autre état appelé *état des préfixes publics publiés*.</span><span class="sxs-lookup"><span data-stu-id="af02b-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="af02b-154">Les préfixes publics publiés doivent afficher l’état *configured* , à la fois pour que la session BGP soit opérationnelle et pour que votre routage fonctionne de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="af02b-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="af02b-155">Si l'état du préfixe public publié indique qu’une *validation est nécessaire* , la session BGP n'est pas activée car les préfixes publiés ne correspondent pas au numéro AS dans un des registres de routage.</span><span class="sxs-lookup"><span data-stu-id="af02b-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="af02b-156">Si l'état des préfixes publics publiés indique une *validation manuelle* , vous devez ouvrir un ticket de support auprès du [support Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) et fournir la preuve que vous possédez les adresses IP publiés ainsi que le numéro système autonome associé.</span><span class="sxs-lookup"><span data-stu-id="af02b-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="af02b-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af02b-157">Next steps</span></span>
* <span data-ttu-id="af02b-158">Configurez votre connexion ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="af02b-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="af02b-159">Création d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="af02b-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="af02b-160">Configuration du routage</span><span class="sxs-lookup"><span data-stu-id="af02b-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="af02b-161">Liaison d’un réseau virtuel à un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="af02b-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

