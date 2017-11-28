---
title: "Interface utilisateur d'Azure Mobile Engagement : Paramètres"
description: "Découvrez comment gérer les paramètres globaux de votre application grâce à Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 858f4cb4-14de-4bb5-826f-28cadbfc928b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af5c81df2b9f288161b38625d3ac2adde8fb195d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-global-settings-of-your-application"></a><span data-ttu-id="dcef6-103">Comment gérer les paramètres globaux de votre application</span><span class="sxs-lookup"><span data-stu-id="dcef6-103">How to manage the global settings of your application</span></span>
<span data-ttu-id="dcef6-104">Les options de menu **Paramètres** disponibles pour une application dépendent de la plateforme de l’application et des autorisations qui vous ont été accordées pour cette application.</span><span class="sxs-lookup"><span data-stu-id="dcef6-104">The **Settings** menu options available for an application vary, depending on the platform of the application and the permissions you have been granted for the application.</span></span> <span data-ttu-id="dcef6-105">Les paramètres suivants sont inclus : Détails, Projets, Native Push, Push Speed, Balise (Information sur l’application) et Pression commerciale.</span><span class="sxs-lookup"><span data-stu-id="dcef6-105">Settings include the following: Details, Projects, Native Push, Push Speed, Tag (app info), and Commercial Pressure.</span></span> <span data-ttu-id="dcef6-106">L’option de menu Balise (Informations sur l’application) peut être gérée par votre application (à l’aide du Kit de développement logiciel (SDK)) ou par votre backend (à l’aide de l’API d’appareil).</span><span class="sxs-lookup"><span data-stu-id="dcef6-106">The Tag (app info) menu option of the Settings section can be managed by your application (using the SDK) or by your backend (using the Device API).</span></span> 

> [!NOTE]
> <span data-ttu-id="dcef6-107">De nombreuses sections de l’interface utilisateur du portail **Mobile Engagement** contiennent un bouton **AFFICHER L’AIDE**.</span><span class="sxs-lookup"><span data-stu-id="dcef6-107">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="dcef6-108">Appuyez sur ce bouton pour obtenir des informations contextuelles supplémentaires sur une section.</span><span class="sxs-lookup"><span data-stu-id="dcef6-108">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="details"></a><span data-ttu-id="dcef6-109">Détails</span><span class="sxs-lookup"><span data-stu-id="dcef6-109">Details</span></span>
<span data-ttu-id="dcef6-110">Permet de modifier le nom et la description de votre application, d’afficher le propriétaire de votre application et vos autorisations de rôle.</span><span class="sxs-lookup"><span data-stu-id="dcef6-110">Allows you to change the name and description of your application, view the owner of your application and your role permissions.</span></span> 

<span data-ttu-id="dcef6-111">La configuration de l’analytique permet d’afficher ou de modifier le jour du début de semaine et la durée de rétention en jour(s).</span><span class="sxs-lookup"><span data-stu-id="dcef6-111">Analytics configuration enables  you to view or change the day weeks start on and the retention time in day(s).</span></span>

  ![settings1][46]

## <a name="projects"></a><span data-ttu-id="dcef6-113">Projets</span><span class="sxs-lookup"><span data-stu-id="dcef6-113">Projects</span></span>
<span data-ttu-id="dcef6-114">Vous pouvez sélectionner tous les projets que vous souhaitez voir apparaître dans votre application.</span><span class="sxs-lookup"><span data-stu-id="dcef6-114">Allows you to select all projects you want your application to appear in.</span></span> 

<span data-ttu-id="dcef6-115">Vous pouvez également rechercher un projet et afficher le nom, la description, le propriétaire et vos autorisations de rôle pour n'importe quel projet dont votre application fait partie.</span><span class="sxs-lookup"><span data-stu-id="dcef6-115">You can also search for a project and view the name, description, owner and your role permissions of any project your application is part of.</span></span>

<span data-ttu-id="dcef6-116">Pour plus d’informations, consultez [Documentation sur l’interface utilisateur - Accueil][Link 13]</span><span class="sxs-lookup"><span data-stu-id="dcef6-116">For more information, see: [UI Documentation – Home][Link 13]</span></span>

  ![settings3][48]

## <a name="native-push"></a><span data-ttu-id="dcef6-118">Native Push</span><span class="sxs-lookup"><span data-stu-id="dcef6-118">Native Push</span></span>
<span data-ttu-id="dcef6-119">Vous pouvez inscrire un nouveau certificat ou supprimer un certificat existant pour une utilisation avec Native Push.</span><span class="sxs-lookup"><span data-stu-id="dcef6-119">Allows you to register a new certificate or delete and existing certificate for use with native push.</span></span> <span data-ttu-id="dcef6-120">Native Push permet à Azure Mobile Engagement de transmettre des opérations push à votre application à tout moment, même lorsqu'elle n'est pas en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="dcef6-120">Native Push enables Azure Mobile Engagement to push to your application at any time, even when it is not running.</span></span> 

<span data-ttu-id="dcef6-121">Après avoir fourni des informations d'identification ou des certificats pour au moins un service Native Push, vous pouvez sélectionner « Tout le temps » lors de la création de campagnes Reach et également utiliser le paramètre « Notification » dans l'API de PUSH.</span><span class="sxs-lookup"><span data-stu-id="dcef6-121">After providing credentials or certificates for at least one Native Push service, you can select "Any time" when creating Reach Campaigns, and also use the "notifier" parameter in the PUSH API.</span></span>

### <a name="apple-push-notification-service-apns"></a><span data-ttu-id="dcef6-122">Service de notifications Push Apple (APNS)</span><span class="sxs-lookup"><span data-stu-id="dcef6-122">Apple Push Notification Service (APNS)</span></span>
<span data-ttu-id="dcef6-123">Pour activer Native Push à l'aide du Service de notifications Push Apple (APNS), vous devez enregistrer votre certificat.</span><span class="sxs-lookup"><span data-stu-id="dcef6-123">To enable Native Push using the Apple Push Notification Service you will need to register your certificate.</span></span> <span data-ttu-id="dcef6-124">Vous devrez spécifier le type de certificat, soit de développement (DEV), soit de production (PROD).</span><span class="sxs-lookup"><span data-stu-id="dcef6-124">You will need to specify the type of certificate as either development (DEV) or production (PROD).</span></span> <span data-ttu-id="dcef6-125">Vous allez ensuite devoir charger votre certificat et définir son mot de passe.</span><span class="sxs-lookup"><span data-stu-id="dcef6-125">Then you will need upload your certificate and the password.</span></span>

<span data-ttu-id="dcef6-126">Pour plus d’informations, consultez [Documentation du Kit de développement logiciel (SDK) - iOS - Préparation de votre application pour les notifications Push Apple][Link 5]</span><span class="sxs-lookup"><span data-stu-id="dcef6-126">For more information, see: [SDK Documentation - iOS - How to Prepare your Application for Apple Push notifications][Link 5]</span></span>

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a><span data-ttu-id="dcef6-128">Service de notifications Push Windows (WPNS)</span><span class="sxs-lookup"><span data-stu-id="dcef6-128">Windows Push Notification Service (WPNS)</span></span>
<span data-ttu-id="dcef6-129">Pour activer Native Push à l'aide du Service de notifications Push Windows (WPNS), vous devez fournir les informations d'identification de votre application.</span><span class="sxs-lookup"><span data-stu-id="dcef6-129">To enable Native Push using Windows Notification Service, you must provide your application's credentials.</span></span> <span data-ttu-id="dcef6-130">Vous aurez besoin de votre ID de sécurité (SID) de Package et la clé secrète.</span><span class="sxs-lookup"><span data-stu-id="dcef6-130">You will need your Package security identifier (SID) and your Secret key.</span></span>

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a><span data-ttu-id="dcef6-132">Google Cloud Messaging pour Android (GCM)</span><span class="sxs-lookup"><span data-stu-id="dcef6-132">Google Cloud Messaging for Android (GCM)</span></span>
<span data-ttu-id="dcef6-133">Pour activer le Push Native à l'aide de GCM, vous devez suivre les instructions fournies par Google.</span><span class="sxs-lookup"><span data-stu-id="dcef6-133">To enable Native Push using GCM, you need to follow the instructions from Google.</span></span> <span data-ttu-id="dcef6-134">Puis vous devez coller une clé d'API simple de serveur, configurée sans restriction d'adresse IP.</span><span class="sxs-lookup"><span data-stu-id="dcef6-134">Then you must paste a server simple API key, configured without IP restrictions.</span></span> <span data-ttu-id="dcef6-135">Requiert l'intégration avec le Kit de développement logiciel (SDK) pour Android v1.12.0 +.</span><span class="sxs-lookup"><span data-stu-id="dcef6-135">Requires integration with the SDK for Android v1.12.0+.</span></span>

<span data-ttu-id="dcef6-136">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="dcef6-136">For more information, see:</span></span> 

* <span data-ttu-id="dcef6-137">[Documentation du Kit de développement logiciel (SDK) Android - Intégrer GCM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="dcef6-137">[SDK Documentation Android How to Integrate GCM][Link 5]</span></span>
* [<span data-ttu-id="dcef6-138">Guide de développement Google GCM</span><span class="sxs-lookup"><span data-stu-id="dcef6-138">Google Developer GCM Guide</span></span>](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a><span data-ttu-id="dcef6-139">Amazon Device Messaging pour Android (ADM)</span><span class="sxs-lookup"><span data-stu-id="dcef6-139">Amazon Device Messaging for Android (ADM)</span></span>
<span data-ttu-id="dcef6-140">Pour activer Native Push avec Amazon Device Messaging (ADM), vous devez fournir des <OAuth credentials> Amazon qui consistent en un ID Client et Secret Client (requiert l'intégration avec le Kit de développement logiciel (SDK) pour Android v2.1.0 +).</span><span class="sxs-lookup"><span data-stu-id="dcef6-140">To enable Native Push using ADM, you must provide Amazon <OAuth credentials> consisting of a Client ID and Client Secret (Requires integration with SDK for Android v2.1.0+).</span></span>

<span data-ttu-id="dcef6-141">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="dcef6-141">For more information, see:</span></span> 

* <span data-ttu-id="dcef6-142">[Documentation du Kit de développement logiciel (SDK) Android - Intégrer ADM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="dcef6-142">[SDK Documentation Android How to Integrate ADM][Link 5]</span></span>
* [<span data-ttu-id="dcef6-143">Documentation pour les développeurs Amazon ADM</span><span class="sxs-lookup"><span data-stu-id="dcef6-143">Amazon Developer ADM Documentation</span></span>](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a><span data-ttu-id="dcef6-145">Push Speed</span><span class="sxs-lookup"><span data-stu-id="dcef6-145">Push Speed</span></span>
<span data-ttu-id="dcef6-146">Vous pouvez afficher la vitesse de transmission actuelle de votre application et définir la vitesse de transmission de votre application.</span><span class="sxs-lookup"><span data-stu-id="dcef6-146">Shows the current push speed of your application and allows you to define the push speed of your application.</span></span>

  ![settings7][52]

## <a name="tag-app-info"></a><span data-ttu-id="dcef6-148">Balise (Informations sur l’application)</span><span class="sxs-lookup"><span data-stu-id="dcef6-148">Tag (app info)</span></span>
![settings11][56]

## <a name="commercial-pressure"></a><span data-ttu-id="dcef6-150">Pression commerciale</span><span class="sxs-lookup"><span data-stu-id="dcef6-150">Commercial Pressure</span></span>
![settings12][57]

## <a name="see-also"></a><span data-ttu-id="dcef6-152">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="dcef6-152">See also</span></span>
* <span data-ttu-id="dcef6-153">[Concepts][Link 6]</span><span class="sxs-lookup"><span data-stu-id="dcef6-153">[Concepts][Link 6]</span></span>
* <span data-ttu-id="dcef6-154">[Service de guide de résolution des problèmes][Link 24]</span><span class="sxs-lookup"><span data-stu-id="dcef6-154">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

