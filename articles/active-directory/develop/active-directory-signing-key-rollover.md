---
title: "Substitution des clés dans Azure AD d’aaaSigning | Documents Microsoft"
description: "Cet article traite des meilleures pratiques de la substitution de la clé de signature pour Azure Active Directory de hello"
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
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="a2e8f-103">Substitution de la clé de signature dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2e8f-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="a2e8f-104">Cette rubrique explique ce que vous devez tooknow sur les clés publiques hello sont utilisées dans les jetons de sécurité Azure Active Directory (Azure AD) toosign.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="a2e8f-105">Il est important toonote que ces clés sont remplacées régulièrement et, en cas d’urgence, peut être déployée sur immédiatement.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="a2e8f-106">Toutes les applications qui utilisent Azure AD doivent être en mesure de tooprogrammatically handle hello substitution de clé processus ou établir un processus de substitution manuelle périodique.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="a2e8f-107">Continuer à lire toounderstand comment les clés hello fonctionnent, comment tooassess hello impact de l’application de tooyour substitution hello et tooupdate votre application ou une substitution de clé de substitution manuelle périodique processus toohandle à établir si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="a2e8f-108">Vue d’ensemble des clés de signature dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e8f-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="a2e8f-109">Azure AD utilise le chiffrement de clé publique générée sur secteur normes tooestablish approbation entre lui-même et hello applications qui l’utilisent.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="a2e8f-110">En pratique, cela fonctionne dans hello suivant : Azure AD utilise une clé de signature qui se compose d’une paire de clés publique et privée.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="a2e8f-111">Lorsqu’un utilisateur se connecte tooan application qui utilise Azure AD pour l’authentification, Azure AD crée un jeton de sécurité qui contient des informations sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="a2e8f-112">Ce jeton est signé par Azure AD à l’aide de sa clé privée avant son envoi différé toohello application.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="a2e8f-113">tooverify hello jeton est valide et provient bien d’Azure AD, l’application hello doit valider la signature du jeton hello à l’aide de la clé publique de hello exposé par Azure AD, qui est contenue dans le locataire hello [document de découverte OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) ou SAML/WS-Fed [document de métadonnées de fédération](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="a2e8f-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="a2e8f-114">Pour des raisons de sécurité clé restaure de manière périodique et, dans les cas de hello d’urgence, la signature d’Azure AD peut être annulés immédiatement.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="a2e8f-115">Toute application qui s’intègre à Azure AD doit être préparée toohandle un événement de substitution de clé quel que soit la fréquence à laquelle il peut se produire.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="a2e8f-116">Si ce n’est pas et que votre application tente de toouse une signature de hello tooverify clés ayant expiré sur un jeton, la demande de connexion hello échoue.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="a2e8f-117">Plus d’une clé valide est toujours disponible dans le document de découverte OpenID Connect hello et le document de métadonnées de fédération hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="a2e8f-118">Votre application doit être préparée toouse toutes les clés de hello spécifié dans le document de hello, car une clé peut être changée rapidement, un autre peut être son remplacement et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="a2e8f-119">Comment tooassess si votre application est affectée et le toodo concernant</span><span class="sxs-lookup"><span data-stu-id="a2e8f-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="a2e8f-120">Comment votre application gère la substitution de clé dépend de variables telles que de type hello d’application ou le protocole d’identité et de la bibliothèque a été utilisée.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="a2e8f-121">les sections Hello ci-dessous évaluer si les types courants de hello d’applications sont affectées par la substitution de clé hello et fournissent des conseils sur la façon dont tooupdate hello la substitution automatique des applications toosupport ou mettre à jour manuellement la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="a2e8f-122">Applications clientes natives ayant accès aux ressources</span><span class="sxs-lookup"><span data-stu-id="a2e8f-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="a2e8f-123">Applications web/API ayant accès aux ressources</span><span class="sxs-lookup"><span data-stu-id="a2e8f-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="a2e8f-124">Applications web/API protégeant les ressources et créées à l’aide d’Azure App Services</span><span class="sxs-lookup"><span data-stu-id="a2e8f-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="a2e8f-125">Applications web/API protégeant les ressources à l’aide du middleware .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="a2e8f-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="a2e8f-126">Applications web/API protégeant les ressources à l’aide du middleware .NET Core OpenID Connect ou JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="a2e8f-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="a2e8f-127">Applications web/API protégeant les ressources à l’aide du module passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="a2e8f-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="a2e8f-128">Applications web/API protégeant les ressources et créées avec Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a2e8f-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="a2e8f-129">Applications web protégeant les ressources et créées avec Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a2e8f-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="a2e8f-130">API web protégeant les ressources et créées avec Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a2e8f-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="a2e8f-131">Applications web protégeant les ressources et créées avec Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a2e8f-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="a2e8f-132">Applications web protégeant les ressources et créées avec Visual Studio 2010, 2008 ou avec Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="a2e8f-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="a2e8f-133">Applications Web / API de protection des ressources à l’aide d’un autres bibliothèques ou implémenter manuellement hello protocoles pris en charge</span><span class="sxs-lookup"><span data-stu-id="a2e8f-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="a2e8f-134">Ce guide n’est **pas** applicable aux :</span><span class="sxs-lookup"><span data-stu-id="a2e8f-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="a2e8f-135">Les applications ajoutées à partir de la galerie d’applications Azure AD (y compris personnalisé) ont des directives spécifiques avec des clés de toosigning ce qui concerne les.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="a2e8f-136">Plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="a2e8f-137">Les applications publiées via le proxy d’application n’ont pas tooworry sur les clés de signature sur site.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="a2e8f-138"><a name="nativeclient"></a>Applications clientes natives ayant accès aux ressources</span><span class="sxs-lookup"><span data-stu-id="a2e8f-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="a2e8f-139">En général, les applications qui ont uniquement accès aux ressources (par exemple,</span><span class="sxs-lookup"><span data-stu-id="a2e8f-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="a2e8f-140">Microsoft Graph, KeyVault, API d’Outlook et d’autres APIs Microsoft) en général uniquement obtenir un jeton et transmettre toohello propriétaire de la ressource.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="a2e8f-141">Étant donné qu’ils ne protègent pas toutes les ressources, ils n’inspectent pas de jeton de hello et est donc inutile de tooensure qu’il est correctement signé.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="a2e8f-142">Si l’ordinateur de bureau ou mobile, les applications clientes natives, appartiennent à cette catégorie et ne sont donc pas affectées par la substitution de hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="a2e8f-143"><a name="webclient"></a>Applications web/API ayant accès aux ressources</span><span class="sxs-lookup"><span data-stu-id="a2e8f-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="a2e8f-144">En général, les applications qui ont uniquement accès aux ressources (par exemple,</span><span class="sxs-lookup"><span data-stu-id="a2e8f-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="a2e8f-145">Microsoft Graph, KeyVault, API d’Outlook et d’autres APIs Microsoft) en général uniquement obtenir un jeton et transmettre toohello propriétaire de la ressource.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="a2e8f-146">Étant donné qu’ils ne protègent pas toutes les ressources, ils n’inspectent pas de jeton de hello et est donc inutile de tooensure qu’il est correctement signé.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="a2e8f-147">Applications et web API qui est à l’aide de flux d’application uniquement hello (informations d’identification de client / certificat client), appartiennent à cette catégorie et ne sont donc pas affectées par la substitution de hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="a2e8f-148"><a name="appservices"></a>Applications web/API protégeant les ressources et créées à l’aide d’Azure App Services</span><span class="sxs-lookup"><span data-stu-id="a2e8f-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="a2e8f-149">L’authentification des Services App Azure / de la fonctionnalité d’autorisation (EasyAuth) a déjà substitution de la logique nécessaire hello toohandle clé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="a2e8f-150"><a name="owin"></a>Applications web/API protégeant les ressources à l’aide du middleware .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="a2e8f-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="a2e8f-151">Si votre application utilise hello .NET OWIN OpenID Connect, WS-Fed ou WindowsAzureActiveDirectoryBearerAuthentication intergiciel (middleware), il est déjà substitution de la logique nécessaire hello toohandle clé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="a2e8f-152">Vous pouvez vérifier que votre application utilise l’un de ces éléments en recherchant les Hello suivant des extraits de code dans votre application Startup.cs ou Startup.Auth.cs</span><span class="sxs-lookup"><span data-stu-id="a2e8f-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="a2e8f-153"><a name="owincore"></a>Applications web/API protégeant les ressources à l’aide du middleware .NET Core OpenID Connect ou JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="a2e8f-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="a2e8f-154">Si votre application utilise hello .NET Core OWIN OpenID Connect ou JwtBearerAuthentication intergiciel (middleware), il est déjà substitution de la logique nécessaire hello toohandle clé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="a2e8f-155">Vous pouvez vérifier que votre application utilise l’un de ces éléments en recherchant les Hello suivant des extraits de code dans votre application Startup.cs ou Startup.Auth.cs</span><span class="sxs-lookup"><span data-stu-id="a2e8f-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="a2e8f-156"><a name="passport"></a>Applications web/API protégeant les ressources à l’aide du module passport-azure-ad Node.js</span><span class="sxs-lookup"><span data-stu-id="a2e8f-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="a2e8f-157">Si votre application utilise le module de passport-ad Node.js hello, il est déjà substitution de la logique nécessaire hello toohandle clé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="a2e8f-158">Vous pouvez vous assurer que votre application passport-ad en recherchant des hello suivant extrait de code dans votre application app.js</span><span class="sxs-lookup"><span data-stu-id="a2e8f-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="a2e8f-159"><a name="vs2015"></a>Applications web/API protégeant les ressources et créées avec Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a2e8f-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="a2e8f-160">Si vous avez sélectionné et que votre application a été créée à l’aide d’un modèle d’application web dans Visual Studio 2015 ou Visual Studio 2017 **travail et les comptes d’établissement scolaire** de hello **modifier l’authentification** menu, il déjà a la substitution de la logique nécessaire hello toohandle clé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="a2e8f-161">Cette logique, incorporée dans le middleware OWIN OpenID Connect de hello, récupère et met en cache les clés hello à partir du document de découverte OpenID Connect hello et actualise régulièrement les.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="a2e8f-162">Si vous avez ajouté manuellement solution tooyour d’authentification, votre application ne peut pas avoir logique de substitution de clé nécessaire hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="a2e8f-163">Vous devez toowrite il vous-même ou hello de suivre les étapes [applications Web API à l’aide de toutes les autres bibliothèques ou implémenter manuellement hello pris en charge les protocoles.](#other).</span><span class="sxs-lookup"><span data-stu-id="a2e8f-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="a2e8f-164"><a name="vs2013"></a>Applications web protégeant les ressources et créées avec Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a2e8f-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="a2e8f-165">Si votre application a été créée à l’aide d’un modèle d’application web dans Visual Studio 2013 et que vous avez sélectionné **comptes professionnels** de hello **modifier l’authentification** menu, il a déjà hello nécessaire logique toohandle automatiquement de substitution de clé.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="a2e8f-166">Cette logique stocke l’identificateur unique de votre organisation et hello dans deux tables de base de données associés hello projet des informations de clé de signature.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="a2e8f-167">Vous trouverez des chaîne de connexion hello pour la base de données hello dans le fichier Web.config du projet hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="a2e8f-168">Si vous avez ajouté manuellement solution tooyour d’authentification, votre application ne peut pas avoir logique de substitution de clé nécessaire hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="a2e8f-169">Vous devez toowrite il vous-même ou hello de suivre les étapes [applications Web API à l’aide de toutes les autres bibliothèques ou implémenter manuellement hello pris en charge les protocoles.](#other).</span><span class="sxs-lookup"><span data-stu-id="a2e8f-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="a2e8f-170">Hello suit vous permet de vérifier que la logique hello fonctionne correctement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="a2e8f-171">Dans Visual Studio 2013, ouvrez la solution de hello, puis sur hello **l’Explorateur de serveurs** onglet hello fenêtre de droite.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="a2e8f-172">Développez **Connexions de données**, **DefaultConnection**, puis **Tables**.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="a2e8f-173">Recherchez hello **IssuingAuthorityKeys** table, faites un clic droit, puis cliquez sur **afficher les données de Table**.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="a2e8f-174">Bonjour **IssuingAuthorityKeys** table, il y aura au moins une ligne, ce qui correspond la valeur d’empreinte numérique toohello pour la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="a2e8f-175">Supprimer des lignes dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="a2e8f-176">Avec le bouton hello **locataires** de table, puis cliquez sur **afficher les données de Table**.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="a2e8f-177">Bonjour **locataires** table, il y aura au moins une ligne, laquelle correspond l’identificateur du locataire tooa répertoire unique.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="a2e8f-178">Supprimer des lignes dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-178">Delete any rows in hello table.</span></span> <span data-ttu-id="a2e8f-179">Si vous ne supprimez pas les lignes hello dans les deux hello **locataires** table et **IssuingAuthorityKeys** table, vous obtiendrez une erreur lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="a2e8f-180">Générez et exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-180">Build and run hello application.</span></span> <span data-ttu-id="a2e8f-181">Une fois que vous êtes connecté tooyour compte, vous pouvez arrêter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="a2e8f-182">Retourner toohello **l’Explorateur de serveurs** et observer les valeurs hello Bonjour **IssuingAuthorityKeys** et **locataires** table.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="a2e8f-183">Vous remarquerez qu’ils ont été complétées automatiquement avec les informations appropriées hello à partir du document de métadonnées de fédération hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="a2e8f-184"><a name="vs2013"></a>API web protégeant les ressources et créées avec Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a2e8f-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="a2e8f-185">Si vous créé une application de l’API web dans Visual Studio 2013 à l’aide du modèle d’API Web hello, puis sélectionné **comptes professionnels** de hello **modifier l’authentification** menu, déjà hello logique nécessaire dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="a2e8f-186">Si vous avez configuré manuellement l’authentification, suivez les instructions de hello sous toolearn comment tooconfigure tooautomatically de votre API Web mettre à jour ses informations de clé.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="a2e8f-187">Hello extrait de code suivant montre comment tooget hello dernières clés à partir du document de métadonnées de fédération hello et ensuite utiliser hello [Gestionnaire de jetons JWT](https://msdn.microsoft.com/library/dn205065.aspx) jeton de hello toovalidate.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="a2e8f-188">extrait de code Hello part du principe que vous allez utiliser votre propre mécanisme de persistance toovalidate clé de hello future de la mise en cache des jetons d’Azure AD, que ce soit dans une base de données, le fichier de configuration ou ailleurs.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

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

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
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
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
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

### <span data-ttu-id="a2e8f-189"><a name="vs2012"></a>Applications web protégeant les ressources et créées avec Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a2e8f-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="a2e8f-190">Si votre application a été créée dans Visual Studio 2012, vous avez probablement utilisé hello identité et outil d’accès aux tooconfigure votre application.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="a2e8f-191">Il est également probable que vous utilisez hello [validation émetteur de nom de Registre (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2e8f-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="a2e8f-192">Hello VINR est chargé de gérer les informations sur les fournisseurs d’identité approuvés (Azure AD) et les clés de hello utilisées toovalidate les jetons émis par eux.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="a2e8f-193">Hello VINR rend également facile tooautomatically mise à jour hello informations de clé stockées dans un fichier Web.config en téléchargeant hello dernier fédération document de métadonnées associé à votre annuaire, en vérifiant si la configuration de hello est obsolète par hello plus récentes document et mise à jour hello toouse hello nouvelle clé d’application si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="a2e8f-194">Si vous avez créé votre application à l’aide d’un des exemples de code hello ou de la documentation détaillée fournis par Microsoft, la logique de substitution de clé hello est déjà incluse dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="a2e8f-195">Vous remarquerez que code hello ci-dessous existe déjà dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="a2e8f-196">Si votre application n’a pas déjà cette logique, suivez les étapes de hello ci-dessous tooadd et tooverify fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="a2e8f-197">Dans **l’Explorateur de solutions**, ajoutez une référence toohello **System.IdentityModel** assembly pour le projet approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="a2e8f-198">Ouvrez hello **Global.asax.cs** de fichier et ajoutez hello qui suit à l’aide de directives :</span><span class="sxs-lookup"><span data-stu-id="a2e8f-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="a2e8f-199">Ajouter hello suivant de méthode toohello **Global.asax.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="a2e8f-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="a2e8f-200">Appeler hello **RefreshValidationSettings()** méthode Bonjour **Application_Start()** méthode dans **Global.asax.cs** comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="a2e8f-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="a2e8f-201">Une fois que vous avez suivi ces étapes, le fichier Web.config de votre application sera mis à jour avec hello dernières informations du document de métadonnées de fédération hello, y compris les dernières clés de hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="a2e8f-202">Cette mise à jour se produit chaque fois que votre pool d’applications est recyclé dans IIS. par défaut IIS a la valeur toorecycle applications toutes les 29 heures.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="a2e8f-203">Suivez les étapes de hello ci-dessous tooverify fonctionnement de la logique de substitution de clé hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="a2e8f-204">Après avoir vérifié que votre application à l’aide de code hello ci-dessus, ouvrez hello **Web.config** de fichiers et accédez toohello  **<issuerNameRegistry>**  bloc, spécifiquement pour hello quelques lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2e8f-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="a2e8f-205">Bonjour  **<add thumbprint=””>**  définir, modifier valeur d’empreinte numérique hello en remplaçant les caractères à une autre.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="a2e8f-206">Enregistrer hello **Web.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="a2e8f-207">Générez l’application hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-207">Build hello application, and then run it.</span></span> <span data-ttu-id="a2e8f-208">Si vous pouvez terminer le processus de connexion hello, votre application est correctement mise à jour de clé de hello en téléchargeant les informations hello requis à partir du document de métadonnées de fédération de votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="a2e8f-209">Si vous rencontrez des problèmes de connexion, vérifiez les modifications de hello dans votre application sont correctes en lisant hello [tooYour Ajout de l’authentification à l’aide d’applications Web Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) rubrique, ou de télécharger et en inspectant hello suivant l’exemple de code : [ Une Application Cloud mutualisée pour Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="a2e8f-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="a2e8f-210"><a name="vs2010"></a>Applications web protégeant les ressources et créées avec Visual Studio 2008 ou 2010 et avec Windows Identity Foundation (WIF) version 1.0 pour .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="a2e8f-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="a2e8f-211">Si vous avez créé une application sur WIF v1.0, il n’est aucune actualisation de tooautomatically mécanisme toouse de configuration de votre application une nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="a2e8f-212">*Moyen le plus simple* utiliser les outils de FedUtil hello inclus dans hello WIF SDK, qui peut récupérer le dernier document de métadonnées hello et mettre à jour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="a2e8f-213">Mettre à jour votre too.NET application 4.5, qui inclut la version la plus récente de WIF dans l’espace de noms système hello hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="a2e8f-214">Vous pouvez ensuite utiliser hello [validation émetteur de nom de Registre (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform les mises à jour automatiques de la configuration de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="a2e8f-215">Effectuer une restauration manuelle conformément aux instructions hello à fin hello de ce guide.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="a2e8f-216">Instructions toouse hello FedUtil tooupdate votre configuration :</span><span class="sxs-lookup"><span data-stu-id="a2e8f-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="a2e8f-217">Vérifiez que vous avez hello WIF v1.0 SDK installé sur votre ordinateur de développement pour Visual Studio 2008 ou 2010.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="a2e8f-218">Dans le cas contraire, vous pouvez [le télécharger ici](https://www.microsoft.com/en-us/download/details.aspx?id=4451).</span><span class="sxs-lookup"><span data-stu-id="a2e8f-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="a2e8f-219">Dans Visual Studio, ouvrez la solution de hello, puis cliquez sur le projet applicable de hello et sélectionnez **mettre à jour des métadonnées de fédération**.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="a2e8f-220">Si cette option n’est pas disponible, FedUtil et/ou hello WIF v1.0 SDK n’a pas été installé.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="a2e8f-221">À partir de l’invite de commandes hello, sélectionnez **mise à jour** toobegin mise à jour les métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="a2e8f-222">Si vous avez accès toohello server environnement où l’application hello est hébergée, vous pouvez éventuellement utiliser FedUtil [Planificateur de mise à jour automatique des métadonnées](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2e8f-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="a2e8f-223">Cliquez sur **Terminer** processus de mise à jour toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="a2e8f-224"><a name="other"></a>Applications Web / API de protection des ressources à l’aide d’un autres bibliothèques ou implémenter manuellement hello protocoles pris en charge</span><span class="sxs-lookup"><span data-stu-id="a2e8f-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="a2e8f-225">Si vous utilisez une autre bibliothèque ou implémentée manuellement un des protocoles de hello pris en charge, vous aurez besoin de bibliothèque de hello tooreview ou tooensure votre implémentation qui hello clé est récupérée sur le document de découverte OpenID Connect hello ou hello document de métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="a2e8f-226">Une façon toocheck pour ce est toodo une recherche dans votre code ou de la bibliothèque hello pour les appels de n’importe quel document de découverte OpenID tooeither hello ou le document de métadonnées de fédération hello.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="a2e8f-227">Si la clé est stocké ailleurs ou codé en dur dans votre application, vous pouvez manuellement récupérer la clé de hello et mise à jour il en conséquence effectuer une restauration manuelle conformément aux instructions hello à fin hello de ce guide.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="a2e8f-228">**Il est fortement recommandé que vous améliorez la substitution automatique des toosupport votre application** à l’aide de hello est proche de plan dans cette surcharge et les interruptions de futures tooavoid article si Azure AD augmente sa cadence de substitution ou a une substitution d’out-of-band d’urgence.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="a2e8f-229">Comment tootest votre toodetermine application si elle est affectée</span><span class="sxs-lookup"><span data-stu-id="a2e8f-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="a2e8f-230">Vous pouvez vérifier si votre application prend en charge la substitution automatique de la clé en téléchargeant les scripts de hello et en suivant les instructions de hello dans [ce référentiel GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="a2e8f-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="a2e8f-231">Comment tooperform une restauration manuelle si votre application ne prend pas en charge la substitution automatique</span><span class="sxs-lookup"><span data-stu-id="a2e8f-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="a2e8f-232">Si votre application ne **pas** prend en charge la substitution automatique, vous devez tooestablish un processus qui régulièrement moniteurs Azure AD de signature des clés et effectue une restauration manuelle en conséquence.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="a2e8f-233">[Ce référentiel GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contient des scripts et des instructions sur la façon de toodo cela.</span><span class="sxs-lookup"><span data-stu-id="a2e8f-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

