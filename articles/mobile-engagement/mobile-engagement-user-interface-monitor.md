---
title: Interface utilisateur d'Azure Mobile Engagement - Moniteur
description: "En savoir plus sur la surveillance des données en temps réel de votre application à l’aide d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b91ad89a-b89d-4377-abb0-cc2d16a2836d
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5f8a02e35db93585e0fe46d77b3ad18b94c99597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-monitor-real-time-data-about-your-application"></a><span data-ttu-id="ac97f-103">Surveillance des données en temps réel de votre application</span><span class="sxs-lookup"><span data-stu-id="ac97f-103">How to monitor real-time data about your application</span></span>
<span data-ttu-id="ac97f-104">Cet article décrit l’onglet **SURVEILLER** du portail **Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="ac97f-104">This article describes the **MONITOR** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="ac97f-105">Le portail **Mobile Engagement** sert à surveiller et à gérer vos applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="ac97f-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="ac97f-106">Notez que pour utiliser le portail, vous devez tout d’abord créer un compte **Azure Mobile Engagement** .</span><span class="sxs-lookup"><span data-stu-id="ac97f-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> 

<span data-ttu-id="ac97f-107">La section Surveiller de l’interface utilisateur offre des analyses en temps réel et vous permet de définir des alertes lorsque des seuils sont atteints pour la plupart des informations disponibles dans l’historique de la section [Analyse](mobile-engagement-user-interface-analytics.md) de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ac97f-107">The Monitor section of the UI provides real-time analytics information and allows you to set alerts when thresholds are reached for most of the same information that is available historically in the [ANALYTICS](mobile-engagement-user-interface-analytics.md) section of the UI.</span></span> <span data-ttu-id="ac97f-108">Consultez la section **Glossaire** de la rubrique [Concepts](http://go.microsoft.com/fwlink/?LinkId=525555) qui présente les définitions des termes et abréviations indiqués dans Analyse et Surveillance, notamment : utilisateur actif, nouvel utilisateur, utilisateur conservé, session, graphique du chemin d’accès utilisateur, mappage des utilisateurs, URL de suivi, tendances, activité, événement, travail, erreur, informations supplémentaires, incident et informations sur l’application.</span><span class="sxs-lookup"><span data-stu-id="ac97f-108">See the **Glossary** section in the [Concepts](http://go.microsoft.com/fwlink/?LinkId=525555) topic for definitions of terms and abbreviations in Analytics and Monitoring (such as the following: Active User, New user, Retained User, Session, User Path Graph, Users Map, Tracking URLs, Trends, Activity, Event, Job, Error, Extra Info, Crash, and App-info).</span></span>

> [!NOTE]
> <span data-ttu-id="ac97f-109">De nombreuses sections de l’interface utilisateur du portail **Mobile Engagement** contiennent un bouton **AFFICHER L’AIDE**.</span><span class="sxs-lookup"><span data-stu-id="ac97f-109">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="ac97f-110">Appuyez sur ce bouton pour obtenir des informations contextuelles supplémentaires sur une section.</span><span class="sxs-lookup"><span data-stu-id="ac97f-110">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="monitor---sessions-jobs-events-errors-and-crashes"></a><span data-ttu-id="ac97f-111">Surveillance - Sessions, travaux, événements, erreurs et incidents</span><span class="sxs-lookup"><span data-stu-id="ac97f-111">Monitor - Sessions, Jobs, Events, Errors, and Crashes</span></span>
<span data-ttu-id="ac97f-112">Vous pouvez afficher le nombre d'utilisateurs actuellement dans une session, les écrans sur lesquels ils se trouvent et les actions spécifiques qu'ils effectuent.</span><span class="sxs-lookup"><span data-stu-id="ac97f-112">You can see how many users are currently in session and on specific screens or doing specific actions.</span></span> <span data-ttu-id="ac97f-113">Vous pouvez afficher l'activité de l'utilisateur répartie selon les sessions, les tâches, les événements, les erreurs et les incidents.</span><span class="sxs-lookup"><span data-stu-id="ac97f-113">You can view user activity divided by Sessions, Jobs, Events, Errors, and Crashes.</span></span> <span data-ttu-id="ac97f-114">Vous pouvez voir l'information actuelle ainsi que les informations de la dernière heure, du dernier jour ou de la dernière semaine.</span><span class="sxs-lookup"><span data-stu-id="ac97f-114">You can see the current information and show the information from the last hour, day, or week.</span></span> <span data-ttu-id="ac97f-115">Vous pouvez voir toutes les informations dans chaque catégorie ou les trier suivant la session, la tâche, l'événement, l'erreur ou l'incident.</span><span class="sxs-lookup"><span data-stu-id="ac97f-115">You can see all of the information in each category or sort by the specific Session, Job, Event, Error, and Crash.</span></span>  <span data-ttu-id="ac97f-116">La surveillance directe est utile lors d'événements tels qu'une campagne Push pour voir si l'action est en légère hausse juste après l'envoi de votre notification Push.</span><span class="sxs-lookup"><span data-stu-id="ac97f-116">Live monitoring is helpful to use during events such as a Push campaign to see if there is an uptick in action right after you send your Push notification.</span></span>

![Moniteur1][14]  

## <a name="troubleshooting-with-monitor---events---details"></a><span data-ttu-id="ac97f-118">Résolution des problèmes liés à la section Surveillance - Événements - Détails</span><span class="sxs-lookup"><span data-stu-id="ac97f-118">Troubleshooting with Monitor - Events - Details</span></span>
<span data-ttu-id="ac97f-119">La génération d'un événement dans votre application à partir de votre appareil de test et sa recherche dans Surveillance - Événements - Détails est l'un des moyens les plus faciles pour trouver l'ID de votre appareil pour votre appareil de test et pour confirmer que l'intégration des sections Analyse, Surveillance et Segments par Azure Mobile Engagement fonctionne à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="ac97f-119">Generating an event in your application from your test device and finding it in Monitor - Events - Details is one of the easiest ways to find your Device ID for your test device and to confirm that Azure Mobile Engagement integration of Analytics, Monitoring, and Segments is working from your application.</span></span> <span data-ttu-id="ac97f-120">Une fois que vous avez l'ID de l'appareil de votre appareil de test, vous pouvez l'ajouter à vos appareils de test dans « Mon compte - Appareils ».</span><span class="sxs-lookup"><span data-stu-id="ac97f-120">Once you have the Device ID of your test device, you can add it to your test devices in “My Account - Devices”.</span></span> <span data-ttu-id="ac97f-121">Si vous ne parvenez pas à générer un événement, assurez-vous qu'Azure Mobile Engagement est bien intégré à votre application Android, iOS, Web, Windows ou Windows Phone à l'aide du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="ac97f-121">If you can't generate an event, make sure that Azure Mobile Engagement is correctly integrated in your Android/iOS/Web/Windows/Windows Phone app with the SDK.</span></span>

<span data-ttu-id="ac97f-122">Pour plus d’informations, consultez la [documentation du Kit de développement logiciel (SDK)][Link 5]</span><span class="sxs-lookup"><span data-stu-id="ac97f-122">For more information, see:  [SDK Documentation][Link 5]</span></span>

![Moniteur2][15]  

## <a name="troubleshooting-with-monitor---crashes---details"></a><span data-ttu-id="ac97f-124">Résolution des problèmes liés à la section Surveillance - Incidents - Détails</span><span class="sxs-lookup"><span data-stu-id="ac97f-124">Troubleshooting with Monitor - Crashes - Details</span></span>
<span data-ttu-id="ac97f-125">Vous pouvez consulter les informations relatives à l'incident de votre application dans Surveillance - Incidents - Détails pour vous aider à déterminer les raisons de l'incident survenu dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ac97f-125">You can review crash information about your app from Monitor - Crashes - Details to help determine why your app is crashing.</span></span> <span data-ttu-id="ac97f-126">Nous vous invitons à chercher également des problèmes connus avec chaque version du Kit de développement logiciel (SDK) dans les notes de publication pour chaque version du Kit de développement logiciel (SDK) pour Android, iOS, Web, Windows et Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="ac97f-126">You should also look up known issues with each version of the SDK in the release notes for each version of the SDK for Android/iOS/Web/Windows/Windows Phone.</span></span>

<span data-ttu-id="ac97f-127">Pour plus d’informations, consultez la [documentation du Kit de développement logiciel (SDK) et les notes de publication][Link 5]</span><span class="sxs-lookup"><span data-stu-id="ac97f-127">For more information, see:  [SDK Documentation - Release notes][Link 5]</span></span>

![Moniteur3][16]

## <a name="monitor---alerts"></a><span data-ttu-id="ac97f-129">Analyse - Alertes</span><span class="sxs-lookup"><span data-stu-id="ac97f-129">Monitor - Alerts</span></span>
<span data-ttu-id="ac97f-130">Vous pouvez également indiquer des conditions pour des alertes qui vous seront automatiquement envoyées par courrier électronique ou message instantané.</span><span class="sxs-lookup"><span data-stu-id="ac97f-130">You can also specify conditions for Alerts that will be automatically sent to you via e-mail or instant message.</span></span> <span data-ttu-id="ac97f-131">(Tout les services conformes à XMPP tels que Google Talk de Google ou iChat d'Apple sont pris en charge). Les alertes sont basées sur un seuil de détection prédéfini supérieur (>) ou inférieur à (<) un nombre spécifique de sessions, de tâches, d'événements, d'erreurs ou d'incidents par seconde, par minute ou par heure.</span><span class="sxs-lookup"><span data-stu-id="ac97f-131">(Any XMPP-compliant services like Google's GTalk or Apple's iChat are supported.) Alerts are based on a pre-defined detection threshold greater than (>) or less than (<) a specific number of Sessions, Jobs, Events, Errors, or Crashes per second, minute, or hour.</span></span> <span data-ttu-id="ac97f-132">Les alertes peuvent surveiller toutes les activités d'un type donné ou simplement surveiller l'activité d'une tâche, d'un événement ou d'une erreur spécifique.</span><span class="sxs-lookup"><span data-stu-id="ac97f-132">Alerts can monitor all activities of a given type, or just monitor a specific Job, Event, or Error activity.</span></span> 

<span data-ttu-id="ac97f-133">Vous pouvez également indiquer un taux de détection minimum qui correspond au nombre de minutes minimal entre deux notifications pour la même alerte afin de vous assurer que, lorsque l’alerte est déclenchée, vous ne recevez qu’une notification par intervalle spécifié.</span><span class="sxs-lookup"><span data-stu-id="ac97f-133">You can also specify a Minimum Detection Rate, which is the minimum amount of minutes that will separate two notifications for the same alert to make sure that when your alert is triggered, you will never receive more than 1 notification per interval specified.</span></span>

![Moniteur4][17]

## <a name="see-also"></a><span data-ttu-id="ac97f-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ac97f-135">See also</span></span>
* <span data-ttu-id="ac97f-136">[Concepts][Link 6]</span><span class="sxs-lookup"><span data-stu-id="ac97f-136">[Concepts][Link 6]</span></span>
* <span data-ttu-id="ac97f-137">[Service de guide de résolution des problèmes][Link 24]</span><span class="sxs-lookup"><span data-stu-id="ac97f-137">[Troubleshooting Guide Service][Link 24]</span></span>

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
