---
title: "Prise en main d’Azure AD Node.js | Microsoft Docs"
description: "Création d’une API web REST Node.js qui s’intègre à Azure AD pour l’authentification."
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
ms.openlocfilehash: 4f58177f540c14172d7ece8b4bc8c8a2b9787f8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="312e1-103">Prise en main d’API web pour Node.js</span><span class="sxs-lookup"><span data-stu-id="312e1-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="312e1-104">*Passport* est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="312e1-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="312e1-105">Flexible et modulaire, Passport peut discrètement intervenir dans n’importe quelle application web basée sur Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="312e1-105">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="312e1-106">Une gamme complète de stratégies prend en charge l’authentification avec un nom d’utilisateur et un mot de passe, Facebook, Twitter et bien d’autres.</span><span class="sxs-lookup"><span data-stu-id="312e1-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="312e1-107">Nous avons développé une stratégie pour Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="312e1-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="312e1-108">Nous installons ce module, puis nous y ajoutons le plug-in `passport-azure-ad` Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="312e1-108">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="312e1-109">Pour cela, vous devez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="312e1-109">To do this, you need to:</span></span>

1. <span data-ttu-id="312e1-110">inscrivez une application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="312e1-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="312e1-111">configurez votre application pour utiliser le plug-in `passport-azure-ad` Passport ;</span><span class="sxs-lookup"><span data-stu-id="312e1-111">Set up your app to use Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="312e1-112">configurez une application cliente pour appeler l’API web To Do List.</span><span class="sxs-lookup"><span data-stu-id="312e1-112">Configure a client application to call the To Do List web API.</span></span>

<span data-ttu-id="312e1-113">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="312e1-113">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="312e1-114">Cet article ne couvre pas l’implémentation de la connexion, de l’inscription ou de la gestion de profil avec Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="312e1-114">This article doesn't cover how to implement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="312e1-115">Il s'intéresse principalement à l'appel d'API web après que l'utilisateur s'est authentifié.</span><span class="sxs-lookup"><span data-stu-id="312e1-115">It focuses on calling web APIs after the user is already authenticated.</span></span>  <span data-ttu-id="312e1-116">Nous recommandons de commencer par le document [How to integrate with Azure Active Directory](active-directory-how-to-integrate.md) (Intégration à Azure Active Directory) pour en savoir plus sur les notions de base d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="312e1-116">We recommend that you start with [How to integrate with Azure Active Directory document](active-directory-how-to-integrate.md) to learn about the basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="312e1-117">Nous avons publié tout le code source de cet exemple dans GitHub sous une licence MIT. N’hésitez pas à cloner (ou mieux, à répliquer), à commenter et à soumettre des demandes d’extraction.</span><span class="sxs-lookup"><span data-stu-id="312e1-117">We've released all the source code for this running example in GitHub under an MIT license, so feel free to clone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="312e1-118">À propos des modules Node.js</span><span class="sxs-lookup"><span data-stu-id="312e1-118">About Node.js modules</span></span>
<span data-ttu-id="312e1-119">Nous utilisons des modules Node.js au cours de cette procédure détaillée.</span><span class="sxs-lookup"><span data-stu-id="312e1-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="312e1-120">Les modules sont des packages JavaScript chargeables qui fournissent une fonctionnalité spécifique à votre application.</span><span class="sxs-lookup"><span data-stu-id="312e1-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="312e1-121">Vous installez généralement des modules à l’aide de Node.js, un outil de ligne de commande NPM dans le répertoire d’installation NPM.</span><span class="sxs-lookup"><span data-stu-id="312e1-121">You usually install modules by using the Node.js an NPM command-line tool in the NPM installation directory.</span></span> <span data-ttu-id="312e1-122">Toutefois, certains modules, comme le module HTTP, sont inclus dans le package Node.js principal.</span><span class="sxs-lookup"><span data-stu-id="312e1-122">However, some modules, such as the HTTP module, are included in the core Node.js package.</span></span>

<span data-ttu-id="312e1-123">Les modules installés sont stockés dans le répertoire **node_modules**, à la racine de votre répertoire Node.js.</span><span class="sxs-lookup"><span data-stu-id="312e1-123">Installed modules are saved in the **node_modules** directory at the root of your Node.js installation directory.</span></span> <span data-ttu-id="312e1-124">Chaque module du répertoire **node_modules** conserve son propre répertoire **node_modules** qui contient tous les modules dont il dépend.</span><span class="sxs-lookup"><span data-stu-id="312e1-124">Each module in the **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="312e1-125">Chaque module requis dispose également de son propre répertoire **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="312e1-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="312e1-126">Cette structure de répertoire récursive représente la chaîne de dépendance.</span><span class="sxs-lookup"><span data-stu-id="312e1-126">This recursive directory structure represents the dependency chain.</span></span>

<span data-ttu-id="312e1-127">Cette structure de chaîne de dépendance augmente l’encombrement de l’application.</span><span class="sxs-lookup"><span data-stu-id="312e1-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="312e1-128">Mais elle garantit également que toutes les dépendances sont satisfaites et que la version des modules utilisée dans le développement est également utilisée en production.</span><span class="sxs-lookup"><span data-stu-id="312e1-128">But it also guarantees that all dependencies are met and that the version of the modules that's used in development is also used in production.</span></span> <span data-ttu-id="312e1-129">Le comportement de l’application de production est ainsi plus prévisible et cela évite les problèmes de version pouvant affecter les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="312e1-129">This makes the production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="312e1-130">Étape 1 : inscription d’un client Azure AD</span><span class="sxs-lookup"><span data-stu-id="312e1-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="312e1-131">Pour utiliser cet exemple, vous avez besoin d’un client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="312e1-131">To use this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="312e1-132">Si vous n’êtes pas sûr de ce qu’est un locataire ou si vous ne savez pas comment en obtenir un, consultez la page [Obtention d’un client Azure Active Directory](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="312e1-132">If you're not sure what a tenant is or how to get one, see [How to get an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="312e1-133">Étape 2 : création d’une application</span><span class="sxs-lookup"><span data-stu-id="312e1-133">Step 2: Create an application</span></span>
<span data-ttu-id="312e1-134">Vous créez ensuite dans votre répertoire une application fournissant à Azure AD les informations nécessaires pour communiquer de manière sécurisée avec votre application.</span><span class="sxs-lookup"><span data-stu-id="312e1-134">Next you create an app in your directory that gives Azure AD information that it needs to securely communicate with your app.</span></span>  <span data-ttu-id="312e1-135">L’application cliente et l’API web sont toutes les deux représentées par un seul **ID d’application** dans ce cas, car elles constituent une application logique.</span><span class="sxs-lookup"><span data-stu-id="312e1-135">Both the client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="312e1-136">Pour créer une application, suivez [ces instructions](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="312e1-136">To create an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="312e1-137">Si vous générez une application métier, [ces instructions supplémentaires peuvent être utiles](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="312e1-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="312e1-138">Pour créer une application :</span><span class="sxs-lookup"><span data-stu-id="312e1-138">To create an application:</span></span>

1. <span data-ttu-id="312e1-139">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="312e1-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="312e1-140">Dans le menu supérieur, sélectionnez votre compte.</span><span class="sxs-lookup"><span data-stu-id="312e1-140">On the top menu, select your account.</span></span> <span data-ttu-id="312e1-141">Puis, dans la liste **Répertoire**, choisissez le client Active Directory auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="312e1-141">Then, under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="312e1-142">Dans le menu à gauche, sélectionnez **Plus de services**, puis **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="312e1-142">In the menu on the left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="312e1-143">Sélectionnez **Inscriptions d’applications**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="312e1-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="312e1-144">Suivez les invites pour créer une **application web et/ou une API web**.</span><span class="sxs-lookup"><span data-stu-id="312e1-144">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="312e1-145">Le **nom** de l’application doit décrire votre application aux utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="312e1-145">The **name** of the application describes your application to end users.</span></span>

      * <span data-ttu-id="312e1-146">L’ **URL de connexion** est l’URL de base de votre application.</span><span class="sxs-lookup"><span data-stu-id="312e1-146">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="312e1-147">L’URL par défaut de l’exemple de code est `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="312e1-147">The default URL of the sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="312e1-148">Une fois l’application enregistrée, Azure AD lui affecte un ID d’application unique.</span><span class="sxs-lookup"><span data-stu-id="312e1-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="312e1-149">Copiez cette valeur à partir de la page de l’application, car vous en aurez besoin dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="312e1-149">You need this value in the next sections, so copy it from the application page.</span></span>

7. <span data-ttu-id="312e1-150">À partir de la page **Paramètres** -> **Propriétés** de votre application, mettez à jour l’URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="312e1-150">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="312e1-151">Un **URI ID d’application** est un identificateur unique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="312e1-151">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="312e1-152">L’usage est d’utiliser `https://<tenant-domain>/<app-name>`, par exemple : `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="312e1-152">The convention is to use `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="312e1-153">Créez une **clé** pour votre application dans la page **Paramètres** et notez-la.</span><span class="sxs-lookup"><span data-stu-id="312e1-153">Create a **Key** for your application from the **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="312e1-154">Vous en aurez besoin rapidement.</span><span class="sxs-lookup"><span data-stu-id="312e1-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="312e1-155">Étape 3 : téléchargement de Node.js pour votre plateforme</span><span class="sxs-lookup"><span data-stu-id="312e1-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="312e1-156">Pour réussir à utiliser cet exemple, Node.js doit être installé correctement.</span><span class="sxs-lookup"><span data-stu-id="312e1-156">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="312e1-157">Installez Node.js à partir de l’adresse suivante : [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="312e1-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="312e1-158">Étape 4 : installation de MongoDB sur votre plateforme</span><span class="sxs-lookup"><span data-stu-id="312e1-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="312e1-159">Pour réussir à utiliser cet exemple, MongoDB doit être installé correctement.</span><span class="sxs-lookup"><span data-stu-id="312e1-159">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="312e1-160">Vous utilisez MongoDB afin que votre API REST soit persistante sur les instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="312e1-160">You use MongoDB to make the REST API persistent across server instances.</span></span>

<span data-ttu-id="312e1-161">Installez MongoDB à partir de l’adresse suivante : [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="312e1-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="312e1-162">Cette procédure détaillée suppose que vous utilisez l’installation et les points de terminaison du serveur par défaut pour MongoDB, c’est-à-dire les suivants au moment de la rédaction : mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="312e1-162">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="312e1-163">Étape 5 : installation des modules Restify sur votre API web</span><span class="sxs-lookup"><span data-stu-id="312e1-163">Step 5: Install the Restify modules in your web API</span></span>
<span data-ttu-id="312e1-164">Nous utilisons Restify pour concevoir notre API REST.</span><span class="sxs-lookup"><span data-stu-id="312e1-164">We are using Restify to build our REST API.</span></span> <span data-ttu-id="312e1-165">Restify est une infrastructure d’application Node.js minimale et flexible qui est dérivée d’Express.</span><span class="sxs-lookup"><span data-stu-id="312e1-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="312e1-166">Elle inclut un ensemble complet de fonctionnalités de création API REST sur Connect.</span><span class="sxs-lookup"><span data-stu-id="312e1-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="312e1-167">Installation de Restify</span><span class="sxs-lookup"><span data-stu-id="312e1-167">Install Restify</span></span>
1. <span data-ttu-id="312e1-168">Depuis la ligne de commande, accédez au répertoire **azuread**.</span><span class="sxs-lookup"><span data-stu-id="312e1-168">From the command line, change directories to the **azuread** directory.</span></span> <span data-ttu-id="312e1-169">Si le répertoire **azuread** n’existe pas, créez-le.</span><span class="sxs-lookup"><span data-stu-id="312e1-169">If the **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="312e1-170">Tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="312e1-170">Type the following command:</span></span>

    `npm install restify`

    <span data-ttu-id="312e1-171">Cette commande permet d’installer Restify.</span><span class="sxs-lookup"><span data-stu-id="312e1-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="312e1-172">Une erreur est-elle survenue ?</span><span class="sxs-lookup"><span data-stu-id="312e1-172">Did you get an error?</span></span>
<span data-ttu-id="312e1-173">Lorsque vous utilisez NPM sur certains systèmes d’exploitation, vous pouvez obtenir le message d’erreur suivant : **Error: EPERM, chmod '/usr/local/bin/..'**</span><span class="sxs-lookup"><span data-stu-id="312e1-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="312e1-174">et la suggestion d’essayer d’exécuter le compte en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="312e1-174">and a suggestion that you try running the account as an administrator.</span></span> <span data-ttu-id="312e1-175">Si cette erreur survient, utilisez la commande sudo pour exécuter NPM avec des privilèges plus élevés.</span><span class="sxs-lookup"><span data-stu-id="312e1-175">If this occurs, use the sudo command to run NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="312e1-176">Une erreur relative à DTRACE est-elle survenue ?</span><span class="sxs-lookup"><span data-stu-id="312e1-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="312e1-177">Lors de l’installation de Restify, vous risquez de voir une erreur comme celle-ci :</span><span class="sxs-lookup"><span data-stu-id="312e1-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="312e1-178">Restify fournit un mécanisme puissant pour suivre les appels REST à l’aide de DTrace.</span><span class="sxs-lookup"><span data-stu-id="312e1-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="312e1-179">Toutefois, de nombreux systèmes d’exploitation ne disposent pas de DTrace.</span><span class="sxs-lookup"><span data-stu-id="312e1-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="312e1-180">Vous pouvez ignorer ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="312e1-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="312e1-181">Le résultat de cette commande doit ressembler au résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="312e1-181">The output of this command should look similar to the following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="312e1-182">Étape 6 : installation de Passport.js dans votre API web</span><span class="sxs-lookup"><span data-stu-id="312e1-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="312e1-183">[Passport](http://passportjs.org/) est un intergiciel d’authentification pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="312e1-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="312e1-184">Flexible et modulaire, Passport peut discrètement intervenir dans n’importe quelle application web basée sur Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="312e1-184">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="312e1-185">Une gamme complète de stratégies prend en charge l’authentification avec un nom d’utilisateur et un mot de passe, Facebook, Twitter et bien d’autres.</span><span class="sxs-lookup"><span data-stu-id="312e1-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="312e1-186">Nous avons développé une stratégie pour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="312e1-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="312e1-187">Nous installons ce module, puis nous y ajoutons le plug-in stratégique Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="312e1-187">We install this module and then add the Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="312e1-188">Depuis la ligne de commande, accédez au répertoire **azuread**.</span><span class="sxs-lookup"><span data-stu-id="312e1-188">From the command line, change directories to the **azuread** directory.</span></span>

2. <span data-ttu-id="312e1-189">Pour installer passport.js, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="312e1-189">To install passport.js, enter the following command :</span></span>

    `npm install passport`

    <span data-ttu-id="312e1-190">Le résultat de la commande doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="312e1-190">The output of the command should look similar to the following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="312e1-191">Étape 7 : ajout de Passport-Azure-AD à votre API web</span><span class="sxs-lookup"><span data-stu-id="312e1-191">Step 7: Add Passport-Azure-AD to your web API</span></span>
<span data-ttu-id="312e1-192">Nous ajoutons alors la stratégie OAuth à l’aide de `passport-azure-ad`, une suite de stratégies qui connectent Azure Active Directory à Passport.</span><span class="sxs-lookup"><span data-stu-id="312e1-192">Next we add the OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory to Passport.</span></span> <span data-ttu-id="312e1-193">Nous utilisons cette stratégie pour les jetons du porteur dans cet exemple d’API REST.</span><span class="sxs-lookup"><span data-stu-id="312e1-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="312e1-194">Bien qu’OAuth2 fournisse une infrastructure dans laquelle tout type de jeton connu peut être émis, seuls certains types de jeton sont couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="312e1-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="312e1-195">Les jetons du porteur sont les jetons les plus couramment utilisés pour la protection des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="312e1-195">Bearer tokens are the most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="312e1-196">Il s’agit du type de jeton le plus fréquemment émis dans OAuth2.</span><span class="sxs-lookup"><span data-stu-id="312e1-196">They are the most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="312e1-197">De nombreuses implémentations partent du principe qu’il s’agit du seul type de jeton émis.</span><span class="sxs-lookup"><span data-stu-id="312e1-197">Many implementations assume that bearer tokens are the only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="312e1-198">Depuis la ligne de commande, accédez au répertoire **azuread**.</span><span class="sxs-lookup"><span data-stu-id="312e1-198">From the command line, change directories to the **azuread** directory.</span></span>

<span data-ttu-id="312e1-199">Saisissez la commande suivante pour installer le Passport.js `passport-azure-ad module` :</span><span class="sxs-lookup"><span data-stu-id="312e1-199">Type the following command to install the Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="312e1-200">Le résultat de la commande doit ressembler au résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="312e1-200">The output of the command should look similar to the following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="312e1-201">Étape 8 : ajout des modules MongoDB à votre API web</span><span class="sxs-lookup"><span data-stu-id="312e1-201">Step 8: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="312e1-202">Nous utilisons MongoDB comme magasin de données.</span><span class="sxs-lookup"><span data-stu-id="312e1-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="312e1-203">Pour cette raison, nous devons installer le plug-in largement utilisé appelé Mongoose pour gérer les modèles et schémas.</span><span class="sxs-lookup"><span data-stu-id="312e1-203">For that reason, we need to install the widely used plug-in called Mongoose to manage models and schemas.</span></span> <span data-ttu-id="312e1-204">Nous devons également installer le pilote de base de données de MongoDB (qui est également appelé MongoDB).</span><span class="sxs-lookup"><span data-stu-id="312e1-204">We also need to install the database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="312e1-205">Étape 9 : installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="312e1-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="312e1-206">Ensuite, nous installons les autres modules requis.</span><span class="sxs-lookup"><span data-stu-id="312e1-206">Next we install the remaining required modules.</span></span>

1. <span data-ttu-id="312e1-207">Depuis la ligne de commande, accédez au dossier **azuread** si vous n’y êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="312e1-207">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="312e1-208">Entrez les commandes suivantes pour installer ces modules dans le répertoire **node_modules** :</span><span class="sxs-lookup"><span data-stu-id="312e1-208">Enter the following commands to install these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="312e1-209">Étape 10 : création d’un server.js avec vos dépendances</span><span class="sxs-lookup"><span data-stu-id="312e1-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="312e1-210">Le fichier server.js fournit la plupart des fonctionnalités de notre serveur d’API web.</span><span class="sxs-lookup"><span data-stu-id="312e1-210">The server.js file provides most of the functionality for our web API server.</span></span> <span data-ttu-id="312e1-211">Nous ajoutons la plupart du code à ce fichier.</span><span class="sxs-lookup"><span data-stu-id="312e1-211">We add most of our code to this file.</span></span> <span data-ttu-id="312e1-212">À des fins de production, nous vous recommandons de refactoriser la fonctionnalité en fichiers plus petits, par exemple des itinéraires et des contrôleurs distincts.</span><span class="sxs-lookup"><span data-stu-id="312e1-212">For production purposes, we recommend that you refactor the functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="312e1-213">Dans cette démonstration, nous utilisons server.js pour cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="312e1-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="312e1-214">Depuis la ligne de commande, accédez au dossier **azuread** si vous n’y êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="312e1-214">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="312e1-215">Créez un fichier `server.js` dans votre éditeur favori, puis ajoutez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="312e1-215">Create a `server.js` file in your favorite editor, and then add the following information:</span></span>

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

3. <span data-ttu-id="312e1-216">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="312e1-216">Save the file.</span></span> <span data-ttu-id="312e1-217">Nous y reviendrons rapidement.</span><span class="sxs-lookup"><span data-stu-id="312e1-217">We'll return to it shortly.</span></span>

## <a name="step-11-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="312e1-218">Étape 11 : création d’un fichier de configuration pour stocker vos paramètres Azure AD</span><span class="sxs-lookup"><span data-stu-id="312e1-218">Step 11: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="312e1-219">Ce fichier de code transmet les paramètres de configuration de votre portail Azure Active Directory vers Passport.js.</span><span class="sxs-lookup"><span data-stu-id="312e1-219">This code file passes the configuration parameters from your Azure Active Directory portal to Passport.js.</span></span> <span data-ttu-id="312e1-220">Vous avez créé ces valeurs de configuration lorsque vous avez ajouté l’API web au portail, dans la première partie de la procédure détaillée.</span><span class="sxs-lookup"><span data-stu-id="312e1-220">You created these configuration values when you added the web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="312e1-221">Copiez le code. Après quoi, nous vous expliquerons ce qu’il convient de placer dans les valeurs de ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="312e1-221">We explain what to put in the values of these parameters after you copy the code.</span></span>

1. <span data-ttu-id="312e1-222">Depuis la ligne de commande, accédez au dossier **azuread** si vous n’y êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="312e1-222">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="312e1-223">Créez un fichier `config.js` dans votre éditeur favori, puis ajoutez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="312e1-223">Create a `config.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in to your server unless you use the common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in to your server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes to stderr in Unix.

         };
    ```
3. <span data-ttu-id="312e1-224">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="312e1-224">Save the file.</span></span>

## <a name="step-12-add-configuration-values-to-your-serverjs-file"></a><span data-ttu-id="312e1-225">Étape 12 : ajout de valeurs de configuration à votre fichier server.js</span><span class="sxs-lookup"><span data-stu-id="312e1-225">Step 12: Add configuration values to your server.js file</span></span>
<span data-ttu-id="312e1-226">Nous avons besoin de lire ces valeurs dans le fichier .config que vous avez créé dans notre application.</span><span class="sxs-lookup"><span data-stu-id="312e1-226">We need to read these values from the .config file that you created across our application.</span></span> <span data-ttu-id="312e1-227">Pour cela, nous ajoutons le fichier .config en tant que ressource requise dans notre application.</span><span class="sxs-lookup"><span data-stu-id="312e1-227">To do this, we add the .config file as a required resource in our application.</span></span> <span data-ttu-id="312e1-228">Nous définissons ensuite les variables globales pour qu’elles correspondent aux variables dans le document config.js.</span><span class="sxs-lookup"><span data-stu-id="312e1-228">Then we set the global variables to match the variables in the config.js document.</span></span>

1. <span data-ttu-id="312e1-229">Depuis la ligne de commande, accédez au dossier **azuread** si vous n’y êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="312e1-229">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="312e1-230">Ouvrez votre fichier `server.js` dans votre éditeur favori, puis ajoutez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="312e1-230">Open your `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="312e1-231">Ensuite, ajoutez une nouvelle section à `server.js` avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="312e1-231">Then add a new section to `server.js` with the following code:</span></span>

    ```Javascript
    var options = {
        // The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array to hold logged in users and the current logged in user (owner).
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

      // If the logging level is specified, switch to it.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="312e1-232">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="312e1-232">Save the file.</span></span>

## <a name="step-13-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="312e1-233">Étape 13 : ajout des informations du modèle et du schéma MongoDB à l’aide de Mongoose</span><span class="sxs-lookup"><span data-stu-id="312e1-233">Step 13: Add The MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="312e1-234">Toute cette préparation va maintenant prouver son utilité : associons ces trois fichiers dans un service API REST.</span><span class="sxs-lookup"><span data-stu-id="312e1-234">Now all this preparation is going to start paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="312e1-235">Pour cette procédure détaillée, nous utilisons MongoDB pour stocker les tâches, comme indiqué dans l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="312e1-235">For this walkthrough, we use MongoDB to store our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="312e1-236">Dans le fichier `config.js` que nous avons créé dans l’étape 11, nous avons appelé notre base de données `tasklist`, car c’était ce que nous avions placé à la fin de l’URL de connexion **mogoose_auth_local**.</span><span class="sxs-lookup"><span data-stu-id="312e1-236">In the `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at the end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="312e1-237">Vous n’avez pas besoin de créer cette base de données au préalable dans MongoDB.</span><span class="sxs-lookup"><span data-stu-id="312e1-237">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="312e1-238">MongoDB le fait pour nous au moment de la première exécution de l’application serveur (en supposant que la base de données n’existe pas déjà).</span><span class="sxs-lookup"><span data-stu-id="312e1-238">Instead, MongoDB creates this for us on the first run of our server application (assuming that the database doesn't already exist).</span></span>

<span data-ttu-id="312e1-239">Maintenant que nous avons indiqué au serveur quelle base de données MongoDB nous souhaitons utiliser, nous devons écrire du code supplémentaire pour créer le modèle et le schéma pour les tâches du serveur.</span><span class="sxs-lookup"><span data-stu-id="312e1-239">Now that we've told the server which MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's tasks.</span></span>

### <a name="discussion-of-the-model"></a><span data-ttu-id="312e1-240">Considérations sur le modèle</span><span class="sxs-lookup"><span data-stu-id="312e1-240">Discussion of the model</span></span>
<span data-ttu-id="312e1-241">Notre modèle de schéma est simple.</span><span class="sxs-lookup"><span data-stu-id="312e1-241">Our schema model is simple.</span></span> <span data-ttu-id="312e1-242">Vous le développez en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="312e1-242">You expand it as required.</span></span>

<span data-ttu-id="312e1-243">NOM : le nom de la personne à qui la tâche est assignée.</span><span class="sxs-lookup"><span data-stu-id="312e1-243">NAME: The name of the person who is assigned to the task.</span></span> <span data-ttu-id="312e1-244">**Chaîne**.</span><span class="sxs-lookup"><span data-stu-id="312e1-244">A **String**.</span></span>

<span data-ttu-id="312e1-245">TÂCHE : la tâche elle-même.</span><span class="sxs-lookup"><span data-stu-id="312e1-245">TASK: The task itself.</span></span> <span data-ttu-id="312e1-246">**Chaîne**.</span><span class="sxs-lookup"><span data-stu-id="312e1-246">A **String**.</span></span>

<span data-ttu-id="312e1-247">DATE : la date d’échéance de la tâche.</span><span class="sxs-lookup"><span data-stu-id="312e1-247">DATE: The date that the task is due.</span></span> <span data-ttu-id="312e1-248">**DATEHEURE**.</span><span class="sxs-lookup"><span data-stu-id="312e1-248">A **DATETIME**.</span></span>

<span data-ttu-id="312e1-249">TERMINÉ : indique si la tâche est terminée ou non.</span><span class="sxs-lookup"><span data-stu-id="312e1-249">COMPLETED: If the task has been completed or not.</span></span> <span data-ttu-id="312e1-250">**BOOLÉEN**.</span><span class="sxs-lookup"><span data-stu-id="312e1-250">A **BOOLEAN**.</span></span>

### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="312e1-251">Création du schéma dans le code</span><span class="sxs-lookup"><span data-stu-id="312e1-251">Creating the schema in the code</span></span>
1. <span data-ttu-id="312e1-252">Depuis la ligne de commande, accédez au dossier **azuread** si vous n’y êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="312e1-252">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="312e1-253">Ouvrez votre fichier `server.js` dans votre éditeur favori, puis ajoutez les informations suivantes sous l’entrée de configuration :</span><span class="sxs-lookup"><span data-stu-id="312e1-253">Open your `server.js` file in your favorite editor, and then add the following information below the configuration entry:</span></span>

    ```Javascript
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema to store our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="312e1-254">Comme vous pouvez le voir dans le code, nous créons notre schéma en premier.</span><span class="sxs-lookup"><span data-stu-id="312e1-254">As you can tell from the code, we create our schema first.</span></span> <span data-ttu-id="312e1-255">Nous créons ensuite un objet de modèle que nous utilisons pour stocker nos données dans le code lorsque nous définissons nos **itinéraires**.</span><span class="sxs-lookup"><span data-stu-id="312e1-255">Then we create a model object that we use to store our data throughout the code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="312e1-256">Étape 14 : ajout de nos itinéraires pour notre serveur de tâche de l’API REST</span><span class="sxs-lookup"><span data-stu-id="312e1-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="312e1-257">Maintenant que nous disposons d’un modèle de base de données, ajoutons les itinéraires que nous allons utiliser pour notre serveur API REST.</span><span class="sxs-lookup"><span data-stu-id="312e1-257">Now that we have a database model to work with, let's add the routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="312e1-258">À propos des itinéraires dans Restify</span><span class="sxs-lookup"><span data-stu-id="312e1-258">About routes in Restify</span></span>
<span data-ttu-id="312e1-259">Dans Restify, les itinéraires fonctionnent de la même façon que dans la pile Express.</span><span class="sxs-lookup"><span data-stu-id="312e1-259">Routes work in Restify the same way they do in the Express stack.</span></span> <span data-ttu-id="312e1-260">Vous définissez des itinéraires à l’aide de l’URI qui, selon vous, sera appelé par les applications clientes.</span><span class="sxs-lookup"><span data-stu-id="312e1-260">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="312e1-261">En général, vous définissez vos itinéraires dans un fichier distinct.</span><span class="sxs-lookup"><span data-stu-id="312e1-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="312e1-262">Pour cet exemple, nous plaçons nos itinéraires dans le fichier server.js.</span><span class="sxs-lookup"><span data-stu-id="312e1-262">For our purposes, we put our routes in the server.js file.</span></span> <span data-ttu-id="312e1-263">Nous vous recommandons de factoriser ces itinéraires dans leur propre fichier s’ils sont destinés à la production.</span><span class="sxs-lookup"><span data-stu-id="312e1-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="312e1-264">Un exemple de modèle d’un itinéraire Restify se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="312e1-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep the server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="312e1-265">Il s’agit d’un modèle très basique.</span><span class="sxs-lookup"><span data-stu-id="312e1-265">This is the pattern at its most basic level.</span></span> <span data-ttu-id="312e1-266">Restify (et Express) fournit des fonctionnalités bien plus approfondies, comme la définition de types d’application et la fourniture d’un routage complexe entre différents points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="312e1-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="312e1-267">Pour nos objectifs, nous conservons ces itinéraires simples.</span><span class="sxs-lookup"><span data-stu-id="312e1-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="312e1-268">Ajout d’itinéraires par défaut à notre serveur</span><span class="sxs-lookup"><span data-stu-id="312e1-268">Add default routes to our server</span></span>
<span data-ttu-id="312e1-269">Nous ajoutons à présent les itinéraires CRUD de base suivants : Créer, Extraire, Mettre à jour et Supprimer.</span><span class="sxs-lookup"><span data-stu-id="312e1-269">We now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="312e1-270">Depuis la ligne de commande, accédez au dossier **azuread** si vous n’y êtes pas déjà :</span><span class="sxs-lookup"><span data-stu-id="312e1-270">From the command line, change directories to the **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="312e1-271">Ouvrez le fichier `server.js` dans votre éditeur favori, puis ajoutez les informations suivantes en-dessous des entrées de base de données précédentes que vous avez créées :</span><span class="sxs-lookup"><span data-stu-id="312e1-271">Open the `server.js` file in your favorite editor, and then add the following information below the previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it to Mongodb.
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

/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

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
            log.warn(err, "There is no tasks in the database. Did you initialize the database as stated in the README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="312e1-272">Ajouter la gestion des erreurs dans nos API</span><span class="sxs-lookup"><span data-stu-id="312e1-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back to the client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="312e1-273">Étape 15 : création de votre serveur</span><span class="sxs-lookup"><span data-stu-id="312e1-273">Step 15: Create your server</span></span>
<span data-ttu-id="312e1-274">Nous avons défini notre base de données et nos itinéraires sont en place.</span><span class="sxs-lookup"><span data-stu-id="312e1-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="312e1-275">La dernière étape consiste à ajouter l’instance de serveur qui gérera vos appels.</span><span class="sxs-lookup"><span data-stu-id="312e1-275">The last thing to do is add the server instance that manages our calls.</span></span>

<span data-ttu-id="312e1-276">Dans Restify (et Express), vous disposez de nombreuses options de personnalisation approfondie pour un serveur API REST, mais à nouveau, nous allons utiliser la configuration la plus simple pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="312e1-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going to use the most basic setup for our purposes.</span></span>

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

// Allow five requests per second by IP, and burst to 10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping to REST.
```

## <a name="step-16-add-the-routes-to-the-server-without-authentication-for-now"></a><span data-ttu-id="312e1-277">Étape 16 : ajout des itinéraires au serveur (sans authentification à ce stade)</span><span class="sxs-lookup"><span data-stu-id="312e1-277">Step 16: Add the routes to the server (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In the pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need to maintain session state. You can experiment with removing API protection
/* by removing the passport.authenticate() method as follows:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-the-server-before-adding-oauth-support"></a><span data-ttu-id="312e1-278">Étape 17 : exécution du serveur (avant l’ajout de la prise en charge d’OAuth)</span><span class="sxs-lookup"><span data-stu-id="312e1-278">Step 17: Run the server (before adding OAuth support)</span></span>
<span data-ttu-id="312e1-279">Testez votre serveur avant d’ajouter l’authentification.</span><span class="sxs-lookup"><span data-stu-id="312e1-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="312e1-280">Pour tester votre serveur, le plus simple consiste à utiliser curl dans une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="312e1-280">The easiest way to test your server is by using curl in a command line.</span></span> <span data-ttu-id="312e1-281">Avant cela, nous avons besoin d’un utilitaire qui nous permette d’analyser la sortie au format JSON.</span><span class="sxs-lookup"><span data-stu-id="312e1-281">Before we do that, we need a utility that allows us to parse output as JSON.</span></span>

1. <span data-ttu-id="312e1-282">Installez l’outil JSON suivant (les exemples suivants utilisent cet outil) :</span><span class="sxs-lookup"><span data-stu-id="312e1-282">Install the following JSON tool (all the following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="312e1-283">Cette opération installe totalement l’outil JSON.</span><span class="sxs-lookup"><span data-stu-id="312e1-283">This installs the JSON tool globally.</span></span> <span data-ttu-id="312e1-284">Maintenant que l’outil JSON est installé, amusons-nous avec le serveur :</span><span class="sxs-lookup"><span data-stu-id="312e1-284">Now that we’ve accomplished that, let’s play with the server:</span></span>

2. <span data-ttu-id="312e1-285">Vérifiez tout d’abord que votre instance mongoDB est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="312e1-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="312e1-286">Accédez ensuite au répertoire et commencez à utiliser curl :</span><span class="sxs-lookup"><span data-stu-id="312e1-286">Then, change to the directory and start curling:</span></span>

    <span data-ttu-id="312e1-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="312e1-287">`$ cd azuread` `$ node server.js`</span></span>

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

4. <span data-ttu-id="312e1-288">Nous pouvons à présent ajouter une tâche de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="312e1-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="312e1-289">La réponse doit être la suivante :</span><span class="sxs-lookup"><span data-stu-id="312e1-289">The response should be:</span></span>

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
    <span data-ttu-id="312e1-290">Et nous pouvons répertorier des tâches pour Brandon de cette manière :</span><span class="sxs-lookup"><span data-stu-id="312e1-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="312e1-291">Si tout cela fonctionne, nous sommes prêts à ajouter OAuth au serveur API REST.</span><span class="sxs-lookup"><span data-stu-id="312e1-291">If all this works, we're ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="312e1-292">Vous avez un serveur d’API REST avec MongoDB !</span><span class="sxs-lookup"><span data-stu-id="312e1-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="312e1-293">Étape 18 : ajout d’une authentification à notre serveur API REST</span><span class="sxs-lookup"><span data-stu-id="312e1-293">Step 18: Add authentication to our REST API server</span></span>
<span data-ttu-id="312e1-294">Maintenant que nous disposons d’une API REST en cours d’exécution, commençons à l’utiliser avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="312e1-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="312e1-295">Depuis la ligne de commande, accédez au dossier **azuread** si vous n’y êtes pas déjà.</span><span class="sxs-lookup"><span data-stu-id="312e1-295">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="312e1-296">Utiliser la stratégie OIDCBearerStrategy incluse avec passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="312e1-296">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="312e1-297">Jusqu’à présent, nous avons créé un serveur REST TODO standard ne disposant d’aucune autorisation.</span><span class="sxs-lookup"><span data-stu-id="312e1-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="312e1-298">Nous allons commencer à tout rassembler.</span><span class="sxs-lookup"><span data-stu-id="312e1-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="312e1-299">Tout d’abord, nous devons indiquer que nous voulons utiliser Passport.</span><span class="sxs-lookup"><span data-stu-id="312e1-299">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="312e1-300">Placez cela juste après la configuration de l’autre serveur :</span><span class="sxs-lookup"><span data-stu-id="312e1-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="312e1-301">Lors de l’écriture d’API, nous vous recommandons de toujours lier les données à un élément unique du jeton, dont un utilisateur ne peut pas usurper l’identité.</span><span class="sxs-lookup"><span data-stu-id="312e1-301">When you write APIs, we recommend that you always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="312e1-302">Lorsque ce serveur stocke les éléments TODO, il le fait en fonction de l’ID d’objet de l’utilisateur dans le jeton (appelé via token.oid) que nous avons placé dans le champ « propriétaire ».</span><span class="sxs-lookup"><span data-stu-id="312e1-302">When this server stores TODO items, it stores them based on the object ID of the user in the token (called through token.oid), which we put in the “owner” field.</span></span> <span data-ttu-id="312e1-303">Cela permet de s’assurer que seul cet utilisateur peut accéder à ses éléments TODO.</span><span class="sxs-lookup"><span data-stu-id="312e1-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="312e1-304">Il n’y a pas d’exposition dans l’API du « propriétaire », afin qu’un utilisateur externe puisse demander les éléments TODO d’un tiers même s’ils sont authentifiés.</span><span class="sxs-lookup"><span data-stu-id="312e1-304">There is no exposure in the API of “owner,” so an external user can request the TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="312e1-305">Maintenant, utilisons la stratégie du porteur fournie avec `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="312e1-305">Next let’s use the bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="312e1-306">Examinez le code pour l’instant, nous fournirons des explications sous peu.</span><span class="sxs-lookup"><span data-stu-id="312e1-306">Look at the code for now and we'll explain the rest shortly.</span></span> <span data-ttu-id="312e1-307">Placez ceci après ce que vous avez collé ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="312e1-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling the OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides the need to manage users and info tokens
    /* with a FindorCreate() method that must be provided by the implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want to do something smarter.
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
            log.info('verifying the user');
            log.info(token, 'was the token retreived');
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

<span data-ttu-id="312e1-308">Passport utilise un modèle semblable pour toutes ses stratégies (Twitter, Facebook, etc.), que respectent tous les enregistreurs de stratégie.</span><span class="sxs-lookup"><span data-stu-id="312e1-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="312e1-309">Comme vous pouvez le voir dans la stratégie, nous transmettons une fonction dont les paramètres sont un jeton et un done.</span><span class="sxs-lookup"><span data-stu-id="312e1-309">Looking at the strategy, you see we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="312e1-310">La stratégie nous revient une fois le travail effectué.</span><span class="sxs-lookup"><span data-stu-id="312e1-310">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="312e1-311">Nous stockons l’utilisateur et le jeton afin de ne pas avoir à les redemander.</span><span class="sxs-lookup"><span data-stu-id="312e1-311">After it does, we store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="312e1-312">Le code précédent note tout utilisateur s’authentifiant sur notre serveur.</span><span class="sxs-lookup"><span data-stu-id="312e1-312">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="312e1-313">C’est ce qu’on appelle l’enregistrement automatique.</span><span class="sxs-lookup"><span data-stu-id="312e1-313">This is known as auto-registration.</span></span> <span data-ttu-id="312e1-314">Dans les serveurs de production, nous vous recommandons de faire passer toute personne qui essaie de se connecter par un processus d’inscription de votre choix.</span><span class="sxs-lookup"><span data-stu-id="312e1-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="312e1-315">C’est généralement le modèle des applications consommateur qui vous permettent de vous inscrire via Facebook, mais vous demandent ensuite de renseigner des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="312e1-315">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="312e1-316">S’il ne s’agissait pas d’un programme de ligne de commande, nous aurions pu extraire l’adresse de messagerie à partir de l’objet de jeton retourné, avant d’inviter l’utilisateur à entrer des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="312e1-316">If this wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="312e1-317">Étant donné qu’il s’agit d’un serveur de test, nous les ajoutons simplement à la base de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="312e1-317">Because this is a test server, we simply add them to the in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="312e1-318">Protéger certains points de terminaison</span><span class="sxs-lookup"><span data-stu-id="312e1-318">Protect some endpoints</span></span>
<span data-ttu-id="312e1-319">Pour protéger les points de terminaison, spécifiez l’appel `passport.authenticate()` avec le protocole que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="312e1-319">You protect endpoints by specifying the `passport.authenticate()` call with the protocol that you want to use.</span></span>

<span data-ttu-id="312e1-320">Pour que notre code de serveur effectue quelque chose de plus intéressant, modifions l’itinéraire.</span><span class="sxs-lookup"><span data-stu-id="312e1-320">To make our server code do something more interesting, let’s edit the route.</span></span>

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

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="312e1-321">Étape 19 : ré-exécution de votre application serveur et contrôle du rejet</span><span class="sxs-lookup"><span data-stu-id="312e1-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="312e1-322">Nous allons de nouveau utiliser `curl` pour voir si nous disposons à présent de la protection OAuth2 sur nos points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="312e1-322">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="312e1-323">Nous faisons ce contrôle avant d’exécuter l’un de nos Kits de développement logiciel (SDK) clients sur ce point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="312e1-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="312e1-324">Les en-têtes renvoyés doivent être suffisants pour nous dire si nous sommes sur le bon chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="312e1-324">The headers that are returned should be enough to tell us if we're going down the right path.</span></span>

1. <span data-ttu-id="312e1-325">Vérifiez tout d’abord que votre instance mongoDB est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="312e1-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="312e1-326">Accédez ensuite au répertoire et commencez à utiliser curl.</span><span class="sxs-lookup"><span data-stu-id="312e1-326">Then, change to the directory and start curling.</span></span>

      <span data-ttu-id="312e1-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="312e1-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="312e1-328">Essayez une commande basique, comme POST.</span><span class="sxs-lookup"><span data-stu-id="312e1-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="312e1-329">Une erreur 401 est la réponse que vous cherchez ici.</span><span class="sxs-lookup"><span data-stu-id="312e1-329">A 401 is the response you are looking for here.</span></span> <span data-ttu-id="312e1-330">Cette réponse indique que la couche de Passport tente de rediriger vers le point de terminaison autorisé, ce qui est exactement ce que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="312e1-330">This response indicates that the Passport layer is trying to redirect to the authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="312e1-331">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="312e1-331">Next steps</span></span>
<span data-ttu-id="312e1-332">Vous êtes allé aussi loin que possible avec ce serveur sans utiliser un client compatible OAuth2.</span><span class="sxs-lookup"><span data-stu-id="312e1-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="312e1-333">Vous devrez suivre une autre procédure détaillée.</span><span class="sxs-lookup"><span data-stu-id="312e1-333">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="312e1-334">Vous savez maintenant comment implémenter une API REST à l’aide de Restify et d’OAuth2.</span><span class="sxs-lookup"><span data-stu-id="312e1-334">You've now learned how to implement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="312e1-335">Vous disposez également de plus de code pour continuer à développer votre service et à apprendre comment créer sur la base de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="312e1-335">You also have more than enough code to keep developing your service and learning how to build on this example.</span></span>

<span data-ttu-id="312e1-336">Si vous êtes intéressé par les étapes suivantes dans votre parcours de la bibliothèque ADAL, voici quelques clients de la bibliothèque ADAL pris en charge que nous vous recommandons de continuer à utiliser.</span><span class="sxs-lookup"><span data-stu-id="312e1-336">If you are interested in the next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="312e1-337">Clonez sur votre ordinateur de développement et configurez comme décrit dans la procédure détaillée.</span><span class="sxs-lookup"><span data-stu-id="312e1-337">Clone down to your developer machine and configure as described in the walkthrough.</span></span>

[<span data-ttu-id="312e1-338">Bibliothèque ADAL pour iOS</span><span class="sxs-lookup"><span data-stu-id="312e1-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="312e1-339">Bibliothèque ADAL pour Android</span><span class="sxs-lookup"><span data-stu-id="312e1-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
