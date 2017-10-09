---
title: aaaAzure application de sur le site/cloud hybride de relais de WCF (.NET) | Documents Microsoft
description: "Découvrez comment application hybride de toocreate un .NET sur le site/cloud à l’aide de relais WCF de Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Application .NET locale/de cloud hybride avec Azure WCF Relay
## <a name="introduction"></a>Introduction

Cet article explique comment toobuild hybride cloud application avec Microsoft Azure et Visual Studio. didacticiel de Hello suppose que vous n’avez aucune expérience préalable à l’aide d’Azure. Vous devez en moins de 30 minutes, une application qui utilise plusieurs ressources Azure et en cours d’exécution dans le cloud de hello.

Vous apprendrez à effectuer les opérations suivantes :

* Comment toocreate ou adapter un service web existant pour la consommation par une solution web.
* Comment les données toouse hello Azure WCF relais service tooshare entre une application Windows Azure et un service web hébergé ailleurs.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Avantages de l’utilisation d’Azure Relay pour les solutions hybrides

Les solutions d’entreprise sont généralement composées d’une combinaison de code personnalisé écrit tootackle nouvelle et besoins uniques et les fonctionnalités existantes fournies par les solutions et les systèmes qui sont déjà en place.

Architectes de solutions commencent cloud de hello toouse pour gérer plus facilement les exigences de mise à l’échelle et de réduction des coûts opérationnels. Ce faisant, ils recherchent que les ressources de service existantes souhaite tooleverage comme blocs de construction pour leurs solutions sont à l’intérieur du pare-feu d’entreprise de hello et à l’extérieur facile atteint pour l’accès par la solution de cloud computing hello. De nombreux services internes ne sont pas créées ou hébergées de façon qu’elles peuvent être facilement exposées en périphérie du réseau d’entreprise hello.

[Relais Azure](https://azure.microsoft.com/services/service-bus/) est conçu pour hello cas d’utilisation des services web de Windows Communication Foundation (WCF) existants et de les mettre des services accessibles en toute sécurité toosolutions qui résident en dehors du périmètre de l’entreprise hello sans nécessiter de infrastructure de réseau d’entreprise toohello modifications contraignant. Ces services de relais se trouvent toujours dans leur environnement existant, mais ils déléguer l’écoute entrant sessions et demandes toohello hébergé dans le cloud service de relais. Azure Relay protège également ces services de tout accès non autorisé à l’aide de l’authentification par [signature d’accès partagé](../service-bus-messaging/service-bus-sas.md) (SAP).

## <a name="solution-scenario"></a>Scénario de la solution
Dans ce didacticiel, vous allez créer un site Web ASP.NET qui permet de vous toosee une liste de produits dans la page stock de produit hello.

![][0]

Hello est supposé contenir des informations produit dans un système local existant et d’utilise Azure relais tooreach dans ce système. La simulation met en scène un service Web exécuté dans une simple application console et appuyé par un ensemble de produits en mémoire. Vous toorun en mesure de cette application de console sur votre ordinateur et déployez un rôle web de hello dans Azure. En procédant ainsi, vous verrez comment les rôles de web hello en hello centre de données Azure appellera en effet sur votre ordinateur, même si votre ordinateur se trouvera certainement derrière des pare-feu au moins une et une couche de traduction d’adresse réseau.

## <a name="set-up-hello-development-environment"></a>Configuration d’environnement de développement hello

Avant de commencer à développer des applications Azure, téléchargez les outils hello et configurer votre environnement de développement :

1. Installer hello Azure SDK pour .NET à partir de hello SDK [page Téléchargements](https://azure.microsoft.com/downloads/).
2. Bonjour **.NET** colonne, cliquez sur la version de hello de [Visual Studio](http://www.visualstudio.com) que vous utilisez. Hello étapes dans ce didacticiel, utilisez Visual Studio 2015, mais ils fonctionnent également avec Visual Studio 2017.
3. Lorsque vous y êtes invité toorun ou enregistrer le programme d’installation Bonjour, cliquez sur **exécuter**.
4. Bonjour **Web Platform Installer**, cliquez sur **installer** et poursuivre l’installation de hello.
5. Une fois l’installation de hello est terminée, vous devez tous les éléments nécessaires toostart toodevelop hello application. Hello SDK inclut des outils qui vous permettent de développer facilement des applications Azure dans Visual Studio.

## <a name="create-a-namespace"></a>Créer un espace de noms

à l’aide de toobegin hello des fonctionnalités de relais dans Azure, vous devez d’abord créer un espace de noms de service. Un espace de noms fournit un conteneur d’étendue pour l’adressage des ressources Azure au sein de votre application. Suivez hello [ici les instructions](relay-create-namespace-portal.md) toocreate un espace de noms de relais.

## <a name="create-an-on-premises-server"></a>Création d’un serveur local

Vous créez d'abord un système local de catalogue de produits (fictif). Il sera relativement simple ; Vous pouvez voir cela comme représentant un système de catalogue produit réel local avec une surface de service complet que nous essayons de toointegrate.

Ce projet est une application de console Visual Studio et utilise hello [package NuGet d’Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello bibliothèques Service Bus et les paramètres de configuration.

### <a name="create-hello-project"></a>Créer le projet de hello

1. Avec les privilèges d’administrateur, démarrez Microsoft Visual Studio. toodo, cliquez sur icône du programme Visual Studio hello, puis cliquez sur **exécuter en tant qu’administrateur**.
2. Dans Visual Studio, sur hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.
3. Dans **Modèles installés**, sous **Visual C#**, cliquez sur **Application console (.NET Framework)**. Bonjour **nom** zone, entrez un nom hello **ProductsServer**:

   ![][11]
4. Cliquez sur **OK** toocreate hello **ProductsServer** projet.
5. Si vous avez déjà installé le Gestionnaire de package NuGet hello pour Visual Studio, ignorer l’étape suivante de toohello. Sinon, accédez à [NuGet][NuGet], puis cliquez sur [Installer NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c). Suivez le Gestionnaire de package NuGet hello invites tooinstall hello, puis redémarrez Visual Studio.
6. Dans l’Explorateur de solutions, cliquez sur hello **ProductsServer** de projet, puis cliquez sur **gérer les Packages NuGet**.
7. Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`. Sélectionnez hello **WindowsAzure.ServiceBus** package.
8. Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.

   ![][13]

   Notez que hello client assemblys requis sont désormais référencés.
8. Ajoutez une nouvelle classe pour votre contrat de produit. Dans l’Explorateur de solutions, cliquez sur hello **ProductsServer** projet puis cliquez sur **ajouter**, puis cliquez sur **classe**.
9. Bonjour **nom** zone, entrez un nom hello **ProductsContract.cs**. Cliquez ensuite sur **Add**.
10. Dans **ProductsContract.cs**, remplacer la définition d’espace de noms de hello par hello suivant de code, qui définit le contrat hello pour le service de hello.

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. Dans le fichier Program.cs, remplacez définition d’espace de noms hello hello suivant du code qui ajoute le service de profil hello et hôte hello pour celle-ci.

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. Dans l’Explorateur de solutions, double-cliquez sur hello **App.config** tooopen de fichiers dans l’éditeur de Visual Studio hello. En bas de hello Hello `<system.ServiceModel>` élément (mais toujours compris `<system.ServiceModel>`), ajouter hello suivant le code XML. Être vraiment tooreplace *yourServiceNamespace* avec nom hello de votre espace de noms et *yourKey* avec la clé SAS hello extrait précédemment à partir du portail de hello :

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. Toujours dans le fichier App.config, Bonjour `<appSettings>` élément, la valeur de chaîne de connexion de hello remplacer avec la chaîne de connexion hello obtenu à partir du portail de hello.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Appuyez sur **Ctrl + Maj + B** ou à partir de hello **générer** menu, cliquez sur **générer la Solution** toobuild hello application et vérifier la précision de hello de votre travail jusqu'à présent.

## <a name="create-an-aspnet-application"></a>Création d’une application ASP.NET

Dans cette section, vous allez générer une application ASP.NET simple qui affiche des données récupérées de votre service de produit.

### <a name="create-hello-project"></a>Créer le projet de hello

1. Vérifiez que Visual Studio fonctionne avec les privilèges d’administrateur.
2. Dans Visual Studio, sur hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.
3. Dans **Modèles installés**, sous **Visual C#**, cliquez sur **Application web ASP.NET (.NET Framework)**. Projet de hello nom **ProductsPortal**. Cliquez ensuite sur **OK**.

   ![][15]

4. À partir de hello **modèles ASP.NET** liste Bonjour **nouvelle Application Web ASP.NET** boîte de dialogue, cliquez sur **MVC**.

   ![][16]

6. Cliquez sur hello **modifier l’authentification** bouton. Bonjour **modifier l’authentification** boîte de dialogue zone, vérifiez que **aucune authentification** est sélectionné, puis cliquez sur **OK**. Pour ce didacticiel, vous déployez une application qui n’a pas besoin de connexion de l’utilisateur.

    ![][18]

7. Dans hello **nouvelle Application Web ASP.NET** boîte de dialogue, cliquez sur **OK** toocreate hello MVC application.
8. Vous devez maintenant configurer les ressources Azure d’une nouvelle application web. Suivez les étapes de hello Bonjour [section tooAzure de cet article de la publication](../app-service-web/app-service-web-get-started-dotnet.md). Ensuite, retourner toothis didacticiel et continuer toohello prochaine étape.
10. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Modèles**, puis cliquez sur **Ajouter** et sur **Classe**. Bonjour **nom** zone, entrez un nom hello **Product.cs**. Cliquez ensuite sur **Add**.

    ![][17]

### <a name="modify-hello-web-application"></a>Modifier l’application web de hello

1. Dans le fichier de Product.cs hello dans Visual Studio, remplacez définition d’espace de noms existante hello hello suivant de code.

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. Dans l’Explorateur de solutions, développez hello **contrôleurs** dossier, puis double-cliquez sur hello **HomeController.cs** tooopen de fichiers dans Visual Studio.
3. Dans **HomeController.cs**, remplacez définition d’espace de noms existante hello hello suivant de code.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. Dans l’Explorateur de solutions, développez le dossier Views\Shared de hello, puis double-cliquez sur **_Layout.cshtml** tooopen dans l’éditeur de Visual Studio hello.
5. Remplacez toutes les occurrences de **mon Application ASP.NET** trop**produits LITWARE**.
6. Supprimer hello **accueil**, **sur**, et **Contact** des liens. Bonjour l’exemple suivant, supprimer les code hello mis en surbrillance.

    ![][41]

7. Dans l’Explorateur de solutions, développez le dossier Views\Home de hello, puis double-cliquez sur **Index.cshtml** tooopen dans l’éditeur de Visual Studio hello. Remplacez hello tout contenu de fichier de hello hello suivant de code.

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. précision de hello tooverify de votre travail jusqu'à présent, vous pouvez appuyer sur **Ctrl + Maj + B** projet hello de toobuild.

### <a name="run-hello-app-locally"></a>Exécuter des application hello localement

Exécutez tooverify application hello qu’il fonctionne.

1. Vérifiez que **ProductsPortal** est le projet actif de hello. Cliquez sur le nom de projet hello dans l’Explorateur de solutions et sélectionnez **définir comme projet de démarrage**.
2. Dans Visual Studio, appuyez sur **F5**.
3. Votre application doit s’exécuter dans un navigateur :

   ![][21]

## <a name="put-hello-pieces-together"></a>Rassembler les pièces hello

étape suivante de Hello est toohook serveur produits hello local hello application ASP.NET.

1. Si elle n’est pas déjà ouvert, dans Visual Studio rouvrez hello **ProductsPortal** projet que vous avez créé dans hello [créer une application ASP.NET](#create-an-aspnet-application) section.
2. Étape toohello similaire dans la section « Création d’un serveur local » de hello, ajouter des références de projet hello NuGet package toohello. Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** de projet, puis cliquez sur **gérer les Packages NuGet**.
3. Recherche de « Service Bus » et sélectionnez hello **WindowsAzure.ServiceBus** élément. Terminer l’installation de hello, puis fermez cette boîte de dialogue.
4. Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** de projet, puis cliquez sur **ajouter**, puis **élément existant**.
5. Accédez toohello **ProductsContract.cs** fichier hello **ProductsServer** projet console. Cliquez sur toohighlight ProductsContract.cs. Cliquez sur hello bas suivant trop**ajouter**, puis cliquez sur **ajouter en tant que lien**.

   ![][24]

6. Ouvrez maintenant hello **HomeController.cs** de fichiers dans l’éditeur de Visual Studio hello et remplacez hello espace de noms définition par hello suivant de code. Être vraiment tooreplace *yourServiceNamespace* avec nom hello de votre espace de noms de service et *yourKey* avec votre clé SAP. Cette opération activera hello client toocall hello services locaux, obtenir de résultats de l’appel de hello hello.

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** solution (Assurez-vous que tooright clic hello solution, pas hello projet). Cliquez sur **Ajouter**, puis sur **Projet existant**.
8. Accédez toohello **ProductsServer** de projet, puis double-cliquez sur hello **ProductsServer.csproj** tooadd du fichier solution il.
9. **ProductsServer** doit être en cours d’exécution dans les données de commande toodisplay hello **ProductsPortal**. Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** solution et cliquez sur **propriétés**. Hello **Pages de propriétés** boîte de dialogue s’affiche.
10. Dans hello côté gauche, cliquez sur **projet de démarrage**. Sur le côté droit de hello, cliquez sur **plusieurs projets de démarrage**. Vérifiez que **ProductsServer** et **ProductsPortal** apparaissent dans cet ordre, avec **Démarrer** défini en tant qu’action hello pour les deux.

      ![][25]

11. Toujours en hello **propriétés** boîte de dialogue, cliquez sur **dépendances du projet** sur hello côté gauche.
12. Bonjour **projets** , cliquez sur **ProductsServer**. Vérifiez que **ProductsPortal** n’est pas sélectionné.
13. Bonjour **projets** , cliquez sur **ProductsPortal**. Vérifiez que **ProductsServer** est sélectionné.

    ![][26]

14. Cliquez sur **OK** Bonjour **Pages de propriétés** boîte de dialogue.

## <a name="run-hello-project-locally"></a>Exécutez le projet de hello localement

Appuyez sur tootest hello localement application, dans Visual Studio **F5**. serveur local de Hello (**ProductsServer**) doit démarrer en premier, puis hello **ProductsPortal** application doit démarrer dans une fenêtre de navigateur. Cette fois-ci, vous verrez que l’inventaire produits hello répertorie les données récupérées à partir du système de hello produit service local.

![][10]

Appuyez sur **Actualiser** sur hello **ProductsPortal** page. Chaque fois que vous actualisez la page de hello, vous verrez hello server application affiche un message lorsque `GetProducts()` de **ProductsServer** est appelée.

Fermez les deux applications avant de poursuivre la procédure toohello.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Déployer le projet hello ProductsPortal tooan l’application web Azure

étape suivante de Hello est toorepublish hello Azure Web app **ProductsPortal** serveur frontal. Hello suivant :

1. Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** le projet, puis cliquez sur **publier**. Ensuite, cliquez sur **publier** sur hello **publier** page.

  > [!NOTE]
  > Vous pouvez voir un message d’erreur dans la fenêtre du navigateur hello lorsque hello **ProductsPortal** projet web est lancé automatiquement après le déploiement de hello. Cela est prévu et se produit parce que hello **ProductsServer** application n’est pas encore exécuté.
>
>

2. Copier l’URL de hello hello déployé l’application web, car vous en aurez besoin URL hello dans l’étape suivante de hello. Vous pouvez également obtenir cette URL à partir de la fenêtre d’activité de Service d’application Azure hello dans Visual Studio :

  ![][9]

3. Fermez Bonjour Bonjour du toostop fenêtre de navigateur exécutant l’application.

### <a name="set-productsportal-as-web-app"></a>Définition de ProductsPortal en tant qu’application web

Avant l’exécution de l’application hello dans le cloud de hello, vous devez vous assurer que **ProductsPortal** est lancé au sein de Visual Studio en tant qu’une application web.

1. Dans Visual Studio, avec le bouton droit hello **ProductsPortal** de projet, puis cliquez sur **propriétés**.
2. Dans la colonne de gauche hello, cliquez sur **Web**.
3. Bonjour **Action de démarrage** , cliquez sur hello **démarrer l’URL** bouton, puis dans la zone de texte hello entrez hello URL pour votre application web déployée précédemment ; par exemple, `http://productsportal1234567890.azurewebsites.net/`.

    ![][27]

4. À partir de hello **fichier** menu dans Visual Studio, cliquez sur **Enregistrer tout**.
5. À partir du menu Générer de hello dans Visual Studio, cliquez sur **régénérer la Solution**.

## <a name="run-hello-application"></a>Exécutez l’application hello

1. Appuyez sur F5 toobuild et exécuter l’application hello. serveur local de Hello (hello **ProductsServer** application console) doit démarrer en premier, puis hello **ProductsPortal** application doit démarrer dans une fenêtre de navigateur, comme indiqué dans hello suivant l’écran capture de. Notez à nouveau que l’inventaire produits hello répertorie les données récupérées à partir du système de hello produit service local et les affiche dans l’application web hello. Vérifiez que hello-URL-toomake qui **ProductsPortal** est en cours d’exécution dans le cloud hello, comme une application web Azure.

   ![][1]

   > [!IMPORTANT]
   > Hello **ProductsServer** application console doit être en cours d’exécution et en mesure de tooserve hello données toohello **ProductsPortal** application. Si le navigateur de hello affiche une erreur, attendez quelques secondes plus pour **ProductsServer** tooload et hello complet suivant du message. Appuyez sur **Actualiser** dans le navigateur de hello.
   >
   >

   ![][37]
2. Dans le navigateur de hello, appuyez sur **Actualiser** sur hello **ProductsPortal** page. Chaque fois que vous actualisez la page de hello, vous verrez hello server application affiche un message lorsque `GetProducts()` de **ProductsServer** est appelée.

    ![][38]

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur Azure relais, consultez hello suivant des ressources :  

* [Qu’est-ce qu’Azure Relay ?](relay-what-is-it.md)  
* [Comment toouse de relais](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
