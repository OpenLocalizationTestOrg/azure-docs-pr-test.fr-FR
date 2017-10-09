---
title: "aaaAzure Mobile Engagement l’Interface utilisateur - paramètres"
description: "Découvrez comment toomanage hello paramètres globaux de votre application à l’aide d’Azure Mobile Engagement"
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
ms.openlocfilehash: 02d4a36c591fc5e097410b7e931d1c9ce81d68d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-global-settings-of-your-application"></a>Comment toomanage hello paramètres globaux de votre application
Hello **paramètres** des options de menu disponibles pour une application dépendent de la plateforme hello de l’application hello et autorisations hello vous ont été accordées pour l’application hello. Les paramètres suivants de hello : détails, projets, Push natif, vitesse de Push, Tag (app info) et une pression commerciale. Hello, option de menu de balise (informations de l’application) de la section Paramètres hello peut être géré par votre application (à l’aide de hello SDK) ou par votre serveur principal (à l’aide de hello Device API). 

> [!NOTE]
> De nombreuses sections de hello **Mobile Engagement** interface utilisateur du portail contient hello **afficher l’aide** bouton. Appuyez sur ce bouton tooget informations contextuelles supplémentaires sur une section.
> 
> 

## <a name="details"></a>Détails
Vous permet de nom de hello toochange et une description de votre application, le propriétaire de la vue hello de votre application et vos autorisations de rôle. 

Configuration de l’Analytique vous permet de tooview ou modification jour hello semaines démarrer sur et hello durée de rétention en jours.

  ![settings1][46]

## <a name="projects"></a>Projets
Vous permet de tooselect tous les projets que vous souhaitez tooappear de votre application dans. 

Vous pouvez également rechercher un projet et afficher le nom de hello, la description, le propriétaire et vos autorisations de rôle d’un projet de votre application fait partie.

Pour plus d’informations, consultez [Documentation sur l’interface utilisateur - Accueil][Link 13]

  ![settings3][48]

## <a name="native-push"></a>Native Push
Vous permet de tooregister un nouveau certificat ou le supprimer et le certificat existant pour utilisent avec push natif. Push natif permet l’application de tooyour toopush Azure Mobile Engagement à tout moment, même quand il n’est pas en cours d’exécution. 

Après avoir entré les informations d’identification ou des certificats au moins un service de Push natif, vous pouvez sélectionner « Tout temps » lors de la création de couvertures campagne et également utiliser hello « notifiant » paramètre Bonjour API de PUSH.

### <a name="apple-push-notification-service-apns"></a>Service de notifications Push Apple (APNS)
tooenable le Push natif à l’aide de hello Apple Push Notification Service vous devez tooregister votre certificat. Vous aurez besoin de type hello de toospecify de certificat en tant que le développement (DEV) ou la production (production). Puis vous allez peut-être télécharger votre certificat et hello le mot de passe.

Pour plus d’informations, consultez : [Documentation du Kit de développement logiciel - iOS - comment tooPrepare votre Application pour les notifications Push Apple][Link 5]

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a>Service de notifications Push Windows (WPNS)
tooenable le Push natif à l’aide du Service de Notification Windows, vous devez fournir les informations d’identification de votre application. Vous aurez besoin de votre ID de sécurité (SID) de Package et la clé secrète.

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a>Google Cloud Messaging pour Android (GCM)
tooenable du Push natif à l’aide de GCM, vous avez besoin d’instructions de hello toofollow à partir de Google. Puis vous devez coller une clé d'API simple de serveur, configurée sans restriction d'adresse IP. Nécessite une intégration avec hello SDK pour Android v1.12.0 +.

Pour plus d'informations, consultez les pages suivantes : 

* [Kit de développement logiciel Documentation Android comment tooIntegrate GCM][Link 5]
* [Guide de développement Google GCM](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a>Amazon Device Messaging pour Android (ADM)
tooenable natif Push à l’aide de ADM, vous devez fournir Amazon <OAuth credentials> consistant en un ID Client et la clé secrète du Client (requiert l’intégration avec le SDK pour Android v2.1.0 +).

Pour plus d'informations, consultez les pages suivantes : 

* [Kit de développement logiciel Documentation Android comment tooIntegrate ADM][Link 5]
* [Documentation pour les développeurs Amazon ADM](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a>Push Speed
Affiche hello actuel vitesse de push de votre application et vous permet de vitesse de push hello toodefine de votre application.

  ![settings7][52]

## <a name="tag-app-info"></a>Balise (Informations sur l’application)
![settings11][56]

## <a name="commercial-pressure"></a>Pression commerciale
![settings12][57]

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

