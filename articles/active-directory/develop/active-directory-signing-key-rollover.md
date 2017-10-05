---
title: "Substitution de la clé de signature dans Azure AD | Microsoft Docs"
description: "Cet article décrit les meilleures pratiques de substitution de clé de signature pour Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 228bb9058537af1e4eb38207c376c2eb86aee68c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="e74ca-103">Substitution de la clé de signature dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e74ca-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="e74ca-104">Cette rubrique explique ce que vous devez savoir sur les clés publiques utilisées dans Azure Active Directory (Azure AD) pour la signature des jetons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="e74ca-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="e74ca-105">Il est important de noter que ces clés sont substituées régulièrement, voire immédiatement en cas d’urgence.</span><span class="sxs-lookup"><span data-stu-id="e74ca-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="e74ca-106">Toutes les applications qui utilisent Azure AD doivent être en mesure de gérer le processus de substitution de clé ou d’établir un processus périodique de substitution manuelle de clé par le biais d’un programme.</span><span class="sxs-lookup"><span data-stu-id="e74ca-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="e74ca-107">En lisant cet article, vous allez comprendre le fonctionnement des clés, savoir comment évaluer l’impact de la substitution de votre application et comment mettre à jour votre application ou établir un processus périodique de substitution manuelle de clé pour gérer la substitution de clé si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e74ca-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="e74ca-108">Vue d’ensemble des clés de signature dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="e74ca-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="e74ca-109">Azure AD utilise une technique de chiffrement de clés publiques conforme aux normes du secteur pour établir une relation de confiance avec les applications qui l’utilisent.</span><span class="sxs-lookup"><span data-stu-id="e74ca-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="e74ca-110">Plus concrètement, cela signifie qu’Azure AD utilise une clé de signature se composant d’une paire clé publique-clé privée.</span><span class="sxs-lookup"><span data-stu-id="e74ca-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="e74ca-111">Lorsqu’un utilisateur se connecte à une application qui utilise Azure AD pour s’authentifier, Azure AD crée un jeton de sécurité qui contient des informations sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e74ca-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="e74ca-112">Ce jeton est signé par Azure AD à l’aide de sa clé privée avant d’être renvoyé à l’application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="e74ca-113">Pour vérifier que le jeton est valide et provient bien d’Azure AD, l’application doit valider la signature du jeton à l’aide de la clé publique exposée par Azure AD contenue dans le [document de découverte OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) ou dans le [document de métadonnées de fédération](active-directory-federation-metadata.md) SAML/WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="e74ca-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="e74ca-114">Pour des raisons de sécurité, les clés de signature d’Azure AD sont substituées régulièrement, voire immédiatement en cas d’urgence.</span><span class="sxs-lookup"><span data-stu-id="e74ca-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="e74ca-115">Toute application intégré à Azure AD doit être préparée à gérer un événement de substitution de clé, quelle que soit sa fréquence.</span><span class="sxs-lookup"><span data-stu-id="e74ca-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="e74ca-116">Si ce n’est pas le cas et que votre application tente d’utiliser une clé ayant expiré pour vérifier la signature d’un jeton, la demande de connexion échouera.</span><span class="sxs-lookup"><span data-stu-id="e74ca-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="e74ca-117">Plusieurs clés valides sont disponibles à tout moment dans le document de découverte OpenID Connect et dans le document de métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="e74ca-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="e74ca-118">Votre application doit être préparée à utiliser n’importe quelle clé spécifiée dans le document, car une clé peut être substituée rapidement et une autre prise en remplacement, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="e74ca-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="e74ca-119">Comment évaluer si votre application sera affectée et que faire si cela se produit</span><span class="sxs-lookup"><span data-stu-id="e74ca-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="e74ca-120">La manière dont votre application gère la substitution de la clé dépend de variables comme le type d’application ou le protocole d’identité et la bibliothèque utilisés.</span><span class="sxs-lookup"><span data-stu-id="e74ca-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="e74ca-121">Les sections ci-dessous évaluent si les types d’application les plus courants sont affectés par la substitution de clé et fournissent des conseils sur la mise à jour de l’application pour prendre en charge la substitution automatique ou mettre la clé à jour manuellement.</span><span class="sxs-lookup"><span data-stu-id="e74ca-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="e74ca-122">Applications clientes natives ayant accès aux ressources</span><span class="sxs-lookup"><span data-stu-id="e74ca-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="e74ca-123">Applications web/API ayant accès aux ressources</span><span class="sxs-lookup"><span data-stu-id="e74ca-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="e74ca-124">Applications web/API protégeant les ressources et créées à l’aide d’Azure App Services</span><span class="sxs-lookup"><span data-stu-id="e74ca-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="e74ca-125">Applications web/API protégeant les ressources à l’aide du middleware .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="e74ca-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="e74ca-126">Applications web/API protégeant les ressources à l’aide du middleware .NET Core OpenID Connect ou JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="e74ca-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="e74ca-127">Applications web/API protégeant les ressources à l’aide du module passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="e74ca-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="e74ca-128">Applications web/API protégeant les ressources et créées avec Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e74ca-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="e74ca-129">Applications web protégeant les ressources et créées avec Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e74ca-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="e74ca-130">API web protégeant les ressources et créées avec Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e74ca-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="e74ca-131">Applications web protégeant les ressources et créées avec Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e74ca-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="e74ca-132">Applications web protégeant les ressources et créées avec Visual Studio 2010, 2008 ou avec Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="e74ca-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="e74ca-133">Applications web/API protégeant les ressources avec d’autres bibliothèques ou implémentant manuellement l’un des protocoles pris en charge</span><span class="sxs-lookup"><span data-stu-id="e74ca-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="e74ca-134">Ce guide n’est **pas** applicable aux :</span><span class="sxs-lookup"><span data-stu-id="e74ca-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="e74ca-135">Applications ajoutées depuis la galerie d’applications Azure AD (y compris les applications personnalisées), pour lesquelles il existe des directives spécifiques en ce qui concerne les clés de signature.</span><span class="sxs-lookup"><span data-stu-id="e74ca-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> [<span data-ttu-id="e74ca-136">Plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e74ca-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="e74ca-137">Applications locales publiées via le proxy d’application, qui ne sont pas concernées par les clés de signature.</span><span class="sxs-lookup"><span data-stu-id="e74ca-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <span data-ttu-id="e74ca-138"><a name="nativeclient"></a>Applications clientes natives ayant accès aux ressources</span><span class="sxs-lookup"><span data-stu-id="e74ca-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="e74ca-139">En général, les applications qui ont uniquement accès aux ressources (par exemple,</span><span class="sxs-lookup"><span data-stu-id="e74ca-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="e74ca-140">Microsoft Graph, KeyVault, l’API Outlook et d’autres API Microsoft) obtiennent uniquement un jeton et le transmettent au propriétaire de la ressource.</span><span class="sxs-lookup"><span data-stu-id="e74ca-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="e74ca-141">Étant donné qu’elles ne protègent pas les ressources, elles n’inspectent pas le jeton et n’ont donc pas besoin de s’assurer qu’il est correctement signé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="e74ca-142">Les applications clientes natives, de bureau ou mobiles, appartiennent à cette catégorie et ne sont donc pas affectées par la substitution.</span><span class="sxs-lookup"><span data-stu-id="e74ca-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="e74ca-143"><a name="webclient"></a>Applications web/API ayant accès aux ressources</span><span class="sxs-lookup"><span data-stu-id="e74ca-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="e74ca-144">En général, les applications qui ont uniquement accès aux ressources (par exemple,</span><span class="sxs-lookup"><span data-stu-id="e74ca-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="e74ca-145">Microsoft Graph, KeyVault, l’API Outlook et d’autres API Microsoft) obtiennent uniquement un jeton et le transmettent au propriétaire de la ressource.</span><span class="sxs-lookup"><span data-stu-id="e74ca-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="e74ca-146">Étant donné qu’elles ne protègent pas les ressources, elles n’inspectent pas le jeton et n’ont donc pas besoin de s’assurer qu’il est correctement signé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="e74ca-147">Les applications Web et les API web qui utilisent le flux d’application uniquement (informations d’identification du client/certificat client) appartiennent à cette catégorie et ne sont donc pas affectées par la substitution.</span><span class="sxs-lookup"><span data-stu-id="e74ca-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="e74ca-148"><a name="appservices"></a>Applications web/API protégeant les ressources et créées à l’aide d’Azure App Services</span><span class="sxs-lookup"><span data-stu-id="e74ca-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="e74ca-149">La fonctionnalité d’authentification/d’autorisation d’Azure App Services (EasyAuth) possède déjà la logique nécessaire pour gérer automatiquement la substitution de clé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <span data-ttu-id="e74ca-150"><a name="owin"></a>Applications web/API protégeant les ressources à l’aide du middleware .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="e74ca-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="e74ca-151">Si votre application utilise le middleware .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication, elle possède déjà la logique nécessaire pour gérer automatiquement la substitution de clé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="e74ca-152">Vous pouvez vérifier que votre application utilise l’un de ces middlewares en recherchant les extraits de code suivants dans le fichier Startup.cs ou Startup.Auth.cs de l’application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="e74ca-153"><a name="owincore"></a>Applications web/API protégeant les ressources à l’aide du middleware .NET Core OpenID Connect ou JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="e74ca-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="e74ca-154">Si votre application utilise le middleware .NET Core OWIN OpenID Connect ou JwtBearerAuthentication, elle possède déjà la logique nécessaire pour gérer automatiquement la substitution de clé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="e74ca-155">Vous pouvez vérifier que votre application utilise l’un de ces middlewares en recherchant les extraits de code suivants dans le fichier Startup.cs ou Startup.Auth.cs de l’application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="e74ca-156"><a name="passport"></a>Applications web/API protégeant les ressources à l’aide du module passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="e74ca-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="e74ca-157">Si votre application utilise le module passport-ad Node.js, elle possède déjà la logique nécessaire pour gérer automatiquement la substitution de clé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="e74ca-158">Vous pouvez vérifier que votre application utilise passport-ad en recherchant l’extrait de code suivant dans le fichier app.js de l’application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="e74ca-159"><a name="vs2015"></a>Applications web/API protégeant les ressources et créées avec Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e74ca-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="e74ca-160">Si votre application a été générée à l’aide d’un modèle d’application web dans Visual Studio 2015 ou Visual Studio 2017, et que vous avez sélectionné **Comptes professionnels et scolaires** dans le menu **Modifier l’authentification**, elle a déjà la logique nécessaire pour gérer automatiquement la substitution de clé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="e74ca-161">Cette logique, incorporée dans le middleware OWIN OpenID Connect, récupère et met en cache les clés à partir du document de découverte OpenID Connect, et les actualise régulièrement.</span><span class="sxs-lookup"><span data-stu-id="e74ca-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="e74ca-162">Si vous avez ajouté manuellement l’authentification à votre solution, votre application ne possède peut-être pas la logique de substitution de clé nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e74ca-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="e74ca-163">Vous devrez l’écrire vous-même ou suivre les étapes décrites dans [Applications web/API protégeant les ressources avec d’autres bibliothèques ou implémentant manuellement l’un des protocoles pris en charge](#other).</span><span class="sxs-lookup"><span data-stu-id="e74ca-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <span data-ttu-id="e74ca-164"><a name="vs2013"></a>Applications web protégeant les ressources et créées avec Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e74ca-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="e74ca-165">Si votre application a été générée à l’aide d’un modèle d’application web dans Visual Studio 2013 et que vous avez sélectionné **Comptes professionnels** dans le menu **Modifier l’authentification**, elle possède déjà la logique nécessaire pour gérer automatiquement la substitution de clé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="e74ca-166">Cette logique stocke l’identifiant unique de votre organisation et les informations de clé de signature dans deux tables de base de données associées au projet.</span><span class="sxs-lookup"><span data-stu-id="e74ca-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="e74ca-167">Vous trouverez la chaîne de connexion de la base de données dans le fichier Web.config du projet.</span><span class="sxs-lookup"><span data-stu-id="e74ca-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="e74ca-168">Si vous avez ajouté manuellement l’authentification à votre solution, votre application ne possède peut-être pas la logique de substitution de clé nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e74ca-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="e74ca-169">Vous devrez l’écrire vous-même ou suivre les étapes décrites dans [Applications web/API protégeant les ressources avec d’autres bibliothèques ou implémentant manuellement l’un des protocoles pris en charge](#other).</span><span class="sxs-lookup"><span data-stu-id="e74ca-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="e74ca-170">Les étapes suivantes vous aideront à vérifier le bon fonctionnement de la logique de votre application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="e74ca-171">Dans Visual Studio 2013, ouvrez la solution, puis cliquez sur l’onglet **Explorateur de serveurs** dans la fenêtre de droite.</span><span class="sxs-lookup"><span data-stu-id="e74ca-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="e74ca-172">Développez **Connexions de données**, **DefaultConnection**, puis **Tables**.</span><span class="sxs-lookup"><span data-stu-id="e74ca-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="e74ca-173">Recherchez la table **IssuingAuthorityKeys**, cliquez dessus avec le bouton droit, puis cliquez sur **Afficher les données de la table**.</span><span class="sxs-lookup"><span data-stu-id="e74ca-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="e74ca-174">La table **IssuingAuthorityKeys** comporte au moins une ligne correspondant à la valeur de l’empreinte de la clé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="e74ca-175">Supprimez toutes les lignes de la table.</span><span class="sxs-lookup"><span data-stu-id="e74ca-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="e74ca-176">Cliquez avec le bouton droit sur la table **Clients**, puis cliquez sur **Afficher les données de la table**.</span><span class="sxs-lookup"><span data-stu-id="e74ca-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="e74ca-177">La table **Clients** comporte au moins une ligne correspondant à un identifiant unique du client de répertoire.</span><span class="sxs-lookup"><span data-stu-id="e74ca-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="e74ca-178">Supprimez toutes les lignes de la table.</span><span class="sxs-lookup"><span data-stu-id="e74ca-178">Delete any rows in the table.</span></span> <span data-ttu-id="e74ca-179">Si vous ne supprimez pas les lignes à la fois dans la table **Clients** et dans la table **IssuingAuthorityKeys**, vous obtiendrez une erreur au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="e74ca-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="e74ca-180">Générez et exécutez l’application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-180">Build and run the application.</span></span> <span data-ttu-id="e74ca-181">Une fois connecté à votre compte, vous pouvez arrêter l’application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="e74ca-182">Revenez à **l’Explorateur de serveurs** et examinez les valeurs contenues dans les tables **IssuingAuthorityKeys** et **Clients**.</span><span class="sxs-lookup"><span data-stu-id="e74ca-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="e74ca-183">Vous remarquerez qu’elles ont été automatiquement complétées avec les informations appropriées extraites du document de métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="e74ca-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <span data-ttu-id="e74ca-184"><a name="vs2013"></a>API web protégeant les ressources et créées avec Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e74ca-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="e74ca-185">Si vous avez créé une application API web dans Visual Studio 2013 à l’aide du modèle API web et que vous avez sélectionné **Comptes professionnels** dans le menu **Modifier l’authentification**, votre application contient déjà la logique nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e74ca-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="e74ca-186">Si vous avez configuré l’authentification manuellement, suivez les instructions ci-dessous pour savoir comment configurer votre API web afin de mettre automatiquement à jour ses informations de clé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="e74ca-187">L’extrait de code suivant montre comment obtenir les clés les plus récentes à partir du document de métadonnées de fédération, puis comment utiliser le [Gestionnaire de jetons JWT](https://msdn.microsoft.com/library/dn205065.aspx) pour valider le jeton.</span><span class="sxs-lookup"><span data-stu-id="e74ca-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="e74ca-188">Cet extrait de code suppose que vous allez utiliser votre propre mécanisme de mise en cache pour conserver la clé afin de valider les prochains jetons d’Azure AD (dans une base de données, dans le fichier de configuration ou à un autre emplacement).</span><span class="sxs-lookup"><span data-stu-id="e74ca-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="e74ca-189"><a name="vs2012"></a>Applications web protégeant les ressources et créées avec Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e74ca-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="e74ca-190">Si votre application a été créée dans Visual Studio 2012, vous avez probablement utilisé l’outil Identité et accès pour configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="e74ca-191">Il est également probable que vous utilisiez le [registre de validation de nom d’émetteur (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="e74ca-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="e74ca-192">Le VINR est chargé de conserver les informations relatives aux fournisseurs d’identité approuvés (Azure AD) ainsi que les clés utilisées pour valider les jetons qu’ils émettent.</span><span class="sxs-lookup"><span data-stu-id="e74ca-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="e74ca-193">Le VINR permet également de mettre à jour automatiquement les informations de clé stockées dans un fichier Web.config en téléchargeant le dernier document de métadonnées de fédération associé à votre annuaire, en vérifiant si la configuration est à jour avec le dernier document et en mettant à jour l’application pour utiliser la nouvelle clé si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e74ca-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="e74ca-194">Si vous avez créé votre application à l’aide des exemples de code ou de la documentation détaillée fournis par Microsoft, la logique de substitution de clé est déjà incluse dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e74ca-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="e74ca-195">Vous remarquerez que le code ci-dessous existe déjà dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e74ca-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="e74ca-196">Si votre application ne contient pas déjà cette logique, suivez les étapes ci-dessous pour l’ajouter et vérifier qu’elle fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="e74ca-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="e74ca-197">Dans **l’Explorateur de solutions**, ajoutez une référence à l’assembly **System.IdentityModel** correspondant au projet approprié.</span><span class="sxs-lookup"><span data-stu-id="e74ca-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="e74ca-198">Ouvrez le fichier **Global.asax.cs** et ajoutez le code suivant en utilisant les directives :</span><span class="sxs-lookup"><span data-stu-id="e74ca-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="e74ca-199">Ajoutez la méthode suivante au fichier **Global.asax.cs** :</span><span class="sxs-lookup"><span data-stu-id="e74ca-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="e74ca-200">Appelez la méthode **RefreshValidationSettings()** dans la méthode **Application_Start()** dans **Global.asax.cs** comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="e74ca-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="e74ca-201">Une fois ces étapes effectuées, le fichier Web.config de votre application sera mis à jour avec les dernières informations du document de métadonnées de fédération, y compris les clés les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="e74ca-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="e74ca-202">Cette mise à jour sera effectuée chaque fois que votre pool d’applications sera recyclé dans IIS. Par défaut, IIS est configuré pour recycler les applications toutes les 29 heures.</span><span class="sxs-lookup"><span data-stu-id="e74ca-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="e74ca-203">Suivez les étapes ci-dessous pour vérifier que la logique de substitution de clé fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="e74ca-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="e74ca-204">Vérifiez que votre application utilise bien le code ci-dessus, puis ouvrez le fichier **Web.config** et accédez au bloc **<issuerNameRegistry>**. Examinez plus attentivement les quelques lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e74ca-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="e74ca-205">La table **<add thumbprint=””>** , modifiez la valeur de l’empreinte en remplaçant l’un des caractères par un caractère différent.</span><span class="sxs-lookup"><span data-stu-id="e74ca-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="e74ca-206">Enregistrez le fichier **Web.config** .</span><span class="sxs-lookup"><span data-stu-id="e74ca-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="e74ca-207">Générez puis exécutez l’application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-207">Build the application, and then run it.</span></span> <span data-ttu-id="e74ca-208">Si vous pouvez terminer le processus de connexion, votre application mettra correctement à jour la clé en téléchargeant les informations requises à partir du document de métadonnées de fédération de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="e74ca-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="e74ca-209">Si vous rencontrez des problèmes de connexion, vérifiez que les modifications apportées à votre application sont correctes. Pour cela, consultez la rubrique [Ajout de l’authentification à votre application web à l’aide d’Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect), ou téléchargez et examinez l’exemple de code suivant : [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b) (Application cloud multilocataire pour Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e74ca-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="e74ca-210"><a name="vs2010"></a>Applications web protégeant les ressources et créées avec Visual Studio 2008 ou 2010 et avec Windows Identity Foundation (WIF) version 1.0 pour .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="e74ca-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="e74ca-211">Si vous avez créé une application sur WIF v1.0, aucun mécanisme n’est prévu pour actualiser automatiquement la configuration de votre application afin de permettre l’utilisation d’une nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="e74ca-212">*Moyen le plus simple* Utilisez les outils FedUtil inclus dans le SDK WIF, qui permettent de récupérer le dernier document de métadonnées et de mettre à jour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="e74ca-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="e74ca-213">Mettez à jour votre application vers .NET 4.5, qui inclut la dernière version de WIF contenue dans l’espace de noms système.</span><span class="sxs-lookup"><span data-stu-id="e74ca-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="e74ca-214">Vous pouvez ensuite utiliser le [registre de validation de nom d’émetteur (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) pour mettre à jour automatiquement la configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="e74ca-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="e74ca-215">Effectuez une substitution manuelle en suivant les instructions indiquées à la fin de ce document.</span><span class="sxs-lookup"><span data-stu-id="e74ca-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="e74ca-216">Instructions d’utilisation de FedUtil pour mettre à jour votre configuration :</span><span class="sxs-lookup"><span data-stu-id="e74ca-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="e74ca-217">Vérifiez que le SDK WIF v1.0 est  installé sur votre ordinateur de développement pour Visual Studio 2008 ou 2010.</span><span class="sxs-lookup"><span data-stu-id="e74ca-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="e74ca-218">Dans le cas contraire, vous pouvez [le télécharger ici](https://www.microsoft.com/en-us/download/details.aspx?id=4451).</span><span class="sxs-lookup"><span data-stu-id="e74ca-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="e74ca-219">Dans Visual Studio, ouvrez la solution, puis cliquez avec le bouton droit sur le projet applicable et sélectionnez **Update federation metadata**(Mettre à jour les métadonnées de fédération).</span><span class="sxs-lookup"><span data-stu-id="e74ca-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="e74ca-220">Si cette option n’est pas disponible, cela signifie que l’outil FedUtil et/ou le SDK WIF v1.0 n’a pas été installé.</span><span class="sxs-lookup"><span data-stu-id="e74ca-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="e74ca-221">À l’invite, sélectionnez **Mettre à jour** pour mettre à jour vos métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="e74ca-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="e74ca-222">Si vous avez accès à l’environnement serveur sur lequel l’application est hébergée, vous pouvez éventuellement utiliser le [planificateur de mise à jour automatique des métadonnées](https://msdn.microsoft.com/library/ee517272.aspx)de FedUtil.</span><span class="sxs-lookup"><span data-stu-id="e74ca-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="e74ca-223">Cliquez sur **Terminer** pour terminer le processus de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="e74ca-223">Click **Finish** to complete the update process.</span></span>

### <span data-ttu-id="e74ca-224"><a name="other"></a>Applications web/API protégeant les ressources avec d’autres bibliothèques ou implémentant manuellement l’un des protocoles pris en charge</span><span class="sxs-lookup"><span data-stu-id="e74ca-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="e74ca-225">Si vous utilisez une autre bibliothèque ou si vous avez implémenté manuellement l’un des protocoles pris en charge, vous devez examiner la bibliothèque ou votre implémentation afin de vous assurer que la clé est récupérée à partir du document de découverte OpenID Connect ou du document de métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="e74ca-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="e74ca-226">Pour le vérifier, vous pouvez rechercher dans votre code ou dans le code de la bibliothèque les appels vers le document de découverte OpenID ou le document de métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="e74ca-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="e74ca-227">Si la clé est stockée quelque part ou codée en dur dans votre application, vous pouvez récupérer la clé et la mettre à jour manuellement en suivant les instructions indiquées à la fin de ce document.</span><span class="sxs-lookup"><span data-stu-id="e74ca-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="e74ca-228">**Nous vous recommandons fortement d’améliorer votre application pour prendre en charge la substitution automatique** en utilisant l’une des approches présentées dans cet article pour éviter les perturbations et les surcharges à l’avenir si Azure AD augmente sa cadence de substitution ou doit effectuer une substitution hors bande en urgence.</span><span class="sxs-lookup"><span data-stu-id="e74ca-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="e74ca-229">Comment tester votre application pour savoir si elle sera affectée</span><span class="sxs-lookup"><span data-stu-id="e74ca-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="e74ca-230">Pour vérifier que votre application prend en charge la substitution automatique de clé, téléchargez les scripts et suivez les instructions de [ce référentiel GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="e74ca-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="e74ca-231">Comment effectuer une substitution manuelle si votre application ne prend pas en charge la substitution automatique</span><span class="sxs-lookup"><span data-stu-id="e74ca-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="e74ca-232">Si votre application ne prend **pas** en charge la substitution automatique, vous devez établir un processus permettant de surveiller périodiquement les clés de signature d’Azure AD et d’effectuer une substitution manuelle en conséquence.</span><span class="sxs-lookup"><span data-stu-id="e74ca-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="e74ca-233">[Ce référentiel GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contient des scripts et des instructions sur la façon de procéder.</span><span class="sxs-lookup"><span data-stu-id="e74ca-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

