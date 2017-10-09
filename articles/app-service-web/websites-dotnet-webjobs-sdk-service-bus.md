---
title: aaaHow toouse Azure Service Bus avec hello WebJobs SDK
description: "Découvrez comment les files d’attente du Bus des services Azure toouse et des rubriques avec hello WebJobs SDK."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>Comment toouse Azure Service Bus avec hello WebJobs SDK
## <a name="overview"></a>Vue d'ensemble
Ce guide fournit des c# des exemples de code qui montrent comment tootrigger un processus lors de la réception d’un message d’Azure Service Bus. utilisation des exemples de code de Hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.

guide de Hello suppose que vous connaissez [comment toocreate un projet de la tâche Web dans Visual Studio avec connexion chaînes ce compte de stockage point tooyour](websites-dotnet-webjobs-sdk-get-started.md).

extraits de code Hello affichent uniquement les fonctions, ne Hello pas de code qui crée hello `JobHost` objet comme dans cet exemple :

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

A [exemple de code complet Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) est dans le référentiel de tâches Web azure-exemples sdk hello sur GitHub.com.

## <a id="prerequisites"></a> Conditions préalables
toowork avec Service Bus vous avez tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package en outre toohello autres packages WebJobs SDK. 

Vous avez également la chaîne de connexion AzureWebJobsServiceBus tooset hello dans les chaînes de connexion de stockage toohello Ajout.  Cela Bonjour `connectionStrings` section du fichier App.config de hello, comme indiqué dans hello l’exemple suivant :

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Pour un exemple de projet qui inclut un paramètre de chaîne de connexion de Service Bus hello dans le fichier App.config hello, consultez [exemple de Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

chaînes de connexion Hello peuvent également être définies dans l’environnement d’exécution Azure hello, qui remplace ensuite les paramètres App.config hello lorsque hello la tâche Web s’exécute dans Azure. Pour plus d’informations, consultez [prise en main hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Comment tootrigger une fonction quand un Bus de Service de file d’attente de message est reçu
toowrite une fonction qui hello WebJobs SDK appelle lors de la réception d’un message de la file d’attente, utilisez hello `ServiceBusTrigger` attribut. constructeur d’attribut Hello prend un paramètre qui spécifie le nom hello de toopoll de file d’attente hello.

### <a name="how-servicebustrigger-works"></a>Fonctionnement de ServiceBusTrigger
Kit de développement logiciel Hello reçoit un message dans `PeekLock` mode et les appels `Complete` sur le message de type hello si hello est terminée avec succès, ou des appels `Abandon` si hello fonction échoue. Si la fonction hello s’exécute plus longtemps que hello `PeekLock` délai d’attente, les verrous hello est automatiquement renouvelée.

Bus de service effectue sa propre gestion de la file d’attente de messages incohérents qui ne peut pas être contrôlée ou configurée par hello WebJobs SDK. 

### <a name="string-queue-message"></a>Message de file d’attente de chaîne
Hello exemple de code suivant lit un message de la file d’attente qui contient une chaîne et écrit la chaîne de hello toohello du tableau de bord WebJobs SDK.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Remarque :** si vous créez hello messages de la file d’attente dans une application qui n’utilise pas hello WebJobs SDK, assurez-vous que tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) trop « text/plain ».

### <a name="poco-queue-message"></a>Message de file d’attente POCO
Hello SDK désérialise automatiquement un message de la file d’attente contenant du texte JSON pour un POCO [(objet CLR simple](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type. Hello exemple de code suivant lit un message de la file d’attente qui contient un `BlobInformation` objet qui a un `BlobName` propriété :

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Pour obtenir des exemples de code montrant comment les propriétés de toouse de toowork POCO hello avec les objets BLOB et tables dans hello même fonction, consultez hello [version de files d’attente de stockage de cet article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Si votre code qui crée le message de file d’attente hello n’utilise pas hello WebJobs SDK, utilisez toohello similaire de code exemple suivant :

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Types utilisés par ServiceBusTrigger
En outre `string` et types POCO, vous pouvez utiliser hello `ServiceBusTrigger` attribut avec un tableau d’octets ou un `BrokeredMessage` objet.

## <a id="create"></a>Comment toocreate Bus de Service de file d’attente des messages
une fonction qui crée un nouveau message de file d’attente de toowrite utiliser hello `ServiceBus` d’attribut et passez dans le constructeur d’attribut toohello nom hello file d’attente. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Création d’un message de file d’attente unique dans une fonction non asynchrone
Hello suivant l’exemple de code utilise un toocreate de paramètre de sortie un nouveau message dans la file d’attente hello nommé « outputqueue » avec hello même contenu en tant que hello message reçu dans la file d’attente hello nommé « inputqueue ».

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

le paramètre de sortie Hello pour la création d’un message de la file d’attente unique peut être un des types suivants de hello :

* `string`
* `byte[]`
* `BrokeredMessage`
* Type POCO sérialisable que vous définissez. Sérialisé automatiquement au format JSON.

Pour les paramètres de type POCO, un message de la file d’attente est toujours créé lors de la fonction hello se termine. Si le paramètre hello est null, hello SDK crée un message de la file d’attente qui retourne la valeur null lorsque le message de type hello est reçu et désérialisé. Pour hello autres types, si le paramètre hello est null aucun message de la file d’attente n’est créée.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Création de plusieurs messages de file d’attente dans des fonctions asynchrones
toocreate plusieurs messages, utilisez hello `ServiceBus` d’attribut avec `ICollector<T>` ou `IAsyncCollector<T>`, comme indiqué dans hello suivant l’exemple de code :

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Chaque message de la file d’attente est créée immédiatement lorsque hello `Add` méthode est appelée.

## <a id="topics"></a>Comment toowork avec des rubriques Service Bus
toowrite une fonction qui hello du Kit de développement appelle lorsqu’un message est reçu sur une rubrique Service Bus, utilisez hello `ServiceBusTrigger` attribut avec constructeur hello qui prend le nom de la rubrique et le nom d’abonnement, comme indiqué dans hello suivant l’exemple de code :

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

toocreate un message à une rubrique, utilisez hello `ServiceBus` d’attribut avec un Bonjour de nom de rubrique même façon que vous l’utilisez avec un nom de file d’attente.

## <a name="features-added-in-release-11"></a>Fonctionnalités ajoutées dans la version 1.1
Hello suivant les fonctionnalités ont été ajoutée dans la version 1.1 :

* Autoriser la personnalisation complète du traitement des messages via `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`prend en charge la personnalisation de hello Service Bus `MessagingFactory` et `NamespaceManager`.
* A `MessageProcessor` modèle de stratégie vous permet de toospecify un processeur par file d’attente/rubrique.
* L'accès concurrentiel de traitement des message est pris en charge par défaut. 
* Personnalisation facile de `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.
* Autoriser [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe spécifié sur `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (pour les scénarios où vous ne disposez pas gérer les droits). Notez que les tâches Web Azure est files d’attente d’inexistant tooautomatically Impossible de configurer et de rubriques sans AccessRights de gérer.

## <a id="queues"></a>Rubriques connexes couvertes par les files d’attente de stockage hello procédure-tooarticle
Pour plus d’informations sur les scénarios de WebJobs SDK tooService non spécifique des Bus, consultez [comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Les sujets abordés dans cet article hello suivants :

* Fonctions asynchrones
* Instances multiples
* Arrêt approprié
* Utiliser les attributs de WebJobs SDK dans le corps d’une fonction de hello
* Définir des chaînes de connexion du Kit de développement logiciel hello dans le code
* Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code
* Déclenchement manuel d’une fonction
* Écriture de journaux

## <a id="nextsteps"></a> Étapes suivantes
Ce guide a fourni le code des exemples qui montrent comment toohandle des scénarios courants pour l’utilisation avec Azure Service Bus. Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [Azure WebJobs recommandé de ressources](http://go.microsoft.com/fwlink/?linkid=390226).

