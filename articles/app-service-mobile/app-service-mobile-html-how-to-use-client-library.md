---
title: "Utilisation du Kit de développement logiciel (SDK) JavaScript pour Azure Mobile Apps"
description: "Utilisation de v pour Azure Mobile Apps"
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
ms.openlocfilehash: 0c4b4de560d70592f5bbdee28b56a7686b5689f4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="d3797-103">Utilisation de la bibliothèque cliente JavaScript pour Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="d3797-103">How to Use the JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="d3797-104">Ce guide indique le déroulement de scénarios courants dans le cadre de l’utilisation du dernier [Kit de développement logiciel (SDK) JavaScript pour Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="d3797-104">This guide teaches you to perform common scenarios using the latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="d3797-105">Si vous ne connaissez pas Azure Mobile Apps, consultez d’abord la section [Démarrage rapide d’Azure Mobile Apps] pour créer un backend et créer une table.</span><span class="sxs-lookup"><span data-stu-id="d3797-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend and create a table.</span></span> <span data-ttu-id="d3797-106">Dans ce guide, nous nous concentrons sur l’utilisation du backend mobile dans les applications web HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d3797-106">In this guide, we focus on using the mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="d3797-107">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="d3797-107">Supported platforms</span></span>
<span data-ttu-id="d3797-108">Nous limitons la prise en charge aux versions actuelles, ainsi qu’aux dernières versions des principaux navigateurs : Google Chrome, Microsoft Edge, Microsoft Internet Explorer et Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="d3797-108">We limit browser support to the current and last versions of the major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="d3797-109">Le Kit de développement logiciel (SDK) devrait fonctionner avec n’importe quel navigateur relativement récent.</span><span class="sxs-lookup"><span data-stu-id="d3797-109">We expect the SDK to function with any relatively modern browser.</span></span>

<span data-ttu-id="d3797-110">Le package est distribué comme un module JavaScript universel et prend donc en charge les format Globals, AMD et CommonJS.</span><span class="sxs-lookup"><span data-stu-id="d3797-110">The package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="d3797-111"><a name="Setup"></a>Configuration et conditions préalables</span><span class="sxs-lookup"><span data-stu-id="d3797-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="d3797-112">Ce guide part du principe que vous avez créé un serveur principal avec une table.</span><span class="sxs-lookup"><span data-stu-id="d3797-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="d3797-113">Ce guide suppose que la table a le même schéma que les tables dans ces didacticiels.</span><span class="sxs-lookup"><span data-stu-id="d3797-113">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span>

<span data-ttu-id="d3797-114">Installez le Kit de développement logiciel (SDK) JavaScript Azure Mobile Apps à partir de la commande `npm` :</span><span class="sxs-lookup"><span data-stu-id="d3797-114">Installing the Azure Mobile Apps JavaScript SDK can be done via the `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="d3797-115">La bibliothèque peut également être utilisée en tant que module ES2015, au sein d'environnements CommonJS tels que Browserify et Webpack, et en tant que bibliothèque AMD.</span><span class="sxs-lookup"><span data-stu-id="d3797-115">The library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="d3797-116">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d3797-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="d3797-117">Vous pouvez également utiliser une version du Kit de développement logiciel (SDK) avant génération en téléchargeant directement à partir de notre CDN :</span><span class="sxs-lookup"><span data-stu-id="d3797-117">You can also use a pre-built version of the SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="d3797-118"><a name="auth"></a>Procédure : authentification des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d3797-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="d3797-119">Azure App Service prend en charge l’authentification et l’autorisation des utilisateurs d’applications par le biais de divers fournisseurs d’identité externes : Facebook, Google, compte Microsoft et Twitter.</span><span class="sxs-lookup"><span data-stu-id="d3797-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="d3797-120">Vous pouvez définir des autorisations sur les tables pour limiter l'accès à certaines opérations aux seuls utilisateurs authentifiés.</span><span class="sxs-lookup"><span data-stu-id="d3797-120">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="d3797-121">Vous pouvez également utiliser l’identité des utilisateurs authentifiés pour implémenter des règles d’autorisation dans les scripts serveur.</span><span class="sxs-lookup"><span data-stu-id="d3797-121">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="d3797-122">Pour plus d'informations, consultez la page [Prise en main de l'authentification] .</span><span class="sxs-lookup"><span data-stu-id="d3797-122">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="d3797-123">Deux flux d’authentification sont pris en charge : un flux serveur et un flux client.</span><span class="sxs-lookup"><span data-stu-id="d3797-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="d3797-124">Le flux serveur fournit l'authentification la plus simple, car il repose sur l'interface d'authentification Web du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="d3797-124">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="d3797-125">Le flux client permet une intégration approfondie avec les fonctionnalités propres aux appareils, telles que l'authentification unique, car il repose sur des Kits de développement logiciel (SDK) propres aux fournisseurs.</span><span class="sxs-lookup"><span data-stu-id="d3797-125">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="d3797-126"><a name="configure-external-redirect-urls"></a>Configurer votre Mobile App Service pour les URL de redirection externes.</span><span class="sxs-lookup"><span data-stu-id="d3797-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="d3797-127">Plusieurs types d’applications JavaScript utilisent une fonctionnalité de bouclage pour gérer les flux d’interface utilisateur OAuth.</span><span class="sxs-lookup"><span data-stu-id="d3797-127">Several types of JavaScript applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="d3797-128">Ces fonctionnalités sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d3797-128">These capabilities include:</span></span>

* <span data-ttu-id="d3797-129">Exécuter votre service en local</span><span class="sxs-lookup"><span data-stu-id="d3797-129">Running your service locally</span></span>
* <span data-ttu-id="d3797-130">Utilisation de Live Reload avec l’infrastructure Ionic</span><span class="sxs-lookup"><span data-stu-id="d3797-130">Using Live Reload with the Ionic Framework</span></span>
* <span data-ttu-id="d3797-131">Redirection vers le App Service pour authentification.</span><span class="sxs-lookup"><span data-stu-id="d3797-131">Redirecting to App Service for authentication.</span></span>

<span data-ttu-id="d3797-132">L’exécution locale peut entraîner des problèmes car, par défaut, l’authentification d’App Service est uniquement configurée pour autoriser l’accès à partir du serveur principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="d3797-132">Running locally can cause problems because, by default, App Service authentication is only configured to allow access from your Mobile App backend.</span></span> <span data-ttu-id="d3797-133">Utilisez la procédure suivante pour modifier les paramètres d’App Service afin d’activer l’authentification lors de l’exécution locale du serveur :</span><span class="sxs-lookup"><span data-stu-id="d3797-133">Use the following steps to change the App Service settings to enable authentication when running the server locally:</span></span>

1. <span data-ttu-id="d3797-134">Connectez-vous au [portail Azure]</span><span class="sxs-lookup"><span data-stu-id="d3797-134">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="d3797-135">Accédez à votre backend d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="d3797-135">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="d3797-136">Sélectionnez **Explorateur de ressources** dans le menu **OUTILS DE DÉVELOPPEMENT**.</span><span class="sxs-lookup"><span data-stu-id="d3797-136">Select **Resource explorer** in the **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="d3797-137">Cliquez sur **Aller** pour ouvrir l’Explorateur de ressources pour votre application mobile principale dans une fenêtre ou un nouvel onglet.</span><span class="sxs-lookup"><span data-stu-id="d3797-137">Click **Go** to open the resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="d3797-138">Développez le nœud **config** > **authsettings** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="d3797-138">Expand the **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="d3797-139">Cliquez sur le bouton **Modifier** pour activer la modification de la ressource.</span><span class="sxs-lookup"><span data-stu-id="d3797-139">Click the **Edit** button to enable editing of the resource.</span></span>
7. <span data-ttu-id="d3797-140">Trouvez l’élément **allowedExternalRedirectUrls** , qui doit être null.</span><span class="sxs-lookup"><span data-stu-id="d3797-140">Find the **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="d3797-141">Ajoutez vos URL dans un tableau :</span><span class="sxs-lookup"><span data-stu-id="d3797-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="d3797-142">Remplacez les URL dans le tableau par les URL de votre service ; dans cet exemple, `http://localhost:3000` pour l’exemple de service Node.js local.</span><span class="sxs-lookup"><span data-stu-id="d3797-142">Replace the URLs in the array with the URLs of your service, which in this example is `http://localhost:3000` for the local Node.js sample service.</span></span> <span data-ttu-id="d3797-143">Vous pouvez également utiliser `http://localhost:4400` pour le service Ripple ou d’autres URL, selon la configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="d3797-143">You could also use `http://localhost:4400` for the Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="d3797-144">En haut de la page, cliquez sur **Lecture/Écriture**, puis sur **PUT** pour enregistrer vos mises à jour.</span><span class="sxs-lookup"><span data-stu-id="d3797-144">At the top of the page, click **Read/Write**, then click **PUT** to save your updates.</span></span>

<span data-ttu-id="d3797-145">Vous devez aussi ajouter les mêmes URL de bouclage aux paramètres de la liste blanche CORS :</span><span class="sxs-lookup"><span data-stu-id="d3797-145">You also need to add the same loopback URLs to the CORS whitelist settings:</span></span>

1. <span data-ttu-id="d3797-146">Revenez au [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="d3797-146">Navigate back to the [Azure portal].</span></span>
2. <span data-ttu-id="d3797-147">Accédez à votre backend d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="d3797-147">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="d3797-148">Cliquez sur **CORS** dans le menu **API**.</span><span class="sxs-lookup"><span data-stu-id="d3797-148">Click **CORS** in the **API** menu.</span></span>
4. <span data-ttu-id="d3797-149">Saisissez chaque URL dans la zone de texte **Origines autorisées** vide.</span><span class="sxs-lookup"><span data-stu-id="d3797-149">Enter each URL in the empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="d3797-150">Une zone de texte est créée.</span><span class="sxs-lookup"><span data-stu-id="d3797-150">A new text box is created.</span></span>
5. <span data-ttu-id="d3797-151">Cliquez sur **ENREGISTRER**</span><span class="sxs-lookup"><span data-stu-id="d3797-151">Click **SAVE**</span></span>

<span data-ttu-id="d3797-152">Après que le serveur principal sera mis à jour, vous serez en mesure d’utiliser les nouvelles URL de bouclage dans votre application.</span><span class="sxs-lookup"><span data-stu-id="d3797-152">After the backend updates, you will be able to use the new loopback URLs in your app.</span></span>

<!-- URLs. -->
<span data-ttu-id="d3797-153">[Démarrage rapide d’Azure Mobile Apps]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="d3797-153">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="d3797-154">[Prise en main de l'authentification]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="d3797-154">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="d3797-155">[portail Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="d3797-155">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="d3797-156">[Kit de développement logiciel (SDK) JavaScript pour Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client</span><span class="sxs-lookup"><span data-stu-id="d3797-156">[JavaScript SDK for Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
