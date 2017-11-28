---
title: "aaaGet démarrer avec ASP.NET dans le Service d’applications et les applications API | Documents Microsoft"
description: "Découvrez comment toocreate, déployer et utiliser une application API ASP.NET dans Azure App Service, à l’aide de Visual Studio 2015."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="a969b-103">Prise en main d’API Apps, d’ASP.NET et de Swagger dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a969b-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="a969b-104">Il est tout d’abord hello dans une série de didacticiels qui montrent comment toouse les fonctionnalités d’Azure App Service qui sont utiles pour le développement et l’hébergement d’une API RESTful.</span><span class="sxs-lookup"><span data-stu-id="a969b-104">This is hello first in a series of tutorials that show how toouse features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="a969b-105">Ce didacticiel décrit la prise en charge des métadonnées des API au format Swagger.</span><span class="sxs-lookup"><span data-stu-id="a969b-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="a969b-106">Vous apprendrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a969b-106">You'll learn:</span></span>

* <span data-ttu-id="a969b-107">Comment toocreate et déployer [applications API](app-service-api-apps-why-best-platform.md) dans Azure App Service à l’aide des outils intégrés à Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a969b-107">How toocreate and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="a969b-108">Comment empaqueter de découverte tooautomate API à l’aide de hello Swashbuckle NuGet toodynamically génèrent des métadonnées de l’API de Swagger.</span><span class="sxs-lookup"><span data-stu-id="a969b-108">How tooautomate API discovery by using hello Swashbuckle NuGet package toodynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="a969b-109">Comment tooautomatically de métadonnées Swagger des API toouse générer du code client pour une application API.</span><span class="sxs-lookup"><span data-stu-id="a969b-109">How toouse Swagger API metadata tooautomatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="a969b-110">Vue d’ensemble de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="a969b-110">Sample application overview</span></span>
<span data-ttu-id="a969b-111">Dans ce didacticiel, vous travaillez avec un exemple d’application de liste des tâches simples.</span><span class="sxs-lookup"><span data-stu-id="a969b-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="a969b-112">application Hello a frontal une seule page application (SPA), une couche intermédiaire d’API Web ASP.NET et une couche de données d’API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a969b-112">hello application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Exemple de schéma d’application API Apps](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="a969b-114">Voici une capture d’écran de hello [AngularJS](https://angularjs.org/) front-end.</span><span class="sxs-lookup"><span data-stu-id="a969b-114">Here's a screen shot of hello [AngularJS](https://angularjs.org/) front end.</span></span>

![Applications API exemple application toodo de liste](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="a969b-116">Hello solution Visual Studio comprend trois projets :</span><span class="sxs-lookup"><span data-stu-id="a969b-116">hello Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="a969b-117">**ToDoListAngular** -frontal hello : un SPA AngularJS qui appelle intermédiaire hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-117">**ToDoListAngular** - hello front end: an AngularJS SPA that calls hello middle tier.</span></span>
* <span data-ttu-id="a969b-118">**ToDoListAPI** -intermédiaire hello : un projet d’API Web ASP.NET qui appelle couche de données hello tooperform les opérations CRUD sur les éléments d’action.</span><span class="sxs-lookup"><span data-stu-id="a969b-118">**ToDoListAPI** - hello middle tier: an ASP.NET Web API project that calls hello data tier tooperform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="a969b-119">**ToDoListDataAPI** -niveau de données hello : un projet d’API Web ASP.NET qui exécute des opérations CRUD sur les éléments d’action.</span><span class="sxs-lookup"><span data-stu-id="a969b-119">**ToDoListDataAPI** - hello data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="a969b-120">architecture à trois niveaux de Hello est un des nombreux architectures que vous pouvez implémenter à l’aide des applications API et êtes utilisé ici uniquement à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="a969b-120">hello three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="a969b-121">code Hello dans chaque niveau est aussi simple que les fonctionnalités d’applications API toodemonstrate possible ; par exemple, la couche de données hello utilise mémoire du serveur plutôt que dans une base de données comme mécanisme de persistance.</span><span class="sxs-lookup"><span data-stu-id="a969b-121">hello code in each tier is as simple as possible toodemonstrate API Apps features; for example, hello data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="a969b-122">Une fois ce didacticiel, vous aurez deux projets d’API Web hello haut et en cours d’exécution dans le cloud hello dans les applications de l’API de Service d’application.</span><span class="sxs-lookup"><span data-stu-id="a969b-122">On completing this tutorial, you'll have hello two Web API projects up and running in hello cloud in App Service API apps.</span></span>

<span data-ttu-id="a969b-123">Hello étape suivante du didacticiel dans la série de hello déploie cloud toohello de hello SPA front-end.</span><span class="sxs-lookup"><span data-stu-id="a969b-123">hello next tutorial in hello series deploys hello SPA front end toohello cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a969b-124">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a969b-124">Prerequisites</span></span>
* <span data-ttu-id="a969b-125">ASP.NET Web API - instructions de didacticiel de hello supposent que vous avez une connaissance élémentaire de la façon toowork avec ASP.NET [API Web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a969b-125">ASP.NET Web API - hello tutorial instructions assume you have a basic knowledge of how toowork with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="a969b-126">Compte Azure : vous pouvez [ouvrir un compte Azure gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) ou [activer les avantages de l’abonnement à Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="a969b-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="a969b-127">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de vous inscrivez pour un compte Azure, accédez trop[Service d’applications essayez](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="a969b-127">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="a969b-128">De là, vous pouvez créer immédiatement une première application temporaire dans App Service. **Aucune carte de crédit** ni aucun engagement ne sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="a969b-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="a969b-129">Visual Studio 2015 avec hello [Azure SDK pour .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK installe Visual Studio 2015 automatiquement si vous n’est pas déjà installé.</span><span class="sxs-lookup"><span data-stu-id="a969b-129">Visual Studio 2015 with hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - hello SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="a969b-130">Dans Visual Studio, cliquez sur Aide -> À propos de Microsoft Visual Studio et vérifiez que « Azure App Service Tools v2.9.1 » ou ultérieur est installé.</span><span class="sxs-lookup"><span data-stu-id="a969b-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Version d’Azure App Service Tools](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="a969b-132">Selon le nombre de dépendances du Kit de développement logiciel hello vous disposez déjà sur votre ordinateur, hello lors de l’installation du SDK peut prendre beaucoup de temps, à partir de plusieurs minutes tooa demi-heure ou plus.</span><span class="sxs-lookup"><span data-stu-id="a969b-132">Depending on how many of hello SDK dependencies you already have on your machine, installing hello SDK could take a long time, from several minutes tooa half hour or more.</span></span>
    > 
    > 

## <a name="download-hello-sample-application"></a><span data-ttu-id="a969b-133">Télécharger l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="a969b-133">Download hello sample application</span></span>
1. <span data-ttu-id="a969b-134">Télécharger hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) référentiel.</span><span class="sxs-lookup"><span data-stu-id="a969b-134">Download hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="a969b-135">Vous pouvez cliquer sur hello **ZIP de téléchargement** bouton ou un clone référentiel hello sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="a969b-135">You can click hello **Download ZIP** button or clone hello repository on your local machine.</span></span>
2. <span data-ttu-id="a969b-136">Ouvrez la solution de ToDoList hello dans Visual Studio 2015 ou 2013.</span><span class="sxs-lookup"><span data-stu-id="a969b-136">Open hello ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="a969b-137">Vous devez tootrust chaque solution.</span><span class="sxs-lookup"><span data-stu-id="a969b-137">You will need tootrust each solution.</span></span>
         <span data-ttu-id="a969b-138">![Avertissement de sécurité](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="a969b-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="a969b-139">Générez les packages NuGet hello hello solution (CTRL + MAJ + B) toorestore.</span><span class="sxs-lookup"><span data-stu-id="a969b-139">Build hello solution (CTRL + SHIFT + B)  toorestore hello NuGet packages.</span></span>
   
    <span data-ttu-id="a969b-140">Si vous souhaitez une application hello toosee opération avant de le déployer, vous pouvez l’exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="a969b-140">If you want toosee hello application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="a969b-141">Assurez-vous que ToDoListDataAPI est votre projet de démarrage et l’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-141">Make sure that ToDoListDataAPI is your startup project and run hello solution.</span></span> <span data-ttu-id="a969b-142">Vous devriez toosee un HTTP 403 erreur dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="a969b-142">You should expect toosee a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="a969b-143">Utiliser l’interface utilisateur et les métadonnées d’API Swagger</span><span class="sxs-lookup"><span data-stu-id="a969b-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="a969b-144">La prise en charge des métadonnées d’API [Swagger](http://swagger.io/) 2.0 est intégrée aux applications API App Service.</span><span class="sxs-lookup"><span data-stu-id="a969b-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="a969b-145">Chaque application API peut spécifier un point de terminaison d’URL qui retourne des métadonnées pour hello API au format JSON de Swagger.</span><span class="sxs-lookup"><span data-stu-id="a969b-145">Each API app can specify a URL endpoint that returns metadata for hello API in Swagger JSON format.</span></span> <span data-ttu-id="a969b-146">Hello retournée à partir de ce point de terminaison de métadonnées peuvent être utilisé de code client toogenerate.</span><span class="sxs-lookup"><span data-stu-id="a969b-146">hello metadata returned from that endpoint can be used toogenerate client code.</span></span>

<span data-ttu-id="a969b-147">Un projet d’API Web ASP.NET peut générer dynamiquement des métadonnées Swagger à l’aide de hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) package NuGet.</span><span class="sxs-lookup"><span data-stu-id="a969b-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="a969b-148">Hello package Swashbuckle NuGet est déjà installé dans les projets ToDoListDataAPI et ToDoListAPI hello que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="a969b-148">hello Swashbuckle NuGet package is already installed in hello ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="a969b-149">Dans cette section du didacticiel de hello, examiner des métadonnées Swagger 2.0 de hello généré, puis essayer un test de l’interface utilisateur qui est basée sur les métadonnées de Swagger hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-149">In this section of hello tutorial, you look at hello generated Swagger 2.0 metadata, and then you try out a test UI that is based on hello Swagger metadata.</span></span>

1. <span data-ttu-id="a969b-150">Définissez hello ToDoListDataAPI projet (**pas** projet ToDoListAPI de hello) en tant que projet de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-150">Set hello ToDoListDataAPI project (**not** hello ToDoListAPI project) as hello startup project.</span></span>
   
    ![Définir ToDoDataAPI comme projet de démarrage](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="a969b-152">Appuyez sur F5 ou cliquez sur **Déboguer > Démarrer le débogage** projet de hello toorun en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="a969b-152">Press F5 or click **Debug > Start Debugging** toorun hello project in debug mode.</span></span>
   
    <span data-ttu-id="a969b-153">navigateur de Hello s’ouvre et affiche la page d’erreur HTTP 403 hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-153">hello browser opens and shows hello HTTP 403 error page.</span></span>
3. <span data-ttu-id="a969b-154">Dans la barre d’adresse de votre navigateur, ajoutez `swagger/docs/v1` fin toohello de ligne de hello, puis appuyez sur retour.</span><span class="sxs-lookup"><span data-stu-id="a969b-154">In your browser address bar, add `swagger/docs/v1` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="a969b-155">(hello URL est `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="a969b-155">(hello URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="a969b-156">Il s’agit d’URL par défaut de hello utilisé par les métadonnées de JSON de 2.0 Swagger Swashbuckle tooreturn pour hello API.</span><span class="sxs-lookup"><span data-stu-id="a969b-156">This is hello default URL used by Swashbuckle tooreturn Swagger 2.0 JSON metadata for hello API.</span></span>
   
    <span data-ttu-id="a969b-157">Si vous utilisez Internet Explorer, hello navigateur vous invite à toodownload une *v1.json* fichier.</span><span class="sxs-lookup"><span data-stu-id="a969b-157">If you're using Internet Explorer, hello browser prompts you toodownload a *v1.json* file.</span></span>
   
    ![Télécharger les métadonnées JSON dans Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="a969b-159">Si vous utilisez Edge, Firefox ou Chrome, navigateur de hello affiche hello JSON dans une fenêtre de navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-159">If you're using Chrome, Firefox, or Edge, hello browser displays hello JSON in hello browser window.</span></span> <span data-ttu-id="a969b-160">Différents navigateurs gèrent différemment les JSON, et la fenêtre du navigateur ne semblent pas exactement comme exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-160">Different browsers handle JSON differently, and your browser window may not look exactly like hello example.</span></span>
   
    ![Métadonnées JSON dans Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="a969b-162">Hello suivant montre hello première section de métadonnées Swagger de hello pour hello API, avec définition hello pour hello Get (méthode).</span><span class="sxs-lookup"><span data-stu-id="a969b-162">hello following sample shows hello first section of hello Swagger metadata for hello API, with hello definition for hello Get method.</span></span> <span data-ttu-id="a969b-163">Ces métadonnées sont le hello lecteurs Swagger interface utilisateur que vous utilisez dans hello comme suit, et que vous l’utilisez dans une section ultérieure de tooautomatically de didacticiel hello générer le code client.</span><span class="sxs-lookup"><span data-stu-id="a969b-163">This metadata is what drives hello Swagger UI that you use in hello following steps, and you use it in a later section of hello tutorial tooautomatically generate client code.</span></span>
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. <span data-ttu-id="a969b-164">Fermez le navigateur de hello et arrêter le débogage de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a969b-164">Close hello browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="a969b-165">Bonjour ToDoListDataAPI projet **l’Explorateur de solutions**, ouvrez hello *App_Start\SwaggerConfig.cs* le fichier, puis de défilement vers le bas tooline 174 et ne commentez pas hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="a969b-165">In hello ToDoListDataAPI project in **Solution Explorer**, open hello *App_Start\SwaggerConfig.cs* file, then scroll down tooline 174 and uncomment hello following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="a969b-166">Hello *SwaggerConfig.cs* fichier est créé lorsque vous installez le package de Swashbuckle hello dans un projet.</span><span class="sxs-lookup"><span data-stu-id="a969b-166">hello *SwaggerConfig.cs* file is created when you install hello Swashbuckle package in a project.</span></span> <span data-ttu-id="a969b-167">fichier de Hello fournit un certain nombre de façons tooconfigure Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="a969b-167">hello file provides a number of ways tooconfigure Swashbuckle.</span></span>
   
    <span data-ttu-id="a969b-168">code Hello que vous avez supprimées hello Active Swagger interface utilisateur que vous utilisez dans hello suivant les étapes.</span><span class="sxs-lookup"><span data-stu-id="a969b-168">hello code you've uncommented enables hello Swagger UI that you use in hello following steps.</span></span> <span data-ttu-id="a969b-169">Lorsque vous créez un projet d’API Web à l’aide du modèle de projet application hello API, ce code est mis en commentaire par défaut en tant que mesure de sécurité.</span><span class="sxs-lookup"><span data-stu-id="a969b-169">When you create a Web API project by using hello API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="a969b-170">Réexécutez hello projet.</span><span class="sxs-lookup"><span data-stu-id="a969b-170">Run hello project again.</span></span>
7. <span data-ttu-id="a969b-171">Dans la barre d’adresse de votre navigateur, ajoutez `swagger` fin toohello de ligne de hello, puis appuyez sur retour.</span><span class="sxs-lookup"><span data-stu-id="a969b-171">In your browser address bar, add `swagger` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="a969b-172">(hello URL est `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="a969b-172">(hello URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="a969b-173">Lorsque la page de l’interface utilisateur de Swagger hello s’affiche, cliquez sur **ToDoList** méthodes de hello toosee disponibles.</span><span class="sxs-lookup"><span data-stu-id="a969b-173">When hello Swagger UI page appears, click **ToDoList** toosee hello methods available.</span></span>
   
    ![Méthodes disponibles dans l’interface utilisateur Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="a969b-175">Commencez par cliquer sur hello **obtenir** bouton dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-175">Click hello first **Get** button in hello list.</span></span>
10. <span data-ttu-id="a969b-176">Bonjour **paramètres** section, entrez un astérisque en tant que valeur hello Hello `owner` paramètre, puis cliquez sur **essayez-le**.</span><span class="sxs-lookup"><span data-stu-id="a969b-176">In hello **Parameters** section, enter an asterisk as hello value of hello `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="a969b-177">Lorsque vous ajoutez l’authentification dans des didacticiels ultérieurs, intermédiaire hello fournira la couche de données hello toohello de l’ID réel de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a969b-177">When you add authentication in later tutorials, hello middle tier will provide hello actual user ID toohello data tier.</span></span> <span data-ttu-id="a969b-178">Pour l’instant, toutes les tâches ont astérisque en tant que leur ID de propriétaire, tandis que l’application hello s’exécute sans activer l’authentification.</span><span class="sxs-lookup"><span data-stu-id="a969b-178">For now, all tasks will have asterisk as their owner ID while hello application runs without authentication enabled.</span></span>
    
    ![Essayer l’interface utilisateur Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="a969b-180">Hello Swagger de l’interface utilisateur appelle la méthode Get de la liste des tâches de hello et affiche le code de réponse hello et résultats JSON.</span><span class="sxs-lookup"><span data-stu-id="a969b-180">hello Swagger UI calls hello ToDoList Get method and displays hello response code and JSON results.</span></span>
    
    ![Essayer l’interface utilisateur Swagger - Résultats](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="a969b-182">Cliquez sur **Post**, puis cliquez sur la zone hello sous **schéma de modèle**.</span><span class="sxs-lookup"><span data-stu-id="a969b-182">Click **Post**, and then click hello box under **Model Schema**.</span></span>
    
    <span data-ttu-id="a969b-183">En cliquant sur hello modèle schéma prefills hello zone d’entrée où vous pouvez spécifier la valeur du paramètre hello pour hello méthode Post.</span><span class="sxs-lookup"><span data-stu-id="a969b-183">Clicking hello model schema prefills hello input box where you can specify hello parameter value for hello Post method.</span></span> <span data-ttu-id="a969b-184">(Si cela ne fonctionne pas dans Internet Explorer, utilisez un autre navigateur ou entrez la valeur du paramètre hello manuellement à l’étape suivante de hello).</span><span class="sxs-lookup"><span data-stu-id="a969b-184">(If this doesn't work in Internet Explorer, use a different browser or enter hello parameter value manually in hello next step.)</span></span>  
    
    ![Essayer l’interface utilisateur Swagger - Publication](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="a969b-186">Hello modification JSON Bonjour `todo` paramètre d’entrée afin qu’il ressemble à hello l’exemple suivant, ou les remplacer par votre propre texte de description :</span><span class="sxs-lookup"><span data-stu-id="a969b-186">Change hello JSON in hello `todo` parameter input box so that it looks like hello following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="a969b-187">Cliquez sur **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="a969b-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="a969b-188">Hello ToDoList API renvoie un code de réponse HTTP 204 qui indique la réussite.</span><span class="sxs-lookup"><span data-stu-id="a969b-188">hello ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="a969b-189">Commencez par cliquer sur hello **obtenir** bouton, puis cliquez dans cette section de la page de hello hello **essayez-le** bouton.</span><span class="sxs-lookup"><span data-stu-id="a969b-189">Click hello first **Get** button, and then in that section of hello page click hello **Try it out** button.</span></span>
    
    <span data-ttu-id="a969b-190">Hello réponse de la méthode Get inclut désormais un nouvel élément de toodo hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-190">hello Get method response now includes hello new toodo item.</span></span>
15. <span data-ttu-id="a969b-191">Facultatif : Essayez également hello Put, Delete et obtenir par les méthodes de code.</span><span class="sxs-lookup"><span data-stu-id="a969b-191">Optional: Try also hello Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="a969b-192">Fermez le navigateur de hello et arrêter le débogage de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a969b-192">Close hello browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="a969b-193">Swashbuckle fonctionne avec n’importe quel projet d’API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a969b-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="a969b-194">Si vous souhaitez tooadd Swagger métadonnées génération tooan un projet existant, installez simplement le package de Swashbuckle hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-194">If you want tooadd Swagger metadata generation tooan existing project, just install hello Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="a969b-195">Les métadonnées Swagger incluent un ID unique pour chaque opération d’API.</span><span class="sxs-lookup"><span data-stu-id="a969b-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="a969b-196">Par défaut, Swashbuckle peut générer des ID d’opération Swagger en double pour vos méthodes de contrôleur d’API web.</span><span class="sxs-lookup"><span data-stu-id="a969b-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="a969b-197">Cela se produit si les méthodes HTTP du contrôleur sont surchargées, par exemple `Get()` et `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="a969b-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="a969b-198">Pour plus d’informations sur la façon dont les surcharges de toohandle, consultez [définitions généré Swashbuckle de personnaliser les API](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="a969b-198">For information about how toohandle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="a969b-199">Si vous créez un projet d’API Web dans Visual Studio à l’aide du modèle d’application API Azure hello, code qui génère l’ID d’opération est automatiquement ajouté toohello *SwaggerConfig.cs* fichier.</span><span class="sxs-lookup"><span data-stu-id="a969b-199">If you create a Web API project in Visual Studio by using hello Azure API App template, code that generates unique operation IDs is automatically added toohello *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="a969b-200"><a id="createapiapp"></a>Créer une application API dans Azure et de déployer le code tooit</span><span class="sxs-lookup"><span data-stu-id="a969b-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code tooit</span></span>
<span data-ttu-id="a969b-201">Dans cette section, vous utilisez les outils Azure qui sont intégrés à Visual Studio de hello **publier le site Web** application toocreate une nouvelle API d’Assistant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a969b-201">In this section, you use Azure tools that are integrated into hello Visual Studio **Publish Web** wizard toocreate a new API app in Azure.</span></span> <span data-ttu-id="a969b-202">Puis vous déployez hello ToDoListDataAPI projet toohello nouvelle application API et appelez des API de hello en hello Swagger de l’interface utilisateur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a969b-202">Then you deploy hello ToDoListDataAPI project toohello new API app and call hello API by running hello Swagger UI.</span></span>

1. <span data-ttu-id="a969b-203">Dans **l’Explorateur de solutions**, cliquez sur le projet de ToDoListDataAPI hello, puis cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="a969b-203">In **Solution Explorer**, right-click hello ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Cliquez sur Publier dans Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="a969b-205">Bonjour **profil** étape Hello **publier le site Web** Assistant, cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="a969b-205">In hello **Profile** step of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Cliquez sur Azure App Service dans Publier le site web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="a969b-207">Connectez-vous à tooyour compte Azure si vous n’avez pas déjà fait, ou actualiser vos informations d’identification s’ils sont arrivés à expiration.</span><span class="sxs-lookup"><span data-stu-id="a969b-207">Sign in tooyour Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="a969b-208">Dans les hello boîte de dialogue du Service d’applications, choisissez hello Azure **abonnement** vous souhaitez toouse, puis cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="a969b-208">In hello App Service dialog box, choose hello Azure **Subscription** you want toouse, and then click **New**.</span></span>
   
    ![Cliquez sur Nouveau dans la boîte de dialogue App Service](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="a969b-210">Hello **hébergement** onglet Hello **créer un Service application** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a969b-210">hello **Hosting** tab of hello **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="a969b-211">Étant donné que vous déployez un projet d’API Web qui a Swashbuckle installé, Visual Studio suppose que vous souhaitez toocreate une application API.</span><span class="sxs-lookup"><span data-stu-id="a969b-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want toocreate an API App.</span></span> <span data-ttu-id="a969b-212">Cela est indiqué par hello **Name de l’application API** titre et par hello fait ce hello **modifier le Type de** liste déroulante est définie trop**application API**.</span><span class="sxs-lookup"><span data-stu-id="a969b-212">This is indicated by hello **API App Name** title and by hello fact that hello **Change Type** drop-down list is set too**API App**.</span></span>
   
    ![Type d’application dans la boîte de dialogue App Service](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="a969b-214">Entrez un **Name de l’application API** qui est unique dans hello *azurewebsites.net* domaine.</span><span class="sxs-lookup"><span data-stu-id="a969b-214">Enter an **API App Name** that is unique in hello *azurewebsites.net* domain.</span></span> <span data-ttu-id="a969b-215">Vous pouvez accepter le nom par défaut hello proposé par Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a969b-215">You can accept hello default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="a969b-216">Si vous entrez un nom d’une autre personne a déjà utilisé, vous consultez un toohello de point d’exclamation rouge à droite.</span><span class="sxs-lookup"><span data-stu-id="a969b-216">If you enter a name that someone else has already used, you see a red exclamation mark toohello right.</span></span>
   
    <span data-ttu-id="a969b-217">Hello URL de l’application hello API sera `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="a969b-217">hello URL of hello API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="a969b-218">Bonjour **groupe de ressources** déroulante, cliquez sur **nouveau**, puis entrez « ToDoListGroup » ou un autre nom si vous préférez.</span><span class="sxs-lookup"><span data-stu-id="a969b-218">In hello **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="a969b-219">Un groupe de ressources est une collection de ressources Azure telles que des applications API, des bases de données, des machines virtuelles, etc.</span><span class="sxs-lookup"><span data-stu-id="a969b-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="a969b-220">Pour ce didacticiel, il est meilleure toocreate un groupe de ressources car qui la rendent facile toodelete en une seule étape que toutes hello des ressources Azure que vous créez pour le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-220">For this tutorial, it's best toocreate a new resource group because that makes it easy toodelete in one step all hello Azure resources that you create for hello tutorial.</span></span>
   
    <span data-ttu-id="a969b-221">Cette zone vous permet de sélectionner un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) ou d’en créer un avec un nom différent de ceux qui existent déjà dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a969b-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="a969b-222">Cliquez sur hello **nouveau** toohello suivant du bouton **du Plan App Service** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="a969b-222">Click hello **New** button next toohello **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="a969b-223">capture d’écran Hello montre exemples de valeurs pour **Name de l’application API**, **abonnement**, et **groupe de ressources** --vos valeurs seront différentes.</span><span class="sxs-lookup"><span data-stu-id="a969b-223">hello screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Boîte de dialogue Créer App Service](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="a969b-225">Bonjour suit vous créer un plan App Service pour le nouveau groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-225">In hello following steps you create an App Service plan for hello new resource group.</span></span> <span data-ttu-id="a969b-226">Un plan App Service spécifie les ressources de calcul hello qui s’exécute votre application API.</span><span class="sxs-lookup"><span data-stu-id="a969b-226">An App Service plan specifies hello compute resources that your API app runs on.</span></span> <span data-ttu-id="a969b-227">Par exemple, si vous choisissez le niveau gratuit de hello, votre application API s’exécute sur les ordinateurs virtuels partagés, alors que pour certains niveaux payants, il s’exécute sur des machines virtuelles dédiées.</span><span class="sxs-lookup"><span data-stu-id="a969b-227">For example, if you choose hello free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="a969b-228">Pour plus d’informations sur les plans App Service, consultez [Présentation des plans App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a969b-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="a969b-229">Bonjour **configurer un Plan App Service** boîte de dialogue, entrez « ToDoListPlan » ou un autre nom si vous préférez.</span><span class="sxs-lookup"><span data-stu-id="a969b-229">In hello **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="a969b-230">Bonjour **emplacement** liste déroulante, sélectionnez l’emplacement de hello tooyou le plus proche.</span><span class="sxs-lookup"><span data-stu-id="a969b-230">In hello **Location** drop-down list, choose hello location that is closest tooyou.</span></span>
   
    <span data-ttu-id="a969b-231">Ce paramètre indique le centre de données Azure dans lequel votre application sera exécutée.</span><span class="sxs-lookup"><span data-stu-id="a969b-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="a969b-232">Choisissez un emplacement fermer tooyou toominimize [latence](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="a969b-232">Choose a location close tooyou toominimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="a969b-233">Bonjour **taille** déroulante, cliquez sur **libre**.</span><span class="sxs-lookup"><span data-stu-id="a969b-233">In hello **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="a969b-234">Pour ce didacticiel, hello libre tarification fournissent des performances suffisantes.</span><span class="sxs-lookup"><span data-stu-id="a969b-234">For this tutorial, hello free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="a969b-235">Bonjour **configurer un Plan App Service** boîte de dialogue, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a969b-235">In hello **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Cliquez sur OK dans Configurer le plan App Service](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="a969b-237">Bonjour **créer un Service application** boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="a969b-237">In hello **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Cliquez sur Créer dans la boîte de dialogue App Service](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="a969b-239">Visual Studio crée l’application d’API hello et un profil de publication qui a tous les paramètres de hello requis pour application hello API.</span><span class="sxs-lookup"><span data-stu-id="a969b-239">Visual Studio creates hello API app and a publish profile that has all of hello required settings for hello API app.</span></span> <span data-ttu-id="a969b-240">Il s’ouvre et affiche hello **publier le site Web** Assistant que vous allez utiliser project de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a969b-240">Then it opens hello **Publish Web** wizard, which you'll use toodeploy hello project.</span></span>
    
    <span data-ttu-id="a969b-241">Hello **publier le site Web** Assistant s’ouvre sur hello **connexion** onglet (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="a969b-241">hello **Publish Web** wizard opens on hello **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="a969b-242">Sur hello **connexion** sous l’onglet hello **Server** et **nom du Site** paramètres point tooyour API app.</span><span class="sxs-lookup"><span data-stu-id="a969b-242">On hello **Connection** tab, hello **Server** and **Site name** settings point tooyour API app.</span></span> <span data-ttu-id="a969b-243">Hello **nom d’utilisateur** et **mot de passe** sont les informations d’identification de déploiement Azure crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="a969b-243">hello **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="a969b-244">Après le déploiement, Visual Studio ouvre un navigateur toohello **URL de Destination** (qui est le seul but de hello pour **URL de Destination**).</span><span class="sxs-lookup"><span data-stu-id="a969b-244">After deployment, Visual Studio opens a browser toohello **Destination URL** (that's hello only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="a969b-245">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a969b-245">Click **Next**.</span></span>
    
    ![Cliquez sur Suivant dans l’onglet Connexion de l’assistant Publier le site Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="a969b-247">onglet suivant de Hello est hello **paramètres** onglet (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="a969b-247">hello next tab is hello **Settings** tab (shown below).</span></span> <span data-ttu-id="a969b-248">Vous pouvez modifier ici une version debug de hello build configuration onglet toodeploy [débogage distant](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="a969b-248">Here you can change hello build configuration tab toodeploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="a969b-249">Hello onglet offre également plusieurs **Options de publication du fichier**:</span><span class="sxs-lookup"><span data-stu-id="a969b-249">hello tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="a969b-250">Supprimer les fichiers supplémentaires de la destination</span><span class="sxs-lookup"><span data-stu-id="a969b-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="a969b-251">Précompiler durant la publication</span><span class="sxs-lookup"><span data-stu-id="a969b-251">Precompile during publishing</span></span>
    * <span data-ttu-id="a969b-252">Exclure les fichiers du dossier App_Data hello</span><span class="sxs-lookup"><span data-stu-id="a969b-252">Exclude files from hello App_Data folder</span></span>
    
    <span data-ttu-id="a969b-253">Pour ce didacticiel, vous n’avez besoin d’aucune de ces options.</span><span class="sxs-lookup"><span data-stu-id="a969b-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="a969b-254">Pour obtenir des explications détaillées sur leur action, consultez la rubrique [Déploiement d’un projet web à l’aide de la publication en un clic dans Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="a969b-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="a969b-255">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a969b-255">Click **Next**.</span></span>
    
    ![Cliquez sur Suivant dans l’onglet Paramètres de l’assistant Publier le site Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="a969b-257">L’élément suivant est hello **aperçu** onglet (voir ci-dessous), qui vous donne un toosee opportunité quels fichiers vont toobe copié à partir de votre application toohello API de projet.</span><span class="sxs-lookup"><span data-stu-id="a969b-257">Next is hello **Preview** tab (shown below), which gives you an opportunity toosee what files are going toobe copied from your project toohello API app.</span></span> <span data-ttu-id="a969b-258">Lorsque vous déployez une application de tooan API de projet que vous avez déjà déployé de tooearlier, seuls les fichiers modifiés sont copiés.</span><span class="sxs-lookup"><span data-stu-id="a969b-258">When you're deploying a project tooan API app that you already deployed tooearlier, only changed files are copied.</span></span> <span data-ttu-id="a969b-259">Si vous souhaitez toosee une liste de ce que sera copié, vous pouvez cliquer sur hello **démarrer la version préliminaire** bouton.</span><span class="sxs-lookup"><span data-stu-id="a969b-259">If you want toosee a list of what will be copied, you can click hello **Start Preview** button.</span></span>
15. <span data-ttu-id="a969b-260">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="a969b-260">Click **Publish**.</span></span>
    
    ![Cliquez sur Publier dans l’onglet Aperçu de l’assistant Publier le site Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="a969b-262">Visual Studio déploie hello ToDoListDataAPI projet toohello nouvelle application API.</span><span class="sxs-lookup"><span data-stu-id="a969b-262">Visual Studio deploys hello ToDoListDataAPI project toohello new API app.</span></span> <span data-ttu-id="a969b-263">Hello **sortie** ouvre une fenêtre de réussir le déploiement, et une page « a été créée » s’affiche dans une URL de toohello navigateur fenêtre ouverte de l’application hello API.</span><span class="sxs-lookup"><span data-stu-id="a969b-263">hello **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened toohello URL of hello API app.</span></span>
    
    ![Réussite du déploiement dans la fenêtre de sortie](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Page Application API créée avec succès](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="a969b-266">Ajouter des URL de toohello « swagger » dans la barre d’adresses du navigateur hello et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="a969b-266">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="a969b-267">(hello URL est `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="a969b-267">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="a969b-268">navigateur de Hello affiche hello même Swagger l’interface utilisateur que vous avez vu précédemment, mais maintenant elle est en cours d’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-268">hello browser displays hello same Swagger UI that you saw earlier, but now it's running in hello cloud.</span></span> <span data-ttu-id="a969b-269">Essayer hello méthode Get, et vous constatez que vous êtes des éléments de tâches 2 toohello différé par défaut.</span><span class="sxs-lookup"><span data-stu-id="a969b-269">Try out hello Get method, and you see that you're back toohello default 2 to-do items.</span></span> <span data-ttu-id="a969b-270">Hello apportées précédemment ont été enregistrées dans la mémoire sur l’ordinateur local de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-270">hello changes you made earlier were saved in memory in hello local machine.</span></span>
17. <span data-ttu-id="a969b-271">Ouvrez hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a969b-271">Open hello [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="a969b-272">Hello portail Azure est une interface web pour la gestion des ressources Azure telles que les applications API.</span><span class="sxs-lookup"><span data-stu-id="a969b-272">hello Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="a969b-273">Cliquez sur **Plus de services > App Services**.</span><span class="sxs-lookup"><span data-stu-id="a969b-273">Click **More Services > App Services**.</span></span>
    
    ![Parcourir App Services](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="a969b-275">Bonjour **des Services d’application** panneau, recherchez et cliquez sur votre nouvelle application API.</span><span class="sxs-lookup"><span data-stu-id="a969b-275">In hello **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="a969b-276">(Dans hello portail Azure, les fenêtres qui s’ouvrent toohello droite sont appelés *panneaux*.)</span><span class="sxs-lookup"><span data-stu-id="a969b-276">(In hello Azure portal, windows that open toohello right are called *blades*.)</span></span>
    
    ![Panneau App Services](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="a969b-278">Deux panneaux s’ouvrent.</span><span class="sxs-lookup"><span data-stu-id="a969b-278">Two blades open.</span></span> <span data-ttu-id="a969b-279">Un panneau a une vue d’ensemble de l’application d’API hello, et a une longue liste de paramètres que vous pouvez afficher et modifier.</span><span class="sxs-lookup"><span data-stu-id="a969b-279">One blade has an overview of hello API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="a969b-280">Bonjour **paramètres** panneau, rechercher hello **API** et cliquez sur **définition d’API**.</span><span class="sxs-lookup"><span data-stu-id="a969b-280">In hello **Settings** blade, find hello **API** section and click **API Definition**.</span></span>
    
    ![Définition de l’API dans le panneau Paramètres](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="a969b-282">Hello **définition d’API** panneau vous permet de spécifier des URL de hello qui retourne des métadonnées Swagger 2.0 au format JSON.</span><span class="sxs-lookup"><span data-stu-id="a969b-282">hello **API Definition** blade lets you specify hello URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="a969b-283">Lorsque Visual Studio crée l’application hello API, il définit hello API définition URL toohello par défaut pour Swashbuckle métadonnées générées que vous avez vu précédemment, qui est l’application hello API de base d’URL plu `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="a969b-283">When Visual Studio creates hello API app, it sets hello API definition URL toohello default value for Swashbuckle-generated metadata that you saw earlier, which is hello API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL de définition de l’API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="a969b-285">Lorsque vous sélectionnez un code de client toogenerate l’application API pour celle-ci, Visual Studio récupère les métadonnées de hello à partir de cette URL.</span><span class="sxs-lookup"><span data-stu-id="a969b-285">When you select an API app toogenerate client code for it, Visual Studio retrieves hello metadata from this URL.</span></span>

## <span data-ttu-id="a969b-286"><a id="codegen"></a>Générer le code client pour le niveau de données hello</span><span class="sxs-lookup"><span data-stu-id="a969b-286"><a id="codegen"></a> Generate client code for hello data tier</span></span>
<span data-ttu-id="a969b-287">Un des avantages de hello de l’intégration de Swagger dans les applications API Azure est la génération de code automatique.</span><span class="sxs-lookup"><span data-stu-id="a969b-287">One of hello advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="a969b-288">Classes de client généré vous code toowrite plus simple qui appelle une application API.</span><span class="sxs-lookup"><span data-stu-id="a969b-288">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="a969b-289">Hello ToDoListAPI projet déjà hello généré le code client, mais Bonjour comme suit, vous allez supprimer et régénérer toosee toodo hello comment la génération de code.</span><span class="sxs-lookup"><span data-stu-id="a969b-289">hello ToDoListAPI project already has hello generated client code, but in hello following steps you'll delete it and regenerate it toosee how toodo hello code generation.</span></span>

1. <span data-ttu-id="a969b-290">Dans Visual Studio **l’Explorateur de solutions**, Bonjour ToDoListAPI projet d’équipe, supprimez hello *ToDoListDataAPI* dossier.</span><span class="sxs-lookup"><span data-stu-id="a969b-290">In Visual Studio **Solution Explorer**, in hello ToDoListAPI project, delete hello *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="a969b-291">**Attention : Supprimer uniquement le dossier hello, pas le projet de ToDoListDataAPI hello.**</span><span class="sxs-lookup"><span data-stu-id="a969b-291">**Caution: Delete only hello folder, not hello ToDoListDataAPI project.**</span></span>
   
    ![Suppression du code client généré](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="a969b-293">Ce dossier a été créé à l’aide du processus de génération de code hello que vous êtes sur toogo via.</span><span class="sxs-lookup"><span data-stu-id="a969b-293">This folder was created by using hello code generation process that you're about toogo through.</span></span>
2. <span data-ttu-id="a969b-294">Projet de ToDoListAPI hello d’avec le bouton droit, puis cliquez sur **Ajouter > Client de l’API REST**.</span><span class="sxs-lookup"><span data-stu-id="a969b-294">Right-click hello ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Ajouter un client API REST dans Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="a969b-296">Bonjour **Client de l’API REST ajouter** boîte de dialogue, cliquez sur **URL Swagger**, puis cliquez sur **sélectionner les ressources Azure**.</span><span class="sxs-lookup"><span data-stu-id="a969b-296">In hello **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Sélectionner une ressource Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="a969b-298">Bonjour **du Service d’applications** boîte de dialogue, développez le groupe de ressources hello vous utilisez pour ce didacticiel, sélectionnez votre application API, puis cliquez **OK**.</span><span class="sxs-lookup"><span data-stu-id="a969b-298">In hello **App Service** dialog box, expand hello resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Sélectionnez une application API pour la génération de code](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="a969b-300">Notez que lorsque vous retournez toohello **Client de l’API REST ajouter** boîte de dialogue, zone de texte hello est rempli avec la définition de l’API de hello valeur de l’URL que vous avez vu plus haut dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-300">Notice that when you return toohello **Add REST API Client** dialog, hello text box has been filled in with hello API definition URL value that you saw earlier in hello portal.</span></span>
   
    ![URL de définition de l’API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="a969b-302">Métadonnées de tooget d’autre moyen pour la génération de code sont l’URL de hello tooenter directement au lieu de passer par la boîte de dialogue Parcourir hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-302">An alternative way tooget metadata for code generation is tooenter hello URL directly instead of going through hello browse dialog.</span></span> <span data-ttu-id="a969b-303">Ou si vous souhaitez que le code client toogenerate avant de déployer tooAzure, vous pouvez exécuter le projet d’API Web hello localement, accédez toohello URL qui fournit le fichier Swagger de JSON de hello, enregistrer le fichier de hello, et utiliser hello **sélectionner un fichier de métadonnées Swagger existant**option.</span><span class="sxs-lookup"><span data-stu-id="a969b-303">Or if you want toogenerate client code before deploying tooAzure, you could run hello Web API project locally, go toohello URL that provides hello Swagger JSON file, save hello file, and use hello **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="a969b-304">Bonjour **Client de l’API REST ajouter** boîte de dialogue, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a969b-304">In hello **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="a969b-305">Visual Studio crée un dossier nommé d’après l’application hello API et génère des classes de client.</span><span class="sxs-lookup"><span data-stu-id="a969b-305">Visual Studio creates a folder named after hello API app and generates client classes.</span></span>
   
    ![Fichiers de code pour le client généré](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="a969b-307">Dans le projet de ToDoListAPI hello, ouvrez *Controllers\ToDoListController.cs* code hello de toosee à la ligne 40 qui appelle des API de hello à l’aide du client de hello généré.</span><span class="sxs-lookup"><span data-stu-id="a969b-307">In hello ToDoListAPI project, open *Controllers\ToDoListController.cs* toosee hello code at line 40  that calls hello API by using hello generated client.</span></span>
   
    <span data-ttu-id="a969b-308">Hello suivant extrait de code montre comment le code de hello instancie objet de client hello et appels hello méthode Get.</span><span class="sxs-lookup"><span data-stu-id="a969b-308">hello following snippet shows how hello code instantiates hello client object and calls hello Get method.</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    <span data-ttu-id="a969b-309">paramètre de constructeur Hello Obtient l’URL de point de terminaison hello de hello `toDoListDataAPIURL` paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="a969b-309">hello constructor parameter gets hello endpoint URL from  hello `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="a969b-310">Dans le fichier Web.config hello, cette valeur est toohello ensemble local IIS Express URL de hello API projet afin que vous puissiez exécuter des application hello localement.</span><span class="sxs-lookup"><span data-stu-id="a969b-310">In hello Web.config file, that value is set toohello local IIS Express URL of hello API project so that you can run hello application locally.</span></span> <span data-ttu-id="a969b-311">Si vous omettez le paramètre de constructeur hello, point de terminaison par défaut hello est hello URL que vous avez généré le code hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-311">If you omit hello constructor parameter, hello default endpoint is hello URL that you generated hello code from.</span></span>
7. <span data-ttu-id="a969b-312">Votre classe de client est généré avec un nom différent selon le nom de votre application API ; modifier le code hello dans *Controllers\ToDoListController.cs* afin que hello nom de type correspond à ce qui a été généré dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="a969b-312">Your client class will be generated with a different name based on your API app name; change hello code in *Controllers\ToDoListController.cs* so that hello type name matches what was generated in your project.</span></span> <span data-ttu-id="a969b-313">Par exemple, si vous avez nommé votre application API ToDoListDataAPI071316, vous modifieriez ce code :</span><span class="sxs-lookup"><span data-stu-id="a969b-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="a969b-314">toothis :</span><span class="sxs-lookup"><span data-stu-id="a969b-314">toothis:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a><span data-ttu-id="a969b-315">Créer une couche API application toohost hello intermédiaire</span><span class="sxs-lookup"><span data-stu-id="a969b-315">Create an API app toohost hello middle tier</span></span>
<span data-ttu-id="a969b-316">Plus tôt vous [hello données couche API application créée et déployée code tooit](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="a969b-316">Earlier you [created hello data tier API app and deployed code tooit](#createapiapp).</span></span>  <span data-ttu-id="a969b-317">Maintenant vous suivez hello même procédure pour l’application de couche intermédiaire API hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-317">Now you follow hello same procedure for hello middle tier API app.</span></span>

1. <span data-ttu-id="a969b-318">Dans **l’Explorateur de solutions**, avec le bouton hello intermédiaire ToDoListAPI (pas hello couche données ToDoListDataAPI) du projet, puis cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="a969b-318">In **Solution Explorer**, right-click hello middle tier ToDoListAPI  project (not hello data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Cliquez sur Publier dans Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="a969b-320">Bonjour **profil** onglet Hello **publier le site Web** Assistant, cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="a969b-320">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="a969b-321">Bonjour **du Service d’applications** boîte de dialogue, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="a969b-321">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="a969b-322">Bonjour **hébergement** onglet Hello **créer un Service application** boîte de dialogue zone, accepter la valeur par défaut hello **Name de l’application API** ou entrer un nom unique dans hello  *azurewebsites.NET* domaine.</span><span class="sxs-lookup"><span data-stu-id="a969b-322">In hello **Hosting** tab of hello **Create App Service** dialog box, accept hello default **API App Name** or enter a name that is unique in hello *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="a969b-323">Choisissez hello Azure **abonnement** vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="a969b-323">Choose hello Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="a969b-324">Bonjour **groupe de ressources** liste déroulante, choisissez hello même groupe de ressources vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="a969b-324">In hello **Resource Group** drop-down, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="a969b-325">Bonjour **Plan App Service** liste déroulante, choisissez hello même plan que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="a969b-325">In hello **App Service Plan** drop-down, choose hello same plan you created earlier.</span></span> <span data-ttu-id="a969b-326">Il prend par défaut la valeur de toothat.</span><span class="sxs-lookup"><span data-stu-id="a969b-326">It will default toothat value.</span></span>
8. <span data-ttu-id="a969b-327">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a969b-327">Click **Create**.</span></span>
   
    <span data-ttu-id="a969b-328">Visual Studio crée l’application hello API, crée un profil de publication pour celle-ci et affiche hello **connexion** étape Hello **publier le site Web** Assistant.</span><span class="sxs-lookup"><span data-stu-id="a969b-328">Visual Studio creates hello API app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
9. <span data-ttu-id="a969b-329">Bonjour **connexion** étape Hello **publier le site Web** Assistant, cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="a969b-329">In hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="a969b-330">Visual Studio déploie hello ToDoListAPI projet toohello nouvelle application API et ouvre le navigateur toohello URL d’application d’API hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-330">Visual Studio deploys hello ToDoListAPI project toohello new API app and opens a browser toohello URL of hello API app.</span></span> <span data-ttu-id="a969b-331">page de Hello « créée avec succès » s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a969b-331">hello "successfully created" page appears.</span></span>

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a><span data-ttu-id="a969b-332">Configurer la couche de données hello intermédiaire toocall hello</span><span class="sxs-lookup"><span data-stu-id="a969b-332">Configure hello middle tier toocall hello data tier</span></span>
<span data-ttu-id="a969b-333">Si vous avez appelé application API de niveau intermédiaire hello maintenant, il serait essayer la couche de données hello toocall à l’aide des URL localhost hello qui se trouve toujours dans le fichier Web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-333">If you called hello middle tier API app now, it would try toocall hello data tier using hello localhost URL that is still in hello Web.config file.</span></span> <span data-ttu-id="a969b-334">Dans cette section, vous entrez des URL de l’application API niveau données hello dans un paramètre d’environnement dans l’application API de niveau intermédiaire hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-334">In this section you enter hello data tier API app URL into an environment setting in hello middle tier API app.</span></span> <span data-ttu-id="a969b-335">Quand hello code dans l’application API de niveau intermédiaire hello récupère du paramètre d’URL hello données couche, paramètre d’environnement hello remplace ce qui est dans le fichier Web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-335">When hello code in hello middle tier API app retrieves hello data tier URL setting, hello environment setting will override what's in hello Web.config file.</span></span>

1. <span data-ttu-id="a969b-336">Accédez toohello [portail Azure](https://portal.azure.com/), puis accédez toohello **application API** panneau pour l’application hello API que vous avez créé le projet de toohost hello TodoListAPI (intermédiaire).</span><span class="sxs-lookup"><span data-stu-id="a969b-336">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **API App** blade for hello API app that you created toohost hello TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="a969b-337">Dans hello l’application API **paramètres** panneau, cliquez sur **paramètres de l’Application**.</span><span class="sxs-lookup"><span data-stu-id="a969b-337">In hello API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="a969b-338">Dans hello l’application API **paramètres de l’Application** panneau, faites défiler vers le bas toohello **paramètres de l’application** section et ajouter des éléments suivants de hello clé et la valeur.</span><span class="sxs-lookup"><span data-stu-id="a969b-338">In hello API App's **Application Settings** blade, scroll down toohello **App settings** section and add hello following key and value.</span></span> <span data-ttu-id="a969b-339">Hello aura l’URL de hello de hello première API application que vous avez publié dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a969b-339">hello value will be hello URL of hello first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="a969b-340">**Clé**</span><span class="sxs-lookup"><span data-stu-id="a969b-340">**Key**</span></span> | <span data-ttu-id="a969b-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="a969b-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="a969b-342">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="a969b-342">**Value**</span></span> |<span data-ttu-id="a969b-343">https://{nom de votre application API de la couche Données}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="a969b-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="a969b-344">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="a969b-344">**Example**</span></span> |<span data-ttu-id="a969b-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="a969b-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="a969b-346">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a969b-346">Click **Save**.</span></span>
   
    ![Cliquez sur Enregistrer pour les paramètres de l’application](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="a969b-348">Lorsque le code de hello s’exécute dans Azure, cette valeur remplace maintenant hello localhost URL qui se trouve dans le fichier Web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-348">When hello code runs in Azure, this value will now override hello localhost URL that is in hello Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="a969b-349">Test</span><span class="sxs-lookup"><span data-stu-id="a969b-349">Test</span></span>
1. <span data-ttu-id="a969b-350">Dans une fenêtre de navigateur, accédez URL toohello de couche intermédiaire nouvelle application API que vous venez de créer pour ToDoListAPI hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-350">In a browser window, browse toohello URL of hello new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="a969b-351">Vous pouvez y accéder en cliquant sur les URL hello dans le panneau principal de l’application hello API dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-351">You can get there by clicking hello URL in hello API app's main blade in hello portal.</span></span>
2. <span data-ttu-id="a969b-352">Ajouter des URL de toohello « swagger » dans la barre d’adresses du navigateur hello et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="a969b-352">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="a969b-353">(hello URL est `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="a969b-353">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="a969b-354">navigateur affiche Hello hello même Swagger l’interface utilisateur que vous avez vu précédemment pour ToDoListDataAPI, mais désormais `owner` n’est pas un champ obligatoire pour l’opération d’obtention de hello, car l’application de couche intermédiaire API hello envoie cette application de valeur toohello données couche API pour vous.</span><span class="sxs-lookup"><span data-stu-id="a969b-354">hello browser displays hello same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for hello Get operation, because hello middle tier API app is sending that value toohello data tier API app for you.</span></span> <span data-ttu-id="a969b-355">(Lorsque vous hello didacticiels de l’authentification, intermédiaire hello enverra des ID de l’utilisateur réel pour hello `owner` paramètre ; pour maintenant il est le codage en dur un astérisque.)</span><span class="sxs-lookup"><span data-stu-id="a969b-355">(When you do hello authentication tutorials, hello middle tier will send actual user IDs for hello `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="a969b-356">Essayer hello méthode Get et hello toovalidate autres méthodes qui hello application API de niveau intermédiaire est correctement appel hello données couche application API.</span><span class="sxs-lookup"><span data-stu-id="a969b-356">Try out hello Get method and hello other methods toovalidate that hello middle tier API app is successfully calling hello data tier API app.</span></span>
   
    ![Méthode Get de l’interface utilisateur Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="a969b-358">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a969b-358">Troubleshooting</span></span>
<span data-ttu-id="a969b-359">Si vous rencontrez un problème tout au long de ce didacticiel, voici quelques suggestions de dépannage :</span><span class="sxs-lookup"><span data-stu-id="a969b-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="a969b-360">Assurez-vous que vous utilisez la version la plus récente de hello hello [Azure SDK pour .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="a969b-360">Make sure that you're using hello latest version of hello [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="a969b-361">Deux des noms de projet hello sont similaires (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="a969b-361">Two of hello project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="a969b-362">Si les éléments ne s’affichent pas comme décrit dans les instructions hello lorsque vous travaillez avec un projet, assurez-vous que vous avez ouvert le projet approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-362">If things don't look as described in hello instructions when you are working with a project, make sure you have opened hello correct project.</span></span>
* <span data-ttu-id="a969b-363">Si vous êtes sur un réseau d’entreprise et que vous essayez de toodeploy tooAzure du Service d’applications via un pare-feu, assurez-vous que les ports 443 et 8172 sont ouverts pour Web Deploy.</span><span class="sxs-lookup"><span data-stu-id="a969b-363">If you're on a corporate network and are trying toodeploy tooAzure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="a969b-364">Si vous ne pouvez pas ouvrir ces ports, vous pouvez utiliser d’autres méthodes de déploiement.</span><span class="sxs-lookup"><span data-stu-id="a969b-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="a969b-365">Consultez [déployer votre tooAzure d’application du Service d’applications](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a969b-365">See [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="a969b-366">Erreurs « noms d’itinéraires doivent être uniques » : vous pouvez obtenir ces si vous accidentellement déployez hello projet incorrect tooan API app et puis déployez ultérieurement un tooit correct de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-366">"Route names must be unique" errors -- you could get these if you accidentally deploy hello wrong project tooan API app and then later deploy hello correct one tooit.</span></span> <span data-ttu-id="a969b-367">toocorrect, application toohello API de redéploiement hello projet approprié et sur hello **paramètres** onglet Hello **publier le site Web** Assistant, sélectionnez **supprimer les fichiers supplémentaires à la destination**.</span><span class="sxs-lookup"><span data-stu-id="a969b-367">toocorrect this, redeploy hello correct project toohello API app, and on hello **Settings** tab of hello **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="a969b-368">Après avoir configuré votre application API ASP.NET en cours d’exécution dans Azure App Service, vous souhaiterez peut-être toolearn plus d’informations sur les fonctionnalités de Visual Studio qui simplifient la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="a969b-368">After you have your ASP.NET API app running in Azure App Service, you may want toolearn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="a969b-369">Pour plus d’informations sur la journalisation, le débogage à distance, etc. consultez la section [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md) (Résolution des problèmes des applications web Azure App Service dans Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="a969b-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a969b-370">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a969b-370">Next steps</span></span>
<span data-ttu-id="a969b-371">Vous avez vu comment toodeploy API Web projets tooAPI applications existantes, générer le code client pour les applications d’API et consommer des applications API à partir de clients .NET.</span><span class="sxs-lookup"><span data-stu-id="a969b-371">You've seen how toodeploy existing Web API projects tooAPI apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="a969b-372">Hello étape suivante du didacticiel de cette série montre comment trop[utiliser CORS tooconsume API des applications à partir de clients JavaScript](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a969b-372">hello next tutorial in this series shows how too[use CORS tooconsume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="a969b-373">Pour plus d’informations sur la génération de code client, consultez hello [Azure/AutoRest](https://github.com/azure/autorest) référentiel sur GitHub.com. Pour l’aide sur les problèmes à l’aide du client de hello généré, ouvrez un [problème dans le référentiel de AutoRest hello](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="a969b-373">For more information about client code generation, see hello [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com. For help with problems using hello generated client, open an [issue in hello AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="a969b-374">Si vous souhaitez toocreate nouveaux projets d’application API à partir de zéro, utilisez hello **application API Azure** modèle.</span><span class="sxs-lookup"><span data-stu-id="a969b-374">If you want toocreate new API app projects from scratch, use hello **Azure API App** template.</span></span>

![Modèle d’application API dans Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="a969b-376">Hello **application API Azure** modèle de projet est l’équivalent toochoosing hello **vide** ASP.NET 4.5.2 modèle, en cliquant sur la prise en charge des API Web tooadd case à cocher hello et l’installation de package NuGet de Swashbuckle de hello.</span><span class="sxs-lookup"><span data-stu-id="a969b-376">hello **Azure API App** project template is equivalent toochoosing hello **Empty** ASP.NET 4.5.2 template, clicking hello check box tooadd Web API support, and installing hello Swashbuckle NuGet package.</span></span> <span data-ttu-id="a969b-377">En outre, le modèle de hello ajoute Swashbuckle configuration code conçu tooprevent hello créer des doublons Swagger opération ID.</span><span class="sxs-lookup"><span data-stu-id="a969b-377">In addition, hello template adds some Swashbuckle configuration code designed tooprevent hello creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="a969b-378">Une fois que vous avez créé un projet d’application API, vous pouvez le déployer hello d’application tooan API même façon que vous l’avez vu dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a969b-378">Once you've created an API App project, you can deploy it tooan API app hello same way you saw in this tutorial.</span></span>

