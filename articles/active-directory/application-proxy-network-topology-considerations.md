---
title: "Considérations sur la topologie aaaNetwork lors de l’utilisation du Proxy d’Application Azure Active Directory | Documents Microsoft"
description: "Couvre les considérations sur la topologie du réseau lors de l’utilisation du proxy d’application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a><span data-ttu-id="da8b4-103">Considérations sur la topologie du réseau lors de l’utilisation du proxy d’application Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da8b4-103">Network topology considerations when using Azure Active Directory Application Proxy</span></span>

<span data-ttu-id="da8b4-104">Cet article explique les considérations de topologie réseau lors de l’utilisation de l’application de proxy d’application Azure Active Directory (Azure AD) pour la publication et l’accès à distance de vos applications.</span><span class="sxs-lookup"><span data-stu-id="da8b4-104">This article explains network topology considerations when using Azure Active Directory (Azure AD) Application Proxy for publishing and accessing your applications remotely.</span></span>

## <a name="traffic-flow"></a><span data-ttu-id="da8b4-105">Flux de trafic</span><span class="sxs-lookup"><span data-stu-id="da8b4-105">Traffic flow</span></span>

<span data-ttu-id="da8b4-106">Lorsqu’une application est publiée via le Proxy d’Application Azure AD, le trafic à partir d’applications de toohello utilisateurs hello passe par trois connexions :</span><span class="sxs-lookup"><span data-stu-id="da8b4-106">When an application is published through Azure AD Application Proxy, traffic from hello users toohello applications flows through three connections:</span></span>

1. <span data-ttu-id="da8b4-107">Hello se connecte toohello Proxy d’Application Azure AD service point de terminaison public sur Azure</span><span class="sxs-lookup"><span data-stu-id="da8b4-107">hello user connects toohello Azure AD Application Proxy service public endpoint on Azure</span></span>
2. <span data-ttu-id="da8b4-108">Hello service Proxy d’Application connecte le connecteur de Proxy d’Application toohello</span><span class="sxs-lookup"><span data-stu-id="da8b4-108">hello Application Proxy service connects toohello Application Proxy connector</span></span>
3. <span data-ttu-id="da8b4-109">connecteur de Proxy d’Application Hello connecte l’application cible de toohello</span><span class="sxs-lookup"><span data-stu-id="da8b4-109">hello Application Proxy connector connects toohello target application</span></span>

![Diagramme montrant le flux de trafic à partir de l’application utilisateur tootarget](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a><span data-ttu-id="da8b4-111">Emplacement du locataire et service de proxy d’application</span><span class="sxs-lookup"><span data-stu-id="da8b4-111">Tenant location and Application Proxy service</span></span>

<span data-ttu-id="da8b4-112">Lorsque vous vous inscrivez pour un locataire Azure AD, région de hello de votre client est déterminée par pays hello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="da8b4-112">When you sign up for an Azure AD tenant, hello region of your tenant is determined by hello country you specify.</span></span> <span data-ttu-id="da8b4-113">Lorsque vous activez le Proxy d’Application, les instances de service de Proxy d’Application hello pour votre client sont choisis ou créées Bonjour même région que votre client Azure AD ou tooit de région hello le plus proche.</span><span class="sxs-lookup"><span data-stu-id="da8b4-113">When you enable Application Proxy, hello Application Proxy service instances for your tenant are chosen or created in hello same region as your Azure AD tenant, or hello closest region tooit.</span></span>

<span data-ttu-id="da8b4-114">Par exemple, si la région de votre locataire Azure AD est hello Union européenne (UE), tous les connecteurs de Proxy d’Application utilisent des instances de service dans des centres de données Azure Bonjour Europe.</span><span class="sxs-lookup"><span data-stu-id="da8b4-114">For example, if your Azure AD tenant’s region is hello European Union (EU), all your Application Proxy connectors use service instances in Azure datacenters in hello EU.</span></span> <span data-ttu-id="da8b4-115">Lorsque vos utilisateurs un accès des applications publiées, leur trafic passe par les instances de service de Proxy d’Application hello dans cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="da8b4-115">When your users access published applications, their traffic goes through hello Application Proxy service instances in this location.</span></span>

## <a name="considerations-for-reducing-latency"></a><span data-ttu-id="da8b4-116">Considérations relatives à la réduction de la latence</span><span class="sxs-lookup"><span data-stu-id="da8b4-116">Considerations for reducing latency</span></span>

<span data-ttu-id="da8b4-117">Toutes les solutions de proxy ajoutent de la latence à votre connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="da8b4-117">All proxy solutions introduce latency into your network connection.</span></span> <span data-ttu-id="da8b4-118">Quel que soit le proxy ou une solution VPN que vous choisissez en tant que votre solution d’accès à distance, il inclut toujours un ensemble de serveurs, l’activation de hello connexion tooinside votre réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="da8b4-118">No matter which proxy or VPN solution you choose as your remote access solution, it always includes a set of servers enabling hello connection tooinside your corporate network.</span></span>

<span data-ttu-id="da8b4-119">Les organisations comptent généralement des points de terminaison de serveur dans leur réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="da8b4-119">Organizations typically include server endpoints in their perimeter network.</span></span> <span data-ttu-id="da8b4-120">Proxy d’Application Azure AD, toutefois, le trafic acheminé via le service de proxy hello dans le cloud de hello tandis que les connecteurs hello résident sur votre réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="da8b4-120">With Azure AD Application Proxy, however, traffic flows through hello proxy service in hello cloud while hello connectors reside on your corporate network.</span></span> <span data-ttu-id="da8b4-121">Aucun réseau de périmètre n’est requis.</span><span class="sxs-lookup"><span data-stu-id="da8b4-121">No perimeter network is required.</span></span>

<span data-ttu-id="da8b4-122">les sections suivantes Hello contient toohelp d’autres suggestions vous réduisez encore davantage la latence.</span><span class="sxs-lookup"><span data-stu-id="da8b4-122">hello next sections contain additional suggestions toohelp you reduce latency even further.</span></span> 

### <a name="connector-placement"></a><span data-ttu-id="da8b4-123">Placement d’un connecteur</span><span class="sxs-lookup"><span data-stu-id="da8b4-123">Connector placement</span></span>

<span data-ttu-id="da8b4-124">Le Proxy d’application choisit emplacement hello d’instances pour vous, en fonction de votre emplacement du client.</span><span class="sxs-lookup"><span data-stu-id="da8b4-124">Application Proxy chooses hello location of instances for you, based on your tenant location.</span></span> <span data-ttu-id="da8b4-125">Toutefois, vous obtenez toodecide où le connecteur de hello tooinstall, ce qui vous donne hello caractéristiques de latence d’alimentation toodefine hello de votre trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="da8b4-125">However, you get toodecide where tooinstall hello connector, giving you hello power toodefine hello latency characteristics of your network traffic.</span></span>

<span data-ttu-id="da8b4-126">Lorsque vous configurez hello service Proxy d’Application, demander hello suivant questions :</span><span class="sxs-lookup"><span data-stu-id="da8b4-126">When setting up hello Application Proxy service, ask hello following questions:</span></span>

* <span data-ttu-id="da8b4-127">Application hello emplacement ?</span><span class="sxs-lookup"><span data-stu-id="da8b4-127">Where is hello app located?</span></span>
* <span data-ttu-id="da8b4-128">Où se trouvent la plupart des utilisateurs qui ont accès à application hello située ?</span><span class="sxs-lookup"><span data-stu-id="da8b4-128">Where are most users who access hello app located?</span></span>
* <span data-ttu-id="da8b4-129">Instance de Proxy d’Application hello emplacement ?</span><span class="sxs-lookup"><span data-stu-id="da8b4-129">Where is hello Application Proxy instance located?</span></span>
* <span data-ttu-id="da8b4-130">Vous disposez déjà d’un réseau dédié connexion tooAzure des centres de données configuré, comme Azure ExpressRoute ou d’un réseau privé virtuel similaire ?</span><span class="sxs-lookup"><span data-stu-id="da8b4-130">Do you already have a dedicated network connection tooAzure datacenters set up, like Azure ExpressRoute or a similar VPN?</span></span>

<span data-ttu-id="da8b4-131">connecteur de Hello a toocommunicate avec Azure et vos applications (étapes 2 et 3 dans le diagramme de flux de trafic hello), donc hello la sélection élective de la latence de hello hello connecteur affecte ces deux connexions.</span><span class="sxs-lookup"><span data-stu-id="da8b4-131">hello connector has toocommunicate with both Azure and your applications (steps 2 and 3 in hello Traffic flow diagram), so hello placement of hello connector affects hello latency of those two connections.</span></span> <span data-ttu-id="da8b4-132">Lorsque vous évaluez la sélection élective hello du connecteur de hello, gardez Bonjour l’esprit les points suivants :</span><span class="sxs-lookup"><span data-stu-id="da8b4-132">When evaluating hello placement of hello connector, keep in mind hello following points:</span></span>

* <span data-ttu-id="da8b4-133">Si vous souhaitez toouse la délégation Kerberos contrainte (KCD) pour l’authentification unique, puis connecteur de hello a besoin d’un centre de données de tooa de ligne de vue.</span><span class="sxs-lookup"><span data-stu-id="da8b4-133">If you want toouse Kerberos constrained delegation (KCD) for single sign-on, then hello connector needs a line of sight tooa datacenter.</span></span> <span data-ttu-id="da8b4-134">En outre, le serveur de connecteur hello doit toobe joint au domaine.</span><span class="sxs-lookup"><span data-stu-id="da8b4-134">Additionally, hello connector server needs toobe domain joined.</span></span>  
* <span data-ttu-id="da8b4-135">En cas de doute, installez application toohello proche de hello connecteur.</span><span class="sxs-lookup"><span data-stu-id="da8b4-135">When in doubt, install hello connector closer toohello application.</span></span>

### <a name="general-approach-toominimize-latency"></a><span data-ttu-id="da8b4-136">Latence de toominimize approche générale</span><span class="sxs-lookup"><span data-stu-id="da8b4-136">General approach toominimize latency</span></span>

<span data-ttu-id="da8b4-137">Vous pouvez réduire la latence de hello du trafic de bout en bout hello en optimisant chaque connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="da8b4-137">You can minimize hello latency of hello end-to-end traffic by optimizing each network connection.</span></span> <span data-ttu-id="da8b4-138">Chaque connexion peut être optimisée en :</span><span class="sxs-lookup"><span data-stu-id="da8b4-138">Each connection can be optimized by:</span></span>

* <span data-ttu-id="da8b4-139">Réduire la distance entre deux extrémités de hello du saut de hello hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-139">Reducing hello distance between hello two ends of hello hop.</span></span>
* <span data-ttu-id="da8b4-140">En choisissant l’option tootraverse de réseau adéquat hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-140">Choosing hello right network tootraverse.</span></span> <span data-ttu-id="da8b4-141">Par exemple, parcourir un réseau privé et non hello Internet public peut être plus rapide, en raison des liens de toodedicated.</span><span class="sxs-lookup"><span data-stu-id="da8b4-141">For example, traversing a private network rather than hello public Internet may be faster, due toodedicated links.</span></span>

<span data-ttu-id="da8b4-142">Si vous disposez d’une liaison VPN ou ExpressRoute dédiée entre Azure et votre réseau d’entreprise, vous souhaiterez peut-être toouse qui.</span><span class="sxs-lookup"><span data-stu-id="da8b4-142">If you have a dedicated VPN or ExpressRoute link between Azure and your corporate network, you may want toouse that.</span></span>

## <a name="focus-your-optimization-strategy"></a><span data-ttu-id="da8b4-143">Concentrer votre stratégie d’optimisation</span><span class="sxs-lookup"><span data-stu-id="da8b4-143">Focus your optimization strategy</span></span>

<span data-ttu-id="da8b4-144">Il est peu que vous pouvez effectuer la connexion de hello toocontrol entre vos utilisateurs et le service Proxy d’Application de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-144">There's little that you can do toocontrol hello connection between your users and hello Application Proxy service.</span></span> <span data-ttu-id="da8b4-145">Les utilisateurs peuvent accéder à vos applications à partir d’un réseau domestique, d’un café ou d’un autre pays.</span><span class="sxs-lookup"><span data-stu-id="da8b4-145">Users may access your apps from a home network, a coffee shop, or a different country.</span></span> <span data-ttu-id="da8b4-146">Au lieu de cela, vous pouvez optimiser les connexions à partir des connecteurs toohello applications du Proxy d’Application toohello hello Proxy d’Application service hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-146">Instead, you can optimize hello connections from hello Application Proxy service toohello Application Proxy connectors toohello apps.</span></span> <span data-ttu-id="da8b4-147">Incorporez hello suivant des modèles dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="da8b4-147">Consider incorporating hello following patterns in your environment.</span></span>

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a><span data-ttu-id="da8b4-148">Modèle 1 : Put hello connecteur toohello fermer application</span><span class="sxs-lookup"><span data-stu-id="da8b4-148">Pattern 1: Put hello connector close toohello application</span></span>

<span data-ttu-id="da8b4-149">Application cible place hello connecteur toohello Fermer dans le réseau de client hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-149">Place hello connector close toohello target application in hello customer network.</span></span> <span data-ttu-id="da8b4-150">Cette configuration réduit l’étape 3 dans le diagramme de topographie hello, étant donné que l’application et le connecteur de hello sont proches.</span><span class="sxs-lookup"><span data-stu-id="da8b4-150">This configuration minimizes step 3 in hello topography diagram, because hello connector and application are close.</span></span> 

<span data-ttu-id="da8b4-151">Si votre connecteur a besoin d’un contrôleur de domaine de ligne de vue toohello, ce modèle est avantageux.</span><span class="sxs-lookup"><span data-stu-id="da8b4-151">If your connector needs a line of sight toohello domain controller, then this pattern is advantageous.</span></span> <span data-ttu-id="da8b4-152">La plupart de nos clients utilisent ce modèle, car il fonctionne bien pour la majorité des scénarios.</span><span class="sxs-lookup"><span data-stu-id="da8b4-152">Most of our customers use this pattern, because it works well for most scenarios.</span></span> <span data-ttu-id="da8b4-153">Ce modèle peut aussi être combiné avec le trafic de 2 toooptimize modèle entre le service de hello et de connecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-153">This pattern can also be combined with pattern 2 toooptimize traffic between hello service and hello connector.</span></span>

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a><span data-ttu-id="da8b4-154">Modèle 2 : Tirer parti d’ExpressRoute avec l’homologation publique</span><span class="sxs-lookup"><span data-stu-id="da8b4-154">Pattern 2: Take advantage of ExpressRoute with public peering</span></span>

<span data-ttu-id="da8b4-155">Si vous avez configuré avec l’homologation publique de ExpressRoute, vous pouvez utiliser la connexion ExpressRoute plus rapide de hello pour le trafic entre le Proxy d’Application et le connecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-155">If you have ExpressRoute set up with public peering, you can use hello faster ExpressRoute connection for traffic between Application Proxy and hello connector.</span></span> <span data-ttu-id="da8b4-156">connecteur de Hello est toujours sur votre réseau, fermer toohello application.</span><span class="sxs-lookup"><span data-stu-id="da8b4-156">hello connector is still on your network, close toohello app.</span></span>

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a><span data-ttu-id="da8b4-157">Modèle 3 : Tirer parti d’ExpressRoute avec l’homologation privée</span><span class="sxs-lookup"><span data-stu-id="da8b4-157">Pattern 3: Take advantage of ExpressRoute with private peering</span></span>

<span data-ttu-id="da8b4-158">Si vous avez une installation VPN ou ExpressRoute dédiée avec l’homologation privée entre Azure et votre réseau d’entreprise, vous avez une autre option.</span><span class="sxs-lookup"><span data-stu-id="da8b4-158">If you have a dedicated VPN or ExpressRoute set up with private peering between Azure and your corporate network, you have another option.</span></span> <span data-ttu-id="da8b4-159">Dans cette configuration, réseau virtuel de hello dans Azure est généralement considéré comme une extension du réseau d’entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-159">In this configuration, hello virtual network in Azure is typically considered as an extension of hello corporate network.</span></span> <span data-ttu-id="da8b4-160">Par conséquent, vous pouvez installer le connecteur de hello Bonjour centre de données Azure et toujours satisfaire aux exigences de faible latence de hello de connexion du connecteur pour application hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-160">So you can install hello connector in hello Azure datacenter, and still satisfy hello low latency requirements of hello connector-to-app connection.</span></span>

<span data-ttu-id="da8b4-161">La latence n’est pas compromise, car le trafic circule sur une connexion dédiée.</span><span class="sxs-lookup"><span data-stu-id="da8b4-161">Latency is not compromised because traffic is flowing over a dedicated connection.</span></span> <span data-ttu-id="da8b4-162">Vous obtenez également améliorer la latence de connecteur de service Proxy d’Application, car le connecteur de hello est installé dans un emplacement du client Azure AD du centre de données Azure fermer tooyour.</span><span class="sxs-lookup"><span data-stu-id="da8b4-162">You also get improved Application Proxy service-to-connector latency because hello connector is installed in an Azure datacenter close tooyour Azure AD tenant location.</span></span>

![Diagramme illustrant un connecteur installé dans un centre de données Azure](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a><span data-ttu-id="da8b4-164">Autres approches</span><span class="sxs-lookup"><span data-stu-id="da8b4-164">Other approaches</span></span>

<span data-ttu-id="da8b4-165">Bien que le focus hello de cet article est l’emplacement d’un connecteur, vous pouvez également modifier la sélection élective hello de hello application tooget meilleure latence.</span><span class="sxs-lookup"><span data-stu-id="da8b4-165">Although hello focus of this article is connector placement, you can also change hello placement of hello application tooget better latency characteristics.</span></span>

<span data-ttu-id="da8b4-166">De plus en plus d’organisations déplacent leurs réseaux dans des environnements hébergés.</span><span class="sxs-lookup"><span data-stu-id="da8b4-166">Increasingly, organizations are moving their networks into hosted environments.</span></span> <span data-ttu-id="da8b4-167">Cela leur permet de tooplace leurs applications dans un environnement hébergé qui fait également partie de leur réseau d’entreprise et être toujours dans le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-167">This enables them tooplace their apps in a hosted environment that is also part of their corporate network, and still be within hello domain.</span></span> <span data-ttu-id="da8b4-168">Dans ce cas, les modèles de hello décrits dans les sections précédentes de hello peuvent être appliqué toohello nouvel emplacement d’application.</span><span class="sxs-lookup"><span data-stu-id="da8b4-168">In this case, hello patterns discussed in hello preceding sections can be applied toohello new application location.</span></span> <span data-ttu-id="da8b4-169">Si vous envisagez cette option, consultez la page [Services de domaine Azure AD](../active-directory-domain-services/active-directory-ds-overview.md).</span><span class="sxs-lookup"><span data-stu-id="da8b4-169">If you're considering this option, see [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md).</span></span>

<span data-ttu-id="da8b4-170">En outre, envisagez d’organiser vos connecteurs à l’aide de [groupes de connecteurs](active-directory-application-proxy-connectors.md) tootarget les applications qui se trouvent dans différents emplacements et des réseaux.</span><span class="sxs-lookup"><span data-stu-id="da8b4-170">Additionally, consider organizing your connectors using [connector groups](active-directory-application-proxy-connectors.md) tootarget apps that are in different locations and networks.</span></span> 

## <a name="common-use-cases"></a><span data-ttu-id="da8b4-171">Cas d’utilisation courants</span><span class="sxs-lookup"><span data-stu-id="da8b4-171">Common use cases</span></span>

<span data-ttu-id="da8b4-172">Dans cette section, nous allons étudier quelques scénarios courants.</span><span class="sxs-lookup"><span data-stu-id="da8b4-172">In this section, we walk through a few common scenarios.</span></span> <span data-ttu-id="da8b4-173">Supposons que hello locataire Azure AD (et par conséquent un point de terminaison de service proxy) se trouve dans hello États-Unis (US).</span><span class="sxs-lookup"><span data-stu-id="da8b4-173">Assume that hello Azure AD tenant (and therefore proxy service endpoint) is located in hello United States (US).</span></span> <span data-ttu-id="da8b4-174">Hello les observations présentées dans ces cas d’utilisation s’appliquent également des régions tooother monde hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-174">hello considerations discussed in these use cases also apply tooother regions around hello globe.</span></span>

<span data-ttu-id="da8b4-175">Dans ces scénarios, nous appelons chaque connexion un « tronçon » et nous les numérotons dans un souci de simplification :</span><span class="sxs-lookup"><span data-stu-id="da8b4-175">For these scenarios, we call each connection a "hop" and number them for easier discussion:</span></span>

- <span data-ttu-id="da8b4-176">**Sauts 1**: utilisateur toohello service Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="da8b4-176">**Hop 1**: User toohello Application Proxy service</span></span>
- <span data-ttu-id="da8b4-177">**Sauts 2**: connecteur de Proxy d’Application de Proxy d’Application service toohello</span><span class="sxs-lookup"><span data-stu-id="da8b4-177">**Hop 2**: Application Proxy service toohello Application Proxy connector</span></span>
- <span data-ttu-id="da8b4-178">**Sauts 3**: application de Proxy d’Application connecteur toohello cible</span><span class="sxs-lookup"><span data-stu-id="da8b4-178">**Hop 3**: Application Proxy connector toohello target application</span></span> 

### <a name="use-case-1"></a><span data-ttu-id="da8b4-179">Cas d’utilisation 1</span><span class="sxs-lookup"><span data-stu-id="da8b4-179">Use case 1</span></span>

<span data-ttu-id="da8b4-180">**Scénario :** application hello est dans un réseau d’entreprise Bonjour US, avec des utilisateurs dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="da8b4-180">**Scenario:** hello app is in an organization's network in hello US, with users in hello same region.</span></span> <span data-ttu-id="da8b4-181">Aucun ExpressRoute ou un VPN n’existe entre hello centre de données Azure et de réseau d’entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-181">No ExpressRoute or VPN exists between hello Azure datacenter and hello corporate network.</span></span>

<span data-ttu-id="da8b4-182">**Recommandation :** modèle de suivi 1, expliqué dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-182">**Recommendation:** Follow pattern 1, explained in hello previous section.</span></span> <span data-ttu-id="da8b4-183">Pour une latence améliorée, envisagez l’utilisation d’ExpressRoute, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="da8b4-183">For improved latency, consider using ExpressRoute, if needed.</span></span>

<span data-ttu-id="da8b4-184">Il s’agit d’un modèle simple.</span><span class="sxs-lookup"><span data-stu-id="da8b4-184">This is a simple pattern.</span></span> <span data-ttu-id="da8b4-185">Pour optimiser les sauts 3 en plaçant le connecteur hello côté application hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-185">You optimize hop 3 by placing hello connector near hello app.</span></span> <span data-ttu-id="da8b4-186">C’est également un choix naturel, car le connecteur de hello est généralement installé avec ligne de vue toohello application et toohello centre de données tooperform KCD operations.</span><span class="sxs-lookup"><span data-stu-id="da8b4-186">This is also a natural choice, because hello connector typically is installed with line of sight toohello app and toohello datacenter tooperform KCD operations.</span></span>

![Diagramme montrant que les utilisateurs, proxy, connecteur et application figurent tous dans hello nous](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a><span data-ttu-id="da8b4-188">Cas d’utilisation 2</span><span class="sxs-lookup"><span data-stu-id="da8b4-188">Use case 2</span></span>

<span data-ttu-id="da8b4-189">**Scénario :** application hello est dans un réseau d’entreprise Bonjour US, avec des utilisateurs répartis de manière globale.</span><span class="sxs-lookup"><span data-stu-id="da8b4-189">**Scenario:** hello app is in an organization's network in hello US, with users spread out globally.</span></span> <span data-ttu-id="da8b4-190">Aucun ExpressRoute ou un VPN n’existe entre hello centre de données Azure et de réseau d’entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-190">No ExpressRoute or VPN exists between hello Azure datacenter and hello corporate network.</span></span>

<span data-ttu-id="da8b4-191">**Recommandation :** modèle de suivi 1, expliqué dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-191">**Recommendation:** Follow pattern 1, explained in hello previous section.</span></span> 

<span data-ttu-id="da8b4-192">Là encore, hello est courant toooptimize saut 3, où vous placez le connecteur hello côté application hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-192">Again, hello common pattern is toooptimize hop 3, where you place hello connector near hello app.</span></span> <span data-ttu-id="da8b4-193">Saut 3 n’est pas généralement coûteuse, s’il s’agit dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="da8b4-193">Hop 3 is not typically expensive, if it is all within hello same region.</span></span> <span data-ttu-id="da8b4-194">Toutefois, tronçon 1 peut être plus coûteux selon l’emplacement utilisateur de hello, étant donné que les utilisateurs au sein de Bonjour doivent accéder à l’instance de Proxy d’Application hello Bonjour des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="da8b4-194">However, hop 1 can be more expensive depending on where hello user is, because users across hello world must access hello Application Proxy instance in hello US.</span></span> <span data-ttu-id="da8b4-195">Il est important de noter que toutes les solutions de proxy ont des caractéristiques similaires en ce qui concerne les utilisateurs répartis globalement.</span><span class="sxs-lookup"><span data-stu-id="da8b4-195">It's worth noting that any proxy solution has similar characteristics regarding users being spread out globally.</span></span>

![Diagramme montrant que les utilisateurs sont réparties globalement, mais application connecteur et proxy de hello dans hello des États-Unis](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a><span data-ttu-id="da8b4-197">Cas d’utilisation 3</span><span class="sxs-lookup"><span data-stu-id="da8b4-197">Use case 3</span></span>

<span data-ttu-id="da8b4-198">**Scénario :** application hello est dans un réseau d’entreprise Bonjour US.</span><span class="sxs-lookup"><span data-stu-id="da8b4-198">**Scenario:** hello app is in an organization's network in hello US.</span></span> <span data-ttu-id="da8b4-199">ExpressRoute avec l’homologation publique existe entre Azure et hello réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="da8b4-199">ExpressRoute with public peering exists between Azure and hello corporate network.</span></span>

<span data-ttu-id="da8b4-200">**Recommandation :** suivent des modèles 1 et 2, expliqué dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-200">**Recommendation:** Follow patterns 1 and 2, explained in hello previous section.</span></span>

<span data-ttu-id="da8b4-201">Placez d’abord, connecteur hello aussi proche que possible toohello application.</span><span class="sxs-lookup"><span data-stu-id="da8b4-201">First, place hello connector as close as possible toohello app.</span></span> <span data-ttu-id="da8b4-202">Ensuite, système de hello utilise automatiquement ExpressRoute tronçon 2.</span><span class="sxs-lookup"><span data-stu-id="da8b4-202">Then, hello system automatically uses ExpressRoute for hop 2.</span></span> 

<span data-ttu-id="da8b4-203">Si le lien de connexion ExpressRoute hello est à l’aide de l’homologation publique, hello passe le trafic entre le proxy de hello et le connecteur de hello sur ce lien.</span><span class="sxs-lookup"><span data-stu-id="da8b4-203">If hello ExpressRoute link is using public peering, hello traffic between hello proxy and hello connector flows over that link.</span></span> <span data-ttu-id="da8b4-204">Le tronçon 2 a une latence optimisée.</span><span class="sxs-lookup"><span data-stu-id="da8b4-204">Hop 2 has optimized latency.</span></span>

![Diagramme montrant ExpressRoute entre le connecteur et le proxy de hello](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a><span data-ttu-id="da8b4-206">Cas d’utilisation 4</span><span class="sxs-lookup"><span data-stu-id="da8b4-206">Use case 4</span></span>

<span data-ttu-id="da8b4-207">**Scénario :** application hello est dans un réseau d’entreprise Bonjour US.</span><span class="sxs-lookup"><span data-stu-id="da8b4-207">**Scenario:** hello app is in an organization's network in hello US.</span></span> <span data-ttu-id="da8b4-208">ExpressRoute avec l’homologation privée existe entre Azure et hello réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="da8b4-208">ExpressRoute with private peering exists between Azure and hello corporate network.</span></span>

<span data-ttu-id="da8b4-209">**Recommandation :** modèle de suivi 3, expliqué dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-209">**Recommendation:** Follow pattern 3, explained in hello previous section.</span></span>

<span data-ttu-id="da8b4-210">Placez le connecteur de hello Bonjour centre de données Azure qui est connecté toohello le réseau d’entreprise via l’homologation privée ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="da8b4-210">Place hello connector in hello Azure datacenter that is connected toohello corporate network through ExpressRoute private peering.</span></span> 

<span data-ttu-id="da8b4-211">connecteur de Hello peut être placée dans hello centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="da8b4-211">hello connector can be placed in hello Azure datacenter.</span></span> <span data-ttu-id="da8b4-212">Étant donné que le connecteur de hello a toujours une ligne de vue toohello application et le centre de données de hello via le réseau privé de hello, saut 3 reste optimisé.</span><span class="sxs-lookup"><span data-stu-id="da8b4-212">Since hello connector still has a line of sight toohello application and hello datacenter through hello private network, hop 3 remains optimized.</span></span> <span data-ttu-id="da8b4-213">En outre, le tronçon 2 est davantage optimisé.</span><span class="sxs-lookup"><span data-stu-id="da8b4-213">In addition, hop 2 is optimized further.</span></span>

![Diagramme montrant le connecteur de hello dans un centre de données Azure et ExpressRoute entre l’application et le connecteur de hello](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a><span data-ttu-id="da8b4-215">Cas d’utilisation 5</span><span class="sxs-lookup"><span data-stu-id="da8b4-215">Use case 5</span></span>

<span data-ttu-id="da8b4-216">**Scénario :** application hello est dans un réseau d’entreprise Bonjour Europe, avec une instance de Proxy d’Application de hello et la plupart des utilisateurs Bonjour US.</span><span class="sxs-lookup"><span data-stu-id="da8b4-216">**Scenario:** hello app is in an organization's network in hello EU, with hello Application Proxy instance and most users in hello US.</span></span>

<span data-ttu-id="da8b4-217">**Recommandation :** connecteur de hello sur Place vers une application hello.</span><span class="sxs-lookup"><span data-stu-id="da8b4-217">**Recommendation:** Place hello connector near hello app.</span></span> <span data-ttu-id="da8b4-218">Étant donné que les États-Unis utilisateurs accèdent à une instance de Proxy d’Application qui se produit toobe Bonjour même région, tronçon 1 n’est pas trop onéreuse.</span><span class="sxs-lookup"><span data-stu-id="da8b4-218">Because US users are accessing an Application Proxy instance that happens toobe in hello same region, hop 1 is not too expensive.</span></span> <span data-ttu-id="da8b4-219">Le tronçon 3 est optimisé.</span><span class="sxs-lookup"><span data-stu-id="da8b4-219">Hop 3 is optimized.</span></span> <span data-ttu-id="da8b4-220">Envisagez d’utiliser ExpressRoute toooptimize tronçon 2.</span><span class="sxs-lookup"><span data-stu-id="da8b4-220">Consider using ExpressRoute toooptimize hop 2.</span></span> 

![Diagramme indiquant les utilisateurs et proxy hello US, avec le connecteur de hello et l’application en hello Europe](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

<span data-ttu-id="da8b4-222">Vous pouvez également envisager d’utiliser une autre variante dans cette situation.</span><span class="sxs-lookup"><span data-stu-id="da8b4-222">You can also consider using one other variant in this situation.</span></span> <span data-ttu-id="da8b4-223">Si la plupart des utilisateurs dans l’organisation de hello sont Bonjour nous, puis sans doute que votre réseau s’étend toohello nous ainsi.</span><span class="sxs-lookup"><span data-stu-id="da8b4-223">If most users in hello organization are in hello US, then chances are that your network extends toohello US as well.</span></span> <span data-ttu-id="da8b4-224">Placer le connecteur de hello Bonjour des États-Unis et utiliser application toohello en ligne de réseau d’entreprise interne hello dédié Bonjour Europe.</span><span class="sxs-lookup"><span data-stu-id="da8b4-224">Place hello connector in hello US, and use hello dedicated internal corporate network line toohello application in hello EU.</span></span> <span data-ttu-id="da8b4-225">Les tronçons 2 et 3 sont ainsi optimisés.</span><span class="sxs-lookup"><span data-stu-id="da8b4-225">This way hops 2 and 3 are optimized.</span></span>

![Diagramme montrant les utilisateurs, de proxy et de connecteur Bonjour US, application Bonjour Europe](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a><span data-ttu-id="da8b4-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="da8b4-227">Next steps</span></span>

- [<span data-ttu-id="da8b4-228">Activer le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="da8b4-228">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
- [<span data-ttu-id="da8b4-229">Activer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="da8b4-229">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="da8b4-230">Activer l’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="da8b4-230">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
- [<span data-ttu-id="da8b4-231">Résoudre les problèmes rencontrés avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="da8b4-231">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)