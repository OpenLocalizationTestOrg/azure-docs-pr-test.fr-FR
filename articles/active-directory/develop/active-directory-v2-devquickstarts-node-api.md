---
title: "Sécuriser une API web Azure Active Directory 2.0 à l’aide de Node.js | Microsoft Docs"
description: "Découvrez comment créer une API web Node.js qui accepte des jetons d’un compte Microsoft personnel, ou de comptes professionnels ou scolaires."
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
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="4c465-103">Sécuriser une API web à l’aide de Node.js</span><span class="sxs-lookup"><span data-stu-id="4c465-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="4c465-104">Certains scénarios et fonctionnalités d’Azure Active Directory ne fonctionnent pas avec le point de terminaison 2.0.</span><span class="sxs-lookup"><span data-stu-id="4c465-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="4c465-105">Pour déterminer si vous devez utiliser le point de terminaison 2.0 ou 1.0, consultez les [limitations de 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="4c465-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="4c465-106">Quand vous utilisez le point de terminaison Azure Active Directory (Azure AD) 2.0, vous pouvez utiliser des jetons d’accès [OAuth 2.0](active-directory-v2-protocols.md) pour protéger votre API web.</span><span class="sxs-lookup"><span data-stu-id="4c465-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="4c465-107">Avec les jetons d’accès OAuth 2.0, les utilisateurs disposant à la fois d’un compte Microsoft personnel et de comptes professionnels ou scolaires peuvent accéder de façon sécurisée à votre API web.</span><span class="sxs-lookup"><span data-stu-id="4c465-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="4c465-108">*Passport* est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="4c465-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="4c465-109">Flexible et modulaire, Passport peut être intégré de façon transparente dans n’importe quelle application web Restify ou basée sur Express.</span><span class="sxs-lookup"><span data-stu-id="4c465-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="4c465-110">Dans Passport, une gamme complète de stratégies prend en charge l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe, de Facebook, de Twitter ou d’autres options.</span><span class="sxs-lookup"><span data-stu-id="4c465-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="4c465-111">Nous avons développé une stratégie pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c465-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="4c465-112">Dans cet article, nous vous montrons comment installer le module, puis comment ajouter le plug-in `passport-azure-ad` d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c465-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="4c465-113">Télécharger</span><span class="sxs-lookup"><span data-stu-id="4c465-113">Download</span></span>
<span data-ttu-id="4c465-114">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="4c465-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="4c465-115">Pour suivre le didacticiel, vous pouvez [télécharger la structure de l’application au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip) ou bien la cloner :</span><span class="sxs-lookup"><span data-stu-id="4c465-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="4c465-116">Vous pouvez également obtenir l’application terminée à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4c465-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="4c465-117">1 : Inscrire une application</span><span class="sxs-lookup"><span data-stu-id="4c465-117">1: Register an app</span></span>
<span data-ttu-id="4c465-118">Créez une application sur [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md) pour inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="4c465-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="4c465-119">Assurez-vous d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c465-119">Make sure you:</span></span>

* <span data-ttu-id="4c465-120">Copiez l’**ID d’application** affecté à votre application.</span><span class="sxs-lookup"><span data-stu-id="4c465-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="4c465-121">Vous en aurez besoin pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4c465-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="4c465-122">ajouter la plateforme **Mobile** pour votre application ;</span><span class="sxs-lookup"><span data-stu-id="4c465-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="4c465-123">Copiez **l’URI de redirection** provenant du portail.</span><span class="sxs-lookup"><span data-stu-id="4c465-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="4c465-124">Vous devez utiliser la valeur d’URI par défaut `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="4c465-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="4c465-125">2 : Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="4c465-125">2: Install Node.js</span></span>
<span data-ttu-id="4c465-126">Pour utiliser l’exemple de ce didacticiel, vous devez [installer Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="4c465-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="4c465-127">3 : Installer MongoDB</span><span class="sxs-lookup"><span data-stu-id="4c465-127">3: Install MongoDB</span></span>
<span data-ttu-id="4c465-128">Pour pouvoir utiliser cet exemple, vous devez [installer MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="4c465-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="4c465-129">Dans cet exemple, nous utilisons MongoDB pour rendre votre API REST persistante sur les instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="4c465-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="4c465-130">Dans cet article, nous partons du principe que vous utilisez les points de terminaison d’installation et de serveur par défaut pour MongoDB : mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="4c465-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="4c465-131">4 : Installer les modules Restify dans votre API web</span><span class="sxs-lookup"><span data-stu-id="4c465-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="4c465-132">Nous utilisons Restify pour créer notre API REST.</span><span class="sxs-lookup"><span data-stu-id="4c465-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="4c465-133">Restify est une infrastructure d’application Node.js minimale et flexible qui est dérivée d’Express.</span><span class="sxs-lookup"><span data-stu-id="4c465-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="4c465-134">Restify a un ensemble robuste de fonctionnalités que vous pouvez utiliser pour créer des API REST sur Connect.</span><span class="sxs-lookup"><span data-stu-id="4c465-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="4c465-135">Installer Restify</span><span class="sxs-lookup"><span data-stu-id="4c465-135">Install restify</span></span>
1.  <span data-ttu-id="4c465-136">À l’invite de commandes, accédez au répertoire **azuread** :</span><span class="sxs-lookup"><span data-stu-id="4c465-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="4c465-137">Si le répertoire **azuread** n’existe pas, créez-le :</span><span class="sxs-lookup"><span data-stu-id="4c465-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="4c465-138">Installez Restify :</span><span class="sxs-lookup"><span data-stu-id="4c465-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="4c465-139">La sortie de cette commande doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4c465-139">The output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="4c465-140">Une erreur est-elle survenue ?</span><span class="sxs-lookup"><span data-stu-id="4c465-140">Did you get an error?</span></span>
<span data-ttu-id="4c465-141">Sur certains systèmes d’exploitation, quand vous utilisez la commande `npm`, ce message peut apparaître : `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="4c465-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="4c465-142">Après cette erreur, il vous est demandé d’essayer d’exécuter le compte en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4c465-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="4c465-143">Si ceci se produit, utilisez la commande `sudo` pour exécuter `npm` avec un niveau de privilèges plus élevé.</span><span class="sxs-lookup"><span data-stu-id="4c465-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="4c465-144">Avez-vous reçu une erreur liée à DTrace ?</span><span class="sxs-lookup"><span data-stu-id="4c465-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="4c465-145">Quand vous installez Restify, ce message peut apparaître :</span><span class="sxs-lookup"><span data-stu-id="4c465-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="4c465-146">Restify fournit un mécanisme puissant pour suivre les appels REST en utilisant DTrace.</span><span class="sxs-lookup"><span data-stu-id="4c465-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="4c465-147">Cependant, DTrace n’est pas disponible sur de nombreux systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="4c465-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="4c465-148">Vous pouvez ignorer sans problème ce message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="4c465-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="4c465-149">5 : Installer Passport.js dans votre API web</span><span class="sxs-lookup"><span data-stu-id="4c465-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="4c465-150">À l’invite de commandes, accédez au répertoire **azuread**.</span><span class="sxs-lookup"><span data-stu-id="4c465-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="4c465-151">Installez Passport.js :</span><span class="sxs-lookup"><span data-stu-id="4c465-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="4c465-152">La sortie de la commande doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4c465-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="4c465-153">6 : Ajouter passport-azure-ad à votre API web</span><span class="sxs-lookup"><span data-stu-id="4c465-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="4c465-154">Ensuite, ajoutez la stratégie OAuth en utilisant passport-azuread.</span><span class="sxs-lookup"><span data-stu-id="4c465-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="4c465-155">`passport-azuread` est une suite de stratégies qui connectent Azure AD à Passport.</span><span class="sxs-lookup"><span data-stu-id="4c465-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="4c465-156">Nous utilisons cette stratégie pour les jetons du porteur dans cet exemple d’API REST.</span><span class="sxs-lookup"><span data-stu-id="4c465-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="4c465-157">Bien qu’OAuth 2.0 fournisse un framework dans lequel tout type de jeton connu peut être émis, seuls certains types de jetons sont couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="4c465-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="4c465-158">Les jetons du porteur sont couramment utilisés pour protéger les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4c465-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="4c465-159">Il s’agit du type de jeton le plus fréquemment émis dans OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="4c465-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="4c465-160">De nombreuses implémentations d’OAuth 2.0 partent du principe que les jetons du porteur sont le seul type de jeton émis.</span><span class="sxs-lookup"><span data-stu-id="4c465-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="4c465-161">À l’invite de commandes, accédez au répertoire **azuread**.</span><span class="sxs-lookup"><span data-stu-id="4c465-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="4c465-162">Installez le module `passport-azure-ad` de Passport.js :</span><span class="sxs-lookup"><span data-stu-id="4c465-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="4c465-163">La sortie de la commande doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4c465-163">The output of the command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="4c465-164">7 : Ajouter les modules MongoDB à votre API web</span><span class="sxs-lookup"><span data-stu-id="4c465-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="4c465-165">Dans cet exemple, nous utilisons MongoDB comme notre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="4c465-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="4c465-166">Installez Mongoose, un plug-in largement utilisé, pour gérer les modèles et les schémas :</span><span class="sxs-lookup"><span data-stu-id="4c465-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="4c465-167">Installez le pilote de base de données pour MongoDB (également appelé MongoDB) :</span><span class="sxs-lookup"><span data-stu-id="4c465-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="4c465-168">8 : Installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4c465-168">8: Install additional modules</span></span>
<span data-ttu-id="4c465-169">Installez les autres modules nécessaires.</span><span class="sxs-lookup"><span data-stu-id="4c465-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="4c465-170">À l’invite de commandes, accédez au répertoire **azuread** :</span><span class="sxs-lookup"><span data-stu-id="4c465-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4c465-171">Entrez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="4c465-171">Enter the following commands.</span></span> <span data-ttu-id="4c465-172">Les commandes installent les modules suivants dans votre répertoire node_modules :</span><span class="sxs-lookup"><span data-stu-id="4c465-172">The commands install the following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="4c465-173">9 : Créer un fichier Server.js pour vos dépendances</span><span class="sxs-lookup"><span data-stu-id="4c465-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="4c465-174">Un fichier Server.js contient la plupart des fonctionnalités de votre serveur d’API web.</span><span class="sxs-lookup"><span data-stu-id="4c465-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="4c465-175">Ajoutez la plus grande partie de votre code à ce fichier.</span><span class="sxs-lookup"><span data-stu-id="4c465-175">Add most of your code to this file.</span></span> <span data-ttu-id="4c465-176">À des fins de production, vous pouvez refactoriser les fonctionnalités en fichiers plus petits, comme pour des routes et des contrôleurs distincts.</span><span class="sxs-lookup"><span data-stu-id="4c465-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="4c465-177">Dans cet article, nous utilisons Server.js à cet effet.</span><span class="sxs-lookup"><span data-stu-id="4c465-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="4c465-178">À l’invite de commandes, accédez au répertoire **azuread** :</span><span class="sxs-lookup"><span data-stu-id="4c465-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4c465-179">À l’aide d’un éditeur de votre choix, créez un fichier Server.js.</span><span class="sxs-lookup"><span data-stu-id="4c465-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="4c465-180">Ajoutez les informations suivantes au fichier :</span><span class="sxs-lookup"><span data-stu-id="4c465-180">Add the following information to the file:</span></span>

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

3.  <span data-ttu-id="4c465-181">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="4c465-181">Save the file.</span></span> <span data-ttu-id="4c465-182">Nous y reviendrons sous peu.</span><span class="sxs-lookup"><span data-stu-id="4c465-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="4c465-183">10 : création d’un fichier de configuration pour stocker vos paramètres Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c465-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="4c465-184">Ce fichier de code passe les paramètres de configuration de votre portail Azure AD à Passport.js.</span><span class="sxs-lookup"><span data-stu-id="4c465-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="4c465-185">Vous avez créé ces valeurs de configuration quand vous avez ajouté l’API web au portail, au début de cet article.</span><span class="sxs-lookup"><span data-stu-id="4c465-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="4c465-186">Copiez le code. Après quoi, nous vous expliquerons ce qu’il convient de placer dans les valeurs de ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="4c465-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="4c465-187">À l’invite de commandes, accédez au répertoire **azuread** :</span><span class="sxs-lookup"><span data-stu-id="4c465-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4c465-188">Dans un éditeur, créez un fichier Config.js.</span><span class="sxs-lookup"><span data-stu-id="4c465-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="4c465-189">Ajoutez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c465-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="4c465-190">Valeurs requises</span><span class="sxs-lookup"><span data-stu-id="4c465-190">Required values</span></span>

*   <span data-ttu-id="4c465-191">**IdentityMetadata** : c’est ici que `passport-azure-ad` cherche vos données de configuration pour le fournisseur d’identité et les clés pour valider les jetons JWT (JSON Web Token).</span><span class="sxs-lookup"><span data-stu-id="4c465-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="4c465-192">Si vous utilisez Azure AD, vous ne voulez probablement pas changer ceci.</span><span class="sxs-lookup"><span data-stu-id="4c465-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="4c465-193">**audience**: URI de redirection à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="4c465-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4c465-194">Changez régulièrement vos clés.</span><span class="sxs-lookup"><span data-stu-id="4c465-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="4c465-195">Vérifiez que votre extraction est toujours effectuée à partir de l’URL « openid_keys » et que l’application peut accéder à Internet.</span><span class="sxs-lookup"><span data-stu-id="4c465-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="4c465-196">11 : Ajouter la configuration à votre fichier Server.js</span><span class="sxs-lookup"><span data-stu-id="4c465-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="4c465-197">Votre application doit lire les valeurs à partir du fichier de configuration que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="4c465-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="4c465-198">Ajoutez le fichier .config en tant que ressource requise dans votre application.</span><span class="sxs-lookup"><span data-stu-id="4c465-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="4c465-199">Définissez les variables globales sur celles qui se trouvent dans Config.js.</span><span class="sxs-lookup"><span data-stu-id="4c465-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="4c465-200">À l’invite de commandes, accédez au répertoire **azuread** :</span><span class="sxs-lookup"><span data-stu-id="4c465-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4c465-201">Dans un éditeur, ouvrez Server.js.</span><span class="sxs-lookup"><span data-stu-id="4c465-201">In an editor, open Server.js.</span></span> <span data-ttu-id="4c465-202">Ajoutez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c465-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="4c465-203">Ajoutez une nouvelle section à Server.js :</span><span class="sxs-lookup"><span data-stu-id="4c465-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="4c465-204">12 : Ajouter les informations de modèle et de schéma MongoDB à l’aide de Mongoose</span><span class="sxs-lookup"><span data-stu-id="4c465-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="4c465-205">Ensuite, connectez ces trois fichiers dans un service d’API REST.</span><span class="sxs-lookup"><span data-stu-id="4c465-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="4c465-206">Dans cet article, nous utilisons MongoDB pour stocker nos tâches.</span><span class="sxs-lookup"><span data-stu-id="4c465-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="4c465-207">Nous traitons de cela dans l’*étape 4*.</span><span class="sxs-lookup"><span data-stu-id="4c465-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="4c465-208">Dans le fichier Config.js que vous avez créé à l’étape 11, votre base de données est appelée *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="4c465-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="4c465-209">C’est ce que vous mettez à la fin de l’URL de connexion mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="4c465-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="4c465-210">Vous n’avez pas besoin de créer cette base de données au préalable dans MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4c465-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="4c465-211">La base de données est créée lors de la première exécution de votre application serveur (en supposant que la base de données n’existe pas déjà).</span><span class="sxs-lookup"><span data-stu-id="4c465-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="4c465-212">Vous avez indiqué au serveur la base de données MongoDB à utiliser.</span><span class="sxs-lookup"><span data-stu-id="4c465-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="4c465-213">Ensuite, vous devez écrire du code supplémentaire pour créer le modèle et le schéma pour les tâches de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="4c465-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="4c465-214">Le modèle</span><span class="sxs-lookup"><span data-stu-id="4c465-214">The model</span></span>
<span data-ttu-id="4c465-215">Le modèle de schéma est élémentaire.</span><span class="sxs-lookup"><span data-stu-id="4c465-215">The schema model is very basic.</span></span> <span data-ttu-id="4c465-216">Vous pouvez le développer si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4c465-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="4c465-217">Le modèle de schéma a ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="4c465-217">The schema model has these values:</span></span>

*   <span data-ttu-id="4c465-218">**NAME**.</span><span class="sxs-lookup"><span data-stu-id="4c465-218">**NAME**.</span></span> <span data-ttu-id="4c465-219">Personne affectée à la tâche.</span><span class="sxs-lookup"><span data-stu-id="4c465-219">The person assigned to the task.</span></span> <span data-ttu-id="4c465-220">Il s’agit d’une valeur de type **string**.</span><span class="sxs-lookup"><span data-stu-id="4c465-220">This is a **string** value.</span></span>
*   <span data-ttu-id="4c465-221">**TASK**.</span><span class="sxs-lookup"><span data-stu-id="4c465-221">**TASK**.</span></span> <span data-ttu-id="4c465-222">Nom de la tâche.</span><span class="sxs-lookup"><span data-stu-id="4c465-222">The name of the task.</span></span> <span data-ttu-id="4c465-223">Il s’agit d’une valeur de type **string**.</span><span class="sxs-lookup"><span data-stu-id="4c465-223">This is a **string** value.</span></span>
*   <span data-ttu-id="4c465-224">**DATE**.</span><span class="sxs-lookup"><span data-stu-id="4c465-224">**DATE**.</span></span> <span data-ttu-id="4c465-225">Date d’échéance de la tâche.</span><span class="sxs-lookup"><span data-stu-id="4c465-225">The date that the task is due.</span></span> <span data-ttu-id="4c465-226">Il s’agit d’une valeur de type **datetime**.</span><span class="sxs-lookup"><span data-stu-id="4c465-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="4c465-227">**COMPLETED**.</span><span class="sxs-lookup"><span data-stu-id="4c465-227">**COMPLETED**.</span></span> <span data-ttu-id="4c465-228">Indique si la tâche est terminée.</span><span class="sxs-lookup"><span data-stu-id="4c465-228">Whether the task is completed.</span></span> <span data-ttu-id="4c465-229">Il s’agit d’une valeur de type **boolean**.</span><span class="sxs-lookup"><span data-stu-id="4c465-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="4c465-230">Créer le schéma dans le code</span><span class="sxs-lookup"><span data-stu-id="4c465-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="4c465-231">À l’invite de commandes, accédez au répertoire **azuread** :</span><span class="sxs-lookup"><span data-stu-id="4c465-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4c465-232">Dans votre éditeur, ouvrez Server.js.</span><span class="sxs-lookup"><span data-stu-id="4c465-232">In your editor, open Server.js.</span></span> <span data-ttu-id="4c465-233">Sous l’entrée de configuration, ajoutez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c465-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="4c465-234">Ce code se connecte au serveur MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4c465-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="4c465-235">Il retourne également un objet de schéma.</span><span class="sxs-lookup"><span data-stu-id="4c465-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="4c465-236">En utilisant le schéma, créez votre modèle dans le code.</span><span class="sxs-lookup"><span data-stu-id="4c465-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="4c465-237">Sous le code précédent, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="4c465-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="4c465-238">Comme vous pouvez le voir dans le code, vous créez d’abord votre schéma.</span><span class="sxs-lookup"><span data-stu-id="4c465-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="4c465-239">Ensuite, vous créez un objet de modèle.</span><span class="sxs-lookup"><span data-stu-id="4c465-239">Next, you create a model object.</span></span> <span data-ttu-id="4c465-240">Vous utilisez l’objet de modèle pour stocker vos données dans le code quand vous définissez vos **routes**.</span><span class="sxs-lookup"><span data-stu-id="4c465-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="4c465-241">13 : Ajouter vos routes pour votre serveur API REST de tâches</span><span class="sxs-lookup"><span data-stu-id="4c465-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="4c465-242">Maintenant que vous disposez d’un modèle de base de données, ajoutez les routes que vous utiliserez pour le serveur d’API REST.</span><span class="sxs-lookup"><span data-stu-id="4c465-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="4c465-243">À propos des routes dans Restify</span><span class="sxs-lookup"><span data-stu-id="4c465-243">About routes in restify</span></span>
<span data-ttu-id="4c465-244">Les routes dans Restify fonctionnent exactement de la même façon que quand vous utilisez la pile Express.</span><span class="sxs-lookup"><span data-stu-id="4c465-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="4c465-245">Vous définissez des itinéraires à l’aide de l’URI qui, selon vous, sera appelé par les applications clientes.</span><span class="sxs-lookup"><span data-stu-id="4c465-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="4c465-246">En général, vous définissez vos itinéraires dans un fichier distinct.</span><span class="sxs-lookup"><span data-stu-id="4c465-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="4c465-247">Dans ce didacticiel, nous avons mis nos routes dans Server.js.</span><span class="sxs-lookup"><span data-stu-id="4c465-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="4c465-248">Pour une utilisation en production, nous vous recommandons de factoriser ces routes dans leur propre fichier.</span><span class="sxs-lookup"><span data-stu-id="4c465-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="4c465-249">Voici un exemple de modèle d’une route Restify :</span><span class="sxs-lookup"><span data-stu-id="4c465-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="4c465-250">Il s’agit d’un modèle très basique.</span><span class="sxs-lookup"><span data-stu-id="4c465-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="4c465-251">Restify (et Express) fournit des fonctionnalités bien plus avancées, comme la possibilité de définir des types d’applications et le routage complexe entre différents points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4c465-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="4c465-252">Ajouter des itinéraires par défaut à votre serveur</span><span class="sxs-lookup"><span data-stu-id="4c465-252">Add default routes to your server</span></span>
<span data-ttu-id="4c465-253">Ajoutez les routes CRUD de base : **create**, **retrieve**, **update** et **delete**.</span><span class="sxs-lookup"><span data-stu-id="4c465-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="4c465-254">À l’invite de commandes, accédez au répertoire **azuread** :</span><span class="sxs-lookup"><span data-stu-id="4c465-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4c465-255">Dans un éditeur, ouvrez Server.js.</span><span class="sxs-lookup"><span data-stu-id="4c465-255">In an editor, open Server.js.</span></span> <span data-ttu-id="4c465-256">Ajoutez les informations suivantes en dessous des entrées de base de données créées précédemment :</span><span class="sxs-lookup"><span data-stu-id="4c465-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
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
    req.log.warn(err, 'createTask: unable to save');
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
    'removeTask: unable to delete %s',
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
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
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
    log.warn(err, "There are no tasks in the database. Add one!");
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

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="4c465-257">Ajouter la gestion des erreurs pour les itinéraires</span><span class="sxs-lookup"><span data-stu-id="4c465-257">Add error handling for the routes</span></span>
<span data-ttu-id="4c465-258">Ajoutez une gestion des erreurs afin de communiquer avec le client sur le problème rencontré.</span><span class="sxs-lookup"><span data-stu-id="4c465-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="4c465-259">Ajoutez le code suivant sous le code que vous avez déjà écrit :</span><span class="sxs-lookup"><span data-stu-id="4c465-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="4c465-260">14 : Créer votre serveur</span><span class="sxs-lookup"><span data-stu-id="4c465-260">14: Create your server</span></span>
<span data-ttu-id="4c465-261">La dernière chose à faire consiste à ajouter votre instance de serveur.</span><span class="sxs-lookup"><span data-stu-id="4c465-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="4c465-262">L’instance de serveur gère vos appels.</span><span class="sxs-lookup"><span data-stu-id="4c465-262">The server instance manages your calls.</span></span>

<span data-ttu-id="4c465-263">Restify (et Express) permettent une personnalisation avancée, que vous pouvez utiliser avec un serveur d’API REST.</span><span class="sxs-lookup"><span data-stu-id="4c465-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="4c465-264">Dans ce didacticiel, nous utilisons la configuration la plus simple.</span><span class="sxs-lookup"><span data-stu-id="4c465-264">In this tutorial, we use the most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst to 10.
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
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="4c465-265">15 : Ajouter les routes (pour l’instant sans authentification)</span><span class="sxs-lookup"><span data-stu-id="4c465-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="4c465-266">16 : Exécuter le serveur</span><span class="sxs-lookup"><span data-stu-id="4c465-266">16: Run the server</span></span>
<span data-ttu-id="4c465-267">Il est judicieux de tester votre serveur avant d’ajouter l’authentification.</span><span class="sxs-lookup"><span data-stu-id="4c465-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="4c465-268">Pour tester votre serveur, le plus simple consiste à utiliser curl à une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="4c465-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="4c465-269">Pour ce faire, vous avez besoin d’un utilitaire simple que vous pouvez utiliser pour analyser la sortie au format JSON.</span><span class="sxs-lookup"><span data-stu-id="4c465-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="4c465-270">Installez l’outil JSON que nous utilisons dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="4c465-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="4c465-271">Cette opération installe totalement l’outil JSON.</span><span class="sxs-lookup"><span data-stu-id="4c465-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="4c465-272">Vérifiez que votre instance MongoDB est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="4c465-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="4c465-273">Accédez au répertoire **azuread**, puis exécutez curl :</span><span class="sxs-lookup"><span data-stu-id="4c465-273">Change the directory to **azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="4c465-274">Pour ajouter une tâche :</span><span class="sxs-lookup"><span data-stu-id="4c465-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="4c465-275">La réponse doit être la suivante :</span><span class="sxs-lookup"><span data-stu-id="4c465-275">The response should be:</span></span>

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

5.  <span data-ttu-id="4c465-276">Répertoriez les tâches pour Brandon :</span><span class="sxs-lookup"><span data-stu-id="4c465-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="4c465-277">Si toutes ces commandes s’exécutent sans erreur, vous êtes prêt à ajouter OAuth au serveur d’API REST.</span><span class="sxs-lookup"><span data-stu-id="4c465-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="4c465-278">*Vous avez maintenant un serveur d’API REST avec MongoDB !*</span><span class="sxs-lookup"><span data-stu-id="4c465-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="4c465-279">17 : Ajouter une authentification à votre serveur d’API REST</span><span class="sxs-lookup"><span data-stu-id="4c465-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="4c465-280">Maintenant que vous avez une API REST en cours d’exécution, configurez-la pour l’utiliser avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c465-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="4c465-281">À l’invite de commandes, accédez au répertoire **azuread** :</span><span class="sxs-lookup"><span data-stu-id="4c465-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="4c465-282">Utiliser la stratégie oidcbearerstrategy incluse avec passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="4c465-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="4c465-283">Jusqu’à présent, vous avez créé un serveur REST TODO classique sans aucune gestion des autorisations.</span><span class="sxs-lookup"><span data-stu-id="4c465-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="4c465-284">Ajoutez maintenant l’authentification.</span><span class="sxs-lookup"><span data-stu-id="4c465-284">Now, add authentication.</span></span>

<span data-ttu-id="4c465-285">Indiquez d’abord que vous voulez utiliser Passport.</span><span class="sxs-lookup"><span data-stu-id="4c465-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="4c465-286">Placez ceci juste après votre configuration précédente du serveur :</span><span class="sxs-lookup"><span data-stu-id="4c465-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="4c465-287">Quand vous écrivez des API, il est judicieux de toujours lier les données à un élément unique du jeton, dont un utilisateur ne peut pas usurper l’identité.</span><span class="sxs-lookup"><span data-stu-id="4c465-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="4c465-288">Quand ce serveur stocke des éléments TODO, il le fait en fonction de l’ID d’abonnement de l’utilisateur dans le jeton (appelé via token.sub).</span><span class="sxs-lookup"><span data-stu-id="4c465-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="4c465-289">Vous placez le token.sub dans le champ « owner ».</span><span class="sxs-lookup"><span data-stu-id="4c465-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="4c465-290">Ceci garantit que seul cet utilisateur peut accéder à ses éléments TODO.</span><span class="sxs-lookup"><span data-stu-id="4c465-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="4c465-291">Personne d’autre ne peut accéder aux éléments TODO qui ont été entrés.</span><span class="sxs-lookup"><span data-stu-id="4c465-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="4c465-292">Il n’existe pas d’exposition dans l’API pour « owner ».</span><span class="sxs-lookup"><span data-stu-id="4c465-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="4c465-293">Un utilisateur externe peut demander les éléments TODO d’autres utilisateurs, même s’ils sont authentifiés.</span><span class="sxs-lookup"><span data-stu-id="4c465-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="4c465-294">Ensuite, utilisez la stratégie Open ID Connect Bearer qui est fournie avec `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="4c465-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="4c465-295">Placez ceci après ce que vous avez collé précédemment :</span><span class="sxs-lookup"><span data-stu-id="4c465-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
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
log.info('verifying the user');
log.info(token, 'was the token retrieved');
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

<span data-ttu-id="4c465-296">Passport utilise un modèle similaire pour toutes ses stratégies (Twitter, Facebook, etc.).</span><span class="sxs-lookup"><span data-stu-id="4c465-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="4c465-297">Tous les enregistreurs de stratégie adhèrent au modèle.</span><span class="sxs-lookup"><span data-stu-id="4c465-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="4c465-298">Transmettez à la stratégie une `function()` qui utilise un jeton et `done` comme paramètres.</span><span class="sxs-lookup"><span data-stu-id="4c465-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="4c465-299">La stratégie est retournée une fois qu’elle a effectué tout son travail.</span><span class="sxs-lookup"><span data-stu-id="4c465-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="4c465-300">Stockez l’utilisateur et mettez le jeton de côté pour ne pas avoir à le redemander.</span><span class="sxs-lookup"><span data-stu-id="4c465-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c465-301">Le code précédent accepte n’importe quel utilisateur qui peut s’authentifier auprès de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="4c465-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="4c465-302">C’est ce qu’on appelle l’enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="4c465-302">This is known as auto-registration.</span></span> <span data-ttu-id="4c465-303">Sur un serveur de production, vous n’allez laisser entrer personne sans d’abord lui imposer un processus d’inscription de votre choix.</span><span class="sxs-lookup"><span data-stu-id="4c465-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="4c465-304">C’est généralement le modèle que vous voyez dans les applications consommateur.</span><span class="sxs-lookup"><span data-stu-id="4c465-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="4c465-305">L’application peut permettre de vous inscrire sur Facebook, mais elle vous demande ensuite d’entrer des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4c465-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="4c465-306">Si vous n’utilisiez pas un programme de ligne de commande pour ce didacticiel, vous pouvez extraire l’e-mail de l’objet jeton qui est retourné.</span><span class="sxs-lookup"><span data-stu-id="4c465-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="4c465-307">Ensuite, vous pouvez demander à l’utilisateur d’entrer des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4c465-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="4c465-308">Comme il s’agit d’un serveur de test, vous ajoutez l’utilisateur directement à la base de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="4c465-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="4c465-309">Protéger les points de terminaison</span><span class="sxs-lookup"><span data-stu-id="4c465-309">Protect endpoints</span></span>
<span data-ttu-id="4c465-310">Protégez les points de terminaison en spécifiant l’appel **passport.authenticate()** avec le protocole que vous voulez utiliser.</span><span class="sxs-lookup"><span data-stu-id="4c465-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="4c465-311">Vous pouvez modifier votre route dans le code de votre serveur pour une option plus avancée :</span><span class="sxs-lookup"><span data-stu-id="4c465-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="4c465-312">18 : Réexécuter votre application serveur</span><span class="sxs-lookup"><span data-stu-id="4c465-312">18: Run your server application again</span></span>
<span data-ttu-id="4c465-313">Là encore, utilisez curl pour voir si vous avez une protection OAuth 2.0 pour vos points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4c465-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="4c465-314">Faites-le avant d’exécuter un SDK client sur ce point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4c465-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="4c465-315">Les en-têtes retournés doivent vous indiquer si l’authentification fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="4c465-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="4c465-316">Vérifiez que votre instance MongoDB est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="4c465-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="4c465-317">Accédez au répertoire **azuread** puis utilisez curl :</span><span class="sxs-lookup"><span data-stu-id="4c465-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="4c465-318">Essayez une commande basique, comme POST :</span><span class="sxs-lookup"><span data-stu-id="4c465-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="4c465-319">Une réponse 401 indique que la couche Passport tente de rediriger vers le point de terminaison autorisé, ce qui est exactement ce que vous voulez.</span><span class="sxs-lookup"><span data-stu-id="4c465-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="4c465-320">*Vous disposez maintenant d’un service API REST qui utilise OAuth 2.0 !*</span><span class="sxs-lookup"><span data-stu-id="4c465-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="4c465-321">Vous êtes allé aussi loin que possible avec ce serveur sans utiliser un client compatible OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="4c465-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="4c465-322">Pour cela, vous devez consulter un autre didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4c465-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c465-323">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c465-323">Next steps</span></span>
<span data-ttu-id="4c465-324">Pour référence, l’exemple terminé (sans vos valeurs de configuration) est fourni en tant que [fichier .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4c465-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="4c465-325">Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="4c465-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="4c465-326">Vous pouvez maintenant aborder des rubriques plus avancées.</span><span class="sxs-lookup"><span data-stu-id="4c465-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="4c465-327">Vous pouvez essayer [Sécuriser une application Node.js en utilisant le point de terminaison v2.0](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="4c465-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="4c465-328">Voici quelques ressources supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="4c465-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="4c465-329">Guide du développeur Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="4c465-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="4c465-330">Balise « azure-active-directory » dans Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="4c465-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="4c465-331">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="4c465-331">Get security updates for our products</span></span>
<span data-ttu-id="4c465-332">Nous vous encourageons à vous inscrire pour être averti quand des incidents de sécurité se produisent.</span><span class="sxs-lookup"><span data-stu-id="4c465-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="4c465-333">Sur la page [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948), abonnez-vous aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="4c465-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

