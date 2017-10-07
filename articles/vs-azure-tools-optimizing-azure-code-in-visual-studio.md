---
title: aaaOptimizing votre Azure de code dans Visual Studio | Documents Microsoft
description: "Découvrez comment les outils d'optimisation du code Azure dans Visual Studio peuvent rendre votre code plus robuste et plus performant."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>Optimisation de votre code Azure
Quand vous programmez des applications qui utilisent Microsoft Azure, il existe certaines pratiques de codage que vous devez suivre toohelp éviter les problèmes d’évolutivité de l’application, les comportements et les performances dans un environnement de cloud. Microsoft fournit un outil Azure Code Analysis, qui reconnaît et identifie plusieurs des problèmes couramment rencontrés et qui vous aide à les résoudre. Vous pouvez télécharger l’outil hello dans Visual Studio via NuGet.

## <a name="azure-code-analysis-rules"></a>Règles d’Azure Code Analysis
outil d’analyse du Code Azure Hello utilise hello suivant les règles tooautomatically indicateur votre code lorsqu’il détecte des performances en évitant les problèmes connus. Les problèmes détectés apparaissent sous la forme d’avertissements ou d’erreurs du compilateur. Code corrections ou suggestions tooresolve hello avertissement ou erreur sont souvent fournis via une icône d’ampoule.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Évitez d'utiliser le mode d'état de session (in-process) par défaut
### <a name="id"></a>ID
AP0000

### <a name="description"></a>Description
Si vous utilisez le mode d’état de session (in-process) par défaut hello pour les applications cloud, vous risquez de perdre l’état de session.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Par défaut, le mode d’état de session hello spécifié dans le fichier web.config de hello est in-process. En outre, si aucune entrée n’est spécifiée dans le fichier de configuration hello, mode d’état de Session hello par défaut tooin-process. mode de Hello in-process stocke l’état de session en mémoire sur le serveur web de hello. Lorsqu’une instance est redémarrée ou une nouvelle instance est utilisée pour l’équilibrage de charge ou de la prise en charge du basculement, l’état de session stockée en mémoire sur le serveur web de hello hello n’est pas enregistré. Cette situation empêche l’application hello évolutivité de sur le cloud de hello.

L’état de session ASP.NET prend en charge plusieurs options de stockage différentes pour les données d’état de session : InProc, StateServer, SQLServer, personnalisée et désactivée. Il est recommandé que vous utiliserez personnalisé en mode toohost sur un magasin d’état de Session externe, tel que [fournisseur d’état de Session Azure pour Redis](http://go.microsoft.com/fwlink/?LinkId=401521).

### <a name="solution"></a>Solution
Une solution recommandée est l’état de session toostore sur un service de cache géré. Découvrez comment toouse [fournisseur d’état de Session Azure pour Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore votre état de session. Vous pouvez également magasin d’état de session dans d’autres emplacements de tooensure que votre application est évolutive dans le cloud de hello. toolearn plus d’informations sur les solutions alternatives, consultez [Modes d’état de Session](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>La méthode d'exécution ne doit pas être asynchrone
### <a name="id"></a>ID
AP1000

### <a name="description"></a>Description
Créez des méthodes asynchrones (telles que [await](https://msdn.microsoft.com/library/hh156528.aspx)) en dehors de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (méthode), puis d’appeler des méthodes hello asynchrone à partir de [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). Déclaration hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) de la méthode async provoque travailleur de hello rôle tooenter une boucle de redémarrage.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Appel de méthodes asynchrones à l’intérieur de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) méthode entraîne un rôle de travail hello cloud service runtime toorecycle hello. Lorsqu’un rôle de travail démarre, l’exécution du programme tous les a lieu à l’intérieur de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (méthode). Sortie hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) méthode entraîne un travail de hello toorestart de rôle. Lors de l’exécution du rôle de travail hello atteint la méthode async de hello, il répartit toutes les opérations après la méthode async de hello, puis retourne. Cela provoque la travailleur de hello rôle tooexit de hello [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (méthode) et redémarrez. Dans l’itération suivante de hello d’exécution, rôle de travail hello atteint la méthode async hello et redémarre, à l’origine de travail de hello toorecycle rôle également.

### <a name="solution"></a>Solution
Placez toutes les opérations asynchrones en dehors de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (méthode). Ensuite, appelez la méthode async de hello refactorisé à partir d’à l’intérieur de hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) méthode, telle que RunAsync () .wait. outil d’analyse du Code Azure Hello peut vous aider à résoudre ce problème.

Hello suivant extrait de code illustre le correctif de code hello pour résoudre ce problème :

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Utiliser l’authentification de signature d’accès partagé Service Bus
### <a name="id"></a>ID
AP2000

### <a name="description"></a>Description
Utilisez la signature d’accès partagé (SAP) pour l’authentification. Le service de contrôle d’accès (ACS) est obsolète pour l’authentification Service Bus.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Pour une sécurité renforcée, Azure Active Directory remplace l’authentification du service de contrôle d’accès (ACS) par l’authentification de signature d’accès partagé (SAP). Consultez [Azure Active Directory est hello future des services ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) pour plus d’informations sur le plan de transition hello.

### <a name="solution"></a>Solution
Utilisez l’authentification de signature d’accès partagé dans vos applications. Bonjour à l’exemple suivant montre comment toouse un tooaccess jeton SAS existant un service bus espace de noms ou de l’entité.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

Consultez hello rubriques pour plus d’informations suivantes.

* Pour une vue d’ensemble, consultez [Authentification de signature d’accès partagé avec Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)
* [Comment toouse authentification de Signature d’accès partagé avec Service Bus](https://msdn.microsoft.com/library/dn205161.aspx)
* Pour un exemple de projet, consultez [Utilisation de l’authentification de signature d’accès partagé avec des abonnements Service Bus](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>Envisagez d’utiliser tooavoid de méthode OnMessage « receive loop »
### <a name="id"></a>ID
AP2002

### <a name="description"></a>Description
tooavoid dans une « boucle de réception, » hello appelant **OnMessage** méthode est une meilleure solution pour la réception des messages que l’appelant hello **réception** (méthode). Toutefois, si vous devez utiliser hello **réception** (méthode) et que vous spécifiez un délai d’attente par défaut serveur, vérifiez que temps d’attente serveur hello plus d’une minute.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Lors de l’appel **OnMessage**, client de hello démarre une pompe de messages interne qui interroge en permanence la file d’attente hello ou un abonnement. Cette pompe de messages contient une boucle infinie qui émet un appel tooreceive messages. Si l’appel de hello expire, il émet un nouvel appel. intervalle de délai d’attente Hello est déterminé par la valeur hello hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) propriété Hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)qui est utilisé.

avantage de l’utilisation de Hello **OnMessage** comparées trop**réception** est que les utilisateurs n’ont pas toomanually vérifier les messages, gestion des exceptions, traiter plusieurs messages en parallèle et terminer hello messages.

Si vous appelez **réception** sans utiliser sa valeur par défaut, être vraiment hello *ServerWaitTime* valeur est plus d’une minute. Paramètre *ServerWaitTime* toomore d’une minute empêche le serveur de hello n’expire pas avant la réception du message de type hello est entièrement.

### <a name="solution"></a>Solution
Consultez hello suivant des exemples de code pour les utilisations recommandées. Pour plus d’informations, consultez [QueueClient.OnMessage (méthode) (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) et [QueueClient.Receive (méthode) (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

tooimprove des performances de hello Hello infrastructure de messagerie Azure, consultez le modèle de conception hello [manuel de la messagerie asynchrone](https://msdn.microsoft.com/library/dn589781.aspx).

Hello Voici un exemple d’utilisation **OnMessage** tooreceive messages.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

Hello Voici un exemple d’utilisation **réception** avec le serveur par défaut de hello du temps d’attente.

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

Hello Voici un exemple d’utilisation **réception** avec un serveur non définis par défaut du temps d’attente.

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>Envisagez d'utiliser les méthodes asynchrones de Service Bus
### <a name="id"></a>ID
AP2003

### <a name="description"></a>Description
Utilisez des performances tooimprove de méthodes asynchrones Service Bus avec la messagerie répartie.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Permet de simultanée de programmes d’application à l’aide de méthodes asynchrones, car l’exécution de chaque appel ne bloque pas les thread principal hello. Lors de l’utilisation des méthodes de messagerie Service Bus, les opérations (envoi, réception, suppression, etc.) prennent du temps. Ce temps inclut traitement hello d’opération de hello en hello Service service Bus de latence de toohello d’ajout de la demande de hello et réponse de hello. nombre de hello tooincrease d’opérations par période, les opérations doivent s’exécuter simultanément. Pour plus d’informations, consultez trop[meilleures pratiques pour les performances améliorations apportées à l’aide de messagerie répartie Service Bus](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>Solution
Consultez [classe QueueClient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) pour plus d’informations sur comment toouse hello recommandé de méthode asynchrone.

tooimprove des performances de hello Hello infrastructure de messagerie Azure, consultez le modèle de conception hello [manuel de la messagerie asynchrone](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>Envisagez de partitionner les files d’attente et les rubriques Service Bus
### <a name="id"></a>ID
AP2004

### <a name="description"></a>Description
Partitionnement des files d’attente et des rubriques Service Bus pour de meilleures performances avec la messagerie Service Bus.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Partitionnement des rubriques et files d’attente Service Bus augmente les performances de débit et le service de disponibilité hello débit global d’une file d’attente partitionnée ou une rubrique est n’est plus limité par des performances d’un seul broker ou de la banque de messages hello. En outre, la panne temporaire d’un magasin de messagerie ne rend pas une rubrique ou une file d’attente partitionnée indisponible. Pour plus d’informations, consultez la rubrique [Partitionnement des entités de messagerie](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>Solution
Hello suivant extrait de code montre comment toopartition des entités de messagerie.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Pour plus d’informations, consultez [partitionné les files d’attente de Service Bus et rubriques | Blog de Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) et extraire hello [file d’attente de Microsoft Azure Service Bus partitionnée](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) exemple.

## <a name="do-not-set-sharedaccessstarttime"></a>Ne pas définir SharedAccessStartTime
### <a name="id"></a>ID
AP3001

### <a name="description"></a>Description
Évitez d’utiliser SharedAccessStartTimeset toohello heure actuelle tooimmediately démarrer hello stratégie d’accès partagé. Vous ne devez tooset cette propriété si vous souhaitez que d’une stratégie d’accès partagé hello toostart ultérieurement.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
La synchronisation de l’heure provoque une légère différence d’heure entre les centres de données. Par exemple, il serait logique heure de début de paramètre hello une stratégie de stockage SAS car hello heure actuelle à l’aide de DateTime.Now ou une méthode similaire entraîne l’effet de tootake hello SAS stratégie immédiatement. Toutefois, hello légère différence d’heure entre les centres de données peut entraîner des problèmes dans la mesure où certains centres peuvent être légèrement postérieure à l’heure de début de hello, tandis que d’autres sont en avance. Par conséquent, hello stratégie de SAP peut expirer rapidement (ou même immédiatement) si la durée de vie de stratégie hello est trop faible.

Pour plus d’informations sur l’utilisation de la Signature d’accès partagé sur le stockage Azure, consultez [présentation de la Table SAS (Shared Access Signature) SAS de file d’attente de Site et mise à jour tooBlob SAS - Blog d’équipe Microsoft Azure Storage - accueil - Blogs MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Solution
Supprimez l’instruction hello qui définit l’heure de début hello de stratégie d’accès partagé de hello. outil d’analyse du Code Azure Hello fournit un correctif pour résoudre ce problème. Pour plus d’informations sur la gestion de la sécurité, consultez le modèle de conception hello [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).

Hello suivant extrait de code illustre le correctif de code hello pour résoudre ce problème.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>Le délai d'expiration de la stratégie d'accès partagé doit être de plus de cinq minutes
### <a name="id"></a>ID
AP3002

### <a name="description"></a>Description
Il peut y avoir jusqu'à cinq minutes de différence entre les centres de données situés à différents emplacements en raison de la condition tooa appelé « décalage d’horloge. » les horloges jeton de stratégie tooprevent hello SAP à partir de la date d’expiration définie plus tôt que prévu, toobe de temps d’expiration hello plus de cinq minutes.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Centres de données situés à différents emplacements monde hello synchronisent à un signal d’horloge. Étant donné que le temps requis pour l’horloge signal tootravel toodifferent des emplacements, il peut y avoir un écart de temps entre les centres de données à différents emplacements géographiques bien que tout est censé être synchronisé. Cette différence peut affecter hello accès partagé début temps et expiration intervalle de stratégie. Par conséquent, tooensure stratégie d’accès partagé prend effet immédiatement, ne spécifiez pas l’heure de début hello. En outre, veillez à délai d’expiration de hello est supérieure au délai d’expiration de 5 minutes tooprevent anticipée.

Pour plus d’informations sur l’utilisation de la Signature d’accès partagé sur le stockage Azure, consultez [présentation de la Table SAS (Shared Access Signature) SAS de file d’attente de Site et mise à jour tooBlob SAS - Blog d’équipe Microsoft Azure Storage - accueil - Blogs MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Solution
Pour plus d’informations sur la gestion de la sécurité, consultez le modèle de conception hello [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).

Hello Voici un exemple de ne pas spécifier une heure de début de stratégie accès partagé.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Hello Voici un exemple de spécification d’une heure de début de stratégie accès partagé avec une durée d’expiration de stratégie supérieure à cinq minutes.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Pour plus d'informations, consultez [Créer et utiliser une signature d’accès partagé](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>Utiliser CloudConfigurationManager
### <a name="id"></a>ID
AP4000

### <a name="description"></a>Description
À l’aide de hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) classe pour les projets, telles que les sites Web Azure et services mobiles Azure ne présentent aucun problème d’exécution. Comme meilleure pratique, cependant, il est une bonne idée de toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) de façon unifiée de gestion des configurations pour toutes les applications de Cloud Azure.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
CloudConfigurationManager lit l’environnement d’application hello configuration fichier toohello approprié.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>Solution
Refactoriser votre hello toouse de code [classe CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Un correctif pour résoudre ce problème est fourni par l’outil d’analyse de Code Azure hello.

Hello suivant extrait de code illustre le correctif de code hello pour résoudre ce problème. Replace

`var settings = ConfigurationManager.AppSettings["mySettings"];`

par

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Voici un exemple de comment toostore hello le paramètre de configuration dans un fichier App.config ou Web.config. Ajoutez la section appSettings toohello du paramètres hello hello du fichier de configuration. Hello Voici fichier Web.config de hello pour l’exemple de code précédent hello.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Évitez d'utiliser des chaînes de connexion codées en dur
### <a name="id"></a>ID
AP4001

### <a name="description"></a>Description
Si vous utilisez des chaînes de connexion codées en dur et que vous devez tooupdate les plus tard, vous disposez du code source de toomake modifications tooyour et recompiler l’application hello. Toutefois, si vous stockez vos chaînes de connexion dans un fichier de configuration, vous pouvez modifier les ultérieurement en mettant simplement à jour le fichier de configuration hello.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Le codage en dur les chaînes de connexion est une mauvaise pratique, car elle présente des problèmes lorsque les chaînes de connexion doivent toobe modifiée rapidement. En outre, si hello doit toobe archivé toosource contrôle, les chaînes de connexion codées en dur introduisent des failles de sécurité dans la mesure où les chaînes de hello peuvent être affichées dans le code source de hello.

### <a name="solution"></a>Solution
Stocker des chaînes de connexion dans les fichiers de configuration hello ou environnements Azure.

* Pour les applications autonomes, utilisez les paramètres de chaîne de connexion toostore app.config.
* Pour les applications web hébergé par IIS, utilisez les chaînes de connexion web.config toostore.
* Pour les applications ASP.NET vNext, utilisez configuration.json toostore les chaînes de connexion.

Pour plus d’informations sur l’utilisation de fichiers de configuration comme web.config ou app.config, consultez la page [Conseils de configuration ASP.NET web](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Pour plus d’informations sur le fonctionnement des variables d’environnement Azure, consultez [Sites web Microsoft Azure : Fonctionnement des chaînes d’application et des chaînes de connexion](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/). Pour plus d’informations sur le stockage de la chaîne de connexion dans le contrôle de code source, consultez la rubrique [Éviter de placer des informations sensibles (par exemple, des chaînes de connexion) dans des fichiers stockés dans des référentiels de code source](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).

## <a name="use-diagnostics-configuration-file"></a>Utiliser le fichier de configuration des diagnostics
### <a name="id"></a>ID
AP5000

### <a name="description"></a>Description
Au lieu de configurer les paramètres de diagnostic dans votre code, par exemple à l’aide de hello Microsoft.WindowsAzure.Diagnostics API de programmation, vous devez configurer les paramètres de diagnostic dans le fichier de diagnostics.wadcfg hello. (ou diagnostics.wadcfgx si vous utilisez Azure SDK 2.5). Ce faisant, vous pouvez modifier les paramètres de diagnostic sans avoir toorecompile votre code.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Avant Azure SDK 2.5 (qui utilise Azure diagnostics 1.3), Azure Diagnostics (WAD) peut être configuré à l’aide de différentes méthodes : ajout de son objet blob de configuration toohello dans le stockage, à l’aide du code impératif, une configuration déclarative ou par défaut de hello configuration. Toutefois, hello préféré de façon tooconfigure diagnostics est toouse un fichier de configuration XML (diagnostics.wadcfg ou Diagnostics.wadcfgx pour le SDK 2.5 et versions ultérieures) dans un projet d’application hello. Dans cette approche, fichier de diagnostics.wadcfg hello complètement définit la configuration de hello et peut être mis à jour et redéployé à volonté. Utilisation de hello du fichier de configuration diagnostics.wadcfg hello redémarrables avec hello des méthodes de programmation de la définition de configurations à l’aide de hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)ou [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) classes peuvent entraîner des tooconfusion. Consultez la rubrique [Initialiser ou modifier la configuration des diagnostics Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) pour plus d’informations.

Depuis WAD 1.3 (fourni avec Azure SDK 2.5), il n’est plus diagnostics tooconfigure du code toouse possible. Par conséquent, vous pouvez fournir uniquement configuration hello lors de l’application ou extension de diagnostics hello de mise à jour.

### <a name="solution"></a>Solution
Utilisez hello diagnostics concepteur toomove les paramètres de diagnostic toohello diagnostics configuration fichier de configuration (Diagnostics.wadcfg ou Diagnostics.wadcfgx pour le SDK 2.5 et versions ultérieures). Il est également recommandé d’installer [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) et utiliser la fonctionnalité diagnostics de la plus récente hello.

1. Dans le menu contextuel hello rôle hello que vous souhaitez tooconfigure, choisissez Propriétés, puis onglet de Configuration hello.
2. Bonjour **Diagnostics** section, assurez-vous que hello **activer les Diagnostics** case à cocher est activée.
3. Choisissez hello **configurer** bouton.

   ![Option de hello activer les Diagnostics de l’accès à](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Consultez [Configuration des diagnostics pour Azure Cloud Services et Azure Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) pour plus d’informations.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>Éviter de déclarer les objets DbContext comme statiques
### <a name="id"></a>ID
AP6000

### <a name="description"></a>Description
toosave mémoire, évitez de déclarer les objets DBContext comme statiques.

Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motif
Les objets DBContext contiennent hello des résultats de requête à partir de chaque appel. Les objets DBContext statiques ne sont pas supprimés jusqu'à ce que le domaine d’application hello est déchargé. Par conséquent, un objet DBContext statique peut consommer de grandes quantités de mémoire.

### <a name="solution"></a>Solution
Déclarer DBContext comme variable locale ou champ d’instance non statique, l’utiliser pour une tâche et le laisser être supprimé après utilisation.

Hello suivant l’exemple de classe de contrôleur MVC montre comment toouse hello DBContext objet.

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur l’optimisation et la résolution des problèmes d’applications Azure, consultez [dépanner une application web dans Azure App Service à l’aide de Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).
