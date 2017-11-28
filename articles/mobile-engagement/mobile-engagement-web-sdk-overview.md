---
title: "vue d’ensemble du Kit de développement Web Mobile Engagement d’aaaAzure | Documents Microsoft"
description: "Hello les dernières mises à jour et les procédures à suivre pour hello Web SDK pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="e0803-103">Kit de développement logiciel (SDK) web pour Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e0803-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="e0803-104">Démarrez ici pour tous les hello plus d’informations sur la façon toointegrate Azure Mobile Engagement dans une application web.</span><span class="sxs-lookup"><span data-stu-id="e0803-104">Start here for all hello details about how toointegrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="e0803-105">Si vous souhaitez que toogive il une tentative de mise en route avec votre propre application web, consultez notre [15 minutes didacticiel](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0803-105">If you'd like toogive it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="e0803-106">Procédures d'intégration</span><span class="sxs-lookup"><span data-stu-id="e0803-106">Integration procedures</span></span>
1. <span data-ttu-id="e0803-107">En savoir plus [comment toointegrate Mobile Engagement dans votre application web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="e0803-107">Learn [how toointegrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="e0803-108">Pour l’implémentation du plan de balise, Découvrez [comment toouse hello avancé Mobile Engagement marquage API dans votre application web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="e0803-108">For tag plan implementation, learn [how toouse hello advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="e0803-109">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="e0803-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="e0803-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="e0803-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="e0803-111">Résolution d’un incident dans la navigation privée (Safari).</span><span class="sxs-lookup"><span data-stu-id="e0803-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="e0803-112">Résolution d’un incident sur les navigateurs avec cookies désactivés.</span><span class="sxs-lookup"><span data-stu-id="e0803-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="e0803-113">Pour toutes les versions, consultez hello [terminer les notes de publication](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="e0803-113">For all versions, please see hello [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="e0803-114">Procédures de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="e0803-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-too200"></a><span data-ttu-id="e0803-115">Mise à niveau à partir de 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="e0803-115">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="e0803-116">Hello sections suivantes décrivent comment toomigrate une intégration du Kit de développement Web Mobile Engagement à partir du service de Capptain hello, prestation Capptain SAS, tooan Azure Mobile Engagement application.</span><span class="sxs-lookup"><span data-stu-id="e0803-116">hello following sections describe how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="e0803-117">Si vous effectuez une migration depuis une version antérieure à 1.2.1, consultez hello Capptain site Web toomigrate too1.2.1 tout d’abord, puis appliquez hello procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="e0803-117">If you are migrating from a version earlier than 1.2.1, please consult hello Capptain website toomigrate too1.2.1 first, and then apply hello following procedures.</span></span>

<span data-ttu-id="e0803-118">Cette version du Kit de développement Web Mobile Engagement de hello ne prend pas en charge les TV actives Samsung, Opera TV, webOS ou fonctionnalité de couverture hello.</span><span class="sxs-lookup"><span data-stu-id="e0803-118">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0803-119">Capptain et Azure Mobile Engagement ne sont pas hello même service, et hello procédures suivantes en surbrillance uniquement comment toomigrate hello application cliente.</span><span class="sxs-lookup"><span data-stu-id="e0803-119">Capptain and Azure Mobile Engagement are not hello same service, and hello following procedures highlight only how toomigrate hello client app.</span></span> <span data-ttu-id="e0803-120">Migration hello Kit de développement Web Mobile Engagement dans l’application hello ne migre pas vos données à partir d’un serveur Capptain server tooa Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e0803-120">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="e0803-121">Fichiers JavaScript</span><span class="sxs-lookup"><span data-stu-id="e0803-121">JavaScript files</span></span>
<span data-ttu-id="e0803-122">Remplacez hello fichier capptain-sdk.js par hello fichier azure-engagement.js, puis mettez à jour votre script importe en conséquence.</span><span class="sxs-lookup"><span data-stu-id="e0803-122">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="e0803-123">Supprimer Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="e0803-123">Remove Capptain Reach</span></span>
<span data-ttu-id="e0803-124">Cette version du Kit de développement Web Mobile Engagement de hello ne prend pas en charge la fonctionnalité de couverture hello.</span><span class="sxs-lookup"><span data-stu-id="e0803-124">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="e0803-125">Si vous avez intégré Capptain portée dans votre application, vous devez tooremove il.</span><span class="sxs-lookup"><span data-stu-id="e0803-125">If you have integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="e0803-126">Suppression hello atteindre le CSS importation à partir de votre page et fichier .css connexes de hello (capptain-reach.css, par défaut).</span><span class="sxs-lookup"><span data-stu-id="e0803-126">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="e0803-127">Supprimer hello suivant des ressources de portée : hello fermer image (capptain-close.png, par défaut) et l’icône de marque hello (capptain-notification-icône, par défaut).</span><span class="sxs-lookup"><span data-stu-id="e0803-127">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="e0803-128">Supprimez hello atteindre de l’interface utilisateur pour les notifications dans l’application.</span><span class="sxs-lookup"><span data-stu-id="e0803-128">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="e0803-129">disposition par défaut de Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="e0803-129">hello default layout looks like this:</span></span>

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

<span data-ttu-id="e0803-130">Supprimez hello atteindre de l’interface utilisateur pour les annonces de web et de texte et les sondages.</span><span class="sxs-lookup"><span data-stu-id="e0803-130">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="e0803-131">disposition par défaut de Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="e0803-131">hello default layout looks like this:</span></span>

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

<span data-ttu-id="e0803-132">Supprimer hello `reach` de l’objet à partir de votre configuration, si elle existe.</span><span class="sxs-lookup"><span data-stu-id="e0803-132">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="e0803-133">Voici à quoi cela ressemble :</span><span class="sxs-lookup"><span data-stu-id="e0803-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="e0803-134">Supprimez toute autre personnalisation Reach, notamment les catégories.</span><span class="sxs-lookup"><span data-stu-id="e0803-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="e0803-135">Supprimer les API déconseillées</span><span class="sxs-lookup"><span data-stu-id="e0803-135">Remove deprecated APIs</span></span>
<span data-ttu-id="e0803-136">Certaines API de Capptain est déconseillées dans hello Kit de développement Web Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e0803-136">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="e0803-137">Supprimer tout toohello appels suivant API : `agent.connect`, `agent.disconnect`, `agent.pause`, et `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="e0803-137">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="e0803-138">Supprimer les hello suivant des rappels à partir de votre configuration Capptain : `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, et `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="e0803-138">Remove any of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="e0803-139">Configuration</span><span class="sxs-lookup"><span data-stu-id="e0803-139">Configuration</span></span>
<span data-ttu-id="e0803-140">Mobile Engagement utilise une connexion chaîne tooconfigure Kit de développement logiciel des identificateurs, par exemple, identificateur d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e0803-140">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="e0803-141">Remplacez l’ID de l’application hello avec votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="e0803-141">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="e0803-142">Notez qu’objet global hello de hello configuration du Kit de développement logiciel passe de `capptain` trop`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="e0803-142">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="e0803-143">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="e0803-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="e0803-144">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="e0803-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="e0803-145">chaîne de connexion Hello pour votre application s’affiche dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e0803-145">hello connection string for your application is displayed in hello Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="e0803-146">API JavaScript</span><span class="sxs-lookup"><span data-stu-id="e0803-146">JavaScript APIs</span></span>
<span data-ttu-id="e0803-147">objet JavaScript global de Hello `window.capptain` a été renommé `window.azureEngagement`, mais vous pouvez utiliser hello `window.engagement` alias pour les appels d’API.</span><span class="sxs-lookup"><span data-stu-id="e0803-147">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="e0803-148">Vous ne pouvez pas utiliser cette configuration de kit de développement logiciel alias toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="e0803-148">You can't use this alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="e0803-149">Par exemple : `capptain.deviceId` devient `engagement.deviceId`, `capptain.agent.startActivity` devient `engagement.agent.startActivity`, etc.</span><span class="sxs-lookup"><span data-stu-id="e0803-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="e0803-150">Si vous avez déjà intégré une version antérieure de hello Kit de développement Web Azure Mobile Engagement dans votre application, veuillez lire [mise à niveau des procédures](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="e0803-150">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

