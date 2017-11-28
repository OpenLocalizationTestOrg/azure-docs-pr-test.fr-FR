---
title: aaaAzure AD Node.js prise en main | Documents Microsoft
description: "Comment toobuild une API web de Node.js REST qui s’intègre à Azure AD pour l’authentification."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="52c79-103">Prise en main d’API web pour Node.js</span><span class="sxs-lookup"><span data-stu-id="52c79-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="52c79-104">*Passport* est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="52c79-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="52c79-105">Flexible et modulaire, Passport peut être supprimé de manière transparente dans tooany rapides ou Restify d’application web.</span><span class="sxs-lookup"><span data-stu-id="52c79-105">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="52c79-106">Une gamme complète de stratégies prend en charge l’authentification avec un nom d’utilisateur et un mot de passe, Facebook, Twitter et bien d’autres.</span><span class="sxs-lookup"><span data-stu-id="52c79-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="52c79-107">Nous avons développé une stratégie pour Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52c79-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="52c79-108">Nous installer ce module et puis ajoutez hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="52c79-108">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="52c79-109">toodo, vous devez :</span><span class="sxs-lookup"><span data-stu-id="52c79-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="52c79-110">inscrivez une application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="52c79-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="52c79-111">Configurer votre application toouse Passport `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="52c79-111">Set up your app toouse Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="52c79-112">Configurer une client application toocall hello tooDo API web de liste.</span><span class="sxs-lookup"><span data-stu-id="52c79-112">Configure a client application toocall hello tooDo List web API.</span></span>

<span data-ttu-id="52c79-113">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="52c79-113">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="52c79-114">Cet article n’aborde pas comment tooimplement connectez-vous, d’abonnement, ou le profil de gestion avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="52c79-114">This article doesn't cover how tooimplement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="52c79-115">Il se concentre sur des API web appelant après que hello utilisateur est déjà authentifié.</span><span class="sxs-lookup"><span data-stu-id="52c79-115">It focuses on calling web APIs after hello user is already authenticated.</span></span>  <span data-ttu-id="52c79-116">Nous vous recommandons de commencer avec [comment toointegrate avec le document d’Azure Active Directory](active-directory-how-to-integrate.md) toolearn relatives aux principes élémentaires de hello d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52c79-116">We recommend that you start with [How toointegrate with Azure Active Directory document](active-directory-how-to-integrate.md) toolearn about hello basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="52c79-117">Nous avons publié à tout le code source hello pour cet exemple en cours d’exécution dans GitHub sous une licence du MIT, nous avons tooclone libre (ou mieux encore, branche) et fournir des commentaires et extraire des demandes.</span><span class="sxs-lookup"><span data-stu-id="52c79-117">We've released all hello source code for this running example in GitHub under an MIT license, so feel free tooclone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="52c79-118">À propos des modules Node.js</span><span class="sxs-lookup"><span data-stu-id="52c79-118">About Node.js modules</span></span>
<span data-ttu-id="52c79-119">Nous utilisons des modules Node.js au cours de cette procédure détaillée.</span><span class="sxs-lookup"><span data-stu-id="52c79-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="52c79-120">Les modules sont des packages JavaScript chargeables qui fournissent une fonctionnalité spécifique à votre application.</span><span class="sxs-lookup"><span data-stu-id="52c79-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="52c79-121">Généralement, vous installez des modules d’à l’aide de hello Node.js un outil de ligne de commande NPM dans le répertoire d’installation NPM hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-121">You usually install modules by using hello Node.js an NPM command-line tool in hello NPM installation directory.</span></span> <span data-ttu-id="52c79-122">Toutefois, certains modules, tels que du module HTTP du hello, sont inclus dans le package de Node.js hello core.</span><span class="sxs-lookup"><span data-stu-id="52c79-122">However, some modules, such as hello HTTP module, are included in hello core Node.js package.</span></span>

<span data-ttu-id="52c79-123">Modules installés sont enregistrés dans hello **node_modules** répertoire à votre répertoire d’installation de Node.js racine hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-123">Installed modules are saved in hello **node_modules** directory at hello root of your Node.js installation directory.</span></span> <span data-ttu-id="52c79-124">Chaque module Bonjour **node_modules** répertoire maintient son propre **node_modules** répertoire qui contient tous les modules dont il dépend.</span><span class="sxs-lookup"><span data-stu-id="52c79-124">Each module in hello **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="52c79-125">Chaque module requis dispose également de son propre répertoire **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="52c79-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="52c79-126">Cette structure de répertoire récursive représente la chaîne de dépendance hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-126">This recursive directory structure represents hello dependency chain.</span></span>

<span data-ttu-id="52c79-127">Cette structure de chaîne de dépendance augmente l’encombrement de l’application.</span><span class="sxs-lookup"><span data-stu-id="52c79-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="52c79-128">Mais elle garantit également que toutes les dépendances sont respectées, cette version de modules de hello hello qui est utilisée dans le développement est également utilisée en production.</span><span class="sxs-lookup"><span data-stu-id="52c79-128">But it also guarantees that all dependencies are met and that hello version of hello modules that's used in development is also used in production.</span></span> <span data-ttu-id="52c79-129">Comportement d’application hello de production est ainsi plus prévisibles et évite les problèmes de contrôle de version qui peuvent affecter les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="52c79-129">This makes hello production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="52c79-130">Étape 1 : inscription d’un client Azure AD</span><span class="sxs-lookup"><span data-stu-id="52c79-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="52c79-131">toouse cet exemple, vous avez besoin d’un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52c79-131">toouse this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="52c79-132">Si vous ne savez pas quel un locataire est ou tooget, voir [comment tooget une annonce Azure locataire](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="52c79-132">If you're not sure what a tenant is or how tooget one, see [How tooget an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="52c79-133">Étape 2 : création d’une application</span><span class="sxs-lookup"><span data-stu-id="52c79-133">Step 2: Create an application</span></span>
<span data-ttu-id="52c79-134">Ensuite, vous créez une application dans votre annuaire que Azure AD de fournit des informations qu’il doit toosecurely communiquent avec votre application.</span><span class="sxs-lookup"><span data-stu-id="52c79-134">Next you create an app in your directory that gives Azure AD information that it needs toosecurely communicate with your app.</span></span>  <span data-ttu-id="52c79-135">Application cliente de hello et API web sont représentés par un seul **ID d’Application** dans ce cas, car ils constituent une seule application logique.</span><span class="sxs-lookup"><span data-stu-id="52c79-135">Both hello client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="52c79-136">toocreate une application, procédez comme [ces instructions](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="52c79-136">toocreate an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="52c79-137">Si vous générez une application métier, [ces instructions supplémentaires peuvent être utiles](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="52c79-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="52c79-138">toocreate une application :</span><span class="sxs-lookup"><span data-stu-id="52c79-138">toocreate an application:</span></span>

1. <span data-ttu-id="52c79-139">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="52c79-139">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="52c79-140">Dans le menu supérieur de hello, sélectionnez votre compte.</span><span class="sxs-lookup"><span data-stu-id="52c79-140">On hello top menu, select your account.</span></span> <span data-ttu-id="52c79-141">Ensuite, sous hello **répertoire** , choisissez client Active Directory de hello où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="52c79-141">Then, under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="52c79-142">Dans le menu hello hello gauche, sélectionnez **plus Services**, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52c79-142">In hello menu on hello left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="52c79-143">Sélectionnez **Inscriptions d’applications**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="52c79-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="52c79-144">Suivez hello invites toocreate un **Application Web et/ou WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="52c79-144">Follow hello prompts toocreate a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="52c79-145">Hello **nom** Hello application décrit utilisateurs tooend de votre application.</span><span class="sxs-lookup"><span data-stu-id="52c79-145">hello **name** of hello application describes your application tooend users.</span></span>

      * <span data-ttu-id="52c79-146">Hello **URL de connexion** est l’URL de base hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="52c79-146">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="52c79-147">Hello par défaut de l’URL de l’exemple de code hello est `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="52c79-147">hello default URL of hello sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="52c79-148">Une fois l’application enregistrée, Azure AD lui affecte un ID d’application unique.</span><span class="sxs-lookup"><span data-stu-id="52c79-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="52c79-149">Vous avez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de la page de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-149">You need this value in hello next sections, so copy it from hello application page.</span></span>

7. <span data-ttu-id="52c79-150">À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="52c79-150">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="52c79-151">Hello **URI ID d’application** est un identificateur unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="52c79-151">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="52c79-152">convention de Hello est toouse `https://<tenant-domain>/<app-name>`, par exemple : `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="52c79-152">hello convention is toouse `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="52c79-153">Créer un **clé** pour votre application à partir de hello **paramètres** page, puis le copier quelque part.</span><span class="sxs-lookup"><span data-stu-id="52c79-153">Create a **Key** for your application from hello **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="52c79-154">Vous en aurez besoin rapidement.</span><span class="sxs-lookup"><span data-stu-id="52c79-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="52c79-155">Étape 3 : téléchargement de Node.js pour votre plateforme</span><span class="sxs-lookup"><span data-stu-id="52c79-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="52c79-156">toosuccessfully utiliser cet exemple, vous devez disposer d’une installation active de Node.js.</span><span class="sxs-lookup"><span data-stu-id="52c79-156">toosuccessfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="52c79-157">Installez Node.js à partir de l’adresse suivante : [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="52c79-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="52c79-158">Étape 4 : installation de MongoDB sur votre plateforme</span><span class="sxs-lookup"><span data-stu-id="52c79-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="52c79-159">toosuccessfully utiliser cet exemple, vous devez disposer d’une installation active de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="52c79-159">toosuccessfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="52c79-160">Vous utilisez MongoDB toomake hello API REST persistant entre les instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="52c79-160">You use MongoDB toomake hello REST API persistent across server instances.</span></span>

<span data-ttu-id="52c79-161">Installez MongoDB à partir de l’adresse suivante : [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="52c79-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="52c79-162">Cette procédure pas à pas suppose que vous utilisez points de terminaison hello par défaut installation et le serveur pour MongoDB, qui au moment de la rédaction de hello est mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="52c79-162">This walkthrough assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="52c79-163">Étape 5 : Installer les modules de Restify hello dans votre API web</span><span class="sxs-lookup"><span data-stu-id="52c79-163">Step 5: Install hello Restify modules in your web API</span></span>
<span data-ttu-id="52c79-164">Nous utilisons Restify toobuild notre API REST.</span><span class="sxs-lookup"><span data-stu-id="52c79-164">We are using Restify toobuild our REST API.</span></span> <span data-ttu-id="52c79-165">Restify est une infrastructure d’application Node.js minimale et flexible qui est dérivée d’Express.</span><span class="sxs-lookup"><span data-stu-id="52c79-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="52c79-166">Elle inclut un ensemble complet de fonctionnalités de création API REST sur Connect.</span><span class="sxs-lookup"><span data-stu-id="52c79-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="52c79-167">Installation de Restify</span><span class="sxs-lookup"><span data-stu-id="52c79-167">Install Restify</span></span>
1. <span data-ttu-id="52c79-168">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** active.</span><span class="sxs-lookup"><span data-stu-id="52c79-168">From hello command line, change directories toohello **azuread** directory.</span></span> <span data-ttu-id="52c79-169">Si hello **organisation** répertoire n’existe pas, créez-le.</span><span class="sxs-lookup"><span data-stu-id="52c79-169">If hello **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="52c79-170">Tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52c79-170">Type hello following command:</span></span>

    `npm install restify`

    <span data-ttu-id="52c79-171">Cette commande permet d’installer Restify.</span><span class="sxs-lookup"><span data-stu-id="52c79-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="52c79-172">Une erreur est-elle survenue ?</span><span class="sxs-lookup"><span data-stu-id="52c79-172">Did you get an error?</span></span>
<span data-ttu-id="52c79-173">Lorsque vous utilisez NPM sur certains systèmes d’exploitation, vous pouvez obtenir le message d’erreur suivant : **Error: EPERM, chmod '/usr/local/bin/..'**</span><span class="sxs-lookup"><span data-stu-id="52c79-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="52c79-174">et une suggestion que vous essayez de compte de hello en cours d’exécution en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="52c79-174">and a suggestion that you try running hello account as an administrator.</span></span> <span data-ttu-id="52c79-175">Si cela se produit, utilisez toorun de commande hello sudo NPM à un niveau de privilège supérieur.</span><span class="sxs-lookup"><span data-stu-id="52c79-175">If this occurs, use hello sudo command toorun NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="52c79-176">Une erreur relative à DTRACE est-elle survenue ?</span><span class="sxs-lookup"><span data-stu-id="52c79-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="52c79-177">Lors de l’installation de Restify, vous risquez de voir une erreur comme celle-ci :</span><span class="sxs-lookup"><span data-stu-id="52c79-177">You might see an error like this when installing Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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
<span data-ttu-id="52c79-178">Restify fournit un mécanisme puissant pour suivre les appels REST à l’aide de DTrace.</span><span class="sxs-lookup"><span data-stu-id="52c79-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="52c79-179">Toutefois, de nombreux systèmes d’exploitation ne disposent pas de DTrace.</span><span class="sxs-lookup"><span data-stu-id="52c79-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="52c79-180">Vous pouvez ignorer ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="52c79-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="52c79-181">sortie Hello de cette commande doit ressembler similaire toohello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="52c79-181">hello output of this command should look similar toohello following output:</span></span>

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
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="52c79-182">Étape 6 : installation de Passport.js dans votre API web</span><span class="sxs-lookup"><span data-stu-id="52c79-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="52c79-183">[Passport](http://passportjs.org/) est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="52c79-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="52c79-184">Flexible et modulaire, Passport peut être supprimé de manière transparente dans tooany rapides ou Restify d’application web.</span><span class="sxs-lookup"><span data-stu-id="52c79-184">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="52c79-185">Une gamme complète de stratégies prend en charge l’authentification avec un nom d’utilisateur et un mot de passe, Facebook, Twitter et bien d’autres.</span><span class="sxs-lookup"><span data-stu-id="52c79-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="52c79-186">Nous avons développé une stratégie pour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52c79-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="52c79-187">Nous installer ce module et que vous ajoutez ensuite la stratégie d’Azure Active Directory hello plug-in.</span><span class="sxs-lookup"><span data-stu-id="52c79-187">We install this module and then add hello Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="52c79-188">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** active.</span><span class="sxs-lookup"><span data-stu-id="52c79-188">From hello command line, change directories toohello **azuread** directory.</span></span>

2. <span data-ttu-id="52c79-189">tooinstall passport.js, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52c79-189">tooinstall passport.js, enter hello following command :</span></span>

    `npm install passport`

    <span data-ttu-id="52c79-190">sortie de Hello de commande hello doit ressembler similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c79-190">hello output of hello command should look similar toohello following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="52c79-191">Étape 7 : Ajouter Passport-Azure-AD tooyour web API</span><span class="sxs-lookup"><span data-stu-id="52c79-191">Step 7: Add Passport-Azure-AD tooyour web API</span></span>
<span data-ttu-id="52c79-192">Ensuite, nous ajoutons stratégie de hello OAuth à l’aide de `passport-azure-ad`, un ensemble de stratégies qui se connectent tooPassport d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52c79-192">Next we add hello OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory tooPassport.</span></span> <span data-ttu-id="52c79-193">Nous utilisons cette stratégie pour les jetons du porteur dans cet exemple d’API REST.</span><span class="sxs-lookup"><span data-stu-id="52c79-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="52c79-194">Bien qu’OAuth2 fournisse une infrastructure dans laquelle tout type de jeton connu peut être émis, seuls certains types de jeton sont couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="52c79-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="52c79-195">Jetons de support sont des jetons de hello couramment utilisé pour protéger les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="52c79-195">Bearer tokens are hello most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="52c79-196">Ils sont type hello plus largement émis de jeton dans OAuth2.</span><span class="sxs-lookup"><span data-stu-id="52c79-196">They are hello most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="52c79-197">De nombreuses implémentations supposent que les jetons de porteur hello seul type de jetons émis.</span><span class="sxs-lookup"><span data-stu-id="52c79-197">Many implementations assume that bearer tokens are hello only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="52c79-198">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** active.</span><span class="sxs-lookup"><span data-stu-id="52c79-198">From hello command line, change directories toohello **azuread** directory.</span></span>

<span data-ttu-id="52c79-199">Tapez ce qui suit hello commande tooinstall hello Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="52c79-199">Type hello following command tooinstall hello Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="52c79-200">sortie de Hello de commande hello doit ressembler similaire toohello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="52c79-200">hello output of hello command should look similar toohello following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="52c79-201">Étape 8 : Ajouter MongoDB modules tooyour web API</span><span class="sxs-lookup"><span data-stu-id="52c79-201">Step 8: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="52c79-202">Nous utilisons MongoDB comme magasin de données.</span><span class="sxs-lookup"><span data-stu-id="52c79-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="52c79-203">Pour cette raison, nous devons tooinstall hello est largement utilisé plug-in appelée Mongoose toomanage les modèles et les schémas.</span><span class="sxs-lookup"><span data-stu-id="52c79-203">For that reason, we need tooinstall hello widely used plug-in called Mongoose toomanage models and schemas.</span></span> <span data-ttu-id="52c79-204">Nous devons également le pilote de base de données tooinstall hello pour MongoDB (qui est également appelée MongoDB).</span><span class="sxs-lookup"><span data-stu-id="52c79-204">We also need tooinstall hello database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="52c79-205">Étape 9 : installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="52c79-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="52c79-206">Ensuite, nous installons hello restant modules requis.</span><span class="sxs-lookup"><span data-stu-id="52c79-206">Next we install hello remaining required modules.</span></span>

1. <span data-ttu-id="52c79-207">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="52c79-207">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="52c79-208">Entrez hello suivant de commandes tooinstall ces modules dans votre **node_modules** active :</span><span class="sxs-lookup"><span data-stu-id="52c79-208">Enter hello following commands tooinstall these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="52c79-209">Étape 10 : création d’un server.js avec vos dépendances</span><span class="sxs-lookup"><span data-stu-id="52c79-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="52c79-210">fichier de server.js Hello fournit la plupart des fonctionnalités de hello pour notre serveur d’API web.</span><span class="sxs-lookup"><span data-stu-id="52c79-210">hello server.js file provides most of hello functionality for our web API server.</span></span> <span data-ttu-id="52c79-211">Nous ajoutons la plupart de nos toothis du fichier de code.</span><span class="sxs-lookup"><span data-stu-id="52c79-211">We add most of our code toothis file.</span></span> <span data-ttu-id="52c79-212">À des fins de production, nous vous recommandons de refactoriser fonctionnalité hello en fichiers plus petits, tels que les contrôleurs et itinéraires distincts.</span><span class="sxs-lookup"><span data-stu-id="52c79-212">For production purposes, we recommend that you refactor hello functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="52c79-213">Dans cette démonstration, nous utilisons server.js pour cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="52c79-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="52c79-214">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="52c79-214">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="52c79-215">Créer un `server.js` dans votre éditeur favori et puis ajoutez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c79-215">Create a `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="52c79-216">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-216">Save hello file.</span></span> <span data-ttu-id="52c79-217">Nous allons retourner tooit peu de temps.</span><span class="sxs-lookup"><span data-stu-id="52c79-217">We'll return tooit shortly.</span></span>

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="52c79-218">Étape 11 : Créer un toostore de fichier de configuration de vos paramètres d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="52c79-218">Step 11: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="52c79-219">Ce fichier de code passe les paramètres de configuration hello depuis votre tooPassport.js portail Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52c79-219">This code file passes hello configuration parameters from your Azure Active Directory portal tooPassport.js.</span></span> <span data-ttu-id="52c79-220">Vous avez créé ces valeurs de configuration lorsque vous avez ajouté le portail de hello web API toohello dans hello première partie de procédure pas à pas hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-220">You created these configuration values when you added hello web API toohello portal in hello first part of hello walkthrough.</span></span> <span data-ttu-id="52c79-221">Nous vous expliquons quels tooput dans les valeurs hello de ces paramètres après avoir copié les code hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-221">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

1. <span data-ttu-id="52c79-222">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="52c79-222">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="52c79-223">Créer un `config.js` dans votre éditeur favori et puis ajoutez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c79-223">Create a `config.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. <span data-ttu-id="52c79-224">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-224">Save hello file.</span></span>

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a><span data-ttu-id="52c79-225">Étape 12 : Ajouter le fichier de configuration valeurs tooyour server.js</span><span class="sxs-lookup"><span data-stu-id="52c79-225">Step 12: Add configuration values tooyour server.js file</span></span>
<span data-ttu-id="52c79-226">Nous devons tooread de ces valeurs à partir du fichier .config hello que vous avez créé dans notre application.</span><span class="sxs-lookup"><span data-stu-id="52c79-226">We need tooread these values from hello .config file that you created across our application.</span></span> <span data-ttu-id="52c79-227">toodo, nous ajouter le fichier .config de hello en tant qu’une ressource requise dans notre application.</span><span class="sxs-lookup"><span data-stu-id="52c79-227">toodo this, we add hello .config file as a required resource in our application.</span></span> <span data-ttu-id="52c79-228">Ensuite, nous avons défini hello global toomatch hello des variables dans le document de config.js hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-228">Then we set hello global variables toomatch hello variables in hello config.js document.</span></span>

1. <span data-ttu-id="52c79-229">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="52c79-229">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="52c79-230">Ouvrez votre `server.js` dans votre éditeur favori et puis ajoutez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c79-230">Open your `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="52c79-231">Puis ajoutez une nouvelle section trop`server.js` avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="52c79-231">Then add a new section too`server.js` with hello following code:</span></span>

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="52c79-232">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-232">Save hello file.</span></span>

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="52c79-233">Étape 13 : Ajouter hello informations MongoDB modèle et de schéma à l’aide de Mongoose</span><span class="sxs-lookup"><span data-stu-id="52c79-233">Step 13: Add hello MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="52c79-234">Toute cette préparation va maintenant toostart rembourser que nous combiner ces trois fichiers dans un service de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="52c79-234">Now all this preparation is going toostart paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="52c79-235">Pour cette procédure pas à pas, nous utilisons MongoDB toostore notre tâches comme indiqué à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="52c79-235">For this walkthrough, we use MongoDB toostore our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="52c79-236">Bonjour `config.js` que nous avons créé à l’étape 11, nous vous avons appelé notre base de données de fichiers `tasklist`, car il s’agit de ce que nous mettre à fin hello de notre **mogoose_auth_local** URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="52c79-236">In hello `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at hello end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="52c79-237">Vous n’avez pas besoin toocreate cette base de données au préalable dans MongoDB.</span><span class="sxs-lookup"><span data-stu-id="52c79-237">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="52c79-238">Au lieu de cela, MongoDB crée cela pour nous sur hello première exécution de notre application de serveur (en supposant que cette base de données hello n’existe pas déjà).</span><span class="sxs-lookup"><span data-stu-id="52c79-238">Instead, MongoDB creates this for us on hello first run of our server application (assuming that hello database doesn't already exist).</span></span>

<span data-ttu-id="52c79-239">Maintenant que nous avons dit server de hello quelle base de données MongoDB nous aimerions toouse, nous devons toowrite certains modèles de code supplémentaire toocreate hello et un schéma pour les tâches de notre serveur.</span><span class="sxs-lookup"><span data-stu-id="52c79-239">Now that we've told hello server which MongoDB database we'd like toouse, we need toowrite some additional code toocreate hello model and schema for our server's tasks.</span></span>

### <a name="discussion-of-hello-model"></a><span data-ttu-id="52c79-240">Présentation du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="52c79-240">Discussion of hello model</span></span>
<span data-ttu-id="52c79-241">Notre modèle de schéma est simple.</span><span class="sxs-lookup"><span data-stu-id="52c79-241">Our schema model is simple.</span></span> <span data-ttu-id="52c79-242">Vous le développez en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="52c79-242">You expand it as required.</span></span>

<span data-ttu-id="52c79-243">: Hello nom de personne hello toohello tâche est affectée.</span><span class="sxs-lookup"><span data-stu-id="52c79-243">NAME: hello name of hello person who is assigned toohello task.</span></span> <span data-ttu-id="52c79-244">**Chaîne**.</span><span class="sxs-lookup"><span data-stu-id="52c79-244">A **String**.</span></span>

<span data-ttu-id="52c79-245">TÂCHE : la tâche hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="52c79-245">TASK: hello task itself.</span></span> <span data-ttu-id="52c79-246">**Chaîne**.</span><span class="sxs-lookup"><span data-stu-id="52c79-246">A **String**.</span></span>

<span data-ttu-id="52c79-247">DATE : date de hello cette tâche hello est plein.</span><span class="sxs-lookup"><span data-stu-id="52c79-247">DATE: hello date that hello task is due.</span></span> <span data-ttu-id="52c79-248">**DATEHEURE**.</span><span class="sxs-lookup"><span data-stu-id="52c79-248">A **DATETIME**.</span></span>

<span data-ttu-id="52c79-249">TERMINÉE : Si la tâche hello a été effectuée ou non.</span><span class="sxs-lookup"><span data-stu-id="52c79-249">COMPLETED: If hello task has been completed or not.</span></span> <span data-ttu-id="52c79-250">**BOOLÉEN**.</span><span class="sxs-lookup"><span data-stu-id="52c79-250">A **BOOLEAN**.</span></span>

### <a name="creating-hello-schema-in-hello-code"></a><span data-ttu-id="52c79-251">Création de schéma de hello dans du code hello</span><span class="sxs-lookup"><span data-stu-id="52c79-251">Creating hello schema in hello code</span></span>
1. <span data-ttu-id="52c79-252">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="52c79-252">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="52c79-253">Ouvrez votre `server.js` dans votre éditeur favori et puis ajoutez hello informations sous l’entrée de configuration hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c79-253">Open your `server.js` file in your favorite editor, and then add hello following information below hello configuration entry:</span></span>

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="52c79-254">Comme vous pouvez le voir à partir du code hello, nous créons notre schéma tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="52c79-254">As you can tell from hello code, we create our schema first.</span></span> <span data-ttu-id="52c79-255">Nous créons un objet de modèle que nous utilisons toostore nos données tout au long de hello le code quand nous définissons notre **itinéraires**.</span><span class="sxs-lookup"><span data-stu-id="52c79-255">Then we create a model object that we use toostore our data throughout hello code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="52c79-256">Étape 14 : ajout de nos itinéraires pour notre serveur de tâche de l’API REST</span><span class="sxs-lookup"><span data-stu-id="52c79-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="52c79-257">Maintenant que nous avons un toowork de modèle de base de données avec, vous allez ajouter des itinéraires hello nous sommes allons utiliser pour le serveur d’API REST.</span><span class="sxs-lookup"><span data-stu-id="52c79-257">Now that we have a database model toowork with, let's add hello routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="52c79-258">À propos des itinéraires dans Restify</span><span class="sxs-lookup"><span data-stu-id="52c79-258">About routes in Restify</span></span>
<span data-ttu-id="52c79-259">Fonctionnement des gammes Restify hello même façon qu’ils Bonjour Express empilent.</span><span class="sxs-lookup"><span data-stu-id="52c79-259">Routes work in Restify hello same way they do in hello Express stack.</span></span> <span data-ttu-id="52c79-260">Vous définissez des itinéraires à l’aide de hello URI que vous attendez hello client applications toocall.</span><span class="sxs-lookup"><span data-stu-id="52c79-260">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="52c79-261">En général, vous définissez vos itinéraires dans un fichier distinct.</span><span class="sxs-lookup"><span data-stu-id="52c79-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="52c79-262">Nous concerne, nous plaçons notre itinéraires dans le fichier de server.js hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-262">For our purposes, we put our routes in hello server.js file.</span></span> <span data-ttu-id="52c79-263">Nous vous recommandons de factoriser ces itinéraires dans leur propre fichier s’ils sont destinés à la production.</span><span class="sxs-lookup"><span data-stu-id="52c79-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="52c79-264">Un exemple de modèle d’un itinéraire Restify se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="52c79-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="52c79-265">Il s’agit de modèle hello à son niveau le plus simple.</span><span class="sxs-lookup"><span data-stu-id="52c79-265">This is hello pattern at its most basic level.</span></span> <span data-ttu-id="52c79-266">Restify (et Express) fournit des fonctionnalités bien plus approfondies, comme la définition de types d’application et la fourniture d’un routage complexe entre différents points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="52c79-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="52c79-267">Pour nos objectifs, nous conservons ces itinéraires simples.</span><span class="sxs-lookup"><span data-stu-id="52c79-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-tooour-server"></a><span data-ttu-id="52c79-268">Ajouter le serveur de tooour d’itinéraires par défaut</span><span class="sxs-lookup"><span data-stu-id="52c79-268">Add default routes tooour server</span></span>
<span data-ttu-id="52c79-269">Nous avons maintenant ajouter hello base CRUD itinéraires de créer, récupérer, mettre à jour et supprimer.</span><span class="sxs-lookup"><span data-stu-id="52c79-269">We now add hello basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="52c79-270">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà :</span><span class="sxs-lookup"><span data-stu-id="52c79-270">From hello command line, change directories toohello **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="52c79-271">Ouvrez hello `server.js` dans votre éditeur favori et puis ajoutez hello suivant ci-dessous hello de base de données les entrées précédentes que vous avez apportées :</span><span class="sxs-lookup"><span data-stu-id="52c79-271">Open hello `server.js` file in your favorite editor, and then add hello following information below hello previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="52c79-272">Ajouter la gestion des erreurs dans nos API</span><span class="sxs-lookup"><span data-stu-id="52c79-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="52c79-273">Étape 15 : création de votre serveur</span><span class="sxs-lookup"><span data-stu-id="52c79-273">Step 15: Create your server</span></span>
<span data-ttu-id="52c79-274">Nous avons défini notre base de données et nos itinéraires sont en place.</span><span class="sxs-lookup"><span data-stu-id="52c79-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="52c79-275">Hello dernière chose toodo est ajouter l’instance de serveur hello qui gère les appels.</span><span class="sxs-lookup"><span data-stu-id="52c79-275">hello last thing toodo is add hello server instance that manages our calls.</span></span>

<span data-ttu-id="52c79-276">Restify (et Express), vous pouvez effectuer un grand nombre de personnalisation pour un serveur d’API REST, mais à nouveau, nous allons le programme d’installation toouse hello plus simple pour nos besoins.</span><span class="sxs-lookup"><span data-stu-id="52c79-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going toouse hello most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a><span data-ttu-id="52c79-277">Étape 16 : Ajouter le serveur de toohello hello itinéraires (sans authentification pour l’instant)</span><span class="sxs-lookup"><span data-stu-id="52c79-277">Step 16: Add hello routes toohello server (without authentication for now)</span></span>
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a><span data-ttu-id="52c79-278">Étape 17 : Exécuter un serveur hello (avant d’ajouter la prise en charge OAuth)</span><span class="sxs-lookup"><span data-stu-id="52c79-278">Step 17: Run hello server (before adding OAuth support)</span></span>
<span data-ttu-id="52c79-279">Testez votre serveur avant d’ajouter l’authentification.</span><span class="sxs-lookup"><span data-stu-id="52c79-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="52c79-280">tootest de façon plus simple de Hello votre serveur est à l’aide de curl dans une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="52c79-280">hello easiest way tootest your server is by using curl in a command line.</span></span> <span data-ttu-id="52c79-281">Avant cela, nous avons besoin d’un utilitaire qui permet de sortie tooparse au format JSON.</span><span class="sxs-lookup"><span data-stu-id="52c79-281">Before we do that, we need a utility that allows us tooparse output as JSON.</span></span>

1. <span data-ttu-id="52c79-282">Installez hello suivant outil JSON (tous les hello exemple suivant permet d’utiliser cet outil) :</span><span class="sxs-lookup"><span data-stu-id="52c79-282">Install hello following JSON tool (all hello following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="52c79-283">Cette commande installe outil JSON hello globalement.</span><span class="sxs-lookup"><span data-stu-id="52c79-283">This installs hello JSON tool globally.</span></span> <span data-ttu-id="52c79-284">Maintenant que nous avons accompli qui, nous allons lire avec un serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="52c79-284">Now that we’ve accomplished that, let’s play with hello server:</span></span>

2. <span data-ttu-id="52c79-285">Vérifiez tout d’abord que votre instance mongoDB est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="52c79-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="52c79-286">Ensuite, basculez de toohello et démarrer curling :</span><span class="sxs-lookup"><span data-stu-id="52c79-286">Then, change toohello directory and start curling:</span></span>

    <span data-ttu-id="52c79-287">`$ cd azuread``$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="52c79-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. <span data-ttu-id="52c79-288">Nous pouvons à présent ajouter une tâche de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="52c79-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="52c79-289">réponse de Hello doit être :</span><span class="sxs-lookup"><span data-stu-id="52c79-289">hello response should be:</span></span>

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
    <span data-ttu-id="52c79-290">Et nous pouvons répertorier des tâches pour Brandon de cette manière :</span><span class="sxs-lookup"><span data-stu-id="52c79-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="52c79-291">Si tout cela fonctionne, nous sommes le serveur d’API REST toohello tooadd prêt OAuth.</span><span class="sxs-lookup"><span data-stu-id="52c79-291">If all this works, we're ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="52c79-292">Vous avez un serveur d’API REST avec MongoDB !</span><span class="sxs-lookup"><span data-stu-id="52c79-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-tooour-rest-api-server"></a><span data-ttu-id="52c79-293">Étape 18 : Ajouter le serveur d’authentification tooour API REST</span><span class="sxs-lookup"><span data-stu-id="52c79-293">Step 18: Add authentication tooour REST API server</span></span>
<span data-ttu-id="52c79-294">Maintenant que nous disposons d’une API REST en cours d’exécution, commençons à l’utiliser avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52c79-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="52c79-295">À partir de la ligne de commande hello, modifiez les répertoires toohello **organisation** dossier si vous n’êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="52c79-295">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="52c79-296">Utilisez hello OIDCBearerStrategy qui est inclus avec passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="52c79-296">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="52c79-297">Jusqu’à présent, nous avons créé un serveur REST TODO standard ne disposant d’aucune autorisation.</span><span class="sxs-lookup"><span data-stu-id="52c79-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="52c79-298">Nous allons commencer à tout rassembler.</span><span class="sxs-lookup"><span data-stu-id="52c79-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="52c79-299">Tout d’abord, nous devons tooindicate que nous souhaitons toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="52c79-299">First, we need tooindicate that we want toouse Passport.</span></span> <span data-ttu-id="52c79-300">Placez cela juste après la configuration de l’autre serveur :</span><span class="sxs-lookup"><span data-stu-id="52c79-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="52c79-301">Lorsque vous écrivez API, nous vous recommandons de toujours lier hello toosomething de données unique à partir du jeton hello qui hello utilisateur ne peut pas usurper l’identité.</span><span class="sxs-lookup"><span data-stu-id="52c79-301">When you write APIs, we recommend that you always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="52c79-302">Lorsque ce serveur stocke des éléments de tâche, il les stocke en fonction de l’ID d’objet hello d’utilisateur hello dans le jeton hello (appelé via token.oid), que nous avons dans le champ « propriétaire » de hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-302">When this server stores TODO items, it stores them based on hello object ID of hello user in hello token (called through token.oid), which we put in hello “owner” field.</span></span> <span data-ttu-id="52c79-303">Cela permet de s’assurer que seul cet utilisateur peut accéder à ses éléments TODO.</span><span class="sxs-lookup"><span data-stu-id="52c79-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="52c79-304">Il n’aucune exposition Bonjour API de « propriétaire », un utilisateur externe peut demander hello TODOs autres même s’ils sont authentifiés.</span><span class="sxs-lookup"><span data-stu-id="52c79-304">There is no exposure in hello API of “owner,” so an external user can request hello TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="52c79-305">Suivant nous allons utiliser la stratégie de support hello fourni avec `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="52c79-305">Next let’s use hello bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="52c79-306">Recherchez le code hello pour le moment et nous expliquerons rest de hello peu de temps.</span><span class="sxs-lookup"><span data-stu-id="52c79-306">Look at hello code for now and we'll explain hello rest shortly.</span></span> <span data-ttu-id="52c79-307">Placez ceci après ce que vous avez collé ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="52c79-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="52c79-308">Passport utilise un modèle semblable pour toutes ses stratégies (Twitter, Facebook, etc.), que respectent tous les enregistreurs de stratégie.</span><span class="sxs-lookup"><span data-stu-id="52c79-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="52c79-309">Stratégie de hello, vous constatez que nous transmettons une fonction qui a un jeton et un terminé en tant que paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-309">Looking at hello strategy, you see we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="52c79-310">stratégie de Hello est fourni dans toous une fois qu’il effectue son travail.</span><span class="sxs-lookup"><span data-stu-id="52c79-310">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="52c79-311">Une fois que c’est le cas nous stockons les utilisateur hello et jeton de hello dissimulation donc nous ne devons tooask pour celle-ci à nouveau.</span><span class="sxs-lookup"><span data-stu-id="52c79-311">After it does, we store hello user and stash hello token so we won’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52c79-312">code de précédent Hello prend tout utilisateur qui se produit tooauthenticate tooour server.</span><span class="sxs-lookup"><span data-stu-id="52c79-312">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="52c79-313">C’est ce qu’on appelle l’enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="52c79-313">This is known as auto-registration.</span></span> <span data-ttu-id="52c79-314">Dans les serveurs de production, nous vous recommandons de faire passer toute personne qui essaie de se connecter par un processus d’inscription de votre choix.</span><span class="sxs-lookup"><span data-stu-id="52c79-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="52c79-315">Il s’agit généralement de modèle hello que vous voyez dans les applications consommateur, ce qui vous permettent tooregister avec Facebook, mais vous demander de toofill des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="52c79-315">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="52c79-316">Si ce n’était pas un programme de ligne de commande, nous avons extrait par courrier électronique hello à partir de l’objet du jeton hello qui est retourné et demandé toofill d’utilisateur hello des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="52c79-316">If this wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="52c79-317">Comme il s’agit d’un serveur de test, nous avons simplement ajouter toohello base de données.</span><span class="sxs-lookup"><span data-stu-id="52c79-317">Because this is a test server, we simply add them toohello in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="52c79-318">Protéger certains points de terminaison</span><span class="sxs-lookup"><span data-stu-id="52c79-318">Protect some endpoints</span></span>
<span data-ttu-id="52c79-319">Protéger les points de terminaison en spécifiant hello `passport.authenticate()` appel avec le protocole de hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="52c79-319">You protect endpoints by specifying hello `passport.authenticate()` call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="52c79-320">toomake notre code de serveur faire quelque chose plus intéressant, nous allons modifier un itinéraire hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-320">toomake our server code do something more interesting, let’s edit hello route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="52c79-321">Étape 19 : ré-exécution de votre application serveur et contrôle du rejet</span><span class="sxs-lookup"><span data-stu-id="52c79-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="52c79-322">Nous allons utiliser `curl` toosee à nouveau si vous disposez à présent OAuth2 protection par rapport à ses points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="52c79-322">Let's use `curl` again toosee if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="52c79-323">Nous faisons ce contrôle avant d’exécuter l’un de nos Kits de développement logiciel (SDK) clients sur ce point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="52c79-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="52c79-324">Hello en-têtes retournés doivent être suffisamment tootell nous si nous allons vers le bas du chemin d’accès correct de hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-324">hello headers that are returned should be enough tootell us if we're going down hello right path.</span></span>

1. <span data-ttu-id="52c79-325">Vérifiez tout d’abord que votre instance mongoDB est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="52c79-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="52c79-326">Ensuite, basculez de toohello et former une boucle.</span><span class="sxs-lookup"><span data-stu-id="52c79-326">Then, change toohello directory and start curling.</span></span>

      <span data-ttu-id="52c79-327">`$ cd azuread``$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="52c79-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="52c79-328">Essayez une commande basique, comme POST.</span><span class="sxs-lookup"><span data-stu-id="52c79-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="52c79-329">Une erreur 401 est réponse hello que vous cherchez ici.</span><span class="sxs-lookup"><span data-stu-id="52c79-329">A 401 is hello response you are looking for here.</span></span> <span data-ttu-id="52c79-330">Cette réponse indique que cette couche de Passport hello tente de point de terminaison tooredirect toohello autorisé, qui est exactement ce que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="52c79-330">This response indicates that hello Passport layer is trying tooredirect toohello authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52c79-331">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52c79-331">Next steps</span></span>
<span data-ttu-id="52c79-332">Vous êtes allé aussi loin que possible avec ce serveur sans utiliser un client compatible OAuth2.</span><span class="sxs-lookup"><span data-stu-id="52c79-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="52c79-333">Vous devez toogo via une procédure pas à pas supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="52c79-333">You will need toogo through an additional walkthrough.</span></span>

<span data-ttu-id="52c79-334">Vous savez maintenant comment tooimplement une API REST à l’aide de Restify et OAuth2.</span><span class="sxs-lookup"><span data-stu-id="52c79-334">You've now learned how tooimplement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="52c79-335">Vous avez également plus que suffisante tookeep code développement de votre service et à l’apprentissage comment toobuild dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="52c79-335">You also have more than enough code tookeep developing your service and learning how toobuild on this example.</span></span>

<span data-ttu-id="52c79-336">Si vous êtes intéressé par les étapes suivantes hello dans votre parcours de la bibliothèque ADAL, Voici certains clients pris en charge ADAL, nous recommandons que vous conservez à travailler avec.</span><span class="sxs-lookup"><span data-stu-id="52c79-336">If you are interested in hello next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="52c79-337">Cloner la machine de développement tooyour et le configurer comme décrit dans la procédure pas à pas hello.</span><span class="sxs-lookup"><span data-stu-id="52c79-337">Clone down tooyour developer machine and configure as described in hello walkthrough.</span></span>

[<span data-ttu-id="52c79-338">Bibliothèque ADAL pour iOS</span><span class="sxs-lookup"><span data-stu-id="52c79-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="52c79-339">Bibliothèque ADAL pour Android</span><span class="sxs-lookup"><span data-stu-id="52c79-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
