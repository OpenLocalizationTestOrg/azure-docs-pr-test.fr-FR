---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - atteindre How To"
description: "Présentation de l'interface utilisateur d'Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>Comment tooget utilisation et gestion pousse tooreach des utilisateurs finaux de tooyour
Une fois que hello SDK est entièrement intégré à votre application, vous pouvez commencer à l’aide de la section de portée hello hello de hello UI tooPush notifications toohello les utilisateurs de votre application.  

## <a name="do-your-first-push-notification-campaign"></a>Lancer votre première campagne de notification push
* Vérifiez que votre portée est intégrée dans votre application avec le Kit de développement logiciel de hello. 
* Sélectionnez votre application

![Premier 1][1]

* Accédez toohello Section de « Portée » et cliquez sur « nouvelle annonce »

![Premier 2][2]

* Créez une campagne et donnez-lui un nom
  
![Premier 3][3]

* Sélectionnez le mode de remise des notifications de hello, comme dans l’application uniquement

![Premier 4][4]

* Créer le message de type hello souhaité toopush

![Premier 5][5]

* Vous pouvez écrire un titre sur la notification de hello (facultatif).
* Écrivez le contenu du message push.
* Vous pouvez télécharger une image. N’oubliez pas que taille hello du fichier de hello ne peut pas dépasser 32 768 octets.
* Vous avez également hello capacité tooselect plus d’options, mais de focus hello de ce didacticiel, nous verrons que plus tard.
* Sélectionnez le type de contenu hello en tant que Notification uniquement

![Premier 6][6]

* Créez votre campagne push. Elle apparaîtra dans votre liste de campagnes.

![Premier 7][7]

## <a name="test-your-push-notification-campaign"></a>Tester votre campagne de notification push
![Test 1][8]

* Enregistrez votre appareil.
* Cliquez sur la case à cocher hello du périphérique de hello souhaité toopush.
* Cliquez sur hello le périphérique toohello de « Test » bouton toosend hello par émission de données.

![Test 2][9]

* Activer hello campagne

![Test 3][10]

* Maintenant que vous avez créé votre campagne vous devez simplement tooactivate pour hello notification toobe envoyées tooyour utilisateurs.

## <a name="send-personalized-pushes"></a>Envoyer des notifications push personnalisées
* Cet exemple crée un push où un code de remise personnalisée est entré dans la notification d’émission hello.

![Personnalisé 1][11]

Fonctionnement de la personnalisation en remplaçant un marqueur par une application d’info par conséquent, vous aurez toomake qu’utilisateur de hello a hello approprié-informations sur l’application d’abord définis. Dans cette hello exemple utilisateurs ciblés aura une balise d’informations application nommée rebate_code définie.
Comme ci-dessus, consultez le contenu de notification push hello inclut hello marqueur ${rebate_code} qui indique qu’il s’agit de toobe remplacé par le contenu réel de hello de balise d’info application hello.

> [!WARNING]
> Si l’étiquette d’info hello application n’est pas défini pour l’utilisateur de hello, utilisateur de hello ne recevra pas de push de hello.

* Résultat

![Personnalisé 2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>Vous pouvez personnaliser encore plus texte hello votre notification
![Personnalisé 3][13]

* Y compris le titre hello de notification de hello,
* Et le contenu du message de type hello hello.
* Choisissez le type hello d’annonce (affichage du texte ou Web)

![Personnalisé 4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>corps Hello d’une annonce peut également être personnalisée avec :
* URL d’action Hello, si vous souhaitez que hello toocustomize page d’accueil
* titre de Hello,
* corps de Hello du message de type hello.

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>Différencier votre notification push (dans ou en dehors de l'application)
* Choisissez le type hello de notification push, sélectionnez votre application, accédez toohello « Portée » section, sélectionner ou créer une campagne de push et atteindre la section « Notification » de toohello.
* Cliquez sur hello « mode de livraison » que vous souhaitez.
* Cliquez sur la case à cocher « Activités restreindre » lorsque vous souhaitez que la notification de hello se produit sur des activités spécifiques (écrans) de hello.

![Différentiation 1][15]

### <a name="out-of-app-only-delivery-mode"></a>Mode de remise « Hors de l'application uniquement »
![Différentiation 2][16]

« Hors de l’application » mode de livraison fournit des notifications push lors de l’application hello est fermée. Il s’agit de hello standard de notifications push.
Lorsque vous sélectionnez « hors de l’application », vous devez avoir déjà fourni certificats hello à partir de la plateforme de hello spécialisée (APN ou GCM) dans votre application.

### <a name="see-also"></a>Voir aussi
* [Service de notification Push d’Apple – Certificats](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging – Certificat](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>Mode de remise « Dans l'application uniquement »
![Différentiation 3][17]

Mode de livraison « Dans l’application uniquement » fournit des notifications push lors de l’application hello est en cours d’exécution.
Pour cette notification, il est inutile toogo via hello APN et système GCM.
Vous pouvez utiliser tooreach de système de messagerie dans l’application hello vos utilisateurs finaux.
Vous pouvez entièrement personnaliser hello notification et décider dans quelle activité (écran) une notification de hello s’affichera.

### <a name="anytime-delivery-mode"></a>Mode de remise « À tout moment »
Vous pouvez choisir un mode de livraison « À tout moment », vous garantit tooreach votre utilisateur final hello si application est en cours d’exécution ou non.
Lorsque vous sélectionnez « Achat », vous devez avoir déjà fourni certificats hello à partir de la plateforme de hello la création de votre application (APN ou GCM). 

## <a name="schedule-a-push-campaign"></a>Planifier une campagne push
### <a name="plan-toostart-a-campaign"></a>Planifier une campagne de tooStart
![Planification 1][18]

Il est hello 21 mars et vous disposez d’une annonce toomake et planifié pour hello 22 du mois de mars, à minuit. Vous n’avez pas toostay devant hello interface toodo un push ! Vous pouvez planifier à l’avance hello exacte minute notifications seront envoyées.

* Décochez la case hello « None » case à cocher et sélectionnez une heure de début 
* Choisissez la date de hello et l’heure hello campagne de push toostart hello.

### <a name="plan-tooend-a-campaign"></a>Planifier une campagne de tooend
![Planification 2][19]

Vous souhaitez que votre toostop campagne sur hello 25 du mois de mars à 15 h 00, mais vous savez que vous ne serez plus toodo il.
Vous n’avez pas toostay devant hello interface toopush ! Vous pouvez planifier à l’avance hello exacte minute que votre campagne s’arrêtera.

* Cliquez sur hello, « None » case à cocher ou sélectionnez une heure de fin
* Choisissez la date de hello et l’heure hello campagne de push toofinish hello.

### <a name="end-a-campaign-manually"></a>Arrêter manuellement une campagne
![Planification 3][20]

Par défaut, hello « None »-cases sont cochées.
Cela signifie que la campagne de hello démarre dès que vous l’activez Bonjour atteindre la section et de fin lorsque vous l’arrêtez sur hello atteindra section.

> [!NOTE]
> Les campagnes créées sans une date de fin stockent hello push localement sur l’appareil de hello et les affichent hello prochaine application hello est ouvert, même si la campagne de hello terminée manuellement.

## <a name="enhance-a-push-notification-with-a-text-view"></a>Renforcer une notification push avec une vue de texte
### <a name="what-is-a-text-view"></a>Qu'est-ce que la vue de texte ?
![Vue de texte 1][21]

Une vue de texte est une fenêtre contextuelle contenant du texte. Cette fenêtre contextuelle apparaît une fois que l’utilisateur final hello a cliqué sur la notification d’émission hello.
Une vue de texte vous permet de toopresent par l’utilisateur de tooyour plus de contenu. Il s’agit également hello opportunité toopresent une tooaction appel telles que le moment du saut de page tooa de votre application, en redirigeant tooa ouverture de magasin, une page web, envoyer un message électronique, à partir d’un GÉOLOCALISÉS de recherche, un etc....

### <a name="example-text-view"></a>Exemple : vue de texte
* Créer votre campagne de notification Push dans la section de « Atteindre » hello et donnez un nom à votre campagne

![Vue de texte 2][22]

* Écrire le message de type hello qui s’affiche lors de la notification de hello.
* Sélectionnez hello annonce les Type de contenu de « texte »

![Vue de texte 3][23]

> [!NOTE]
> Quand vous envoyez une vue de texte, elle est toujours précédée d’une notification. 

* Définir le texte hello (après avoir sélectionné texte annonce hello, sous-section hello s’affiche, ce qui vous toodefine hello texte toobe affiché.)

![Vue de texte 4][24]

* Écrire hello titre qui s’affiche en haut de hello du message de type hello.
* Écriture du contenu principal de hello de vue de texte hello.
* Écriture du contenu de hello qui apparaîtra sur le bouton d’action hello (un bouton d’action permet de hello application toomake une action spécifique telle que l’ouverture d’une page de l’application hello, redirection tooan App store ou tout type de sources, que vous pouvez fournir).
* Contenu hello écriture qui apparaîtra sur le bouton de sortie hello (en cliquant sur le bouton de sortie hello, affichage de texte hello disparaît.)
* Créer votre campagne de notification push et elle apparaîtra dans la liste des campagnes hello.

![Vue de texte 5][25]

* Activez vos utilisateurs push notification campagne toosend hello texte vue tooyour.

![Vue de texte 6][26]

* Résultat

![Vue de texte 7][27]

* Hello utilisateur reçoit une notification de hello, puis cliquez dessus.
* affichage de texte Hello apparaît comme un toointeract utilisateur hello autoriser publicitaires avec lui.

## <a name="enhance-a-push-notification-with-a-web-view"></a>Renforcer une notification push avec une vue web
### <a name="what-is-a-web-view"></a>Qu'est-ce qu'une vue web ?
![Vue web 1][28]

Une vue web est une fenêtre contextuelle avec du contenu web. Cette fenêtre contextuelle s’affiche lorsque l’utilisateur final hello a cliqué sur la notification d’émission hello.
Un affichage web vous permet de toohave plus d’interaction avec l’utilisateur final hello.
Il s’agit également hello opportunité toopresent une tooaction appel telles que la redirection tooApp magasin, ouverture d’une page web, envoyer un message électronique, à partir d’un GÉOLOCALISÉS de recherche, un etc....

### <a name="example-web-view"></a>Exemple : vue web
* Créer votre campagne Push dans la section de « Atteindre » hello et donnez un nom à votre campagne.

![Vue web 2][29]

* Écrire le message de type hello qui s’affiche lors de la notification de hello.
* Sélectionnez hello annonce le Type de contenu en tant que « web »

![Vue web 3][30]

### <a name="about-announcement-types"></a>À propos des types d'annonce :
* Notification uniquement : il s’agit d’une simple notification standard. Ce qui signifie que si un utilisateur clique dessus, aucun affichage supplémentaire ne s’affiche, mais seulement l’action hello associée tooit se produira.
* Annonce de texte : il est une notification qui engage hello utilisateur toohave examiner une vue de texte.
* Annonce de Web : il est une notification qui engage hello utilisateur toohave examiner un affichage web.
  Sélectionnez hello contenu de « Annonce Web ».

> [!NOTE]
> quand vous envoyez une vue web, elle est toujours précédée d'une notification.

* Définir le contenu web hello (après avoir sélectionné un contenu hello web annonce, sous-section de hello s’affiche, ce qui vous toodefine hello afficher le contenu web souhaitée toobe affiché.)

![Vue web 4][31]

* Écrire hello titre qui s’affiche en haut de hello du message de type hello (facultatif).
* Écrivez ici votre code HTML.
* Cliquez sur l’édition de tooswitch de bouton de mode d’édition de la source hello et voir comment il ressemble.
* Écriture du contenu de hello qui apparaîtra sur le bouton d’action hello (un bouton d’action permet de hello application toomake une action spécifique telle que l’ouverture d’une page de l’application hello, redirection tooa magasin ou tous les types de sources, que vous pouvez fournir).
* Contenu hello écriture qui apparaîtra sur le bouton de sortie hello (en cliquant sur le bouton de sortie hello, l’affichage web hello disparaît).
* Résultat

![Vue web 5][32]

* utilisateur de Hello recevoir une notification de hello et cliquez dessus.
* affichage de texte Hello apparaît comme un toointeract utilisateur hello autoriser publicitaires avec lui.

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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

