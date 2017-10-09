---
title: "vue d’ensemble de la grille d’événement aaaAzure"
description: "Détaille Azure Event Grid et ses concepts."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="82db1-103">Un tooAzure présentation grille d’événement</span><span class="sxs-lookup"><span data-stu-id="82db1-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="82db1-104">Azure grille d’événement vous permet de créer des applications tooeasily avec les architectures basées sur les événements.</span><span class="sxs-lookup"><span data-stu-id="82db1-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="82db1-105">Vous sélectionnez hello ressources Azure vous comme toosubscribe à et donner le Gestionnaire d’événements hello ou WebHook point de terminaison toosend hello événement.</span><span class="sxs-lookup"><span data-stu-id="82db1-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="82db1-106">Event Grid dispose d’une prise en charge intégrée pour les événements provenant des services Azure, tels que les objets BLOB de stockage et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="82db1-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="82db1-107">Event Grid dispose également d’une prise en charge personnalisée pour les événements d’application et de tiers, à l’aide des rubriques et webhooks personnalisés.</span><span class="sxs-lookup"><span data-stu-id="82db1-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="82db1-108">Vous pouvez utiliser les filtres tooroute des événements spécifiques toodifferent points, points de terminaison de multidiffusion toomultiple et assurez-vous que vos événements sont remis de manière fiable.</span><span class="sxs-lookup"><span data-stu-id="82db1-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="82db1-109">Event Grid dispose également d’une prise en charge intégrée pour des événements personnalisés et tiers.</span><span class="sxs-lookup"><span data-stu-id="82db1-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="82db1-110">Pour la version préliminaire de hello, prend en charge la grille d’événement **westus2** et **westcentralus** emplacements.</span><span class="sxs-lookup"><span data-stu-id="82db1-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="82db1-111">D’autres régions seront ajoutées.</span><span class="sxs-lookup"><span data-stu-id="82db1-111">Other regions will be added.</span></span>

<span data-ttu-id="82db1-112">Cet article fournit une vue d’ensemble d’Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="82db1-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="82db1-113">Si vous souhaitez tooget main de grille d’événement, consultez [créer et itinéraire des événements personnalisés avec la grille d’événement Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="82db1-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Modèle de grille d’événement fonctionnel](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="82db1-115">Stockage Blob n’est pas disponible publiquement en tant qu’éditeur.</span><span class="sxs-lookup"><span data-stu-id="82db1-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="82db1-116">Concepts</span><span class="sxs-lookup"><span data-stu-id="82db1-116">Concepts</span></span>

<span data-ttu-id="82db1-117">Il existe cinq concepts dans Azure Event Grid qui vous permettent de démarrer :</span><span class="sxs-lookup"><span data-stu-id="82db1-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="82db1-118">**Événements** : ce qu’il s’est passé.</span><span class="sxs-lookup"><span data-stu-id="82db1-118">**Events** - What happened.</span></span>
* <span data-ttu-id="82db1-119">**Sources/éditeurs d’événements** : si l’événement de hello a eu lieu.</span><span class="sxs-lookup"><span data-stu-id="82db1-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="82db1-120">**Rubriques** -hello du point de terminaison où envoyer des événements par les serveurs de publication.</span><span class="sxs-lookup"><span data-stu-id="82db1-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="82db1-121">**Abonnements aux événements** -événements de tooroute mécanisme intégré ou de point de terminaison des hello, parfois toomultiple gestionnaires.</span><span class="sxs-lookup"><span data-stu-id="82db1-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="82db1-122">Les abonnements sont également utilisés par les événements entrants gestionnaires toointelligently filtre.</span><span class="sxs-lookup"><span data-stu-id="82db1-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="82db1-123">**Gestionnaires d’événements** - hello application ou service réaction toohello événement.</span><span class="sxs-lookup"><span data-stu-id="82db1-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="82db1-124">Pour plus d’informations sur ces concepts, consultez [Concepts dans Azure Event Grid](concepts.md).</span><span class="sxs-lookup"><span data-stu-id="82db1-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="82db1-125">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="82db1-125">Capabilities</span></span>

<span data-ttu-id="82db1-126">Voici quelques-unes des principales fonctionnalités de hello de grille d’événement Azure :</span><span class="sxs-lookup"><span data-stu-id="82db1-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="82db1-127">**Simplicité** -Point et cliquer sur les événements tooaim à partir de votre gestionnaire d’événements tooany ressource Azure ou d’un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="82db1-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="82db1-128">**Filtrage avancé** -filtre sur un événement de type ou l’événement de publication tooensure de chemin d’accès gestionnaires d’événements reçoivent uniquement les événements pertinents.</span><span class="sxs-lookup"><span data-stu-id="82db1-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="82db1-129">**Distribution ramifiée** -s’abonner à plusieurs points de terminaison toohello même événement toosend copie de hello événement tooas beaucoup d’emplacements en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="82db1-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="82db1-130">**Fiabilité** -utiliser la nouvelle tentative de 24 heures avec tooensure interruption exponentielle les événements sont remis.</span><span class="sxs-lookup"><span data-stu-id="82db1-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="82db1-131">**Payer par événement** - payez uniquement pour la quantité de hello vous utilisez la grille d’événement.</span><span class="sxs-lookup"><span data-stu-id="82db1-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="82db1-132">**Débit élevé** : générez des charges de travail élevées sur Event Grid avec prise en charge de millions d’événements par seconde.</span><span class="sxs-lookup"><span data-stu-id="82db1-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="82db1-133">**Événements intégrés** : préparez et soyez rapidement opérationnel avec des événements intégrés définis par la ressource.</span><span class="sxs-lookup"><span data-stu-id="82db1-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="82db1-134">**Événements personnalisés** : utilisez le routage Event Grid, le filtrage et les événements personnalisés livré de manière fiable dans votre application.</span><span class="sxs-lookup"><span data-stu-id="82db1-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="82db1-135">Intégration du gestionnaire et de l’éditeur intégrés</span><span class="sxs-lookup"><span data-stu-id="82db1-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="82db1-136">Azure propose la prise en charge de l’événement intégré à l’aide de nombreux services, y compris les éditeurs et les gestionnaires.</span><span class="sxs-lookup"><span data-stu-id="82db1-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="82db1-137">Éditeurs</span><span class="sxs-lookup"><span data-stu-id="82db1-137">Publishers</span></span>

<span data-ttu-id="82db1-138">Actuellement, hello services Azure suivants ont prise en charge de serveur de publication intégré pour la grille d’événement :</span><span class="sxs-lookup"><span data-stu-id="82db1-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="82db1-139">Groupes de ressources (opérations de gestion)</span><span class="sxs-lookup"><span data-stu-id="82db1-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="82db1-140">Abonnements Azure (opérations de gestion)</span><span class="sxs-lookup"><span data-stu-id="82db1-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="82db1-141">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="82db1-141">Event Hubs</span></span>
* <span data-ttu-id="82db1-142">Rubriques personnalisées</span><span class="sxs-lookup"><span data-stu-id="82db1-142">Custom Topics</span></span>

<span data-ttu-id="82db1-143">D’autres services Azure seront ajoutés cette année.</span><span class="sxs-lookup"><span data-stu-id="82db1-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="82db1-144">Gestionnaires</span><span class="sxs-lookup"><span data-stu-id="82db1-144">Handlers</span></span>

<span data-ttu-id="82db1-145">Actuellement, hello services Azure suivants ont intégré Gestionnaire prise en charge pour la grille d’événement :</span><span class="sxs-lookup"><span data-stu-id="82db1-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="82db1-146">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="82db1-146">Azure Functions</span></span>
* <span data-ttu-id="82db1-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="82db1-147">Logic Apps</span></span>
* <span data-ttu-id="82db1-148">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="82db1-148">Azure Automation</span></span>
* <span data-ttu-id="82db1-149">WebHooks</span><span class="sxs-lookup"><span data-stu-id="82db1-149">WebHooks</span></span>

<span data-ttu-id="82db1-150">D’autres services Azure seront ajoutés cette année.</span><span class="sxs-lookup"><span data-stu-id="82db1-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="82db1-151">Que puis-je faire avec Event Grid ?</span><span class="sxs-lookup"><span data-stu-id="82db1-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="82db1-152">Azure Event Grid fournit plusieurs fonctionnalités qui améliorent considérablement l’automatisation d’opérations sans serveur et le travail d’intégration :</span><span class="sxs-lookup"><span data-stu-id="82db1-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="82db1-153">Architectures d’application sans serveur</span><span class="sxs-lookup"><span data-stu-id="82db1-153">Serverless application architectures</span></span>

![Application sans serveur](./media/overview/serverless_web_app.png)

<span data-ttu-id="82db1-155">La grille d’événement connecte des sources de données et des gestionnaires d’événements.</span><span class="sxs-lookup"><span data-stu-id="82db1-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="82db1-156">Par exemple, utiliser déclencheur tooinstantly de grille d’événement pour une analyse d’image sans fonction toorun chaque fois qu’une nouvelle photo est ajouté le conteneur de stockage d’objets blob tooa.</span><span class="sxs-lookup"><span data-stu-id="82db1-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="82db1-157">Automatisation des opérations</span><span class="sxs-lookup"><span data-stu-id="82db1-157">Ops Automation</span></span>

![Automatisation des opérations](./media/overview/Ops_automation.png)

<span data-ttu-id="82db1-159">Grille d’événement vous permet d’automatiser de toospeed et simplifier la mise en œuvre de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="82db1-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="82db1-160">Par exemple, Event Grid peut informer Azure Automation lors de la création d’une machine virtuelle ou de l’entrée en service d’une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="82db1-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="82db1-161">Ces événements peuvent être utilisés tooautomatically vérifier que les configurations de service sont compatibles, placer des métadonnées dans les outils, les machines virtuelles de balise ou les éléments de travail de fichier.</span><span class="sxs-lookup"><span data-stu-id="82db1-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="82db1-162">Intégration d’applications</span><span class="sxs-lookup"><span data-stu-id="82db1-162">Application integration</span></span>

![Intégration d’applications](./media/overview/app_integration.png)

<span data-ttu-id="82db1-164">Event Grid connecte votre application à d’autres services.</span><span class="sxs-lookup"><span data-stu-id="82db1-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="82db1-165">Par exemple, créez une rubrique personnalisée de toosend tooEvent de données d’événement de votre application grille et tirer parti de sa remise fiable, avancée, le routage et intégration directe avec Azure.</span><span class="sxs-lookup"><span data-stu-id="82db1-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="82db1-166">Ou bien, vous pouvez utiliser grille d’événement avec des données Logic Apps tooprocess n’importe où, sans écrire de code.</span><span class="sxs-lookup"><span data-stu-id="82db1-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="82db1-167">En quoi Event Grid est différent d’autres services d’intégration Azure ?</span><span class="sxs-lookup"><span data-stu-id="82db1-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="82db1-168">Event Grid est un fond de panier de gestion des événements qui permet la programmation réactive, pilotée par événements.</span><span class="sxs-lookup"><span data-stu-id="82db1-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="82db1-169">Elle est intégrée en profondeur aux services Azure et peut être intégrée à des services tiers.</span><span class="sxs-lookup"><span data-stu-id="82db1-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="82db1-170">message d’événement Hello contient les informations de hello nécessaires toochanges tooreact dans les services et applications.</span><span class="sxs-lookup"><span data-stu-id="82db1-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="82db1-171">Grille d’événement n’est pas un pipeline de données et il ne remet plus aucun objet hello réel qui a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="82db1-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="82db1-172">Service Bus est parfaitement adapté aux applications d’entreprise traditionnelles qui nécessitent des transactions, des classements, la détection des doublons et une cohérence instantanée.</span><span class="sxs-lookup"><span data-stu-id="82db1-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="82db1-173">Event Grid est conçu pour la vitesse, la mise à l’échelle, l’étendue et le bas coût dans un modèle réactif.</span><span class="sxs-lookup"><span data-stu-id="82db1-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="82db1-174">Il est parfaitement tooserverless architecture.</span><span class="sxs-lookup"><span data-stu-id="82db1-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="82db1-175">Event Grid complète d’autres services Azure tels que Logic Apps et Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="82db1-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="82db1-176">Les déclencheurs d’événements grille hello logique application toobegin son flux de travail.</span><span class="sxs-lookup"><span data-stu-id="82db1-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="82db1-177">Concentrateurs d’événements fonctionne avec la grille d’événement en vous tooevents tooreact de capturer des concentrateurs d’événements et les pipelines d’entrée et de transformation de données de build.</span><span class="sxs-lookup"><span data-stu-id="82db1-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="82db1-178">Combien coûte Event Grid ?</span><span class="sxs-lookup"><span data-stu-id="82db1-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="82db1-179">Azure Event Grid utilise un modèle de tarification de paie par événement, afin que vous ne payez que ce que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="82db1-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="82db1-180">Grille d’événement coûte 0,60 $ par million d’opérations (0,30 pendant la version préliminaire) et hello opération 100 000 premiers par mois sont gratuits.</span><span class="sxs-lookup"><span data-stu-id="82db1-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="82db1-181">Les opérations sont définies comme entrée d’événement, correspondance avancée, tentative de livraison et appels de gestion.</span><span class="sxs-lookup"><span data-stu-id="82db1-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="82db1-182">Vous trouverez plus de détails sur hello [page de tarification](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="82db1-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82db1-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82db1-183">Next steps</span></span>

* <span data-ttu-id="82db1-184">[Créer et de s’abonner à des événements de toocustom](custom-event-quickstart.md) concrète et démarrer l’envoi de votre propre point de terminaison tooany événements personnalisés à l’aide du démarrage rapide de grille d’événement Azure hello.</span><span class="sxs-lookup"><span data-stu-id="82db1-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="82db1-185">[À l’aide de Logic Apps comme gestionnaire d’événements](monitor-virtual-machine-changes-event-grid-logic-app.md) un didacticiel sur la création d’une application à l’aide de Logic Apps tooreact tooevents exécute un push de grille d’événement.</span><span class="sxs-lookup"><span data-stu-id="82db1-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="82db1-186">Référence de l'API REST Event Grid</span><span class="sxs-lookup"><span data-stu-id="82db1-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="82db1-187">Fournit des informations techniques supplémentaires sur hello grille d’événement Azure et une référence pour la gestion des abonnements aux événements, routage et le filtrage.</span><span class="sxs-lookup"><span data-stu-id="82db1-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
