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
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>Prise en main d’API Apps, d’ASP.NET et de Swagger dans Azure App Service
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

Il est tout d’abord hello dans une série de didacticiels qui montrent comment toouse les fonctionnalités d’Azure App Service qui sont utiles pour le développement et l’hébergement d’une API RESTful.  Ce didacticiel décrit la prise en charge des métadonnées des API au format Swagger.

Vous apprendrez ce qui suit :

* Comment toocreate et déployer [applications API](app-service-api-apps-why-best-platform.md) dans Azure App Service à l’aide des outils intégrés à Visual Studio 2015.
* Comment empaqueter de découverte tooautomate API à l’aide de hello Swashbuckle NuGet toodynamically génèrent des métadonnées de l’API de Swagger.
* Comment tooautomatically de métadonnées Swagger des API toouse générer du code client pour une application API.

## <a name="sample-application-overview"></a>Vue d’ensemble de l’exemple d’application
Dans ce didacticiel, vous travaillez avec un exemple d’application de liste des tâches simples. application Hello a frontal une seule page application (SPA), une couche intermédiaire d’API Web ASP.NET et une couche de données d’API Web ASP.NET.

![Exemple de schéma d’application API Apps](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

Voici une capture d’écran de hello [AngularJS](https://angularjs.org/) front-end.

![Applications API exemple application toodo de liste](./media/app-service-api-dotnet-get-started/todospa.png)

Hello solution Visual Studio comprend trois projets :

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -frontal hello : un SPA AngularJS qui appelle intermédiaire hello.
* **ToDoListAPI** -intermédiaire hello : un projet d’API Web ASP.NET qui appelle couche de données hello tooperform les opérations CRUD sur les éléments d’action.
* **ToDoListDataAPI** -niveau de données hello : un projet d’API Web ASP.NET qui exécute des opérations CRUD sur les éléments d’action.

architecture à trois niveaux de Hello est un des nombreux architectures que vous pouvez implémenter à l’aide des applications API et êtes utilisé ici uniquement à des fins de démonstration. code Hello dans chaque niveau est aussi simple que les fonctionnalités d’applications API toodemonstrate possible ; par exemple, la couche de données hello utilise mémoire du serveur plutôt que dans une base de données comme mécanisme de persistance.

Une fois ce didacticiel, vous aurez deux projets d’API Web hello haut et en cours d’exécution dans le cloud hello dans les applications de l’API de Service d’application.

Hello étape suivante du didacticiel dans la série de hello déploie cloud toohello de hello SPA front-end.

## <a name="prerequisites"></a>Composants requis
* ASP.NET Web API - instructions de didacticiel de hello supposent que vous avez une connaissance élémentaire de la façon toowork avec ASP.NET [API Web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) dans Visual Studio.
* Compte Azure : vous pouvez [ouvrir un compte Azure gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) ou [activer les avantages de l’abonnement à Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
  
    Si vous souhaitez tooget démarré avec le Service d’application Azure avant de vous inscrivez pour un compte Azure, accédez trop[Service d’applications essayez](https://azure.microsoft.com/try/app-service/). De là, vous pouvez créer immédiatement une première application temporaire dans App Service. **Aucune carte de crédit** ni aucun engagement ne sont nécessaires.
* Visual Studio 2015 avec hello [Azure SDK pour .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK installe Visual Studio 2015 automatiquement si vous n’est pas déjà installé.
  
  * Dans Visual Studio, cliquez sur Aide -> À propos de Microsoft Visual Studio et vérifiez que « Azure App Service Tools v2.9.1 » ou ultérieur est installé.
    
    ![Version d’Azure App Service Tools](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > Selon le nombre de dépendances du Kit de développement logiciel hello vous disposez déjà sur votre ordinateur, hello lors de l’installation du SDK peut prendre beaucoup de temps, à partir de plusieurs minutes tooa demi-heure ou plus.
    > 
    > 

## <a name="download-hello-sample-application"></a>Télécharger l’exemple d’application hello
1. Télécharger hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) référentiel.
   
    Vous pouvez cliquer sur hello **ZIP de téléchargement** bouton ou un clone référentiel hello sur votre ordinateur local.
2. Ouvrez la solution de ToDoList hello dans Visual Studio 2015 ou 2013.
   
   1. Vous devez tootrust chaque solution.
         ![Avertissement de sécurité](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. Générez les packages NuGet hello hello solution (CTRL + MAJ + B) toorestore.
   
    Si vous souhaitez une application hello toosee opération avant de le déployer, vous pouvez l’exécuter localement. Assurez-vous que ToDoListDataAPI est votre projet de démarrage et l’exécution hello. Vous devriez toosee un HTTP 403 erreur dans votre navigateur.

## <a name="use-swagger-api-metadata-and-ui"></a>Utiliser l’interface utilisateur et les métadonnées d’API Swagger
La prise en charge des métadonnées d’API [Swagger](http://swagger.io/) 2.0 est intégrée aux applications API App Service. Chaque application API peut spécifier un point de terminaison d’URL qui retourne des métadonnées pour hello API au format JSON de Swagger. Hello retournée à partir de ce point de terminaison de métadonnées peuvent être utilisé de code client toogenerate.

Un projet d’API Web ASP.NET peut générer dynamiquement des métadonnées Swagger à l’aide de hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) package NuGet. Hello package Swashbuckle NuGet est déjà installé dans les projets ToDoListDataAPI et ToDoListAPI hello que vous avez téléchargé.

Dans cette section du didacticiel de hello, examiner des métadonnées Swagger 2.0 de hello généré, puis essayer un test de l’interface utilisateur qui est basée sur les métadonnées de Swagger hello.

1. Définissez hello ToDoListDataAPI projet (**pas** projet ToDoListAPI de hello) en tant que projet de démarrage hello.
   
    ![Définir ToDoDataAPI comme projet de démarrage](./media/app-service-api-dotnet-get-started/startupproject.png)
2. Appuyez sur F5 ou cliquez sur **Déboguer > Démarrer le débogage** projet de hello toorun en mode débogage.
   
    navigateur de Hello s’ouvre et affiche la page d’erreur HTTP 403 hello.
3. Dans la barre d’adresse de votre navigateur, ajoutez `swagger/docs/v1` fin toohello de ligne de hello, puis appuyez sur retour. (hello URL est `http://localhost:45914/swagger/docs/v1`.)
   
    Il s’agit d’URL par défaut de hello utilisé par les métadonnées de JSON de 2.0 Swagger Swashbuckle tooreturn pour hello API.
   
    Si vous utilisez Internet Explorer, hello navigateur vous invite à toodownload une *v1.json* fichier.
   
    ![Télécharger les métadonnées JSON dans Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    Si vous utilisez Edge, Firefox ou Chrome, navigateur de hello affiche hello JSON dans une fenêtre de navigateur hello. Différents navigateurs gèrent différemment les JSON, et la fenêtre du navigateur ne semblent pas exactement comme exemple de hello.
   
    ![Métadonnées JSON dans Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    Hello suivant montre hello première section de métadonnées Swagger de hello pour hello API, avec définition hello pour hello Get (méthode). Ces métadonnées sont le hello lecteurs Swagger interface utilisateur que vous utilisez dans hello comme suit, et que vous l’utilisez dans une section ultérieure de tooautomatically de didacticiel hello générer le code client.
   
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
4. Fermez le navigateur de hello et arrêter le débogage de Visual Studio.
5. Bonjour ToDoListDataAPI projet **l’Explorateur de solutions**, ouvrez hello *App_Start\SwaggerConfig.cs* le fichier, puis de défilement vers le bas tooline 174 et ne commentez pas hello suivant de code.
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    Hello *SwaggerConfig.cs* fichier est créé lorsque vous installez le package de Swashbuckle hello dans un projet. fichier de Hello fournit un certain nombre de façons tooconfigure Swashbuckle.
   
    code Hello que vous avez supprimées hello Active Swagger interface utilisateur que vous utilisez dans hello suivant les étapes. Lorsque vous créez un projet d’API Web à l’aide du modèle de projet application hello API, ce code est mis en commentaire par défaut en tant que mesure de sécurité.
6. Réexécutez hello projet.
7. Dans la barre d’adresse de votre navigateur, ajoutez `swagger` fin toohello de ligne de hello, puis appuyez sur retour. (hello URL est `http://localhost:45914/swagger`.)
8. Lorsque la page de l’interface utilisateur de Swagger hello s’affiche, cliquez sur **ToDoList** méthodes de hello toosee disponibles.
   
    ![Méthodes disponibles dans l’interface utilisateur Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. Commencez par cliquer sur hello **obtenir** bouton dans la liste de hello.
10. Bonjour **paramètres** section, entrez un astérisque en tant que valeur hello Hello `owner` paramètre, puis cliquez sur **essayez-le**.
    
    Lorsque vous ajoutez l’authentification dans des didacticiels ultérieurs, intermédiaire hello fournira la couche de données hello toohello de l’ID réel de l’utilisateur. Pour l’instant, toutes les tâches ont astérisque en tant que leur ID de propriétaire, tandis que l’application hello s’exécute sans activer l’authentification.
    
    ![Essayer l’interface utilisateur Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    Hello Swagger de l’interface utilisateur appelle la méthode Get de la liste des tâches de hello et affiche le code de réponse hello et résultats JSON.
    
    ![Essayer l’interface utilisateur Swagger - Résultats](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. Cliquez sur **Post**, puis cliquez sur la zone hello sous **schéma de modèle**.
    
    En cliquant sur hello modèle schéma prefills hello zone d’entrée où vous pouvez spécifier la valeur du paramètre hello pour hello méthode Post. (Si cela ne fonctionne pas dans Internet Explorer, utilisez un autre navigateur ou entrez la valeur du paramètre hello manuellement à l’étape suivante de hello).  
    
    ![Essayer l’interface utilisateur Swagger - Publication](./media/app-service-api-dotnet-get-started/post.png)
12. Hello modification JSON Bonjour `todo` paramètre d’entrée afin qu’il ressemble à hello l’exemple suivant, ou les remplacer par votre propre texte de description :
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. Cliquez sur **Try it out**.
    
    Hello ToDoList API renvoie un code de réponse HTTP 204 qui indique la réussite.
14. Commencez par cliquer sur hello **obtenir** bouton, puis cliquez dans cette section de la page de hello hello **essayez-le** bouton.
    
    Hello réponse de la méthode Get inclut désormais un nouvel élément de toodo hello.
15. Facultatif : Essayez également hello Put, Delete et obtenir par les méthodes de code.
16. Fermez le navigateur de hello et arrêter le débogage de Visual Studio.

Swashbuckle fonctionne avec n’importe quel projet d’API Web ASP.NET. Si vous souhaitez tooadd Swagger métadonnées génération tooan un projet existant, installez simplement le package de Swashbuckle hello.

> [!NOTE]
> Les métadonnées Swagger incluent un ID unique pour chaque opération d’API. Par défaut, Swashbuckle peut générer des ID d’opération Swagger en double pour vos méthodes de contrôleur d’API web. Cela se produit si les méthodes HTTP du contrôleur sont surchargées, par exemple `Get()` et `Get(id)`. Pour plus d’informations sur la façon dont les surcharges de toohandle, consultez [définitions généré Swashbuckle de personnaliser les API](app-service-api-dotnet-swashbuckle-customize.md). Si vous créez un projet d’API Web dans Visual Studio à l’aide du modèle d’application API Azure hello, code qui génère l’ID d’opération est automatiquement ajouté toohello *SwaggerConfig.cs* fichier.  
> 
> 

## <a id="createapiapp"></a>Créer une application API dans Azure et de déployer le code tooit
Dans cette section, vous utilisez les outils Azure qui sont intégrés à Visual Studio de hello **publier le site Web** application toocreate une nouvelle API d’Assistant dans Azure. Puis vous déployez hello ToDoListDataAPI projet toohello nouvelle application API et appelez des API de hello en hello Swagger de l’interface utilisateur en cours d’exécution.

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de ToDoListDataAPI hello, puis cliquez sur **publier**.
   
    ![Cliquez sur Publier dans Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. Bonjour **profil** étape Hello **publier le site Web** Assistant, cliquez sur **Microsoft Azure App Service**.
   
   ![Cliquez sur Azure App Service dans Publier le site web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. Connectez-vous à tooyour compte Azure si vous n’avez pas déjà fait, ou actualiser vos informations d’identification s’ils sont arrivés à expiration.
4. Dans les hello boîte de dialogue du Service d’applications, choisissez hello Azure **abonnement** vous souhaitez toouse, puis cliquez sur **nouveau**.
   
    ![Cliquez sur Nouveau dans la boîte de dialogue App Service](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    Hello **hébergement** onglet Hello **créer un Service application** boîte de dialogue s’affiche.
   
    Étant donné que vous déployez un projet d’API Web qui a Swashbuckle installé, Visual Studio suppose que vous souhaitez toocreate une application API. Cela est indiqué par hello **Name de l’application API** titre et par hello fait ce hello **modifier le Type de** liste déroulante est définie trop**application API**.
   
    ![Type d’application dans la boîte de dialogue App Service](./media/app-service-api-dotnet-get-started/apptype.png)
5. Entrez un **Name de l’application API** qui est unique dans hello *azurewebsites.net* domaine. Vous pouvez accepter le nom par défaut hello proposé par Visual Studio.
   
    Si vous entrez un nom d’une autre personne a déjà utilisé, vous consultez un toohello de point d’exclamation rouge à droite.
   
    Hello URL de l’application hello API sera `{API app name}.azurewebsites.net`.
6. Bonjour **groupe de ressources** déroulante, cliquez sur **nouveau**, puis entrez « ToDoListGroup » ou un autre nom si vous préférez.
   
    Un groupe de ressources est une collection de ressources Azure telles que des applications API, des bases de données, des machines virtuelles, etc.    Pour ce didacticiel, il est meilleure toocreate un groupe de ressources car qui la rendent facile toodelete en une seule étape que toutes hello des ressources Azure que vous créez pour le didacticiel de hello.
   
    Cette zone vous permet de sélectionner un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) ou d’en créer un avec un nom différent de ceux qui existent déjà dans votre abonnement.
7. Cliquez sur hello **nouveau** toohello suivant du bouton **du Plan App Service** liste déroulante.
   
    capture d’écran Hello montre exemples de valeurs pour **Name de l’application API**, **abonnement**, et **groupe de ressources** --vos valeurs seront différentes.
   
    ![Boîte de dialogue Créer App Service](./media/app-service-api-dotnet-get-started/createas.png)
   
    Bonjour suit vous créer un plan App Service pour le nouveau groupe de ressources hello. Un plan App Service spécifie les ressources de calcul hello qui s’exécute votre application API. Par exemple, si vous choisissez le niveau gratuit de hello, votre application API s’exécute sur les ordinateurs virtuels partagés, alors que pour certains niveaux payants, il s’exécute sur des machines virtuelles dédiées. Pour plus d’informations sur les plans App Service, consultez [Présentation des plans App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
8. Bonjour **configurer un Plan App Service** boîte de dialogue, entrez « ToDoListPlan » ou un autre nom si vous préférez.
9. Bonjour **emplacement** liste déroulante, sélectionnez l’emplacement de hello tooyou le plus proche.
   
    Ce paramètre indique le centre de données Azure dans lequel votre application sera exécutée. Choisissez un emplacement fermer tooyou toominimize [latence](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).
10. Bonjour **taille** déroulante, cliquez sur **libre**.
    
    Pour ce didacticiel, hello libre tarification fournissent des performances suffisantes.
11. Bonjour **configurer un Plan App Service** boîte de dialogue, cliquez sur **OK**.
    
    ![Cliquez sur OK dans Configurer le plan App Service](./media/app-service-api-dotnet-get-started/configasp.png)
12. Bonjour **créer un Service application** boîte de dialogue, cliquez sur **créer**.
    
    ![Cliquez sur Créer dans la boîte de dialogue App Service](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Visual Studio crée l’application d’API hello et un profil de publication qui a tous les paramètres de hello requis pour application hello API. Il s’ouvre et affiche hello **publier le site Web** Assistant que vous allez utiliser project de hello toodeploy.
    
    Hello **publier le site Web** Assistant s’ouvre sur hello **connexion** onglet (voir ci-dessous).
    
    Sur hello **connexion** sous l’onglet hello **Server** et **nom du Site** paramètres point tooyour API app. Hello **nom d’utilisateur** et **mot de passe** sont les informations d’identification de déploiement Azure crée pour vous. Après le déploiement, Visual Studio ouvre un navigateur toohello **URL de Destination** (qui est le seul but de hello pour **URL de Destination**).  
13. Cliquez sur **Suivant**.
    
    ![Cliquez sur Suivant dans l’onglet Connexion de l’assistant Publier le site Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    onglet suivant de Hello est hello **paramètres** onglet (voir ci-dessous). Vous pouvez modifier ici une version debug de hello build configuration onglet toodeploy [débogage distant](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug). Hello onglet offre également plusieurs **Options de publication du fichier**:
    
    * Supprimer les fichiers supplémentaires de la destination
    * Précompiler durant la publication
    * Exclure les fichiers du dossier App_Data hello
    
    Pour ce didacticiel, vous n’avez besoin d’aucune de ces options. Pour obtenir des explications détaillées sur leur action, consultez la rubrique [Déploiement d’un projet web à l’aide de la publication en un clic dans Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).
14. Cliquez sur **Suivant**.
    
    ![Cliquez sur Suivant dans l’onglet Paramètres de l’assistant Publier le site Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    L’élément suivant est hello **aperçu** onglet (voir ci-dessous), qui vous donne un toosee opportunité quels fichiers vont toobe copié à partir de votre application toohello API de projet. Lorsque vous déployez une application de tooan API de projet que vous avez déjà déployé de tooearlier, seuls les fichiers modifiés sont copiés. Si vous souhaitez toosee une liste de ce que sera copié, vous pouvez cliquer sur hello **démarrer la version préliminaire** bouton.
15. Cliquez sur **Publier**.
    
    ![Cliquez sur Publier dans l’onglet Aperçu de l’assistant Publier le site Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    Visual Studio déploie hello ToDoListDataAPI projet toohello nouvelle application API. Hello **sortie** ouvre une fenêtre de réussir le déploiement, et une page « a été créée » s’affiche dans une URL de toohello navigateur fenêtre ouverte de l’application hello API.
    
    ![Réussite du déploiement dans la fenêtre de sortie](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Page Application API créée avec succès](./media/app-service-api-dotnet-get-started/appcreated.png)
16. Ajouter des URL de toohello « swagger » dans la barre d’adresses du navigateur hello et appuyez sur ENTRÉE. (hello URL est `http://{apiappname}.azurewebsites.net/swagger`.)
    
    navigateur de Hello affiche hello même Swagger l’interface utilisateur que vous avez vu précédemment, mais maintenant elle est en cours d’exécution dans le cloud de hello. Essayer hello méthode Get, et vous constatez que vous êtes des éléments de tâches 2 toohello différé par défaut. Hello apportées précédemment ont été enregistrées dans la mémoire sur l’ordinateur local de hello.
17. Ouvrez hello [portail Azure](https://portal.azure.com/).
    
    Hello portail Azure est une interface web pour la gestion des ressources Azure telles que les applications API.
18. Cliquez sur **Plus de services > App Services**.
    
    ![Parcourir App Services](./media/app-service-api-dotnet-get-started/browseas.png)
19. Bonjour **des Services d’application** panneau, recherchez et cliquez sur votre nouvelle application API. (Dans hello portail Azure, les fenêtres qui s’ouvrent toohello droite sont appelés *panneaux*.)
    
    ![Panneau App Services](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    Deux panneaux s’ouvrent. Un panneau a une vue d’ensemble de l’application d’API hello, et a une longue liste de paramètres que vous pouvez afficher et modifier.
20. Bonjour **paramètres** panneau, rechercher hello **API** et cliquez sur **définition d’API**.
    
    ![Définition de l’API dans le panneau Paramètres](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    Hello **définition d’API** panneau vous permet de spécifier des URL de hello qui retourne des métadonnées Swagger 2.0 au format JSON. Lorsque Visual Studio crée l’application hello API, il définit hello API définition URL toohello par défaut pour Swashbuckle métadonnées générées que vous avez vu précédemment, qui est l’application hello API de base d’URL plu `/swagger/docs/v1`.
    
    ![URL de définition de l’API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    Lorsque vous sélectionnez un code de client toogenerate l’application API pour celle-ci, Visual Studio récupère les métadonnées de hello à partir de cette URL.

## <a id="codegen"></a>Générer le code client pour le niveau de données hello
Un des avantages de hello de l’intégration de Swagger dans les applications API Azure est la génération de code automatique. Classes de client généré vous code toowrite plus simple qui appelle une application API.

Hello ToDoListAPI projet déjà hello généré le code client, mais Bonjour comme suit, vous allez supprimer et régénérer toosee toodo hello comment la génération de code.

1. Dans Visual Studio **l’Explorateur de solutions**, Bonjour ToDoListAPI projet d’équipe, supprimez hello *ToDoListDataAPI* dossier. **Attention : Supprimer uniquement le dossier hello, pas le projet de ToDoListDataAPI hello.**
   
    ![Suppression du code client généré](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    Ce dossier a été créé à l’aide du processus de génération de code hello que vous êtes sur toogo via.
2. Projet de ToDoListAPI hello d’avec le bouton droit, puis cliquez sur **Ajouter > Client de l’API REST**.
   
    ![Ajouter un client API REST dans Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. Bonjour **Client de l’API REST ajouter** boîte de dialogue, cliquez sur **URL Swagger**, puis cliquez sur **sélectionner les ressources Azure**.
   
    ![Sélectionner une ressource Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. Bonjour **du Service d’applications** boîte de dialogue, développez le groupe de ressources hello vous utilisez pour ce didacticiel, sélectionnez votre application API, puis cliquez **OK**.
   
    ![Sélectionnez une application API pour la génération de code](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    Notez que lorsque vous retournez toohello **Client de l’API REST ajouter** boîte de dialogue, zone de texte hello est rempli avec la définition de l’API de hello valeur de l’URL que vous avez vu plus haut dans le portail de hello.
   
    ![URL de définition de l’API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > Métadonnées de tooget d’autre moyen pour la génération de code sont l’URL de hello tooenter directement au lieu de passer par la boîte de dialogue Parcourir hello. Ou si vous souhaitez que le code client toogenerate avant de déployer tooAzure, vous pouvez exécuter le projet d’API Web hello localement, accédez toohello URL qui fournit le fichier Swagger de JSON de hello, enregistrer le fichier de hello, et utiliser hello **sélectionner un fichier de métadonnées Swagger existant**option.
   > 
   > 
5. Bonjour **Client de l’API REST ajouter** boîte de dialogue, cliquez sur **OK**.
   
    Visual Studio crée un dossier nommé d’après l’application hello API et génère des classes de client.
   
    ![Fichiers de code pour le client généré](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. Dans le projet de ToDoListAPI hello, ouvrez *Controllers\ToDoListController.cs* code hello de toosee à la ligne 40 qui appelle des API de hello à l’aide du client de hello généré.
   
    Hello suivant extrait de code montre comment le code de hello instancie objet de client hello et appels hello méthode Get.
   
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
   
    paramètre de constructeur Hello Obtient l’URL de point de terminaison hello de hello `toDoListDataAPIURL` paramètre d’application. Dans le fichier Web.config hello, cette valeur est toohello ensemble local IIS Express URL de hello API projet afin que vous puissiez exécuter des application hello localement. Si vous omettez le paramètre de constructeur hello, point de terminaison par défaut hello est hello URL que vous avez généré le code hello.
7. Votre classe de client est généré avec un nom différent selon le nom de votre application API ; modifier le code hello dans *Controllers\ToDoListController.cs* afin que hello nom de type correspond à ce qui a été généré dans votre projet. Par exemple, si vous avez nommé votre application API ToDoListDataAPI071316, vous modifieriez ce code :
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis :

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>Créer une couche API application toohost hello intermédiaire
Plus tôt vous [hello données couche API application créée et déployée code tooit](#createapiapp).  Maintenant vous suivez hello même procédure pour l’application de couche intermédiaire API hello.

1. Dans **l’Explorateur de solutions**, avec le bouton hello intermédiaire ToDoListAPI (pas hello couche données ToDoListDataAPI) du projet, puis cliquez sur **publier**.
   
    ![Cliquez sur Publier dans Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. Bonjour **profil** onglet Hello **publier le site Web** Assistant, cliquez sur **Microsoft Azure App Service**.
3. Bonjour **du Service d’applications** boîte de dialogue, cliquez sur **nouveau**.
4. Bonjour **hébergement** onglet Hello **créer un Service application** boîte de dialogue zone, accepter la valeur par défaut hello **Name de l’application API** ou entrer un nom unique dans hello  *azurewebsites.NET* domaine.
5. Choisissez hello Azure **abonnement** vous avez utilisé.
6. Bonjour **groupe de ressources** liste déroulante, choisissez hello même groupe de ressources vous avez créé précédemment.
7. Bonjour **Plan App Service** liste déroulante, choisissez hello même plan que vous avez créé précédemment. Il prend par défaut la valeur de toothat.
8. Cliquez sur **Créer**.
   
    Visual Studio crée l’application hello API, crée un profil de publication pour celle-ci et affiche hello **connexion** étape Hello **publier le site Web** Assistant.
9. Bonjour **connexion** étape Hello **publier le site Web** Assistant, cliquez sur **publier**.
   
   Visual Studio déploie hello ToDoListAPI projet toohello nouvelle application API et ouvre le navigateur toohello URL d’application d’API hello. page de Hello « créée avec succès » s’affiche.

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>Configurer la couche de données hello intermédiaire toocall hello
Si vous avez appelé application API de niveau intermédiaire hello maintenant, il serait essayer la couche de données hello toocall à l’aide des URL localhost hello qui se trouve toujours dans le fichier Web.config de hello. Dans cette section, vous entrez des URL de l’application API niveau données hello dans un paramètre d’environnement dans l’application API de niveau intermédiaire hello. Quand hello code dans l’application API de niveau intermédiaire hello récupère du paramètre d’URL hello données couche, paramètre d’environnement hello remplace ce qui est dans le fichier Web.config de hello.

1. Accédez toohello [portail Azure](https://portal.azure.com/), puis accédez toohello **application API** panneau pour l’application hello API que vous avez créé le projet de toohost hello TodoListAPI (intermédiaire).
2. Dans hello l’application API **paramètres** panneau, cliquez sur **paramètres de l’Application**.
3. Dans hello l’application API **paramètres de l’Application** panneau, faites défiler vers le bas toohello **paramètres de l’application** section et ajouter des éléments suivants de hello clé et la valeur. Hello aura l’URL de hello de hello première API application que vous avez publié dans ce didacticiel.
   
   | **Clé** | toDoListDataAPIURL |
   | --- | --- |
   | **Valeur** |https://{nom de votre application API de la couche Données}.azurewebsites.net |
   | **Exemple** |https://todolistdataapi.azurewebsites.net |
4. Cliquez sur **Enregistrer**.
   
    ![Cliquez sur Enregistrer pour les paramètres de l’application](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    Lorsque le code de hello s’exécute dans Azure, cette valeur remplace maintenant hello localhost URL qui se trouve dans le fichier Web.config de hello.

## <a name="test"></a>Test
1. Dans une fenêtre de navigateur, accédez URL toohello de couche intermédiaire nouvelle application API que vous venez de créer pour ToDoListAPI hello. Vous pouvez y accéder en cliquant sur les URL hello dans le panneau principal de l’application hello API dans le portail de hello.
2. Ajouter des URL de toohello « swagger » dans la barre d’adresses du navigateur hello et appuyez sur ENTRÉE. (hello URL est `http://{apiappname}.azurewebsites.net/swagger`.)
   
    navigateur affiche Hello hello même Swagger l’interface utilisateur que vous avez vu précédemment pour ToDoListDataAPI, mais désormais `owner` n’est pas un champ obligatoire pour l’opération d’obtention de hello, car l’application de couche intermédiaire API hello envoie cette application de valeur toohello données couche API pour vous. (Lorsque vous hello didacticiels de l’authentification, intermédiaire hello enverra des ID de l’utilisateur réel pour hello `owner` paramètre ; pour maintenant il est le codage en dur un astérisque.)
3. Essayer hello méthode Get et hello toovalidate autres méthodes qui hello application API de niveau intermédiaire est correctement appel hello données couche application API.
   
    ![Méthode Get de l’interface utilisateur Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous rencontrez un problème tout au long de ce didacticiel, voici quelques suggestions de dépannage :

* Assurez-vous que vous utilisez la version la plus récente de hello hello [Azure SDK pour .NET](http://go.microsoft.com/fwlink/?linkid=518003).
* Deux des noms de projet hello sont similaires (ToDoListAPI, ToDoListDataAPI). Si les éléments ne s’affichent pas comme décrit dans les instructions hello lorsque vous travaillez avec un projet, assurez-vous que vous avez ouvert le projet approprié de hello.
* Si vous êtes sur un réseau d’entreprise et que vous essayez de toodeploy tooAzure du Service d’applications via un pare-feu, assurez-vous que les ports 443 et 8172 sont ouverts pour Web Deploy. Si vous ne pouvez pas ouvrir ces ports, vous pouvez utiliser d’autres méthodes de déploiement.  Consultez [déployer votre tooAzure d’application du Service d’applications](../app-service-web/web-sites-deploy.md).
* Erreurs « noms d’itinéraires doivent être uniques » : vous pouvez obtenir ces si vous accidentellement déployez hello projet incorrect tooan API app et puis déployez ultérieurement un tooit correct de hello. toocorrect, application toohello API de redéploiement hello projet approprié et sur hello **paramètres** onglet Hello **publier le site Web** Assistant, sélectionnez **supprimer les fichiers supplémentaires à la destination**.

Après avoir configuré votre application API ASP.NET en cours d’exécution dans Azure App Service, vous souhaiterez peut-être toolearn plus d’informations sur les fonctionnalités de Visual Studio qui simplifient la résolution des problèmes. Pour plus d’informations sur la journalisation, le débogage à distance, etc. consultez la section [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md) (Résolution des problèmes des applications web Azure App Service dans Visual Studio).

## <a name="next-steps"></a>Étapes suivantes
Vous avez vu comment toodeploy API Web projets tooAPI applications existantes, générer le code client pour les applications d’API et consommer des applications API à partir de clients .NET. Hello étape suivante du didacticiel de cette série montre comment trop[utiliser CORS tooconsume API des applications à partir de clients JavaScript](app-service-api-cors-consume-javascript.md).

Pour plus d’informations sur la génération de code client, consultez hello [Azure/AutoRest](https://github.com/azure/autorest) référentiel sur GitHub.com. Pour l’aide sur les problèmes à l’aide du client de hello généré, ouvrez un [problème dans le référentiel de AutoRest hello](https://github.com/azure/autorest/issues).

Si vous souhaitez toocreate nouveaux projets d’application API à partir de zéro, utilisez hello **application API Azure** modèle.

![Modèle d’application API dans Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

Hello **application API Azure** modèle de projet est l’équivalent toochoosing hello **vide** ASP.NET 4.5.2 modèle, en cliquant sur la prise en charge des API Web tooadd case à cocher hello et l’installation de package NuGet de Swashbuckle de hello. En outre, le modèle de hello ajoute Swashbuckle configuration code conçu tooprevent hello créer des doublons Swagger opération ID. Une fois que vous avez créé un projet d’application API, vous pouvez le déployer hello d’application tooan API même façon que vous l’avez vu dans ce didacticiel.

