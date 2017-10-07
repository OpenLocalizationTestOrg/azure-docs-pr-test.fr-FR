---
title: "aaaHow tooUse plug-in d’Apache Cordova pour les applications mobiles Azure"
description: "Comment tooUse plug-in d’Apache Cordova pour les applications mobiles Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="ac262-103">La bibliothèque cliente de toouse Apache Cordova pour les applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="ac262-103">How toouse Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="ac262-104">Ce guide vous explique tooperform des scénarios courants utilisant hello dernières [plug-in d’Apache Cordova pour les applications mobiles Azure].</span><span class="sxs-lookup"><span data-stu-id="ac262-104">This guide teaches you tooperform common scenarios using hello latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="ac262-105">Si vous êtes tooAzure Mobile de nouvelles applications, d’abord terminer [démarrage rapide d’Azure Mobile Apps] toocreate un service principal, créez une table et télécharger un projet Apache Cordova avant génération.</span><span class="sxs-lookup"><span data-stu-id="ac262-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="ac262-106">Dans ce guide, nous nous concentrer sur le côté client hello plug-in de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ac262-106">In this guide, we focus on hello client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="ac262-107">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="ac262-107">Supported platforms</span></span>
<span data-ttu-id="ac262-108">Ce kit de développement logiciel (SDK) prend en charge Apache Cordova 6.0.0 et version ultérieure sur les appareils iOS, Android et Windows.</span><span class="sxs-lookup"><span data-stu-id="ac262-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="ac262-109">prise en charge de la plateforme Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="ac262-109">hello platform support is as follows:</span></span>

* <span data-ttu-id="ac262-110">Android API 19-24 (KitKat à Nougat).</span><span class="sxs-lookup"><span data-stu-id="ac262-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="ac262-111">iOS 8.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="ac262-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="ac262-112">Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="ac262-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="ac262-113">Plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="ac262-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="ac262-114"><a name="Setup"></a>Configuration et conditions préalables</span><span class="sxs-lookup"><span data-stu-id="ac262-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="ac262-115">Ce guide part du principe que vous avez créé un serveur principal avec une table.</span><span class="sxs-lookup"><span data-stu-id="ac262-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="ac262-116">Ce guide part du principe que la table hello a hello même schéma en tant que tables hello dans ces didacticiels.</span><span class="sxs-lookup"><span data-stu-id="ac262-116">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="ac262-117">Ce guide suppose également que vous avez ajouté le code de tooyour hello plug-in de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ac262-117">This guide also assumes that you have added hello Apache Cordova Plugin tooyour code.</span></span>  <span data-ttu-id="ac262-118">Si vous n'avez pas fait, vous pouvez ajouter le projet de tooyour hello Apache Cordova plug-in sur la ligne de commande hello :</span><span class="sxs-lookup"><span data-stu-id="ac262-118">If you have not done so, you may add hello Apache Cordova plugin tooyour project on hello command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="ac262-119">Pour plus d’informations sur la création de [votre première application Apache Cordova], consultez la documentation officielle.</span><span class="sxs-lookup"><span data-stu-id="ac262-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="ac262-120"><a name="ionic"></a>Configuration d’une application Ionic v2</span><span class="sxs-lookup"><span data-stu-id="ac262-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="ac262-121">configurer un projet Ionic v2 tooproperly, tout d’abord créer une application de base et ajouter le plug-in de hello Cordova :</span><span class="sxs-lookup"><span data-stu-id="ac262-121">tooproperly configure an Ionic v2 project, first create a basic app and add hello Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="ac262-122">Ajouter hello lignes suivantes trop`app.component.ts` objet de client toocreate hello :</span><span class="sxs-lookup"><span data-stu-id="ac262-122">Add hello following lines too`app.component.ts` toocreate hello client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="ac262-123">Vous pouvez maintenant générer et exécuter des projets de hello dans le navigateur de hello :</span><span class="sxs-lookup"><span data-stu-id="ac262-123">You can now build and run hello project in hello browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="ac262-124">le plug-in de Hello Azure Mobile Apps Cordova prend en charge les deux applications v1 et v2 Ionic.</span><span class="sxs-lookup"><span data-stu-id="ac262-124">hello Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="ac262-125">Uniquement les applications de hello Ionic v2 nécessitent la déclaration supplémentaire pour hello `WindowsAzure` objet.</span><span class="sxs-lookup"><span data-stu-id="ac262-125">Only hello Ionic v2 apps require the additional declaration for hello `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="ac262-126"><a name="auth"></a>Procédure : authentification des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ac262-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="ac262-127">Azure App Service prend en charge l’authentification et l’autorisation des utilisateurs d’applications par le biais de divers fournisseurs d’identité externes : Facebook, Google, compte Microsoft et Twitter.</span><span class="sxs-lookup"><span data-stu-id="ac262-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="ac262-128">Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié.</span><span class="sxs-lookup"><span data-stu-id="ac262-128">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="ac262-129">Vous pouvez également utiliser l’identité hello des règles d’autorisation de tooimplement utilisateurs authentifiés dans les scripts de serveur.</span><span class="sxs-lookup"><span data-stu-id="ac262-129">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="ac262-130">Pour plus d’informations, consultez hello [prise en main d’authentification] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ac262-130">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="ac262-131">Lorsque vous utilisez l’authentification dans une application Apache Cordova, hello suivant plug-ins Cordova doit être disponible :</span><span class="sxs-lookup"><span data-stu-id="ac262-131">When using authentication in an Apache Cordova app, hello following Cordova plugins must be available:</span></span>

* <span data-ttu-id="ac262-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="ac262-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="ac262-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="ac262-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="ac262-134">Deux flux d’authentification sont pris en charge : un flux serveur et un flux client.</span><span class="sxs-lookup"><span data-stu-id="ac262-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="ac262-135">flux de serveur Hello fournit expérience d’authentification la plus simple hello, car il repose sur l’interface d’authentification web du fournisseur hello.</span><span class="sxs-lookup"><span data-stu-id="ac262-135">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="ac262-136">Hello flux client permet une intégration plus étroite avec des fonctionnalités spécifiques à l’appareil comme single-sign-on comme il s’appuie sur les kits de développement logiciel spécifique au fournisseur spécifique à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ac262-136">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="ac262-137"><a name="configure-external-redirect-urls"></a>Configurer votre Mobile App Service pour les URL de redirection externes.</span><span class="sxs-lookup"><span data-stu-id="ac262-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="ac262-138">Plusieurs types d’applications Apache Cordova utilisent un toohandle de la fonctionnalité de bouclage Qu'oauth UI flux.</span><span class="sxs-lookup"><span data-stu-id="ac262-138">Several types of Apache Cordova applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="ac262-139">Flux OAuth UI sur localhost provoquent des problèmes, étant donné que le service d’authentification hello uniquement sait comment tooutilize votre service par défaut.</span><span class="sxs-lookup"><span data-stu-id="ac262-139">OAuth UI flows on localhost cause problems since hello authentication service only knows how tooutilize your service by default.</span></span>  <span data-ttu-id="ac262-140">Voici quelques exemples de problèmes causés par les flux d’interface utilisateur OAuth :</span><span class="sxs-lookup"><span data-stu-id="ac262-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="ac262-141">émulateur Ripple de Hello.</span><span class="sxs-lookup"><span data-stu-id="ac262-141">hello Ripple emulator.</span></span>
* <span data-ttu-id="ac262-142">Live recharger avec Ionic.</span><span class="sxs-lookup"><span data-stu-id="ac262-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="ac262-143">En cours d’exécution hello backend mobile localement</span><span class="sxs-lookup"><span data-stu-id="ac262-143">Running hello mobile backend locally</span></span>
* <span data-ttu-id="ac262-144">En cours d’exécution backend mobile de hello dans un autre Service d’application Azure à l’authentification en fournissant un hello.</span><span class="sxs-lookup"><span data-stu-id="ac262-144">Running hello mobile backend in a different Azure App Service than hello one providing authentication.</span></span>

<span data-ttu-id="ac262-145">Suivez ces tooadd instructions votre configuration de toohello paramètres locaux :</span><span class="sxs-lookup"><span data-stu-id="ac262-145">Follow these instructions tooadd your local settings toohello configuration:</span></span>

1. <span data-ttu-id="ac262-146">Connectez-vous à toohello [portail Azure]</span><span class="sxs-lookup"><span data-stu-id="ac262-146">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="ac262-147">Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre application Mobile.</span><span class="sxs-lookup"><span data-stu-id="ac262-147">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="ac262-148">Cliquez sur **Outils**</span><span class="sxs-lookup"><span data-stu-id="ac262-148">Click **Tools**</span></span>
4. <span data-ttu-id="ac262-149">Cliquez sur **l’Explorateur de ressources** dans le menu d’observer hello, puis cliquez sur **accédez**.</span><span class="sxs-lookup"><span data-stu-id="ac262-149">Click **Resource explorer** in hello OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="ac262-150">Une nouvelle fenêtre ou un nouvel onglet s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="ac262-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="ac262-151">Développez hello **config**, **authsettings** nœuds pour votre site de navigation de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="ac262-151">Expand hello **config**, **authsettings** nodes for your site in hello left-hand navigation.</span></span>
6. <span data-ttu-id="ac262-152">Cliquez sur **Modifier**</span><span class="sxs-lookup"><span data-stu-id="ac262-152">Click **Edit**</span></span>
7. <span data-ttu-id="ac262-153">Recherchez l’élément de « allowedExternalRedirectUrls » hello.</span><span class="sxs-lookup"><span data-stu-id="ac262-153">Look for hello "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="ac262-154">Elle peut être définie toonull ou un tableau de valeurs.</span><span class="sxs-lookup"><span data-stu-id="ac262-154">It may be set toonull or an array of values.</span></span>  <span data-ttu-id="ac262-155">Modifiez toohello de valeur hello valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="ac262-155">Change hello value toohello following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="ac262-156">Remplacer les URL hello hello les URL de votre service.</span><span class="sxs-lookup"><span data-stu-id="ac262-156">Replace hello URLs with hello URLs of your service.</span></span>  <span data-ttu-id="ac262-157">Exemples « http://localhost:3000 » (pour hello Node.js exemple de service) ou « http://localhost:4400 » (pour le service d’ondulation hello).</span><span class="sxs-lookup"><span data-stu-id="ac262-157">Examples include "http://localhost:3000" (for hello Node.js sample service), or "http://localhost:4400" (for hello Ripple service).</span></span>  <span data-ttu-id="ac262-158">Toutefois, ces URL est exemples - votre situation, y compris pour les services hello mentionnés dans les exemples hello, peuvent être différents.</span><span class="sxs-lookup"><span data-stu-id="ac262-158">However, these URLs are examples - your situation, including for hello services mentioned in hello examples, may be different.</span></span>
8. <span data-ttu-id="ac262-159">Cliquez sur hello **en lecture/écriture** bouton hello en haut à droite de l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="ac262-159">Click hello **Read/Write** button in hello top-right corner of hello screen.</span></span>
9. <span data-ttu-id="ac262-160">Cliquez sur hello verte **PUT** bouton.</span><span class="sxs-lookup"><span data-stu-id="ac262-160">Click hello green **PUT** button.</span></span>

<span data-ttu-id="ac262-161">les paramètres de Hello sont enregistrés à ce stade.</span><span class="sxs-lookup"><span data-stu-id="ac262-161">hello settings are saved at this point.</span></span>  <span data-ttu-id="ac262-162">Ne fermez pas de fenêtre de navigateur hello jusqu'à la fin de paramètres de hello l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="ac262-162">Do not close hello browser window until hello settings have finished saving.</span></span>
<span data-ttu-id="ac262-163">Également ajouter ces paramètres CORS de bouclage URL toohello pour votre application de Service :</span><span class="sxs-lookup"><span data-stu-id="ac262-163">Also add these loopback URLs toohello CORS settings for your App Service:</span></span>

1. <span data-ttu-id="ac262-164">Connectez-vous à toohello [portail Azure]</span><span class="sxs-lookup"><span data-stu-id="ac262-164">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="ac262-165">Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre application Mobile.</span><span class="sxs-lookup"><span data-stu-id="ac262-165">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="ac262-166">Panneau de paramètres Hello s’ouvre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ac262-166">hello Settings blade opens automatically.</span></span>  <span data-ttu-id="ac262-167">Si ce n’est pas le cas, cliquez sur **Tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="ac262-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="ac262-168">Cliquez sur **CORS** sous le menu de hello API.</span><span class="sxs-lookup"><span data-stu-id="ac262-168">Click **CORS** under hello API menu.</span></span>
5. <span data-ttu-id="ac262-169">Entrez les URL hello que vous souhaitez tooadd dans zone de hello et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="ac262-169">Enter hello URL that you wish tooadd in hello box provided and press Enter.</span></span>
6. <span data-ttu-id="ac262-170">Entrez des URL supplémentaires, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ac262-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="ac262-171">Cliquez sur **enregistrer** toosave les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="ac262-171">Click **Save** toosave hello settings.</span></span>

<span data-ttu-id="ac262-172">Il prend environ 10 à 15 secondes pour effet de tootake hello nouveaux paramètres.</span><span class="sxs-lookup"><span data-stu-id="ac262-172">It takes approximately 10-15 seconds for hello new settings tootake effect.</span></span>

## <span data-ttu-id="ac262-173"><a name="register-for-push"></a>Procédure : inscription aux notifications Push</span><span class="sxs-lookup"><span data-stu-id="ac262-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="ac262-174">Installer hello [push de plug-in de phonegap] toohandle les notifications push.</span><span class="sxs-lookup"><span data-stu-id="ac262-174">Install hello [phonegap-plugin-push] toohandle push notifications.</span></span>  <span data-ttu-id="ac262-175">Ce plug-in peut être aisément ajouté à l’aide de la `cordova plugin add` commande sur la ligne de commande hello ou via le programme d’installation du plug-in Git hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ac262-175">This plugin can be easily added using the `cordova plugin add` command on hello command line, or via hello Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="ac262-176">Le code suivant dans votre application Apache Cordova inscrit votre appareil aux notifications Push :</span><span class="sxs-lookup"><span data-stu-id="ac262-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="ac262-177">Utiliser des notifications push toosend de hello Notification Hubs SDK à partir du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="ac262-177">Use hello Notification Hubs SDK toosend push notifications from hello server.</span></span>  <span data-ttu-id="ac262-178">N’envoyez jamais de notifications Push directement depuis les clients.</span><span class="sxs-lookup"><span data-stu-id="ac262-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="ac262-179">Cette opération donc pourrait être tootrigger utilisé une attaque par déni de service par rapport aux concentrateurs de Notification ou hello PNS.</span><span class="sxs-lookup"><span data-stu-id="ac262-179">Doing so could be used tootrigger a denial of service attack against Notification Hubs or hello PNS.</span></span>  <span data-ttu-id="ac262-180">Hello PNS peut interdire le trafic de votre suite à telles attaques.</span><span class="sxs-lookup"><span data-stu-id="ac262-180">hello PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="ac262-181">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="ac262-181">More information</span></span>

<span data-ttu-id="ac262-182">Vous pouvez trouver des informations sur les API dans notre [documentation sur les API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="ac262-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
[portail Azure]: https://portal.azure.com
[démarrage rapide d’Azure Mobile Apps]: app-service-mobile-cordova-get-started.md
[prise en main d’authentification]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[plug-in d’Apache Cordova pour les applications mobiles Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[votre première application Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[push de plug-in de phonegap]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
