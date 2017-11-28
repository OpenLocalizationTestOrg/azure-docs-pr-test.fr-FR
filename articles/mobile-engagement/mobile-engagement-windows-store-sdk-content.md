---
title: "Contenu du Kit de développement logiciel (SDK) des applications Windows Universal"
description: "Découvrez le contenu du Kit de développement logiciel (SDK) des applications Windows Universal pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b28d525ab16487b963772e23fdecd11f94dcabd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="7527f-103">Contenu du Kit de développement logiciel (SDK) des applications Windows Universal</span><span class="sxs-lookup"><span data-stu-id="7527f-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="7527f-104">Ce document répertorie et décrit le contenu déployé par le Kit de développement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="7527f-104">This document lists and describes the content deployed by the SDK in your application.</span></span>

## <a name="the-resources-folder"></a><span data-ttu-id="7527f-105">Le dossier `/Resources`</span><span class="sxs-lookup"><span data-stu-id="7527f-105">The `/Resources` folder</span></span>
<span data-ttu-id="7527f-106">Ce dossier contient toutes les ressources dont Mobile Engagement a besoin.</span><span class="sxs-lookup"><span data-stu-id="7527f-106">This folder contains all the resources that Mobile Engagement needs.</span></span> <span data-ttu-id="7527f-107">Vous pouvez également les personnaliser pour les adapter à votre application.</span><span class="sxs-lookup"><span data-stu-id="7527f-107">You can also customize them to fit your app.</span></span>

* <span data-ttu-id="7527f-108">`EngagementConfiguration.xml` : fichier de configuration de Mobile Engagement. C'est dans ce fichier que vous pouvez personnaliser les paramètres de Mobile Engagement (chaîne de connexion Mobile Engagement, rapport sur les incidents, etc.).</span><span class="sxs-lookup"><span data-stu-id="7527f-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="7527f-109">Dossier /html</span><span class="sxs-lookup"><span data-stu-id="7527f-109">/html folder</span></span>
* <span data-ttu-id="7527f-110">`EngagementNotification.html` : conception html de la vue web `Notification` pour les bannières dans l'application.</span><span class="sxs-lookup"><span data-stu-id="7527f-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="7527f-111">`EngagementAnnouncement.html` : conception html de la vue web `Announcement` pour les bannières dans les vues interstitielles.</span><span class="sxs-lookup"><span data-stu-id="7527f-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="7527f-112">Dossier /images</span><span class="sxs-lookup"><span data-stu-id="7527f-112">/images folder</span></span>
* <span data-ttu-id="7527f-113">`EngagementIconNotification.png` : l’icône de marque affichée à gauche d'une notification. Remplacez celle-ci par l'icône de votre marque.</span><span class="sxs-lookup"><span data-stu-id="7527f-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="7527f-114">`EngagementIconOk.png` : l’icône `Ok` des pages de contenu de Couverture pour le bouton d'action ou de validation.</span><span class="sxs-lookup"><span data-stu-id="7527f-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span></span>
* <span data-ttu-id="7527f-115">`EngagementIconNOK.png` : l’icône `NOK` utilisée quand le bouton de validation des pages de contenu de Couverture est désactivé.</span><span class="sxs-lookup"><span data-stu-id="7527f-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span></span>
* <span data-ttu-id="7527f-116">`EngagementIconClose.png` : l’icône `Close` des notifications et du contenu de couverture pour le bouton Ignorer.</span><span class="sxs-lookup"><span data-stu-id="7527f-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="7527f-117">Dossier /overlay</span><span class="sxs-lookup"><span data-stu-id="7527f-117">/overlay folder</span></span>
* <span data-ttu-id="7527f-118">`EngagementPageOverlay.cs` : page de superposition responsable de l'ajout de l'interface utilisateur Engagement Reach dans l'application à son enfant.</span><span class="sxs-lookup"><span data-stu-id="7527f-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span></span>

