---
title: "aaaMonitor d’API avec gestion des API Azure et les concentrateurs d’événements Runscope | Documents Microsoft"
description: "Exemple d’application illustrant la stratégie de journal à eventhub hello par connexion gestion des API Azure, Azure Event Hubs et Runscope pour le protocole HTTP, journalisation et de surveillance"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="f3750-103">Surveiller vos API avec gestion des API Azure, les hubs d’événements et Runscope</span><span class="sxs-lookup"><span data-stu-id="f3750-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="f3750-104">Hello [service de gestion des API](api-management-key-concepts.md) fournit de nombreuses fonctionnalités tooenhance hello le traitement des demandes envoyées de HTTP tooyour API HTTP.</span><span class="sxs-lookup"><span data-stu-id="f3750-104">hello [API Management service](api-management-key-concepts.md) provides many capabilities tooenhance hello processing of HTTP requests sent tooyour HTTP API.</span></span> <span data-ttu-id="f3750-105">Toutefois, hello existence de hello demandes et réponses sont temporaires.</span><span class="sxs-lookup"><span data-stu-id="f3750-105">However, hello existence of hello requests and responses are transient.</span></span> <span data-ttu-id="f3750-106">Hello est demandé et il transite par hello gestion des API service tooyour API de service principal.</span><span class="sxs-lookup"><span data-stu-id="f3750-106">hello request is made and it flows through hello API Management service tooyour backend API.</span></span> <span data-ttu-id="f3750-107">Votre API traite la demande de hello et une réponse transite par le biais de toohello API consommateur.</span><span class="sxs-lookup"><span data-stu-id="f3750-107">Your API processes hello request and a response flows back through toohello API consumer.</span></span> <span data-ttu-id="f3750-108">Hello service de gestion des API conserve des statistiques importantes concernant hello API pour l’affichage dans le tableau de bord de portail de Publisher hello, mais, les détails de hello ont disparu.</span><span class="sxs-lookup"><span data-stu-id="f3750-108">hello API Management service keeps some important statistics about hello APIs for display in hello Publisher portal dashboard, but beyond that, hello details are gone.</span></span>

<span data-ttu-id="f3750-109">À l’aide de hello [journal à eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [stratégie](api-management-howto-policies.md) Bonjour service de gestion des API, vous pouvez envoyer des détails à partir de tooan de demande et de réponse hello [concentrateur d’événements Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="f3750-109">By using hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in hello API Management service you can send any details from hello request and response tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="f3750-110">Il existe de nombreuses raisons pour lesquelles vous souhaiterez peut-être toogenerate des événements à partir de messages HTTP envoyés tooyour API.</span><span class="sxs-lookup"><span data-stu-id="f3750-110">There are a variety of reasons why you may want toogenerate events from HTTP messages being sent tooyour APIs.</span></span> <span data-ttu-id="f3750-111">Certains exemples incluent une piste d’audit des mises à jour, une analyse des usages, une alerte en cas d’exception et l’intégration de tiers.</span><span class="sxs-lookup"><span data-stu-id="f3750-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="f3750-112">Cet article montre comment les toocapture hello HTTP demande et réponse message entier, envoyer tooan concentrateur d’événements et de relais ensuite ce service de tiers tooa message qui fournit la journalisation et analyse des services HTTP.</span><span class="sxs-lookup"><span data-stu-id="f3750-112">This article demonstrates how toocapture hello entire HTTP request and response message, send it tooan Event Hub and then relay that message tooa third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="f3750-113">Pourquoi effectuer l’envoi depuis un service de gestion d’API ?</span><span class="sxs-lookup"><span data-stu-id="f3750-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="f3750-114">Il est possible de toowrite HTTP intergiciel (middleware) qui peut s’intégrer à l’API HTTP infrastructures toocapture demandes et réponses HTTP et les flux dans l’analyse des systèmes et de journalisation.</span><span class="sxs-lookup"><span data-stu-id="f3750-114">It is possible toowrite HTTP middleware that can plug into HTTP API frameworks toocapture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="f3750-115">Hello inconvénient toothis consiste intergiciel (middleware) de hello HTTP doit toobe intégré dans les API de service principal hello et doit correspondre à la plateforme hello de hello API.</span><span class="sxs-lookup"><span data-stu-id="f3750-115">hello downside toothis approach is hello HTTP middleware needs toobe integrated into hello backend API and must match hello platform of hello API.</span></span> <span data-ttu-id="f3750-116">S’il existe plusieurs API chacun d’eux doit déployer hello intergiciel (middleware).</span><span class="sxs-lookup"><span data-stu-id="f3750-116">If there are multiple APIs then each one must deploy hello middleware.</span></span> <span data-ttu-id="f3750-117">Il existe souvent des raisons pour lesquelles les API de serveur principal ne peuvent pas être mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f3750-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="f3750-118">À l’aide de toointegrate de service de gestion des API Azure hello avec l’infrastructure de journalisation fournit une solution centralisée et indépendante de la plate-forme.</span><span class="sxs-lookup"><span data-stu-id="f3750-118">Using hello Azure API Management service toointegrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="f3750-119">Il est également évolutif en partie toohello [géo-réplication](api-management-howto-deploy-multi-region.md) fonctionnalités de gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="f3750-119">It is also scalable, in part due toohello [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-tooan-azure-event-hub"></a><span data-ttu-id="f3750-120">Pourquoi envoyer tooan concentrateur d’événements Azure ?</span><span class="sxs-lookup"><span data-stu-id="f3750-120">Why send tooan Azure Event Hub?</span></span>
<span data-ttu-id="f3750-121">Il s’agit d’un tooask raisonnable, pourquoi créer une stratégie de concentrateurs d’événements tooAzure spécifique ?</span><span class="sxs-lookup"><span data-stu-id="f3750-121">It is a reasonable tooask, why create a policy that is specific tooAzure Event Hubs?</span></span> <span data-ttu-id="f3750-122">Il existe de nombreux emplacements distincts et où je souhaite avoir toolog mes demandes.</span><span class="sxs-lookup"><span data-stu-id="f3750-122">There are many different places where I might want toolog my requests.</span></span> <span data-ttu-id="f3750-123">Pourquoi ne pas envoyer hello demande directement toohello sa destination finale ?</span><span class="sxs-lookup"><span data-stu-id="f3750-123">Why not just send hello requests directly toohello final destination?</span></span>  <span data-ttu-id="f3750-124">C’est une option.</span><span class="sxs-lookup"><span data-stu-id="f3750-124">That is an option.</span></span> <span data-ttu-id="f3750-125">Toutefois, lors de la journalisation des requêtes à partir d’un service de gestion des API, il est nécessaire tooconsider comment des messages de journalisation aura un impact sur les performances hello Hello API.</span><span class="sxs-lookup"><span data-stu-id="f3750-125">However, when making logging requests from an API management service, it is necessary tooconsider how logging messages will impact hello performance of hello API.</span></span> <span data-ttu-id="f3750-126">L’augmentation progressive de charge peut être traitées par l’augmentation du nombre d’instances disponibles de composants système ou par le biais de la géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="f3750-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="f3750-127">Toutefois, courts pics de trafic peuvent entraîner des toobe demandes considérablement retardé si le démarrage de l’infrastructure de toologging demandes tooslow sous charge.</span><span class="sxs-lookup"><span data-stu-id="f3750-127">However, short spikes in traffic can cause requests toobe significantly delayed if requests toologging infrastructure start tooslow under load.</span></span>

<span data-ttu-id="f3750-128">Hello Azure Event Hubs est conçue tooingress très grands volumes de données, avec une capacité de traitement avec un nombre beaucoup plus élevé d’événements que nombre hello du serveur proxy demande la plupart des processus d’API.</span><span class="sxs-lookup"><span data-stu-id="f3750-128">hello Azure Event Hubs is designed tooingress huge volumes of data, with capacity for dealing with a far higher number of events than hello number of HTTP requests most APIs process.</span></span> <span data-ttu-id="f3750-129">Hello concentrateur d’événements agit comme un type de tampon sophistiqué entre votre infrastructure de gestion API service et hello qui devront stocker et traiter les messages de type hello.</span><span class="sxs-lookup"><span data-stu-id="f3750-129">hello Event Hub acts as a kind of sophisticated buffer between your API management service and hello infrastructure that will store and process hello messages.</span></span> <span data-ttu-id="f3750-130">Cela garantit que les performances de votre API ne seront pas affectées en raison de l’infrastructure d’enregistrement toohello.</span><span class="sxs-lookup"><span data-stu-id="f3750-130">This ensures that your API performance will not suffer due toohello logging infrastructure.</span></span>  

<span data-ttu-id="f3750-131">Une fois que les données de salutation a été passées tooan concentrateur d’événements, il est conservé et attendra tooprocess des consommateurs de concentrateur d’événements qu’il.</span><span class="sxs-lookup"><span data-stu-id="f3750-131">Once hello data has been passed tooan Event Hub it is persisted and will wait for Event Hub consumers tooprocess it.</span></span> <span data-ttu-id="f3750-132">Hello concentrateur d’événements ne soucie pas du mode de traitement, il reconnaît uniquement sur l’établissement de message de type hello soient correctement remis.</span><span class="sxs-lookup"><span data-stu-id="f3750-132">hello Event Hub does not care how it will be processed, it just cares about making sure hello message will be successfully delivered.</span></span>     

<span data-ttu-id="f3750-133">Concentrateurs d’événements ont des groupes de consommateurs toomultiple hello capacité toostream événements.</span><span class="sxs-lookup"><span data-stu-id="f3750-133">Event Hubs have hello ability toostream events toomultiple consumer groups.</span></span> <span data-ttu-id="f3750-134">Cela permet de toobe événements traité par les systèmes complètement différents.</span><span class="sxs-lookup"><span data-stu-id="f3750-134">This allows events toobe processed by completely different systems.</span></span> <span data-ttu-id="f3750-135">Cela permet la prise en charge de nombreux scénarios d’intégration sans avoir à insérer des retards d’ajout sur hello du traitement de la demande d’API hello au sein du service de gestion des API hello qu’un seul événement besoins toobe généré.</span><span class="sxs-lookup"><span data-stu-id="f3750-135">This enables supporting many integration scenarios without putting addition delays on hello processing of hello API request within hello API Management service as only one event needs toobe generated.</span></span>

## <a name="a-policy-toosend-applicationhttp-messages"></a><span data-ttu-id="f3750-136">Une stratégie toosend application/http les messages</span><span class="sxs-lookup"><span data-stu-id="f3750-136">A policy toosend application/http messages</span></span>
<span data-ttu-id="f3750-137">Un hub d’événements accepte des données d’événement en tant que chaîne simple.</span><span class="sxs-lookup"><span data-stu-id="f3750-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="f3750-138">Hello contenu de cette chaîne est complètement les tooyou.</span><span class="sxs-lookup"><span data-stu-id="f3750-138">hello contents of that string are completely up tooyou.</span></span> <span data-ttu-id="f3750-139">toopackage en mesure de toobe jusqu'à une requête HTTP et envoyer tooEvent concentrateurs, nous avons besoin de chaîne de hello tooformat avec les informations de demande ou réponse hello.</span><span class="sxs-lookup"><span data-stu-id="f3750-139">toobe able toopackage up an HTTP request and send it off tooEvent Hubs we need tooformat hello string with hello request or response information.</span></span> <span data-ttu-id="f3750-140">Dans de tels cas, s’il existe un format existant, que nous pouvons réutiliser, puis nous pouvons inutile toowrite notre propre à l’analyse de code.</span><span class="sxs-lookup"><span data-stu-id="f3750-140">In situations like this, if there is an existing format we can reuse, then we may not have toowrite our own parsing code.</span></span> <span data-ttu-id="f3750-141">Initialement, j’envisagé à l’aide de hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) pour l’envoi de demandes et réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="f3750-141">Initially I considered using hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="f3750-142">Cependant, ce format est optimisé pour stocker une séquence de requêtes HTTP dans un format basé sur JSON.</span><span class="sxs-lookup"><span data-stu-id="f3750-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="f3750-143">Elle contenait un nombre d’éléments obligatoires qui a ajouté une complexité inutile pour le scénario hello du passage d’un message de type hello HTTP acheminement hello.</span><span class="sxs-lookup"><span data-stu-id="f3750-143">It contained a number of mandatory elements that added unnecessary complexity for hello scenario of passing hello HTTP message over hello wire.</span></span>  

<span data-ttu-id="f3750-144">Une autre option a été toouse hello `application/http` type de média comme décrit dans la spécification de hello HTTP [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="f3750-144">An alternative option was toouse hello `application/http` media type as described in hello HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="f3750-145">Ce type de média utilise hello exacte dans le même format qui est utilisé tooactually envoyer des messages HTTP acheminement hello, mais la totalité du message hello peut être placé dans le corps de hello d’une autre demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="f3750-145">This media type uses hello exact same format that is used tooactually send HTTP messages over hello wire, but hello entire message can be put in hello body of another HTTP request.</span></span> <span data-ttu-id="f3750-146">Dans notre cas, nous allons corps de hello toouse en tant que notre tooEvent de toosend message concentrateurs.</span><span class="sxs-lookup"><span data-stu-id="f3750-146">In our case we are just going toouse hello body as our message toosend tooEvent Hubs.</span></span> <span data-ttu-id="f3750-147">Pour des raisons pratiques, est un analyseur qui existe dans [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliothèques qui peuvent analyser ce format et le convertir en hello natif `HttpRequestMessage` et `HttpResponseMessage` objets.</span><span class="sxs-lookup"><span data-stu-id="f3750-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into hello native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="f3750-148">toocreate en mesure de toobe ce message, nous devons parti tootake de C# [expressions de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx) dans Gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="f3750-148">toobe able toocreate this message we need tootake advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="f3750-149">Voici la stratégie hello qui envoie un tooAzure de message de demande HTTP concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="f3750-149">Here is hello policy which sends a HTTP request message tooAzure Event Hubs.</span></span>

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a><span data-ttu-id="f3750-150">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="f3750-150">Policy declaration</span></span>
<span data-ttu-id="f3750-151">Il y a quelques éléments particuliers à examiner sur cette expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="f3750-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="f3750-152">stratégie de journal à eventhub Hello possède un attribut appelé « id d’enregistreur d’événements qui fait référence nom toohello de journal qui a été créé dans le service de gestion des API de hello ».</span><span class="sxs-lookup"><span data-stu-id="f3750-152">hello log-to-eventhub policy has an attribute called logger-id which refers toohello name of logger that has been created within hello API Management service.</span></span> <span data-ttu-id="f3750-153">Hello les détails de la toosetup un enregistreur d’événements de concentrateur d’événements dans le service de gestion des API hello se trouvent dans les documents hello [comment toolog événements tooAzure Hubs d’événements dans la gestion des API Azure](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="f3750-153">hello details of how toosetup an Event Hub logger in hello API Management service can be found in hello document [How toolog events tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="f3750-154">attribut de deuxième Hello est un paramètre facultatif qui indique des messages hello partition toostore dans les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="f3750-154">hello second attribute is an optional parameter that instructs Event Hubs which partition toostore hello message in.</span></span> <span data-ttu-id="f3750-155">Concentrateurs d’événements utilisent des partitions tooenable expansion et nécessitent un minimum de deux.</span><span class="sxs-lookup"><span data-stu-id="f3750-155">Event Hubs use partitions tooenable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="f3750-156">Hello livraison chronologique des messages est garantie uniquement au sein d’une partition.</span><span class="sxs-lookup"><span data-stu-id="f3750-156">hello ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="f3750-157">Si nous ne pas demander à concentrateur d’événements dans le message de type hello tooplace partition, il utilise un algorithme round-robin toodistribute hello de charge.</span><span class="sxs-lookup"><span data-stu-id="f3750-157">If we do not instruct Event Hub in which partition tooplace hello message, it will use a round-robin algorithm toodistribute hello load.</span></span> <span data-ttu-id="f3750-158">Toutefois, qui peut entraîner certaines de nos toobe de messages traité dans le désordre.</span><span class="sxs-lookup"><span data-stu-id="f3750-158">However, that may cause some of our messages toobe processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="f3750-159">Partitions</span><span class="sxs-lookup"><span data-stu-id="f3750-159">Partitions</span></span>
<span data-ttu-id="f3750-160">tooensure nos messages sont remis tooconsumers dans l’ordre et tirer parti de la fonctionnalité de distribution de charge hello de partitions, j’ai choisi toosend HTTP demande messages tooone partitions et la deuxième partition HTTP réponse messages tooa.</span><span class="sxs-lookup"><span data-stu-id="f3750-160">tooensure our messages are delivered tooconsumers in order and take advantage of hello load distribution capability of partitions, I chose toosend HTTP request messages tooone partition and HTTP response messages tooa second partition.</span></span> <span data-ttu-id="f3750-161">Cela garantit une distribution régulière de charge et nous pouvons garantir que toutes les demandes seront consommées dans l’ordre, de même que toutes les réponses.</span><span class="sxs-lookup"><span data-stu-id="f3750-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="f3750-162">Il est possible pour un toobe réponse consommé avant la demande correspondante de hello, mais qui n’est pas un problème que nous avons un mécanisme différent pour la corrélation demande tooresponses et nous savons que les demandes sont toujours placés avant les réponses.</span><span class="sxs-lookup"><span data-stu-id="f3750-162">It is possible for a response toobe consumed before hello corresponding request, but as that is not a problem as we have a different mechanism for correlating requests tooresponses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="f3750-163">Charges utiles HTTP</span><span class="sxs-lookup"><span data-stu-id="f3750-163">HTTP payloads</span></span>
<span data-ttu-id="f3750-164">Après la génération de hello `requestLine` nous vérifions toosee si le corps de la demande hello doit être tronqué.</span><span class="sxs-lookup"><span data-stu-id="f3750-164">After building hello `requestLine` we check toosee if hello request body should be truncated.</span></span> <span data-ttu-id="f3750-165">corps de la demande Hello est tronquée tooonly 1024.</span><span class="sxs-lookup"><span data-stu-id="f3750-165">hello request body is truncated tooonly 1024.</span></span> <span data-ttu-id="f3750-166">Cela peut être augmentée, toutefois les messages individuels du concentrateur d’événements sont too256KB limitée, il est probable que certains HTTP corps ne tient ne pas dans un seul message.</span><span class="sxs-lookup"><span data-stu-id="f3750-166">This could be increased, however individual Event Hub messages are limited too256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="f3750-167">Lors de la journalisation et analytique une quantité importante d’informations peut être dérivé de simplement les en-têtes et de ligne de requête HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="f3750-167">When doing logging and analytics a significant amount of information can be derived from just hello HTTP request line and headers.</span></span> <span data-ttu-id="f3750-168">En outre, grand nombre de demandes API retourne uniquement les petits corps et perte hello de valeur des informations en tronquant corps volumineux est relativement minime réduction de toohello de comparaison de transfert, le traitement et stockage coûte tookeep tout le contenu du corps.</span><span class="sxs-lookup"><span data-stu-id="f3750-168">Also, many API requests only return small bodies and so hello loss of information value by truncating large bodies is fairly minimal in comparison toohello reduction in transfer, processing and storage costs tookeep all body contents.</span></span> <span data-ttu-id="f3750-169">Une dernière remarque sur le traitement hello corps est que nous devons toopass `true` toohello comme<string>(méthode) (), car nous lisons le contenu du corps de hello, mais elle était également que vous souhaitez hello principal API toobe tooread en mesure de hello corps.</span><span class="sxs-lookup"><span data-stu-id="f3750-169">One final note about processing hello body is that we need toopass `true` toohello As<string>() method because we are reading hello body contents, but was also want hello backend API toobe able tooread hello body.</span></span> <span data-ttu-id="f3750-170">En passant true toothis méthode nous entraîner hello toobe de corps mis en mémoire tampon afin qu’il puisse être lu une deuxième fois.</span><span class="sxs-lookup"><span data-stu-id="f3750-170">By passing true toothis method we cause hello body toobe buffered so that it can be read a second time.</span></span> <span data-ttu-id="f3750-171">Cela est important toobe prenant en charge de si vous avez une API qui ne le téléchargement de fichiers très volumineux ou d’utilise d’interrogation longue.</span><span class="sxs-lookup"><span data-stu-id="f3750-171">This is important toobe aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="f3750-172">Dans ce cas, il serait meilleures tooavoid lors de la lecture du corps de hello du tout.</span><span class="sxs-lookup"><span data-stu-id="f3750-172">In these cases it would be best tooavoid reading hello body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="f3750-173">En-têtes HTTP</span><span class="sxs-lookup"><span data-stu-id="f3750-173">HTTP headers</span></span>
<span data-ttu-id="f3750-174">En-têtes HTTP peuvent être simplement transférés sur dans le format de message hello sous forme de paire clé/valeur simple.</span><span class="sxs-lookup"><span data-stu-id="f3750-174">HTTP Headers can be simply transferred over into hello message format in a simple key/value pair format.</span></span> <span data-ttu-id="f3750-175">Nous avons choisi toostrip certaines sécurité champs sensibles, tooavoid inutilement une fuite d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="f3750-175">We have chosen toostrip out certain security sensitive fields, tooavoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="f3750-176">Il est peu probable que les clés d’API et les autres informations d’identification à utiliser à des fins d’analyse.</span><span class="sxs-lookup"><span data-stu-id="f3750-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="f3750-177">Si nous souhaitons toodo analyse sur l’utilisateur de hello et produit hello qu’ils utilisent, puis nous ne pouvons obtenir que de hello `context` de l’objet et ajouter ce message toohello.</span><span class="sxs-lookup"><span data-stu-id="f3750-177">If we wish toodo analysis on hello user and hello particular product they are using then we could get that from hello `context` object and add that toohello message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="f3750-178">Métadonnées de message</span><span class="sxs-lookup"><span data-stu-id="f3750-178">Message Metadata</span></span>
<span data-ttu-id="f3750-179">Lorsque vous créez un concentrateur d’événements hello achever message toosend toohello, hello première ligne n’est pas réellement partie de hello `application/http` message.</span><span class="sxs-lookup"><span data-stu-id="f3750-179">When building hello complete message toosend toohello event hub, hello first line is not actually part of hello `application/http` message.</span></span> <span data-ttu-id="f3750-180">Hello première ligne est composée de déterminer si le message de type hello est un message de demande ou de réponse des métadonnées supplémentaires et un id de message qui est utilisé toocorrelate demande tooresponses.</span><span class="sxs-lookup"><span data-stu-id="f3750-180">hello first line is additional metadata consisting of whether hello message is a request or response message and a message id which is used toocorrelate requests tooresponses.</span></span> <span data-ttu-id="f3750-181">id de message Hello est créé à l’aide d’une autre stratégie qui ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="f3750-181">hello message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="f3750-182">Message de demande hello, stocké dans une variable en tant que hello réponse a été retournée et ensuite simplement envoyée hello demande et réponse en tant qu’un seul message nous auraient pu être créées.</span><span class="sxs-lookup"><span data-stu-id="f3750-182">We could have created hello request message, stored that in a variable until hello response was returned and then simply sent hello request and response as a single message.</span></span> <span data-ttu-id="f3750-183">Toutefois, par envoi de réponse et une demande de hello indépendamment et à l’aide d’un toocorrelate d’id de message hello deux, nous obtenons un peu plus de souplesse dans la taille des messages hello, parti de tootake hello possibilité de plusieurs partitions, tout en conservant hello et l’ordre des messages demande s’affichera plus tôt dans notre tableau de bord de journalisation.</span><span class="sxs-lookup"><span data-stu-id="f3750-183">However, by sending hello request and response independently and using a message id toocorrelate hello two, we get a bit more flexibility in hello message size, hello ability tootake advantage of multiple partitions whilst maintaining message order and hello request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="f3750-184">Il peut également être certains scénarios où une réponse valide n’est jamais envoyée concentrateur d’événements toohello, probablement en raison de l’erreur de demande irrécupérable tooa dans le service de gestion des API hello, mais nous avons toujours aura un enregistrement de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="f3750-184">There also may be some scenarios where a valid response is never sent toohello event hub, possibly due tooa fatal request error in hello API Management service, but we still will have a record of hello request.</span></span>

<span data-ttu-id="f3750-185">message HTTP de la réponse Hello stratégie toosend hello semble très similaire toohello demande et donc hello terminer la configuration de la stratégie ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="f3750-185">hello policy toosend hello response HTTP message looks very similar toohello request and so hello complete policy configuration looks like this:</span></span>

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

<span data-ttu-id="f3750-186">Hello `set-variable` stratégie crée une valeur qui est accessible par les deux hello `log-to-eventhub` stratégie Bonjour `<inbound>` section et hello `<outbound>` section.</span><span class="sxs-lookup"><span data-stu-id="f3750-186">hello `set-variable` policy creates a value that is accessible by both hello `log-to-eventhub` policy in hello `<inbound>` section and hello `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="f3750-187">Réception d’événements de hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="f3750-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="f3750-188">Réception d’événements à partir du concentrateur d’événements Azure à l’aide de hello [protocole AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="f3750-188">Events from Azure Event Hub are received using hello [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="f3750-189">équipe de Microsoft Service Bus Hello apportées client hello toomake disponible de bibliothèques consommation d’événements plus faciles.</span><span class="sxs-lookup"><span data-stu-id="f3750-189">hello Microsoft Service Bus team have made client libraries available toomake hello consuming events easier.</span></span> <span data-ttu-id="f3750-190">Il existe deux approches différentes de prise en charge, un est en cours d’un *consommateur Direct* et hello autres à l’aide de hello `EventProcessorHost` classe.</span><span class="sxs-lookup"><span data-stu-id="f3750-190">There are two different approaches supported, one is being a *Direct Consumer* and hello other is using hello `EventProcessorHost` class.</span></span> <span data-ttu-id="f3750-191">Vous trouverez les exemples de ces deux approches Bonjour [Guide de programmation de concentrateurs d’événements](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="f3750-191">Examples of these two approaches can be found in hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="f3750-192">version abrégée de Hello des différences de hello est, `Direct Consumer` vous donne un contrôle complet et hello `EventProcessorHost` d’intervient hello plomberie pour vous mais entraîne certaines hypothèses concernant la façon dont vous allez traiter ces événements.</span><span class="sxs-lookup"><span data-stu-id="f3750-192">hello short version of hello differences is, `Direct Consumer` gives you complete control and hello `EventProcessorHost` does some of hello plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="f3750-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="f3750-193">EventProcessorHost</span></span>
<span data-ttu-id="f3750-194">Dans cet exemple, nous allons utiliser hello `EventProcessorHost` par souci de simplicité, cependant il ne peut pas hello meilleur choix pour ce scénario particulier.</span><span class="sxs-lookup"><span data-stu-id="f3750-194">In this sample, we will use hello `EventProcessorHost` for simplicity, however it may not hello best choice for this particular scenario.</span></span> <span data-ttu-id="f3750-195">`EventProcessorHost`hello travail de s’assurer que vous n’avez pas tooworry à propos du threading problèmes au sein de la classe du processeur un événement particulier.</span><span class="sxs-lookup"><span data-stu-id="f3750-195">`EventProcessorHost` does hello hard work of making sure you don't have tooworry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="f3750-196">Toutefois, dans notre scénario, nous allons simplement convertir le format de tooanother message hello et en lui passant le long de service tooanother à l’aide d’une méthode async.</span><span class="sxs-lookup"><span data-stu-id="f3750-196">However, in our scenario, we are simply converting hello message tooanother format and passing it along tooanother service using an async method.</span></span> <span data-ttu-id="f3750-197">Il est inutile de mettre à jour l’état partagé et par conséquent, il n’y a aucun risque de problème lié aux threads.</span><span class="sxs-lookup"><span data-stu-id="f3750-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="f3750-198">La plupart des scénarios, `EventProcessorHost` est probablement hello meilleure option et il est certainement option plus facile de hello.</span><span class="sxs-lookup"><span data-stu-id="f3750-198">For most scenarios, `EventProcessorHost` is probably hello best choice and it is certainly hello easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="f3750-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="f3750-199">IEventProcessor</span></span>
<span data-ttu-id="f3750-200">concept de central Hello lors de l’utilisation `EventProcessorHost` toocreate n’est une implémentation de hello `IEventProcessor` interface qui contient la méthode hello `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="f3750-200">hello central concept when using `EventProcessorHost` is toocreate a an implementation of hello `IEventProcessor` interface which contains hello method `ProcessEventAsync`.</span></span> <span data-ttu-id="f3750-201">essentiellement Hello, cette méthode est illustrée ici :</span><span class="sxs-lookup"><span data-stu-id="f3750-201">hello essence of that method is shown here:</span></span>

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

<span data-ttu-id="f3750-202">Une liste d’objets de EventData sont passés à la méthode hello et nous itérer sur cette liste.</span><span class="sxs-lookup"><span data-stu-id="f3750-202">A list of EventData objects are passed into hello method and we iterate over that list.</span></span> <span data-ttu-id="f3750-203">octets Hello de chaque méthode sont analysées dans un objet HttpMessage et instance de tooan de IHttpMessageProcessor est passé à cet objet.</span><span class="sxs-lookup"><span data-stu-id="f3750-203">hello bytes of each method are parsed into a HttpMessage object and that object is passed tooan instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="f3750-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="f3750-204">HttpMessage</span></span>
<span data-ttu-id="f3750-205">Hello `HttpMessage` instance contient trois éléments de données :</span><span class="sxs-lookup"><span data-stu-id="f3750-205">hello `HttpMessage` instance contains three pieces of data:</span></span>

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

<span data-ttu-id="f3750-206">Hello `HttpMessage` instance contient un `MessageId` GUID qui nous permet de demande de hello HTTP tooconnect toohello les réponses HTTP correspondant et une valeur booléenne de valeur qui identifie si l’objet de hello contient une instance d’un élément HttpRequestMessage et HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="f3750-206">hello `HttpMessage` instance contains a `MessageId` GUID that allows us tooconnect hello HTTP request toohello corresponding HTTP response and a boolean value that identifies if hello object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="f3750-207">À l’aide de hello générée dans les classes HTTP à partir de `System.Net.Http`, j’ai parti tootake en mesure de hello `application/http` l’analyse du code qui est inclus dans `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="f3750-207">By using hello built in HTTP classes from `System.Net.Http`, I was able tootake advantage of hello `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="f3750-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="f3750-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="f3750-209">Hello `HttpMessage` instance est ensuite transférée tooimplementation de `IHttpMessageProcessor` qui est une interface que j’ai créé la réception toodecouple hello et l’interprétation des événements de hello de concentrateur d’événements Azure et hello réelle du traitement de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="f3750-209">hello `HttpMessage` instance is then forwarded tooimplementation of `IHttpMessageProcessor` which is an interface I created toodecouple hello receiving and interpretation of hello event from Azure Event Hub and hello actual processing of it.</span></span>

## <a name="forwarding-hello-http-message"></a><span data-ttu-id="f3750-210">Transfert du message HTTP hello</span><span class="sxs-lookup"><span data-stu-id="f3750-210">Forwarding hello HTTP message</span></span>
<span data-ttu-id="f3750-211">J’ai décidé de cet exemple, il serait intéressant toopush hello requête HTTP sur trop[Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="f3750-211">For this sample, I decided it would be interesting toopush hello HTTP Request over too[Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="f3750-212">Runscope est un service cloud qui se spécialise dans le débogage HTTP, la journalisation et la surveillance.</span><span class="sxs-lookup"><span data-stu-id="f3750-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="f3750-213">Ils ont un niveau gratuit, il est donc facile tootry et il permet les requêtes HTTP toosee hello pour le flux en temps réel via notre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f3750-213">They have a free tier, so it is easy tootry and it allows us toosee hello HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="f3750-214">Hello `IHttpMessageProcessor` implémentation ressemble à ceci,</span><span class="sxs-lookup"><span data-stu-id="f3750-214">hello `IHttpMessageProcessor` implementation looks like this,</span></span>

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

<span data-ttu-id="f3750-215">J’ai parti tootake en mesure d’une [bibliothèque client existant pour Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) qui la rendent facile toopush `HttpRequestMessage` et `HttpResponseMessage` instances dans leur service.</span><span class="sxs-lookup"><span data-stu-id="f3750-215">I was able tootake advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy toopush `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="f3750-216">Dans l’ordre tooaccess hello API Runscope avoir un compte et une clé d’API.</span><span class="sxs-lookup"><span data-stu-id="f3750-216">In order tooaccess hello Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="f3750-217">Vous trouverez les instructions pour obtenir une clé API Bonjour [tooAccess de création d’Applications Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) capture.</span><span class="sxs-lookup"><span data-stu-id="f3750-217">Instructions for getting an API key can be found in hello [Creating Applications tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="f3750-218">Exemple complet</span><span class="sxs-lookup"><span data-stu-id="f3750-218">Complete sample</span></span>
<span data-ttu-id="f3750-219">Hello [code source](https://github.com/darrelmiller/ApimEventProcessor) et tests pour l’exemple hello se trouvent sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f3750-219">hello [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for hello sample are on GitHub.</span></span> <span data-ttu-id="f3750-220">Vous devez une [Service Gestion des API](api-management-get-started.md), [un Hub d’événements connecté](api-management-howto-log-event-hubs.md)et un [compte de stockage](../storage/common/storage-create-storage-account.md) toorun hello exemple par vous-même.</span><span class="sxs-lookup"><span data-stu-id="f3750-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) toorun hello sample for yourself.</span></span>   

<span data-ttu-id="f3750-221">exemple Hello est simplement une application Console simple qui écoute les événements provenant de concentrateur d’événements, les convertit en un `HttpRequestMessage` et `HttpResponseMessage` objets, puis transfère les toohello Runscope API.</span><span class="sxs-lookup"><span data-stu-id="f3750-221">hello sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on toohello Runscope API.</span></span>

<span data-ttu-id="f3750-222">Bonjour suivant image animée, vous pouvez voir une demande effectuée tooan API Bonjour portail des développeurs, hello Console application affichant hello, le message en cours traitée et transférées et puis hello demande et réponse s’affiche dans hello Runscope trafic inspecteur.</span><span class="sxs-lookup"><span data-stu-id="f3750-222">In hello following animated image, you can see a request being made tooan API in hello Developer Portal, hello Console application showing hello message being received, processed and forwarded and then hello request and response showing up in hello Runscope Traffic inspector.</span></span>

![Démonstration de la demande de transfert tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="f3750-224">Résumé</span><span class="sxs-lookup"><span data-stu-id="f3750-224">Summary</span></span>
<span data-ttu-id="f3750-225">Service de gestion des API Azure fournit un outil idéal toocapture hello HTTP du trafic se déplaçant dans tooand à partir de votre API.</span><span class="sxs-lookup"><span data-stu-id="f3750-225">Azure API Management service provides an ideal place toocapture hello HTTP traffic travelling tooand from your APIs.</span></span> <span data-ttu-id="f3750-226">Azure Event Hubs est une solution pouvant être mise à l’échelle et économique de capturer le trafic et de l’intégrer à des systèmes de traitement secondaire pour la journalisation, la surveillance et d’autres analyses sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="f3750-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="f3750-227">Connexion des systèmes comme Runscope est un simple en tant que quelques douzaines de lignes de code de surveillance du trafic d’une partie de too3rd.</span><span class="sxs-lookup"><span data-stu-id="f3750-227">Connecting too3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3750-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3750-228">Next steps</span></span>
* <span data-ttu-id="f3750-229">En savoir plus sur Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f3750-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="f3750-230">Prise en main avec Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f3750-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="f3750-231">Réception de messages avec EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="f3750-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="f3750-232">Guide de programmation Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f3750-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="f3750-233">En savoir plus sur l’intégration de Gestion des API et Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f3750-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="f3750-234">Comment toolog événements tooAzure Hubs d’événements dans la gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="f3750-234">How toolog events tooAzure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="f3750-235">Référence d’entité d’enregistreur</span><span class="sxs-lookup"><span data-stu-id="f3750-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="f3750-236">Référence de stratégie log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="f3750-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
