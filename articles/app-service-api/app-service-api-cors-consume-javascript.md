---
title: "aaaCORS prend en charge dans le Service d’applications | Documents Microsoft"
description: "Découvrez comment toouse CORS prennent en charge dans Azure Azure App Service."
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
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="ffec4-103">Consommer une application API à partir de JavaScript à l’aide de CORS</span><span class="sxs-lookup"><span data-stu-id="ffec4-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="ffec4-104">Service d’applications offre une prise en charge intégrée pour [partage de ressources entre origine (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), ce qui permet de JavaScript clients toomake inter-domaine appelle tooAPIs qui sont hébergés dans les applications API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="ffec4-105">Service d’applications vous permet de configurer les CORS accès tooyour API sans écrire de code dans votre API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="ffec4-106">Cet article contient deux sections :</span><span class="sxs-lookup"><span data-stu-id="ffec4-106">This article contains two sections:</span></span>

* <span data-ttu-id="ffec4-107">Hello [comment tooconfigure CORS](#corsconfig) section explique de façon générale tooconfigure CORS application API, application web ou des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="ffec4-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="ffec4-108">Elle s’applique également tooall infrastructures prises en charge par le Service d’application, y compris .NET, Node.js et Java.</span><span class="sxs-lookup"><span data-stu-id="ffec4-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="ffec4-109">En commençant par hello [poursuivre les didacticiels de prise en main de .NET hello](#tutorialstart) section, l’article de hello est un didacticiel qui montre les CORS prennent en charge en s’appuyant sur ce que vous avez fait [hello première API Apps lors de l’obtention didacticiel ](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ffec4-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="ffec4-110"><a id="corsconfig"></a>Comment tooconfigure CORS dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ffec4-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="ffec4-111">Vous pouvez configurer des règles CORS Bonjour portail Azure ou à l’aide de [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) outils.</span><span class="sxs-lookup"><span data-stu-id="ffec4-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="ffec4-112">Configurer les règles CORS Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="ffec4-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="ffec4-113">Dans un navigateur, accédez toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ffec4-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ffec4-114">Cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![Sélectionnez l’application API dans le portail](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="ffec4-116">Bonjour **paramètres** panneau qui s’affiche à droite de toohello Hello **application API** panneau, rechercher hello **API** section, puis cliquez sur **CORS**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Sélectionnez CORS dans le panneau Paramètres](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="ffec4-118">Dans la zone de texte hello entrez hello URL ou URL de tooallow JavaScript appelle toocome à partir de.</span><span class="sxs-lookup"><span data-stu-id="ffec4-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="ffec4-119">Par exemple, si vous avez déployé votre application web JavaScript application tooa nommée todolistangular, entrez « https://todolistangular.azurewebsites.net ».</span><span class="sxs-lookup"><span data-stu-id="ffec4-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="ffec4-120">En guise d’alternative, vous pouvez entrer une toospecify d’astérisque (*) que tous les domaines d’origine sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="ffec4-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="ffec4-121">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-121">Click **Save**.</span></span>
   
   ![Cliquez sur Enregistrer.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="ffec4-123">Après avoir cliqué sur **enregistrer**, application hello API acceptera JavaScript appelle à partir de hello spécifié l’URL.</span><span class="sxs-lookup"><span data-stu-id="ffec4-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="ffec4-124">Configurer CORS à l’aide des outils Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ffec4-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="ffec4-125">Vous pouvez également configurer des règles CORS pour une application API à l’aide de [modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) dans les outils de ligne de commande tels que [Azure PowerShell](/powershell/azureps-cmdlets-docs) et hello [CLI d’Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ffec4-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="ffec4-126">Pour obtenir un exemple d’un modèle de gestionnaire de ressources Azure qui définit la propriété CORS hello, ouvrez hello [fichier azuredeploy.json dans le référentiel de hello pour exemple d’application de ce didacticiel](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ffec4-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="ffec4-127">Recherchez section hello du modèle hello qui ressemble à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ffec4-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="ffec4-128"><a id="tutorialstart"></a>Continuer le didacticiel de prise en main de .NET hello</span><span class="sxs-lookup"><span data-stu-id="ffec4-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="ffec4-129">Si vous suivez hello Node.js ou Java-mise en route série pour les applications d’API, vous avez terminé hello prise en main série.</span><span class="sxs-lookup"><span data-stu-id="ffec4-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="ffec4-130">Ignorer toohello [étapes](#next-steps) section suggestions toofind pour se familiariser davantage les applications API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="ffec4-131">Hello reste de cet article est la suite de hello série de prise en main de .NET et part du principe que vous terminé [premier didacticiel de hello](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ffec4-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="ffec4-132">Déployer hello ToDoListAngular projet tooa nouvelle application web</span><span class="sxs-lookup"><span data-stu-id="ffec4-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="ffec4-133">Dans [premier didacticiel de hello](app-service-api-dotnet-get-started.md), vous avez créé une application API de niveau intermédiaire et une application API de couche données.</span><span class="sxs-lookup"><span data-stu-id="ffec4-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="ffec4-134">Dans ce didacticiel vous créez une application web de l’application à page unique (SPA) à cette application de couche intermédiaire API appels hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="ffec4-135">Vous pouvez hello SPA toowork tooenable CORS sur la couche intermédiaire de hello application API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="ffec4-136">Bonjour [exemple d’application ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), projet de ToDoListAngular hello est un client AngularJS simple qui appelle hello intermédiaire ToDoListAPI Web API projet.</span><span class="sxs-lookup"><span data-stu-id="ffec4-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="ffec4-137">Hello du code JavaScript dans hello *app/scripts/todoListSvc.js* fichier appelle hello API à l’aide du fournisseur de AngularJS HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="ffec4-138">Créer une application web pour le projet de ToDoListAngular hello</span><span class="sxs-lookup"><span data-stu-id="ffec4-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="ffec4-139">Hello procédure toocreate une application web du Service d’applications et de déployer un projet tooit est toowhat similaires, vous avez vu pour [créer et déployer une application API dans hello premier didacticiel de cette série](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="ffec4-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="ffec4-140">Hello seule différence est ce type d’application hello est **Web App** au lieu de **application API**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="ffec4-141">Pour les captures d’écran de boîtes de dialogue hello, consultez</span><span class="sxs-lookup"><span data-stu-id="ffec4-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="ffec4-142">Dans **l’Explorateur de solutions**, cliquez sur le projet de ToDoListAngular hello, puis cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="ffec4-143">Bonjour **profil** onglet Hello **publier le site Web** Assistant, cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="ffec4-144">Bonjour **du Service d’applications** boîte de dialogue, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="ffec4-145">Bonjour **hébergement** onglet Hello **créer un Service application** boîte de dialogue, entrez un **nom de l’application Web** qui est unique dans hello *azurewebsites.net* domaine.</span><span class="sxs-lookup"><span data-stu-id="ffec4-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="ffec4-146">Choisissez hello Azure **abonnement** vous souhaitez toowork avec.</span><span class="sxs-lookup"><span data-stu-id="ffec4-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="ffec4-147">Bonjour **groupe de ressources** liste déroulante, sélectionnez hello même groupe de ressources vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="ffec4-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="ffec4-148">Bonjour **Plan App Service** liste déroulante, sélectionnez hello même plan que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="ffec4-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="ffec4-149">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-149">Click **Create**.</span></span>
   
    <span data-ttu-id="ffec4-150">Visual Studio crée l’application web hello, crée un profil de publication pour celle-ci et affiche hello **connexion** étape Hello **publier le site Web** Assistant.</span><span class="sxs-lookup"><span data-stu-id="ffec4-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="ffec4-151">Attendez encore avant de cliquer sur **Publier** .</span><span class="sxs-lookup"><span data-stu-id="ffec4-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="ffec4-152">Bonjour suivant la section, vous configurez hello application toocall hello intermédiaire API application web qui s’exécute dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="ffec4-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="ffec4-153">Définir l’URL de la couche intermédiaire hello dans les paramètres de l’application web</span><span class="sxs-lookup"><span data-stu-id="ffec4-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="ffec4-154">Accédez toohello [portail Azure](https://portal.azure.com/), puis accédez toohello **Web App** panneau pour l’application hello web que vous avez créé le projet de toohost hello TodoListAngular (frontal).</span><span class="sxs-lookup"><span data-stu-id="ffec4-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="ffec4-155">Cliquez sur **Paramètres > Paramètres de l'application**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="ffec4-156">Bonjour **paramètres de l’application** section, ajoutez hello clé et la valeur :</span><span class="sxs-lookup"><span data-stu-id="ffec4-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="ffec4-157">Clé</span><span class="sxs-lookup"><span data-stu-id="ffec4-157">Key</span></span> | <span data-ttu-id="ffec4-158">Valeur</span><span class="sxs-lookup"><span data-stu-id="ffec4-158">Value</span></span> | <span data-ttu-id="ffec4-159">Exemple</span><span class="sxs-lookup"><span data-stu-id="ffec4-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="ffec4-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="ffec4-160">toDoListAPIURL</span></span> |<span data-ttu-id="ffec4-161">https://{nom de votre application API de niveau intermédiaire}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ffec4-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="ffec4-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ffec4-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="ffec4-163">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-163">Click **Save**.</span></span>
   
    <span data-ttu-id="ffec4-164">Lorsque le code de hello s’exécute dans Azure, cette valeur remplace les URL localhost hello Bonjour *Web.config* fichier.</span><span class="sxs-lookup"><span data-stu-id="ffec4-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="ffec4-165">code Hello qui obtient la valeur du paramètre hello se trouve dans *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="ffec4-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="ffec4-166">Hello code dans *todoListSvc.js* utilise le paramètre de hello :</span><span class="sxs-lookup"><span data-stu-id="ffec4-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="ffec4-167">Déployer hello ToDoListAngular web projet toohello nouvelle application web</span><span class="sxs-lookup"><span data-stu-id="ffec4-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="ffec4-168">Dans Visual Studio, Bonjour **connexion** étape Hello **publier le site Web** Assistant, cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="ffec4-169">Visual Studio déploie hello ToDoListAngular projet toohello nouvelle application web et ouvre une URL toohello de navigateur de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="ffec4-170">Tester l’application hello sans CORS activé</span><span class="sxs-lookup"><span data-stu-id="ffec4-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="ffec4-171">Dans les outils de développement de votre navigateur, ouvrez la fenêtre de Console hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="ffec4-172">Dans la fenêtre du navigateur hello qui affiche hello AngularJS UI, cliquez sur hello **tooDo liste** lien.</span><span class="sxs-lookup"><span data-stu-id="ffec4-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="ffec4-173">Hello du code JavaScript essaie toocall hello intermédiaire application API, mais échec de l’appel de hello car frontal hello est en cours d’exécution dans un domaine différent de celui hello précédent fin.</span><span class="sxs-lookup"><span data-stu-id="ffec4-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="ffec4-174">fenêtre de Console des outils de développement du navigateur Hello affiche un message d’erreur de cross-origin.</span><span class="sxs-lookup"><span data-stu-id="ffec4-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Message d’erreur cross-origin](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="ffec4-176">Configurer les CORS pour le niveau intermédiaire de hello application API</span><span class="sxs-lookup"><span data-stu-id="ffec4-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="ffec4-177">Dans cette section, vous configurer paramètre CORS de hello dans Azure pour la couche intermédiaire de hello application ToDoListAPI API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="ffec4-178">Ce paramètre autorise hello intermédiaire application tooreceive JavaScript appels d’API de l’application hello web que vous avez créé pour le projet de ToDoListAngular hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="ffec4-179">Dans un navigateur, accédez à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ffec4-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ffec4-180">Cliquez sur **des Services d’application**, puis cliquez sur application hello ToDoListAPI (intermédiaire) API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![Sélectionnez l’application API dans le portail](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="ffec4-182">Bonjour **paramètres** panneau qui s’affiche à droite de toohello Hello **application API** panneau, rechercher hello **API** section, puis cliquez sur **CORS**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Sélectionnez CORS dans le portail](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="ffec4-184">Dans la zone de texte hello, entrez les URL hello pour l’application web hello ToDoListAngular (frontal).</span><span class="sxs-lookup"><span data-stu-id="ffec4-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="ffec4-185">Par exemple, si vous avez déployé hello ToDoListAngular projet tooa l’application web nommée todolistangular0121, autorisent les appels de hello URL `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="ffec4-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="ffec4-186">En guise d’alternative, vous pouvez entrer une toospecify d’astérisque (*) que tous les domaines d’origine sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="ffec4-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="ffec4-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ffec4-187">Click **Save**.</span></span>
   
   ![Cliquez sur Enregistrer.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="ffec4-189">Après avoir cliqué sur **enregistrer**, application hello API acceptera JavaScript appelle à partir de hello spécifié l’URL.</span><span class="sxs-lookup"><span data-stu-id="ffec4-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="ffec4-190">Dans cette capture d’écran, hello ToDoListAPI0223 API application accepte les appels du client JavaScript de l’application web de ToDoListAngular hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="ffec4-191">Tester l’application hello avec CORS activé</span><span class="sxs-lookup"><span data-stu-id="ffec4-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="ffec4-192">Ouvrez un navigateur de toohello URL HTTPS de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="ffec4-193">Cette application hello de temps vous permet d’afficher, ajouter, modifier et supprimer des éléments d’action.</span><span class="sxs-lookup"><span data-stu-id="ffec4-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![page de liste tooDo de l’exemple d’application](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="ffec4-195">Service d’application CORS et API web CORS</span><span class="sxs-lookup"><span data-stu-id="ffec4-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="ffec4-196">Dans un projet d’API Web, vous pouvez installer hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify de package NuGet dans les domaines qui accepte votre API JavaScript appelle à partir de code.</span><span class="sxs-lookup"><span data-stu-id="ffec4-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="ffec4-197">La prise en charge de CORS dans l’API web est plus flexible que celle offerte par App Service.</span><span class="sxs-lookup"><span data-stu-id="ffec4-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="ffec4-198">Par exemple : dans le code, vous pouvez spécifier différentes origines acceptées pour différentes méthodes d’action, tandis que dans App Service, vous spécifiez un ensemble d’origines acceptées pour toutes les méthodes d’une application API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="ffec4-199">N’essayez pas toouse Web API CORS et CORS de Service d’application dans une application API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="ffec4-200">Le protocole CORS d’App Service est prioritaire (CORS dans l’API web n’aura aucun effet).</span><span class="sxs-lookup"><span data-stu-id="ffec4-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="ffec4-201">Par exemple, si vous activez un domaine d’origine dans le Service d’applications et activez tous les domaines d’origine dans votre code de l’API Web, votre application API Azure n’accepte que les appels à partir du domaine de hello spécifié dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ffec4-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="ffec4-202">Comment tooenable CORS dans le code de l’API Web</span><span class="sxs-lookup"><span data-stu-id="ffec4-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="ffec4-203">Hello suit résument les processus hello pour activer la prise en charge Web API CORS.</span><span class="sxs-lookup"><span data-stu-id="ffec4-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="ffec4-204">Pour plus d’informations, consultez le didacticiel [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)(Activation des demandes multi-origines dans l’API Web ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="ffec4-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="ffec4-205">Dans un projet d’API Web, installez hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) package NuGet.</span><span class="sxs-lookup"><span data-stu-id="ffec4-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="ffec4-206">Inclure un `config.EnableCors()` ligne de code hello **inscrire** méthode Hello **WebApiConfig** (classe), comme dans l’exemple suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
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
3. <span data-ttu-id="ffec4-207">Dans votre contrôleur d’API Web, ajoutez un `using` instruction pour hello `System.Web.Http.Cors` espace de noms et ajoutez hello `EnableCors` toohello contrôleur tooindividual classe ou méthodes d’action d’attribut.</span><span class="sxs-lookup"><span data-stu-id="ffec4-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="ffec4-208">Dans l’exemple suivant de hello, prise en charge CORS s’applique contrôleur entière de toohello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="ffec4-209">Utilisation de Gestion des API Azure avec les applications API.</span><span class="sxs-lookup"><span data-stu-id="ffec4-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="ffec4-210">Si vous utilisez la gestion des API Azure avec une application API, vous pouvez configurer CORS dans Gestion des API au lieu de dans l’application d’API hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="ffec4-211">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="ffec4-211">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="ffec4-212">Vue d’ensemble de Gestion des API Azure (vidéo : CORS commence à 12:10)</span><span class="sxs-lookup"><span data-stu-id="ffec4-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="ffec4-213">Gestion des API dans les stratégies de domaine</span><span class="sxs-lookup"><span data-stu-id="ffec4-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="ffec4-214">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="ffec4-214">Troubleshooting</span></span>
<span data-ttu-id="ffec4-215">Si vous rencontrez un problème tout au long de ce didacticiel, voici quelques suggestions :</span><span class="sxs-lookup"><span data-stu-id="ffec4-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="ffec4-216">Assurez-vous que vous utilisez la version la plus récente de hello hello [Azure SDK pour .NET de Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="ffec4-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="ffec4-217">Assurez-vous que vous avez entré `https` dans hello du paramètre de CORS et vous assurer que vous utilisez `https` toorun hello frontal web app.</span><span class="sxs-lookup"><span data-stu-id="ffec4-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="ffec4-218">Assurez-vous que vous avez entré de paramètre de CORS hello dans l’application API de niveau intermédiaire hello, pas dans l’application web frontale de hello.</span><span class="sxs-lookup"><span data-stu-id="ffec4-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="ffec4-219">Si vous configurez des règles CORS dans le code d’application et le Service d’applications Azure, notez que paramètre d’application Service CORS hello remplace tout ce que vous effectuez dans le code d’application.</span><span class="sxs-lookup"><span data-stu-id="ffec4-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="ffec4-220">toolearn savoir plus sur les fonctionnalités de Visual Studio qui simplifient la résolution des problèmes, consultez [des applications de résolution des problèmes du Service d’applications Azure dans Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ffec4-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffec4-221">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ffec4-221">Next steps</span></span>
<span data-ttu-id="ffec4-222">Dans cet article, vous avez vu comment tooenable App Service CORS prennent en charge afin que le code JavaScript client peut appeler une API dans un domaine différent.</span><span class="sxs-lookup"><span data-stu-id="ffec4-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="ffec4-223">toolearn plus d’informations sur les applications API, lire hello [tooauthentication de présentation dans le Service d’applications](../app-service/app-service-authentication-overview.md), puis passez toohello [l’authentification utilisateur pour les applications API](app-service-api-dotnet-user-principal-auth.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ffec4-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

