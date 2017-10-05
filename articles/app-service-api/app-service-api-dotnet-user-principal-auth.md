---
title: Authentification utilisateur pour API Apps dans Azure App Service | Microsoft Docs
description: "Découvrez comment protéger une application API dans Azure App Service en accordant l’accès uniquement aux utilisateurs authentifiés."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: a5b713f3a60b3886d813438496d704f464d914e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Authentification utilisateur pour API Apps dans Azure App Service
## <a name="overview"></a>Vue d'ensemble
Cet article montre comment protéger une application API Azure, afin que seuls les utilisateurs authentifiés puissent l’appeler. Cet article suppose que vous avez lu la [Vue d’ensemble de l’authentification Azure App Service](../app-service/app-service-authentication-overview.md).

Vous apprendrez ce qui suit :

* La configuration d’un fournisseur d’authentification, avec des détails destinés à Azure Active Directory (Azure AD).
* L’utilisation d’une application API protégée à l’aide d’ [ADAL (Active Directory Authentication Library) pour JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

Cet article contient deux sections :

* La section [Configuration de l’authentification utilisateur dans Azure App Service](#authconfig) explique comment configurer l’authentification utilisateur de n’importe quelle application API. Elle s’applique également à toutes les infrastructures prises en charge par App Service, notamment .NET, Node.js et Java.
* Cet article, qui commence par la section [Suite des didacticiels API Apps .NET](#tutorialstart) , vous guide dans la configuration d’un exemple d’application avec un backend .NET et un frontal AngularJS afin d’utiliser Azure Active Directory pour l’authentification utilisateur. 

## <a id="authconfig"></a> Configuration de l’authentification utilisateur dans Azure App Service
Cette section fournit des instructions générales s’appliquant à n’importe quelle application API. Pour connaître les étapes spécifiques à l’exemple d’application .NET To Do List, passez à la section [Suite des didacticiels de mise en route de .NET](#tutorialstart).

1. Dans le [portail Azure](https://portal.azure.com/), accédez au panneau **Paramètres** de l’application API que vous souhaitez protéger, puis recherchez la section **Fonctionnalités** et cliquez sur **Authentification/Autorisation**.
   
    ![Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Dans le panneau **Authentification/Autorisation**, cliquez sur **Activé**.
3. Sélectionnez une des options de la liste déroulante **Action à exécuter quand une demande n’est pas authentifiée** .
   
   * Si vous souhaitez que seuls les appels authentifiés accèdent à votre application API, choisissez parmi les options **Se connecter avec...** . Cette option vous permet de protéger l’application API sans écrire de code s’exécutant dans cette dernière.
   * Si vous souhaitez que tous les appels accèdent à votre application API, choisissez **Autoriser la demande (aucune action)**. Vous pouvez utiliser cette option pour diriger les appelants non authentifiés vers une sélection de fournisseurs d’authentification. Avec cette option, vous devez écrire du code pour gérer l’autorisation.
     
     Pour plus d’informations, consultez la page [Authentification et autorisation pour API Apps dans Azure App Service](app-service-api-authentication.md#multiple-protection-options).
4. Sélectionnez un ou plusieurs **fournisseurs d’authentification**.
   
    L’image montre les options qui exigent que tous les appelants soient authentifiés par Azure AD.
   
    ![Panneau Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Lorsque vous choisissez un fournisseur d’authentification, le portail affiche un panneau de configuration correspondant à ce fournisseur. 
   
    Pour obtenir des instructions détaillées sur la procédure de configuration des panneaux de configuration du fournisseur d’authentification, consultez la page [Configurer votre application App Service pour utiliser la connexion Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (Le lien mène à un article sur Azure AD, mais l’article lui-même contient des onglets associés à des articles destinés aux autres fournisseurs d’authentification).
5. Une fois que vous en avez terminé avec le panneau de configuration du fournisseur d’authentification, cliquez sur **OK**.
6. Dans le panneau **Authentification/Autorisation**, cliquez sur **Enregistrer**.

App Service authentifie alors tous les appels API avant qu’ils atteignent l’application API. Ces services d’authentification fonctionnent de la même manière pour tous les langages pris en charge par App Service, notamment .NET, Node.js et Java. 

Pour exécuter des appels d’API authentifiés, l’appelant inclut le jeton de porteur OAuth 2.0 du fournisseur d’authentification dans l’en-tête d’autorisation des demandes HTTP. Le jeton peut être acquis à l’aide du kit de développement logiciel du fournisseur d’authentification.

## <a id="tutorialstart"></a> Suite des didacticiels API Apps .NET
Si vous suivez les didacticiels Node.js ou Java pour les applications API, passez à l’article suivant, intitulé [Authentification de principal du service pour API Apps](app-service-api-dotnet-service-principal-auth.md). 

Si vous suivez la série de didacticiels .NET pour les applications API et si vous avez déjà déployé l’exemple d’application comme indiqué dans les [premier](app-service-api-dotnet-get-started.md) et [deuxième](app-service-api-cors-consume-javascript.md) didacticiels, passez à la section [Configurer l’authentification dans App Service et Azure AD](#azureauth).

Si vous souhaitez suivre ce didacticiel sans suivre le premier et le deuxième didacticiels, effectuez les étapes suivantes, qui expliquent comment commencer en utilisant un processus automatisé pour déployer l’exemple d’application.

> [!NOTE]
> Les étapes suivantes vous mènent au même point de départ que si vous aviez suivi les deux premiers didacticiels, à une exception près : Visual Studio ne sait pas vers quelle application web ou application API chaque projet est déployé. Cela signifie que ce didacticiel ne vous présentera pas d’instructions précises pour déployer vers les bonnes cibles. Si vous ne vous sentez pas suffisamment à l’aise pour effectuer seul les étapes de déploiement, il est préférable de suivre la série de didacticiels à partir du [premier didacticiel](app-service-api-dotnet-get-started.md) plutôt que de commencer par ce processus de déploiement automatisé.
> 
> 

1. Assurez-vous de disposer de tous les composants requis répertoriés dans le [premier didacticiel](app-service-api-dotnet-get-started.md). Outre la configuration requise indiquée, ces didacticiels d’authentification supposent que vous avez déjà travaillé avec des applications web et des applications API App Service dans Visual Studio et le portail Azure.
2. Cliquez sur le bouton **Déployer dans Azure** dans le [fichier readme du référentiel de l’exemple To Do List](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) pour déployer les applications API et l’application web. Prenez note du groupe de ressources Azure qui est créé, car vous pourrez l’utiliser ultérieurement pour rechercher les noms de l’application API et de l’application web.
3. Téléchargez ou clonez le [référentiel de l’exemple To Do List](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) pour obtenir le code que vous utiliserez localement dans Visual Studio.

## <a id="azureauth"></a> Configurer l’authentification dans App Service et Azure AD
L’application s’exécute désormais dans Azure App Service sans exiger que les utilisateurs soient authentifiés. Dans cette section, vous allez ajouter l’authentification en effectuant les tâches suivantes :

* Configurez App Service pour qu’elle exige une authentification Azure Active Directory (Azure AD) pour appeler l’application API de niveau intermédiaire.
* Créez une application Azure AD.
* Configurez l’application Azure AD pour envoyer le jeton de porteur après la connexion au frontal AngularJS. 

Si vous rencontrez des problèmes en suivant les instructions du didacticiel, consultez la section [Résolution de problèmes](#troubleshooting) à la fin du didacticiel. 

### <a name="configure-authentication-for-the-middle-tier-api-app"></a>Configurer l’authentification pour l’application API de niveau intermédiaire
1. Dans le [portail Azure](https://portal.azure.com/), accédez au panneau **Paramètres** de l’application API que vous avez créée pour le projet ToDoListAPI, recherchez la section **Fonctionnalités** et cliquez sur **Authentification/Autorisation**.
   
    ![Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Dans le panneau **Authentification/Autorisation**, cliquez sur **Activé**.
3. Dans la liste déroulante **Action à effectuer lorsque la demande n’est pas authentifiée**, sélectionnez **Se connecter avec Azure Active Directory**.
   
    Cette option permet de s’assurer qu’aucune demande non authentifiée n’atteindra l’application API. 
4. Sous **Fournisseurs d’authentification**, cliquez sur **Azure Active Directory**.
   
    ![Panneau Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Dans le panneau **Paramètres Azure Active Directory**, cliquez sur **Express**
   
    ![Option Express du panneau Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Avec l’option **Express**, App Service permet à Azure AD de créer automatiquement une application Azure AD dans le [client](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Vous n’avez pas à créer un client, car chaque compte Azure en possède un.
6. Sous **Mode d’administration**, cliquez sur **Créer une application AD** si cette option n’est pas déjà sélectionnée, notez la valeur qui se trouve dans la zone de texte **Créer une application**. Vous allez rechercher cette application AAD dans le portail Azure Classic plus tard.
   
    ![Paramètres Azure AD du portail Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure crée automatiquement une application Azure AD avec le nom indiqué dans votre client Azure AD. Par défaut, l’application Azure AD porte le même nom que celui de l’application API. Vous pouvez, si vous le souhaitez, choisir un autre nom.
7. Cliquez sur **OK**.
8. Dans le panneau **Authentification/Autorisation**, cliquez sur **Enregistrer**.
   
    ![Cliquez sur Enregistrer.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Maintenant, seuls les utilisateurs de votre client Azure AD peuvent appeler l’application API.

### <a name="optional-test-the-api-app"></a>Facultatif : tester l’application API
1. Dans un navigateur, accédez à l’URL de l’application API : dans le panneau **Application API** du portail Azure, cliquez sur le lien situé sous **URL**.  
   
    Vous êtes redirigé vers un écran de connexion, car les demandes non authentifiées ne sont pas autorisées à atteindre l’application API.
   
    Si votre navigateur accède à la page « créé avec succès », le navigateur peut déjà être connecté. Dans ce cas, ouvrez une fenêtre InPrivate ou Incognito et accédez à l’URL de l’application API.
2. Connectez-vous avec les informations d’identification d’un utilisateur de votre client Azure AD.
   
    Une fois que vous êtes connecté, la page signalant que la création a réussi s’affiche dans le navigateur.
3. Fermez le navigateur.

### <a name="configure-the-azure-ad-application"></a>Configuration de l’application Azure Active Directory
Lorsque vous avez configuré l’authentification Azure AD, App Service a créé pour vous une application Azure AD. Par défaut, la nouvelle application Azure AD a été configurée pour fournir le jeton de porteur à l’URL de l’application API. Dans cette section, vous allez configurer l’application Azure AD pour fournir le jeton de porteur au frontal AngularJS plutôt que directement à l’application de niveau intermédiaire de l’application API. Le frontal AngularJS envoie le jeton à l’application API lorsqu’il appelle l’application API.

> [!NOTE]
> Pour conserver un processus qui soit le plus simple possible, ce didacticiel utilise une seule application Azure AD pour le serveur frontal et l’application API de niveau intermédiaire. Une autre option consiste à utiliser deux applications Azure AD. Dans ce cas, vous devez autoriser l’application Azure AD du serveur frontal à appeler l’application Azure AD de niveau intermédiaire. Cette approche à plusieurs applications permet d’obtenir un contrôle plus granulaire sur les autorisations à chaque niveau.
> 
> 

1. Dans le [portail Azure Classic](https://manage.windowsazure.com/), accédez à **Azure Active Directory**.
   
   Vous devez utiliser le portail classique, car certains paramètres Azure Active Directory auxquels vous devez accéder ne sont pas encore disponibles dans le portail Azure actuel.
2. Sous l’onglet **Annuaire** , cliquez sur votre client AAD.
   
   ![Azure AD dans le portail classique](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Cliquez sur **Applications > Applications que ma société possède**, puis cliquez sur la coche.
   
   Vous devrez peut-être aussi actualiser la page pour afficher la nouvelle application.
4. Dans la liste des applications, cliquez sur le nom de celle qu’Azure a créée pour vous quand vous avez activé l’authentification pour votre application API.
   
   ![Onglet Applications Azure AD](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Cliquez sur **Configurer**.
   
   ![Onglet Configurer Azure AD](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Définissez **URL de connexion** sur l’URL de votre application web AngularJS, sans barre oblique à la fin.
   
   Par exemple : https://todolistangular.azurewebsites.net
   
   ![URL de connexion](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Définissez **URL de réponse** sur l’URL de votre application web, sans barre oblique à la fin.
   
   Par exemple : https://todolistsangular.azurewebsites.net
8. Cliquez sur **Enregistrer**.
   
   ![URL de réponse](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. En bas de la page, cliquez sur **Gérer le manifeste > Télécharger le manifeste**.
   
   ![Télécharger le manifeste](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Téléchargez le fichier à un emplacement où vous pouvez le modifier.
11. Dans le fichier manifeste téléchargé, recherchez la propriété `oauth2AllowImplicitFlow`. Modifiez la valeur de cette propriété en remplaçant `false` par `true`, puis enregistrez le fichier.
    
    Ce paramètre est obligatoire pour l’accès depuis une application de page JavaScript unique. Il permet au jeton de porteur Oauth 2.0 d’être renvoyé dans le fragment d’URL.
12. Cliquez sur **Gérer le manifeste > Télécharger le manifeste**, puis chargez le fichier mis à jour à l’étape précédente.
    
    ![Télécharger le manifeste sur le serveur](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Copiez la valeur **ID client** et enregistrez-la à un emplacement où vous pourrez la récupérer par la suite.

## <a name="configure-the-todolistangular-project-to-use-authentication"></a>Configurer le projet ToDoListAngular pour utiliser l’authentification
Dans cette section, vous allez modifier le serveur frontal AngularJS afin qu’il utilise ADAL (Active Directory Authentication Library) pour que JS acquière un jeton de porteur pour l’utilisateur connecté à partir d’Azure AD. Le code inclut le jeton dans les requêtes HTTP envoyées au niveau intermédiaire, comme l’indique le diagramme suivant. 

![Diagramme d’authentification de l’utilisateur](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Apportez les modifications suivantes au projet ToDoListAngular.

1. Ouvrez le fichier *index.cshtml*.
2. Supprimez les commentaires des lignes faisant référence à la bibliothèque d’authentification Active Directory (ADAL) pour les scripts JS.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Ouvrez le fichier *app/scripts/app.js* .
4. Supprimez le commentaire du bloc de code marqué pour « sans authentification » et supprimez le bloc de code marqué « avec authentification ».
   
    Cette modification fait référence au fournisseur d’authentification ADAL JS et lui fournit des valeurs de configuration. Lors des étapes suivantes, vous allez définir les valeurs de configuration pour votre application API et l’application Azure AD.
5. Dans le code qui définit la variable `endpoints` , définissez l’URL de l’API sur l’URL de l’application API créée pour le projet ToDoListAPI et définissez l’ID d’application Azure AD sur l’ID client que vous avez copié depuis le portail Azure Classic.
   
    Le code ressemble maintenant à l’exemple suivant.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. Dans l’appel de `adalProvider.init`, définissez `tenant` sur votre nom de client et `clientId` sur la valeur utilisée à l’étape précédente.
   
    Le code ressemble maintenant à l’exemple suivant.
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    Ces modifications de `app.js` indiquent que le code appelant et l’API appelée se trouvent dans la même application Azure AD.
7. Ouvrez le fichier *app/scripts/homeCtrl.js* .
8. Supprimez le commentaire du bloc de code marqué pour « sans authentification » et supprimez le bloc de code marqué « avec authentification ».
9. Ouvrez le fichier *app/scripts/indexCtrl.js* .
10. Supprimez le commentaire du bloc de code marqué pour « sans authentification » et supprimez le bloc de code marqué « avec authentification ».

### <a name="deploy-the-todolistangular-project-to-azure"></a>Déployer le projet ToDoListAngular dans Azure
1. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet ToDoListAngular, puis cliquez sur **Publier**.
2. Cliquez sur **Publier**.
   
    Visual Studio déploie le projet et ouvre un navigateur vers l’URL de base d’application Web. Cette commande affiche la page d’erreur 403, ce qui est normal pour une tentative d’accès à une URL de base d’API Web depuis un navigateur.
   
    Vous devez toujours apporter une modification à l’application API de niveau intermédiaire avant de pouvoir tester l’application.
3. Fermez le navigateur.

## <a name="configure-the-todolistapi-project-to-use-authentication"></a>Configurer le projet ToDoListAPI pour utiliser l’authentification
Pour le moment, le projet ToDoListAPI envoie « * » comme valeur `owner` pour ToDoListDataAPI. Dans cette section, vous allez modifier le code pour envoyer l’ID de l’utilisateur connecté.

Apportez les modifications suivantes au projet ToDoListAPI.

1. Ouvrez le fichier *Controllers/ToDoListController.cs* et supprimez les commentaires correspondant à la ligne de chaque méthode d’action définissant `owner` sur la valeur de revendication `NameIdentifier` d’Azure AD. Par exemple :
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Important** : ne supprimez pas les commentaires de code dans la méthode `ToDoListDataAPI`. Vous le ferez plus tard dans le didacticiel d’authentification du principal du service.

### <a name="deploy-the-todolistapi-project-to-azure"></a>Déployez le projet ToDoListAPI vers Azure
1. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet ToDoListAPI, puis cliquez sur **Publier**.
2. Cliquez sur **Publier**.
   
    Visual Studio déploie le projet et ouvre un navigateur vers l’URL de base d’application API.
3. Fermez le navigateur.

### <a name="test-the-application"></a>Test de l'application
1. Accédez à l’URL de l’application web, **Utilisation de HTTPS et non de HTTP**.
2. Cliquez sur l’onglet **To Do List** .
   
    Vous êtes invité à vous connecter.
3. Connectez-vous avec les informations d’identification d’un utilisateur dans votre client AAD.
4. La page **To do List** s’affiche.
   
   ![Page To Do List](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Aucune tâche ne s’affiche, car jusqu’ici, elles étaient toutes pour le propriétaire « * ». Maintenant le niveau intermédiaire demande des éléments pour l’utilisateur connecté, et aucun n’a encore été créé.
5. Ajoutez de nouveaux éléments de tâche pour vérifier que l’application fonctionne.
6. Dans une autre fenêtre de navigateur, accédez à l’URL de l’interface utilisateur Swagger pour l’application API ToDoListDataAPI, puis cliquez sur **ToDoList > Get**. Entrez un astérisque en tant que paramètre `owner` , puis cliquez sur **Try it out**.
   
   La réponse indique que la propriété Propriétaire des nouveaux éléments de tâche contient l’ID d’utilisateur Active Directory Azure.
   
   ![ID du propriétaire de la réponse JSON](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-the-projects-from-scratch"></a>Génération de projets de toutes pièces
Les deux projets d’API Web ont été créés à l’aide du modèle de projet **Azure API App** et par remplacement du contrôleur Values par défaut par un contrôleur ToDoList. 

Pour plus d’informations sur la création d’une application à page unique AngularJS avec un backend d’API Web 2, consultez [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs) (Exercice pratique : créer une application à page unique (SPA) avec l’API Web ASP.NET et Angular.js). Pour plus d’informations sur l’ajout du code d’authentification Azure AD, consultez les ressources suivantes :

* [Sécurisation d’une application à page unique AngularJS avec Azure AD](../active-directory/active-directory-devquickstarts-angular.md).
* [Présentation de JS ADAL v1](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Résolution de problèmes
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Assurez-vous de ne pas confondre ToDoListAPI (niveau intermédiaire) et ToDoListDataAPI (couche de données). Par exemple, vérifiez que vous avez ajouté l’authentification à l’application API de niveau intermédiaire, pas la couche de données. 
* Assurez-vous que le code source AngularJS fait référence à l’URL de l’application API de niveau intermédiaire (ToDoListAPI, pas ToDoListDataAPI) et à l’ID client correct d’Azure AD. 

## <a name="next-steps"></a>Étapes suivantes
Ce didacticiel vous a montré comment utiliser l’authentification du Service d’application pour une application API et comment appeler l’application API à l’aide de la bibliothèque ADAL JS. Dans le didacticiel suivant, vous allez découvrir comment [sécuriser l’accès à votre application API pour les scénarios de service à service](app-service-api-dotnet-service-principal-auth.md).

