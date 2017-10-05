---
title: Prise en charge de CORS dans App Service | Microsoft Docs
description: "Découvrez comment utiliser la prise en charge de CORS dans Azure App Service."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: f8373cf5b2e06e6c71bce51cd9e9d5123eea7cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="d6330-103">Consommer une application API à partir de JavaScript à l’aide de CORS</span><span class="sxs-lookup"><span data-stu-id="d6330-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="d6330-104">App Service prend en charge [CORS (Cross Origin Resource Sharing)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), ce qui permet aux clients JavaScript d’effectuer des appels entre domaines vers des API hébergées dans les applications API.</span><span class="sxs-lookup"><span data-stu-id="d6330-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients to make cross-domain calls to APIs that are hosted in API apps.</span></span> <span data-ttu-id="d6330-105">App Service vous permet de configurer CORS sur votre API sans y écrire de code.</span><span class="sxs-lookup"><span data-stu-id="d6330-105">App Service lets you configure CORS access to your API without writing any code in your API.</span></span>

<span data-ttu-id="d6330-106">Cet article contient deux sections :</span><span class="sxs-lookup"><span data-stu-id="d6330-106">This article contains two sections:</span></span>

* <span data-ttu-id="d6330-107">La section [Configuration de CORS](#corsconfig) explique de façon générale comment configurer CORS pour toute application API, web ou mobile.</span><span class="sxs-lookup"><span data-stu-id="d6330-107">The [How to configure CORS](#corsconfig) section explains in general how to configure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="d6330-108">Cette section s’applique également à toutes les infrastructures prises en charge par App Service, y compris .NET, Node.js et Java.</span><span class="sxs-lookup"><span data-stu-id="d6330-108">It applies equally to all frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="d6330-109">À partir de la section [Suite des didacticiels dédiés à la prise en main de .NET](#tutorialstart), cet article sous forme de didacticiel démontre la prise en charge de CORS en s’appuyant sur la procédure que vous avez suivie dans le [premier didacticiel dédié à la prise en main d’API Apps](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6330-109">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the article is a tutorial that demonstrates CORS support by building on what you did in [the first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="d6330-110"><a id="corsconfig"></a> Configuration de CORS dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d6330-110"><a id="corsconfig"></a> How to configure CORS in Azure App Service</span></span>
<span data-ttu-id="d6330-111">Vous pouvez configurer CORS dans le portail Azure ou à l’aide des outils [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6330-111">You can configure CORS in the Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-the-azure-portal"></a><span data-ttu-id="d6330-112">Configuration de CORS dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d6330-112">Configure CORS in the Azure portal</span></span>
1. <span data-ttu-id="d6330-113">Dans votre navigateur, accédez au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d6330-113">In a browser go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d6330-114">Cliquez sur **App Services**, puis sur le nom de votre application API.</span><span class="sxs-lookup"><span data-stu-id="d6330-114">Click **App Services**, and then click the name of your API app.</span></span>
   
    ![Sélectionnez l’application API dans le portail](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="d6330-116">Dans le panneau **Paramètres** qui s’ouvre à droite du panneau **application API**, recherchez la section **API**, puis cliquez sur **CORS**.</span><span class="sxs-lookup"><span data-stu-id="d6330-116">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Sélectionnez CORS dans le panneau Paramètres](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="d6330-118">Dans la zone de texte, saisissez la ou les URL depuis laquelle/lesquelles vous souhaitez autoriser les appels JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d6330-118">In the text box enter the URL or URLs that you want to allow JavaScript calls to come from.</span></span>

    <span data-ttu-id="d6330-119">Par exemple, si vous avez déployé votre application JavaScript sur une application web nommée todolistangular, saisissez « https://todolistangular.azurewebsites.net ».</span><span class="sxs-lookup"><span data-stu-id="d6330-119">For example, if you deployed your JavaScript application to a web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="d6330-120">Vous pouvez également saisir un astérisque (*) pour indiquer que tous les domaines d’origine sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="d6330-120">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="d6330-121">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d6330-121">Click **Save**.</span></span>
   
   ![Cliquez sur Enregistrer.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="d6330-123">Lorsque vous cliquez sur **Enregistrer**, l’application API accepte les appels JavaScript depuis les URL spécifiées.</span><span class="sxs-lookup"><span data-stu-id="d6330-123">After you click **Save**, the API app will accept JavaScript calls from the specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="d6330-124">Configurer CORS à l’aide des outils Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d6330-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="d6330-125">Vous pouvez également configurer CORS pour une application API à l’aide des [modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) dans les outils de ligne de commande, par exemple [Azure PowerShell](/powershell/azureps-cmdlets-docs) et l’[interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d6330-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="d6330-126">Pour obtenir un exemple de modèle Azure Resource Manager qui définit la propriété CORS, ouvrez le [fichier azuredeploy.json dans le référentiel correspondant à l’exemple d’application de ce didacticiel](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="d6330-126">For an example of an Azure Resource Manager template that sets the CORS property, open the [azuredeploy.json file in the repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="d6330-127">Recherchez la section du modèle qui ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d6330-127">Find the section of the template that looks like the following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="d6330-128"><a id="tutorialstart"></a> Suite du didacticiel dédié à la prise en main de .NET</span><span class="sxs-lookup"><span data-stu-id="d6330-128"><a id="tutorialstart"></a> Continuing the .NET getting-started tutorial</span></span>
<span data-ttu-id="d6330-129">Si vous suivez la série dédiée à la mise en route de Node.js ou Java pour les applications API, vous avez terminé la série de mise en route.</span><span class="sxs-lookup"><span data-stu-id="d6330-129">If you are following the Node.js or Java getting-started series for API apps, you have completed the getting started series.</span></span> <span data-ttu-id="d6330-130">Passez à la section [Étapes suivantes](#next-steps) pour trouver des suggestions afin d’en savoir plus sur les applications API.</span><span class="sxs-lookup"><span data-stu-id="d6330-130">Skip to the [Next steps](#next-steps) section to find suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="d6330-131">Le reste de cet article, qui s’inscrit dans le prolongement de la série dédiée à la prise en main de .NET, suppose que vous avez correctement exécuté [le premier didacticiel](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6330-131">The remainder of this article is a continuation of the .NET getting-started series and assumes that you successfully completed [the first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-the-todolistangular-project-to-a-new-web-app"></a><span data-ttu-id="d6330-132">Déployer le projet ToDoListAngular dans une nouvelle application web</span><span class="sxs-lookup"><span data-stu-id="d6330-132">Deploy the ToDoListAngular project to a new web app</span></span>
<span data-ttu-id="d6330-133">Dans [le premier didacticiel](app-service-api-dotnet-get-started.md), vous avez créé une application API de niveau intermédiaire ainsi qu’une application API de la couche Données.</span><span class="sxs-lookup"><span data-stu-id="d6330-133">In [the first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="d6330-134">Dans ce didacticiel, vous allez créer une application web monopage (SPA) qui appelle l’API de niveau intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="d6330-134">In this tutorial you create a single-page application (SPA) web app that calls the middle tier API app.</span></span> <span data-ttu-id="d6330-135">Pour que cette application puisse fonctionner, vous devez activer CORS sur l’application API de niveau intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="d6330-135">For the SPA to work you have to enable CORS on the middle tier API app.</span></span> 

<span data-ttu-id="d6330-136">Dans l’ [exemple d’application ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), le projet ToDoListAngular est un client AngularJS simple qui appelle le projet web d’API ToDoListAPI de niveau intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="d6330-136">In the [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), the ToDoListAngular project is a simple AngularJS client that calls the middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="d6330-137">Le code JavaScript du fichier *app/scripts/todoListSvc.js* appelle l’API à l’aide du fournisseur HTTP AngularJS.</span><span class="sxs-lookup"><span data-stu-id="d6330-137">The JavaScript code in the *app/scripts/todoListSvc.js* file calls the API by using the AngularJS HTTP provider.</span></span> 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-the-todolistangular-project"></a><span data-ttu-id="d6330-138">Créer une application web pour le projet ToDoListAngular</span><span class="sxs-lookup"><span data-stu-id="d6330-138">Create a new web app for the ToDoListAngular project</span></span>
<span data-ttu-id="d6330-139">La procédure de création d’une application web App Service et de déploiement d’un projet dans cette application est identique à celle que vous avez vue pour la [création et le déploiement d’une application API dans le premier didacticiel de cette série](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="d6330-139">The procedure to create a new App Service web app and deploy a project to it is similar to what you saw for [creating and deploying an API app in the first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="d6330-140">à ceci près que le type d’application est **application web** au lieu d’**application API**.</span><span class="sxs-lookup"><span data-stu-id="d6330-140">The only difference is that the app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="d6330-141">Pour les captures d’écran des boîtes de dialogue, voir</span><span class="sxs-lookup"><span data-stu-id="d6330-141">For screen shots of the dialogs, see</span></span> 

1. <span data-ttu-id="d6330-142">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet ToDoListAngular, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="d6330-142">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="d6330-143">Sous l’onglet **Profil** de l’Assistant **Publier le site web**, cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="d6330-143">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="d6330-144">Dans la boîte de dialogue **App Service**, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d6330-144">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="d6330-145">Sous l’onglet **Hébergement** de la boîte de dialogue **Créer App Service**, entrez un **Nom de l’application web** unique dans le domaine *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="d6330-145">In the **Hosting** tab of the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="d6330-146">Choisissez l’ **abonnement** Azure que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d6330-146">Choose the Azure **Subscription** you want to work with.</span></span>
6. <span data-ttu-id="d6330-147">Dans la liste déroulante **Groupe de ressources** , choisissez le groupe de ressources créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d6330-147">In the **Resource Group** drop-down list, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="d6330-148">Dans la liste déroulante **Plan App Service** , choisissez le plan créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d6330-148">In the **App Service Plan** drop-down list, choose the same plan you created earlier.</span></span> 
8. <span data-ttu-id="d6330-149">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d6330-149">Click **Create**.</span></span>
   
    <span data-ttu-id="d6330-150">Visual Studio crée l’application web, crée un profil de publication pour elle et affiche l’étape **Connexion** de l’Assistant **Publier le site web**.</span><span class="sxs-lookup"><span data-stu-id="d6330-150">Visual Studio creates the web app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="d6330-151">Attendez encore avant de cliquer sur **Publier** .</span><span class="sxs-lookup"><span data-stu-id="d6330-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="d6330-152">Dans la section suivante, vous allez configurer la nouvelle application web de manière à appeler l’application API de niveau intermédiaire exécutée dans App Service.</span><span class="sxs-lookup"><span data-stu-id="d6330-152">In the following section, you configure the new web app to call the middle tier API app that is running in App Service.</span></span> 

### <a name="set-the-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="d6330-153">Définir l’URL de niveau intermédiaire dans les paramètres de l’application web</span><span class="sxs-lookup"><span data-stu-id="d6330-153">Set the middle tier URL in web app settings</span></span>
1. <span data-ttu-id="d6330-154">Dans le [portail Azure](https://portal.azure.com/), accédez au panneau **application web** de l’application web que vous avez créée pour héberger le projet TodoListAngular (frontal).</span><span class="sxs-lookup"><span data-stu-id="d6330-154">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **Web App** blade for the web app that you created to host the TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="d6330-155">Cliquez sur **Paramètres > Paramètres de l'application**.</span><span class="sxs-lookup"><span data-stu-id="d6330-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="d6330-156">Dans la section **Paramètres de l’application** , ajoutez la clé et la valeur suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6330-156">In the **App settings** section, add the following key and value:</span></span>
   
   | <span data-ttu-id="d6330-157">Clé</span><span class="sxs-lookup"><span data-stu-id="d6330-157">Key</span></span> | <span data-ttu-id="d6330-158">Valeur</span><span class="sxs-lookup"><span data-stu-id="d6330-158">Value</span></span> | <span data-ttu-id="d6330-159">Exemple</span><span class="sxs-lookup"><span data-stu-id="d6330-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="d6330-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="d6330-160">toDoListAPIURL</span></span> |<span data-ttu-id="d6330-161">https://{nom de votre application API de niveau intermédiaire}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="d6330-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="d6330-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="d6330-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="d6330-163">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d6330-163">Click **Save**.</span></span>
   
    <span data-ttu-id="d6330-164">Une fois le code exécuté dans Azure, cette valeur remplace l’URL de l’hôte local qui se trouve dans le fichier *Web.config* .</span><span class="sxs-lookup"><span data-stu-id="d6330-164">When the code runs in Azure, this value overrides the localhost URL that is in the *Web.config* file.</span></span> 
   
    <span data-ttu-id="d6330-165">Le code permettant d’obtenir la valeur du paramètre se trouve dans le fichier *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="d6330-165">The code that gets the setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="d6330-166">Le code du fichier *todoListSvc.js* utilise le paramètre :</span><span class="sxs-lookup"><span data-stu-id="d6330-166">The code in *todoListSvc.js* uses the setting:</span></span>
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-the-todolistangular-web-project-to-the-new-web-app"></a><span data-ttu-id="d6330-167">Déployer le projet web ToDoListAngular dans la nouvelle application web</span><span class="sxs-lookup"><span data-stu-id="d6330-167">Deploy the ToDoListAngular web project to the new web app</span></span>
* <span data-ttu-id="d6330-168">Dans Visual Studio, à l’étape **Connexion** de l’Assistant **Publier le site web**, cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="d6330-168">In Visual Studio, in the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="d6330-169">Visual Studio déploie le projet ToDoListAngular dans la nouvelle application web et ouvre un navigateur à l’URL de l’application web.</span><span class="sxs-lookup"><span data-stu-id="d6330-169">Visual Studio deploys the ToDoListAngular project to the new web app and opens a browser to the URL of the web app.</span></span> 

### <a name="test-the-application-without-cors-enabled"></a><span data-ttu-id="d6330-170">Tester l’application sans activer CORS</span><span class="sxs-lookup"><span data-stu-id="d6330-170">Test the application without CORS enabled</span></span>
1. <span data-ttu-id="d6330-171">Dans les outils de développement de votre navigateur, ouvrez la fenêtre de Console.</span><span class="sxs-lookup"><span data-stu-id="d6330-171">In your browser Developer Tools, open the Console window.</span></span>
2. <span data-ttu-id="d6330-172">Dans la fenêtre de navigateur qui affiche l’interface utilisateur AngularJS, cliquez sur le lien **Todo List** .</span><span class="sxs-lookup"><span data-stu-id="d6330-172">In the browser window that displays the AngularJS UI, click the **To Do List** link.</span></span>
   
    <span data-ttu-id="d6330-173">Le code JavaScript essaie d’appeler l’application API de niveau intermédiaire, mais l’appel échoue car le serveur frontal est en cours d’exécution dans un autre domaine que le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="d6330-173">The JavaScript code tries to call the middle tier API app, but the call fails because the front end is running in a different domain than the back end.</span></span> <span data-ttu-id="d6330-174">La fenêtre de Console des outils de développement du navigateur affiche un message d’erreur cross-origin.</span><span class="sxs-lookup"><span data-stu-id="d6330-174">The browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Message d’erreur cross-origin](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-the-middle-tier-api-app"></a><span data-ttu-id="d6330-176">Configurer CORS pour l’application API de niveau intermédiaire</span><span class="sxs-lookup"><span data-stu-id="d6330-176">Configure CORS for the middle tier API app</span></span>
<span data-ttu-id="d6330-177">Dans cette section, vous configurez le paramètre CORS dans Azure pour l’application API ToDoListAPI API de niveau intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="d6330-177">In this section, you configure the CORS setting in Azure for the middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="d6330-178">Ce paramètre autorise l’application API de niveau intermédiaire à recevoir des appels JavaScript à partir de l’application web que vous avez créée pour le projet ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="d6330-178">This setting will allow the middle tier API app to receive JavaScript calls from the web app that you created for the ToDoListAngular project.</span></span>

1. <span data-ttu-id="d6330-179">Dans votre navigateur, accédez au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d6330-179">In a browser, go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d6330-180">Cliquez sur **App Services**, puis sur l’application API (niveau intermédiaire) ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="d6330-180">Click **App Services**, and then click the ToDoListAPI (middle tier) API app.</span></span>
   
    ![Sélectionnez l’application API dans le portail](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="d6330-182">Dans le panneau **Paramètres** qui s’ouvre à droite du panneau **application API**, recherchez la section **API**, puis cliquez sur **CORS**.</span><span class="sxs-lookup"><span data-stu-id="d6330-182">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Sélectionnez CORS dans le portail](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="d6330-184">Dans la zone de texte, saisissez l’URL de l’application web ToDoListAngular (frontale).</span><span class="sxs-lookup"><span data-stu-id="d6330-184">In the text box, enter the URL for the ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="d6330-185">Par exemple, si vous avez déployé le projet ToDoListAngular pour une application web nommée todolistangular0121, autorisez les appels en provenance de l’URL `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d6330-185">For example, if you deployed the ToDoListAngular project to a web app named todolistangular0121, allow calls from the URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="d6330-186">Vous pouvez également saisir un astérisque (*) pour indiquer que tous les domaines d’origine sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="d6330-186">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="d6330-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d6330-187">Click **Save**.</span></span>
   
   ![Cliquez sur Enregistrer.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="d6330-189">Lorsque vous cliquez sur **Enregistrer**, l’application API accepte les appels JavaScript depuis l’URL spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d6330-189">After you click **Save**, the API app will accept JavaScript calls from the specified URL.</span></span> <span data-ttu-id="d6330-190">Dans cette capture d’écran, l’application API ToDoListAPI0223 accepte les appels de client JavaScript à partir de l’application web ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="d6330-190">In this screen shot, the ToDoListAPI0223 API app will accept JavaScript client calls from the ToDoListAngular web app.</span></span>

### <a name="test-the-application-with-cors-enabled"></a><span data-ttu-id="d6330-191">Tester l’application en activant CORS</span><span class="sxs-lookup"><span data-stu-id="d6330-191">Test the application with CORS enabled</span></span>
* <span data-ttu-id="d6330-192">Dans un navigateur, accédez à l’URL HTTPS de l’application web.</span><span class="sxs-lookup"><span data-stu-id="d6330-192">Open a browser to the HTTPS URL of the web app.</span></span> 
  
    <span data-ttu-id="d6330-193">L’application vous permet cette fois d’afficher, ajouter, modifier et supprimer des éléments d’action.</span><span class="sxs-lookup"><span data-stu-id="d6330-193">This time the application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![Page de liste des tâches de l’exemple d’application](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="d6330-195">Service d’application CORS et API web CORS</span><span class="sxs-lookup"><span data-stu-id="d6330-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="d6330-196">Dans un projet d’API web, vous pouvez installer le package NuGet [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) pour spécifier dans le code les domaines à partir desquels votre API accepte des appels JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d6330-196">In a Web API project, you can install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package to specify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="d6330-197">La prise en charge de CORS dans l’API web est plus flexible que celle offerte par App Service.</span><span class="sxs-lookup"><span data-stu-id="d6330-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="d6330-198">Par exemple : dans le code, vous pouvez spécifier différentes origines acceptées pour différentes méthodes d’action, tandis que dans App Service, vous spécifiez un ensemble d’origines acceptées pour toutes les méthodes d’une application API.</span><span class="sxs-lookup"><span data-stu-id="d6330-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="d6330-199">N’essayez pas d’utiliser le protocole CORS de l’API web et le protocole CORS d’App Service dans une même application API.</span><span class="sxs-lookup"><span data-stu-id="d6330-199">Don't try to use both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="d6330-200">Le protocole CORS d’App Service est prioritaire (CORS dans l’API web n’aura aucun effet).</span><span class="sxs-lookup"><span data-stu-id="d6330-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="d6330-201">Par exemple, si vous activez un domaine d’origine dans App Service et activez tous les domaines d’origine dans votre code API Web, votre application API Azure accepte uniquement les appels en provenance du domaine spécifié dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d6330-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from the domain you specified in Azure.</span></span>
> 
> 

### <a name="how-to-enable-cors-in-web-api-code"></a><span data-ttu-id="d6330-202">Comment activer CORS dans le code de l’API web</span><span class="sxs-lookup"><span data-stu-id="d6330-202">How to enable CORS in Web API code</span></span>
<span data-ttu-id="d6330-203">Les étapes suivantes résument le processus d’activation de la prise en charge de CORS dans l’API web.</span><span class="sxs-lookup"><span data-stu-id="d6330-203">The following steps summarize the process for enabling Web API CORS support.</span></span> <span data-ttu-id="d6330-204">Pour plus d’informations, consultez le didacticiel [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)(Activation des demandes multi-origines dans l’API Web ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="d6330-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="d6330-205">Dans un projet d’API web, installez le package NuGet [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) .</span><span class="sxs-lookup"><span data-stu-id="d6330-205">In a Web API project, install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="d6330-206">Incluez une ligne de code `config.EnableCors()` dans la méthode **Register** de la classe **WebApiConfig**, comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d6330-206">Include a `config.EnableCors()` line of code in the **Register** method of the **WebApiConfig** class, as in the following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // The following line enables you to control CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. <span data-ttu-id="d6330-207">Dans votre contrôleur d’API web, ajoutez une instruction `using` pour l’espace de noms `System.Web.Http.Cors` et ajoutez l’attribut `EnableCors` à la classe de contrôleur ou aux méthodes d’action individuelles.</span><span class="sxs-lookup"><span data-stu-id="d6330-207">In your Web API controller, add a `using` statement for the `System.Web.Http.Cors` namespace, and add the `EnableCors` attribute to the controller class or to individual action methods.</span></span> <span data-ttu-id="d6330-208">Dans l’exemple qui suit, la prise en charge de CORS s’applique à l’ensemble du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="d6330-208">In the following example, CORS support applies to the entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="d6330-209">Utilisation de Gestion des API Azure avec les applications API.</span><span class="sxs-lookup"><span data-stu-id="d6330-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="d6330-210">Si vous utilisez Gestion des API Azure avec une application API, configurez CORS dans Gestion des API plutôt que dans l’application API.</span><span class="sxs-lookup"><span data-stu-id="d6330-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in the API app.</span></span> <span data-ttu-id="d6330-211">Pour plus d’informations, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6330-211">For more information, see the following resources:</span></span>

* [<span data-ttu-id="d6330-212">Vue d’ensemble de Gestion des API Azure (vidéo : CORS commence à 12:10)</span><span class="sxs-lookup"><span data-stu-id="d6330-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="d6330-213">Gestion des API dans les stratégies de domaine</span><span class="sxs-lookup"><span data-stu-id="d6330-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="d6330-214">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d6330-214">Troubleshooting</span></span>
<span data-ttu-id="d6330-215">Si vous rencontrez un problème tout au long de ce didacticiel, voici quelques suggestions :</span><span class="sxs-lookup"><span data-stu-id="d6330-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="d6330-216">Assurez-vous que vous disposez de la version la plus récente du [Kit de développement logiciel (SDK) Azure pour . NET pour Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="d6330-216">Make sure that you're using the latest version of the [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="d6330-217">Assurez-vous que vous avez correctement entré `https` dans le paramètre CORS et que vous utilisez `https` pour exécuter l’application web frontale.</span><span class="sxs-lookup"><span data-stu-id="d6330-217">Make sure that you entered `https` in the CORS setting, and make sure that you're using `https` to run the front-end web app.</span></span>
* <span data-ttu-id="d6330-218">Assurez-vous que vous avez entré le paramètre CORS dans l’application API de niveau intermédiaire, et non dans l’application web frontale.</span><span class="sxs-lookup"><span data-stu-id="d6330-218">Make sure that you entered the CORS setting in the middle tier API app, not in the front-end web app.</span></span>
* <span data-ttu-id="d6330-219">Si vous configurez CORS dans le code d’application et dans Azure App Service, notez que le paramètre CORS d’App Service remplacera tous les éléments contenus dans le code d’application.</span><span class="sxs-lookup"><span data-stu-id="d6330-219">If you're configuring CORS in both application code and Azure App Service, note that the App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="d6330-220">Pour en savoir plus sur les fonctionnalités de Visual Studio conçues pour faciliter la résolution des problèmes, consultez l’article [Dépanner une application web dans le Service d’application Microsoft Azure à l’aide de Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="d6330-220">To learn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6330-221">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6330-221">Next steps</span></span>
<span data-ttu-id="d6330-222">Dans cet article, vous avez vu deux façons d’activer la prise en charge de CORS afin que le code JavaScript client puisse appeler une API dans un autre domaine.</span><span class="sxs-lookup"><span data-stu-id="d6330-222">In this article, you saw how to enable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="d6330-223">Pour en savoir plus sur les applications API, lisez la [présentation de l’authentification dans App Service](../app-service/app-service-authentication-overview.md), puis accédez au didacticiel relatif à l’[authentification utilisateur pour les applications API](app-service-api-dotnet-user-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="d6330-223">To learn more about API apps, read the [introduction to authentication in App Service](../app-service/app-service-authentication-overview.md), and then go to the [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

