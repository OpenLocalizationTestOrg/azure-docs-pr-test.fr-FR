---
title: "application à plusieurs niveaux de aaa.NET à l’aide d’Azure Service Bus | Documents Microsoft"
description: "Un didacticiel .NET qui vous permet de développer une application à plusieurs niveaux dans Azure qui utilise toocommunicate de files d’attente Service Bus entre les couches."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>Application multiniveau .NET avec les files d’attente Azure Service Bus
## <a name="introduction"></a>Introduction
Développement de Microsoft Azure est facile à l’aide de Visual Studio et hello gratuit Azure SDK pour .NET. Ce didacticiel vous guide dans hello étapes toocreate une application qui utilise plusieurs ressources Azure en cours d’exécution dans votre environnement local.

Vous allez apprendre suivant de hello :

* Comment tooenable votre ordinateur pour le développement Azure avec un seul télécharger et installer.
* Comment toodevelop de Visual Studio toouse pour Azure.
* Comment toocreate une application à plusieurs niveaux dans Azure à l’aide de rôles web et worker.
* Comment toocommunicate entre les couches à l’aide de files d’attente Service Bus.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

Dans ce didacticiel vous allez générer et exécuter l’application à plusieurs niveaux de hello dans un service cloud Azure. frontal Hello est un rôle web d’ASP.NET MVC et back-end hello est un rôle de travail qui utilise une file d’attente Service Bus. Vous pouvez créer hello même d’application à plusieurs niveaux avec frontal hello comme un projet web, qui est déployé tooan site Web Azure au lieu d’un service cloud. Vous pouvez également essayer hello [application de .NET sur le site/cloud hybride](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) didacticiel.

Hello capture d’écran suivante montre les application hello s’est terminée.

![][0]

## <a name="scenario-overview-inter-role-communication"></a>Vue d’ensemble du scénario : communication entre les rôles
toosubmit un ordre de traitement, composant UI frontal hello, en cours d’exécution dans un rôle web de hello, doit interagir avec la logique de couche intermédiaire hello en cours d’exécution dans le rôle de travail hello. Cet exemple utilise le Bus des services de messagerie pour les communications entre les couches de hello hello.

Utilisation du Service Bus entre hello central les couches web et de messagerie dissocie les deux composants. En revanche toodirect (autrement dit, TCP ou HTTP), la messagerie de hello couche web ne connecte pas intermédiaire toohello directement. au lieu de cela, il pousse les unités de travail, sous forme de messages, dans Service Bus, ce qui les conserve jusqu'à ce que le niveau intermédiaire de hello est prêt tooconsume et de les traiter de manière fiable.

Service Bus fournit la messagerie de deux entités toosupport répartie : files d’attente et rubriques. Avec les files d’attente, chaque message envoyé à la file d’attente de toohello est consommée par un destinataire unique. Rubriques prennent en charge le modèle de publication/abonnement hello dans lequel chaque message publié est mis abonnement disponible tooa inscrit auprès de hello rubrique. Chaque abonnement gère de façon logique sa propre file d’attente de messages. Abonnements peuvent également être configurés avec les règles de filtre qui restreignent hello ensemble de messages transmis à toothose de file d’attente d’abonnement hello qui correspondent au filtre de hello. Hello exemple suivant utilise les files d’attente Service Bus.

![][1]

Ce mécanisme de communication présente plusieurs avantages par rapport à la messagerie directe :

* **Découplage temporel.** Avec le modèle de messagerie asynchrone hello, producteurs et consommateurs ne sont pas nécessairement en ligne à hello même temps. Bus de service fiable stocke les messages jusqu'à ce que le récepteur hello est prêt à les recevoir. Cela permet aux composants de hello de hello distribué application toobe est déconnecté, soit volontairement, par exemple, pour maintenance ou en raison du blocage d’un composant tooa, sans affecter le système dans son ensemble. En outre, hello consommation application suffit peut-être toocome en ligne à certaines heures de la journée de hello.
* **Nivellement de charge.** Dans de nombreuses applications, la charge système varie au fil du temps, alors que le temps de traitement de hello requis pour chaque unité de travail est généralement constant. Fait message producteurs et consommateurs avec une file d’attente signifie que hello consommation d’application (traitement hello) seuls besoins toobe configuré tooaccommodate les charge moyenne plutôt que des pics de charge. profondeur Hello de file d’attente hello augmente et diminue comme hello les charge entrante varie. Cela plus économique en termes de quantité hello de charge de l’application hello infrastructure tooservice requis.
* **Équilibrage de la charge.** Quand la charge augmente, plus de processus de travail peuvent être ajoutés tooread à partir de la file d’attente hello. Chaque message est traité par un seul hello de processus de travail. En outre, cette extraction d’équilibrage de charge permet une utilisation optimale des ordinateurs de travail hello même si les ordinateurs de travail diffèrent en termes de puissance de traitement, car ils extrairont les messages à leur propre taux maximal. Ce modèle est appelé souvent hello *consommateur concurrent* modèle.
  
  ![][2]

Hello les sections suivantes traite de code hello qui implémente cette architecture.

## <a name="set-up-hello-development-environment"></a>Configuration d’environnement de développement hello
Avant de commencer à développer des applications Azure, obtenez les outils hello et configurer votre environnement de développement.

1. Installer hello Azure SDK pour .NET à partir de hello SDK [page Téléchargements](https://azure.microsoft.com/downloads/).
2. Bonjour **.NET** colonne, cliquez sur la version de hello de [Visual Studio](http://www.visualstudio.com) que vous utilisez. Hello étapes dans ce didacticiel, utilisez Visual Studio 2015, mais ils fonctionnent également avec Visual Studio 2017.
3. Lorsque vous y êtes invité toorun ou enregistrer le programme d’installation Bonjour, cliquez sur **exécuter**.
4. Bonjour **Web Platform Installer**, cliquez sur **installer** et poursuivre l’installation de hello.
5. Une fois l’installation de hello est terminée, vous devez tous les éléments nécessaires toostart toodevelop hello application. Hello SDK inclut des outils qui vous permettent de développer facilement des applications Azure dans Visual Studio.

## <a name="create-a-namespace"></a>Créer un espace de noms
étape suivante de Hello est toocreate un espace de noms de service et obtenir une clé de Signature d’accès partagé (SAS). Un espace de noms fournit une limite d’application pour chaque application exposée via Service Bus. Une clé SAS est générée par le système de hello lors de la création d’un espace de noms. combinaison de Hello d’espace de noms et la clé SAP fournit des informations d’identification de hello pour l’application de Service Bus tooauthenticate access tooan.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>Création d'un rôle web
Dans cette section, vous générez des serveurs frontaux hello de votre application. Tout d’abord, vous créez des pages de hello par votre application.
Après cela, ajoutez le code qui soumet la file d’attente du Service Bus éléments tooa et affiche les informations d’état de file d’attente hello.

### <a name="create-hello-project"></a>Créer le projet de hello
1. À l’aide des privilèges d’administrateur, démarrez Visual Studio : avec le bouton hello **Visual Studio** icône du programme, puis cliquez sur **exécuter en tant qu’administrateur**. émulateur de calcul Azure Hello, présenté plus loin dans cet article, nécessite que Visual Studio est démarré avec des privilèges d’administrateur.
   
   Dans Visual Studio, sur hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.
2. Dans **Modèles installés**, sous **Visual C#**, cliquez sur **Cloud**, puis sur **Azure Cloud Service**. Projet de hello nom **MultiTierApp**. Cliquez ensuite sur **OK**.
   
   ![][9]
3. Dans les rôles **.NET Framework 4.5**, double-cliquez sur **Rôle Web ASP.NET**.
   
   ![][10]
4. Placez le curseur sur **WebRole1** sous **solution Azure Cloud Service**, sur l’icône de crayon hello et renommer le rôle web de hello trop**FrontendWebRole**. Cliquez ensuite sur **OK**. (Entrez bien « Frontend » avec un « e » minuscule, et non « FrontEnd ».)
   
   ![][11]
5. À partir de hello **nouveau projet ASP.NET** la boîte de dialogue hello **sélectionner un modèle** , cliquez sur **MVC**.
   
   ![][12]
6. Toujours en hello **nouveau projet ASP.NET** boîte de dialogue, cliquez sur hello **modifier l’authentification** bouton. Bonjour **modifier l’authentification** boîte de dialogue, cliquez sur **aucune authentification**, puis cliquez sur **OK**. Pour ce didacticiel, vous déployez une application qui n’a pas besoin de connexion de l’utilisateur.
   
    ![][16]
7. Dans hello **nouveau projet ASP.NET** boîte de dialogue, cliquez sur **OK** projet hello de toocreate.
8. Dans **l’Explorateur de solutions**, Bonjour **FrontendWebRole** de projet, cliquez sur **références**, puis cliquez sur **gérer les Packages NuGet**.
9. Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`. Sélectionnez hello **WindowsAzure.ServiceBus** du package, cliquez sur **installer**et acceptez les conditions d’utilisation de hello.
   
   ![][13]
   
   Notez que hello requis assemblys clients sont désormais référencés et des nouveaux fichiers de code ont été ajoutés.
10. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Modèles** et cliquez sur **Ajouter**, puis sur **Classe**. Bonjour **nom** zone, entrez un nom hello **OnlineOrder.cs**. Cliquez ensuite sur **Add**.

### <a name="write-hello-code-for-your-web-role"></a>Écrire du code hello pour votre rôle web
Dans cette section, vous créez hello différentes pages que votre application affiche.

1. Dans le fichier de OnlineOrder.cs hello dans Visual Studio, remplacez la définition de l’espace de noms existant hello suivant de code :
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. Dans l’**Explorateur de solutions**, double-cliquez sur **Controllers\HomeController.cs**. Ajoutez hello suivant **à l’aide de** instructions haut hello hello tooinclude hello espaces de noms pour le modèle que vous venez de créer, ainsi que le Bus des services de fichiers.
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. Également dans le fichier HomeController.cs de hello dans Visual Studio, remplacez la définition de l’espace de noms existant hello suivant de code. Ce code contient des méthodes de gestion de soumission hello de file d’attente de toohello éléments.
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. À partir de hello **générer** menu, cliquez sur **générer la Solution** précision de hello tootest de votre travail jusqu'à présent.
5. Maintenant, créez la vue hello pour hello `Submit()` méthode que vous avez créé précédemment. Avec le bouton droit dans hello `Submit()` (méthode) (surcharge hello de `Submit()` qui ne prend aucun paramètre), puis choisissez **ajouter une vue**.
   
   ![][14]
6. Une boîte de dialogue s’affiche pour la création de vue de hello. Bonjour **modèle** , choisissez **créer**. Bonjour **classe de modèle** , cliquez sur hello **OnlineOrder** classe.
   
   ![][15]
7. Cliquez sur **Add**.
8. Maintenant, hello de modification affiche le nom de votre application. Dans **l’Explorateur de solutions**, double-cliquez sur le **Views\Shared\\_Layout.cshtml** tooopen de fichiers dans l’éditeur de Visual Studio hello.
9. Remplacez toutes les occurrences de **Mon application ASP.NET** par **LITWARE’S Products**.
10. Supprimer hello **accueil**, **sur**, et **Contact** des liens. Supprimer le code de hello mis en surbrillance :
    
    ![][28]
11. Enfin, modifiez hello présentation page tooinclude des informations sur la file d’attente hello. Dans **l’Explorateur de solutions**, double-cliquez sur le **Views\Home\Submit.cshtml** tooopen de fichiers dans l’éditeur de Visual Studio hello. Ajouter hello ligne après `<h2>Submit</h2>`. Pour l’instant, hello `ViewBag.MessageCount` est vide. Vous le remplirez plus tard.
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. Vous avez maintenant implémenté votre interface utilisateur. Vous pouvez appuyer sur **F5** toorun votre application et vérifiez qu’elle s’affiche comme prévu.
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>Écrire du code hello pour l’envoi de file d’attente du Service Bus éléments tooa
Maintenant, ajoutez le code pour l’envoi de file d’attente de tooa éléments. Tout d’abord, vous créez une classe qui contient les informations de connexion à votre file d’attente Service Bus. Ensuite, initialisez votre connexion à partir de Global.aspx.cs. Enfin, mettre à jour de code de soumission hello que vous avez créé précédemment dans la file d’attente HomeController.cs tooactually submit éléments tooa Service Bus.

1. Dans **l’Explorateur de solutions**, avec le bouton droit **FrontendWebRole** (projet de hello avec le bouton droit, pas les rôles hello). Cliquez sur **Ajouter**, puis sur **Classe**.
2. Nom de classe hello **QueueConnector.cs**. Cliquez sur **ajouter** classe hello de toocreate.
3. Maintenant, ajoutez le code qui encapsule les informations de connexion hello et initialise la file d’attente du Service Bus tooa connexion hello. Remplacez hello tout contenu de QueueConnector.cs par hello suivant de code et entrez des valeurs pour `your Service Bus namespace` (votre nom d’espace de noms) et `yourKey`, qui est hello **clé primaire** obtenu à partir de hello Azure portail.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. Ensuite, assurez-vous que votre méthode **Initialize** est bien appelée. Dans l’**Explorateur de solutions**, double-cliquez sur **Global.asax\Global.asax.cs**.
5. Ajouter hello suivant la ligne de code à fin hello Hello **Application_Start** (méthode).
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. Enfin, mettre à jour de code hello du web vous avez créé précédemment, pour soumettre les éléments toohello file. Dans l’**Explorateur de solutions**, double-cliquez sur **Controllers\HomeController.cs**.
7. Hello de mise à jour `Submit()` (méthode) (surcharge hello qui ne prend aucun paramètre) comme suit tooget hello nombre de messages pour la file d’attente hello.
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. Hello de mise à jour `Submit(OnlineOrder order)` (méthode) (surcharge hello qui prend un paramètre) comme suit toosubmit commande file d’attente de toohello plus d’informations.
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. Vous pouvez maintenant exécuter des application hello. Chaque fois que vous soumettez une commande, nombre de messages hello augmente.
   
   ![][18]

## <a name="create-hello-worker-role"></a>Créer le rôle de travail hello
Vous allez maintenant créer rôle de travail hello qui traite les envois d’ordre hello. Cet exemple utilise hello **rôle de travail avec file d’attente du Bus de Service** modèle de projet Visual Studio. Vous avez déjà obtenu des informations d’identification hello requis à partir du portail de hello.

1. Assurez-vous que vous êtes connecté à Visual Studio tooyour compte Azure.
2. Dans Visual Studio, dans **l’Explorateur de solutions** avec le bouton droit le **rôles** dossier sous hello **MultiTierApp** projet.
3. Cliquez sur **Ajouter**, puis sur **Nouveau projet de rôle de travail**. Hello **ajouter un nouveau projet de rôle** boîte de dialogue s’affiche.
   
   ![][26]
4. Bonjour **ajouter un nouveau projet de rôle** boîte de dialogue, cliquez sur **rôle de travail avec file d’attente du Bus de Service**.
   
   ![][23]
5. Bonjour **nom** boîte, projet de hello nom **OrderProcessingRole**. Cliquez ensuite sur **Add**.
6. Copier la chaîne de connexion hello que vous avez obtenue à l’étape 9 de Presse-papiers de toohello section hello « Créer un espace de noms Service Bus ».
7. Dans **l’Explorateur de solutions**, avec le bouton hello **OrderProcessingRole** créé à l’étape 5 (Assurez-vous que vous cliquez sur **OrderProcessingRole** sous **Rôles**, et pas hello classe). Cliquez ensuite sur **Propriétés**.
8. Sur hello **paramètres** onglet Hello **propriétés** boîte de dialogue, cliquez à l’intérieur de hello **valeur** boîte pour **Microsoft.ServiceBus.ConnectionString**, puis collez la valeur de point de terminaison hello copiée à l’étape 6.
   
   ![][25]
9. Créer un **OnlineOrder** classe toorepresent hello orders, comme les traiter à partir de la file d’attente hello. Vous pouvez réutiliser une classe que vous avez déjà créée. Dans **l’Explorateur de solutions**, avec le bouton hello **OrderProcessingRole** (icône avec le bouton droit de la classe de hello, pas les rôles hello) de classe. Cliquez sur **Ajouter**, puis sur **Élément existant**.
10. Recherchez le sous-dossier toohello pour **FrontendWebRole\Models**, puis double-cliquez sur **OnlineOrder.cs** tooadd il toothis projet.
11. Dans **WorkerRole.cs**, modifiez la valeur hello hello **QueueName** variable à partir de `"ProcessingQueue"` trop`"OrdersQueue"` comme indiqué dans hello suivant de code.
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. Ajoutez hello qui suit à l’aide d’instruction haut hello du fichier WorkerRole.cs de hello.
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. Bonjour `Run()` fonction, à l’intérieur de hello `OnMessage()` appeler, remplacez le contenu hello Hello `try` clause avec hello suivant de code.
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. Vous avez terminé l’application hello. Vous pouvez tester l’application complète hello en double-cliquant sur le projet de MultiTierApp hello dans l’Explorateur de solutions, en sélectionnant **définir comme projet de démarrage**, puis en appuyant sur F5. Notez que le nombre de messages n’augmente pas, car le rôle de travail hello traite les éléments à partir de la file d’attente hello et les marque comme étant terminée. Vous pouvez voir la sortie de trace hello de votre rôle de travail en consultant hello Azure Compute Emulator UI. Cela en icône hello émulateur dans la zone de notification hello de votre barre des tâches et en sélectionnant **Show Compute Emulator UI**.
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur le Bus des services, consultez hello suivant des ressources :  

* [Documentation Azure Service Bus][sbdocs]  
* [Page du service Service Bus][sbacom]  
* [Comment tooUse files d’attente du Bus de Service][sbacomqhowto]  

toolearn en savoir plus sur les scénarios à plusieurs niveaux, consultez :  

* [Application multiniveau .NET avec tables, files d’attente et objets blob de stockage][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
