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
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="e10f4-103">Protégez une API web à l’aide de jetons du porteur à partir d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="e10f4-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="e10f4-104">Si vous créez une application qui fournit l’accès tooprotected ressources, vous devez tooknow comment accéder à des ressources de toothose tooprevent injustifiée.</span><span class="sxs-lookup"><span data-stu-id="e10f4-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="e10f4-105">Azure Active Directory (Azure AD) simplifie et simple toohelp protéger une API web à l’aide des jetons d’accès OAuth 2.0 support avec seulement quelques lignes de code.</span><span class="sxs-lookup"><span data-stu-id="e10f4-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="e10f4-106">Dans les applications web ASP.NET, vous pouvez accomplir cette protection à l’aide d’implémentation de Microsoft hello de hello communautaire OWIN intergiciel (middleware) inclus dans le .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e10f4-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="e10f4-107">Ici, nous allons utiliser OWIN toobuild une API web de « tooDo liste » qui :</span><span class="sxs-lookup"><span data-stu-id="e10f4-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="e10f4-108">Désigne les API qui sont protégées.</span><span class="sxs-lookup"><span data-stu-id="e10f4-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="e10f4-109">Valide que les appels d’API web hello contient un jeton d’accès valide.</span><span class="sxs-lookup"><span data-stu-id="e10f4-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="e10f4-110">tooDo de hello toobuild API de liste, vous devez d’abord :</span><span class="sxs-lookup"><span data-stu-id="e10f4-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="e10f4-111">inscrivez une application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="e10f4-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="e10f4-112">Configurer le pipeline de hello application toouse hello OWIN d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e10f4-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="e10f4-113">Configurer un client application toocall hello API web.</span><span class="sxs-lookup"><span data-stu-id="e10f4-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="e10f4-114">tooget démarré, [télécharger squelette d’application hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e10f4-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="e10f4-115">Chaque option est une solution Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="e10f4-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="e10f4-116">Vous devez également un locataire Azure AD dans le tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="e10f4-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="e10f4-117">Si vous n’avez pas déjà, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e10f4-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="e10f4-118">Étape 1 : Inscrire une application auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="e10f4-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="e10f4-119">toohelp sécuriser votre application, vous devez toocreate une application dans votre client et fournissez quelques informations essentielles à Azure AD le.</span><span class="sxs-lookup"><span data-stu-id="e10f4-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="e10f4-120">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e10f4-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e10f4-121">Sur la barre supérieure de hello, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="e10f4-121">On hello top bar, click your account.</span></span> <span data-ttu-id="e10f4-122">Bonjour **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="e10f4-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="e10f4-123">Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e10f4-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="e10f4-124">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e10f4-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="e10f4-125">Suivez les invites hello et créer un nouveau **Application Web et/ou API Web**.</span><span class="sxs-lookup"><span data-stu-id="e10f4-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="e10f4-126">**Nom** décrit toousers de votre application.</span><span class="sxs-lookup"><span data-stu-id="e10f4-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="e10f4-127">Entrez **tooDo Service de liste**.</span><span class="sxs-lookup"><span data-stu-id="e10f4-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="e10f4-128">**Uri de redirection** est une combinaison de schéma et de chaîne Azure AD utilise tooreturn les jetons que votre application a demandé.</span><span class="sxs-lookup"><span data-stu-id="e10f4-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="e10f4-129">Entrez `https://localhost:44321/` pour cette valeur.</span><span class="sxs-lookup"><span data-stu-id="e10f4-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="e10f4-130">À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="e10f4-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="e10f4-131">Entrez un identificateur propre au locataire.</span><span class="sxs-lookup"><span data-stu-id="e10f4-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="e10f4-132">Par exemple, entrez : `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="e10f4-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="e10f4-133">Enregistrer la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="e10f4-133">Save hello configuration.</span></span> <span data-ttu-id="e10f4-134">Laissez portal de hello ouvert, car vous devez également tooregister votre application cliente dans quelques instants.</span><span class="sxs-lookup"><span data-stu-id="e10f4-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="e10f4-135">Étape 2 : Configurer de pipeline de hello application toouse hello OWIN d’authentification</span><span class="sxs-lookup"><span data-stu-id="e10f4-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="e10f4-136">toovalidate les demandes entrantes et les jetons, vous avez besoin tooset toocommunicate de votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e10f4-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="e10f4-137">toobegin, ouvrez hello solution et ajouter projet TodoListService de hello OWIN intergiciel (middleware) NuGet packages toohello à l’aide de hello Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="e10f4-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="e10f4-138">Ajouter un projet de démarrage OWIN la TodoListService de toohello de la classe appelé `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="e10f4-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="e10f4-139">Projet de hello avec le bouton droit, sélectionnez **ajouter** > **un nouvel élément**, puis recherchez **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="e10f4-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="e10f4-140">intergiciel (middleware) OWIN de Hello appellera hello `Configuration(…)` méthode au démarrage de votre application.</span><span class="sxs-lookup"><span data-stu-id="e10f4-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="e10f4-141">Modifier trop de déclaration de classe hello`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="e10f4-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="e10f4-142">Nous avons déjà mis en œuvre une partie de cette classe dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="e10f4-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="e10f4-143">Bonjour `Configuration(…)` (méthode), effectuer un appel trop`ConfgureAuth(…)` tooset l’authentification pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="e10f4-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="e10f4-144">Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et implémenter hello `ConfigureAuth(…)` (méthode).</span><span class="sxs-lookup"><span data-stu-id="e10f4-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="e10f4-145">Hello les paramètres que vous fournissez dans `WindowsAzureActiveDirectoryBearerAuthenticationOptions` servira de coordonnées pour toocommunicate de votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e10f4-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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

5. <span data-ttu-id="e10f4-146">Vous pouvez désormais utiliser `[Authorize]` attributs toohelp protéger vos contrôleurs et vos actions avec l’authentification du support JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="e10f4-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="e10f4-147">Décorer hello `Controllers\TodoListController.cs` classe avec une balise authorize.</span><span class="sxs-lookup"><span data-stu-id="e10f4-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="e10f4-148">Cela obligera toosign d’utilisateur hello dans avant d’accéder à cette page.</span><span class="sxs-lookup"><span data-stu-id="e10f4-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="e10f4-149">Quand un appelant autorisé correctement appelle l’une des hello `TodoListController` API, action de hello peut-être besoin d’accès tooinformation sur l’appelant de hello.</span><span class="sxs-lookup"><span data-stu-id="e10f4-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="e10f4-150">OWIN fournit des revendications toohello d’accès à l’intérieur du jeton de support hello via hello `ClaimsPrincpal` objet.</span><span class="sxs-lookup"><span data-stu-id="e10f4-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="e10f4-151">Une exigence courante pour l’API web est toovalidate hello « étendues » présents dans le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="e10f4-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="e10f4-152">Cela garantit que l’utilisateur hello a consenti toohello autorisations requis tooaccess hello tooDo Service de liste.</span><span class="sxs-lookup"><span data-stu-id="e10f4-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

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

7. <span data-ttu-id="e10f4-153">Ouvrez hello `web.config` fichier racine hello du projet TodoListService de hello et entrez les valeurs de configuration Bonjour `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="e10f4-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="e10f4-154">`ida:Tenant`est le nom hello de votre client Azure AD--par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e10f4-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="e10f4-155">`ida:Audience`est hello URI ID d’application de l’application hello que vous avez entré dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e10f4-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="e10f4-156">Étape 3 : Configurer une application cliente et exécuter le service de hello</span><span class="sxs-lookup"><span data-stu-id="e10f4-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="e10f4-157">Avant de pouvoir afficher hello tooDo Service de liste en action, vous devez client de liste tooconfigure hello tooDo afin de pouvoir obtenir des jetons d’Azure AD et que les appels toohello service.</span><span class="sxs-lookup"><span data-stu-id="e10f4-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="e10f4-158">Revenir en arrière toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e10f4-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e10f4-159">Créer une nouvelle application dans votre locataire Azure AD, puis sélectionnez **Application cliente Native** dans invite résultant de hello.</span><span class="sxs-lookup"><span data-stu-id="e10f4-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="e10f4-160">**Nom** décrit toousers de votre application.</span><span class="sxs-lookup"><span data-stu-id="e10f4-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="e10f4-161">Entrez `http://TodoListClient/` pour hello **Uri de redirection** valeur.</span><span class="sxs-lookup"><span data-stu-id="e10f4-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="e10f4-162">Une fois que vous avez terminé l’inscription, Azure AD assigne une application de tooyour ID unique d’application.</span><span class="sxs-lookup"><span data-stu-id="e10f4-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="e10f4-163">Vous aurez besoin de cette valeur dans les étapes suivantes hello, par conséquent, copiez-le à partir de la page de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e10f4-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="e10f4-164">À partir de hello **paramètres** page, sélectionnez **autorisations requises**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e10f4-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="e10f4-165">Recherchez et sélectionnez hello tooDo Service de liste, ajouter hello **accès TodoListService** autorisation sous **autorisations déléguées**, puis cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="e10f4-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="e10f4-166">Dans Visual Studio, ouvrez `App.config` dans hello TodoListClient projet, puis entrez les valeurs de configuration Bonjour `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="e10f4-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="e10f4-167">`ida:Tenant`est le nom hello de votre client Azure AD--par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e10f4-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="e10f4-168">`ida:ClientId`est l’ID de l’application hello que vous avez copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e10f4-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="e10f4-169">`todo:TodoListResourceId`est hello URI ID d’application de hello tooDo application de Service de liste que vous avez entré dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e10f4-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e10f4-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e10f4-170">Next steps</span></span>
<span data-ttu-id="e10f4-171">Enfin, nettoyez, générez et exécutez chaque projet.</span><span class="sxs-lookup"><span data-stu-id="e10f4-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="e10f4-172">Si vous n’avez pas encore, est désormais hello temps toocreate un nouvel utilisateur dans votre client avec un *. onmicrosoft.com domaine.</span><span class="sxs-lookup"><span data-stu-id="e10f4-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="e10f4-173">Connectez-vous au client de liste toohello tooDo avec cet utilisateur et ajouter la liste des tâches de l’utilisateur toohello de certaines tâches.</span><span class="sxs-lookup"><span data-stu-id="e10f4-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="e10f4-174">Pour référence, l’exemple hello terminée (sans les valeurs de configuration) est disponible dans [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e10f4-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="e10f4-175">Vous pouvez maintenant déplacer sur les scénarios d’identité toomore.</span><span class="sxs-lookup"><span data-stu-id="e10f4-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
