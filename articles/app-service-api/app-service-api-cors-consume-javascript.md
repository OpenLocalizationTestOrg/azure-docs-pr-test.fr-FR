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
# <a name="consume-an-api-app-from-javascript-using-cors"></a>Consommer une application API à partir de JavaScript à l’aide de CORS
Service d’applications offre une prise en charge intégrée pour [partage de ressources entre origine (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), ce qui permet de JavaScript clients toomake inter-domaine appelle tooAPIs qui sont hébergés dans les applications API. Service d’applications vous permet de configurer les CORS accès tooyour API sans écrire de code dans votre API.

Cet article contient deux sections :

* Hello [comment tooconfigure CORS](#corsconfig) section explique de façon générale tooconfigure CORS application API, application web ou des applications mobiles. Elle s’applique également tooall infrastructures prises en charge par le Service d’application, y compris .NET, Node.js et Java. 
* En commençant par hello [poursuivre les didacticiels de prise en main de .NET hello](#tutorialstart) section, l’article de hello est un didacticiel qui montre les CORS prennent en charge en s’appuyant sur ce que vous avez fait [hello première API Apps lors de l’obtention didacticiel ](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>Comment tooconfigure CORS dans Azure App Service
Vous pouvez configurer des règles CORS Bonjour portail Azure ou à l’aide de [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) outils.

#### <a name="configure-cors-in-hello-azure-portal"></a>Configurer les règles CORS Bonjour portail Azure
1. Dans un navigateur, accédez toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application API.
   
    ![Sélectionnez l’application API dans le portail](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Bonjour **paramètres** panneau qui s’affiche à droite de toohello Hello **application API** panneau, rechercher hello **API** section, puis cliquez sur **CORS**.
   
   ![Sélectionnez CORS dans le panneau Paramètres](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Dans la zone de texte hello entrez hello URL ou URL de tooallow JavaScript appelle toocome à partir de.

    Par exemple, si vous avez déployé votre application web JavaScript application tooa nommée todolistangular, entrez « https://todolistangular.azurewebsites.net ». En guise d’alternative, vous pouvez entrer une toospecify d’astérisque (*) que tous les domaines d’origine sont acceptés.


1. Cliquez sur **Enregistrer**.
   
   ![Cliquez sur Enregistrer.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Après avoir cliqué sur **enregistrer**, application hello API acceptera JavaScript appelle à partir de hello spécifié l’URL.

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>Configurer CORS à l’aide des outils Azure Resource Manager
Vous pouvez également configurer des règles CORS pour une application API à l’aide de [modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) dans les outils de ligne de commande tels que [Azure PowerShell](/powershell/azureps-cmdlets-docs) et hello [CLI d’Azure](../cli-install-nodejs.md). 

Pour obtenir un exemple d’un modèle de gestionnaire de ressources Azure qui définit la propriété CORS hello, ouvrez hello [fichier azuredeploy.json dans le référentiel de hello pour exemple d’application de ce didacticiel](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Recherchez section hello du modèle hello qui ressemble à hello l’exemple suivant :

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>Continuer le didacticiel de prise en main de .NET hello
Si vous suivez hello Node.js ou Java-mise en route série pour les applications d’API, vous avez terminé hello prise en main série. Ignorer toohello [étapes](#next-steps) section suggestions toofind pour se familiariser davantage les applications API.

Hello reste de cet article est la suite de hello série de prise en main de .NET et part du principe que vous terminé [premier didacticiel de hello](app-service-api-dotnet-get-started.md).

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>Déployer hello ToDoListAngular projet tooa nouvelle application web
Dans [premier didacticiel de hello](app-service-api-dotnet-get-started.md), vous avez créé une application API de niveau intermédiaire et une application API de couche données. Dans ce didacticiel vous créez une application web de l’application à page unique (SPA) à cette application de couche intermédiaire API appels hello. Vous pouvez hello SPA toowork tooenable CORS sur la couche intermédiaire de hello application API. 

Bonjour [exemple d’application ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), projet de ToDoListAngular hello est un client AngularJS simple qui appelle hello intermédiaire ToDoListAPI Web API projet. Hello du code JavaScript dans hello *app/scripts/todoListSvc.js* fichier appelle hello API à l’aide du fournisseur de AngularJS HTTP hello. 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>Créer une application web pour le projet de ToDoListAngular hello
Hello procédure toocreate une application web du Service d’applications et de déployer un projet tooit est toowhat similaires, vous avez vu pour [créer et déployer une application API dans hello premier didacticiel de cette série](app-service-api-dotnet-get-started.md#createapiapp). Hello seule différence est ce type d’application hello est **Web App** au lieu de **application API**.  Pour les captures d’écran de boîtes de dialogue hello, consultez 

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de ToDoListAngular hello, puis cliquez sur **publier**.
2. Bonjour **profil** onglet Hello **publier le site Web** Assistant, cliquez sur **Microsoft Azure App Service**.
3. Bonjour **du Service d’applications** boîte de dialogue, cliquez sur **nouveau**.
4. Bonjour **hébergement** onglet Hello **créer un Service application** boîte de dialogue, entrez un **nom de l’application Web** qui est unique dans hello *azurewebsites.net* domaine. 
5. Choisissez hello Azure **abonnement** vous souhaitez toowork avec.
6. Bonjour **groupe de ressources** liste déroulante, sélectionnez hello même groupe de ressources vous avez créé précédemment.
7. Bonjour **Plan App Service** liste déroulante, sélectionnez hello même plan que vous avez créé précédemment. 
8. Cliquez sur **Créer**.
   
    Visual Studio crée l’application web hello, crée un profil de publication pour celle-ci et affiche hello **connexion** étape Hello **publier le site Web** Assistant.
   
    Attendez encore avant de cliquer sur **Publier** . Bonjour suivant la section, vous configurez hello application toocall hello intermédiaire API application web qui s’exécute dans le Service d’applications. 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>Définir l’URL de la couche intermédiaire hello dans les paramètres de l’application web
1. Accédez toohello [portail Azure](https://portal.azure.com/), puis accédez toohello **Web App** panneau pour l’application hello web que vous avez créé le projet de toohost hello TodoListAngular (frontal).
2. Cliquez sur **Paramètres > Paramètres de l'application**.
3. Bonjour **paramètres de l’application** section, ajoutez hello clé et la valeur :
   
   | Clé | Valeur | Exemple |
   | --- | --- | --- |
   | toDoListAPIURL |https://{nom de votre application API de niveau intermédiaire}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. Cliquez sur **Enregistrer**.
   
    Lorsque le code de hello s’exécute dans Azure, cette valeur remplace les URL localhost hello Bonjour *Web.config* fichier. 
   
    code Hello qui obtient la valeur du paramètre hello se trouve dans *index.cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    Hello code dans *todoListSvc.js* utilise le paramètre de hello :
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>Déployer hello ToDoListAngular web projet toohello nouvelle application web
* Dans Visual Studio, Bonjour **connexion** étape Hello **publier le site Web** Assistant, cliquez sur **publier**.
  
   Visual Studio déploie hello ToDoListAngular projet toohello nouvelle application web et ouvre une URL toohello de navigateur de l’application web hello. 

### <a name="test-hello-application-without-cors-enabled"></a>Tester l’application hello sans CORS activé
1. Dans les outils de développement de votre navigateur, ouvrez la fenêtre de Console hello.
2. Dans la fenêtre du navigateur hello qui affiche hello AngularJS UI, cliquez sur hello **tooDo liste** lien.
   
    Hello du code JavaScript essaie toocall hello intermédiaire application API, mais échec de l’appel de hello car frontal hello est en cours d’exécution dans un domaine différent de celui hello précédent fin. fenêtre de Console des outils de développement du navigateur Hello affiche un message d’erreur de cross-origin.
   
    ![Message d’erreur cross-origin](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>Configurer les CORS pour le niveau intermédiaire de hello application API
Dans cette section, vous configurer paramètre CORS de hello dans Azure pour la couche intermédiaire de hello application ToDoListAPI API. Ce paramètre autorise hello intermédiaire application tooreceive JavaScript appels d’API de l’application hello web que vous avez créé pour le projet de ToDoListAngular hello.

1. Dans un navigateur, accédez à toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **des Services d’application**, puis cliquez sur application hello ToDoListAPI (intermédiaire) API.
   
    ![Sélectionnez l’application API dans le portail](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Bonjour **paramètres** panneau qui s’affiche à droite de toohello Hello **application API** panneau, rechercher hello **API** section, puis cliquez sur **CORS**.
   
   ![Sélectionnez CORS dans le portail](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Dans la zone de texte hello, entrez les URL hello pour l’application web hello ToDoListAngular (frontal). Par exemple, si vous avez déployé hello ToDoListAngular projet tooa l’application web nommée todolistangular0121, autorisent les appels de hello URL `https://todolistangular0121.azurewebsites.net`.
   
   En guise d’alternative, vous pouvez entrer une toospecify d’astérisque (*) que tous les domaines d’origine sont acceptés.
5. Cliquez sur **Enregistrer**.
   
   ![Cliquez sur Enregistrer.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Après avoir cliqué sur **enregistrer**, application hello API acceptera JavaScript appelle à partir de hello spécifié l’URL. Dans cette capture d’écran, hello ToDoListAPI0223 API application accepte les appels du client JavaScript de l’application web de ToDoListAngular hello.

### <a name="test-hello-application-with-cors-enabled"></a>Tester l’application hello avec CORS activé
* Ouvrez un navigateur de toohello URL HTTPS de l’application web hello. 
  
    Cette application hello de temps vous permet d’afficher, ajouter, modifier et supprimer des éléments d’action. 
  
    ![page de liste tooDo de l’exemple d’application](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>Service d’application CORS et API web CORS
Dans un projet d’API Web, vous pouvez installer hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify de package NuGet dans les domaines qui accepte votre API JavaScript appelle à partir de code.

La prise en charge de CORS dans l’API web est plus flexible que celle offerte par App Service. Par exemple : dans le code, vous pouvez spécifier différentes origines acceptées pour différentes méthodes d’action, tandis que dans App Service, vous spécifiez un ensemble d’origines acceptées pour toutes les méthodes d’une application API.

> [!NOTE]
> N’essayez pas toouse Web API CORS et CORS de Service d’application dans une application API. Le protocole CORS d’App Service est prioritaire (CORS dans l’API web n’aura aucun effet). Par exemple, si vous activez un domaine d’origine dans le Service d’applications et activez tous les domaines d’origine dans votre code de l’API Web, votre application API Azure n’accepte que les appels à partir du domaine de hello spécifié dans Azure.
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>Comment tooenable CORS dans le code de l’API Web
Hello suit résument les processus hello pour activer la prise en charge Web API CORS. Pour plus d’informations, consultez le didacticiel [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)(Activation des demandes multi-origines dans l’API Web ASP.NET).

1. Dans un projet d’API Web, installez hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) package NuGet.
2. Inclure un `config.EnableCors()` ligne de code hello **inscrire** méthode Hello **WebApiConfig** (classe), comme dans l’exemple suivant de hello. 
   
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
3. Dans votre contrôleur d’API Web, ajoutez un `using` instruction pour hello `System.Web.Http.Cors` espace de noms et ajoutez hello `EnableCors` toohello contrôleur tooindividual classe ou méthodes d’action d’attribut. Dans l’exemple suivant de hello, prise en charge CORS s’applique contrôleur entière de toohello.
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>Utilisation de Gestion des API Azure avec les applications API.
Si vous utilisez la gestion des API Azure avec une application API, vous pouvez configurer CORS dans Gestion des API au lieu de dans l’application d’API hello. Pour plus d’informations, consultez hello suivant des ressources :

* [Vue d’ensemble de Gestion des API Azure (vidéo : CORS commence à 12:10)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [Gestion des API dans les stratégies de domaine](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous rencontrez un problème tout au long de ce didacticiel, voici quelques suggestions :

* Assurez-vous que vous utilisez la version la plus récente de hello hello [Azure SDK pour .NET de Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).
* Assurez-vous que vous avez entré `https` dans hello du paramètre de CORS et vous assurer que vous utilisez `https` toorun hello frontal web app.
* Assurez-vous que vous avez entré de paramètre de CORS hello dans l’application API de niveau intermédiaire hello, pas dans l’application web frontale de hello.
* Si vous configurez des règles CORS dans le code d’application et le Service d’applications Azure, notez que paramètre d’application Service CORS hello remplace tout ce que vous effectuez dans le code d’application. 

toolearn savoir plus sur les fonctionnalités de Visual Studio qui simplifient la résolution des problèmes, consultez [des applications de résolution des problèmes du Service d’applications Azure dans Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez vu comment tooenable App Service CORS prennent en charge afin que le code JavaScript client peut appeler une API dans un domaine différent. toolearn plus d’informations sur les applications API, lire hello [tooauthentication de présentation dans le Service d’applications](../app-service/app-service-authentication-overview.md), puis passez toohello [l’authentification utilisateur pour les applications API](app-service-api-dotnet-user-principal-auth.md) didacticiel.

