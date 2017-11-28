---
title: "aaaSecure une API web de v2.0 Azure Active Directory à l’aide de Node.js | Documents Microsoft"
description: "Découvrez comment toobuild un Node.js web API qui accepte les jetons à la fois à partir d’un compte Microsoft personnel et à partir des comptes professionnels ou scolaires."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="3b5c1-103">Sécuriser une API web à l’aide de Node.js</span><span class="sxs-lookup"><span data-stu-id="3b5c1-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="3b5c1-104">Pas toutes les fonctionnalités et les scénarios de Azure Active Directory fonctionnent avec le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="3b5c1-105">toodetermine si vous devez utiliser le point de terminaison hello v2.0 ou point de terminaison hello v1.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="3b5c1-106">Lorsque vous utilisez le point de terminaison v2.0 hello Azure Active Directory (Azure AD), vous pouvez utiliser [OAuth 2.0](active-directory-v2-protocols.md) jetons d’accès tooprotect votre API web.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="3b5c1-107">Avec les jetons d’accès OAuth 2.0, les utilisateurs disposant à la fois d’un compte Microsoft personnel et de comptes professionnels ou scolaires peuvent accéder de façon sécurisée à votre API web.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="3b5c1-108">*Passport* est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="3b5c1-109">Flexible et modulaire, Passport peut être intégré de façon transparente dans n’importe quelle application web Restify ou basée sur Express.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="3b5c1-110">Dans Passport, une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter ou d’autres options.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="3b5c1-111">Nous avons développé une stratégie pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="3b5c1-112">Dans cet article, nous vous indiquons comment tooinstall hello module, puis ajoutez hello Azure AD `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="3b5c1-113">Télécharger</span><span class="sxs-lookup"><span data-stu-id="3b5c1-113">Download</span></span>
<span data-ttu-id="3b5c1-114">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="3b5c1-115">didacticiel de hello toofollow, vous pouvez [télécharger la structure de l’application hello sous forme de fichier .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), ou un clone hello squelette :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="3b5c1-116">Vous pouvez également obtenir l’application hello terminée à fin hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="3b5c1-117">1 : Inscrire une application</span><span class="sxs-lookup"><span data-stu-id="3b5c1-117">1: Register an app</span></span>
<span data-ttu-id="3b5c1-118">Créer une application à [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez [ces étapes détaillées](active-directory-v2-app-registration.md) tooregister une application.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="3b5c1-119">Assurez-vous d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-119">Make sure you:</span></span>

* <span data-ttu-id="3b5c1-120">Hello de copie **Id d’Application** affecté tooyour application.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="3b5c1-121">Vous en aurez besoin pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="3b5c1-122">Ajouter hello **Mobile** plate-forme pour votre application.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="3b5c1-123">Hello de copie **URI de redirection** à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="3b5c1-124">Vous devez utiliser hello URI par défaut de `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="3b5c1-125">2 : Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="3b5c1-125">2: Install Node.js</span></span>
<span data-ttu-id="3b5c1-126">exemple de hello toouse pour ce didacticiel, vous devez [installer Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="3b5c1-127">3 : Installer MongoDB</span><span class="sxs-lookup"><span data-stu-id="3b5c1-127">3: Install MongoDB</span></span>
<span data-ttu-id="3b5c1-128">toosuccessfully utiliser cet exemple, vous devez [installer MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="3b5c1-129">Dans cet exemple, vous utilisez MongoDB toomake votre API REST persistant entre les instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="3b5c1-130">Dans cet article, nous supposons que vous utilisez des points de terminaison hello par défaut installation et le serveur pour MongoDB : mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="3b5c1-131">4 : installation hello restify modules dans votre API web</span><span class="sxs-lookup"><span data-stu-id="3b5c1-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="3b5c1-132">Nous utilisons Resitfy toobuild notre API REST.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="3b5c1-133">Restify est une infrastructure d’application Node.js minimale et flexible qui est dérivée d’Express.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="3b5c1-134">Restify a un ensemble robuste de fonctionnalités que vous pouvez utiliser toobuild API REST sur se connecter.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="3b5c1-135">Installer Restify</span><span class="sxs-lookup"><span data-stu-id="3b5c1-135">Install restify</span></span>
1.  <span data-ttu-id="3b5c1-136">À l’invite de commandes, basculez hello trop**organisation**:</span><span class="sxs-lookup"><span data-stu-id="3b5c1-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="3b5c1-137">Si hello **organisation** répertoire n’existe pas, créez-le :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="3b5c1-138">Installez Restify :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="3b5c1-139">sortie Hello de cette commande doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-139">hello output of this command should look like this:</span></span>

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a><span data-ttu-id="3b5c1-140">Une erreur est-elle survenue ?</span><span class="sxs-lookup"><span data-stu-id="3b5c1-140">Did you get an error?</span></span>
<span data-ttu-id="3b5c1-141">Sur certains systèmes d’exploitation, lorsque vous utilisez hello `npm` de commande, vous pouvez voir ce message : `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="3b5c1-142">Erreur de Hello est suivi d’une requête que vous essayez de compte de hello en cours d’exécution en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="3b5c1-143">Si cela se produit, utilisez la commande hello `sudo` toorun `npm` à un niveau de privilège supérieur.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="3b5c1-144">Vous avez reçu une erreur liée tooDTrace ?</span><span class="sxs-lookup"><span data-stu-id="3b5c1-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="3b5c1-145">Quand vous installez Restify, ce message peut apparaître :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-145">When you install restify, you might see this message:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="3b5c1-146">Restify a un tootrace d’un mécanisme puissant REST appelle à l’aide de DTrace.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="3b5c1-147">Cependant, DTrace n’est pas disponible sur de nombreux systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="3b5c1-148">Vous pouvez ignorer sans problème ce message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="3b5c1-149">5 : Installer Passport.js dans votre API web</span><span class="sxs-lookup"><span data-stu-id="3b5c1-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="3b5c1-150">À l’invite de commandes hello basculez hello trop**organisation**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="3b5c1-151">Installez Passport.js :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="3b5c1-152">sortie Hello de commande hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="3b5c1-153">6 : ajouter les API web passport-azure-ad tooyour</span><span class="sxs-lookup"><span data-stu-id="3b5c1-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="3b5c1-154">Ensuite, ajoutez stratégie hello OAuth à l’aide d’organisation de passport.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="3b5c1-155">`passport-azuread` est une suite de stratégies qui connectent Azure AD à Passport.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="3b5c1-156">Nous utilisons cette stratégie pour les jetons du porteur dans cet exemple d’API REST.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="3b5c1-157">Bien qu’OAuth 2.0 fournisse un framework dans lequel tout type de jeton connu peut être émis, seuls certains types de jetons sont couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="3b5c1-158">Jetons de support sont des points de terminaison tooprotect couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="3b5c1-159">Les jetons de porteur sont hello plus largement émis le jeton OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="3b5c1-160">De nombreuses implémentations OAuth 2.0 supposent que les jetons de porteur hello seul type de jeton émis.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="3b5c1-161">À l’invite de commandes, basculez hello trop**organisation**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="3b5c1-162">Installer hello Passport.js `passport-azure-ad` module :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="3b5c1-163">sortie Hello de commande hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-163">hello output of hello command should look like this:</span></span>

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="3b5c1-164">7 : ajouter MongoDB modules tooyour web API</span><span class="sxs-lookup"><span data-stu-id="3b5c1-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="3b5c1-165">Dans cet exemple, nous utilisons MongoDB comme notre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="3b5c1-166">Installer Mongoose, largement utilisée plug-in, les schémas et les modèles de toomanage :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="3b5c1-167">Installer le pilote de base de données de hello pour MongoDB, également appelé MongoDB :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="3b5c1-168">8 : Installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3b5c1-168">8: Install additional modules</span></span>
<span data-ttu-id="3b5c1-169">Installez hello restant modules requis.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="3b5c1-170">À l’invite de commandes, basculez hello trop**organisation**:</span><span class="sxs-lookup"><span data-stu-id="3b5c1-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="3b5c1-171">Entrez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-171">Enter hello following commands.</span></span> <span data-ttu-id="3b5c1-172">commandes Hello installent hello suivant des modules dans votre répertoire node_modules :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-172">hello commands install hello following modules in your node_modules directory:</span></span>

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="3b5c1-173">9 : Créer un fichier Server.js pour vos dépendances</span><span class="sxs-lookup"><span data-stu-id="3b5c1-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="3b5c1-174">Un fichier de Server.js contient la majorité de hello des fonctionnalités hello pour votre serveur d’API web.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="3b5c1-175">Ajouter la plupart de vos toothis du fichier de code.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-175">Add most of your code toothis file.</span></span> <span data-ttu-id="3b5c1-176">À des fins de production, vous pouvez refactoriser fonctionnalité hello en fichiers plus petits, comme pour les contrôleurs et itinéraires distincts.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="3b5c1-177">Dans cet article, nous utilisons Server.js à cet effet.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="3b5c1-178">À l’invite de commandes, basculez hello trop**organisation**:</span><span class="sxs-lookup"><span data-stu-id="3b5c1-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="3b5c1-179">À l’aide d’un éditeur de votre choix, créez un fichier Server.js.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="3b5c1-180">Ajoutez hello informations toohello fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-180">Add hello following information toohello file:</span></span>

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  <span data-ttu-id="3b5c1-181">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-181">Save hello file.</span></span> <span data-ttu-id="3b5c1-182">Vous revenez dans quelques instants tooit.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="3b5c1-183">10 : créer un toostore de fichier de configuration des paramètres de votre Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b5c1-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="3b5c1-184">Ce fichier de code passe les paramètres de configuration hello depuis votre tooPassport.js portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="3b5c1-185">Vous avez créé ces valeurs de configuration lorsque vous avez ajouté le portail de hello web API toohello au début de hello de l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="3b5c1-186">Après avoir copié les code hello, nous expliquons le tooput dans les valeurs hello de ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="3b5c1-187">À l’invite de commandes, basculez hello trop**organisation**:</span><span class="sxs-lookup"><span data-stu-id="3b5c1-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="3b5c1-188">Dans un éditeur, créez un fichier Config.js.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="3b5c1-189">Ajoutez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="3b5c1-190">Valeurs requises</span><span class="sxs-lookup"><span data-stu-id="3b5c1-190">Required values</span></span>

*   <span data-ttu-id="3b5c1-191">**IdentityMetadata**: c’est là `passport-azure-ad` recherche vos données de configuration pour le fournisseur d’identité (IDP) hello et hello clés toovalidate hello des jetons Web JSON (Jwt).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="3b5c1-192">Si vous utilisez Azure AD, vous n’allez pas toochange.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="3b5c1-193">**audience**: votre URI de redirection à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3b5c1-194">Changez régulièrement vos clés.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="3b5c1-195">Assurez-vous que vous tirez toujours à partir de l’URL de « openid_keys » hello et hello Internet permettre accéder à cette application hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="3b5c1-196">11 : ajouter hello configuration tooyour Server.js fichier</span><span class="sxs-lookup"><span data-stu-id="3b5c1-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="3b5c1-197">Votre application a besoin des valeurs de hello tooread à partir du fichier de configuration hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="3b5c1-198">Ajoutez le fichier .config de hello comme une ressource requise dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="3b5c1-199">Définissez hello variables globales toothose qui se trouvent dans Config.js.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="3b5c1-200">À l’invite de commandes hello basculez hello trop**organisation**:</span><span class="sxs-lookup"><span data-stu-id="3b5c1-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="3b5c1-201">Dans un éditeur, ouvrez Server.js.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-201">In an editor, open Server.js.</span></span> <span data-ttu-id="3b5c1-202">Ajoutez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="3b5c1-203">Ajouter un nouveau tooServer.js de section :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-203">Add a new section tooServer.js:</span></span>

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="3b5c1-204">12 : ajouter des informations de modèle et schéma de MongoDB hello à l’aide de Mongoose</span><span class="sxs-lookup"><span data-stu-id="3b5c1-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="3b5c1-205">Ensuite, connectez ces trois fichiers dans un service d’API REST.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="3b5c1-206">Dans cet article, nous utilisons MongoDB toostore nos tâches.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="3b5c1-207">Nous traitons de cela dans l’*étape 4*.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="3b5c1-208">Dans le fichier de Config.js hello créé à l’étape 11, votre base de données est appelé *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="3b5c1-209">C’est ce que vous mettez à fin hello mongoose_auth_local URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="3b5c1-210">Vous n’avez pas besoin toocreate cette base de données au préalable dans MongoDB.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="3b5c1-211">base de données Hello est créée sur hello première exécution de votre application de serveur (en supposant la base de données hello n’existe pas déjà).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="3b5c1-212">Vous avez indiqué le serveur de hello quel toouse de base de données MongoDB.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="3b5c1-213">Ensuite, vous devez toowrite certains modèles de code supplémentaire toocreate hello et un schéma pour les tâches de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="3b5c1-214">modèle de Hello</span><span class="sxs-lookup"><span data-stu-id="3b5c1-214">hello model</span></span>
<span data-ttu-id="3b5c1-215">modèle de schéma Hello est très simple.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-215">hello schema model is very basic.</span></span> <span data-ttu-id="3b5c1-216">Vous pouvez le développer si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="3b5c1-217">modèle de schéma Hello possède ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="3b5c1-218">**NAME**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-218">**NAME**.</span></span> <span data-ttu-id="3b5c1-219">tâche de Hello personne toohello attribué.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-219">hello person assigned toohello task.</span></span> <span data-ttu-id="3b5c1-220">Il s’agit d’une valeur de type **string**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-220">This is a **string** value.</span></span>
*   <span data-ttu-id="3b5c1-221">**TASK**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-221">**TASK**.</span></span> <span data-ttu-id="3b5c1-222">nom de Hello de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-222">hello name of hello task.</span></span> <span data-ttu-id="3b5c1-223">Il s’agit d’une valeur de type **string**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-223">This is a **string** value.</span></span>
*   <span data-ttu-id="3b5c1-224">**DATE**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-224">**DATE**.</span></span> <span data-ttu-id="3b5c1-225">date de Hello que la tâche hello est plein.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-225">hello date that hello task is due.</span></span> <span data-ttu-id="3b5c1-226">Il s’agit d’une valeur de type **datetime**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="3b5c1-227">**COMPLETED**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-227">**COMPLETED**.</span></span> <span data-ttu-id="3b5c1-228">Indique si la tâche hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-228">Whether hello task is completed.</span></span> <span data-ttu-id="3b5c1-229">Il s’agit d’une valeur de type **boolean**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="3b5c1-230">Créer un schéma de hello dans le code hello</span><span class="sxs-lookup"><span data-stu-id="3b5c1-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="3b5c1-231">À l’invite de commandes, basculez hello trop**organisation**:</span><span class="sxs-lookup"><span data-stu-id="3b5c1-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="3b5c1-232">Dans votre éditeur, ouvrez Server.js.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-232">In your editor, open Server.js.</span></span> <span data-ttu-id="3b5c1-233">Sous l’entrée de configuration hello ajouter hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-233">Below hello configuration entry, add hello following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="3b5c1-234">Ce code connecte toohello MongoDB serveur.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="3b5c1-235">Il retourne également un objet de schéma.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="3b5c1-236">À l’aide du schéma de hello, créez votre modèle dans le code hello</span><span class="sxs-lookup"><span data-stu-id="3b5c1-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="3b5c1-237">Sous hello précédant le code, ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-237">Below hello preceding code, add hello following code:</span></span>

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="3b5c1-238">Comme vous pouvez le voir à partir du code hello, vous créez tout d’abord votre schéma.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="3b5c1-239">Ensuite, vous créez un objet de modèle.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-239">Next, you create a model object.</span></span> <span data-ttu-id="3b5c1-240">Vous utilisez hello modèle objet toostore vos données dans l’ensemble de hello code lorsque vous définissez votre **itinéraires**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="3b5c1-241">13 : Ajouter vos routes pour votre serveur API REST de tâches</span><span class="sxs-lookup"><span data-stu-id="3b5c1-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="3b5c1-242">Maintenant que vous avez un toowork de modèle de base de données avec, ajoutez des itinéraires hello que vous utiliserez pour votre serveur d’API REST.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="3b5c1-243">À propos des routes dans Restify</span><span class="sxs-lookup"><span data-stu-id="3b5c1-243">About routes in restify</span></span>
<span data-ttu-id="3b5c1-244">Itinéraires de restify travail exactement hello même façon que lorsque vous utilisez hello Express pile.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="3b5c1-245">Vous définissez des itinéraires à l’aide de hello URI que vous attendez hello client applications toocall.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="3b5c1-246">En général, vous définissez vos itinéraires dans un fichier distinct.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="3b5c1-247">Dans ce didacticiel, nous avons mis nos routes dans Server.js.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="3b5c1-248">Pour une utilisation en production, nous vous recommandons de factoriser ces routes dans leur propre fichier.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="3b5c1-249">Voici un exemple de modèle d’une route Restify :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="3b5c1-250">Il s’agit de modèle de hello au niveau le plus élémentaire hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="3b5c1-251">Restify (et Express) fournissent des fonctionnalités profonde, telles que les types d’application hello capacité toodefine et routage complexe entre différents points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="3b5c1-252">Ajouter le serveur de tooyour d’itinéraires par défaut</span><span class="sxs-lookup"><span data-stu-id="3b5c1-252">Add default routes tooyour server</span></span>
<span data-ttu-id="3b5c1-253">Ajouter des itinéraires CRUD de base hello : **créer**, **récupérer**, **mettre à jour**, et **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="3b5c1-254">À l’invite de commandes, basculez hello trop**organisation**:</span><span class="sxs-lookup"><span data-stu-id="3b5c1-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="3b5c1-255">Dans un éditeur, ouvrez Server.js.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-255">In an editor, open Server.js.</span></span> <span data-ttu-id="3b5c1-256">Sous les entrées de base de données hello que vous avez apportées précédemment, ajoutez les hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-256">Below hello database entries you made earlier, add hello following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable toosave');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="3b5c1-257">Ajouter la gestion des erreurs pour les itinéraires hello</span><span class="sxs-lookup"><span data-stu-id="3b5c1-257">Add error handling for hello routes</span></span>
<span data-ttu-id="3b5c1-258">Ajouter une gestion des erreurs afin de communiquer client toohello arrière sur le problème hello rencontré.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="3b5c1-259">Ajoutez hello suivant code code hello, qui vous avez déjà écrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-259">Add hello following code below hello code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back toohello client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a><span data-ttu-id="3b5c1-260">14 : Créer votre serveur</span><span class="sxs-lookup"><span data-stu-id="3b5c1-260">14: Create your server</span></span>
<span data-ttu-id="3b5c1-261">Hello dernière chose toodo est tooadd votre instance de serveur.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="3b5c1-262">instance de serveur Hello gère vos appels.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="3b5c1-263">Restify (et Express) permettent une personnalisation avancée, que vous pouvez utiliser avec un serveur d’API REST.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="3b5c1-264">Dans ce didacticiel, nous utilisons le programme d’installation plus simple de hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-264">In this tutorial, we use hello most basic setup.</span></span>

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="3b5c1-265">15 : ajouter des itinéraires hello (sans authentification, pour le moment)</span><span class="sxs-lookup"><span data-stu-id="3b5c1-265">15: Add hello routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a><span data-ttu-id="3b5c1-266">16 : exécutez hello serveur</span><span class="sxs-lookup"><span data-stu-id="3b5c1-266">16: Run hello server</span></span>
<span data-ttu-id="3b5c1-267">Il s’agit d’une bonne idée tootest votre serveur avant d’ajouter l’authentification.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="3b5c1-268">tootest de façon plus simple de Hello votre serveur est à l’aide de curl à une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="3b5c1-269">toodo, vous avez besoin d’un utilitaire simple que vous pouvez utiliser la sortie de tooparse au format JSON.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="3b5c1-270">Installer l’outil JSON hello que nous utilisons Bonjour exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="3b5c1-271">Cette commande installe outil JSON hello globalement.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="3b5c1-272">Vérifiez que votre instance MongoDB est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="3b5c1-273">Basculez hello trop**organisation**, puis exécutez curl :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-273">Change hello directory too**azuread**, and then run curl:</span></span>

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  <span data-ttu-id="3b5c1-274">tooadd une tâche :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="3b5c1-275">réponse de Hello doit être :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-275">hello response should be:</span></span>

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  <span data-ttu-id="3b5c1-276">Répertoriez les tâches pour Brandon :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="3b5c1-277">Si toutes ces commandes s’exécutent sans erreur, vous êtes serveur d’API REST toohello tooadd prêt OAuth.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="3b5c1-278">*Vous avez maintenant un serveur d’API REST avec MongoDB !*</span><span class="sxs-lookup"><span data-stu-id="3b5c1-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="3b5c1-279">17 : ajouter le serveur d’authentification tooyour API REST</span><span class="sxs-lookup"><span data-stu-id="3b5c1-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="3b5c1-280">Maintenant que vous avez une API REST en cours d’exécution, installez-le toouse avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="3b5c1-281">À l’invite de commandes, basculez hello trop**organisation**:</span><span class="sxs-lookup"><span data-stu-id="3b5c1-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="3b5c1-282">Utilisez oidcbearerstrategy hello qui est inclus avec passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="3b5c1-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="3b5c1-283">Jusqu’à présent, vous avez créé un serveur REST TODO classique sans aucune gestion des autorisations.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="3b5c1-284">Ajoutez maintenant l’authentification.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-284">Now, add authentication.</span></span>

<span data-ttu-id="3b5c1-285">Commencez par indiquer que vous souhaitez toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="3b5c1-286">Placez ceci juste après votre configuration précédente du serveur :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="3b5c1-287">Lorsque vous écrivez des API, il est un Bonjour de lien recommandé tooalways toosomething de données unique à partir du jeton hello qui hello utilisateur ne peut pas usurper l’identité.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="3b5c1-288">Lorsque ce serveur stocke des éléments de tâche, il les stocke en fonction de l’ID d’abonnement utilisateur hello dans le jeton hello (appelé via token.sub).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="3b5c1-289">Vous placez hello token.sub dans le champ « propriétaire » de hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="3b5c1-290">Cela garantit que seul cet utilisateur peut accéder à TODOs l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="3b5c1-291">Personne d’autre ne peut accéder aux TODOs hello qui ont été entrés.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="3b5c1-292">Il n’existe pas d’exposition Bonjour API pour « propriétaire ».</span><span class="sxs-lookup"><span data-stu-id="3b5c1-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="3b5c1-293">Un utilisateur externe peut demander les éléments TODO d’autres utilisateurs, même s’ils sont authentifiés.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="3b5c1-294">Ensuite, utilisez la stratégie de support de se connecter ID ouvrir hello fourni avec `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="3b5c1-295">Placez ceci après ce que vous avez collé précédemment :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="3b5c1-296">Passport utilise un modèle similaire pour toutes ses stratégies (Twitter, Facebook, etc.).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="3b5c1-297">Tous les enregistreurs de stratégie respectent toohello modèle.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="3b5c1-298">Stratégie de hello de passer un `function()` qui utilise un jeton et `done` en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="3b5c1-299">stratégie de Hello est retournée une fois qu’il fait tout son travail.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="3b5c1-300">Stocker les utilisateur hello et jeton de hello dissimulation vous n’avez pas besoin tooask pour celle-ci à nouveau.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b5c1-301">Hello code précédent prend tout utilisateur qui peut authentifier tooyour server.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="3b5c1-302">C’est ce qu’on appelle l’enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-302">This is known as auto-registration.</span></span> <span data-ttu-id="3b5c1-303">Sur un serveur de production, vous ne voudriez toolet tout le monde sans avoir d’abord les passent par un processus d’inscription que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="3b5c1-304">Il s’agit généralement de modèle hello que vous voyez dans les applications consommateur.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="3b5c1-305">application Hello peut vous permettre de tooregister avec Facebook, mais il vous demande alors tooenter des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="3b5c1-306">Si vous n’utilisiez un programme de ligne de commande pour ce didacticiel, vous pouvez extraire par courrier électronique hello à partir de l’objet du jeton hello qui est retourné.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="3b5c1-307">Ensuite, vous vous demandez peut-être hello utilisateur tooenter plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="3b5c1-308">Car il s’agit d’un serveur de test, vous ajoutez l’utilisateur de hello directement toohello base de données.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="3b5c1-309">Protéger les points de terminaison</span><span class="sxs-lookup"><span data-stu-id="3b5c1-309">Protect endpoints</span></span>
<span data-ttu-id="3b5c1-310">Protéger les points de terminaison en spécifiant hello **passport.authenticate()** appel avec le protocole de hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="3b5c1-311">Vous pouvez modifier votre route dans le code de votre serveur pour une option plus avancée :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-311">You can edit your route in your server code for a more advanced option:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="3b5c1-312">18 : Réexécuter votre application serveur</span><span class="sxs-lookup"><span data-stu-id="3b5c1-312">18: Run your server application again</span></span>
<span data-ttu-id="3b5c1-313">Utilisez curl nouveau toosee si vous avez la protection de OAuth 2.0 par rapport à vos points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="3b5c1-314">Faites-le avant d’exécuter un SDK client sur ce point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="3b5c1-315">en-têtes Hello retournés doivent indiquer si l’authentification fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="3b5c1-316">Vérifiez que votre instance MongoDB est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="3b5c1-317">Modifier toohello **organisation** répertoire, puis utilisez curl :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="3b5c1-318">Essayez une commande basique, comme POST :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="3b5c1-319">Une réponse 401 indique cette couche de Passport hello essaie tooredirect toohello autoriser le point de terminaison, qui est exactement ce que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="3b5c1-320">*Vous disposez maintenant d’un service API REST qui utilise OAuth 2.0 !*</span><span class="sxs-lookup"><span data-stu-id="3b5c1-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="3b5c1-321">Vous êtes allé aussi loin que possible avec ce serveur sans utiliser un client compatible OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="3b5c1-322">Pour ce faire, vous devez tooreview un didacticiel supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b5c1-323">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b5c1-323">Next steps</span></span>
<span data-ttu-id="3b5c1-324">Pour référence, exemple hello terminée (sans les valeurs de configuration) est fourni en tant que [un fichier .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="3b5c1-325">Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="3b5c1-326">Maintenant, vous pouvez déplacer sur toomore rubriques avancées.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="3b5c1-327">Vous souhaiterez peut-être tootry [sécuriser une application web de Node.js à l’aide du point de terminaison hello v2.0](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="3b5c1-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="3b5c1-328">Voici quelques ressources supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="3b5c1-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="3b5c1-329">Guide du développeur Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="3b5c1-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="3b5c1-330">Balise « azure-active-directory » dans Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="3b5c1-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="3b5c1-331">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="3b5c1-331">Get security updates for our products</span></span>
<span data-ttu-id="3b5c1-332">Nous vous invitons à vous toosign des toobe averti lorsque des incidents de sécurité se produisent.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="3b5c1-333">Sur hello [des Notifications de sécurité techniques Microsoft](https://technet.microsoft.com/security/dd252948) page, s’abonner tooSecurity conseils alertes.</span><span class="sxs-lookup"><span data-stu-id="3b5c1-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

