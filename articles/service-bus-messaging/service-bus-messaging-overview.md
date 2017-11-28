---
title: "Présentation de la messagerie Azure Service Bus | Microsoft Docs"
description: "Description de la messagerie Service Bus et d’Azure Relay"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 3a4382979dd6e18c0e94b4a989bb8289882eeb89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-the-cloud"></a><span data-ttu-id="312e2-103">Messagerie Service Bus : service flexible de distribution de données dans le cloud</span><span class="sxs-lookup"><span data-stu-id="312e2-103">Service Bus messaging: flexible data delivery in the cloud</span></span>
<span data-ttu-id="312e2-104">Microsoft Azure Service Bus est un service fiable de distribution des informations.</span><span class="sxs-lookup"><span data-stu-id="312e2-104">Microsoft Azure Service Bus is a reliable information delivery service.</span></span> <span data-ttu-id="312e2-105">L'objectif de ce service est de simplifier la communication.</span><span class="sxs-lookup"><span data-stu-id="312e2-105">The purpose of this service is to make communication easier.</span></span> <span data-ttu-id="312e2-106">Quand plusieurs parties souhaitent échanger des informations, elles ont besoin d'un système qui facilite la communication.</span><span class="sxs-lookup"><span data-stu-id="312e2-106">When two or more parties want to exchange information, they need a communication facilitator.</span></span> <span data-ttu-id="312e2-107">Service Bus est un système de communication tiers ou réparti,</span><span class="sxs-lookup"><span data-stu-id="312e2-107">Service Bus is a brokered, or third-party communication mechanism.</span></span> <span data-ttu-id="312e2-108">qui peut être comparé à un service postal classique.</span><span class="sxs-lookup"><span data-stu-id="312e2-108">This is similar to a postal service in the physical world.</span></span> <span data-ttu-id="312e2-109">Le service postal permet aux clients d'envoyer facilement partout dans le monde toutes sortes de lettres et de paquets, avec différentes garanties de distribution au choix.</span><span class="sxs-lookup"><span data-stu-id="312e2-109">Postal services make it very easy to send different kinds of letters and packages with a variety of delivery guarantees, anywhere in the world.</span></span>

<span data-ttu-id="312e2-110">À l’instar du service postal de distribution du courrier, Service Bus constitue un moyen flexible de distribuer des informations entre l’expéditeur et le destinataire.</span><span class="sxs-lookup"><span data-stu-id="312e2-110">Similar to the postal service delivering letters, Service Bus is flexible information delivery from both the sender and the recipient.</span></span> <span data-ttu-id="312e2-111">Ce service de messagerie garantit la distribution des informations même si les deux parties concernées ne sont jamais en ligne en même temps ou si elles ne sont pas disponibles au même moment.</span><span class="sxs-lookup"><span data-stu-id="312e2-111">The messaging service ensures that the information is delivered even if the two parties are never both online at the same time, or if they aren't available at the exact same time.</span></span> <span data-ttu-id="312e2-112">C'est en cela que ce système de communication répartie s'apparente à l'envoi d'une lettre, tandis que la communication non répartie équivaut à un appel téléphonique traditionnel (quand il n'y avait pas encore de signal d'appel ni d'identification de l'appelant, qui sont plutôt des fonctionnalités de messagerie répartie).</span><span class="sxs-lookup"><span data-stu-id="312e2-112">In this way, messaging is similar to sending a letter, while non-brokered communication is similar to placing a phone call (or how a phone call used to be - before call waiting and caller ID, which are much more like brokered messaging).</span></span>

<span data-ttu-id="312e2-113">L’expéditeur du message peut aussi choisir divers paramètres de distribution, notamment les transactions, la détection des doublons, l’expiration temporelle et le traitement par lot.</span><span class="sxs-lookup"><span data-stu-id="312e2-113">The message sender can also require a variety of delivery characteristics including transactions, duplicate detection, time-based expiration, and batching.</span></span> <span data-ttu-id="312e2-114">Ces modèles présentent également certaines analogies avec le service postal : tentative renouvelée de distribution, signature obligatoire, changement d'adresse ou rappel.</span><span class="sxs-lookup"><span data-stu-id="312e2-114">These patterns have postal analogies as well: repeat delivery, required signature, address change, or recall.</span></span>

<span data-ttu-id="312e2-115">Service Bus prend en charge deux modèles de messagerie distincts : *Azure Relay* et la *messagerie Service Bus*.</span><span class="sxs-lookup"><span data-stu-id="312e2-115">Service Bus supports two distinct messaging patterns: *Azure Relay* and *Service Bus Messaging*.</span></span>

## <a name="azure-relay"></a><span data-ttu-id="312e2-116">Azure Relay</span><span class="sxs-lookup"><span data-stu-id="312e2-116">Azure Relay</span></span>
<span data-ttu-id="312e2-117">Le composant [Relais WCF](../service-bus-relay/relay-what-is-it.md) d’Azure Relay est un service centralisé (mais très équilibré au niveau de la charge) qui prend en charge différents protocoles de transport et normes de services web.</span><span class="sxs-lookup"><span data-stu-id="312e2-117">The [WCF Relay](../service-bus-relay/relay-what-is-it.md) component of Azure Relay is a centralized (but highly load-balanced) service that supports a variety of different transport protocols and Web services standards.</span></span> <span data-ttu-id="312e2-118">Cela inclut SOAP, WS-* et même REST.</span><span class="sxs-lookup"><span data-stu-id="312e2-118">This includes SOAP, WS-*, and even REST.</span></span> <span data-ttu-id="312e2-119">Le [service de relais](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) fournit une gamme d’options de connectivité relais différentes et aide à négocier des connexions directes peer-to-peer quand c’est possible.</span><span class="sxs-lookup"><span data-stu-id="312e2-119">The [relay service](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) provides a variety of different relay connectivity options and can help negotiate direct peer-to-peer connections when it is possible.</span></span> <span data-ttu-id="312e2-120">Service Bus est optimisé pour les développeurs .NET qui utilisent Windows Communication Foundation (WCF), en ce qui concerne à la fois les performances et la convivialité, et fournit un accès complet à son service de relais via des interfaces SOAP et REST.</span><span class="sxs-lookup"><span data-stu-id="312e2-120">Service Bus is optimized for .NET developers who use the Windows Communication Foundation (WCF), both with regard to performance and usability, and provides full access to its relay service through SOAP and REST interfaces.</span></span> <span data-ttu-id="312e2-121">Cela rend possible l’intégration de n'importe quel environnement de programmation SOAP ou REST à Service Bus.</span><span class="sxs-lookup"><span data-stu-id="312e2-121">This makes it possible for any SOAP or REST programming environment to integrate with Service Bus.</span></span>

<span data-ttu-id="312e2-122">Le service de relais prend en charge la messagerie unidirectionnelle standard, la messagerie demande/réponse et la messagerie d’homologue à homologue.</span><span class="sxs-lookup"><span data-stu-id="312e2-122">The relay service supports traditional one-way messaging, request/response messaging, and peer-to-peer messaging.</span></span> <span data-ttu-id="312e2-123">Il prend également en charge la distribution des événements sur Internet pour activer les scénarios de publication/abonnement et la communication par socket bidirectionnelle pour une efficacité accrue de point à point.</span><span class="sxs-lookup"><span data-stu-id="312e2-123">It also supports event distribution at Internet-scope to enable publish-subscribe scenarios and bi-directional socket communication for increased point-to-point efficiency.</span></span> <span data-ttu-id="312e2-124">Dans le modèle de messagerie par relais, un service local se connecte au service de relais via un port sortant et crée un socket bidirectionnel lié à des adresses de rendez-vous spécifiques.</span><span class="sxs-lookup"><span data-stu-id="312e2-124">In the relayed messaging pattern, an on-premises service connects to the relay service through an outbound port and creates a bi-directional socket for communication tied to a particular rendezvous address.</span></span> <span data-ttu-id="312e2-125">Le client peut ensuite communiquer avec le service local en envoyant des messages au service de relais en ciblant l'adresse de rendezvous.</span><span class="sxs-lookup"><span data-stu-id="312e2-125">The client can then communicate with the on-premises service by sending messages to the relay service targeting the rendezvous address.</span></span> <span data-ttu-id="312e2-126">Le service de relais « relayera » ensuite les messages au service local via le socket bidirectionnel déjà en place.</span><span class="sxs-lookup"><span data-stu-id="312e2-126">The relay service will then "relay" messages to the on-premises service through the bi-directional socket already in place.</span></span> <span data-ttu-id="312e2-127">Le client n’a pas besoin d’une connexion directe au service local ni de savoir où se trouve le service, et le service local n’a pas besoin d’ouvrir de ports entrants sur le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="312e2-127">The client does not need a direct connection to the on-premises service, nor is it required to know where the service resides, and the on-premises service does not need any inbound ports open on the firewall.</span></span>

<span data-ttu-id="312e2-128">Vous lancez la connexion entre votre service local et le service de relais à l’aide d’une suite de liaisons de « relais » WCF.</span><span class="sxs-lookup"><span data-stu-id="312e2-128">You initiate the connection between your on-premises service and the relay service, using a suite of WCF "relay" bindings.</span></span> <span data-ttu-id="312e2-129">En coulisses, les liaisons de relais se mappent à des éléments de liaison de transport destinés à créer des composants de canal WCF qui s’intègrent à Service Bus dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="312e2-129">Behind the scenes, the relay bindings map to transport binding elements designed to create WCF channel components that integrate with Service Bus in the cloud.</span></span>

<span data-ttu-id="312e2-130">WCF Relay offre de nombreux avantages, mais nécessite que le serveur et le client soient en ligne en même temps pour envoyer et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="312e2-130">WCF Relay provides many benefits, but requires the server and client to both be online at the same time in order to send and receive messages.</span></span> <span data-ttu-id="312e2-131">Cela n’est pas optimal pour la communication de style HTTP, dans laquelle les requêtes ne sont généralement pas durables, ni pour les clients qui ne se connectent qu’occasionnellement, comme les navigateurs, les applications mobiles et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="312e2-131">This is not optimal for HTTP-style communication, in which the requests may not be typically long-lived, nor for clients that connect only occasionally, such as browsers, mobile applications, and so on.</span></span> <span data-ttu-id="312e2-132">La messagerie répartie prend en charge la communication répartie et a ses propres avantages ; les clients et les serveurs peuvent se connecter lorsque c’est nécessaire et effectuer leurs opérations de manière asynchrone.</span><span class="sxs-lookup"><span data-stu-id="312e2-132">Brokered messaging supports decoupled communication, and has its own advantages; clients and servers can connect when needed and perform their operations in an asynchronous manner.</span></span>

## <a name="brokered-messaging"></a><span data-ttu-id="312e2-133">Messagerie répartie</span><span class="sxs-lookup"><span data-stu-id="312e2-133">Brokered messaging</span></span>
<span data-ttu-id="312e2-134">Contrairement au modèle de relais, la messagerie Service Bus, ou [messagerie répartie](service-bus-queues-topics-subscriptions.md), peut être considérée comme asynchrone ou « temporellement découplée ».</span><span class="sxs-lookup"><span data-stu-id="312e2-134">In contrast to the relay scheme, Service Bus messaging, or [brokered messaging](service-bus-queues-topics-subscriptions.md) can be thought of as asynchronous, or "temporally decoupled."</span></span> <span data-ttu-id="312e2-135">Les producteurs (expéditeurs) et les consommateurs (récepteurs) n'ont pas besoin d’être en ligne en même temps.</span><span class="sxs-lookup"><span data-stu-id="312e2-135">Producers (senders) and consumers (receivers) do not have to be online at the same time.</span></span> <span data-ttu-id="312e2-136">L'infrastructure de la messagerie stocke les messages de façon fiable dans un « broker » (par exemple, une file d'attente) jusqu'à ce que le récepteur soit prêt à les recevoir.</span><span class="sxs-lookup"><span data-stu-id="312e2-136">The messaging infrastructure reliably stores messages in a "broker" (such as a queue) until the consuming party is ready to receive them.</span></span> <span data-ttu-id="312e2-137">Ceci permet aux composants de l'application distribuée d'être déconnectés, soit volontairement, par exemple pour des raisons de maintenance, soit en raison de l'échec d'un composant, sans conséquences sur le système dans sa globalité.</span><span class="sxs-lookup"><span data-stu-id="312e2-137">This allows the components of the distributed application to be disconnected, either voluntarily; for example, for maintenance, or due to a component crash, without affecting the entire system.</span></span> <span data-ttu-id="312e2-138">En outre, il se peut que l'application réceptrice n’ait besoin d’être en ligne qu’à certaines heures de la journée (par exemple, un système de gestion d'inventaire dont l’exécution n’est requise qu’en fin de journée).</span><span class="sxs-lookup"><span data-stu-id="312e2-138">Furthermore, the receiving application may only have to come online during certain times of the day, such as an inventory management system that only is required to run at the end of the business day.</span></span>

<span data-ttu-id="312e2-139">Les principaux composants de l’infrastructure de la messagerie répartie Service Bus sont des files d’attente, des rubriques et des abonnements.</span><span class="sxs-lookup"><span data-stu-id="312e2-139">The core components of the Service Bus brokered messaging infrastructure are queues, topics, and subscriptions.</span></span>  <span data-ttu-id="312e2-140">La principale différence est que les rubriques prennent en charge les fonctionnalités de publication et d’abonnement qui peuvent être utilisées dans la logique de distribution et de routage basée sur du contenu sophistiqué, y compris l’envoi à plusieurs destinataires.</span><span class="sxs-lookup"><span data-stu-id="312e2-140">The primary difference is that topics support publish/subscribe capabilities that can be used for sophisticated content-based routing and delivery logic, including sending to multiple recipients.</span></span> <span data-ttu-id="312e2-141">Ces composants donnent accès à de nouveaux scénarios de messagerie asynchrone, comme le découplage temporel, la publication/abonnement et l'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="312e2-141">These components enable new asynchronous messaging scenarios, such as temporal decoupling, publish/subscribe, and load balancing.</span></span> <span data-ttu-id="312e2-142">Pour plus d’informations sur ces éléments de messagerie, consultez [Files d’attente, rubriques et abonnements Service Bus](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="312e2-142">For more information about these messaging entities, see [Service Bus queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>

<span data-ttu-id="312e2-143">Comme pour l’infrastructure WCF Relay, la fonctionnalité de messagerie répartie est destinée aux programmeurs WCF et .NET Framework, ainsi que via REST.</span><span class="sxs-lookup"><span data-stu-id="312e2-143">As with the WCF Relay infrastructure, the brokered messaging capability is provided for WCF and .NET Framework programmers, and also via REST.</span></span>

## <a name="next-steps"></a><span data-ttu-id="312e2-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="312e2-144">Next steps</span></span>
<span data-ttu-id="312e2-145">Pour en savoir plus sur la messagerie Service Bus, voir les rubriques suivantes.</span><span class="sxs-lookup"><span data-stu-id="312e2-145">To learn more about Service Bus messaging, see the following topics.</span></span>

* [<span data-ttu-id="312e2-146">Concepts de base de Service Bus</span><span class="sxs-lookup"><span data-stu-id="312e2-146">Service Bus fundamentals</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="312e2-147">Files d’attente, rubriques et abonnements Service Bus</span><span class="sxs-lookup"><span data-stu-id="312e2-147">Service Bus queues, topics, and subscriptions</span></span>](service-bus-queues-topics-subscriptions.md)
* [<span data-ttu-id="312e2-148">Utilisation des files d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="312e2-148">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="312e2-149">Utilisation des rubriques et abonnements Service Bus</span><span class="sxs-lookup"><span data-stu-id="312e2-149">How to use Service Bus topics and subscriptions</span></span>](service-bus-dotnet-how-to-use-topics-subscriptions.md)
