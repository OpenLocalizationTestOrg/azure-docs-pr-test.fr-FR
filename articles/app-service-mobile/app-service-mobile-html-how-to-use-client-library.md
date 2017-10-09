---
title: aaaHow tooUse hello JavaScript SDK pour les applications mobiles Azure
description: Comment v tooUse pour les applications mobiles Azure
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="e0e0c-103">Comment tooUse hello bibliothèque cliente JavaScript pour les applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="e0e0c-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="e0e0c-104">Ce guide vous explique tooperform des scénarios courants utilisant hello dernières [JavaScript SDK pour les applications mobiles Azure].</span><span class="sxs-lookup"><span data-stu-id="e0e0c-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="e0e0c-105">Si vous êtes tooAzure Mobile de nouvelles applications, d’abord terminer [démarrage rapide d’Azure Mobile Apps] toocreate un serveur principal et créez une table.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="e0e0c-106">Dans ce guide, nous concentrer sur l’utilisation du service principal mobile de hello dans les applications Web HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="e0e0c-107">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="e0e0c-107">Supported platforms</span></span>
<span data-ttu-id="e0e0c-108">Nous limiter toohello en cours de la prise en charge de navigateur et le dernier versions Hello principaux navigateurs : Google Chrome, Microsoft Edge, Microsoft Internet Explorer et Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="e0e0c-109">Nous pensons que toofunction du Kit de développement logiciel hello avec n’importe quel navigateur relativement moderne.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="e0e0c-110">package de Hello est distribué comme un JavaScript Module universel, afin qu’il prend en charge les variables globales, AMD, et met en forme CommonJS.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="e0e0c-111"><a name="Setup"></a>Configuration et conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e0e0c-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="e0e0c-112">Ce guide part du principe que vous avez créé un serveur principal avec une table.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="e0e0c-113">Ce guide part du principe que la table hello a hello même schéma en tant que tables hello dans ces didacticiels.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="e0e0c-114">L’installation Bonjour Azure Mobile Apps JavaScript SDK peut être effectuée via hello `npm` commande :</span><span class="sxs-lookup"><span data-stu-id="e0e0c-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="e0e0c-115">Hello bibliothèque peut également être utilisée comme un module ES2015, au sein d’environnements CommonJS tels que Browserify et Webpack et comme une bibliothèque AMD.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="e0e0c-116">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e0e0c-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="e0e0c-117">Vous pouvez également utiliser une version prégénérée de hello SDK en téléchargeant directement à partir de notre CDN :</span><span class="sxs-lookup"><span data-stu-id="e0e0c-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="e0e0c-118"><a name="auth"></a>Procédure : authentification des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="e0e0c-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="e0e0c-119">Azure App Service prend en charge l’authentification et l’autorisation des utilisateurs d’applications par le biais de divers fournisseurs d’identité externes : Facebook, Google, compte Microsoft et Twitter.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="e0e0c-120">Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="e0e0c-121">Vous pouvez également utiliser l’identité hello des règles d’autorisation de tooimplement utilisateurs authentifiés dans les scripts de serveur.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="e0e0c-122">Pour plus d’informations, consultez hello [prise en main d’authentification] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="e0e0c-123">Deux flux d’authentification sont pris en charge : un flux serveur et un flux client.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="e0e0c-124">flux de serveur Hello fournit expérience d’authentification la plus simple hello, car il repose sur l’interface d’authentification web du fournisseur hello.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="e0e0c-125">Hello flux client permet une intégration plus étroite avec des fonctionnalités spécifiques à l’appareil comme single-sign-on comme il s’appuie sur les kits de développement logiciel spécifique au fournisseur.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="e0e0c-126"><a name="configure-external-redirect-urls"></a>Configurer votre Mobile App Service pour les URL de redirection externes.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="e0e0c-127">Plusieurs types d’applications JavaScript utilisent un toohandle de la fonctionnalité de bouclage Qu'oauth UI flux.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="e0e0c-128">Ces fonctionnalités sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0e0c-128">These capabilities include:</span></span>

* <span data-ttu-id="e0e0c-129">Exécuter votre service en local</span><span class="sxs-lookup"><span data-stu-id="e0e0c-129">Running your service locally</span></span>
* <span data-ttu-id="e0e0c-130">À l’aide de rechargement de Live avec hello infrastructure Ionic</span><span class="sxs-lookup"><span data-stu-id="e0e0c-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="e0e0c-131">Redirection tooApp Service pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="e0e0c-132">En cours d’exécution localement peut entraîner des problèmes étant donné que, par défaut, l’authentification est uniquement du Service d’applications accès tooallow à partir de votre serveur principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="e0e0c-133">Utilisez hello suivant les étapes toochange hello d’authentification tooenable de paramètres du Service d’applications lors de l’exécution de serveur de hello localement :</span><span class="sxs-lookup"><span data-stu-id="e0e0c-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="e0e0c-134">Connectez-vous à toohello [portail Azure]</span><span class="sxs-lookup"><span data-stu-id="e0e0c-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="e0e0c-135">Accédez principal de l’application Mobile tooyour.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="e0e0c-136">Sélectionnez **l’Explorateur de ressources** Bonjour **outils de développement** menu.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="e0e0c-137">Cliquez sur **accédez** tooopen l’Explorateur de ressources hello pour votre serveur principal de l’application Mobile dans une fenêtre ou un nouvel onglet.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="e0e0c-138">Développez hello **config** > **authsettings** nœud pour votre application.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="e0e0c-139">Cliquez sur hello **modifier** bouton tooenable modification de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="e0e0c-140">Recherche hello **allowedExternalRedirectUrls** élément, qui doit être null.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="e0e0c-141">Ajoutez vos URL dans un tableau :</span><span class="sxs-lookup"><span data-stu-id="e0e0c-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="e0e0c-142">Remplacez l’URL hello dans le tableau de hello avec des URL de votre service, qui est dans cet exemple hello `http://localhost:3000` pour hello local Node.js exemple de service.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="e0e0c-143">Vous pouvez également utiliser `http://localhost:4400` pour hello Ripple URL de service ou des autres, en fonction de la configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="e0e0c-144">En hello haut hello, cliquez sur **en lecture/écriture**, puis cliquez sur **PUT** toosave vos mises à jour.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="e0e0c-145">Vous devez également tooadd hello même bouclage URL toohello paramètres CORS de l’autorisation :</span><span class="sxs-lookup"><span data-stu-id="e0e0c-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="e0e0c-146">Accédez arrière toohello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="e0e0c-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="e0e0c-147">Accédez principal de l’application Mobile tooyour.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="e0e0c-148">Cliquez sur **CORS** Bonjour **API** menu.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="e0e0c-149">Entrez chaque URL Bonjour vide **autorisé les origines** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="e0e0c-150">Une zone de texte est créée.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-150">A new text box is created.</span></span>
5. <span data-ttu-id="e0e0c-151">Cliquez sur **ENREGISTRER**</span><span class="sxs-lookup"><span data-stu-id="e0e0c-151">Click **SAVE**</span></span>

<span data-ttu-id="e0e0c-152">Après que hello principales mises à jour, vous serez en mesure de toouse hello nouvelles bouclage URL dans votre application.</span><span class="sxs-lookup"><span data-stu-id="e0e0c-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[démarrage rapide d’Azure Mobile Apps]: app-service-mobile-cordova-get-started.md
[prise en main d’authentification]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portail Azure]: https://portal.azure.com/
[JavaScript SDK pour les applications mobiles Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
