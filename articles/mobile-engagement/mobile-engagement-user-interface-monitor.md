---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - analyse"
description: "Découvrez comment toomonitor des données en temps réel sur votre application à l’aide d’Azure Mobile Engagement"
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
ms.openlocfilehash: 3a581e4166bc88e6ee7aa784d4047c94533685b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-real-time-data-about-your-application"></a>Comment toomonitor des données en temps réel sur votre application
Cet article décrit hello **moniteur** onglet Hello **Mobile Engagement** portal. Vous utilisez hello **Mobile Engagement** toomonitor portail et gérer vos applications mobiles. Notez que toostart à l’aide du portail hello vous devez tout d’abord toocreate un **Azure Mobile Engagement** compte. 

Hello section Moniteur de hello l’interface utilisateur fournit des informations de l’analytique en temps réel et vous permet de tooset alertes lorsque les seuils sont atteints pour la plupart des hello même informations disponibles par le passé dans hello [ANALYTICS](mobile-engagement-user-interface-analytics.md) section de Hello l’interface utilisateur. Consultez hello **glossaire** section Bonjour [Concepts](http://go.microsoft.com/fwlink/?LinkId=525555) rubrique pour les définitions des termes et abréviations Analytique et de surveillance (tels que les suivants hello : utilisateur actif, le nouvel utilisateur, conservées un utilisateur, la Session, Graphique de chemin d’accès d’utilisateur, les utilisateurs carte, URL de suivi, les tendances, activité, événements, travail, erreur, des informations supplémentaires, panne et App-info).

> [!NOTE]
> De nombreuses sections de hello **Mobile Engagement** interface utilisateur du portail contient hello **afficher l’aide** bouton. Appuyez sur ce bouton tooget informations contextuelles supplémentaires sur une section.
> 
> 

## <a name="monitor---sessions-jobs-events-errors-and-crashes"></a>Surveillance - Sessions, travaux, événements, erreurs et incidents
Vous pouvez afficher le nombre d'utilisateurs actuellement dans une session, les écrans sur lesquels ils se trouvent et les actions spécifiques qu'ils effectuent. Vous pouvez afficher l'activité de l'utilisateur répartie selon les sessions, les tâches, les événements, les erreurs et les incidents. Vous pouvez voir les informations actuelles hello et affichent des informations de la hello de hello dernière heure, jour ou semaine. Vous pouvez voir toutes les informations de hello dans chaque catégorie ou trier hello spécifique de Session, tâche, événement, erreur et incident.  La surveillance dynamique est utile toouse lors d’événements comme un toosee de campagne Push s’il existe un relèvement en action droit une fois que vous envoyez votre notification Push.

![Moniteur1][14]  

## <a name="troubleshooting-with-monitor---events---details"></a>Résolution des problèmes liés à la section Surveillance - Événements - Détails
Génère un événement dans votre application à partir de votre appareil de test et en recherchant dans le moniteur - événements - détails soient un des plus simple toofind façons hello, ID de votre appareil pour votre appareil de test et le tooconfirm que l’intégration de l’Analytique, surveillance, Azure Mobile Engagement et L’utilisation de segments à partir de votre application. Après avoir hello ID de périphérique de votre appareil de test, vous pouvez les ajouter à des appareils de test tooyour dans « Mes appareils – de compte ». Si vous ne pouvez pas générer un événement, assurez-vous que Azure Mobile Engagement est correctement intégré dans votre application Android/iOS/Web/Windows/Windows Phone avec hello SDK.

Pour plus d’informations, consultez la [documentation du Kit de développement logiciel (SDK)][Link 5]

![Moniteur2][15]  

## <a name="troubleshooting-with-monitor---crashes---details"></a>Résolution des problèmes liés à la section Surveillance - Incidents - Détails
Vous pouvez consulter les informations d’incident sur votre application à partir des détails du moniteur - pannes - toohelp déterminer pourquoi votre application se bloque. Vous devez également rechercher des problèmes connus avec chaque version du Kit de développement logiciel de hello dans les notes de publication hello pour chaque version de hello SDK pour Android/iOS/Web/Windows/Windows Phone.

Pour plus d’informations, consultez la [documentation du Kit de développement logiciel (SDK) et les notes de publication][Link 5]

![Moniteur3][16]

## <a name="monitor---alerts"></a>Analyse - Alertes
Vous pouvez également spécifier des conditions pour les alertes qui seront envoyées automatiquement tooyou par courrier électronique ou message instantané. (Tout les services conformes à XMPP tels que Google Talk de Google ou iChat d'Apple sont pris en charge). Les alertes sont basées sur un seuil de détection prédéfini supérieur (>) ou inférieur à (<) un nombre spécifique de sessions, de tâches, d'événements, d'erreurs ou d'incidents par seconde, par minute ou par heure. Les alertes peuvent surveiller toutes les activités d'un type donné ou simplement surveiller l'activité d'une tâche, d'un événement ou d'une erreur spécifique. 

Vous pouvez également spécifier un taux de détection minimal, qui est la quantité minimale de hello de minutes qui séparera deux notifications pour hello même alerte toomake garantit que quand votre alerte est déclenchée, vous ne recevrez jamais supérieure à 1 notification par intervalle spécifié.

![Moniteur4][17]

## <a name="see-also"></a>Voir aussi
* [Concepts][Link 6]
* [Service de guide de résolution des problèmes][Link 24]

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
