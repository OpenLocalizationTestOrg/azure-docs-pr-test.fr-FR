---
title: "Prise en main d’API Apps et d’ASP.NET dans Azure App Service | Microsoft Docs"
description: "Découvrez comment créer, déployer et consommer une application API ASP.NET dans Azure App Service avec Visual Studio 2015."
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
ms.openlocfilehash: e8fbffde29efcdbb2f67362474061e9f6ee0d59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="685bd-103">Prise en main d’API Apps, d’ASP.NET et de Swagger dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="685bd-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="685bd-104">Ce premier didacticiel de la série explique comment utiliser les fonctionnalités d’Azure App Service pour le développement et l’hébergement d’API RESTful :</span><span class="sxs-lookup"><span data-stu-id="685bd-104">This is the first in a series of tutorials that show how to use features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="685bd-105">Ce didacticiel décrit la prise en charge des métadonnées des API au format Swagger.</span><span class="sxs-lookup"><span data-stu-id="685bd-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="685bd-106">Vous apprendrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="685bd-106">You'll learn:</span></span>

* <span data-ttu-id="685bd-107">Créer et déployer des [applications API](app-service-api-apps-why-best-platform.md) dans Azure App Service à l’aide des outils intégrés à Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="685bd-107">How to create and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="685bd-108">Automatiser la découverte d’API en utilisant le package Swashbuckle NuGet pour générer de manière des métadonnées d’API Swagger</span><span class="sxs-lookup"><span data-stu-id="685bd-108">How to automate API discovery by using the Swashbuckle NuGet package to dynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="685bd-109">Utiliser des métadonnées d’API Swagger pour générer automatiquement un code client pour une application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-109">How to use Swagger API metadata to automatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="685bd-110">Vue d’ensemble de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="685bd-110">Sample application overview</span></span>
<span data-ttu-id="685bd-111">Dans ce didacticiel, vous travaillez avec un exemple d’application de liste des tâches simples.</span><span class="sxs-lookup"><span data-stu-id="685bd-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="685bd-112">L’application contient un composant frontal d’application monopage (SPA), une couche intermédiaire d’API web ASP.NET et une couche de données d’API web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="685bd-112">The application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Exemple de schéma d’application API Apps](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="685bd-114">Voici une capture d’écran du composant frontal [AngularJS](https://angularjs.org/) .</span><span class="sxs-lookup"><span data-stu-id="685bd-114">Here's a screen shot of the [AngularJS](https://angularjs.org/) front end.</span></span>

![Exemple de liste des tâches d’application API Apps](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="685bd-116">La solution Visual Studio inclut trois projets :</span><span class="sxs-lookup"><span data-stu-id="685bd-116">The Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="685bd-117">**ToDoListAngular** (composant frontal) : application monopage AngularJS qui appelle la couche intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="685bd-117">**ToDoListAngular** - The front end: an AngularJS SPA that calls the middle tier.</span></span>
* <span data-ttu-id="685bd-118">**ToDoListAPI** (couche intermédiaire) : projet API web ASP.NET qui appelle la couche Données pour effectuer des opérations CRUD sur les éléments de tâche.</span><span class="sxs-lookup"><span data-stu-id="685bd-118">**ToDoListAPI** - The middle tier: an ASP.NET Web API project that calls the data tier to perform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="685bd-119">**ToDoListAPI** (couche Données) : un projet API web ASP.NET qui exécute les opérations CRUD sur les éléments de tâche.</span><span class="sxs-lookup"><span data-stu-id="685bd-119">**ToDoListDataAPI** - The data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="685bd-120">L’architecture à trois niveaux est une des nombreuses architectures que vous pouvez implémenter à l’aide d’API Apps et est utilisée ici uniquement à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="685bd-120">The three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="685bd-121">Le code de chaque niveau est aussi simple que possible de manière à illustrer les fonctionnalités API Apps ; par exemple, la couche Données utilise la mémoire du serveur plutôt qu’une base de données comme mécanisme de persistance.</span><span class="sxs-lookup"><span data-stu-id="685bd-121">The code in each tier is as simple as possible to demonstrate API Apps features; for example, the data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="685bd-122">À la fin de ce didacticiel, les deux projets d’API web seront opérationnels dans le cloud dans App Service API Apps.</span><span class="sxs-lookup"><span data-stu-id="685bd-122">On completing this tutorial, you'll have the two Web API projects up and running in the cloud in App Service API apps.</span></span>

<span data-ttu-id="685bd-123">Le didacticiel suivant de la série déploie le serveur principal SPA sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="685bd-123">The next tutorial in the series deploys the SPA front end to the cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="685bd-124">Composants requis</span><span class="sxs-lookup"><span data-stu-id="685bd-124">Prerequisites</span></span>
* <span data-ttu-id="685bd-125">API web ASP.NET : les instructions du didacticiel supposent que vous ayez une connaissance de base de l’utilisation de l’ [API web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) ASP.NET dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="685bd-125">ASP.NET Web API - The tutorial instructions assume you have a basic knowledge of how to work with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="685bd-126">Compte Azure : vous pouvez [ouvrir un compte Azure gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) ou [activer les avantages de l’abonnement à Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="685bd-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="685bd-127">Si vous souhaitez commencer à utiliser Azure App Service avant d’ouvrir un compte Azure, accédez à [Essayer App Service](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="685bd-127">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="685bd-128">De là, vous pouvez créer immédiatement une première application temporaire dans App Service. **Aucune carte de crédit** ni aucun engagement ne sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="685bd-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="685bd-129">Visual Studio 2015 avec le [kit de développement logiciel (SDK) Azure pour .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) : le Kit de développement logiciel (SDK) installe automatiquement Visual Studio 2015 si vous ne l’avez pas encore.</span><span class="sxs-lookup"><span data-stu-id="685bd-129">Visual Studio 2015 with the [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - The SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="685bd-130">Dans Visual Studio, cliquez sur Aide -> À propos de Microsoft Visual Studio et vérifiez que « Azure App Service Tools v2.9.1 » ou ultérieur est installé.</span><span class="sxs-lookup"><span data-stu-id="685bd-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Version d’Azure App Service Tools](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="685bd-132">en fonction du nombre de dépendances du Kit de développement logiciel (SDK) qui se trouvent déjà sur votre ordinateur, l'installation du SDK peut prendre un certain temps (de plusieurs minutes à une demi-heure, voire plus).</span><span class="sxs-lookup"><span data-stu-id="685bd-132">Depending on how many of the SDK dependencies you already have on your machine, installing the SDK could take a long time, from several minutes to a half hour or more.</span></span>
    > 
    > 

## <a name="download-the-sample-application"></a><span data-ttu-id="685bd-133">Téléchargement de l'exemple d'application</span><span class="sxs-lookup"><span data-stu-id="685bd-133">Download the sample application</span></span>
1. <span data-ttu-id="685bd-134">Téléchargez le référentiel [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) .</span><span class="sxs-lookup"><span data-stu-id="685bd-134">Download the [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="685bd-135">Vous pouvez cliquer sur le bouton **Download ZIP (Télécharger le zip)** ou cloner le référentiel sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="685bd-135">You can click the **Download ZIP** button or clone the repository on your local machine.</span></span>
2. <span data-ttu-id="685bd-136">Ouvrez la solution ToDoList dans Visual Studio 2015 ou 2013.</span><span class="sxs-lookup"><span data-stu-id="685bd-136">Open the ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="685bd-137">Vous devrez approuver chaque solution.</span><span class="sxs-lookup"><span data-stu-id="685bd-137">You will need to trust each solution.</span></span>
         <span data-ttu-id="685bd-138">![Avertissement de sécurité](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="685bd-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="685bd-139">Générez la solution (CTRL + MAJ + B) pour restaurer les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="685bd-139">Build the solution (CTRL + SHIFT + B)  to restore the NuGet packages.</span></span>
   
    <span data-ttu-id="685bd-140">Si vous souhaitez voir l’application fonctionner avant de la déployer, vous pouvez l’exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="685bd-140">If you want to see the application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="685bd-141">Assurez-vous que ToDoListDataAPI est votre projet de démarrage et exécutez la solution.</span><span class="sxs-lookup"><span data-stu-id="685bd-141">Make sure that ToDoListDataAPI is your startup project and run the solution.</span></span> <span data-ttu-id="685bd-142">Votre navigateur devrait afficher l’erreur HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="685bd-142">You should expect to see a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="685bd-143">Utiliser l’interface utilisateur et les métadonnées d’API Swagger</span><span class="sxs-lookup"><span data-stu-id="685bd-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="685bd-144">La prise en charge des métadonnées d’API [Swagger](http://swagger.io/) 2.0 est intégrée aux applications API App Service.</span><span class="sxs-lookup"><span data-stu-id="685bd-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="685bd-145">Chaque application API peut définir un point de terminaison d’URL qui renvoie à l’API des métadonnées au format JSON Swagger.</span><span class="sxs-lookup"><span data-stu-id="685bd-145">Each API app can specify a URL endpoint that returns metadata for the API in Swagger JSON format.</span></span> <span data-ttu-id="685bd-146">Les métadonnées retournées à partir de ce point de terminaison peuvent être utilisées pour générer le code client.</span><span class="sxs-lookup"><span data-stu-id="685bd-146">The metadata returned from that endpoint can be used to generate client code.</span></span>

<span data-ttu-id="685bd-147">Un projet d’API web ASP.NET peut générer dynamiquement des métadonnées Swagger à l’aide du package NuGet [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) .</span><span class="sxs-lookup"><span data-stu-id="685bd-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="685bd-148">Le package NuGet Swashbuckle est déjà installé dans les projets ToDoListDataAPI et ToDoListAPI que vous avez téléchargés.</span><span class="sxs-lookup"><span data-stu-id="685bd-148">The Swashbuckle NuGet package is already installed in the ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="685bd-149">Dans cette section du didacticiel, nous allons examiner les métadonnées Swagger 2.0 générées, puis essayer une interface utilisateur test basée sur les métadonnées Swagger.</span><span class="sxs-lookup"><span data-stu-id="685bd-149">In this section of the tutorial, you look at the generated Swagger 2.0 metadata, and then you try out a test UI that is based on the Swagger metadata.</span></span>

1. <span data-ttu-id="685bd-150">Définissez le projet ToDoListDataAPI (**et non** le projet ToDoListAPI) comme projet de démarrage.</span><span class="sxs-lookup"><span data-stu-id="685bd-150">Set the ToDoListDataAPI project (**not** the ToDoListAPI project) as the startup project.</span></span>
   
    ![Définir ToDoDataAPI comme projet de démarrage](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="685bd-152">Appuyez sur F5 ou cliquez sur **Déboguer > Démarrer le débogage** pour exécuter le projet en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="685bd-152">Press F5 or click **Debug > Start Debugging** to run the project in debug mode.</span></span>
   
    <span data-ttu-id="685bd-153">Le navigateur s’ouvre et affiche la page d’erreur HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="685bd-153">The browser opens and shows the HTTP 403 error page.</span></span>
3. <span data-ttu-id="685bd-154">Dans la barre d’adresses de votre navigateur, ajoutez `swagger/docs/v1` à la fin de la ligne, puis appuyez sur Retour.</span><span class="sxs-lookup"><span data-stu-id="685bd-154">In your browser address bar, add `swagger/docs/v1` to the end of the line, and then press Return.</span></span> <span data-ttu-id="685bd-155">(L’URL est `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="685bd-155">(The URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="685bd-156">Il s’agit de l’URL par défaut utilisée par Swashbuckle pour retourner les métadonnées JSON Swagger 2.0 pour l’API.</span><span class="sxs-lookup"><span data-stu-id="685bd-156">This is the default URL used by Swashbuckle to return Swagger 2.0 JSON metadata for the API.</span></span>
   
    <span data-ttu-id="685bd-157">Si vous utilisez Internet Explorer, le navigateur vous invite à télécharger un fichier *v1.json* .</span><span class="sxs-lookup"><span data-stu-id="685bd-157">If you're using Internet Explorer, the browser prompts you to download a *v1.json* file.</span></span>
   
    ![Télécharger les métadonnées JSON dans Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="685bd-159">Si vous utilisez Chrome, Firefox ou Edge, le navigateur affiche le fichier JSON dans la fenêtre du navigateur.</span><span class="sxs-lookup"><span data-stu-id="685bd-159">If you're using Chrome, Firefox, or Edge, the browser displays the JSON in the browser window.</span></span> <span data-ttu-id="685bd-160">La gestion du fichier JSON diffère selon les navigateurs, et il se peut que la fenêtre de votre navigateur ne se présente pas exactement comme dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="685bd-160">Different browsers handle JSON differently, and your browser window may not look exactly like the example.</span></span>
   
    ![Métadonnées JSON dans Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="685bd-162">L’exemple suivant montre la première section de métadonnées Swagger de l’API, avec la définition de la méthode Get.</span><span class="sxs-lookup"><span data-stu-id="685bd-162">The following sample shows the first section of the Swagger metadata for the API, with the definition for the Get method.</span></span> <span data-ttu-id="685bd-163">Ce sont ces métadonnées qui pilotent l’interface utilisateur Swagger que vous allez utiliser dans les étapes suivantes, et vous les utiliserez dans une section ultérieure de ce didacticiel pour générer automatiquement le code client.</span><span class="sxs-lookup"><span data-stu-id="685bd-163">This metadata is what drives the Swagger UI that you use in the following steps, and you use it in a later section of the tutorial to automatically generate client code.</span></span>
   
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
4. <span data-ttu-id="685bd-164">Fermez le navigateur et arrêtez le débogage de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="685bd-164">Close the browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="685bd-165">Dans le projet ToDoListDataAPI, dans l’**Explorateur de solutions**, ouvrez le fichier *App_Start\SwaggerConfig.cs*, puis faites défiler la page jusqu’à la ligne 174 et supprimez les marques de commentaire.</span><span class="sxs-lookup"><span data-stu-id="685bd-165">In the ToDoListDataAPI project in **Solution Explorer**, open the *App_Start\SwaggerConfig.cs* file, then scroll down to line 174 and uncomment the following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="685bd-166">Le fichier *SwaggerConfig.cs* est créé quand vous installez le package Swashbuckle dans un projet.</span><span class="sxs-lookup"><span data-stu-id="685bd-166">The *SwaggerConfig.cs* file is created when you install the Swashbuckle package in a project.</span></span> <span data-ttu-id="685bd-167">Ce fichier permet de configurer Swashbuckle de différentes manières.</span><span class="sxs-lookup"><span data-stu-id="685bd-167">The file provides a number of ways to configure Swashbuckle.</span></span>
   
    <span data-ttu-id="685bd-168">Le code dont vous avez supprimé les marques de commentaire active l’interface utilisateur Swagger que vous utiliserez lors des étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="685bd-168">The code you've uncommented enables the Swagger UI that you use in the following steps.</span></span> <span data-ttu-id="685bd-169">Lorsque vous créez un projet d’API Web à l’aide du modèle de projet Application API, ce code est commenté par défaut par mesure de sécurité.</span><span class="sxs-lookup"><span data-stu-id="685bd-169">When you create a Web API project by using the API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="685bd-170">Réexécutez le projet.</span><span class="sxs-lookup"><span data-stu-id="685bd-170">Run the project again.</span></span>
7. <span data-ttu-id="685bd-171">Dans la barre d’adresses de votre navigateur, ajoutez `swagger` à la fin de la ligne, puis appuyez sur Retour.</span><span class="sxs-lookup"><span data-stu-id="685bd-171">In your browser address bar, add `swagger` to the end of the line, and then press Return.</span></span> <span data-ttu-id="685bd-172">(L’URL est `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="685bd-172">(The URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="685bd-173">Quand l’interface utilisateur Swagger apparaît, cliquez sur **ToDoList** pour voir les méthodes disponibles.</span><span class="sxs-lookup"><span data-stu-id="685bd-173">When the Swagger UI page appears, click **ToDoList** to see the methods available.</span></span>
   
    ![Méthodes disponibles dans l’interface utilisateur Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="685bd-175">Cliquez sur le premier bouton **Obtenir** de la liste.</span><span class="sxs-lookup"><span data-stu-id="685bd-175">Click the first **Get** button in the list.</span></span>
10. <span data-ttu-id="685bd-176">Dans la section **Paramètres`owner`, entrez un astérisque comme valeur du paramètre**, puis cliquez sur **Faites un essai**.</span><span class="sxs-lookup"><span data-stu-id="685bd-176">In the **Parameters** section, enter an asterisk as the value of the `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="685bd-177">Lorsque vous ajouterez l’authentification dans les autres didacticiels, la couche intermédiaire fournira l’ID d’utilisateur à la couche de données.</span><span class="sxs-lookup"><span data-stu-id="685bd-177">When you add authentication in later tutorials, the middle tier will provide the actual user ID to the data tier.</span></span> <span data-ttu-id="685bd-178">Pour l’instant, toutes les tâches ont un astérisque comme ID de leur propriétaire tandis que l’application s’exécute sans que l’authentification ne soit activée.</span><span class="sxs-lookup"><span data-stu-id="685bd-178">For now, all tasks will have asterisk as their owner ID while the application runs without authentication enabled.</span></span>
    
    ![Essayer l’interface utilisateur Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="685bd-180">L’interface utilisateur de Swagger appelle la méthode Get de TodoList et affiche le code de réponse et les résultats JSON.</span><span class="sxs-lookup"><span data-stu-id="685bd-180">The Swagger UI calls the ToDoList Get method and displays the response code and JSON results.</span></span>
    
    ![Essayer l’interface utilisateur Swagger - Résultats](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="685bd-182">Cliquez sur **Post**, puis cochez la case sous **Model Schema**.</span><span class="sxs-lookup"><span data-stu-id="685bd-182">Click **Post**, and then click the box under **Model Schema**.</span></span>
    
    <span data-ttu-id="685bd-183">Quand vous cliquez sur le schéma de modèle, la zone de texte est préremplie automatiquement. Vous pouvez y spécifier la valeur du paramètre de la méthode Post.</span><span class="sxs-lookup"><span data-stu-id="685bd-183">Clicking the model schema prefills the input box where you can specify the parameter value for the Post method.</span></span> <span data-ttu-id="685bd-184">(Si cela ne fonctionne pas dans Internet Explorer, utilisez un autre navigateur ou entrez la valeur du paramètre manuellement à l’étape suivante.)</span><span class="sxs-lookup"><span data-stu-id="685bd-184">(If this doesn't work in Internet Explorer, use a different browser or enter the parameter value manually in the next step.)</span></span>  
    
    ![Essayer l’interface utilisateur Swagger - Publication](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="685bd-186">Modifiez le fichier JSON dans la zone d’entrée de paramètre `todo` pour obtenir un résultat similaire à l’exemple suivant, ou insérez votre propre texte descriptif :</span><span class="sxs-lookup"><span data-stu-id="685bd-186">Change the JSON in the `todo` parameter input box so that it looks like the following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy the dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="685bd-187">Cliquez sur **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="685bd-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="685bd-188">L’API ToDoList retourne un code de réponse HTTP 204 indiquant que le processus a réussi.</span><span class="sxs-lookup"><span data-stu-id="685bd-188">The ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="685bd-189">Cliquez sur le premier bouton **Obtenir**, puis, dans cette section de la page, cliquez sur le bouton **Faites un essai**.</span><span class="sxs-lookup"><span data-stu-id="685bd-189">Click the first **Get** button, and then in that section of the page click the **Try it out** button.</span></span>
    
    <span data-ttu-id="685bd-190">La réponse de la méthode Get inclut désormais le nouvel élément de tâche.</span><span class="sxs-lookup"><span data-stu-id="685bd-190">The Get method response now includes the new to do item.</span></span>
15. <span data-ttu-id="685bd-191">Facultatif : essayez également les méthodes Put, Delete et Get by ID.</span><span class="sxs-lookup"><span data-stu-id="685bd-191">Optional: Try also the Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="685bd-192">Fermez le navigateur et arrêtez le débogage de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="685bd-192">Close the browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="685bd-193">Swashbuckle fonctionne avec n’importe quel projet d’API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="685bd-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="685bd-194">Si vous souhaitez ajouter la génération de métadonnées Swagger à un projet existant, il suffit d’installer le package Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="685bd-194">If you want to add Swagger metadata generation to an existing project, just install the Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="685bd-195">Les métadonnées Swagger incluent un ID unique pour chaque opération d’API.</span><span class="sxs-lookup"><span data-stu-id="685bd-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="685bd-196">Par défaut, Swashbuckle peut générer des ID d’opération Swagger en double pour vos méthodes de contrôleur d’API web.</span><span class="sxs-lookup"><span data-stu-id="685bd-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="685bd-197">Cela se produit si les méthodes HTTP du contrôleur sont surchargées, par exemple `Get()` et `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="685bd-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="685bd-198">Pour plus d’informations sur la gestion des surcharges, consultez [Personnaliser les définitions d’API générées par Swashbuckle](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="685bd-198">For information about how to handle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="685bd-199">Si vous créez un projet d’API web dans Visual Studio en utilisant le modèle d’application API Azure, le code qui génère les ID d’opération uniques est automatiquement ajouté au fichier *SwaggerConfig.cs* .</span><span class="sxs-lookup"><span data-stu-id="685bd-199">If you create a Web API project in Visual Studio by using the Azure API App template, code that generates unique operation IDs is automatically added to the *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="685bd-200"><a id="createapiapp"></a> Créer une application API dans Azure et y déployer du code</span><span class="sxs-lookup"><span data-stu-id="685bd-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code to it</span></span>
<span data-ttu-id="685bd-201">Dans cette section, vous allez utiliser les outils Azure intégrés à l’Assistant **Publier le site web** de Visual Studio pour créer une application API dans Azure.</span><span class="sxs-lookup"><span data-stu-id="685bd-201">In this section, you use Azure tools that are integrated into the Visual Studio **Publish Web** wizard to create a new API app in Azure.</span></span> <span data-ttu-id="685bd-202">Ensuite, vous déploierez le projet ToDoListDataAPI vers la nouvelle application API et vous appellerez l’API en exécutant l’interface utilisateur Swagger.</span><span class="sxs-lookup"><span data-stu-id="685bd-202">Then you deploy the ToDoListDataAPI project to the new API app and call the API by running the Swagger UI.</span></span>

1. <span data-ttu-id="685bd-203">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet ToDoListDataAPI, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="685bd-203">In **Solution Explorer**, right-click the ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Cliquez sur Publier dans Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="685bd-205">À l’étape **Profil** de l’Assistant **Publier le site web**, cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="685bd-205">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Cliquez sur Azure App Service dans Publier le site web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="685bd-207">Connectez-vous à votre compte Azure si ce n’est déjà fait, ou actualisez vos informations d’identification si elles ont expiré.</span><span class="sxs-lookup"><span data-stu-id="685bd-207">Sign in to your Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="685bd-208">Dans la boîte de dialogue App Service, choisissez l’**abonnement** Azure que vous souhaitez utiliser, puis cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="685bd-208">In the App Service dialog box, choose the Azure **Subscription** you want to use, and then click **New**.</span></span>
   
    ![Cliquez sur Nouveau dans la boîte de dialogue App Service](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="685bd-210">L’onglet **Hébergement** de la boîte de dialogue **Créer App Service** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="685bd-210">The **Hosting** tab of the **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="685bd-211">Étant donné que vous déployez un projet d’API web dans lequel Swashbuckle est installé, Visual Studio part du principe que vous souhaitez créer une application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want to create an API App.</span></span> <span data-ttu-id="685bd-212">Cela est indiqué par le titre **Nom de l’application API** et par le fait que la liste déroulante **Modifier le type** est définie sur **Application API**.</span><span class="sxs-lookup"><span data-stu-id="685bd-212">This is indicated by the **API App Name** title and by the fact that the **Change Type** drop-down list is set to **API App**.</span></span>
   
    ![Type d’application dans la boîte de dialogue App Service](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="685bd-214">Entrez un **Nom de l’application API** unique dans le domaine *azurewebsites.net* .</span><span class="sxs-lookup"><span data-stu-id="685bd-214">Enter an **API App Name** that is unique in the *azurewebsites.net* domain.</span></span> <span data-ttu-id="685bd-215">Vous pouvez accepter le nom par défaut proposé par Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="685bd-215">You can accept the default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="685bd-216">Si vous entrez un nom déjà utilisé par un autre utilisateur, un point d’exclamation rouge s’affiche à droite.</span><span class="sxs-lookup"><span data-stu-id="685bd-216">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span></span>
   
    <span data-ttu-id="685bd-217">L’URL de l’API sera `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="685bd-217">The URL of the API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="685bd-218">Dans la liste déroulante **Groupe de ressources**, cliquez sur **Nouveau**, puis entrez « ToDoListGroup » ou un autre nom si vous préférez.</span><span class="sxs-lookup"><span data-stu-id="685bd-218">In the **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="685bd-219">Un groupe de ressources est une collection de ressources Azure telles que des applications API, des bases de données, des machines virtuelles, etc.</span><span class="sxs-lookup"><span data-stu-id="685bd-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="685bd-220">Pour ce didacticiel, il est préférable de créer un groupe de ressources, car cela facilite la suppression en une étape de toutes les ressources Azure que vous créez pour le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="685bd-220">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span></span>
   
    <span data-ttu-id="685bd-221">Cette zone vous permet de sélectionner un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) ou d’en créer un avec un nom différent de ceux qui existent déjà dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="685bd-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="685bd-222">Cliquez sur le bouton **Nouveau** situé en regard de la liste déroulante **Plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="685bd-222">Click the **New** button next to the **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="685bd-223">La capture d’écran montre des exemples de valeur pour **Nom de l’application API**, **Abonnement** et **Groupe de ressources**. Vos valeurs seront différentes.</span><span class="sxs-lookup"><span data-stu-id="685bd-223">The screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Boîte de dialogue Créer App Service](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="685bd-225">Au cours des étapes suivantes, vous allez créer un plan de service d’application pour le nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="685bd-225">In the following steps you create an App Service plan for the new resource group.</span></span> <span data-ttu-id="685bd-226">Un plan de service d’application spécifie les ressources de calcul sur lesquelles votre application API s’exécute.</span><span class="sxs-lookup"><span data-stu-id="685bd-226">An App Service plan specifies the compute resources that your API app runs on.</span></span> <span data-ttu-id="685bd-227">Par exemple, si vous choisissez le niveau Gratuit, votre application API s’exécute sur des machines virtuelles partagées, tandis que pour certains niveaux payants, elle s’exécute sur des machines virtuelles dédiées.</span><span class="sxs-lookup"><span data-stu-id="685bd-227">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="685bd-228">Pour plus d’informations sur les plans App Service, consultez [Présentation des plans App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="685bd-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="685bd-229">Dans la boîte de dialogue **Configurer le plan App Service** , entrez « ToDoListPlan » ou un autre nom si vous préférez.</span><span class="sxs-lookup"><span data-stu-id="685bd-229">In the **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="685bd-230">Dans la liste déroulante **Emplacement** , sélectionnez le lieu le plus proche de vous.</span><span class="sxs-lookup"><span data-stu-id="685bd-230">In the **Location** drop-down list, choose the location that is closest to you.</span></span>
   
    <span data-ttu-id="685bd-231">Ce paramètre indique le centre de données Azure dans lequel votre application sera exécutée.</span><span class="sxs-lookup"><span data-stu-id="685bd-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="685bd-232">Choisissez un emplacement proche de vous afin de réduire la [latence](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="685bd-232">Choose a location close to you to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="685bd-233">Dans la liste déroulante **Taille**, cliquez sur **Gratuit**.</span><span class="sxs-lookup"><span data-stu-id="685bd-233">In the **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="685bd-234">Pour ce didacticiel, le niveau tarifaire Gratuit fournit des performances suffisantes.</span><span class="sxs-lookup"><span data-stu-id="685bd-234">For this tutorial, the free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="685bd-235">Dans la boîte de dialogue **Configurer le plan App Service**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="685bd-235">In the **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Cliquez sur OK dans Configurer le plan App Service](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="685bd-237">Dans la boîte de dialogue **Créer App Service**, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="685bd-237">In the **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Cliquez sur Créer dans la boîte de dialogue App Service](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="685bd-239">Visual Studio crée l’application API et un profil de publication qui comporte tous les paramètres nécessaires pour l’application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-239">Visual Studio creates the API app and a publish profile that has all of the required settings for the API app.</span></span> <span data-ttu-id="685bd-240">Puis, il ouvre l’Assistant **Publier le site web** que vous utiliserez pour déployer le projet.</span><span class="sxs-lookup"><span data-stu-id="685bd-240">Then it opens the **Publish Web** wizard, which you'll use to deploy the project.</span></span>
    
    <span data-ttu-id="685bd-241">L’Assistant **Publier le site web** s’ouvre dans l’onglet **Connexion** (illustré ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="685bd-241">The **Publish Web** wizard opens on the **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="685bd-242">Dans l’onglet **Connexion**, les paramètres **Serveur** et **Nom du site** pointent vers votre application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-242">On the **Connection** tab, the **Server** and **Site name** settings point to your API app.</span></span> <span data-ttu-id="685bd-243">Le **nom d’utilisateur** et le **mot de passe** sont les informations d’identification de déploiement créées pour vous par Azure.</span><span class="sxs-lookup"><span data-stu-id="685bd-243">The **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="685bd-244">Après le déploiement, Visual Studio ouvre un navigateur sur l’**URL de destination** (c’est le seul objectif de l’**URL de destination**).</span><span class="sxs-lookup"><span data-stu-id="685bd-244">After deployment, Visual Studio opens a browser to the **Destination URL** (that's the only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="685bd-245">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="685bd-245">Click **Next**.</span></span>
    
    ![Cliquez sur Suivant dans l’onglet Connexion de l’assistant Publier le site Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="685bd-247">L’onglet suivant est l’onglet **Paramètres** (illustré ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="685bd-247">The next tab is the **Settings** tab (shown below).</span></span> <span data-ttu-id="685bd-248">Vous pouvez y modifier l’onglet Configuration de build pour déployer un build de débogage pour le [débogage à distance](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="685bd-248">Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="685bd-249">L’onglet offre également plusieurs **Options de publication des fichiers**:</span><span class="sxs-lookup"><span data-stu-id="685bd-249">The tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="685bd-250">Supprimer les fichiers supplémentaires de la destination</span><span class="sxs-lookup"><span data-stu-id="685bd-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="685bd-251">Précompiler durant la publication</span><span class="sxs-lookup"><span data-stu-id="685bd-251">Precompile during publishing</span></span>
    * <span data-ttu-id="685bd-252">Exclure les fichiers du dossier App_Data</span><span class="sxs-lookup"><span data-stu-id="685bd-252">Exclude files from the App_Data folder</span></span>
    
    <span data-ttu-id="685bd-253">Pour ce didacticiel, vous n’avez besoin d’aucune de ces options.</span><span class="sxs-lookup"><span data-stu-id="685bd-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="685bd-254">Pour obtenir des explications détaillées sur leur action, consultez la rubrique [Déploiement d’un projet web à l’aide de la publication en un clic dans Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="685bd-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="685bd-255">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="685bd-255">Click **Next**.</span></span>
    
    ![Cliquez sur Suivant dans l’onglet Paramètres de l’assistant Publier le site Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="685bd-257">Vient ensuite l’onglet **Aperçu** (illustré ci-dessous), qui vous permet de voir les fichiers qui vont être copiés de votre projet vers l’application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-257">Next is the **Preview** tab (shown below), which gives you an opportunity to see what files are going to be copied from your project to the API app.</span></span> <span data-ttu-id="685bd-258">Lorsque vous déployez un projet vers une application API vers laquelle vous avez déjà déployé auparavant le projet, seuls les fichiers modifiés sont copiés.</span><span class="sxs-lookup"><span data-stu-id="685bd-258">When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied.</span></span> <span data-ttu-id="685bd-259">Si vous souhaitez afficher la liste de ce qui sera copié, vous pouvez cliquer sur le bouton **Démarrer l’aperçu** .</span><span class="sxs-lookup"><span data-stu-id="685bd-259">If you want to see a list of what will be copied, you can click the **Start Preview** button.</span></span>
15. <span data-ttu-id="685bd-260">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="685bd-260">Click **Publish**.</span></span>
    
    ![Cliquez sur Publier dans l’onglet Aperçu de l’assistant Publier le site Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="685bd-262">Visual Studio déploie le projet ToDoListDataAPI vers la nouvelle application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-262">Visual Studio deploys the ToDoListDataAPI project to the new API app.</span></span> <span data-ttu-id="685bd-263">La fenêtre **Sortie** consigne le déploiement réussi, et la page « Créé avec succès » s’affiche dans une fenêtre du navigateur ouverte sur l’URL de l’application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-263">The **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened to the URL of the API app.</span></span>
    
    ![Réussite du déploiement dans la fenêtre de sortie](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Page Application API créée avec succès](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="685bd-266">Ajoutez « swagger » à l’URL dans la barre d’adresses du navigateur, puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="685bd-266">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="685bd-267">(L’URL est `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="685bd-267">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="685bd-268">Le navigateur affiche la même interface utilisateur de Swagger que précédemment, mais elle s’exécute désormais dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="685bd-268">The browser displays the same Swagger UI that you saw earlier, but now it's running in the cloud.</span></span> <span data-ttu-id="685bd-269">La méthode Get vous ramène aux 2 éléments d’action par défaut.</span><span class="sxs-lookup"><span data-stu-id="685bd-269">Try out the Get method, and you see that you're back to the default 2 to-do items.</span></span> <span data-ttu-id="685bd-270">Les modifications apportées précédemment ont été enregistrées dans la mémoire de l’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="685bd-270">The changes you made earlier were saved in memory in the local machine.</span></span>
17. <span data-ttu-id="685bd-271">Ouvrez le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="685bd-271">Open the [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="685bd-272">Le portail Azure est une interface web permettant de gérer les ressources Azure telles que les applications API.</span><span class="sxs-lookup"><span data-stu-id="685bd-272">The Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="685bd-273">Cliquez sur **Plus de services > App Services**.</span><span class="sxs-lookup"><span data-stu-id="685bd-273">Click **More Services > App Services**.</span></span>
    
    ![Parcourir App Services](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="685bd-275">Dans le panneau **App Services** , recherchez votre nouvelle application API et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="685bd-275">In the **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="685bd-276">(Dans le portail Azure, les fenêtres qui s’ouvrent sur la droite sont appelées des *panneaux*.)</span><span class="sxs-lookup"><span data-stu-id="685bd-276">(In the Azure portal, windows that open to the right are called *blades*.)</span></span>
    
    ![Panneau App Services](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="685bd-278">Deux panneaux s’ouvrent.</span><span class="sxs-lookup"><span data-stu-id="685bd-278">Two blades open.</span></span> <span data-ttu-id="685bd-279">L’un présentant une vue d’ensemble de l’application API et l’autre contenant une longue liste des paramètres que vous pouvez afficher et modifier.</span><span class="sxs-lookup"><span data-stu-id="685bd-279">One blade has an overview of the API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="685bd-280">Dans le panneau **Paramètres**, recherchez la section **API**, puis cliquez sur **Définition de l’API**.</span><span class="sxs-lookup"><span data-stu-id="685bd-280">In the **Settings** blade, find the **API** section and click **API Definition**.</span></span>
    
    ![Définition de l’API dans le panneau Paramètres](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="685bd-282">Le panneau **Définition de l’API** vous permet de spécifier l’URL qui renvoie les métadonnées Swagger 2.0 au format JSON.</span><span class="sxs-lookup"><span data-stu-id="685bd-282">The **API Definition** blade lets you specify the URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="685bd-283">Quand Visual Studio crée l’application API, il définit l’URL de définition de l’API, à savoir l’URL de base de l’application API plus `/swagger/docs/v1`sur la valeur par défaut des métadonnées générées par Swashbuckle que vous avez vues précédemment.</span><span class="sxs-lookup"><span data-stu-id="685bd-283">When Visual Studio creates the API app, it sets the API definition URL to the default value for Swashbuckle-generated metadata that you saw earlier, which is the API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL de définition de l’API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="685bd-285">Quand vous sélectionnez une application API pour laquelle générer le code client, Visual Studio extrait les métadonnées à partir de cette URL.</span><span class="sxs-lookup"><span data-stu-id="685bd-285">When you select an API app to generate client code for it, Visual Studio retrieves the metadata from this URL.</span></span>

## <span data-ttu-id="685bd-286"><a id="codegen"></a> Générer le code client pour la couche Données</span><span class="sxs-lookup"><span data-stu-id="685bd-286"><a id="codegen"></a> Generate client code for the data tier</span></span>
<span data-ttu-id="685bd-287">L’un des avantages de l’intégration de Swagger dans les applications API Azure est la génération de code automatique.</span><span class="sxs-lookup"><span data-stu-id="685bd-287">One of the advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="685bd-288">Les classes de client générées facilitent l’écriture du code qui appelle une application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-288">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="685bd-289">Le projet ToDoListAPI comporte déjà le code client généré, mais vous allez le supprimer et le régénérer lors des étapes suivantes pour voir comment procéder.</span><span class="sxs-lookup"><span data-stu-id="685bd-289">The ToDoListAPI project already has the generated client code, but in the following steps you'll delete it and regenerate it to see how to do the code generation.</span></span>

1. <span data-ttu-id="685bd-290">Dans l’ **Explorateur de solutions**de Visual Studio, dans le projet ToDoListAPI, supprimez le dossier *ToDoListDataAPI* .</span><span class="sxs-lookup"><span data-stu-id="685bd-290">In Visual Studio **Solution Explorer**, in the ToDoListAPI project, delete the *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="685bd-291">**Attention : supprimez uniquement le dossier, et non le projet ToDoListDataAPI.**</span><span class="sxs-lookup"><span data-stu-id="685bd-291">**Caution: Delete only the folder, not the ToDoListDataAPI project.**</span></span>
   
    ![Suppression du code client généré](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="685bd-293">Ce dossier a été créé à l’aide du processus de génération de code que vous allez aborder.</span><span class="sxs-lookup"><span data-stu-id="685bd-293">This folder was created by using the code generation process that you're about to go through.</span></span>
2. <span data-ttu-id="685bd-294">Cliquez avec le bouton droit sur le projet ToDoListAPI, puis cliquez sur **Ajouter > Client d’API REST**.</span><span class="sxs-lookup"><span data-stu-id="685bd-294">Right-click the ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Ajouter un client API REST dans Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="685bd-296">Dans la boîte de dialogue **Ajouter un client d’API REST**, cliquez sur **URL Swagger**, puis sur **Sélectionner une ressource Azure**.</span><span class="sxs-lookup"><span data-stu-id="685bd-296">In the **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Sélectionner une ressource Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="685bd-298">Dans la boîte de dialogue **App Service**, développez le groupe de ressources que vous utilisez pour ce didacticiel, sélectionnez votre application API, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="685bd-298">In the **App Service** dialog box, expand the resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Sélectionnez une application API pour la génération de code](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="685bd-300">Notez que lorsque vous revenez à la boîte de dialogue **Client API REST** , la zone de texte a été remplie avec la valeur de l’URL de définition d’API que vous avez vue précédemment dans le portail.</span><span class="sxs-lookup"><span data-stu-id="685bd-300">Notice that when you return to the **Add REST API Client** dialog, the text box has been filled in with the API definition URL value that you saw earlier in the portal.</span></span>
   
    ![URL de définition de l’API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="685bd-302">Pour obtenir les métadonnées nécessaires à la génération du code, vous pouvez également saisir l’URL directement au lieu de passer par la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="685bd-302">An alternative way to get metadata for code generation is to enter the URL directly instead of going through the browse dialog.</span></span> <span data-ttu-id="685bd-303">Ou, si vous souhaitez générer le code client avant le déploiement vers Azure, vous pouvez exécuter localement le projet d’API web, accéder à l’URL qui fournit le fichier JSON Swagger, enregistrer le fichier et utiliser l’option **Sélectionner un fichier de métadonnées Swagger existant** .</span><span class="sxs-lookup"><span data-stu-id="685bd-303">Or if you want to generate client code before deploying to Azure, you could run the Web API project locally, go to the URL that provides the Swagger JSON file, save the file, and use the **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="685bd-304">Dans la boîte de dialogue **Ajouter un client API REST**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="685bd-304">In the **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="685bd-305">Visual Studio crée un dossier nommé d’après l’application API et il génère des classes de client.</span><span class="sxs-lookup"><span data-stu-id="685bd-305">Visual Studio creates a folder named after the API app and generates client classes.</span></span>
   
    ![Fichiers de code pour le client généré](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="685bd-307">Dans le projet ToDoListAPI, ouvrez *Controllers\ToDoListController.cs* pour afficher le code de la ligne 40 qui appelle l’API à l’aide du client généré.</span><span class="sxs-lookup"><span data-stu-id="685bd-307">In the ToDoListAPI project, open *Controllers\ToDoListController.cs* to see the code at line 40  that calls the API by using the generated client.</span></span>
   
    <span data-ttu-id="685bd-308">L’extrait de code suivant montre comment instancier l’objet client et appeler la méthode Get.</span><span class="sxs-lookup"><span data-stu-id="685bd-308">The following snippet shows how the code instantiates the client object and calls the Get method.</span></span>
   
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
   
    <span data-ttu-id="685bd-309">Le paramètre de constructeur obtient l’URL de point de terminaison à partir du paramètre d’application `toDoListDataAPIURL` .</span><span class="sxs-lookup"><span data-stu-id="685bd-309">The constructor parameter gets the endpoint URL from  the `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="685bd-310">Dans le fichier Web.config, cette valeur est définie sur l’URL IIS Express locale du projet d’API pour vous permettre d’exécuter l’application localement.</span><span class="sxs-lookup"><span data-stu-id="685bd-310">In the Web.config file, that value is set to the local IIS Express URL of the API project so that you can run the application locally.</span></span> <span data-ttu-id="685bd-311">Si vous omettez le paramètre de constructeur, le point de terminaison par défaut est l’URL à partir de laquelle vous avez généré le code.</span><span class="sxs-lookup"><span data-stu-id="685bd-311">If you omit the constructor parameter, the default endpoint is the URL that you generated the code from.</span></span>
7. <span data-ttu-id="685bd-312">Votre classe client est générée avec un nom différent selon le nom de votre application API. Modifiez ce code dans *Controllers\ToDoListController.cs* pour que le nom de type corresponde à ce qui a été généré dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="685bd-312">Your client class will be generated with a different name based on your API app name; change the code in *Controllers\ToDoListController.cs* so that the type name matches what was generated in your project.</span></span> <span data-ttu-id="685bd-313">Par exemple, si vous avez nommé votre application API ToDoListDataAPI071316, vous modifieriez ce code :</span><span class="sxs-lookup"><span data-stu-id="685bd-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="685bd-314">De la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="685bd-314">to this:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-to-host-the-middle-tier"></a><span data-ttu-id="685bd-315">Créer une application API pour héberger la couche intermédiaire</span><span class="sxs-lookup"><span data-stu-id="685bd-315">Create an API app to host the middle tier</span></span>
<span data-ttu-id="685bd-316">Vous avez [créé l’application API de la couche Données et déployé du code dans celle-ci](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="685bd-316">Earlier you [created the data tier API app and deployed code to it](#createapiapp).</span></span>  <span data-ttu-id="685bd-317">Maintenant vous suivez la même procédure pour l’application API de niveau intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="685bd-317">Now you follow the same procedure for the middle tier API app.</span></span>

1. <span data-ttu-id="685bd-318">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet ToDoListAPI de la couche intermédiaire (et non sur le projet ToDoListDataAPI), puis sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="685bd-318">In **Solution Explorer**, right-click the middle tier ToDoListAPI  project (not the data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Cliquez sur Publier dans Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="685bd-320">Sous l’onglet **Profil** de l’Assistant **Publier le site web**, cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="685bd-320">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="685bd-321">Dans la boîte de dialogue **App Service**, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="685bd-321">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="685bd-322">Dans l’onglet **Hébergement** de la boîte de dialogue **Créer App Service**, acceptez le **nom d’application API** par défaut ou entrez un nom unique dans le domaine *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="685bd-322">In the **Hosting** tab of the **Create App Service** dialog box, accept the default **API App Name** or enter a name that is unique in the *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="685bd-323">Choisissez l’ **abonnement** Azure que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="685bd-323">Choose the Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="685bd-324">Dans la liste déroulante **Groupe de ressources** , choisissez le groupe de ressources créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="685bd-324">In the **Resource Group** drop-down, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="685bd-325">Dans la liste déroulante **Plan App Service** , choisissez le plan créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="685bd-325">In the **App Service Plan** drop-down, choose the same plan you created earlier.</span></span> <span data-ttu-id="685bd-326">Il est défini par défaut sur cette valeur.</span><span class="sxs-lookup"><span data-stu-id="685bd-326">It will default to that value.</span></span>
8. <span data-ttu-id="685bd-327">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="685bd-327">Click **Create**.</span></span>
   
    <span data-ttu-id="685bd-328">Visual Studio crée l’application API et un profil de publication pour celle-ci, puis affiche l’étape **Connexion** de l’Assistant **Publier le site web**.</span><span class="sxs-lookup"><span data-stu-id="685bd-328">Visual Studio creates the API app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
9. <span data-ttu-id="685bd-329">À l’étape **Connexion** de l’Assistant **Publier le site web**, cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="685bd-329">In the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="685bd-330">Visual Studio déploie le projet ToDoListAPI vers la nouvelle application API et ouvre un navigateur à l’URL de l’application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-330">Visual Studio deploys the ToDoListAPI project to the new API app and opens a browser to the URL of the API app.</span></span> <span data-ttu-id="685bd-331">Une page s’affiche pour confirmer la création.</span><span class="sxs-lookup"><span data-stu-id="685bd-331">The "successfully created" page appears.</span></span>

## <a name="configure-the-middle-tier-to-call-the-data-tier"></a><span data-ttu-id="685bd-332">Configurer la couche intermédiaire pour appeler la couche Données</span><span class="sxs-lookup"><span data-stu-id="685bd-332">Configure the middle tier to call the data tier</span></span>
<span data-ttu-id="685bd-333">Si vous appelez maintenant l’application API de la couche intermédiaire, elle essaie d’appeler la couche Données à l’aide de l’URL d’hôte local qui figure toujours dans le fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="685bd-333">If you called the middle tier API app now, it would try to call the data tier using the localhost URL that is still in the Web.config file.</span></span> <span data-ttu-id="685bd-334">Dans cette section, vous entrez l’URL de l’application API de la couche Données dans un paramètre d’environnement de l’application API de la couche intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="685bd-334">In this section you enter the data tier API app URL into an environment setting in the middle tier API app.</span></span> <span data-ttu-id="685bd-335">Lorsque le code de l’application API de la couche intermédiaire récupère le paramètre d’URL de la couche Données, le paramètre d’environnement remplace ce qui figure dans le fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="685bd-335">When the code in the middle tier API app retrieves the data tier URL setting, the environment setting will override what's in the Web.config file.</span></span>

1. <span data-ttu-id="685bd-336">Dans le [portail Azure](https://portal.azure.com/), accédez au panneau **Application API** de l’application API que vous avez créée pour héberger le projet TodoListAPI (de la couche intermédiaire).</span><span class="sxs-lookup"><span data-stu-id="685bd-336">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that you created to host the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="685bd-337">Dans le panneau **Paramètres** de l’application API, cliquez sur **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="685bd-337">In the API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="685bd-338">Dans le panneau **Paramètres de l’application** de l’application API, faites défiler l’écran jusqu’à la section **Paramètres de l’application** et ajoutez la clé et la valeur suivantes.</span><span class="sxs-lookup"><span data-stu-id="685bd-338">In the API App's **Application Settings** blade, scroll down to the **App settings** section and add the following key and value.</span></span> <span data-ttu-id="685bd-339">La valeur sera l’URL de la première application API que vous avez publiée dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="685bd-339">The value will be the URL of the first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="685bd-340">**Clé**</span><span class="sxs-lookup"><span data-stu-id="685bd-340">**Key**</span></span> | <span data-ttu-id="685bd-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="685bd-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="685bd-342">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="685bd-342">**Value**</span></span> |<span data-ttu-id="685bd-343">https://{nom de votre application API de la couche Données}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="685bd-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="685bd-344">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="685bd-344">**Example**</span></span> |<span data-ttu-id="685bd-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="685bd-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="685bd-346">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="685bd-346">Click **Save**.</span></span>
   
    ![Cliquez sur Enregistrer pour les paramètres de l’application](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="685bd-348">Lorsque le code sera exécuté dans Azure, cette valeur remplacera dès lors l’URL de l’hôte local qui se trouve dans le fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="685bd-348">When the code runs in Azure, this value will now override the localhost URL that is in the Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="685bd-349">Test</span><span class="sxs-lookup"><span data-stu-id="685bd-349">Test</span></span>
1. <span data-ttu-id="685bd-350">Dans une fenêtre de navigateur, accédez à l’URL de la nouvelle application API de la couche intermédiaire que vous venez de créer pour ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="685bd-350">In a browser window, browse to the URL of the new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="685bd-351">Vous pouvez y accéder en cliquant dans le portail sur l’URL se trouvant dans le volet principal de l’application API.</span><span class="sxs-lookup"><span data-stu-id="685bd-351">You can get there by clicking the URL in the API app's main blade in the portal.</span></span>
2. <span data-ttu-id="685bd-352">Ajoutez « swagger » à l’URL dans la barre d’adresses du navigateur, puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="685bd-352">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="685bd-353">(L’URL est `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="685bd-353">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="685bd-354">Le navigateur affiche la même interface utilisateur de Swagger que vous avez vue précédemment pour ToDoListDataAPI, mais `owner` n’est pas un champ obligatoire pour l’opération Get, car l’application API de la couche intermédiaire envoie automatiquement cette valeur à l’application API de la couche Données.</span><span class="sxs-lookup"><span data-stu-id="685bd-354">The browser displays the same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for the Get operation, because the middle tier API app is sending that value to the data tier API app for you.</span></span> <span data-ttu-id="685bd-355">(Lorsque vous effectuez les didacticiels d’authentification, la couche intermédiaire envoie les ID utilisateur réels pour le paramètre `owner`. Pour le moment, elle code un astérisque de manière irréversible.)</span><span class="sxs-lookup"><span data-stu-id="685bd-355">(When you do the authentication tutorials, the middle tier will send actual user IDs for the `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="685bd-356">Essayez la méthode Get ainsi que d’autres méthodes pour confirmer que l’application API de couche intermédiaire appelle correctement l’application API de la couche de données.</span><span class="sxs-lookup"><span data-stu-id="685bd-356">Try out the Get method and the other methods to validate that the middle tier API app is successfully calling the data tier API app.</span></span>
   
    ![Méthode Get de l’interface utilisateur Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="685bd-358">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="685bd-358">Troubleshooting</span></span>
<span data-ttu-id="685bd-359">Si vous rencontrez un problème tout au long de ce didacticiel, voici quelques suggestions de dépannage :</span><span class="sxs-lookup"><span data-stu-id="685bd-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="685bd-360">Assurez-vous que vous disposez de la version la plus récente du [Kit de développement logiciel (SDK) Azure pour . NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="685bd-360">Make sure that you're using the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="685bd-361">Deux des noms de projet sont similaires (ToDoListAPI et ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="685bd-361">Two of the project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="685bd-362">Si les éléments ne s’affichent pas comme décrit dans les instructions lorsque vous travaillez sur un projet, assurez-vous d’avoir ouvert le projet approprié.</span><span class="sxs-lookup"><span data-stu-id="685bd-362">If things don't look as described in the instructions when you are working with a project, make sure you have opened the correct project.</span></span>
* <span data-ttu-id="685bd-363">Si vous vous trouvez sur un réseau d’entreprise et que vous essayez d’exécuter un déploiement au-delà d’un pare-feu dans Azure App Service, assurez-vous que les ports 443 et 8172 sont ouverts pour le déploiement Web.</span><span class="sxs-lookup"><span data-stu-id="685bd-363">If you're on a corporate network and are trying to deploy to Azure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="685bd-364">Si vous ne pouvez pas ouvrir ces ports, vous pouvez utiliser d’autres méthodes de déploiement.</span><span class="sxs-lookup"><span data-stu-id="685bd-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="685bd-365">Voir [Déploiement de votre application dans Azure App Service](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="685bd-365">See [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="685bd-366">Erreurs de type « Les noms d’itinéraires doivent être uniques » : ces erreurs peuvent s’afficher si vous déployez accidentellement le projet incorrect dans une application API, puis déployez ultérieurement le projet correct.</span><span class="sxs-lookup"><span data-stu-id="685bd-366">"Route names must be unique" errors -- you could get these if you accidentally deploy the wrong project to an API app and then later deploy the correct one to it.</span></span> <span data-ttu-id="685bd-367">Pour corriger cette erreur, redéployez le projet correct dans l’application API, puis dans l’onglet **Paramètres** de l’Assistant **Publier le site web**, sélectionnez **Supprimer les fichiers supplémentaires à la destination**.</span><span class="sxs-lookup"><span data-stu-id="685bd-367">To correct this, redeploy the correct project to the API app, and on the **Settings** tab of the **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="685bd-368">Une fois que vous aurez configuré votre application web ASP.NET dans Azure App Service, vous souhaiterez peut-être en savoir plus sur les fonctionnalités de Visual Studio qui simplifient la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="685bd-368">After you have your ASP.NET API app running in Azure App Service, you may want to learn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="685bd-369">Pour plus d’informations sur la journalisation, le débogage à distance, etc. consultez la section [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md) (Résolution des problèmes des applications web Azure App Service dans Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="685bd-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="685bd-370">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="685bd-370">Next steps</span></span>
<span data-ttu-id="685bd-371">Vous avez vu comment déployer des projets d’API web existants sur des applications API, générer du code client pour les applications API et utiliser des applications API à partir de clients .NET.</span><span class="sxs-lookup"><span data-stu-id="685bd-371">You've seen how to deploy existing Web API projects to API apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="685bd-372">Le didacticiel suivant de cette série montre comment [utiliser CORS pour utiliser des applications API à partir de clients JavaScript](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="685bd-372">The next tutorial in this series shows how to [use CORS to consume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="685bd-373">Pour plus d’informations sur la génération de code client, reportez-vous au référentiel [Azure/AutoRest](https://github.com/azure/autorest) sur GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="685bd-373">For more information about client code generation, see the [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com.</span></span> <span data-ttu-id="685bd-374">Pour obtenir de l’aide à la résolution de problèmes relatifs au client généré, signalez le [problème dans le référentiel AutoRest](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="685bd-374">For help with problems using the generated client, open an [issue in the AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="685bd-375">Si vous souhaitez créer des projets d’application API à partir de zéro, utilisez le modèle d’ **Application API Azure** .</span><span class="sxs-lookup"><span data-stu-id="685bd-375">If you want to create new API app projects from scratch, use the **Azure API App** template.</span></span>

![Modèle d’application API dans Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="685bd-377">Choisir le modèle de projet d’**Application API Azure** revient à sélectionner le modèle ASP.NET 4.5.2 **Vide**, à cocher la case pour ajouter la prise en charge d’API web et à installer le package NuGet Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="685bd-377">The **Azure API App** project template is equivalent to choosing the **Empty** ASP.NET 4.5.2 template, clicking the check box to add Web API support, and installing the Swashbuckle NuGet package.</span></span> <span data-ttu-id="685bd-378">En outre, le modèle ajoute du code de configuration Swashbuckle conçu pour empêcher la création d’ID d’opération Swagger en double.</span><span class="sxs-lookup"><span data-stu-id="685bd-378">In addition, the template adds some Swashbuckle configuration code designed to prevent the creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="685bd-379">Une fois le projet d’application API créé, vous pouvez le déployer dans une application API en procédant comme indiqué dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="685bd-379">Once you've created an API App project, you can deploy it to an API app the same way you saw in this tutorial.</span></span>

