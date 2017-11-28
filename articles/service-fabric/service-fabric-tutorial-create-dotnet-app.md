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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="4c129-103">Créer et déployer une application avec un service frontal API Web ASP.NET Core et un service principal avec état</span><span class="sxs-lookup"><span data-stu-id="4c129-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="4c129-104">Ce didacticiel est la première partie d’une série d’étapes.</span><span class="sxs-lookup"><span data-stu-id="4c129-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="4c129-105">Vous allez apprendre comment toocreate une application Azure Service Fabric avec un avant de l’API Web ASP.NET principale mettre fin et un toostore avec état service principal de vos données.</span><span class="sxs-lookup"><span data-stu-id="4c129-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="4c129-106">Lorsque vous avez terminé, vous disposez d’une application de vote avec un serveur web ASP.NET Core frontal qui enregistre les résultats de vote dans un service principal avec état dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="4c129-107">Si vous ne souhaitez pas toomanually créer hello vote application, vous pouvez [télécharger le code source de hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) pour hello terminé l’application et passer trop[guident hello vote exemple d’application](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="4c129-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![Diagramme de l’application](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="4c129-109">Dans la première partie de la série de hello, vous apprenez comment :</span><span class="sxs-lookup"><span data-stu-id="4c129-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4c129-110">Créer un service API Web ASP.NET Core en tant que service fiable avec état</span><span class="sxs-lookup"><span data-stu-id="4c129-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="4c129-111">Créer un service d’application Web ASP.NET Core en tant que service web sans état</span><span class="sxs-lookup"><span data-stu-id="4c129-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="4c129-112">Utilisez hello proxy inverse toocommunicate avec un service avec état hello</span><span class="sxs-lookup"><span data-stu-id="4c129-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="4c129-113">Cette série de didacticiels vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c129-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="4c129-114">Créer une application .NET Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4c129-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="4c129-115">Déployer le cluster de l’application hello tooa à distance</span><span class="sxs-lookup"><span data-stu-id="4c129-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="4c129-116">Configurer l’intégration et le déploiement continus à l’aide de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4c129-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="4c129-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4c129-117">Prerequisites</span></span>
<span data-ttu-id="4c129-118">Avant de commencer ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="4c129-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="4c129-119">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="4c129-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="4c129-120">[Installer Visual Studio 2017](https://www.visualstudio.com/) et installer hello **le développement Azure** et **développement web ASP.NET et** les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="4c129-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="4c129-121">Installer hello SDK de l’infrastructure de Service</span><span class="sxs-lookup"><span data-stu-id="4c129-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="4c129-122">Créer un service API Web ASP.NET en tant que service fiable</span><span class="sxs-lookup"><span data-stu-id="4c129-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="4c129-123">Tout d’abord, créez hello web frontal de hello vote application à l’aide d’ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="4c129-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="4c129-124">ASP.NET Core est une infrastructure de développement web léger et inter-plateformes que vous pouvez utiliser l’interface utilisateur de web moderne toocreate et API web.</span><span class="sxs-lookup"><span data-stu-id="4c129-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="4c129-125">tooget bien comprendre comment ASP.NET Core s’intègre à l’infrastructure de Service, nous recommandons fortement de lire via hello [ASP.NET Core dans Service des Services de Fabric fiables](service-fabric-reliable-services-communication-aspnetcore.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4c129-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="4c129-126">Pour l’instant, vous pouvez suivre ce didacticiel tooget démarré rapidement.</span><span class="sxs-lookup"><span data-stu-id="4c129-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="4c129-127">toolearn savoir plus sur ASP.NET Core, consultez hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="4c129-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="4c129-128">Ce didacticiel est basé sur hello [ASP.NET Core tools pour Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="4c129-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="4c129-129">outils du .NET Core Hello pour Visual Studio 2015 sont plus en cours de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="4c129-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="4c129-130">Lancez Visual Studio en tant qu’**administrateur**.</span><span class="sxs-lookup"><span data-stu-id="4c129-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="4c129-131">Créez un projet en sélectionnant **Fichier**->**Nouveau**->**Projet**.</span><span class="sxs-lookup"><span data-stu-id="4c129-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="4c129-132">Bonjour **nouveau projet** boîte de dialogue, choisissez **Cloud > Application Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="4c129-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="4c129-133">Nommez l’application hello **vote** et appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c129-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Boîte de dialogue Nouveau projet dans Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="4c129-135">Sur hello **nouveau Service Service Fabric** choisissez **sans état ASP.NET Core**et le nom de votre service **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="4c129-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Choix du service web ASP.NET dans la boîte de dialogue hello nouveau service](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="4c129-137">page suivante de Hello fournit un ensemble d’ASP.NET Core modèles de projet.</span><span class="sxs-lookup"><span data-stu-id="4c129-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="4c129-138">Pour ce didacticiel, sélectionnez **Application web**.</span><span class="sxs-lookup"><span data-stu-id="4c129-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![Choisir le type de projet ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="4c129-140">Visual Studio crée une application et un projet de service, et les affiche dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="4c129-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Explorateur de solutions après la création de l’application avec un service API Web ASP.NET Core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="4c129-142">Ajouter un service de VotingWeb toohello AngularJS</span><span class="sxs-lookup"><span data-stu-id="4c129-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="4c129-143">Ajouter [AngularJS](http://angularjs.org/) service tooyour à l’aide intégrée de hello [Bower prise en charge](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="4c129-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="4c129-144">Ouvrez *bower.json* et ajoutez des entrées pour angular et angular-bootstrap, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4c129-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

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
<span data-ttu-id="4c129-145">Lors de l’enregistrement hello *bower.json* fichier angulaire est installé dans votre projet *wwwroot/lib* dossier.</span><span class="sxs-lookup"><span data-stu-id="4c129-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="4c129-146">En outre, il est répertorié dans hello *dépendances/Bower* dossier.</span><span class="sxs-lookup"><span data-stu-id="4c129-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="4c129-147">Fichier de mise à jour hello site.js</span><span class="sxs-lookup"><span data-stu-id="4c129-147">Update hello site.js file</span></span>
<span data-ttu-id="4c129-148">Ouvrez hello *wwwroot/js/site.js* fichier.</span><span class="sxs-lookup"><span data-stu-id="4c129-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="4c129-149">Remplacez son contenu par hello JavaScript utilisé par les modes d’accueil hello :</span><span class="sxs-lookup"><span data-stu-id="4c129-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

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

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="4c129-150">Fichier de mise à jour hello Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="4c129-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="4c129-151">Ouvrez hello *Views/Home/Index.cshtml* fichier, hello vue spécifique toohello accueil du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="4c129-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="4c129-152">Remplacez son contenu par les éléments suivants de hello, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4c129-152">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="4c129-153">Fichier de mise à jour hello _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="4c129-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="4c129-154">Ouvrez hello *Views/Shared/_Layout.cshtml* fichier, la disposition par défaut de hello pour l’application ASP.NET de hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="4c129-155">Remplacez son contenu par les éléments suivants de hello, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4c129-155">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="4c129-156">Fichier de mise à jour hello VotingWeb.cs</span><span class="sxs-lookup"><span data-stu-id="4c129-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="4c129-157">Ouvrez hello *VotingWeb.cs* fichier, lequel crée hello ASP.NET Core WebHost à l’intérieur d’un service sans état hello à l’aide du serveur web de WebListener hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="4c129-158">Ajouter hello `using System.Net.Http;` haut toohello directive du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="4c129-159">Remplacez hello `CreateServiceInstanceListeners()` fonctionne avec les éléments suivants de hello, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4c129-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

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

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="4c129-160">Ajouter le fichier de VotesController.cs hello</span><span class="sxs-lookup"><span data-stu-id="4c129-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="4c129-161">Ajoutez un contrôleur qui définit les actions de vote.</span><span class="sxs-lookup"><span data-stu-id="4c129-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="4c129-162">Avec le bouton droit sur hello **contrôleurs** dossier, puis sélectionnez **Ajouter -> Nouveau-élément > classe**.</span><span class="sxs-lookup"><span data-stu-id="4c129-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="4c129-163">Nommez le fichier hello « VotesController.cs » et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4c129-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="4c129-164">Remplacez le contenu du fichier hello par qui suit hello, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4c129-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="4c129-165">Plus tard, dans [fichier de mise à jour hello VotesController.cs](#updatevotecontroller_anchor), ce fichier sera modifié tooread et écrire les données de votantes du service principal de hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="4c129-166">Pour l’instant, le contrôleur de hello retourne la vue de toohello de données de chaîne statique.</span><span class="sxs-lookup"><span data-stu-id="4c129-166">For now, hello controller returns static string data toohello view.</span></span>

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



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="4c129-167">Déployer et exécuter des application hello localement</span><span class="sxs-lookup"><span data-stu-id="4c129-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="4c129-168">Vous pouvez maintenant continuer et exécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="4c129-169">Dans Visual Studio, appuyez sur `F5` application hello de toodeploy pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="4c129-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="4c129-170">La commande `F5` échoue si vous n’avez pas précédemment ouvert Visual Studio en tant qu’**administrateur**.</span><span class="sxs-lookup"><span data-stu-id="4c129-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="4c129-171">Hello la première fois que vous exécutez et déployez l’application hello localement, Visual Studio crée un cluster local pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="4c129-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="4c129-172">La création de cluster peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="4c129-172">Cluster creation may take some time.</span></span> <span data-ttu-id="4c129-173">état de la création de cluster Hello s’affiche dans la fenêtre de sortie de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="4c129-174">À ce stade, votre application web doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4c129-174">At this point, your web app should look like this:</span></span>

![ASP.NET Core frontal](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="4c129-176">toostop de débogage de l’application hello, revenir en arrière tooVisual Studio, puis appuyez sur **MAJ + F5**.</span><span class="sxs-lookup"><span data-stu-id="4c129-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="4c129-177">Ajouter une application de tooyour avec état service principal</span><span class="sxs-lookup"><span data-stu-id="4c129-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="4c129-178">Maintenant que nous avons un service de l’API Web ASP.NET en cours d’exécution dans notre application, commençons et ajoutez un toostore avec état service fiable des données dans notre application.</span><span class="sxs-lookup"><span data-stu-id="4c129-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="4c129-179">L’infrastructure de service vous permet de tooconsistently et stocker vos données directement à l’intérieur de votre service à l’aide de collections fiables en toute fiabilité.</span><span class="sxs-lookup"><span data-stu-id="4c129-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="4c129-180">Collections fiables sont un ensemble de classes de collection hautement disponible et fiable qui sont familier tooanyone qui a utilisé des collections de c#.</span><span class="sxs-lookup"><span data-stu-id="4c129-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="4c129-181">Dans ce didacticiel, vous créez un service qui stocke une valeur de compteur dans une collection fiable.</span><span class="sxs-lookup"><span data-stu-id="4c129-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="4c129-182">Dans l’Explorateur de solutions, cliquez sur **Services** dans hello du projet d’application et choisissez **Ajouter > nouveau Service Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="4c129-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Ajout d’une application de service tooan existant](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="4c129-184">Bonjour **nouveau Service Service Fabric** boîte de dialogue, choisissez **Stateful ASP.NET Core**et le nom hello service **VotingData** et appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c129-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Boîte de dialogue Nouveau service dans Visual Studio.](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="4c129-186">Une fois votre projet de service créé, votre application contient deux services.</span><span class="sxs-lookup"><span data-stu-id="4c129-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="4c129-187">À mesure que vous toobuild votre application, vous pouvez ajouter d’autres services Bonjour identique.</span><span class="sxs-lookup"><span data-stu-id="4c129-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="4c129-188">Chacun peut être mis à niveau et faire l'objet d'un contrôle de version indépendamment.</span><span class="sxs-lookup"><span data-stu-id="4c129-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="4c129-189">page suivante de Hello fournit un ensemble d’ASP.NET Core modèles de projet.</span><span class="sxs-lookup"><span data-stu-id="4c129-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="4c129-190">Pour ce didacticiel, sélectionnez **API web**.</span><span class="sxs-lookup"><span data-stu-id="4c129-190">For this tutorial, choose **Web API**.</span></span>

    ![Choisir le type de projet ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="4c129-192">Visual Studio crée un projet de service et l’affiche dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="4c129-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Explorateur de solutions](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="4c129-194">Ajouter le fichier de VoteDataController.cs hello</span><span class="sxs-lookup"><span data-stu-id="4c129-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="4c129-195">Bonjour **VotingData** avec le bouton de projet sur hello **contrôleurs** dossier, puis sélectionnez **Ajouter -> Nouveau-élément > classe**.</span><span class="sxs-lookup"><span data-stu-id="4c129-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="4c129-196">Nommez le fichier hello « VoteDataController.cs » et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4c129-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="4c129-197">Remplacez le contenu du fichier hello par qui suit hello, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4c129-197">Replace hello file contents with hello following, then save your changes.</span></span>

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


## <a name="connect-hello-services"></a><span data-ttu-id="4c129-198">Connecter les services de hello</span><span class="sxs-lookup"><span data-stu-id="4c129-198">Connect hello services</span></span>
<span data-ttu-id="4c129-199">Dans cette étape, nous seront hello deux services de connexion et hello frontal Web application obtenir et définir les informations à partir du service principal de hello de vote.</span><span class="sxs-lookup"><span data-stu-id="4c129-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="4c129-200">Service Fabric fournit une flexibilité complète sur votre façon de communiquer avec Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="4c129-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="4c129-201">Dans une même application, vous pouvez avoir des services qui sont accessibles via TCP,</span><span class="sxs-lookup"><span data-stu-id="4c129-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="4c129-202">d’autres services accessibles via une API REST HTTP et encore d’autres services accessibles via des sockets web.</span><span class="sxs-lookup"><span data-stu-id="4c129-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="4c129-203">Pour plus d’informations sur les options hello disponibles et les inconvénients hello, consultez [communiquer avec les services](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="4c129-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="4c129-204">Dans ce didacticiel, nous utilisons [l’API Web ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="4c129-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="4c129-205">Fichier de mise à jour hello VotesController.cs</span><span class="sxs-lookup"><span data-stu-id="4c129-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="4c129-206">Bonjour **VotingWeb** projet, ouvrez hello *Controllers/VotesController.cs* fichier.</span><span class="sxs-lookup"><span data-stu-id="4c129-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="4c129-207">Remplacez hello `VotesController` classe contenu de définition par hello qui suit, puis enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4c129-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

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

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="4c129-208">Parcourez hello vote exemple d’application</span><span class="sxs-lookup"><span data-stu-id="4c129-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="4c129-209">Hello vote application se compose de deux services :</span><span class="sxs-lookup"><span data-stu-id="4c129-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="4c129-210">Web service frontal (VotingWeb) - An ASP.NET Core web service frontal, qui sert de page web de hello et expose web toocommunicate API avec le service principal de hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="4c129-211">Le service principal (VotingData)-service web An ASP.NET Core, qui expose un vote de hello API toostore entraîne un dictionnaire fiable rendues persistantes sur disque.</span><span class="sxs-lookup"><span data-stu-id="4c129-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Diagramme de l’application](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="4c129-213">Lorsque vous marquez Bonjour d’application hello suivant se produisent :</span><span class="sxs-lookup"><span data-stu-id="4c129-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="4c129-214">Un code JavaScript envoie des API du web hello vote demande toohello dans le service frontal hello web comme une demande HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="4c129-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="4c129-215">service de Hello web frontal utilise un toolocate proxy et transférer un service de serveur principal de toohello demande HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="4c129-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="4c129-216">service principal de Hello accepte la demande entrante de hello et magasins hello mis à jour le résultat dans un dictionnaire fiable, qui obtient les nœuds toomultiple répliquées au sein du cluster de hello et rendues persistantes sur disque.</span><span class="sxs-lookup"><span data-stu-id="4c129-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="4c129-217">Données de l’application hello toutes les sont stockées dans le cluster de hello, donc aucune base de données n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4c129-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="4c129-218">Déboguer dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4c129-218">Debug in Visual Studio</span></span>
<span data-ttu-id="4c129-219">Lors du débogage d’application dans Visual Studio, vous utilisez un cluster de développement Service Fabric local.</span><span class="sxs-lookup"><span data-stu-id="4c129-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="4c129-220">Vous avez hello option tooadjust votre scénario de tooyour expérience de débogage.</span><span class="sxs-lookup"><span data-stu-id="4c129-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="4c129-221">Dans cette application, nous stockons les données dans notre service principal à l’aide d’un dictionnaire fiable.</span><span class="sxs-lookup"><span data-stu-id="4c129-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="4c129-222">Visual Studio supprime l’application hello par défaut lorsque vous arrêtez le débogueur de hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="4c129-223">Suppression de l’application hello entraîne les données hello dans hello principal service tooalso être supprimé.</span><span class="sxs-lookup"><span data-stu-id="4c129-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="4c129-224">les données de salutation toopersist entre les sessions de débogage, vous pouvez modifier hello **Mode de débogage d’Application** en tant que propriété sur hello **vote** projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c129-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="4c129-225">toolook à ce qui se passe dans le code hello, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="4c129-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="4c129-226">Ouvrez hello **VotesController.cs** de fichiers et de définir un point d’arrêt dans l’API web de hello **Put** méthode (ligne 47) - vous pouvez rechercher des fichiers hello Bonjour l’Explorateur de solutions dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c129-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="4c129-227">Ouvrez hello **VoteDataController.cs** de fichiers et de définir un point d’arrêt dans cette API web **Put** (méthode) (ligne 50).</span><span class="sxs-lookup"><span data-stu-id="4c129-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="4c129-228">Revenir en arrière toohello navigateur et cliquez sur une option de vote ou ajouter une nouvelle option de vote.</span><span class="sxs-lookup"><span data-stu-id="4c129-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="4c129-229">Vous avez atteint le premier point d’arrêt à la hello dans le contrôleur d’api de hello web frontal.</span><span class="sxs-lookup"><span data-stu-id="4c129-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="4c129-230">Il s’agit où hello JavaScript dans le navigateur de hello envoie un contrôleur d’API web demande toohello dans le service frontal hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Ajouter un service de vote frontend](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="4c129-232">Tout d’abord, nous construisons hello URL toohello ReverseProxy pour notre service principal **(1)**.</span><span class="sxs-lookup"><span data-stu-id="4c129-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="4c129-233">Puis nous envoyer hello la demande HTTP PUT toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="4c129-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="4c129-234">Enfin hello nous retourner hello réponse à partir du client de toohello hello service principal **(3)**.</span><span class="sxs-lookup"><span data-stu-id="4c129-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="4c129-235">Appuyez sur **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="4c129-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="4c129-236">Vous êtes maintenant au point d’arrêt hello dans le service principal hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![Ajouter un service de vote backend](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="4c129-238">Dans la première ligne de hello dans la méthode hello **(1)** , nous utilisons hello `StateManager` tooget ou ajoutez un dictionnaire fiable appelé `counts`.</span><span class="sxs-lookup"><span data-stu-id="4c129-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="4c129-239">Toutes les interactions avec des valeurs d’un dictionnaire fiable requièrent une transaction. Cette instruction using **(2)** crée cette transaction.</span><span class="sxs-lookup"><span data-stu-id="4c129-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="4c129-240">Transaction de hello, nous puis mettre à jour valeur clé hello des hello vote option hello et validations hello opération **(3)**.</span><span class="sxs-lookup"><span data-stu-id="4c129-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="4c129-241">Une fois la validation de hello méthode est retournée, hello données sont mise à jour dans le dictionnaire de hello et répliquées tooother des nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4c129-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="4c129-242">les données de salutation sont maintenant stockées en toute sécurité dans un cluster de hello et service principal de hello peut échouer sur les nœuds tooother, que les données hello disponibles.</span><span class="sxs-lookup"><span data-stu-id="4c129-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="4c129-243">Appuyez sur **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="4c129-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="4c129-244">hello toostop session, appuyez sur le débogage **MAJ + F5**.</span><span class="sxs-lookup"><span data-stu-id="4c129-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4c129-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c129-245">Next steps</span></span>
<span data-ttu-id="4c129-246">Dans cette partie du didacticiel de hello, vous avez appris comment :</span><span class="sxs-lookup"><span data-stu-id="4c129-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4c129-247">Créer un service API Web ASP.NET Core en tant que service fiable avec état</span><span class="sxs-lookup"><span data-stu-id="4c129-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="4c129-248">Créer un service d’application Web ASP.NET Core en tant que service web sans état</span><span class="sxs-lookup"><span data-stu-id="4c129-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="4c129-249">Utilisez hello proxy inverse toocommunicate avec un service avec état hello</span><span class="sxs-lookup"><span data-stu-id="4c129-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="4c129-250">Avance toohello étape suivante du didacticiel :</span><span class="sxs-lookup"><span data-stu-id="4c129-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4c129-251">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="4c129-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
