---
title: "Procédures de mise à niveau du SDK web Azure Mobile Engagement | Microsoft Docs"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) web pour Azure Mobile Engagement"
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
ms.openlocfilehash: afa8037dcb7a53042fa606e2c4014b442d4be326
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="c1fb9-103">Procédures de mise à niveau du SDK web Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c1fb9-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="c1fb9-104">Si vous avez déjà intégré une version antérieure du Kit de développement logiciel (SDK) web Azure Mobile Engagement à votre application web, vous devez considérer les points suivants lorsque vous mettez à niveau le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="c1fb9-104">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your web application, you need to consider the following points when you upgrade the SDK.</span></span>

<span data-ttu-id="c1fb9-105">Si vous avez ignoré plusieurs versions du Kit de développement logiciel (SDK) web Azure Mobile Engagement, vous devrez peut-être effectuer plusieurs procédures pendant le processus de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-105">If you skipped multiple versions of the Mobile Engagement Web SDK, you might need to complete several procedures during the upgrade process.</span></span> <span data-ttu-id="c1fb9-106">Par exemple, si vous migrez de la version 1.4.0 vers la version 1.6.0, suivez d’abord les procédures de mise à niveau de 1.4.0 vers 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-106">For example, if you migrate from 1.4.0 to 1.6.0, first follow the procedures to upgrade from 1.4.0 to 1.5.0.</span></span> <span data-ttu-id="c1fb9-107">Puis suivez les procédures de mise à niveau de 1.5.0 vers 1.6.0.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-107">Then, follow the procedures to upgrade from 1.5.0 to 1.6.0.</span></span>

<span data-ttu-id="c1fb9-108">Quelle que soit la version à partir de laquelle vous effectuez la mise à niveau, remplacez toute version antérieure du fichier azure-engagement.js par la dernière version de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-108">Whichever version you upgrade from, replace any earlier version of the file azure-engagement.js with the latest version of the file.</span></span>

## <a name="upgrade-from-121-to-200"></a><span data-ttu-id="c1fb9-109">Mise à niveau de 1.2.1 vers 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c1fb9-109">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="c1fb9-110">Cette section décrit comment migrer une intégration du Kit de développement logiciel (SDK) web Mobile Engagement à partir du service Capptain, offert par Capptain SAS, vers une application Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-110">This section describes how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="c1fb9-111">Si vous migrez à partir d’une version antérieure, consultez le site web de Capptain pour migrer tout d’abord vers 1.2.1, puis appliquez la procédure suivante.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-111">If you are migrating from an earlier version, please consult the Capptain website to first migrate to 1.2.1, and then apply the following procedures.</span></span>

<span data-ttu-id="c1fb9-112">Cette version du Kit de développement logiciel (SDK) web Mobile Engagement ne prend pas en charge Samsung Smart TV, Opera TV, webOS ou la fonctionnalité Reach.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-112">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1fb9-113">Capptain et Azure Mobile Engagement ne représentent pas le même service.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-113">Capptain and Azure Mobile Engagement are not the same service.</span></span> <span data-ttu-id="c1fb9-114">La procédure suivante explique uniquement comment migrer l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-114">The following procedure highlights only how to migrate the client app.</span></span> <span data-ttu-id="c1fb9-115">La migration du Kit de développement logiciel (SDK) web Mobile Engagement dans l'application ne migre pas vos données d’un serveur Capptain vers un serveur Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-115">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="c1fb9-116">Fichiers JavaScript</span><span class="sxs-lookup"><span data-stu-id="c1fb9-116">JavaScript files</span></span>
<span data-ttu-id="c1fb9-117">Remplacez le fichier capptain-sdk.js par le fichier azure-engagement.js, puis mettez à jour en conséquence les importations de votre script.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-117">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="c1fb9-118">Supprimer Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="c1fb9-118">Remove Capptain Reach</span></span>
<span data-ttu-id="c1fb9-119">Cette version du Kit de développement logiciel (SDK) web Mobile Engagement ne prend pas en charge la fonctionnalité Reach.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-119">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="c1fb9-120">Si vous avez intégré Capptain Reach à votre application, vous devez la supprimer.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-120">If you integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="c1fb9-121">Supprimez l’import CSS Reach de votre page et supprimez le fichier .css associé (capptain-reach.css par défaut).</span><span class="sxs-lookup"><span data-stu-id="c1fb9-121">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="c1fb9-122">Supprimez les ressources Reach suivantes : l’image de fermeture (capptain-close.png par défaut) et l’icône de marque (capptain-notification-icon par défaut).</span><span class="sxs-lookup"><span data-stu-id="c1fb9-122">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="c1fb9-123">Supprimez l’interface utilisateur Reach pour les notifications dans l’application.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-123">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="c1fb9-124">La disposition par défaut ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="c1fb9-124">The default layout looks like this:</span></span>

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

<span data-ttu-id="c1fb9-125">Supprimez l’interface utilisateur Reach pour les annonces texte et web ainsi que pour les sondages.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-125">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="c1fb9-126">La disposition par défaut ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="c1fb9-126">The default layout looks like this:</span></span>

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

<span data-ttu-id="c1fb9-127">Supprimez l’objet `reach` de la configuration, s’il existe.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-127">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="c1fb9-128">Voici à quoi cela ressemble :</span><span class="sxs-lookup"><span data-stu-id="c1fb9-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="c1fb9-129">Supprimez toute autre personnalisation Reach, notamment les catégories.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="c1fb9-130">Supprimer les API déconseillées</span><span class="sxs-lookup"><span data-stu-id="c1fb9-130">Remove deprecated APIs</span></span>
<span data-ttu-id="c1fb9-131">Certaines API de Capptain sont déconseillées dans le Kit de développement logiciel (SDK) web Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-131">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="c1fb9-132">Supprimez tous les appels vers les API suivantes : `agent.connect`, `agent.disconnect`, `agent.pause` et `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-132">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="c1fb9-133">Supprimez toutes les instances des rappels suivants de votre configuration Capptain : `onConnected`, `onDisconnected`, `onDeviceMessageReceived` et `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-133">Remove any instances of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="c1fb9-134">Configuration</span><span class="sxs-lookup"><span data-stu-id="c1fb9-134">Configuration</span></span>
<span data-ttu-id="c1fb9-135">Mobile Engagement utilise une chaîne de connexion pour configurer les identificateurs du SDK, par exemple l'identificateur d'application.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-135">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="c1fb9-136">Remplacez l’ID d’application par votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-136">Replace the application ID with your connection string.</span></span> <span data-ttu-id="c1fb9-137">Notez que l’objet global pour la configuration du Kit de développement logiciel (SDK) passe de `capptain` à `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-137">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="c1fb9-138">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="c1fb9-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="c1fb9-139">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="c1fb9-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="c1fb9-140">La chaîne de connexion de votre application est affichée sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-140">The connection string for your application is displayed in the Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="c1fb9-141">API JavaScript</span><span class="sxs-lookup"><span data-stu-id="c1fb9-141">JavaScript APIs</span></span>
<span data-ttu-id="c1fb9-142">L’objet JavaScript global `window.capptain` a été renommé `window.azureEngagement`, mais vous pouvez utiliser l’alias `window.engagement` pour les appels d’API.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-142">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="c1fb9-143">Vous ne pouvez pas utiliser l’alias pour définir la configuration du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="c1fb9-143">You can't use the alias to define the SDK configuration.</span></span>

<span data-ttu-id="c1fb9-144">Par exemple : `capptain.deviceId` devient `engagement.deviceId`, `capptain.agent.startActivity` devient `engagement.agent.startActivity`, etc.</span><span class="sxs-lookup"><span data-stu-id="c1fb9-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

