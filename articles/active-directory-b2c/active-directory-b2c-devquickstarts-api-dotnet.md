---
title: Azure AD B2C | Microsoft Docs
description: "Comment créer une API web .NET à l’aide d’Azure Active Directory B2C et la sécuriser à l’aide des jetons d’accès OAuth 2.0 pour l’authentification,"
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
ms.openlocfilehash: 48749bfa2ab54a0e766a4aad4f39073cc4e90818
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="b2d2d-103">Azure Active Directory B2C : générer une API web .NET</span><span class="sxs-lookup"><span data-stu-id="b2d2d-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="b2d2d-104">Avec Azure Active Directory (Azure AD) B2C, vous pouvez sécuriser une API web à l’aide de jetons d’accès OAuth 2.0,</span><span class="sxs-lookup"><span data-stu-id="b2d2d-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="b2d2d-105">ce qui permet aux applications clientes de s’authentifier auprès de l’API.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="b2d2d-106">Cet article vous indique comment créer une API .NET MVC « liste de tâches » permettant aux utilisateurs de votre application cliente d’exécuter des actions de création, lecture, mise à jour et suppression (CRUD) sur les tâches.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="b2d2d-107">L’API web est sécurisée à l’aide d’Azure AD B2C et autorise uniquement les utilisateurs authentifiés à gérer leur liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="b2d2d-108">Créer un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="b2d2d-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="b2d2d-109">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="b2d2d-110">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="b2d2d-111">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant d’aller plus loin dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="b2d2d-112">L’application cliente et l’API web doivent utiliser le même répertoire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="b2d2d-113">Créer une API Web</span><span class="sxs-lookup"><span data-stu-id="b2d2d-113">Create a web API</span></span>

<span data-ttu-id="b2d2d-114">Vous devez maintenant créer dans votre répertoire B2C une application API web.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="b2d2d-115">fournissant à Azure AD certaines informations nécessaires pour communiquer de manière sécurisée avec votre application.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="b2d2d-116">Pour créer une application, suivez [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="b2d2d-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="b2d2d-117">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2d2d-117">Be sure to:</span></span>

* <span data-ttu-id="b2d2d-118">Incluez une **application web** ou une **API web** dans l’application.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="b2d2d-119">Utilisez **l’URI de redirection** `https://localhost:44332/` pour l’application web.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="b2d2d-120">Il s’agit de l’emplacement par défaut du client d’application web pour cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="b2d2d-121">Copiez l’ **ID d’application** affecté à votre application.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="b2d2d-122">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-122">You'll need it later.</span></span>
* <span data-ttu-id="b2d2d-123">Entrez un identificateur d’application dans **l’URI d’ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="b2d2d-124">Ajoutez des autorisations via le menu **Étendues publiées**.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="b2d2d-125">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="b2d2d-125">Create your policies</span></span>

<span data-ttu-id="b2d2d-126">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b2d2d-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="b2d2d-127">Vous devez créer une stratégie pour communiquer avec Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="b2d2d-128">Nous recommandons l’utilisation d’une stratégie combinée d’inscription/de connexion, comme décrit dans [l’article de référence sur les stratégies](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b2d2d-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="b2d2d-129">Lorsque vous créez la stratégie, prenez soin de :</span><span class="sxs-lookup"><span data-stu-id="b2d2d-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="b2d2d-130">Choisir un **Nom d’affichage** et d’autres attributs d’inscription dans votre stratégie.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="b2d2d-131">Choisir les revendications **Nom d’affichage** et **ID d’objet** comme revendications d’application pour chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="b2d2d-132">Vous pouvez aussi choisir d'autres revendications.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="b2d2d-133">Copiez le **nom** de chaque stratégie après sa création.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="b2d2d-134">Le nom de stratégie vous sera demandé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="b2d2d-135">Une fois votre stratégie créée, vous pouvez générer votre application.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="b2d2d-136">Téléchargement du code</span><span class="sxs-lookup"><span data-stu-id="b2d2d-136">Download the code</span></span>

<span data-ttu-id="b2d2d-137">Le code associé à ce didacticiel est stocké sur [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="b2d2d-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="b2d2d-138">Vous pouvez cloner l’exemple en exécutant :</span><span class="sxs-lookup"><span data-stu-id="b2d2d-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="b2d2d-139">Une fois l’exemple de code téléchargé, ouvrez le fichier .sln Visual Studio pour commencer.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="b2d2d-140">Le fichier solution contient deux projets : `TaskWebApp` et `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="b2d2d-141">`TaskWebApp` est une application web MVC avec laquelle l’utilisateur interagit.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="b2d2d-142">`TaskService` est l’API web du serveur principal de l’application qui stocke la liste de tâches de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="b2d2d-143">Cet article traite uniquement l’application `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="b2d2d-144">Pour savoir comment générer `TaskWebApp` à l’aide d’Azure AD B2C, consultez [notre didacticiel sur les applications web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="b2d2d-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="b2d2d-145">Mettre à jour la configuration Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="b2d2d-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="b2d2d-146">Notre exemple est configuré pour utiliser les stratégies et l’ID client du client de notre démonstration.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="b2d2d-147">Si vous souhaitez utiliser votre propre client, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b2d2d-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="b2d2d-148">Ouvrez `web.config` dans le projet `TaskService` et remplacez les valeurs de</span><span class="sxs-lookup"><span data-stu-id="b2d2d-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="b2d2d-149">`ida:Tenant` avec le nom de votre client</span><span class="sxs-lookup"><span data-stu-id="b2d2d-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="b2d2d-150">`ida:ClientId` avec votre ID d’application d’API web</span><span class="sxs-lookup"><span data-stu-id="b2d2d-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="b2d2d-151">`ida:SignUpSignInPolicyId` avec votre nom de stratégie d’inscription ou de connexion</span><span class="sxs-lookup"><span data-stu-id="b2d2d-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="b2d2d-152">Ouvrez `web.config` dans le projet `TaskWebApp` et remplacez les valeurs de</span><span class="sxs-lookup"><span data-stu-id="b2d2d-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="b2d2d-153">`ida:Tenant` par le nom de votre locataire</span><span class="sxs-lookup"><span data-stu-id="b2d2d-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="b2d2d-154">`ida:ClientId` par votre ID d’application web</span><span class="sxs-lookup"><span data-stu-id="b2d2d-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="b2d2d-155">`ida:ClientSecret` par votre clé secrète d’application web</span><span class="sxs-lookup"><span data-stu-id="b2d2d-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="b2d2d-156">`ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion</span><span class="sxs-lookup"><span data-stu-id="b2d2d-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="b2d2d-157">`ida:EditProfilePolicyId` par votre nom de stratégie « Modifier le profil »</span><span class="sxs-lookup"><span data-stu-id="b2d2d-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="b2d2d-158">`ida:ResetPasswordPolicyId`avec votre nom de stratégie « Modifier le mot de passe »</span><span class="sxs-lookup"><span data-stu-id="b2d2d-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="b2d2d-159">Sécuriser l’API</span><span class="sxs-lookup"><span data-stu-id="b2d2d-159">Secure the API</span></span>

<span data-ttu-id="b2d2d-160">Lorsque l’un de vos clients appelle votre API, vous pouvez la sécuriser (par exemple, `TaskService`) à l’aide de jetons du porteur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="b2d2d-161">Cela garantit que chaque demande à votre API n’est valide que si la demande a un jeton de support.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="b2d2d-162">Votre API peut accepter et valider les jetons du porteur à l’aide de la bibliothèque OWIN (Open Web Interface for .NET) de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="b2d2d-163">Installer OWIN</span><span class="sxs-lookup"><span data-stu-id="b2d2d-163">Install OWIN</span></span>

<span data-ttu-id="b2d2d-164">Commencez par installer le pipeline d’authentification OWIN OAuth à l’aide de la console du gestionnaire de package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="b2d2d-165">Cette opération installe l’intergiciel OWIN qui accepte et valide les jetons du porteur.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="b2d2d-166">Ajouter une classe de démarrage OWIN</span><span class="sxs-lookup"><span data-stu-id="b2d2d-166">Add an OWIN startup class</span></span>

<span data-ttu-id="b2d2d-167">Ajoutez une classe de démarrage OWIN à l’API appelée `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="b2d2d-168">Cliquez avec le bouton droit sur le projet, sélectionnez **Ajouter** et **Nouvel élément**, puis recherchez OWIN.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="b2d2d-169">L’intergiciel OWIN appelle la méthode `Configuration(…)` lorsque votre application démarre.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="b2d2d-170">Dans notre exemple, nous avons modifié la déclaration de classe sur `public partial class Startup` et implémenté l’autre partie de la classe dans `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="b2d2d-171">À l’intérieur de la méthode `Configuration`, nous avons ajouté un appel vers `ConfigureAuth`, qui est défini dans `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="b2d2d-172">Après modification, `Startup.cs` ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="b2d2d-172">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="b2d2d-173">Configurer l’authentification OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="b2d2d-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="b2d2d-174">Ouvrez le fichier `App_Start\Startup.Auth.cs` et implémentez la méthode `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="b2d2d-175">Par exemple, il peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b2d2d-175">For example, it could look like the following:</span></span>

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
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="b2d2d-176">Sécuriser le contrôleur de tâche</span><span class="sxs-lookup"><span data-stu-id="b2d2d-176">Secure the task controller</span></span>

<span data-ttu-id="b2d2d-177">Une fois que l’application est configurée pour utiliser l’authentification OAuth 2.0, vous pouvez sécuriser votre API web en ajoutant une balise `[Authorize]` au contrôleur de tâches.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="b2d2d-178">Comme il s’agit du contrôleur sur lequel toutes les manipulations de liste des tâches ont lieu, vous devez sécuriser l’ensemble du contrôleur au niveau de la classe.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="b2d2d-179">Vous pouvez également ajouter la balise `[Authorize]` à des actions individuelles afin d’obtenir un contrôle plus précis.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="b2d2d-180">Obtenir des informations utilisateur à partir du jeton</span><span class="sxs-lookup"><span data-stu-id="b2d2d-180">Get user information from the token</span></span>

<span data-ttu-id="b2d2d-181">Le `TasksController` stocke des tâches dans une base de données où chaque tâche est associée à un utilisateur « propriétaire » de la tâche.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="b2d2d-182">Le propriétaire est identifié par **l’ID objet** de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="b2d2d-183">(c’est pourquoi vous devez ajouter l’ID d’objet en tant que revendication d’application dans toutes vous stratégies).</span><span class="sxs-lookup"><span data-stu-id="b2d2d-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="b2d2d-184">Valider les autorisations dans le jeton</span><span class="sxs-lookup"><span data-stu-id="b2d2d-184">Validate the permissions in the token</span></span>

<span data-ttu-id="b2d2d-185">Une exigence courante pour les API web consiste à valider les « étendues » présentes dans le jeton.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="b2d2d-186">Cela garantit que l’utilisateur a donné son consentement pour les autorisations nécessaires pour accéder au To Do List Service.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="b2d2d-187">Exécution de l'exemple d'application</span><span class="sxs-lookup"><span data-stu-id="b2d2d-187">Run the sample app</span></span>

<span data-ttu-id="b2d2d-188">Pour finir, générez et exécutez `TaskWebApp` et `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="b2d2d-189">Créez des tâches sur la liste des tâches de l’utilisateur et notez la façon dont elles restent dans l’API, même une fois que vous avez arrêté et redémarré le client.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="b2d2d-190">Modifier vos stratégies</span><span class="sxs-lookup"><span data-stu-id="b2d2d-190">Edit your policies</span></span>

<span data-ttu-id="b2d2d-191">Une fois que vous avez sécurisé une API avec Azure AD B2C, vous pouvez tester votre stratégie de connexion/d’inscription et afficher le résultat (ou l’absence de résultat) sur l’API.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="b2d2d-192">Vous pouvez manipuler les revendications d’application dans les stratégies et modifier les informations utilisateur qui sont disponibles dans l’API web.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="b2d2d-193">Toutes les revendications que vous ajoutez seront accessibles par votre API web .NET MVC dans l’objet `ClaimsPrincipal` , comme décrit plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b2d2d-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
