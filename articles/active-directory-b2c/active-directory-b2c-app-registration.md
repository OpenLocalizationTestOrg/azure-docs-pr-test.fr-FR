---
title: "Azure Active Directory B2C : inscription d’application | Microsoft Docs"
description: Comment tooregister votre application avec Azure Active Directory B2C
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
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="0ddd4-103">Azure Active Directory B2C : inscription de votre application</span><span class="sxs-lookup"><span data-stu-id="0ddd4-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="0ddd4-104">Ce démarrage rapide vous aide à inscrire une application dans un client B2C Microsoft Azure Active Directory (Azure AD) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="0ddd4-105">Lorsque vous avez terminé, votre application est enregistrée pour une utilisation dans le locataire de hello Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ddd4-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0ddd4-106">Prerequisites</span></span>

<span data-ttu-id="0ddd4-107">toobuild une application qui accepte le consommateur d’inscription et de connexion, vous devez tout d’abord d’application de hello tooregister avec un locataire Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="0ddd4-108">Obtenir votre propre locataire à l’aide de hello étapes [créer un client Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0ddd4-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="0ddd4-109">Les applications créées à partir du panneau hello Azure AD B2C Bonjour portail Azure doivent être gérées à partir de hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="0ddd4-110">Si vous modifiez les applications B2C hello à l’aide de PowerShell ou un autre portail, ils deviennent non pris en charge et ne fonctionnent pas avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="0ddd4-111">Consultez les détails dans hello [a généré une erreur d’applications](#faulted-apps) section.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="0ddd4-112">Accédez tooB2C paramètres</span><span class="sxs-lookup"><span data-stu-id="0ddd4-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="0ddd4-113">Connectez-vous à toohello [portail Azure](https://portal.azure.com/) comme hello administrateur Global du client de hello B2C.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="0ddd4-114">Choisissez les étapes suivantes, selon le type d’application hello que l’inscription :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="0ddd4-115">Inscrire une application web</span><span class="sxs-lookup"><span data-stu-id="0ddd4-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="0ddd4-116">Inscrire une API web</span><span class="sxs-lookup"><span data-stu-id="0ddd4-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="0ddd4-117">Inscrire une application mobile ou native</span><span class="sxs-lookup"><span data-stu-id="0ddd4-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="0ddd4-118">Inscrire une application web</span><span class="sxs-lookup"><span data-stu-id="0ddd4-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="0ddd4-119">Si votre application web appelle une API web sécurisée par Azure AD B2C, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="0ddd4-120">Créer un secret d’application en accédant de toohello **clés** lame et en cliquant sur hello **générer une clé** bouton.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="0ddd4-121">Prenez note de hello **clé application** valeur.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="0ddd4-122">Vous utilisez les valeur hello en tant que secret d’application hello dans le code de votre application.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="0ddd4-123">Cliquez sur **Accès d’API**, cliquez sur **Ajouter**, puis sélectionnez votre API web et les étendues (autorisations).</span><span class="sxs-lookup"><span data-stu-id="0ddd4-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="0ddd4-124">Une **Clé secrète d’application** est une information d’identification de sécurité importante, qui doit être correctement sécurisée.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="0ddd4-125">Raccourcis trop**étapes suivantes**</span><span class="sxs-lookup"><span data-stu-id="0ddd4-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="0ddd4-126">Inscrire une API web</span><span class="sxs-lookup"><span data-stu-id="0ddd4-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="0ddd4-127">Cliquez sur **publié étendues** tooadd plus étendues en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="0ddd4-128">Par défaut, l’étendue hello « user_impersonation » est défini.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="0ddd4-129">l’étendue user_impersonation Hello donne aux autres tooaccess de capacité hello applications Cette api pour le compte d’utilisateur connecté hello.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="0ddd4-130">Si vous le souhaitez, l’étendue user_impersonation hello peut être supprimée.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="0ddd4-131">Raccourcis trop**étapes suivantes**</span><span class="sxs-lookup"><span data-stu-id="0ddd4-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="0ddd4-132">Inscrire une application mobile/native</span><span class="sxs-lookup"><span data-stu-id="0ddd4-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="0ddd4-133">Raccourcis trop**étapes suivantes**</span><span class="sxs-lookup"><span data-stu-id="0ddd4-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="0ddd4-134">Limites</span><span class="sxs-lookup"><span data-stu-id="0ddd4-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="0ddd4-135">Choix d’une URL de réponse d’API ou d’application web</span><span class="sxs-lookup"><span data-stu-id="0ddd4-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="0ddd4-136">Actuellement, les applications qui sont inscrits auprès d’Azure AD B2C sont ensemble restreint tooa limité de valeurs d’URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="0ddd4-137">Hello réponse URL pour les services et applications web doit commencer par le schéma de hello `https`, et répondent à toutes les valeurs d’URL doivent partager un seul domaine DNS.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="0ddd4-138">Par exemple, vous ne pouvez pas inscrire une application web comportant l’une des URL de réponse suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="0ddd4-139">système d’enregistrement de Hello compare hello ensemble nom DNS de hello existant réponse URL toohello nom DNS de l’URL de réponse hello que vous ajoutez.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="0ddd4-140">tooadd hello nom DNS de Hello demande échoue si une de hello conditions suivantes est vraie :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="0ddd4-141">nom DNS complet de Hello hello nouvelle URL de réponse ne correspond pas de nom DNS de hello hello existant URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="0ddd4-142">nom DNS complet de Hello hello nouvelle URL de réponse n’est pas un sous-domaine de l’URL de réponse existante hello.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="0ddd4-143">Par exemple, si hello app a cette URL de réponse :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="0ddd4-144">Vous pouvez ajouter tooit, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="0ddd4-145">Dans ce cas, le nom DNS de hello correspond exactement.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="0ddd4-146">Vous pouvez aussi définir l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="0ddd4-147">Dans ce cas, vous faites référence sous-domaine DNS de tooa de login.contoso.com. Si vous souhaitez toohave une application ayant east.contoso.com de connexion et de connexion-west.contoso.com comme URL de réponse, vous devez ajouter les URL de réponse dans cet ordre :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="0ddd4-148">Vous pouvez ajouter hello deux derniers étant sous-domaines hello première URL de réponse, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="0ddd4-149">Choix d’un URI de redirection d’application native</span><span class="sxs-lookup"><span data-stu-id="0ddd4-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="0ddd4-150">Il existe deux points importants à prendre en considération lors du choix d’un URI de redirection pour les applications mobiles/natives :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="0ddd4-151">**Unique**: schéma hello de l’URI de redirection hello doit être unique pour chaque application.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="0ddd4-152">Dans notre exemple (com.onmicrosoft.contoso.appname://redirect/path), nous utilisons com.onmicrosoft.contoso.appname en tant que schéma de hello.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="0ddd4-153">Nous vous recommandons de suivre ce modèle.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-153">We recommend following this pattern.</span></span> <span data-ttu-id="0ddd4-154">Si les deux applications partagent hello même schéma, hello utilisateur voit une boîte de dialogue « Choisir l’application ».</span><span class="sxs-lookup"><span data-stu-id="0ddd4-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="0ddd4-155">Si l’utilisateur de hello effectue un choix incorrect, la connexion de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="0ddd4-156">**Complet** : l’URI de redirection doit comporter un schéma et un chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="0ddd4-157">chemin d’accès Hello doit contenir au moins une barre oblique (par exemple, //contoso/ fonctionne et //contoso échoue) du domaine hello.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="0ddd4-158">N’Assurez-vous aucun des caractères spéciaux tels que l’uri de redirection des traits de soulignement dans hello.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="0ddd4-159">Applications ayant généré une erreur</span><span class="sxs-lookup"><span data-stu-id="0ddd4-159">Faulted apps</span></span>

<span data-ttu-id="0ddd4-160">Les applications B2C ne doivent PAS être modifiées :</span><span class="sxs-lookup"><span data-stu-id="0ddd4-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="0ddd4-161">Sur les autres portails de gestion des applications tels que le [Portail Azure Classic](https://manage.windowsazure.com/) et le [Portail d’inscription des applications](https://apps.dev.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="0ddd4-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="0ddd4-162">À l’aide de l’API Graph ou de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ddd4-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="0ddd4-163">Si vous modifiez l’application hello B2C comme décrit ci-dessus et tooedit à nouveau dans le panneau de fonctionnalités hello Azure AD B2C sur hello portail Azure, elle devient une application ayant généré une erreur, et votre application n’est plus utilisable avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="0ddd4-164">Vous avez toodelete hello application et créez un nouveau.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="0ddd4-165">application de hello toodelete, accédez toohello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/) et supprimer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="0ddd4-166">Toobe d’application hello visible, vous devez propriétaire hello toobe application hello (et pas seulement à un administrateur de client de hello).</span><span class="sxs-lookup"><span data-stu-id="0ddd4-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ddd4-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ddd4-167">Next steps</span></span>

<span data-ttu-id="0ddd4-168">Maintenant que vous avez une application inscrite auprès de Azure AD B2C, vous pouvez effectuer l’une de [nos didacticiels de démarrage rapide](active-directory-b2c-overview.md#get-started) tooget haut et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0ddd4-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0ddd4-169">Créer une application web ASP.NET avec inscription, connexion et réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="0ddd4-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)