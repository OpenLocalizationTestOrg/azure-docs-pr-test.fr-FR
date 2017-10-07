---
title: aaaCreate une application .NET pour Service Fabric | Documents Microsoft
description: "Découvrez comment toocreate une application avec un frontal ASP.NET Core et fiable avec état principal de service et les déployer hello application tooa cluster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Créer et déployer une application avec un service frontal API Web ASP.NET Core et un service principal avec état
Ce didacticiel est la première partie d’une série d’étapes.  Vous allez apprendre comment toocreate une application Azure Service Fabric avec un avant de l’API Web ASP.NET principale mettre fin et un toostore avec état service principal de vos données. Lorsque vous avez terminé, vous disposez d’une application de vote avec un serveur web ASP.NET Core frontal qui enregistre les résultats de vote dans un service principal avec état dans le cluster de hello. Si vous ne souhaitez pas toomanually créer hello vote application, vous pouvez [télécharger le code source de hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) pour hello terminé l’application et passer trop[guident hello vote exemple d’application](#walkthrough_anchor).

![Diagramme de l’application](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Dans la première partie de la série de hello, vous apprenez comment :

> [!div class="checklist"]
> * Créer un service API Web ASP.NET Core en tant que service fiable avec état
> * Créer un service d’application Web ASP.NET Core en tant que service web sans état
> * Utilisez hello proxy inverse toocommunicate avec un service avec état hello

Cette série de didacticiels vous montre comment effectuer les opérations suivantes :
> [!div class="checklist"]
> * Créer une application .NET Service Fabric
> * [Déployer le cluster de l’application hello tooa à distance](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [Configurer l’intégration et le déploiement continus à l’aide de Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel :
- Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Installer Visual Studio 2017](https://www.visualstudio.com/) et installer hello **le développement Azure** et **développement web ASP.NET et** les charges de travail.
- [Installer hello SDK de l’infrastructure de Service](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Créer un service API Web ASP.NET en tant que service fiable
Tout d’abord, créez hello web frontal de hello vote application à l’aide d’ASP.NET Core. ASP.NET Core est une infrastructure de développement web léger et inter-plateformes que vous pouvez utiliser l’interface utilisateur de web moderne toocreate et API web. tooget bien comprendre comment ASP.NET Core s’intègre à l’infrastructure de Service, nous recommandons fortement de lire via hello [ASP.NET Core dans Service des Services de Fabric fiables](service-fabric-reliable-services-communication-aspnetcore.md) l’article. Pour l’instant, vous pouvez suivre ce didacticiel tooget démarré rapidement. toolearn savoir plus sur ASP.NET Core, consultez hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).

> [!NOTE]
> Ce didacticiel est basé sur hello [ASP.NET Core tools pour Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc). outils du .NET Core Hello pour Visual Studio 2015 sont plus en cours de mise à jour.

1. Lancez Visual Studio en tant qu’**administrateur**.

2. Créez un projet en sélectionnant **Fichier**->**Nouveau**->**Projet**.

3. Bonjour **nouveau projet** boîte de dialogue, choisissez **Cloud > Application Service Fabric**.

4. Nommez l’application hello **vote** et appuyez sur **OK**.

   ![Boîte de dialogue Nouveau projet dans Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. Sur hello **nouveau Service Service Fabric** choisissez **sans état ASP.NET Core**et le nom de votre service **VotingWeb**.
   
   ![Choix du service web ASP.NET dans la boîte de dialogue hello nouveau service](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. page suivante de Hello fournit un ensemble d’ASP.NET Core modèles de projet. Pour ce didacticiel, sélectionnez **Application web**. 
   
   ![Choisir le type de projet ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio crée une application et un projet de service, et les affiche dans l’Explorateur de solutions.

   ![Explorateur de solutions après la création de l’application avec un service API Web ASP.NET Core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>Ajouter un service de VotingWeb toohello AngularJS
Ajouter [AngularJS](http://angularjs.org/) service tooyour à l’aide intégrée de hello [Bower prise en charge](/aspnet/core/client-side/bower). Ouvrez *bower.json* et ajoutez des entrées pour angular et angular-bootstrap, puis enregistrez vos modifications.

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
Lors de l’enregistrement hello *bower.json* fichier angulaire est installé dans votre projet *wwwroot/lib* dossier. En outre, il est répertorié dans hello *dépendances/Bower* dossier.

### <a name="update-hello-sitejs-file"></a>Fichier de mise à jour hello site.js
Ouvrez hello *wwwroot/js/site.js* fichier.  Remplacez son contenu par hello JavaScript utilisé par les modes d’accueil hello :

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-hello-indexcshtml-file"></a>Fichier de mise à jour hello Index.cshtml
Ouvrez hello *Views/Home/Index.cshtml* fichier, hello vue spécifique toohello accueil du contrôleur.  Remplacez son contenu par les éléments suivants de hello, puis enregistrez vos modifications.

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click toovote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-hello-layoutcshtml-file"></a>Fichier de mise à jour hello _Layout.cshtml
Ouvrez hello *Views/Shared/_Layout.cshtml* fichier, la disposition par défaut de hello pour l’application ASP.NET de hello.  Remplacez son contenu par les éléments suivants de hello, puis enregistrez vos modifications.

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-hello-votingwebcs-file"></a>Fichier de mise à jour hello VotingWeb.cs
Ouvrez hello *VotingWeb.cs* fichier, lequel crée hello ASP.NET Core WebHost à l’intérieur d’un service sans état hello à l’aide du serveur web de WebListener hello.  Ajouter hello `using System.Net.Http;` haut toohello directive du fichier de hello.  Remplacez hello `CreateServiceInstanceListeners()` fonctionne avec les éléments suivants de hello, puis enregistrez vos modifications.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-hello-votescontrollercs-file"></a>Ajouter le fichier de VotesController.cs hello
Ajoutez un contrôleur qui définit les actions de vote. Avec le bouton droit sur hello **contrôleurs** dossier, puis sélectionnez **Ajouter -> Nouveau-élément > classe**.  Nommez le fichier hello « VotesController.cs » et cliquez sur **ajouter**.  Remplacez le contenu du fichier hello par qui suit hello, puis enregistrez vos modifications.  Plus tard, dans [fichier de mise à jour hello VotesController.cs](#updatevotecontroller_anchor), ce fichier sera modifié tooread et écrire les données de votantes du service principal de hello.  Pour l’instant, le contrôleur de hello retourne la vue de toohello de données de chaîne statique.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-hello-application-locally"></a>Déployer et exécuter des application hello localement
Vous pouvez maintenant continuer et exécuter l’application hello. Dans Visual Studio, appuyez sur `F5` application hello de toodeploy pour le débogage. La commande `F5` échoue si vous n’avez pas précédemment ouvert Visual Studio en tant qu’**administrateur**.

> [!NOTE]
> Hello la première fois que vous exécutez et déployez l’application hello localement, Visual Studio crée un cluster local pour le débogage.  La création de cluster peut prendre un certain temps. état de la création de cluster Hello s’affiche dans la fenêtre de sortie de Visual Studio hello.

À ce stade, votre application web doit ressembler à ceci :

![ASP.NET Core frontal](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

toostop de débogage de l’application hello, revenir en arrière tooVisual Studio, puis appuyez sur **MAJ + F5**.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>Ajouter une application de tooyour avec état service principal
Maintenant que nous avons un service de l’API Web ASP.NET en cours d’exécution dans notre application, commençons et ajoutez un toostore avec état service fiable des données dans notre application.

L’infrastructure de service vous permet de tooconsistently et stocker vos données directement à l’intérieur de votre service à l’aide de collections fiables en toute fiabilité. Collections fiables sont un ensemble de classes de collection hautement disponible et fiable qui sont familier tooanyone qui a utilisé des collections de c#.

Dans ce didacticiel, vous créez un service qui stocke une valeur de compteur dans une collection fiable.

1. Dans l’Explorateur de solutions, cliquez sur **Services** dans hello du projet d’application et choisissez **Ajouter > nouveau Service Service Fabric**.
   
    ![Ajout d’une application de service tooan existant](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. Bonjour **nouveau Service Service Fabric** boîte de dialogue, choisissez **Stateful ASP.NET Core**et le nom hello service **VotingData** et appuyez sur **OK**.

    ![Boîte de dialogue Nouveau service dans Visual Studio.](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    Une fois votre projet de service créé, votre application contient deux services. À mesure que vous toobuild votre application, vous pouvez ajouter d’autres services Bonjour identique. Chacun peut être mis à niveau et faire l'objet d'un contrôle de version indépendamment.

3. page suivante de Hello fournit un ensemble d’ASP.NET Core modèles de projet. Pour ce didacticiel, sélectionnez **API web**.

    ![Choisir le type de projet ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio crée un projet de service et l’affiche dans l’Explorateur de solutions.

    ![Explorateur de solutions](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Ajouter le fichier de VoteDataController.cs hello

Bonjour **VotingData** avec le bouton de projet sur hello **contrôleurs** dossier, puis sélectionnez **Ajouter -> Nouveau-élément > classe**. Nommez le fichier hello « VoteDataController.cs » et cliquez sur **ajouter**. Remplacez le contenu du fichier hello par qui suit hello, puis enregistrez vos modifications.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-hello-services"></a>Connecter les services de hello
Dans cette étape, nous seront hello deux services de connexion et hello frontal Web application obtenir et définir les informations à partir du service principal de hello de vote.

Service Fabric fournit une flexibilité complète sur votre façon de communiquer avec Reliable Services. Dans une même application, vous pouvez avoir des services qui sont accessibles via TCP, d’autres services accessibles via une API REST HTTP et encore d’autres services accessibles via des sockets web. Pour plus d’informations sur les options hello disponibles et les inconvénients hello, consultez [communiquer avec les services](service-fabric-connect-and-communicate-with-services.md).

Dans ce didacticiel, nous utilisons [l’API Web ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>Fichier de mise à jour hello VotesController.cs
Bonjour **VotingWeb** projet, ouvrez hello *Controllers/VotesController.cs* fichier.  Remplacez hello `VotesController` classe contenu de définition par hello qui suit, puis enregistrez vos modifications.

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-hello-voting-sample-application"></a>Parcourez hello vote exemple d’application
Hello vote application se compose de deux services :
- Web service frontal (VotingWeb) - An ASP.NET Core web service frontal, qui sert de page web de hello et expose web toocommunicate API avec le service principal de hello.
- Le service principal (VotingData)-service web An ASP.NET Core, qui expose un vote de hello API toostore entraîne un dictionnaire fiable rendues persistantes sur disque.

![Diagramme de l’application](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Lorsque vous marquez Bonjour d’application hello suivant se produisent :
1. Un code JavaScript envoie des API du web hello vote demande toohello dans le service frontal hello web comme une demande HTTP PUT.

2. service de Hello web frontal utilise un toolocate proxy et transférer un service de serveur principal de toohello demande HTTP PUT.

3. service principal de Hello accepte la demande entrante de hello et magasins hello mis à jour le résultat dans un dictionnaire fiable, qui obtient les nœuds toomultiple répliquées au sein du cluster de hello et rendues persistantes sur disque. Données de l’application hello toutes les sont stockées dans le cluster de hello, donc aucune base de données n’est nécessaire.

## <a name="debug-in-visual-studio"></a>Déboguer dans Visual Studio
Lors du débogage d’application dans Visual Studio, vous utilisez un cluster de développement Service Fabric local. Vous avez hello option tooadjust votre scénario de tooyour expérience de débogage. Dans cette application, nous stockons les données dans notre service principal à l’aide d’un dictionnaire fiable. Visual Studio supprime l’application hello par défaut lorsque vous arrêtez le débogueur de hello. Suppression de l’application hello entraîne les données hello dans hello principal service tooalso être supprimé. les données de salutation toopersist entre les sessions de débogage, vous pouvez modifier hello **Mode de débogage d’Application** en tant que propriété sur hello **vote** projet dans Visual Studio.

toolook à ce qui se passe dans le code hello, hello complète comme suit :
1. Ouvrez hello **VotesController.cs** de fichiers et de définir un point d’arrêt dans l’API web de hello **Put** méthode (ligne 47) - vous pouvez rechercher des fichiers hello Bonjour l’Explorateur de solutions dans Visual Studio.

2. Ouvrez hello **VoteDataController.cs** de fichiers et de définir un point d’arrêt dans cette API web **Put** (méthode) (ligne 50).

3. Revenir en arrière toohello navigateur et cliquez sur une option de vote ou ajouter une nouvelle option de vote. Vous avez atteint le premier point d’arrêt à la hello dans le contrôleur d’api de hello web frontal.
    
    1. Il s’agit où hello JavaScript dans le navigateur de hello envoie un contrôleur d’API web demande toohello dans le service frontal hello.
    
    ![Ajouter un service de vote frontend](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Tout d’abord, nous construisons hello URL toohello ReverseProxy pour notre service principal **(1)**.
    3. Puis nous envoyer hello la demande HTTP PUT toohello ReverseProxy **(2)**.
    4. Enfin hello nous retourner hello réponse à partir du client de toohello hello service principal **(3)**.

4. Appuyez sur **F5** toocontinue
    1. Vous êtes maintenant au point d’arrêt hello dans le service principal hello.
    
    ![Ajouter un service de vote backend](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. Dans la première ligne de hello dans la méthode hello **(1)** , nous utilisons hello `StateManager` tooget ou ajoutez un dictionnaire fiable appelé `counts`.
    3. Toutes les interactions avec des valeurs d’un dictionnaire fiable requièrent une transaction. Cette instruction using **(2)** crée cette transaction.
    4. Transaction de hello, nous puis mettre à jour valeur clé hello des hello vote option hello et validations hello opération **(3)**. Une fois la validation de hello méthode est retournée, hello données sont mise à jour dans le dictionnaire de hello et répliquées tooother des nœuds de cluster de hello. les données de salutation sont maintenant stockées en toute sécurité dans un cluster de hello et service principal de hello peut échouer sur les nœuds tooother, que les données hello disponibles.
5. Appuyez sur **F5** toocontinue

hello toostop session, appuyez sur le débogage **MAJ + F5**.


## <a name="next-steps"></a>Étapes suivantes
Dans cette partie du didacticiel de hello, vous avez appris comment :

> [!div class="checklist"]
> * Créer un service API Web ASP.NET Core en tant que service fiable avec état
> * Créer un service d’application Web ASP.NET Core en tant que service web sans état
> * Utilisez hello proxy inverse toocommunicate avec un service avec état hello

Avance toohello étape suivante du didacticiel :
> [!div class="nextstepaction"]
> [Déployer hello application tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md)
