---
title: authentification aaaUser pour API Apps dans Azure App Service | Documents Microsoft
description: "Découvrez comment tooprotect une application API dans Azure App Service en permettant aux tooauthenticated seuls utilisateurs."
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
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Authentification utilisateur pour API Apps dans Azure App Service
## <a name="overview"></a>Vue d'ensemble
Cet article explique comment tooprotect une application API Azure afin que seuls les utilisateurs authentifiés permettre appeler. Hello article suppose que vous avez lu hello [vue d’ensemble de l’authentification du Service d’applications Azure](../app-service/app-service-authentication-overview.md).

Vous apprendrez ce qui suit :

* Comment tooconfigure un fournisseur d’authentification, avec les détails pour Azure Active Directory (Azure AD).
* Comment une application API protégée à l’aide de tooconsume hello [Active Directory Authentication Library (ADAL) pour JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

article de Hello contient deux sections :

* Hello [comment l’authentification des utilisateurs dans Azure App Service tooconfigure](#authconfig) section explique de façon générale tooconfigure l’authentification utilisateur pour n’importe quelle application d’API et s’applique aussi bien les infrastructures tooall pris en charge par le Service d’application, y compris .NET, Node.js et Java.
* En commençant par hello [continuer didacticiels d’applications d’API .NET hello](#tutorialstart) section, hello guides article vous guide dans la configuration d’un exemple d’application avec un .NET back-end et un frontal AngularJS afin qu’il utilise Azure Active Directory pour l’utilisateur authentification. 

## <a id="authconfig"></a>Comment tooconfigure l’authentification des utilisateurs dans Azure App Service
Cette section fournit des instructions générales qui s’appliquent tooany API app. Pour tooDo de toohello spécifique comme exemple d’application .NET de la liste, consultez trop[poursuivre les didacticiels de prise en main de .NET hello](#tutorialstart).

1. Bonjour [portail Azure](https://portal.azure.com/), accédez toohello **paramètres** Panneau de l’application hello API que vous souhaitez tooprotect, rechercher hello **fonctionnalités** section, puis cliquez sur  **L’authentification / autorisation**.
   
    ![Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Bonjour **l’authentification / autorisation** panneau, cliquez sur **sur**.
3. Sélectionnez une des options de hello dans hello **tootake Action lors de la demande n’est pas authentifiée** liste déroulante.
   
   * Si vous souhaitez uniquement appels authentifiés tooreach votre application API, choisissez l’une des hello **connexion...**  options. Cette option permet de vous tooprotect hello application API sans écrire de code qui s’exécute qu’elle contient.
   * Si vous souhaitez que tous les appels tooreach votre application API, choisissez **autoriser les requêtes (aucune action)**. Vous pouvez utiliser ce choix de tooa option toodirect non authentifié aux appelants de fournisseurs d’authentification. Avec cette option, vous avez l’autorisation de toohandle toowrite code.
     
     Pour plus d’informations, consultez la page [Authentification et autorisation pour API Apps dans Azure App Service](app-service-api-authentication.md#multiple-protection-options).
4. Sélectionnez un ou plusieurs des hello **fournisseurs d’authentification**.
   
    image de Hello affiche les options qui nécessitent tous les appelants toobe authentifiées par Azure AD.
   
    ![Panneau Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Lorsque vous choisissez un fournisseur d’authentification, le portail de hello affiche un panneau de configuration pour ce fournisseur. 
   
    Pour obtenir des instructions détaillées qui expliquent comment tooconfigure hello panneaux de configuration de fournisseur d’authentification, consultez [comment tooconfigure votre connexion de Service d’applications application toouse Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (lien de hello va article tooan sur Azure AD, mais l’article hello lui-même contient des onglets qui lient tooarticles hello pour les autres fournisseurs d’authentification).
5. Lorsque vous avez terminé avec le panneau de configuration de fournisseur d’authentification hello, cliquez sur **OK**.
6. Bonjour **l’authentification / autorisation** panneau, cliquez sur **enregistrer**.

Dans ce cas, du Service d’applications s’authentifie à tous les appels d’API avant qu’ils atteignent l’application d’API hello. travail des services d’authentification Hello hello identique pour toutes les langues qui prend en charge du service d’applications, y compris .NET, Node.js et Java. 

toomake authentifié d’appels d’API, l’appelant de hello inclut un jeton de porteur OAuth 2.0 du fournisseur d’authentification hello dans l’en-tête d’autorisation de hello de requêtes HTTP. jeton de Hello peut être obtenu à l’aide du Kit de développement logiciel du fournisseur d’authentification hello.

## <a id="tutorialstart"></a>Didacticiels d’applications d’API .NET hello continues
Si vous suivez des didacticiels de Node.js ou Java hello pour les applications d’API, ignorer l’article suivant de toohello, [l’authentification principale du service pour les applications de l’API](app-service-api-dotnet-service-principal-auth.md). 

Si vous sont les suivantes : série de didacticiels .NET hello pour les applications de l’API et que vous avez déjà déployé un exemple d’application hello comme indiqué dans l’hello [première](app-service-api-dotnet-get-started.md) et [deuxième](app-service-api-cors-consume-javascript.md) didacticiels, ignorer toohello [configurer l’authentification dans le Service d’application et Azure AD](#azureauth) section.

Si vous souhaitez toofollow de ce didacticiel sans passer par les didacticiels de première et deuxième hello, procédez comme hello suivant les étapes qui expliquent comment tooget démarrer à l’aide d’un exemple d’application hello toodeploy processus automatisé.

> [!NOTE]
> Hello suit obtenir vous toohello à partir du même point comme si vous hello deux premiers didacticiels, à une exception près : Visual Studio ne sont pas informés déjà les application API qui chaque projet est déployé dans l’application web. Cela signifie que vous n’avez pas des instructions précises dans ce didacticiel expliquant comment les cibles de droite toohello toodeploy. Si vous n’êtes pas familiarisé avec déterminant comment les étapes sur votre propre déploiement de hello toodo, il est mieux série de didacticiels de hello toofollow de hello [premier didacticiel](app-service-api-dotnet-get-started.md) à toostart avec ce automatisée des processus de déploiement.
> 
> 

1. Assurez-vous que vous disposez de toutes les conditions préalables de hello répertoriées Bonjour [premier didacticiel](app-service-api-dotnet-get-started.md). Dans Ajout toohello conditions préalables répertoriées, ces didacticiels authentification supposent que vous avez travaillé avec des applications de Service d’applications web et les API des applications dans Visual Studio et hello portail Azure.
2. Cliquez sur hello **déployer tooAzure** bouton Bonjour [le fichier Lisez-moi référentiel tooDo liste exemple](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) toodeploy hello API apps et hello web app. Prenez note de groupe de ressources Azure hello qui a été créée, vous pouvez utiliser cette toolook ultérieure d’application web et les noms d’application API.
3. Téléchargement ou hello du clone [dépôt d’exemples liste tooDo](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) code hello tooget que vous allez utiliser localement dans Visual Studio.

## <a id="azureauth"></a> Configurer l’authentification dans App Service et Azure AD
Vous disposez désormais d’application hello en cours d’exécution dans Azure App Service sans exiger que les utilisateurs soit authentifié. Dans cette section vous ajoutez l’authentification en procédant comme hello tâches suivantes :

* Configurer l’authentification du Service d’applications toorequire Azure Active Directory (Azure AD) pour l’appel d’application de couche intermédiaire API hello.
* Créez une application Azure AD.
* Configurer le jeton de porteur hello de hello Azure AD application toosend après frontal d’ouverture de session toohello AngularJS. 

Si vous rencontrez des problèmes lors des instructions didacticiel hello suivantes, consultez hello [dépannage](#troubleshooting) section à fin hello du didacticiel de hello. 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>Configurer l’authentification pour le niveau intermédiaire de hello application API
1. Bonjour [portail Azure](https://portal.azure.com/), accédez toohello **paramètres** Panneau de l’application hello API que vous avez créé pour le projet de ToDoListAPI hello, recherche hello **fonctionnalités** section, puis Cliquez sur **l’authentification / autorisation**.
   
    ![Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Bonjour **l’authentification / autorisation** panneau, cliquez sur **sur**.
3. Bonjour **tootake Action lors de la demande n’est pas authentifiée** la liste déroulante, sélectionnez **se connecter avec Azure Active Directory**.
   
    Cette option permet de s’assurer qu’aucune demande unauathenticated n’atteindra hello API app. 
4. Sous **Fournisseurs d’authentification**, cliquez sur **Azure Active Directory**.
   
    ![Panneau Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Bonjour **paramètres Azure Active Directory** panneau, cliquez sur **Express**
   
    ![Option Express du panneau Authentification/Autorisation du portail Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Avec hello **Express** option, du Service d’applications peut automatiquement créer une application Azure AD dans votre annuaire Azure AD [client](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Vous n’avez toocreate d’un client, car chaque compte Azure a automatiquement un.
6. Sous **mode de gestion**, cliquez sur **créer une application AD** s’il n’est pas déjà sélectionnée, notez la valeur hello hello **créer application** zone de texte ; vous devez rechercher cette AAD application Bonjour portail classique Azure plus tard.
   
    ![Paramètres Azure AD du portail Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure crée automatiquement une application Azure AD avec hello le nom indiqué dans votre locataire Azure AD. Par défaut, hello application Azure AD est nommé même hello en tant qu’application hello API. Vous pouvez, si vous le souhaitez, choisir un autre nom.
7. Cliquez sur **OK**.
8. Bonjour **l’authentification / autorisation** panneau, cliquez sur **enregistrer**.
   
    ![Cliquez sur Enregistrer.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Maintenant seulement les utilisateurs dans votre locataire Azure AD peuvent appeler application d’API hello.

### <a name="optional-test-hello-api-app"></a>Facultatif : Application hello API de Test
1. Dans un navigateur, accédez toohello des URL de l’application hello API : Bonjour **application API** panneau Bonjour portail Azure, cliquez sur le lien hello sous **URL**.  
   
    Vous êtes écran de connexion tooa redirigé, car les demandes non authentifiées ne sont pas autorisées tooreach hello API app.
   
    Si votre navigateur est toohello « a été créé » page, navigateur de hello peut-être déjà être enregistré--dans ce cas, ouvrez une fenêtre de navigation InPrivate ou Incognito et atteindre l’URL de l’application toohello API.
2. Connectez-vous avec les informations d’identification d’un utilisateur de votre client Azure AD.
   
    Lorsque vous êtes connecté, la page de « correctement créée » de hello s’affiche dans le navigateur de hello.
3. Navigateur de fermer hello.

### <a name="configure-hello-azure-ad-application"></a>Configurer l’application hello Azure AD
Lorsque vous avez configuré l’authentification Azure AD, App Service a créé pour vous une application Azure AD. Par défaut, application hello nouveau Azure AD a été configuré tooprovide hello PORTEUR jeton toohello API URL de l’application. Dans cette section vous configurerez hello Azure AD application tooprovide hello PORTEUR jeton toohello AngularJS frontal au lieu de l’application de couche intermédiaire API de toohello directement. serveur frontal AngularJS Hello enverra hello jeton toohello API application lorsqu’il appelle l’application d’API hello.

> [!NOTE]
> processus de hello tookeep aussi simples que possible, ce didacticiel utilise une annonce Azure application frontale hello et application de couche intermédiaire API hello. Une autre option consiste à toouse deux des applications Azure AD. Dans ce cas, vous devez de toogive hello frontal Azure AD application autorisation toocall hello d’Azure AD application de couche intermédiaire. Cette approche d’application multiples permet d’obtenir un contrôle plus précis de la couche de tooeach d’autorisations.
> 
> 

1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), accédez trop**Azure Active Directory**.
   
   Vous avez portail classique de toouse hello, car certains paramètres d’Azure Active Directory dont vous avez besoin d’accéder à tooare pas encore disponible dans le portail Azure actuel de hello.
2. Sur hello **répertoire** , cliquez sur votre client AAD.
   
   ![Azure AD dans le portail classique](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Cliquez sur **Applications > Applications que ma société possède**, puis cliquez sur la case à cocher hello.
   
   Vous pouvez également disposer toorefresh hello page toosee hello nouvelle application.
4. Dans la liste de hello des applications, cliquez sur nom hello hello Azure créée pour vous lorsque vous avez activé l’authentification pour votre application API.
   
   ![Onglet Applications Azure AD](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Cliquez sur **Configurer**.
   
   ![Onglet Configurer Azure AD](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Définissez **URL de connexion** toohello des URL pour votre application web AngularJS, aucune barre oblique.
   
   Par exemple : https://todolistangular.azurewebsites.net
   
   ![URL de connexion](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Définissez **URL de réponse** toohello des URL pour votre application web, aucune barre oblique.
   
   Par exemple : https://todolistsangular.azurewebsites.net
8. Cliquez sur **Enregistrer**.
   
   ![URL de réponse](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. Au bas de hello de page de hello, cliquez sur **gérer manifeste > téléchargement manifeste**.
   
   ![Télécharger le manifeste](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Téléchargez hello tooa emplacement_fichier où vous pouvez les modifier.
11. Dans le fichier de manifeste hello téléchargé, recherchez hello `oauth2AllowImplicitFlow` propriété. Modifier la valeur hello de cette propriété à partir de `false` trop`true`, puis enregistrez le fichier de hello.
    
    Ce paramètre est obligatoire pour l’accès depuis une application de page JavaScript unique. Il permet de toobe jeton du porteur Oauth 2.0 hello retournée dans un fragment d’URL hello.
12. Cliquez sur **gérer manifeste > téléchargement manifeste**et le téléchargement hello fichier mis à jour dans hello précédant l’étape.
    
    ![Télécharger le manifeste sur le serveur](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Hello de copie **ID Client** valeur et l’enregistrer dans un endroit vous pouvez l’obtenir à partir de versions ultérieures.

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>Configurer l’authentification de hello ToDoListAngular projet toouse
Dans cette section, vous modifiez le frontal AngularJS hello afin qu’il utilise Active Directory Authentication Library (ADAL) pour JS tooacquire un jeton de support pour l’utilisateur connecté hello d’Azure AD. code de Hello inclut hello jeton dans les requêtes HTTP envoyées toohello de couche intermédiaire, comme indiqué dans hello suivant schéma. 

![Diagramme d’authentification de l’utilisateur](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Rendre hello suivant toofiles des modifications dans le projet de ToDoListAngular hello.

1. Ouvrez hello *index.cshtml* fichier.
2. Supprimez les commentaires des lignes hello qui font référence à hello Active Directory Authentication Library (ADAL) pour les scripts JS.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Ouvrez hello *app/scripts/app.js* fichier.
4. Commentez bloc hello de code marqué pour « sans authentification » et supprimez les commentaires de bloc hello de code marqué pour « avec l’authentification ».
   
    Cette modification fait référence à un fournisseur d’authentification ADAL JS hello et fournit des tooit de valeurs de configuration. Bonjour, comme suit, vous définir des valeurs de configuration hello pour votre application API et l’application Azure AD.
5. Dans le code hello qui définit hello `endpoints` hello variable, affectez la valeur URL de l’API toohello URL de l’application hello API que vous avez créé pour le projet de ToDoListAPI hello, définissez hello Azure AD ID toohello client ID d’application que vous avez copié à partir de hello portail Azure classic.
   
    code de Hello est désormais toohello similaire, l’exemple suivant.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. Bonjour, appelez trop`adalProvider.init`, définissez `tenant` tooyour nom_client et `clientId` valeur toosame utilisé à l’étape précédente de hello.
   
    code de Hello est désormais toohello similaire, l’exemple suivant.
   
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
   
    Ces modifications trop`app.js` spécifier que le code appelant de hello et hello appelé API sont dans l’application hello même instance Azure AD.
7. Ouvrez hello *app/scripts/homeCtrl.js* fichier.
8. Commentez bloc hello de code marqué pour « sans authentification » et supprimez les commentaires de bloc hello de code marqué pour « avec l’authentification ».
9. Ouvrez hello *app/scripts/indexCtrl.js* fichier.
10. Commentez bloc hello de code marqué pour « sans authentification » et supprimez les commentaires de bloc hello de code marqué pour « avec l’authentification ».

### <a name="deploy-hello-todolistangular-project-tooazure"></a>Déployer hello ToDoListAngular projet tooAzure
1. Dans **l’Explorateur de solutions**, cliquez sur le projet de ToDoListAngular hello, puis cliquez sur **publier**.
2. Cliquez sur **Publier**.
   
    Visual Studio déploie hello projet et ouvre l’URL de base d’un navigateur toohello application web. Cette opération affiche une page de 403 erreur, ce qui est normale d’une URL base tentative toogo tooa API Web depuis un navigateur.
   
    Vous avez toujours toomake une couche intermédiaire de modification toohello application API avant de pouvoir tester application hello.
3. Navigateur de fermer hello.

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>Configurer l’authentification de hello ToDoListAPI projet toouse
Actuellement hello envoie de projet ToDoListAPI « * » comme hello `owner` tooToDoListDataAPI de valeur. Dans cette section vous modifiez hello code toosend hello ID de l’utilisateur connecté hello.

Rendre hello suivant modifications hello ToDoListAPI projet.

1. Ouvrez hello *Controllers/ToDoListController.cs* de fichiers et supprimez les commentaires de la ligne hello dans chaque méthode d’action qui définit `owner` toohello AD Azure `NameIdentifier` valeur de revendication. Par exemple :
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Important**: ne supprimez les commentaires de code hello `ToDoListDataAPI` méthode ; vous allez faire ultérieurement pour le didacticiel de l’authentification du principal de service hello.

### <a name="deploy-hello-todolistapi-project-tooazure"></a>Déployer hello ToDoListAPI projet tooAzure
1. Dans **l’Explorateur de solutions**, cliquez sur le projet de ToDoListAPI hello, puis cliquez sur **publier**.
2. Cliquez sur **Publier**.
   
    Visual Studio déploie hello projet et ouvre l’URL de base d’un navigateur toohello API application.
3. Navigateur de fermer hello.

### <a name="test-hello-application"></a>Tester l’application hello
1. Atteindre l’URL toohello de hello web app, **à l’aide de HTTPS, pas HTTP**.
2. Cliquez sur hello **tooDo liste** onglet.
   
    Vous êtes invité à toolog dans.
3. Connectez-vous avec les informations d’identification hello d’un utilisateur dans votre client AAD.
4. Hello **tooDo liste** page s’affiche.
   
   ![page de liste tooDo](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Aucune tâche ne s’affiche, car jusqu’ici, elles étaient toutes pour le propriétaire « * ». Maintenant intermédiaire hello est demandant des éléments pour l’utilisateur connecté hello et aucun n’a encore été créée.
5. Ajouter un nouveau tooverify d’éléments de tâches hello application fonctionne.
6. Dans une autre fenêtre de navigateur, accédez à toohello Swagger une URL de l’interface utilisateur pour l’application d’API de ToDoListDataAPI hello et cliquez sur **ToDoList > obtenir**. Entrez un astérisque pour hello `owner` paramètre, puis cliquez sur **essayez-le**.
   
   réponse de Hello montre que nouveaux éléments de tâches hello ont des ID d’utilisateur hello AD Azure réel dans la propriété de propriétaire hello.
   
   ![ID du propriétaire de la réponse JSON](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>Génération de projets hello à partir de zéro
projets d’API Web Hello deux ont été créés à l’aide de hello **application API Azure** modèle et en remplaçant contrôleur de valeurs par défaut hello avec un contrôleur de la liste des tâches de projet. 

Pour plus d’informations sur la façon de trop de création d’une application de page unique AngularJS avec un API Web 2 serveur principal, consultez [mains sur Lab : générer une Application de Page unique (SPA) avec l’API Web ASP.NET et Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Pour plus d’informations sur la façon tooadd code d’authentification Azure AD, consultez hello suivant des ressources :

* [Sécurisation d’une application à page unique AngularJS avec Azure AD](../active-directory/active-directory-devquickstarts-angular.md).
* [Présentation de JS ADAL v1](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Résolution de problèmes
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Assurez-vous de ne pas confondre ToDoListAPI (niveau intermédiaire) et ToDoListDataAPI (couche de données). Par exemple, vérifiez que vous avez ajouté l’application d’API intermédiaire authentication toohello, pas le niveau de données hello. 
* Vérifiez que l’URL de l’application hello AngularJS source code références hello intermédiaire API (ToDoListAPI, ToDoListDataAPI pas) et hello corrects ID de client Azure AD. 

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toouse l’authentification du Service de l’application pour une application API et comment toocall hello application API à l’aide de hello bibliothèque de la bibliothèque ADAL JS. Dans l’étape suivante du didacticiel hello vous allez apprendre comment trop[application tooyour API de sécuriser l’accès pour les scénarios de service](app-service-api-dotnet-service-principal-auth.md).

