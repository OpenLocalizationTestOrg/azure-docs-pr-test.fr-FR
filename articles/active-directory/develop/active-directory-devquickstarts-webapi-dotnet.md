---
title: "Bien démarrer avec l'API web Azure AD .NET | Microsoft Docs"
description: "Création d’une API web MVC .NET qui s’intègre à Azure AD pour l’authentification et l’autorisation."
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
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="6df1d-103">Protégez une API web à l’aide de jetons du porteur à partir d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="6df1d-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="6df1d-104">Si vous créez une application qui fournit un accès aux ressources protégées, vous devez savoir comment éviter un accès non autorisé à ces ressources.</span><span class="sxs-lookup"><span data-stu-id="6df1d-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="6df1d-105">Azure Active Directory (Azure AD) facilite la protection d’une API web à l’aide de jetons d’accès du porteur OAuth Bearer 2.0 avec seulement quelques lignes de code.</span><span class="sxs-lookup"><span data-stu-id="6df1d-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="6df1d-106">Dans les applications web ASP.NET, vous pouvez y parvenir en utilisant l’implémentation Microsoft de l’intergiciel communautaire OWIN inclus dans .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="6df1d-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="6df1d-107">Ici, nous allons utiliser OWIN pour créer une API web « Liste des tâches » qui effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="6df1d-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="6df1d-108">Désigne les API qui sont protégées.</span><span class="sxs-lookup"><span data-stu-id="6df1d-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="6df1d-109">Valide le fait que les appels d’API web contiennent un jeton d’accès valide.</span><span class="sxs-lookup"><span data-stu-id="6df1d-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="6df1d-110">Pour générer l’API To Do List, vous devez d’abord exécuter les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="6df1d-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="6df1d-111">inscrivez une application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="6df1d-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="6df1d-112">configurez l’application pour utiliser le pipeline d’authentification OWIN ;</span><span class="sxs-lookup"><span data-stu-id="6df1d-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="6df1d-113">configurez une application cliente pour appeler l’API web.</span><span class="sxs-lookup"><span data-stu-id="6df1d-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="6df1d-114">Pour commencer, téléchargez [la structure de l’application](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) ou [l’exemple terminé](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="6df1d-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="6df1d-115">Chaque option est une solution Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6df1d-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="6df1d-116">Vous aurez également besoin d’un locataire Azure AD dans lequel inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="6df1d-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="6df1d-117">Si ce n’est pas déjà fait, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="6df1d-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="6df1d-118">Étape 1 : Inscrire une application auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="6df1d-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="6df1d-119">Pour sécuriser votre application, vous devez tout d’abord créer une application dans votre locataire et fournir quelques informations essentielles à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6df1d-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="6df1d-120">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6df1d-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="6df1d-121">Dans la barre supérieure, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="6df1d-121">On the top bar, click your account.</span></span> <span data-ttu-id="6df1d-122">Dans la liste **Répertoire**, choisissez le locataire Azure AD auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="6df1d-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="6df1d-123">Dans le volet gauche, cliquez sur **Plus de services**, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6df1d-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="6df1d-124">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6df1d-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="6df1d-125">Suivez les invites et créez une **application web et/ou un API web**.</span><span class="sxs-lookup"><span data-stu-id="6df1d-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="6df1d-126">**Nom** décrit votre application pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6df1d-126">**Name** describes your application to users.</span></span> <span data-ttu-id="6df1d-127">Entrez **To Do List Service**.</span><span class="sxs-lookup"><span data-stu-id="6df1d-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="6df1d-128">**URI de redirection** est une combinaison de schémas et de chaînes qu’Azure AD utilise pour renvoyer les jetons demandés par l’application.</span><span class="sxs-lookup"><span data-stu-id="6df1d-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="6df1d-129">Entrez `https://localhost:44321/` pour cette valeur.</span><span class="sxs-lookup"><span data-stu-id="6df1d-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="6df1d-130">À partir de la page **Paramètres** -> **Propriétés** de votre application, mettez à jour l’URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="6df1d-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="6df1d-131">Entrez un identificateur propre au locataire.</span><span class="sxs-lookup"><span data-stu-id="6df1d-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="6df1d-132">Par exemple, entrez : `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="6df1d-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="6df1d-133">Enregistrez la configuration.</span><span class="sxs-lookup"><span data-stu-id="6df1d-133">Save the configuration.</span></span> <span data-ttu-id="6df1d-134">Laissez le portail ouvert, car vous devrez également bientôt inscrire votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="6df1d-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="6df1d-135">Étape 2 : Configurer l’application pour utiliser le pipeline d’authentification OWIN</span><span class="sxs-lookup"><span data-stu-id="6df1d-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="6df1d-136">Pour valider des demandes entrantes et des jetons, vous devez configurer votre application pour communiquer avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6df1d-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="6df1d-137">Pour commencer, ouvrez la solution et ajoutez les packages NuGet de l’intergiciel OWIN au projet TodoListService à l’aide de la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="6df1d-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="6df1d-138">Ajoutez une classe de démarrage OWIN au projet TodoListService appelé `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="6df1d-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="6df1d-139">Cliquez avec le bouton droit sur le projet, sélectionnez **Ajouter** > **Nouvel élément**, puis recherchez **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="6df1d-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="6df1d-140">L’intergiciel OWIN appelle la méthode `Configuration(…)` lorsque votre application démarre.</span><span class="sxs-lookup"><span data-stu-id="6df1d-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="6df1d-141">Remplacez la déclaration de classe par `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="6df1d-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="6df1d-142">Nous avons déjà mis en œuvre une partie de cette classe dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="6df1d-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="6df1d-143">Dans la méthode `Configuration(…)`, appelez `ConfgureAuth(…)` pour configurer l’authentification à votre application web.</span><span class="sxs-lookup"><span data-stu-id="6df1d-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="6df1d-144">Ouvrez le fichier `App_Start\Startup.Auth.cs` et implémentez la méthode `ConfigureAuth(…)`.</span><span class="sxs-lookup"><span data-stu-id="6df1d-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="6df1d-145">Les paramètres que vous fournissez dans `WindowsAzureActiveDirectoryBearerAuthenticationOptions` serviront de coordonnées pour que votre application puisse communiquer avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6df1d-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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

5. <span data-ttu-id="6df1d-146">Vous pouvez désormais utiliser les attributs `[Authorize]` pour protéger vos contrôleurs et vos actions avec l’authentification de porteur JWT (JSON Web Token).</span><span class="sxs-lookup"><span data-stu-id="6df1d-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="6df1d-147">Décorez la classe `Controllers\TodoListController.cs` avec une balise authorize.</span><span class="sxs-lookup"><span data-stu-id="6df1d-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="6df1d-148">Cela force l’utilisateur à se connecter avant d’accéder à cette page.</span><span class="sxs-lookup"><span data-stu-id="6df1d-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="6df1d-149">Lorsqu’un appelant autorisé appelle correctement l’une des API `TodoListController` , l’action peut avoir besoin d’accéder aux informations sur l’appelant.</span><span class="sxs-lookup"><span data-stu-id="6df1d-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="6df1d-150">OWIN fournit l’accès aux revendications dans le jeton porteur via l’objet `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="6df1d-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="6df1d-151">Une exigence courante pour les API web consiste à valider les « étendues » présentes dans le jeton.</span><span class="sxs-lookup"><span data-stu-id="6df1d-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="6df1d-152">Cela garantit que l’utilisateur a donné son consentement pour les autorisations nécessaires pour accéder au To Do List Service.</span><span class="sxs-lookup"><span data-stu-id="6df1d-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="6df1d-153">Ouvrez le fichier `web.config` dans la racine du projet ToDoListService, puis entrez les valeurs de configuration dans la section `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="6df1d-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="6df1d-154">`ida:Tenant` est le nom de votre locataire Azure AD, par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6df1d-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="6df1d-155">`ida:Audience` est l’URI ID d’application que vous avez entré dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6df1d-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="6df1d-156">Étape 3 : Configurer une application cliente et exécuter le service</span><span class="sxs-lookup"><span data-stu-id="6df1d-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="6df1d-157">Avant de pouvoir voir le service Todo List en action, vous devez configurer le client Todo List afin qu’il puisse obtenir des jetons d’Azure AD et appeler le service.</span><span class="sxs-lookup"><span data-stu-id="6df1d-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="6df1d-158">Revenez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6df1d-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="6df1d-159">Créez une application dans votre client Azure AD, puis sélectionnez **Application cliente native** dans l’invite qui en résulte.</span><span class="sxs-lookup"><span data-stu-id="6df1d-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="6df1d-160">**Nom** décrit votre application pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6df1d-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="6df1d-161">Pour **l’URI de redirection**, entrez `http://TodoListClient/`.</span><span class="sxs-lookup"><span data-stu-id="6df1d-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="6df1d-162">Une fois l’inscription terminée, Azure AD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="6df1d-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="6df1d-163">Copiez cette valeur à partir de la page de l’application, car vous en aurez besoin dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="6df1d-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="6df1d-164">Dans la page **Paramètres**, sélectionnez **Autorisations requises**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6df1d-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="6df1d-165">Recherchez et sélectionnez le service To Do List, ajoutez l’autorisation **d’accès à TodoListService** sous **Autorisations déléguées**, puis cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="6df1d-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="6df1d-166">Dans Visual Studio, ouvrez `App.config` dans le projet TodoListClient, puis entrez les valeurs de votre configuration dans la section `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="6df1d-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="6df1d-167">`ida:Tenant` est le nom de votre locataire Azure AD, par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6df1d-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="6df1d-168">`ida:ClientId` est l’ID d’application que vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6df1d-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="6df1d-169">`todo:TodoListResourceId` est l’URI ID d’application de l’application To Do List Service que vous avez entré dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6df1d-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6df1d-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6df1d-170">Next steps</span></span>
<span data-ttu-id="6df1d-171">Enfin, nettoyez, générez et exécutez chaque projet.</span><span class="sxs-lookup"><span data-stu-id="6df1d-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="6df1d-172">Si vous ne l’avez pas encore fait, il est temps de créer un nouvel utilisateur dans votre client, avec un domaine *.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6df1d-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="6df1d-173">Connectez-vous au locataire To Do List avec cet utilisateur et ajoutez quelques tâches à la liste des tâches de cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6df1d-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="6df1d-174">Pour référence, l’exemple terminé (sans vos valeurs de configuration) est disponible dans [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="6df1d-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="6df1d-175">Vous pouvez à présent aborder d’autres scénarios d’identité.</span><span class="sxs-lookup"><span data-stu-id="6df1d-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
