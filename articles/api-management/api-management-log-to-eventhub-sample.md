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
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a>Surveiller vos API avec gestion des API Azure, les hubs d’événements et Runscope
Hello [service de gestion des API](api-management-key-concepts.md) fournit de nombreuses fonctionnalités tooenhance hello le traitement des demandes envoyées de HTTP tooyour API HTTP. Toutefois, hello existence de hello demandes et réponses sont temporaires. Hello est demandé et il transite par hello gestion des API service tooyour API de service principal. Votre API traite la demande de hello et une réponse transite par le biais de toohello API consommateur. Hello service de gestion des API conserve des statistiques importantes concernant hello API pour l’affichage dans le tableau de bord de portail de Publisher hello, mais, les détails de hello ont disparu.

À l’aide de hello [journal à eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [stratégie](api-management-howto-policies.md) Bonjour service de gestion des API, vous pouvez envoyer des détails à partir de tooan de demande et de réponse hello [concentrateur d’événements Azure](../event-hubs/event-hubs-what-is-event-hubs.md). Il existe de nombreuses raisons pour lesquelles vous souhaiterez peut-être toogenerate des événements à partir de messages HTTP envoyés tooyour API. Certains exemples incluent une piste d’audit des mises à jour, une analyse des usages, une alerte en cas d’exception et l’intégration de tiers.   

Cet article montre comment les toocapture hello HTTP demande et réponse message entier, envoyer tooan concentrateur d’événements et de relais ensuite ce service de tiers tooa message qui fournit la journalisation et analyse des services HTTP.

## <a name="why-send-from-api-management-service"></a>Pourquoi effectuer l’envoi depuis un service de gestion d’API ?
Il est possible de toowrite HTTP intergiciel (middleware) qui peut s’intégrer à l’API HTTP infrastructures toocapture demandes et réponses HTTP et les flux dans l’analyse des systèmes et de journalisation. Hello inconvénient toothis consiste intergiciel (middleware) de hello HTTP doit toobe intégré dans les API de service principal hello et doit correspondre à la plateforme hello de hello API. S’il existe plusieurs API chacun d’eux doit déployer hello intergiciel (middleware). Il existe souvent des raisons pour lesquelles les API de serveur principal ne peuvent pas être mises à jour.

À l’aide de toointegrate de service de gestion des API Azure hello avec l’infrastructure de journalisation fournit une solution centralisée et indépendante de la plate-forme. Il est également évolutif en partie toohello [géo-réplication](api-management-howto-deploy-multi-region.md) fonctionnalités de gestion des API Azure.

## <a name="why-send-tooan-azure-event-hub"></a>Pourquoi envoyer tooan concentrateur d’événements Azure ?
Il s’agit d’un tooask raisonnable, pourquoi créer une stratégie de concentrateurs d’événements tooAzure spécifique ? Il existe de nombreux emplacements distincts et où je souhaite avoir toolog mes demandes. Pourquoi ne pas envoyer hello demande directement toohello sa destination finale ?  C’est une option. Toutefois, lors de la journalisation des requêtes à partir d’un service de gestion des API, il est nécessaire tooconsider comment des messages de journalisation aura un impact sur les performances hello Hello API. L’augmentation progressive de charge peut être traitées par l’augmentation du nombre d’instances disponibles de composants système ou par le biais de la géo-réplication. Toutefois, courts pics de trafic peuvent entraîner des toobe demandes considérablement retardé si le démarrage de l’infrastructure de toologging demandes tooslow sous charge.

Hello Azure Event Hubs est conçue tooingress très grands volumes de données, avec une capacité de traitement avec un nombre beaucoup plus élevé d’événements que nombre hello du serveur proxy demande la plupart des processus d’API. Hello concentrateur d’événements agit comme un type de tampon sophistiqué entre votre infrastructure de gestion API service et hello qui devront stocker et traiter les messages de type hello. Cela garantit que les performances de votre API ne seront pas affectées en raison de l’infrastructure d’enregistrement toohello.  

Une fois que les données de salutation a été passées tooan concentrateur d’événements, il est conservé et attendra tooprocess des consommateurs de concentrateur d’événements qu’il. Hello concentrateur d’événements ne soucie pas du mode de traitement, il reconnaît uniquement sur l’établissement de message de type hello soient correctement remis.     

Concentrateurs d’événements ont des groupes de consommateurs toomultiple hello capacité toostream événements. Cela permet de toobe événements traité par les systèmes complètement différents. Cela permet la prise en charge de nombreux scénarios d’intégration sans avoir à insérer des retards d’ajout sur hello du traitement de la demande d’API hello au sein du service de gestion des API hello qu’un seul événement besoins toobe généré.

## <a name="a-policy-toosend-applicationhttp-messages"></a>Une stratégie toosend application/http les messages
Un hub d’événements accepte des données d’événement en tant que chaîne simple. Hello contenu de cette chaîne est complètement les tooyou. toopackage en mesure de toobe jusqu'à une requête HTTP et envoyer tooEvent concentrateurs, nous avons besoin de chaîne de hello tooformat avec les informations de demande ou réponse hello. Dans de tels cas, s’il existe un format existant, que nous pouvons réutiliser, puis nous pouvons inutile toowrite notre propre à l’analyse de code. Initialement, j’envisagé à l’aide de hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) pour l’envoi de demandes et réponses HTTP. Cependant, ce format est optimisé pour stocker une séquence de requêtes HTTP dans un format basé sur JSON. Elle contenait un nombre d’éléments obligatoires qui a ajouté une complexité inutile pour le scénario hello du passage d’un message de type hello HTTP acheminement hello.  

Une autre option a été toouse hello `application/http` type de média comme décrit dans la spécification de hello HTTP [RFC 7230](http://tools.ietf.org/html/rfc7230). Ce type de média utilise hello exacte dans le même format qui est utilisé tooactually envoyer des messages HTTP acheminement hello, mais la totalité du message hello peut être placé dans le corps de hello d’une autre demande HTTP. Dans notre cas, nous allons corps de hello toouse en tant que notre tooEvent de toosend message concentrateurs. Pour des raisons pratiques, est un analyseur qui existe dans [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliothèques qui peuvent analyser ce format et le convertir en hello natif `HttpRequestMessage` et `HttpResponseMessage` objets.

toocreate en mesure de toobe ce message, nous devons parti tootake de C# [expressions de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx) dans Gestion des API Azure. Voici la stratégie hello qui envoie un tooAzure de message de demande HTTP concentrateurs d’événements.

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

### <a name="policy-declaration"></a>Déclaration de stratégie
Il y a quelques éléments particuliers à examiner sur cette expression de stratégie. stratégie de journal à eventhub Hello possède un attribut appelé « id d’enregistreur d’événements qui fait référence nom toohello de journal qui a été créé dans le service de gestion des API de hello ». Hello les détails de la toosetup un enregistreur d’événements de concentrateur d’événements dans le service de gestion des API hello se trouvent dans les documents hello [comment toolog événements tooAzure Hubs d’événements dans la gestion des API Azure](api-management-howto-log-event-hubs.md). attribut de deuxième Hello est un paramètre facultatif qui indique des messages hello partition toostore dans les concentrateurs d’événements. Concentrateurs d’événements utilisent des partitions tooenable expansion et nécessitent un minimum de deux. Hello livraison chronologique des messages est garantie uniquement au sein d’une partition. Si nous ne pas demander à concentrateur d’événements dans le message de type hello tooplace partition, il utilise un algorithme round-robin toodistribute hello de charge. Toutefois, qui peut entraîner certaines de nos toobe de messages traité dans le désordre.  

### <a name="partitions"></a>Partitions
tooensure nos messages sont remis tooconsumers dans l’ordre et tirer parti de la fonctionnalité de distribution de charge hello de partitions, j’ai choisi toosend HTTP demande messages tooone partitions et la deuxième partition HTTP réponse messages tooa. Cela garantit une distribution régulière de charge et nous pouvons garantir que toutes les demandes seront consommées dans l’ordre, de même que toutes les réponses. Il est possible pour un toobe réponse consommé avant la demande correspondante de hello, mais qui n’est pas un problème que nous avons un mécanisme différent pour la corrélation demande tooresponses et nous savons que les demandes sont toujours placés avant les réponses.

### <a name="http-payloads"></a>Charges utiles HTTP
Après la génération de hello `requestLine` nous vérifions toosee si le corps de la demande hello doit être tronqué. corps de la demande Hello est tronquée tooonly 1024. Cela peut être augmentée, toutefois les messages individuels du concentrateur d’événements sont too256KB limitée, il est probable que certains HTTP corps ne tient ne pas dans un seul message. Lors de la journalisation et analytique une quantité importante d’informations peut être dérivé de simplement les en-têtes et de ligne de requête HTTP hello. En outre, grand nombre de demandes API retourne uniquement les petits corps et perte hello de valeur des informations en tronquant corps volumineux est relativement minime réduction de toohello de comparaison de transfert, le traitement et stockage coûte tookeep tout le contenu du corps. Une dernière remarque sur le traitement hello corps est que nous devons toopass `true` toohello comme<string>(méthode) (), car nous lisons le contenu du corps de hello, mais elle était également que vous souhaitez hello principal API toobe tooread en mesure de hello corps. En passant true toothis méthode nous entraîner hello toobe de corps mis en mémoire tampon afin qu’il puisse être lu une deuxième fois. Cela est important toobe prenant en charge de si vous avez une API qui ne le téléchargement de fichiers très volumineux ou d’utilise d’interrogation longue. Dans ce cas, il serait meilleures tooavoid lors de la lecture du corps de hello du tout.   

### <a name="http-headers"></a>En-têtes HTTP
En-têtes HTTP peuvent être simplement transférés sur dans le format de message hello sous forme de paire clé/valeur simple. Nous avons choisi toostrip certaines sécurité champs sensibles, tooavoid inutilement une fuite d’informations d’identification. Il est peu probable que les clés d’API et les autres informations d’identification à utiliser à des fins d’analyse. Si nous souhaitons toodo analyse sur l’utilisateur de hello et produit hello qu’ils utilisent, puis nous ne pouvons obtenir que de hello `context` de l’objet et ajouter ce message toohello.     

### <a name="message-metadata"></a>Métadonnées de message
Lorsque vous créez un concentrateur d’événements hello achever message toosend toohello, hello première ligne n’est pas réellement partie de hello `application/http` message. Hello première ligne est composée de déterminer si le message de type hello est un message de demande ou de réponse des métadonnées supplémentaires et un id de message qui est utilisé toocorrelate demande tooresponses. id de message Hello est créé à l’aide d’une autre stratégie qui ressemble à ceci :

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

Message de demande hello, stocké dans une variable en tant que hello réponse a été retournée et ensuite simplement envoyée hello demande et réponse en tant qu’un seul message nous auraient pu être créées. Toutefois, par envoi de réponse et une demande de hello indépendamment et à l’aide d’un toocorrelate d’id de message hello deux, nous obtenons un peu plus de souplesse dans la taille des messages hello, parti de tootake hello possibilité de plusieurs partitions, tout en conservant hello et l’ordre des messages demande s’affichera plus tôt dans notre tableau de bord de journalisation. Il peut également être certains scénarios où une réponse valide n’est jamais envoyée concentrateur d’événements toohello, probablement en raison de l’erreur de demande irrécupérable tooa dans le service de gestion des API hello, mais nous avons toujours aura un enregistrement de demande de hello.

message HTTP de la réponse Hello stratégie toosend hello semble très similaire toohello demande et donc hello terminer la configuration de la stratégie ressemble à ceci :

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

Hello `set-variable` stratégie crée une valeur qui est accessible par les deux hello `log-to-eventhub` stratégie Bonjour `<inbound>` section et hello `<outbound>` section.  

## <a name="receiving-events-from-event-hubs"></a>Réception d’événements de hubs d’événements
Réception d’événements à partir du concentrateur d’événements Azure à l’aide de hello [protocole AMQP](http://www.amqp.org/). équipe de Microsoft Service Bus Hello apportées client hello toomake disponible de bibliothèques consommation d’événements plus faciles. Il existe deux approches différentes de prise en charge, un est en cours d’un *consommateur Direct* et hello autres à l’aide de hello `EventProcessorHost` classe. Vous trouverez les exemples de ces deux approches Bonjour [Guide de programmation de concentrateurs d’événements](../event-hubs/event-hubs-programming-guide.md). version abrégée de Hello des différences de hello est, `Direct Consumer` vous donne un contrôle complet et hello `EventProcessorHost` d’intervient hello plomberie pour vous mais entraîne certaines hypothèses concernant la façon dont vous allez traiter ces événements.  

### <a name="eventprocessorhost"></a>EventProcessorHost
Dans cet exemple, nous allons utiliser hello `EventProcessorHost` par souci de simplicité, cependant il ne peut pas hello meilleur choix pour ce scénario particulier. `EventProcessorHost`hello travail de s’assurer que vous n’avez pas tooworry à propos du threading problèmes au sein de la classe du processeur un événement particulier. Toutefois, dans notre scénario, nous allons simplement convertir le format de tooanother message hello et en lui passant le long de service tooanother à l’aide d’une méthode async. Il est inutile de mettre à jour l’état partagé et par conséquent, il n’y a aucun risque de problème lié aux threads. La plupart des scénarios, `EventProcessorHost` est probablement hello meilleure option et il est certainement option plus facile de hello.     

### <a name="ieventprocessor"></a>IEventProcessor
concept de central Hello lors de l’utilisation `EventProcessorHost` toocreate n’est une implémentation de hello `IEventProcessor` interface qui contient la méthode hello `ProcessEventAsync`. essentiellement Hello, cette méthode est illustrée ici :

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

Une liste d’objets de EventData sont passés à la méthode hello et nous itérer sur cette liste. octets Hello de chaque méthode sont analysées dans un objet HttpMessage et instance de tooan de IHttpMessageProcessor est passé à cet objet.

### <a name="httpmessage"></a>HttpMessage
Hello `HttpMessage` instance contient trois éléments de données :

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

Hello `HttpMessage` instance contient un `MessageId` GUID qui nous permet de demande de hello HTTP tooconnect toohello les réponses HTTP correspondant et une valeur booléenne de valeur qui identifie si l’objet de hello contient une instance d’un élément HttpRequestMessage et HttpResponseMessage. À l’aide de hello générée dans les classes HTTP à partir de `System.Net.Http`, j’ai parti tootake en mesure de hello `application/http` l’analyse du code qui est inclus dans `System.Net.Http.Formatting`.  

### <a name="ihttpmessageprocessor"></a>IHttpMessageProcessor
Hello `HttpMessage` instance est ensuite transférée tooimplementation de `IHttpMessageProcessor` qui est une interface que j’ai créé la réception toodecouple hello et l’interprétation des événements de hello de concentrateur d’événements Azure et hello réelle du traitement de celui-ci.

## <a name="forwarding-hello-http-message"></a>Transfert du message HTTP hello
J’ai décidé de cet exemple, il serait intéressant toopush hello requête HTTP sur trop[Runscope](http://www.runscope.com). Runscope est un service cloud qui se spécialise dans le débogage HTTP, la journalisation et la surveillance. Ils ont un niveau gratuit, il est donc facile tootry et il permet les requêtes HTTP toosee hello pour le flux en temps réel via notre service de gestion des API.

Hello `IHttpMessageProcessor` implémentation ressemble à ceci,

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

J’ai parti tootake en mesure d’une [bibliothèque client existant pour Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) qui la rendent facile toopush `HttpRequestMessage` et `HttpResponseMessage` instances dans leur service. Dans l’ordre tooaccess hello API Runscope avoir un compte et une clé d’API. Vous trouverez les instructions pour obtenir une clé API Bonjour [tooAccess de création d’Applications Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) capture.

## <a name="complete-sample"></a>Exemple complet
Hello [code source](https://github.com/darrelmiller/ApimEventProcessor) et tests pour l’exemple hello se trouvent sur GitHub. Vous devez une [Service Gestion des API](api-management-get-started.md), [un Hub d’événements connecté](api-management-howto-log-event-hubs.md)et un [compte de stockage](../storage/common/storage-create-storage-account.md) toorun hello exemple par vous-même.   

exemple Hello est simplement une application Console simple qui écoute les événements provenant de concentrateur d’événements, les convertit en un `HttpRequestMessage` et `HttpResponseMessage` objets, puis transfère les toohello Runscope API.

Bonjour suivant image animée, vous pouvez voir une demande effectuée tooan API Bonjour portail des développeurs, hello Console application affichant hello, le message en cours traitée et transférées et puis hello demande et réponse s’affiche dans hello Runscope trafic inspecteur.

![Démonstration de la demande de transfert tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a>Résumé
Service de gestion des API Azure fournit un outil idéal toocapture hello HTTP du trafic se déplaçant dans tooand à partir de votre API. Azure Event Hubs est une solution pouvant être mise à l’échelle et économique de capturer le trafic et de l’intégrer à des systèmes de traitement secondaire pour la journalisation, la surveillance et d’autres analyses sophistiquées. Connexion des systèmes comme Runscope est un simple en tant que quelques douzaines de lignes de code de surveillance du trafic d’une partie de too3rd.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur Azure Event Hubs
  * [Prise en main avec Azure Event Hubs](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Réception de messages avec EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Guide de programmation Event Hubs](../event-hubs/event-hubs-programming-guide.md)
* En savoir plus sur l’intégration de Gestion des API et Event Hubs
  * [Comment toolog événements tooAzure Hubs d’événements dans la gestion des API Azure](api-management-howto-log-event-hubs.md)
  * [Référence d’entité d’enregistreur](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [Référence de stratégie log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
