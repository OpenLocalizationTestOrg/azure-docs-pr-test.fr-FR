---
title: aaaAzure AD .NET web API prise en main | Documents Microsoft
description: "Comment toobuild une API web de .NET MVC qui s’intègre à Azure AD pour l’authentification et d’autorisation."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>Protégez une API web à l’aide de jetons du porteur à partir d’Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Si vous créez une application qui fournit l’accès tooprotected ressources, vous devez tooknow comment accéder à des ressources de toothose tooprevent injustifiée.
Azure Active Directory (Azure AD) simplifie et simple toohelp protéger une API web à l’aide des jetons d’accès OAuth 2.0 support avec seulement quelques lignes de code.

Dans les applications web ASP.NET, vous pouvez accomplir cette protection à l’aide d’implémentation de Microsoft hello de hello communautaire OWIN intergiciel (middleware) inclus dans le .NET Framework 4.5. Ici, nous allons utiliser OWIN toobuild une API web de « tooDo liste » qui :

* Désigne les API qui sont protégées.
* Valide que les appels d’API web hello contient un jeton d’accès valide.

tooDo de hello toobuild API de liste, vous devez d’abord :

1. inscrivez une application auprès d’Azure AD ;
2. Configurer le pipeline de hello application toouse hello OWIN d’authentification.
3. Configurer un client application toocall hello API web.

tooget démarré, [télécharger squelette d’application hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Chaque option est une solution Visual Studio 2013. Vous devez également un locataire Azure AD dans le tooregister votre application. Si vous n’avez pas déjà, [apprendre comment tooget un](active-directory-howto-tenant.md).

## <a name="step-1-register-an-application-with-azure-ad"></a>Étape 1 : Inscrire une application auprès d’Azure AD
toohelp sécuriser votre application, vous devez toocreate une application dans votre client et fournissez quelques informations essentielles à Azure AD le.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Sur la barre supérieure de hello, cliquez sur votre compte. Bonjour **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.

3. Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.

4. Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.

5. Suivez les invites hello et créer un nouveau **Application Web et/ou API Web**.
  * **Nom** décrit toousers de votre application. Entrez **tooDo Service de liste**.
  * **Uri de redirection** est une combinaison de schéma et de chaîne Azure AD utilise tooreturn les jetons que votre application a demandé. Entrez `https://localhost:44321/` pour cette valeur.

6. À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application. Entrez un identificateur propre au locataire. Par exemple, entrez : `https://contoso.onmicrosoft.com/TodoListService`.

7. Enregistrer la configuration de hello. Laissez portal de hello ouvert, car vous devez également tooregister votre application cliente dans quelques instants.

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Étape 2 : Configurer de pipeline de hello application toouse hello OWIN d’authentification
toovalidate les demandes entrantes et les jetons, vous avez besoin tooset toocommunicate de votre application auprès d’Azure AD.

1. toobegin, ouvrez hello solution et ajouter projet TodoListService de hello OWIN intergiciel (middleware) NuGet packages toohello à l’aide de hello Console du Gestionnaire de Package.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Ajouter un projet de démarrage OWIN la TodoListService de toohello de la classe appelé `Startup.cs`.  Projet de hello avec le bouton droit, sélectionnez **ajouter** > **un nouvel élément**, puis recherchez **OWIN**. intergiciel (middleware) OWIN de Hello appellera hello `Configuration(…)` méthode au démarrage de votre application.

3. Modifier trop de déclaration de classe hello`public partial class Startup`. Nous avons déjà mis en œuvre une partie de cette classe dans un autre fichier. Bonjour `Configuration(…)` (méthode), effectuer un appel trop`ConfgureAuth(…)` tooset l’authentification pour votre application web.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et implémenter hello `ConfigureAuth(…)` (méthode). Hello les paramètres que vous fournissez dans `WindowsAzureActiveDirectoryBearerAuthenticationOptions` servira de coordonnées pour toocommunicate de votre application auprès d’Azure AD.

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. Vous pouvez désormais utiliser `[Authorize]` attributs toohelp protéger vos contrôleurs et vos actions avec l’authentification du support JSON Web Token (JWT). Décorer hello `Controllers\TodoListController.cs` classe avec une balise authorize. Cela obligera toosign d’utilisateur hello dans avant d’accéder à cette page.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    Quand un appelant autorisé correctement appelle l’une des hello `TodoListController` API, action de hello peut-être besoin d’accès tooinformation sur l’appelant de hello. OWIN fournit des revendications toohello d’accès à l’intérieur du jeton de support hello via hello `ClaimsPrincpal` objet.  

6. Une exigence courante pour l’API web est toovalidate hello « étendues » présents dans le jeton de hello. Cela garantit que l’utilisateur hello a consenti toohello autorisations requis tooaccess hello tooDo Service de liste.

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. Ouvrez hello `web.config` fichier racine hello du projet TodoListService de hello et entrez les valeurs de configuration Bonjour `<appSettings>` section.
  * `ida:Tenant`est le nom hello de votre client Azure AD--par exemple, contoso.onmicrosoft.com.
  * `ida:Audience`est hello URI ID d’application de l’application hello que vous avez entré dans hello portail Azure.

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>Étape 3 : Configurer une application cliente et exécuter le service de hello
Avant de pouvoir afficher hello tooDo Service de liste en action, vous devez client de liste tooconfigure hello tooDo afin de pouvoir obtenir des jetons d’Azure AD et que les appels toohello service.

1. Revenir en arrière toohello [portail Azure](https://portal.azure.com).

2. Créer une nouvelle application dans votre locataire Azure AD, puis sélectionnez **Application cliente Native** dans invite résultant de hello.
  * **Nom** décrit toousers de votre application.
  * Entrez `http://TodoListClient/` pour hello **Uri de redirection** valeur.

3. Une fois que vous avez terminé l’inscription, Azure AD assigne une application de tooyour ID unique d’application. Vous aurez besoin de cette valeur dans les étapes suivantes hello, par conséquent, copiez-le à partir de la page de l’application hello.

4. À partir de hello **paramètres** page, sélectionnez **autorisations requises**, puis sélectionnez **ajouter**. Recherchez et sélectionnez hello tooDo Service de liste, ajouter hello **accès TodoListService** autorisation sous **autorisations déléguées**, puis cliquez sur **fait**.

5. Dans Visual Studio, ouvrez `App.config` dans hello TodoListClient projet, puis entrez les valeurs de configuration Bonjour `<appSettings>` section.

  * `ida:Tenant`est le nom hello de votre client Azure AD--par exemple, contoso.onmicrosoft.com.
  * `ida:ClientId`est l’ID de l’application hello que vous avez copié à partir de hello portail Azure.
  * `todo:TodoListResourceId`est hello URI ID d’application de hello tooDo application de Service de liste que vous avez entré dans hello portail Azure.

## <a name="next-steps"></a>Étapes suivantes
Enfin, nettoyez, générez et exécutez chaque projet. Si vous n’avez pas encore, est désormais hello temps toocreate un nouvel utilisateur dans votre client avec un *. onmicrosoft.com domaine. Connectez-vous au client de liste toohello tooDo avec cet utilisateur et ajouter la liste des tâches de l’utilisateur toohello de certaines tâches.

Pour référence, l’exemple hello terminée (sans les valeurs de configuration) est disponible dans [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Vous pouvez maintenant déplacer sur les scénarios d’identité toomore.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
