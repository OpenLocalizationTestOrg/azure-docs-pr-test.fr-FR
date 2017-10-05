---
title: "Azure Active Directory B2C : inscription d’application | Microsoft Docs"
description: "Inscription de votre application auprès d’Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: 3d4fe2fa10d848c8b29e4d22d284c0d378f07ae0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="76582-103">Azure Active Directory B2C : inscription de votre application</span><span class="sxs-lookup"><span data-stu-id="76582-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="76582-104">Ce démarrage rapide vous aide à inscrire une application dans un client B2C Microsoft Azure Active Directory (Azure AD) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="76582-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="76582-105">Lorsque vous avez terminé, votre application est inscrite comme utilisable dans le client Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="76582-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76582-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="76582-106">Prerequisites</span></span>

<span data-ttu-id="76582-107">Pour générer une application acceptant l’inscription et la connexion des consommateurs, vous devez commencer par inscrire cette application auprès d’un client Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="76582-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="76582-108">Obtenez votre propre client en suivant la procédure décrite dans [Création d’un client Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="76582-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="76582-109">Les applications créées dans le panneau Azure AD B2C dans le portail Azure doivent être gérées à partir du même emplacement.</span><span class="sxs-lookup"><span data-stu-id="76582-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="76582-110">Si vous modifiez des applications B2C à l’aide de PowerShell ou d’un autre portail, ces dernières ne sont plus prises en charge et ne fonctionnent pas avec Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="76582-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="76582-111">Consultez les détails dans la section [Applications ayant généré une erreur](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="76582-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="76582-112">Accéder aux paramètres B2C</span><span class="sxs-lookup"><span data-stu-id="76582-112">Navigate to B2C settings</span></span>

<span data-ttu-id="76582-113">Connectez-vous au [portail Azure](https://portal.azure.com/) en tant qu’administrateur général du client B2C.</span><span class="sxs-lookup"><span data-stu-id="76582-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="76582-114">Choisissez les étapes suivantes en fonction du type d’application que vous inscrivez :</span><span class="sxs-lookup"><span data-stu-id="76582-114">Choose next steps based on the application type you are registering:</span></span>

* [<span data-ttu-id="76582-115">Inscrire une application web</span><span class="sxs-lookup"><span data-stu-id="76582-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="76582-116">Inscrire une API web</span><span class="sxs-lookup"><span data-stu-id="76582-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="76582-117">Inscrire une application mobile ou native</span><span class="sxs-lookup"><span data-stu-id="76582-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="76582-118">Inscrire une application web</span><span class="sxs-lookup"><span data-stu-id="76582-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="76582-119">Si votre application web appelle une API web sécurisée par Azure AD B2C, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="76582-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="76582-120">Créez une clé secrète d’application en accédant au panneau **Clés** et en cliquant sur le bouton **Générer la clé**.</span><span class="sxs-lookup"><span data-stu-id="76582-120">Create an application secret by going to the **Keys** blade and clicking the **Generate Key** button.</span></span> <span data-ttu-id="76582-121">Prenez note de la valeur **Clé d’application** .</span><span class="sxs-lookup"><span data-stu-id="76582-121">Make note of the **App key** value.</span></span> <span data-ttu-id="76582-122">Vous utilisez la valeur en tant que secret d’application dans le code de votre application.</span><span class="sxs-lookup"><span data-stu-id="76582-122">You use the value as the application secret in your application's code.</span></span>
   2. <span data-ttu-id="76582-123">Cliquez sur **Accès d’API**, cliquez sur **Ajouter**, puis sélectionnez votre API web et les étendues (autorisations).</span><span class="sxs-lookup"><span data-stu-id="76582-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="76582-124">Une **Clé secrète d’application** est une information d’identification de sécurité importante, qui doit être correctement sécurisée.</span><span class="sxs-lookup"><span data-stu-id="76582-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="76582-125">Passer aux **étapes suivantes**</span><span class="sxs-lookup"><span data-stu-id="76582-125">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="76582-126">Inscrire une API web</span><span class="sxs-lookup"><span data-stu-id="76582-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="76582-127">Cliquez sur **Étendues publiées** pour ajouter des étendues si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="76582-127">Click **Published scopes** to add more scopes as necessary.</span></span> <span data-ttu-id="76582-128">Par défaut, l’étendue « user_impersonation » est définie.</span><span class="sxs-lookup"><span data-stu-id="76582-128">By default, the "user_impersonation" scope is defined.</span></span> <span data-ttu-id="76582-129">L’étendue user_impersonation permet à d’autres applications d’accéder à cette API pour le compte de l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="76582-129">The user_impersonation scope gives other applications the ability to access this api on behalf of the signed-in user.</span></span> <span data-ttu-id="76582-130">Si vous le souhaitez, l’étendue user_impersonation peut être supprimée.</span><span class="sxs-lookup"><span data-stu-id="76582-130">If you wish, the user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="76582-131">Passer aux **étapes suivantes**</span><span class="sxs-lookup"><span data-stu-id="76582-131">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="76582-132">Inscrire une application mobile/native</span><span class="sxs-lookup"><span data-stu-id="76582-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="76582-133">Passer aux **étapes suivantes**</span><span class="sxs-lookup"><span data-stu-id="76582-133">Jump to **next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="76582-134">Limites</span><span class="sxs-lookup"><span data-stu-id="76582-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="76582-135">Choix d’une URL de réponse d’API ou d’application web</span><span class="sxs-lookup"><span data-stu-id="76582-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="76582-136">Pour l’instant, les applications qui sont inscrites auprès d’Azure AD B2C sont limitées à un ensemble restreint de valeurs d’URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="76582-136">Currently, apps that are registered with Azure AD B2C are restricted to a limited set of reply URL values.</span></span> <span data-ttu-id="76582-137">L’URL de réponse pour les services et applications web doit commencer par le schéma `https`, et toutes les valeurs d’URL de réponse doivent partager un même domaine DNS.</span><span class="sxs-lookup"><span data-stu-id="76582-137">The reply URL for web apps and services must begin with the scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="76582-138">Par exemple, vous ne pouvez pas inscrire une application web comportant l’une des URL de réponse suivantes :</span><span class="sxs-lookup"><span data-stu-id="76582-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="76582-139">Le système d’inscription compare le nom DNS complet de l’URL de réponse existante au nom DNS de l’URL de réponse que vous ajoutez.</span><span class="sxs-lookup"><span data-stu-id="76582-139">The registration system compares the whole DNS name of the existing reply URL to the DNS name of the reply URL that you are adding.</span></span> <span data-ttu-id="76582-140">La demande d’ajout du nom DNS échoue si l’une des conditions suivantes est remplie :</span><span class="sxs-lookup"><span data-stu-id="76582-140">The request to add the DNS name fails if either of the following conditions is true:</span></span>

* <span data-ttu-id="76582-141">Le nom DNS complet de la nouvelle URL de réponse ne correspond pas au nom DNS de l’URL de réponse existante.</span><span class="sxs-lookup"><span data-stu-id="76582-141">The whole DNS name of the new reply URL does not match the DNS name of the existing reply URL.</span></span>
* <span data-ttu-id="76582-142">Le nom DNS complet de la nouvelle URL de réponse n’est pas un sous-domaine de l’URL de réponse existante.</span><span class="sxs-lookup"><span data-stu-id="76582-142">The whole DNS name of the new reply URL is not a subdomain of the existing reply URL.</span></span>

<span data-ttu-id="76582-143">Par exemple, si l’application a cette URL de réponse :</span><span class="sxs-lookup"><span data-stu-id="76582-143">For example, if the app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="76582-144">Vous pouvez la compléter comme suit :</span><span class="sxs-lookup"><span data-stu-id="76582-144">You can add to it, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="76582-145">Dans ce cas, le nom DNS correspond exactement.</span><span class="sxs-lookup"><span data-stu-id="76582-145">In this case, the DNS name matches exactly.</span></span> <span data-ttu-id="76582-146">Vous pouvez aussi définir l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="76582-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="76582-147">Dans ce cas, vous faites référence à un sous-domaine DNS de login.contoso.com. Si vous voulez disposer d’une application avec login-east.contoso.com et login-west.contoso.com comme URL de réponse, vous devez ajouter ces URL de réponse dans l’ordre suivant :</span><span class="sxs-lookup"><span data-stu-id="76582-147">In this case, you're referring to a DNS subdomain of login.contoso.com. If you want to have an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="76582-148">Vous pouvez ajouter les deux derniers car il s’agit de sous-domaines de la première URL de réponse, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="76582-148">You can add the latter two because they are subdomains of the first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="76582-149">Choix d’un URI de redirection d’application native</span><span class="sxs-lookup"><span data-stu-id="76582-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="76582-150">Il existe deux points importants à prendre en considération lors du choix d’un URI de redirection pour les applications mobiles/natives :</span><span class="sxs-lookup"><span data-stu-id="76582-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="76582-151">**Unique** : le schéma de l’URI de redirection doit être unique pour chaque application.</span><span class="sxs-lookup"><span data-stu-id="76582-151">**Unique**: The scheme of the redirect URI should be unique for every application.</span></span> <span data-ttu-id="76582-152">Dans notre exemple (com.onmicrosoft.contoso.appname://redirect/path), nous utilisons com.onmicrosoft.contoso.appname en tant que schéma.</span><span class="sxs-lookup"><span data-stu-id="76582-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as the scheme.</span></span> <span data-ttu-id="76582-153">Nous vous recommandons de suivre ce modèle.</span><span class="sxs-lookup"><span data-stu-id="76582-153">We recommend following this pattern.</span></span> <span data-ttu-id="76582-154">Si deux applications partagent le même schéma, l’utilisateur voit une boîte de dialogue « Choix d’une application ».</span><span class="sxs-lookup"><span data-stu-id="76582-154">If two applications share the same scheme, the user sees a "choose app" dialog.</span></span> <span data-ttu-id="76582-155">Si l’utilisateur effectue un choix incorrect, la connexion échoue.</span><span class="sxs-lookup"><span data-stu-id="76582-155">If the user makes an incorrect choice, the login fails.</span></span>
* <span data-ttu-id="76582-156">**Complet** : l’URI de redirection doit comporter un schéma et un chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="76582-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="76582-157">Le chemin d’accès doit contenir au moins une barre oblique après le domaine (par exemple, //contoso/ fonctionne, tandis que //contoso échoue).</span><span class="sxs-lookup"><span data-stu-id="76582-157">The path must contain at least one forward slash after the domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="76582-158">Vérifiez que l’URI de redirection ne comporte aucun caractère spécial, tel que des traits de soulignement.</span><span class="sxs-lookup"><span data-stu-id="76582-158">Ensure there are no special characters like underscores in the redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="76582-159">Applications ayant généré une erreur</span><span class="sxs-lookup"><span data-stu-id="76582-159">Faulted apps</span></span>

<span data-ttu-id="76582-160">Les applications B2C ne doivent PAS être modifiées :</span><span class="sxs-lookup"><span data-stu-id="76582-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="76582-161">Sur les autres portails de gestion des applications tels que le [Portail Azure Classic](https://manage.windowsazure.com/) et le [Portail d’inscription des applications](https://apps.dev.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="76582-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="76582-162">À l’aide de l’API Graph ou de PowerShell</span><span class="sxs-lookup"><span data-stu-id="76582-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="76582-163">Si vous modifiez l’application B2C comme décrit ci-dessus, puis que vous tentez de la modifier de nouveau dans le panneau des fonctionnalités d’Azure AD B2C sur le Portail Azure, l’application génére une erreur et n’est plus utilisable avec Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="76582-163">If you edit the B2C application as described above and try to edit it again in the Azure AD B2C features blade on the Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="76582-164">Vous devez supprimer l’application, puis la recréer.</span><span class="sxs-lookup"><span data-stu-id="76582-164">You have to delete the application and create it again.</span></span>

<span data-ttu-id="76582-165">Pour supprimer l’application, accédez au [Portail d’inscription des applications](https://apps.dev.microsoft.com/), puis supprimez l’application à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="76582-165">To delete the app, go to the [Application Registration Portal](https://apps.dev.microsoft.com/) and delete the application there.</span></span> <span data-ttu-id="76582-166">Pour que l’application soit visible, vous devez en être le propriétaire (et non simplement un administrateur du locataire).</span><span class="sxs-lookup"><span data-stu-id="76582-166">In order for the application to be visible, you need to be the owner of the application (and not just an admin of the tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="76582-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76582-167">Next steps</span></span>

<span data-ttu-id="76582-168">À présent que vous avez une application inscrite auprès d’Azure AD B2C, vous pouvez suivre l’un de [nos didacticiels de démarrage rapide](active-directory-b2c-overview.md#get-started) afin de devenir opérationnel.</span><span class="sxs-lookup"><span data-stu-id="76582-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) to get up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="76582-169">Créer une application web ASP.NET avec inscription, connexion et réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="76582-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)