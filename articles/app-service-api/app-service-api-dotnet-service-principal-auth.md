---
title: "l’authentification du principal aaaService pour API Apps dans Azure App Service | Documents Microsoft"
description: "Découvrez comment application tooprotect une API dans Azure App Service pour les scénarios de service."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Authentification de principal du service pour API Apps dans Azure App Service
## <a name="overview"></a>Vue d'ensemble
Cet article explique comment l’authentification du Service d’applications de toouse pour *interne* accéder aux applications de tooAPI. Un scénario interne est où vous avez une application API que vous souhaitez toobe utilisable uniquement par votre propre code d’application. Hello recommandé tooimplement de façon ce scénario dans le Service d’applications est toouse Azure AD tooprotect hello appelée application API. Vous appelez application d’API hello protégé avec un jeton de support que vous obtenez d’Azure AD en fournissant des informations d’identification (principal du service) d’identité de l’application. Pour les alternatives toousing Azure AD, consultez hello **l’authentification de service** section Hello [vue d’ensemble de l’authentification du Service d’applications Azure](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

Cet article porte sur les points suivants :

* Comment toouse Azure Active Directory (Azure AD) tooprotect une API application à partir de l’accès non authentifié.
* Comment application tooconsume API protégée d’une application API, une application web ou une application mobile à l’aide des informations d’identification de l’entité de sécurité (identité de l’application) de service Azure AD. Pour plus d’informations sur la façon tooconsume à partir d’une application logique, consultez [à l’aide de votre API personnalisée hébergé sur App Service avec les applications de la logique](../logic-apps/logic-apps-custom-hosted-api.md).
* Comment toomake que ce hello protégée application API ne peut pas être appelée à partir d’un navigateur par des utilisateurs connectés.
* Comment toomake que ce hello protégée application API peut uniquement être appelée par un spécifique principal du service Azure AD.

article de Hello contient deux sections :

* Hello [comment tooconfigure service principal d’authentification dans Azure App Service](#authconfig) section explique en général l’authentification tooconfigure pour n’importe quelle application API, et comment tooconsume hello protégés application API. Cette section s’applique aussi bien les infrastructures tooall pris en charge par le Service d’application, y compris .NET, Node.js et Java.
* En commençant par hello [poursuivre les didacticiels de prise en main de .NET hello](#tutorialstart) section, hello didacticiel vous guide Configuration d’un scénario de « accès interne » pour un exemple d’application .NET en cours d’exécution dans le Service d’applications. 

## <a id="authconfig"></a>Comment tooconfigure service principal d’authentification dans Azure App Service
Cette section fournit des instructions générales qui s’appliquent tooany API app. Pour tooDo de toohello spécifique comme exemple d’application .NET de la liste, consultez trop[poursuivre la série de didacticiels .NET API Apps hello](#tutorialstart).

1. Bonjour [portail Azure](https://portal.azure.com/), accédez toohello **paramètres** Panneau de l’application hello API que vous le souhaitez tooprotect et recherchez hello **fonctionnalités** et cliquez sur **L’authentification / autorisation**.
   
    ![Authentification/Autorisation dans le portail Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Bonjour **l’authentification / autorisation** panneau, cliquez sur **sur**.
3. Bonjour **tootake Action lors de la demande n’est pas authentifiée** la liste déroulante, sélectionnez **se connecter avec Azure Active Directory** .
4. Sous **Fournisseurs d’authentification**, cliquez sur **Azure Active Directory**.
   
    ![Panneau Authentification/Autorisation dans le portail Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Configurer hello **paramètres Azure Active Directory** panneau toocreate un nouvel Azure application AD ou utilisez une application Azure AD existante si vous en avez déjà que vous souhaitez toouse.
   
    Les scénarios internes impliquent généralement l’appel d’une application API à une autre. Vous pouvez utiliser soit des applications Azure AD distinctes pour chaque application API, soit une simple application Azure AD.
   
    Pour obtenir des instructions détaillées sur ce panneau, consultez [comment tooconfigure votre connexion de Service d’applications application toouse Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Lorsque vous avez terminé avec le panneau de configuration de fournisseur d’authentification hello, cliquez sur **OK**.
7. Bonjour **l’authentification / autorisation** panneau, cliquez sur **enregistrer**.
   
    ![Cliquez sur Enregistrer.](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Dans ce cas, du Service d’applications autorise uniquement les demandes provenant d’appelants dans le locataire Azure AD de hello configuré. Aucun code d’authentification ou d’autorisation n’est requis dans l’application d’API hello protégé. Hello jeton de support est passé application toohello API ainsi que les revendications couramment utilisées dans les en-têtes HTTP, et vous pouvez lire ces informations dans le code toovalidate qui sont des demandes provenant d’un appelant particulière, par exemple un principal de service.

Cette fonctionnalité d’authentification fonctionne hello identique pour toutes les langues que le service application prend en charge, y compris .NET, Node.js et Java. 

#### <a name="how-tooconsume-hello-protected-api-app"></a>Mode de protection de l’application API de tooconsume hello
appelant de Hello devez fournir un jeton de support Azure AD avec les appels d’API. tooget un jeton de support à l’aide des informations d’identification du principal de service, l’appelant de hello utilise la bibliothèque d’authentification Active Directory (ADAL pour [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), ou [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). tooget un jeton, le code hello qui appelle la bibliothèque ADAL fournit hello tooADAL informations suivantes :

* nom de Hello de votre client Azure AD.
* Hello client et ID de clé secrète client (clé d’application) de l’application hello Azure AD associée à l’appelant de hello.
* ID de client Hello Hello application Azure AD associée hello protégé application API. (Si qu’une application Azure AD est utilisée, cela est hello même ID de client comme un appelant de hello hello.)

Ces valeurs sont disponibles dans les pages de hello Azure AD de hello [portail Azure classic](https://manage.windowsazure.com/).

Une fois que le jeton de hello a été acquis, l’appelant de hello inclut les requêtes HTTP dans l’en-tête d’autorisation hello.  Service d’applications valide le jeton de hello et permet de hello de tooreach demandes hello protégé application API.

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>Comment application hello API de tooprotect à partir de l’accès par des utilisateurs Bonjour même locataire
Les jetons de support pour les utilisateurs de hello même client sont considérées comme valides pour hello protégé application API.  Si vous voulez tooensure un service principal peut appeler hello application API protégée, ajoutez le code de hello protégé hello de toovalidate d’application API suivant des revendications à partir du jeton de hello :

* `appid`doit être hello des ID de client de l’application hello Azure AD qui est associée à l’appelant de hello. 
* `oid`(`objectidentifier`) doit être l’ID de principal du service hello de l’appelant de hello. 

Service d’applications fournit également hello `objectidentifier` revendication dans l’en-tête de hello X-MS-CLIENT-PRINCIPAL-ID.

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>Comment tooprotect hello application API à partir de l’accès du navigateur
Si vous ne validez les revendications dans le code dans l’application d’API hello protégé, et si vous utilisez un distinct application Azure AD pour hello protégé API app, assurez-vous que hello URL de réponse de l’application Azure AD est ne Hello pas identique hello URL de base de l’application API. Si hello URL de réponse pointe directement toohello protégé API app, un utilisateur de client de hello même instance Azure AD peut parcourir l’application d’API toohello session et appeler les API hello.

## <a id="tutorialstart"></a>Poursuivre la série de didacticiels hello .NET API Apps
Si vous suivez hello Node.js ou Java série de didacticiels pour les applications d’API, ignorer toohello [étapes](#next-steps) section. 

reste Hello de cet article poursuit la série de didacticiels .NET API Apps hello et suppose que vous avez terminé hello [didacticiel de l’authentification utilisateur](app-service-api-dotnet-user-principal-auth.md) et posséder hello exemple d’application en cours d’exécution dans Azure avec l’authentification utilisateur activé.

## <a name="set-up-authentication-in-azure"></a>Configurer l’authentification dans Azure
Dans cette section vous configurez le Service d’applications afin de rendre ce hello uniquement HTTP demande permet de tooreach hello données couche API application hello ceux ayant Azure valide les jetons de porteur AD. 

Bonjour suivant la section, vous configurez hello intermédiaire API application toosend tooAzure application informations d’identification Active Directory, récupérer un jeton de support, envoyez porteur de hello jeton toohello données couche API app. Ce processus est illustré dans le diagramme de hello.

![Diagramme d’authentification du service](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Si vous rencontrez des problèmes lors des instructions didacticiel hello suivantes, consultez hello [dépannage](#troubleshooting) section à fin hello du didacticiel de hello. 

1. Bonjour [portail Azure](https://portal.azure.com/), accédez toohello **paramètres** Panneau de l’application hello API créé pour l’application d’API hello ToDoListDataAPI (couche de données), puis cliquez sur **paramètres**.
2. Bonjour **paramètres** panneau, rechercher hello **fonctionnalités** section, puis cliquez sur **l’authentification / autorisation**.
   
    ![Authentification/Autorisation dans le portail Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. Bonjour **l’authentification / autorisation** panneau, cliquez sur **sur**.
4. Bonjour **tootake Action lors de la demande n’est pas authentifiée** la liste déroulante, sélectionnez **se connecter avec Azure Active Directory**.
   
    Il s’agit de paramètre hello qui provoque le Service d’applications tooensure qui a authentifié uniquement les demandes portée hello API app. Pour les demandes qui ont des jetons de support valide, Service de l’application transmet les jetons hello le long de l’application de toohello API et remplit les en-têtes HTTP avec des revendications courantes toomake ces informations plus facilement accessibles tooyour code.
5. Sous **Fournisseurs d’authentification**, cliquez sur **Azure Active Directory**.
   
    ![Panneau Authentification/Autorisation dans le portail Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. Bonjour **paramètres Azure Active Directory** panneau, cliquez sur **Express**.
   
    Avec hello **Express** option Azure peut créer automatiquement une application AAD dans votre annuaire Azure AD [client](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Vous n’avez toocreate d’un client, car chaque compte Azure a automatiquement un.
7. Sous **Mode d’administration**, cliquez sur **Créer une application AD**, si cette option n’est pas déjà sélectionnée.
   
    portail de Hello branche hello **créer application** zone d’entrée avec une valeur par défaut. Par défaut, hello application Azure AD est nommé même hello en tant qu’application hello API. Vous pouvez, si vous le souhaitez, choisir un autre nom.
   
    ![Paramètres Azure AD](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Remarque**: en guise d’alternative, vous pouvez utiliser un seul AD Azure application pour les deux hello appelante application API et hello protégé application API. Si vous choisissez cette solution, vous ne devez pas hello **créer une application AD** option ici, car vous déjà créé une application Azure AD plus haut dans le didacticiel de l’authentification utilisateur hello. Pour ce didacticiel, vous allez utiliser séparer des applications Azure AD pour hello appel application API et hello protégé application API.
8. Prenez note de la valeur hello hello **créer application** zone d’entrée ; vous devez rechercher cette application AAD Bonjour portail Azure classic ultérieurement.
9. Cliquez sur **OK**.
10. Bonjour **l’authentification / autorisation** panneau, cliquez sur **enregistrer**.
    
    ![Cliquez sur Enregistrer.](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    Service de l’application crée une application Azure Active Directory avec **URL de connexion** et **URL de réponse** automatiquement la valeur URL toohello de votre application API. valeur de cette dernière Hello permet les utilisateurs de votre toolog de locataire AAD dans et application d’API accès hello.

### <a name="verify-that-hello-api-app-is-protected"></a>Vérifiez que cette application hello API est protégée.
1. Dans un navigateur, accédez toohello des URL de l’application hello API : Bonjour **application API** panneau Bonjour portail Azure, cliquez sur le lien hello sous **URL**. 
   
    Vous êtes écran de connexion tooa redirigé, car les demandes non authentifiées ne sont pas autorisées tooreach hello API app. 
   
    Si votre navigateur accédez toohello Swagger de l’interface utilisateur, votre navigateur peut déjà connecté--dans ce cas, ouvrez une fenêtre de navigation InPrivate ou Incognito et accédez toohello Swagger une URL de l’interface utilisateur.
2. Connectez-vous avec les informations d’identification d’un utilisateur de votre client AAD.
   
   Lorsque vous êtes connecté, la page de « correctement créée » de hello s’affiche dans le navigateur de hello.

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Configurer hello ToDoListAPI projet tooacquire et envoyer le jeton d’Azure AD hello
Dans cette section, vous hello tâche suivantes :

* Ajoutez du code dans l’application d’API de niveau intermédiaire hello qui utilise les informations d’identification tooacquire un jeton de Azure AD application et envoyer des que demandes avec HTTP toohello données couche API app.
* Obtenir des informations d’identification de hello que vous avez besoin d’Azure AD.
* Entrez des informations d’identification de hello dans les paramètres d’environnement runtime du Service d’applications Azure dans la couche intermédiaire de hello application API. 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Configurer hello ToDoListAPI projet tooacquire et envoyer le jeton d’Azure AD hello
Rendre hello suit les modifications dans le projet de ToDoListAPI hello dans Visual Studio.

1. Supprimez les commentaires de tout code hello Bonjour *ServicePrincipal.cs* fichier.
   
    Il s’agit de code hello qui utilise la bibliothèque ADAL pour le jeton de support .NET tooacquire hello Azure AD.  Elle utilise plusieurs valeurs de configuration que vous allez définir ultérieurement dans l’environnement d’exécution Azure hello. Voici le code de hello : 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **Remarque :** ce code nécessite hello ADAL pour le package NuGet .NET (Microsoft.IdentityModel.Clients.ActiveDirectory), qui est déjà installé dans le projet de hello. Si vous avez créé ce projet à partir de zéro, vous devriez tooinstall ce package. Ce package n’est pas installé automatiquement par le modèle de nouveau projet application hello API.
2. Dans *contrôleurs/ToDoListController*, supprimez les commentaires de code hello Bonjour `NewDataAPIClient` méthode qui ajoute des demandes de jeton tooHTTP hello dans l’en-tête d’autorisation hello.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Déployer le projet de ToDoListAPI hello. (Projet de hello d’avec le bouton droit, puis cliquez sur **publier > Publier**.)
   
    Visual Studio déploie hello projet et ouvre l’URL de base d’un navigateur toohello application web. Cette opération affiche une page de 403 erreur, ce qui est normale d’une URL base tentative toogo tooa API Web depuis un navigateur.
4. Navigateur de fermer hello.

### <a name="get-azure-ad-configuration-values"></a>Obtenir les valeurs de configuration Azure AD
1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), accédez trop**Azure Active Directory**.
2. Sur hello **répertoire** , cliquez sur votre client AAD.
3. Cliquez sur **Applications > Applications que ma société possède**, puis cliquez sur la case à cocher hello.
4. Dans la liste de hello des applications, cliquez sur nom hello hello Azure créée pour vous lorsque vous avez activé l’authentification pour l’application d’API hello ToDoListDataAPI (couche de données).
5. Cliquez sur hello **configurer** onglet.
6. Hello de copie **ID Client** valeur et enregistrer un endroit où vous pouvez l’obtenir à partir de versions ultérieures. 
7. Bonjour portail Azure classic revenir en arrière toohello la liste des **Applications que ma société possède**et cliquez sur l’application hello AAD que vous avez créé pour l’application de ToDoListAPI API de niveau intermédiaire hello (hello celui créé dans le cadre du didacticiel précédent hello, pas Hello vous créée dans ce didacticiel).
8. Cliquez sur hello **configurer** onglet.
9. Hello de copie **ID Client** valeur et enregistrer un endroit où vous pouvez l’obtenir à partir de versions ultérieures.
10. Sous **clés**, sélectionnez **1 an** de hello **sélectionner une durée** liste déroulante.
11. Cliquez sur **Enregistrer**.
    
     ![Générer la clé d’application](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Copiez la valeur de clé hello et enregistrer un endroit où que vous pouvez l’obtenir à partir de versions ultérieures.
    
     ![Copiez la nouvelle clé d’application](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>Configurer les paramètres d’Azure AD dans l’environnement d’exécution de l’application de couche intermédiaire API hello
1. Accédez toohello [portail Azure](https://portal.azure.com/), puis accédez toohello **application API** panneau pour l’application hello API qui héberge le projet d’hello TodoListAPI (intermédiaire).
2. Cliquez sur **Paramètres > Paramètres de l'application**.
3. Bonjour **paramètres de l’application** section, ajoutez des clés et de valeurs hello suivant :
   
   | **Clé** | ida:Authority |
   | --- | --- |
   | **Valeur** |https://login.microsoftonline.com/{nom de votre client Azure AD} |
   | **Exemple** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Clé** | ida:ClientId |
   | --- | --- |
   | **Valeur** |ID client de hello appel d’application (couche intermédiaire - ToDoListAPI) |
   | **Exemple** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Clé** | ida:ClientSecret |
   | --- | --- |
   | **Valeur** |Clé d’une application Hello appel d’application (couche intermédiaire - ToDoListAPI) |
   | **Exemple** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Clé** | ida:Resource |
   | --- | --- |
   | **Valeur** |ID client de hello appelée application (couche de données - ToDoListDataAPI) |
   | **Exemple** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Remarque**: pour `ida:Resource`, assurez-vous que vous utilisez hello appelé l’application **ID client** et non pas son **URI ID d’application**.
   
    `ida:ClientId`et `ida:Resource` sont différentes valeurs pour ce didacticiel, car vous utilisez séparer applicaations Azure AD pour la couche intermédiaire de hello et la couche données. Si vous utilisez une seule application Azure AD pour hello appel application API et hello protégé application API, vous utilisez hello même valeur dans les deux `ida:ClientId` et `ida:Resource`.
   
    code de Hello utilise ConfigurationManager tooget ces valeurs, il peut être stockés dans le fichier Web.config du projet hello ou dans l’environnement d’exécution Azure hello. Pendant l’exécution d’une application ASP.NET dans Azure App Service, les paramètres d’environnement remplacent automatiquement les paramètres du fichier Web.config. Paramètres d’environnement sont en général un [plus sécurisé moyen toostore personnelles comparées fichier Web.config de tooa](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Cliquez sur **Enregistrer**.
   
    ![Cliquez sur Enregistrer.](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>Tester l’application hello
1. Dans un navigateur, accédez toohello URL HTTPS de hello AngularJS frontal web app.
2. Cliquez sur hello **tooDo liste** onglet et connectez-vous avec les informations d’identification d’un utilisateur dans votre locataire Azure AD. 
3. Ajouter des tâches éléments tooverify que l’utilisation de l’application hello.
   
    ![page de liste tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Si l’application hello ne fonctionne pas comme prévu, vérifiez que tous les paramètres de hello saisis dans hello portail Azure. Si tous les paramètres de hello apparaissent toobe correct, consultez hello [dépannage](#troubleshooting) section plus loin dans ce didacticiel.

## <a name="protect-hello-api-app-from-browser-access"></a>Protéger hello API application à partir de l’accès du navigateur
Pour ce didacticiel, vous avez créé un distinct application Azure AD pour l’application hello API de ToDoListDataAPI (couche de données). Comme vous avez vu, lorsque le Service d’applications crée une application AAD, il configure application AAD de hello d’une façon qui permet à un utilisateur toogo toohello API URL de l’application dans un navigateur et le journal sur. Cela signifie qu’il est possible pour un utilisateur final dans votre locataire Azure AD, et pas seulement un principal de service, tooaccess hello API. 

Si vous souhaitez que l’accès du navigateur tooprevent sans écrire de code Bonjour protégées application API, vous pouvez modifier hello **URL de réponse** Bonjour application AAD afin qu’il soit différent de l’application hello API URL de base. 

### <a name="disable-browser-access"></a>Désactiver l’accès du navigateur
1. Dans le portail hello classic **configurer** pour application AAD hello qui a été créée pour hello TodoListService, modifiez la valeur hello Bonjour **URL de réponse** champ afin qu’il soit une URL valide, mais pas hello API de l’application URL.
2. Cliquez sur **Enregistrer**.

### <a name="verify-browser-access-no-longer-works"></a>Vérifier que l’accès au navigateur ne fonctionne plus
Précédemment, vous avez vérifié que vous pouvez accéder toohello URL de l’application API à partir d’un navigateur en vous connectant avec les informations d’identification d’un utilisateur individuel. Dans cette section, vous allez vérifier que cet accès ne fonctionne plus. 

1. Dans une nouvelle fenêtre de navigateur, accédez à nouveau toohello des URL de l’application d’API hello.
2. Ouvrez une session lorsque vous y êtes invité toodo donc.
3. Connexion réussit, mais entraîne une page d’erreurs tooan.
   
    Vous avez configuré hello AAD application afin que les utilisateurs du client AAD de hello ne peut pas se connecter et accéder aux API de hello à partir d’un navigateur. Vous pouvez toujours accéder à application d’API hello à l’aide d’un jeton de principal du service, vous pouvez vérifier en sélectionnant des URL de l’application toohello web et ajouter des éléments de tâches plus.

## <a name="restrict-access-tooa-particular-service-principal"></a>Restreindre la principal de service particulier d’accès tooa
Pour l’instant, tout appelant qui peut obtenir un jeton pour un utilisateur ou principal du service dans votre locataire Azure AD peut appeler l’application hello API de TodoListDataAPI (couche de données). Vous souhaiterez peut-être toomake que cette application d’API hello données couche n’accepte que les appels à partir de l’application d’API hello TodoListAPI (intermédiaire) et uniquement à partir d’un principal de service particulier. 

Vous pouvez ajouter ces restrictions en ajoutant hello toovalidate de code `appid` et `objectidentifier` les revendications pour les appels entrants.

Pour ce didacticiel, vous placez hello de code qui valide l’ID d’application et l’ID de principal de service directement dans vos actions de contrôleur.  Alternatives sont toouse personnalisé `Authorize` attribut ou toodo cette validation dans vos séquences de démarrage (par exemple, le middleware OWIN). Pour obtenir un exemple de hello ce dernier, consultez [cet exemple d’application](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Rendre hello suivant du projet de TodoListDataAPI toohello de modifications.

1. Ouvrez hello *Controllers/TodoListController.cs* fichier.
2. Commentaire hello définir `trustedCallerClientId` et `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Supprimez les commentaires de code hello Bonjour CheckCallerId méthode. Cette méthode est appelée au début de hello de chaque méthode d’action de contrôleur de hello. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. Redéployez hello ToDoListDataAPI tooAzure de projet du Service d’applications.
5. Dans votre navigateur, accédez URL HTTPS de l’application web toohello AngularJS front-end et dans la page d’accueil hello, cliquez sur hello **tooDo liste** onglet.
   
    application Hello ne fonctionne pas, car les appels toohello retour de fin échouent. est la vérification du code de nouveau Hello appid réel et objectidentifier, mais il ne dispose pas encore hello valeurs correctes toocheck contre les. navigateur de Hello Console des outils de développement signale que ce serveur hello retourne une erreur HTTP 401.
   
    ![Erreur dans la console des outils de développement](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    Vous configurez les valeurs attendues hello hello comme suit.
6. À l’aide de PowerShell Azure AD, obtenir valeur hello du service de hello principal pour hello application Azure AD que vous avez créé pour le projet de TodoListWebApp hello.
   
    a. Pour obtenir des instructions sur la façon de tooinstall Azure PowerShell et se connecter tooyour abonnement, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).
   
    b. tooget une liste des principaux de service, exécutez hello `Login-AzureRmAccount` des commandes et puis hello `Get-AzureRmADServicePrincipal` commande.
   
    c. Recherchez hello objectid hello principal du service d’application de TodoListAPI hello et enregistrez-le dans un emplacement que vous pouvez copier à partir de versions ultérieures.
7. Dans hello portail Azure, accédez à panneau de l’application API toohello pour l’application hello API que vous avez déployé le projet ToDoListDataAPI hello.
8. Cliquez sur **Paramètres > Paramètres de l’application**.
9. Bonjour **paramètres de l’application** section, ajoutez des clés et de valeurs hello suivant :
   
   | **Clé** | todo:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Valeur** |ID du principal de service principal de l’application appelante |
   | **Exemple** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Clé** | todo:TrustedCallerClientId |
   | --- | --- |
   | **Valeur** |ID de client de l’appel d’application - copiée à partir de l’application de hello TodoListAPI Azure AD |
   | **Exemple** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Cliquez sur **Enregistrer**.
    
     ![Cliquez sur Enregistrer.](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. Dans votre navigateur, retourne l’URL de l’application toohello web, dans la page d’accueil hello, cliquez sur hello **tooDo liste** onglet.
    
     Cette application hello de temps fonctionne comme prévu, car l’application hello appelant approuvé ID et l’ID de principal de service sont les valeurs attendues hello.
    
     ![page de liste tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>Génération de projets hello à partir de zéro
projets d’API Web Hello deux ont été créés à l’aide de hello **application API Azure** modèle et en remplaçant contrôleur de valeurs par défaut hello avec un contrôleur de la liste des tâches de projet. Pour l’acquisition des jetons de principal du service Azure AD dans le projet de ToDoListAPI hello, hello [Active Directory Authentication Library (ADAL) pour .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) le package NuGet a été installé.

Pour plus d’informations sur la façon de trop de création d’une application de page unique AngularJS avec un API Web back-end comme ToDoListAngular, consultez [mains sur Lab : générer une Application de Page unique (SPA) avec l’API Web ASP.NET et Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Pour plus d’informations sur la façon tooadd code d’authentification Azure AD, consultez [sécurisation AngularJS Page applications unique avec Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Résolution des problèmes
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Assurez-vous de ne pas confondre ToDoListAPI (niveau intermédiaire) et ToDoListDataAPI (couche de données). Par exemple, dans ce didacticiel, vous ajoutez l’authentification toohello données couche API app, **mais clé d’une application hello doit provenir d’hello application Azure AD que vous avez créé pour l’application de couche intermédiaire API hello**.

## <a name="next-steps"></a>Étapes suivantes
Il s’agit de didacticiel de dernière hello Bonjour série d’applications API. 

Pour plus d’informations sur Azure Active Directory, consultez hello suivant des ressources.

* [Guide du développeur Azure AD](http://aka.ms/aaddev)
* [Scénarios Azure AD](http://aka.ms/aadscenarios)
* [Exemples Azure AD](http://aka.ms/aadsamples)
  
    Hello [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) exemple est semblable toowhat est indiqué dans ce didacticiel, mais sans utiliser l’authentification du Service d’applications.

Pour plus d’informations sur les autres méthodes toodeploy Visual Studio projets tooAPI applications, à l’aide de Visual Studio ou [automatiser le déploiement](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) à partir d’un [système de contrôle source](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), consultez [comment toodeploy un Azure App service](../app-service-web/web-sites-deploy.md).

