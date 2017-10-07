---
title: aaaAzure Interface utilisateur de Mobile Engagement - atteindre
description: "Découvrez comment tooreach les toohello les utilisateurs de votre application avec les notifications push à l’aide d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a>Comment tooreach les toohello les utilisateurs de votre application avec des notifications push
Cet article décrit hello **atteindre** onglet Hello **Mobile Engagement** portal. Vous utilisez hello **Mobile Engagement** toomonitor portail et gérer vos applications mobiles. Notez que toostart à l’aide du portail hello vous devez tout d’abord toocreate un **Azure Mobile Engagement** compte. Pour plus d'informations, consultez [Create an Azure Mobile Engagement account](mobile-engagement-create.md).

Hello atteindre section Hello interface utilisateur de l’outil de gestion de campagne Push hello dans laquelle vous pouvez créer/modifier/activer/fin/analyse et obtenir les statistiques sur les campagnes Push notification et les fonctionnalités qui sont également accessibles via hello API couverture (et certains éléments de hello basse niveau d’API de Push). Rappelez-vous que si vous utilisez hello API ou hello l’interface utilisateur, vous devez toointegrate Azure Mobile Engagement et portée dans votre application pour chaque plateforme avec hello SDK avant de pouvoir utiliser atteint des campagnes.

> [!NOTE]
> De nombreuses sections de hello **Mobile Engagement** interface utilisateur du portail contient hello **afficher l’aide** bouton. Appuyez sur ce bouton tooget informations contextuelles supplémentaires sur une section.
> 
> 

## <a name="four-types-of-push-notifications"></a>Quatre types de notifications Push
1. Annonces - autoriser un toosend publicité messages toousers qui redirigent les emplacement tooanother à l’intérieur de votre application ou le toosend leur page Web de tooa ou à stocker en dehors de votre application. 
2. Interroge - vous permettent d’informations de toogather aux utilisateurs finaux en posant des questions.
3. Push de données - autoriser toosend un fichier de données binaire ou en base 64. Hello les informations contenues dans un push de données sont envoyées tooyour application toomodify expérience actuelle de vos utilisateurs dans votre application. Votre application a besoin de données hello toobe tooprocess en mesure de push de données.

## <a name="campaign-details"></a>Informations relatives à la campagne
Vous pouvez modifier, cloner, supprimer ou activer les campagnes qui n’ont pas encore été activés en pointant sur leurs noms ou vous pouvez cliquer sur tooopen les. Vous pouvez cloner des campagnes qui ont déjà été activées en pointant sur leurs noms, ou vous pouvez cliquer sur tooopen les. Toutefois, vous ne pouvez pas modifier une campagne une fois celle-ci activée.

![Reach1][18]

## <a name="reach-feedback"></a>Commentaire Reach
Cliquez sur **statistiques** détails de hello toosee d’une couverture campagne. Hello **Simple** vue fournit une représentation visuelle sous forme de hello d’un graphique à barres que s’est-il passé après une campagne a été activée sur la colonne. Hello **avancé** vue fournit des détails plus précis sur la campagne de push hello. Ces informations ne sera pas disponibles si vous envoyez une campagne de test par exemple, un appareil de test tooa envoyés par émission de données. Voici comment interpréter ces détails :

1. **Objet d’un push** -spécifie nombre hello des messages transmis toohello périphériques. Ce nombre dépend visé hello que vous avez spécifié lors de la création de campagne de push hello. Si vous ne spécifiez pas de n’importe quel public cible, puis cette opération push sera envoyée tooall hello inscrit périphériques. Comme tous les autres services par émission de données, nous ne pas distribuer les notifications de hello directement les périphériques toohello mais de les transmettre à la place plateforme respectifs de toohello des Services de Notification Push (PNS - APNS/GCM/WNS) qui leur peuvent de remettre les notifications hello toohello périphériques. 
2. **Remis** -spécifie nombre hello de messages qui sont correctement remis par l’appareil de toohello PNS hello et d’accusé de réception comme reçu par le Kit de développement logiciel de Mobile Engagement. 
   
   *Raisons pour lesquelles le nombre de messages remis est inférieur au nombre de notifications Push :*
   
   1. Si l’utilisateur de hello a désinstallé l’application hello à partir de l’appareil de hello mais hello PNS ne connaît au moment de hello que nous envoyer hello push toohello PNS message de type hello est supprimé.
   2. Si les appareils hello a application hello sans périphériques hello eux-mêmes étaient hors connexion pendant de longues périodes de temps, puis hello PNS échouera appareil de toohello toodeliver hello message. 
   3. Si message de type hello remis toohello appareil mais hello Kit de développement logiciel de Mobile Engagement dans l’application hello ne reconnaît pas le contenu du message de type hello hello, il dépose ensuite ce message. Cela peut se produire si la personnalisation hello de notification hello dans l’application hello génère une exception qui nous catch dans le message de salutation SDK et drop hello. Cela peut également se produire si l’application hello sur l’appareil de hello est à l’aide d’une version de hello Mobile Engagement Kit de développement logiciel qui n’est pas de version plus récente de hello toounderstand en mesure de message de type hello par émission de données envoyées à partir de la plateforme de hello, mais uniquement lorsque l’application hello a été mis à niveau après la notification de hello a été distribuée à partir de la plateforme de service hello. Hello **avancé** onglet indique combien de messages ont été supprimés. 
   4. Sur les appareils iOS, messages parfois ne pas remis si l’appareil hello est sur batterie faible ou si l’application hello consomme une quantité importante de puissance lors du traitement des notifications à distance. Il s’agit d’une limitation des appareils iOS de hello.   
3. **Affiche** -spécifie nombre hello de messages qui sont correctement affichés toohello utilisateur d’applications sur l’appareil hello sous forme de hello d’une notification push/out-de-l’application de système dans le centre de notifications hello ou une notification dans l’application au sein de hello mobile application.  Hello **avancé** onglet vous indique combien ont été les notifications système et combien ont été les notifications dans l’application. 
   
   *Nombre de raisons affichées est inférieur au nombre de remis (toobe attente affiché)*
   
   1. Si la campagne de notification hello avait une date de fin sur celui-ci, il est possible que la remise de notification de hello, mais lorsque le temps de hello fournie tooopen et l’afficher toohello utilisateur d’applications, elle a déjà expiré afin qu’il n’a jamais été affiche.   
   2. Si une notification de hello est une notification dans l’application notifications de hello s’affiche uniquement lorsque l’utilisateur d’application hello ouvre l’application hello. Dans les cas où les utilisateurs d’application hello n’a pas ouvert application hello, hello SDK signalera que notification de hello a été remise mais pas encore affichée jusqu'à ce que l’application hello est ouvert. 
   3. Si la notification de hello est une notification dans l’application et configuré toobe indiqué sur un activité spécifique/écran puis également notification de hello est signalée comme remis mais n’ont ne pas encore été remis en tant qu’utilisateur de hello ouvre application hello sur un écran spécifique. 
4. **Interactions de l’utilisateur** -Spécifie le nombre de hello de messages utilisateur application hello interagisse avec et inclut des messages hello sont actionnés ou quittés. 
   
   * *utilisateur d’application Hello peut actionner une notification, que ce soit de hello suivant façons :*
     
     1. Si hello notification est une notification système/out-de-l’application ou une notification dans l’application est envoyé en tant que notification uniquement utilisateur d’application hello clique ensuite sur la notification de hello.
     2. Si les notifications hello sont une notification dans l’application avec un texte ou un affichage de web ou sondages hello puis utilisateur de l’application clique sur hello bouton d’Action de notification de hello.
     3. Si une notification de hello est une notification dans l’application avec un affichage web puis hello application utilisateur clique sur une URL dans hello web [Android uniquement]
   * *utilisateur d’application Hello peut quitter une notification, que ce soit de hello suivant façons :*
     
     1. Bouton hello fermer de notification de hello directement. 
     2. Le glissement absent ou suppression de notification de hello. 
     3. Notifications dans l’application avec le contenu de texte/web et les sondages sont généralement affichées toohello utilisateur d’applications dans un processus en deux étapes. Ils reçoivent une notification tout d’abord, et lorsqu’ils cliquent dessus, ils voient du contenu texte/web/interrogation hello. utilisateur d’application Hello peut quitter une notification dans une de ces étapes et les détails de hello dans la vue avancée de hello capture cela. 
5. **Déclenchée** -cela spécifie le nombre de hello de messages qui ont été explicitement déclenchée par l’utilisateur d’application hello. Il s’agit de nombre plus intéressant de hello cela indique à combien d’utilisateurs application intéressés par le message de type hello poussé dans la notification de hello. 

> [!NOTE]
> Sur iOS et les plateformes Windows, si utilisateur de hello a application hello ouvrir et la campagne de hello était une campagne « À tout moment », il est possible que les notifications d’application et dans l’application sont affichées sur hello même temps. Cela peut entraîner un nombre affiché supérieur hello remis. Si hello utilisateur interagit ou une notification actions hello, hello puis même nombre d’Interactions d’utilisateur/Actioned peut être supérieur à remis. 
> 
> 

![Reach2][19]

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

