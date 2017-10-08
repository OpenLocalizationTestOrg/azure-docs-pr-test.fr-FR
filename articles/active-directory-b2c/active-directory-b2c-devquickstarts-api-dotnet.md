---
title: aaaAzure AD B2C | Documents Microsoft
description: "Comment toobuild une API Web de .NET à l’aide de B2C d’Active Directory Azure, sécurisés à l’aide des jetons d’accès OAuth 2.0 pour l’authentification."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="627c8-103">Azure Active Directory B2C : générer une API web .NET</span><span class="sxs-lookup"><span data-stu-id="627c8-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="627c8-104">Avec Azure Active Directory (Azure AD) B2C, vous pouvez sécuriser une API web à l’aide de jetons d’accès OAuth 2.0,</span><span class="sxs-lookup"><span data-stu-id="627c8-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="627c8-105">Ces jetons permettent à votre client applications tooauthenticate toohello API.</span><span class="sxs-lookup"><span data-stu-id="627c8-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="627c8-106">Cet article explique comment toocreate une API de la « liste de tâches » MVC .NET qui permet aux utilisateurs de votre client de tâches tooCRUD de l’application.</span><span class="sxs-lookup"><span data-stu-id="627c8-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="627c8-107">Hello web API est sécurisé à l’aide d’Azure AD B2C et autorise uniquement les utilisateurs authentifiés toomanage leur liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="627c8-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="627c8-108">Créer un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="627c8-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="627c8-109">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="627c8-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="627c8-110">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc.</span><span class="sxs-lookup"><span data-stu-id="627c8-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="627c8-111">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant d’aller plus loin dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="627c8-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="627c8-112">application cliente de Hello et API web doivent utiliser Active de B2C hello même instance Azure AD.</span><span class="sxs-lookup"><span data-stu-id="627c8-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="627c8-113">Créer une API Web</span><span class="sxs-lookup"><span data-stu-id="627c8-113">Create a web API</span></span>

<span data-ttu-id="627c8-114">Ensuite, vous devez toocreate une application d’API web dans votre répertoire B2C.</span><span class="sxs-lookup"><span data-stu-id="627c8-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="627c8-115">Cela fournit des informations AD Azure qu’il a besoin toosecurely communiquer avec votre application.</span><span class="sxs-lookup"><span data-stu-id="627c8-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="627c8-116">toocreate une application, procédez comme [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="627c8-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="627c8-117">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="627c8-117">Be sure to:</span></span>

* <span data-ttu-id="627c8-118">Inclure un **application web** ou **web API** dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="627c8-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="627c8-119">Hello d’utilisation **URI de redirection** `https://localhost:44332/` pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="627c8-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="627c8-120">Il s’agit d’emplacement par défaut de hello du client de l’application web hello pour cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="627c8-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="627c8-121">Hello de copie **ID d’Application** qui est attribué tooyour application.</span><span class="sxs-lookup"><span data-stu-id="627c8-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="627c8-122">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="627c8-122">You'll need it later.</span></span>
* <span data-ttu-id="627c8-123">Entrez un identificateur d’application dans **l’URI d’ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="627c8-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="627c8-124">Ajouter des autorisations via hello **publié étendues** menu.</span><span class="sxs-lookup"><span data-stu-id="627c8-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="627c8-125">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="627c8-125">Create your policies</span></span>

<span data-ttu-id="627c8-126">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="627c8-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="627c8-127">Vous devez toocreate un toocommunicate de stratégie avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="627c8-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="627c8-128">Nous recommandons à l’aide de hello combinées de stratégie de connexion-haut/connectez-vous, comme décrit dans hello [article de référence de stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="627c8-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="627c8-129">Lorsque vous créez la stratégie, prenez soin de :</span><span class="sxs-lookup"><span data-stu-id="627c8-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="627c8-130">Choisir un **Nom d’affichage** et d’autres attributs d’inscription dans votre stratégie.</span><span class="sxs-lookup"><span data-stu-id="627c8-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="627c8-131">Choisir les revendications **Nom d’affichage** et **ID d’objet** comme revendications d’application pour chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="627c8-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="627c8-132">Vous pouvez aussi choisir d'autres revendications.</span><span class="sxs-lookup"><span data-stu-id="627c8-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="627c8-133">Hello de copie **nom** de chaque stratégie après l’avoir créée.</span><span class="sxs-lookup"><span data-stu-id="627c8-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="627c8-134">Vous aurez besoin nom de la stratégie hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="627c8-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="627c8-135">Une fois que vous avez créé la stratégie de hello, vous êtes prêt toobuild votre application.</span><span class="sxs-lookup"><span data-stu-id="627c8-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="627c8-136">Télécharger le code de hello</span><span class="sxs-lookup"><span data-stu-id="627c8-136">Download hello code</span></span>

<span data-ttu-id="627c8-137">code Hello pour ce didacticiel est conservée sur [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="627c8-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="627c8-138">Vous pouvez cloner l’exemple hello en exécutant :</span><span class="sxs-lookup"><span data-stu-id="627c8-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="627c8-139">Après avoir téléchargé l’exemple de code hello, ouvrez hello tooget du fichier .sln de Visual Studio a démarré.</span><span class="sxs-lookup"><span data-stu-id="627c8-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="627c8-140">fichier de solution Hello contient deux projets : `TaskWebApp` et `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="627c8-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="627c8-141">`TaskWebApp`est une application web MVC hello utilisateur interagit avec.</span><span class="sxs-lookup"><span data-stu-id="627c8-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="627c8-142">`TaskService`est web principal API de l’application hello qui stocke la liste des actions de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="627c8-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="627c8-143">Cet article traite uniquement hello `TaskService` application.</span><span class="sxs-lookup"><span data-stu-id="627c8-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="627c8-144">toolearn comment toobuild `TaskWebApp` à l’aide d’Azure AD B2C, consultez [notre didacticiel d’application web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="627c8-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="627c8-145">Mettre à jour la configuration de hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="627c8-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="627c8-146">Notre exemple est configuré toouse hello stratégies et ID de client de notre client de démonstration.</span><span class="sxs-lookup"><span data-stu-id="627c8-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="627c8-147">Si vous souhaitez que toouse votre propre client, vous devez hello toodo suivant :</span><span class="sxs-lookup"><span data-stu-id="627c8-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="627c8-148">Ouvrez `web.config` Bonjour `TaskService` de projet et remplacer les valeurs hello pour</span><span class="sxs-lookup"><span data-stu-id="627c8-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="627c8-149">`ida:Tenant` par le nom de votre locataire</span><span class="sxs-lookup"><span data-stu-id="627c8-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="627c8-150">`ida:ClientId` avec votre ID d’application d’API web</span><span class="sxs-lookup"><span data-stu-id="627c8-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="627c8-151">`ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion</span><span class="sxs-lookup"><span data-stu-id="627c8-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="627c8-152">Ouvrez `web.config` Bonjour `TaskWebApp` de projet et remplacer les valeurs hello pour</span><span class="sxs-lookup"><span data-stu-id="627c8-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="627c8-153">`ida:Tenant` par le nom de votre locataire</span><span class="sxs-lookup"><span data-stu-id="627c8-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="627c8-154">`ida:ClientId` par votre ID d’application web</span><span class="sxs-lookup"><span data-stu-id="627c8-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="627c8-155">`ida:ClientSecret` par votre clé secrète d’application web</span><span class="sxs-lookup"><span data-stu-id="627c8-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="627c8-156">`ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion</span><span class="sxs-lookup"><span data-stu-id="627c8-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="627c8-157">`ida:EditProfilePolicyId` par votre nom de stratégie « Modifier le profil »</span><span class="sxs-lookup"><span data-stu-id="627c8-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="627c8-158">`ida:ResetPasswordPolicyId` par votre nom de stratégie « Réinitialiser le mot de passe »</span><span class="sxs-lookup"><span data-stu-id="627c8-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="627c8-159">Sécuriser les API hello</span><span class="sxs-lookup"><span data-stu-id="627c8-159">Secure hello API</span></span>

<span data-ttu-id="627c8-160">Lorsque l’un de vos clients appelle votre API, vous pouvez la sécuriser (par exemple, `TaskService`) à l’aide de jetons du porteur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="627c8-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="627c8-161">Cela garantit que chaque API de tooyour demande sera uniquement valide si la demande de hello possède un jeton de support.</span><span class="sxs-lookup"><span data-stu-id="627c8-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="627c8-162">Votre API peut accepter et valider les jetons du porteur à l’aide de la bibliothèque OWIN (Open Web Interface for .NET) de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="627c8-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="627c8-163">Installer OWIN</span><span class="sxs-lookup"><span data-stu-id="627c8-163">Install OWIN</span></span>

<span data-ttu-id="627c8-164">Commencez par installer un pipeline de l’authentification OWIN OAuth hello à l’aide de hello Console du Gestionnaire de Package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="627c8-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="627c8-165">Ceci installe hello OWIN intergiciel (middleware) qui accepte et valide les jetons de support.</span><span class="sxs-lookup"><span data-stu-id="627c8-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="627c8-166">Ajouter une classe de démarrage OWIN</span><span class="sxs-lookup"><span data-stu-id="627c8-166">Add an OWIN startup class</span></span>

<span data-ttu-id="627c8-167">Ajouter un toohello de classe de démarrage OWIN API appelée `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="627c8-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="627c8-168">Avec le bouton droit sur le projet hello, sélectionnez **ajouter** et **un nouvel élément**, puis recherchez OWIN.</span><span class="sxs-lookup"><span data-stu-id="627c8-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="627c8-169">intergiciel (middleware) OWIN de Hello appellera hello `Configuration(…)` méthode au démarrage de votre application.</span><span class="sxs-lookup"><span data-stu-id="627c8-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="627c8-170">Dans notre exemple, nous avons modifié trop déclaration de classe hello`public partial class Startup` et implémenté hello autre partie de la classe hello dans `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="627c8-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="627c8-171">À l’intérieur hello `Configuration` (méthode), nous avons ajouté un appel trop`ConfigureAuth`, qui est défini dans `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="627c8-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="627c8-172">Après modification de hello, `Startup.cs` ressemble à hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="627c8-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="627c8-173">Configurer l’authentification OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="627c8-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="627c8-174">Les fichiers ouverts hello `App_Start\Startup.Auth.cs`et mettre en œuvre hello `ConfigureAuth(...)` (méthode).</span><span class="sxs-lookup"><span data-stu-id="627c8-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="627c8-175">Par exemple, il peut se présenter comme hello ci-après :</span><span class="sxs-lookup"><span data-stu-id="627c8-175">For example, it could look like hello following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="627c8-176">Contrôleur de tâche hello sécurisé</span><span class="sxs-lookup"><span data-stu-id="627c8-176">Secure hello task controller</span></span>

<span data-ttu-id="627c8-177">Une fois l’application hello l’authentification configurée toouse OAuth 2.0, vous pouvez sécuriser votre API web en ajoutant un `[Authorize]` contrôleur de tâche toohello de balise.</span><span class="sxs-lookup"><span data-stu-id="627c8-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="627c8-178">Il s’agit de contrôleur hello où toutes les manipulations de liste de tâches a lieu, donc vous devez sécuriser le contrôleur d’entier hello au niveau de la classe hello.</span><span class="sxs-lookup"><span data-stu-id="627c8-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="627c8-179">Vous pouvez également ajouter hello `[Authorize]` tooindividual des actions pour un contrôle plus précis de la balise.</span><span class="sxs-lookup"><span data-stu-id="627c8-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="627c8-180">Obtenir des informations sur l’utilisateur à partir de hello jeton</span><span class="sxs-lookup"><span data-stu-id="627c8-180">Get user information from hello token</span></span>

<span data-ttu-id="627c8-181">`TasksController`stocke les tâches dans une base de données où chaque tâche a un utilisateur associé qui « possède » la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="627c8-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="627c8-182">propriétaire de Hello est identifié par l’utilisateur hello **ID d’objet**.</span><span class="sxs-lookup"><span data-stu-id="627c8-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="627c8-183">(C’est pourquoi vous avez besoin d’ID d’objet tooadd hello en tant qu’application par toutes les stratégies de votre demande.)</span><span class="sxs-lookup"><span data-stu-id="627c8-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="627c8-184">Valider les autorisations hello dans le jeton de hello</span><span class="sxs-lookup"><span data-stu-id="627c8-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="627c8-185">Une exigence courante pour l’API web est toovalidate hello « étendues » présents dans le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="627c8-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="627c8-186">Cela garantit que l’utilisateur hello a consenti service de liste de tâches toohello autorisations requis tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="627c8-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="627c8-187">Exécutez l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="627c8-187">Run hello sample app</span></span>

<span data-ttu-id="627c8-188">Pour finir, générez et exécutez `TaskWebApp` et `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="627c8-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="627c8-189">Créer des tâches sur la liste des tâches de l’utilisateur hello et notez comment elles sont conservées dans hello API même après l’arrêt et redémarrez hello client.</span><span class="sxs-lookup"><span data-stu-id="627c8-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="627c8-190">Modifier vos stratégies</span><span class="sxs-lookup"><span data-stu-id="627c8-190">Edit your policies</span></span>

<span data-ttu-id="627c8-191">Une fois que vous avez sécurisé une API à l’aide d’Azure AD B2C, vous pouvez tester votre stratégie de connexion-dans/connexion-haut et afficher les effets hello (ou son manque) sur hello API.</span><span class="sxs-lookup"><span data-stu-id="627c8-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="627c8-192">Vous pouvez manipuler les revendications d’application hello dans les stratégies de hello et modifier les informations utilisateur hello qui est disponibles dans l’API web de hello.</span><span class="sxs-lookup"><span data-stu-id="627c8-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="627c8-193">Toutes les revendications que vous ajoutez sera disponible tooyour .NET MVC web API Bonjour `ClaimsPrincipal` de l’objet, comme décrit précédemment dans cet article.</span><span class="sxs-lookup"><span data-stu-id="627c8-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
