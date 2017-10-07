---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - Segments"
description: "Découvrez comment toocreate et gèrent des segments de modèles d’utilisation tooidentify les utilisateurs à l’aide d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a>Comment toocreate et gèrent des segments de modèles d’utilisation tooidentify les utilisateurs
Cet article décrit hello **SEGMENTS** onglet Hello **Mobile Engagement** portal. Vous utilisez hello **Mobile Engagement** toomonitor portail et gérer vos applications mobiles.

section de Segments Hello Hello l’interface utilisateur vous permet de toowork sur la segmentation de vos utilisateurs basés sur un comportement différent hello et analytique que vous pouvez obtenir à partir de l’application hello et est également accessible via l’API de Segments de hello. Segments sont calculées tout d’abord de 24 heures après leur création, et ils sont recalculées toutes les 24 heures en fonction de l’actualité analytique hello. Une fois qu’un segment est calculé, il affiche un graphique de « L’historique de jour tooday » chaque jour.

> [!NOTE]
> De nombreuses sections de hello **Mobile Engagement** interface utilisateur du portail contient hello **afficher l’aide** bouton. Appuyez sur ce bouton tooget informations contextuelles supplémentaires sur une section.
> 
> 

## <a name="create-segments"></a>Créer des segments
Vous pouvez créer un segment en fonction des critères de too10 sur une période spécifique des jours too60 Bonjour passé à partir de la section d’analytique hello. Par exemple, vous pouvez créer un segment basé sur les personnes hello qui disposent de certaines pages consultées ou recherché un contenu spécifique au sein de votre application dans hello des 10 derniers jours. Ces informations sont disponibles dans la section d’analytique hello. Par conséquent, vous pouvez l’utiliser toocreate un segment et puis définir un tootarget de notification push ce sous-ensemble d’utilisateurs tooget les toocome toohello arrière application. 

> [!NOTE]
> une fois un segment calculé, il ne peut pas être modifié. Il peut uniquement être cloné (copié) ou détruit (supprimé). Un segment peut être dupliqué dans hello même application (avec hello même AppID), et il peut également être dupliqué dans d’autres applications (avec un AppID différents). 

 ![segments1][35] 

## <a name="examples-segments"></a>Exemples de segments
 ![segments2][36]

Les segments permettent aux utilisateurs finaux de hello toosegment de votre application.
La segmentation de vos utilisateurs est une stratégie marketing importante. Azure Mobile Engagement vous permet de tooget les données historiques et créer des segments personnalisés. Cet outil puissant vous permet de toolearn sur l’expérience de vos clients dans votre application. Vous pouvez facilement analyser vos segments et les utiliser comme cibles de notification Push.
Un cas d’usage courant est que vous souhaitez toosend un tooencourage de notification push de vos utilisateurs finaux toorate votre application dans le magasin de hello. Au lieu d’envoyer une notification tooall vos utilisateurs finaux, vous pouvez créer un segment que vous spécifiez uniquement les utilisateurs qui hello mois dernier ont utilisé votre application de tous les jours et ont un utilisateur approprié de rencontrer. Avec des notifications Push moins nombreuses et extrêmement ciblées, vous obtenez un meilleur retour sur investissement.

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a>Vous pouvez créer des segments selon les principaux éléments de Azure Mobile Engagement hello :
* Événement : créer un segment de cet événement spécifique une cible de l’application hello qui se sont produits plus de deux fois par semaine. 
* Session : création d’un segment d’utilisateurs qui ont utilisé l’application hello plus de 5 fois la semaine dernière.
* Activité : créez un segment avec les utilisateurs ayant utilisé une page ou un contenu plus ou moins de 10 fois au cours du mois dernier.
* Tâche : créez un segment avec les utilisateurs ayant effectué une tâche plus de deux fois par jour.
* Panne : création d’un segment de tous les utilisateurs de hello qui ont eu une panne plus de 10 fois la semaine dernière. (Vous pourriez envoyer une notification Push à ce segment pour présenter des excuses ou offrir un coupon !)
* Erreur : créer un segment de tous les utilisateurs de hello qui ont eu une erreur plus de 100 fois 3 jours.
* Informations sur l’application : créer un segment qui cible un informations personnalisées sur l’application qui se sont produites au cours de hello 25 jours.
  
  ![segments4][38]

toouse Segment de façon optimale, vous devez effectuer une intégration personnalisée Hello SDK dans votre application avec un plan de marquage de balises de « Application Info ».
Ensuite, accédez toohello page d’accueil de l’interface de hello, sélectionnez l’application hello et cliquez sur la section « Segments » de hello.

1. Sélectionnez la section « Segments » de hello.
2. Cliquez sur hello « Nouveau segment » bouton toocreate un nouveau segment.

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a>Exemple en conditions réelles : créer un segment simple en fonction des informations de « Session »
Création d’un segment de tous les utilisateurs finals hello qui ont utilisé votre application au moins 50 fois Bonjour la semaine dernière. À partir de là, trouver uniquement hello aux utilisateurs finaux ont passé au moins 30 secondes dans votre application par session. Cette opération affiche tous les hello aux utilisateurs finaux une expérience positive dans votre application. Ensuite, segment hello créé peut être utilisé toopush un tooask les utilisateurs finaux de toothese notification les stocker de votre application Bonjour toorate.

 ![segments5][39]

1. Donnez un nom à votre segment dans l’ordre toofind rapidement dans la liste des « Segment » hello.
2. Cliquez sur hello le bouton « Créer ».
   
   ![segments6][40]

Sélectionnez Session.

 ![segments7][41]

1. Sélectionnez la période hello de « Dernière semaine ».
2. Cliquez sur Suivant.
   
   ![segments8][42]
3. Sélectionnez hello opérateur s’applique parmi la liste de hello : = ; ≥, ≤.
4. Entrez le nombre souhaité de hello.
5. Sélectionnez hello Occurrence souhaité. 
6. Cliquez sur Suivant.
   Cet exemple est défini afin que plus hello semaine dernière, les utilisateurs de correspondance qui ont effectué au moins 50 sessions.
   
   ![segments9][43]

Pour hello segmentation de Session, vous pouvez choisir la longueur de hello par session comme critère de.

1. Sélectionnez hello opérateur à partir de la liste de hello.
2. Fournissez hello longueur par session.
3. Cliquez sur Suivant.
   Dans cet exemple, il indique que sur toutes les hello sessions qui ont été partagées sur une section d’occurrence hello, sélectionnez uniquement hello les utilisateurs qui ont passé à plus de 30 secondes par session.
   
   ![segments10][44]

Nom de votre critère dans tooretrieve order dans hello terminer en entonnoir, puis cliquez sur Terminer.

 ![segments11][45]

Lorsque vous avez défini votre critère, il apparaît dans l’entonnoir de segment hello.
Comme un segment est basé sur les données d'analyse, les segments sont calculés une fois par jour.
Dans cet exemple, 47,7 % des utilisateurs finaux de total hello mis en correspondance le critère de hello. Ils doivent être des utilisateurs de hello qui ont une bonne expérience et s’être tooprovide susceptible d’une évaluation supérieure si vous les envoyez une notification leur demandant application hello de toorate dans le magasin de hello.

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

