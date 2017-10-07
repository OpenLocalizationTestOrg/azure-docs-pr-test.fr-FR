---
title: "procédures de mise à niveau de kit de développement Web Mobile Engagement aaaAzure | Documents Microsoft"
description: "Hello les dernières mises à jour et les procédures à suivre pour hello Web SDK pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="44c05-103">Procédures de mise à niveau du SDK web Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="44c05-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="44c05-104">Si vous avez déjà intégré une version antérieure de hello Kit de développement Web Azure Mobile Engagement dans votre application web, vous devez hello tooconsider points suivants lorsque vous mettez à niveau hello SDK.</span><span class="sxs-lookup"><span data-stu-id="44c05-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="44c05-105">Si vous avez ignoré plusieurs versions du Kit de développement Web Mobile Engagement de hello, vous devrez peut-être toocomplete plusieurs procédures au cours du processus de mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="44c05-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="44c05-106">Par exemple, si vous migrez à partir de 1.4.0 too1.6.0, première tooupgrade procédures hello de suivi à partir de 1.4.0 too1.5.0.</span><span class="sxs-lookup"><span data-stu-id="44c05-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="44c05-107">Ensuite, suivez hello procédures tooupgrade de 1.5.0 too1.6.0.</span><span class="sxs-lookup"><span data-stu-id="44c05-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="44c05-108">Quelle que soit la version mise à niveau à partir, remplacez toute version antérieure du fichier de hello azure-engagement.js avec la version la plus récente du fichier de hello hello.</span><span class="sxs-lookup"><span data-stu-id="44c05-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="44c05-109">Mise à niveau à partir de 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="44c05-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="44c05-110">Cette section décrit comment toomigrate une intégration du Kit de développement Web Mobile Engagement à partir du service de Capptain hello, prestation Capptain SAS, tooan Azure Mobile Engagement application.</span><span class="sxs-lookup"><span data-stu-id="44c05-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="44c05-111">Si vous effectuez une migration à partir d’une version antérieure, veuillez consulter hello toofirst du site Web Capptain migrer too1.2.1 et puis hello procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="44c05-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="44c05-112">Cette version du Kit de développement Web Mobile Engagement de hello ne prend pas en charge les TV actives Samsung, Opera TV, webOS ou fonctionnalité de couverture hello.</span><span class="sxs-lookup"><span data-stu-id="44c05-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44c05-113">Capptain et Azure Mobile Engagement ne sont pas hello même service.</span><span class="sxs-lookup"><span data-stu-id="44c05-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="44c05-114">Hello, suivant la procédure met en surbrillance uniquement comment toomigrate hello application cliente.</span><span class="sxs-lookup"><span data-stu-id="44c05-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="44c05-115">Migration hello Kit de développement Web Mobile Engagement dans l’application hello ne migre pas vos données à partir d’un serveur Capptain server tooa Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="44c05-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="44c05-116">Fichiers JavaScript</span><span class="sxs-lookup"><span data-stu-id="44c05-116">JavaScript files</span></span>
<span data-ttu-id="44c05-117">Remplacez hello fichier capptain-sdk.js par hello fichier azure-engagement.js, puis mettez à jour votre script importe en conséquence.</span><span class="sxs-lookup"><span data-stu-id="44c05-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="44c05-118">Supprimer Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="44c05-118">Remove Capptain Reach</span></span>
<span data-ttu-id="44c05-119">Cette version du Kit de développement Web Mobile Engagement de hello ne prend pas en charge la fonctionnalité de couverture hello.</span><span class="sxs-lookup"><span data-stu-id="44c05-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="44c05-120">Si vous intégré Capptain portée dans votre application, vous devez tooremove il.</span><span class="sxs-lookup"><span data-stu-id="44c05-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="44c05-121">Suppression hello atteindre le CSS importation à partir de votre page et fichier .css connexes de hello (capptain-reach.css, par défaut).</span><span class="sxs-lookup"><span data-stu-id="44c05-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="44c05-122">Supprimer hello suivant des ressources de portée : hello fermer image (capptain-close.png, par défaut) et l’icône de marque hello (capptain-notification-icône, par défaut).</span><span class="sxs-lookup"><span data-stu-id="44c05-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="44c05-123">Supprimez hello atteindre de l’interface utilisateur pour les notifications dans l’application.</span><span class="sxs-lookup"><span data-stu-id="44c05-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="44c05-124">disposition par défaut de Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="44c05-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="44c05-125">Supprimez hello atteindre de l’interface utilisateur pour les annonces de web et de texte et les sondages.</span><span class="sxs-lookup"><span data-stu-id="44c05-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="44c05-126">disposition par défaut de Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="44c05-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="44c05-127">Supprimer hello `reach` de l’objet à partir de votre configuration, si elle existe.</span><span class="sxs-lookup"><span data-stu-id="44c05-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="44c05-128">Voici à quoi cela ressemble :</span><span class="sxs-lookup"><span data-stu-id="44c05-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="44c05-129">Supprimez toute autre personnalisation Reach, notamment les catégories.</span><span class="sxs-lookup"><span data-stu-id="44c05-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="44c05-130">Supprimer les API déconseillées</span><span class="sxs-lookup"><span data-stu-id="44c05-130">Remove deprecated APIs</span></span>
<span data-ttu-id="44c05-131">Certaines API de Capptain est déconseillées dans hello Kit de développement Web Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="44c05-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="44c05-132">Supprimer tout toohello appels suivant API : `agent.connect`, `agent.disconnect`, `agent.pause`, et `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="44c05-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="44c05-133">Supprimez toutes les instances de hello suivant des rappels à partir de votre configuration Capptain : `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, et `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="44c05-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="44c05-134">Configuration</span><span class="sxs-lookup"><span data-stu-id="44c05-134">Configuration</span></span>
<span data-ttu-id="44c05-135">Mobile Engagement utilise une connexion chaîne tooconfigure Kit de développement logiciel des identificateurs, par exemple, identificateur d’application hello.</span><span class="sxs-lookup"><span data-stu-id="44c05-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="44c05-136">Remplacez l’ID de l’application hello avec votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="44c05-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="44c05-137">Notez qu’objet global hello de hello configuration du Kit de développement logiciel passe de `capptain` trop`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="44c05-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="44c05-138">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="44c05-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="44c05-139">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="44c05-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="44c05-140">chaîne de connexion Hello pour votre application s’affiche dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="44c05-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="44c05-141">API JavaScript</span><span class="sxs-lookup"><span data-stu-id="44c05-141">JavaScript APIs</span></span>
<span data-ttu-id="44c05-142">objet JavaScript global de Hello `window.capptain` a été renommé `window.azureEngagement` mais vous pouvez utiliser hello `window.engagement` alias pour les appels d’API.</span><span class="sxs-lookup"><span data-stu-id="44c05-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="44c05-143">Vous ne pouvez pas utiliser configuration de kit de développement logiciel hello alias toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="44c05-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="44c05-144">Par exemple : `capptain.deviceId` devient `engagement.deviceId`, `capptain.agent.startActivity` devient `engagement.agent.startActivity`, etc.</span><span class="sxs-lookup"><span data-stu-id="44c05-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

