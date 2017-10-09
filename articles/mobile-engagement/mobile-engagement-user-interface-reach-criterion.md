---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - atteindre un critère"
description: "Découvrez comment toouse ciblage critères toosend push campagnes tooa sélectionner le sous-ensemble de vos utilisateurs à l’aide d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a>Comment toouse ciblage critères toosend push campagnes tooa sélectionner le sous-ensemble de vos utilisateurs
Cibler votre audience en fonction de critères spécifique avec un bouton « Nouveau critère » hello est un des concepts plus puissantes hello dans Azure Mobile Engagement que vous aide à que vous envoyez pertinentes push notifications que les clients hello répondra tooinstead de courrier indésirable tout le monde. Vous pouvez limiter votre audience en fonction de critères standards et simuler push toodetermine nombre de personnes qui reçoivent une notification de hello.

**Voir aussi :**

* [Documentation de l’interface utilisateur - Reach - Nouvelle campagne Push][Link 27]

## <a name="audience-criteria-can-include"></a>Les critères d’audience peuvent inclure :
* ** Technicals : ** vous pouvez cibler hello en fonction des mêmes informations techniques que vous pouvez voir dans hello Analytique et les sections de l’analyse. **Voir aussi :**[Documentation de l’interface utilisateur - Analyse][Link 15], [Documentation de l’interface utilisateur - Moniteur][Link 16]
* **Emplacement :** permet aux Applications qui utilisent « signalisation de l’emplacement en temps réel » avec la délimitation géographique emplacement géographique comme un tootarget critères une audience à partir de la position de hello. Appel de « Paresseux zone emplacement Reporting » également être utilisé tootarget une audience à partir de l’emplacement de téléphone cellulaire hello (« en temps réel emplacement reporting » et « Paresseux zone emplacement Reporting » doivent être activé à partir de hello SDK). **Consultez également :**[Documentation du Kit de développement logiciel (SDK) - iOS - Intégration][Link 5], [Documentation relative au Kit de développement logiciel (SDK) - Android - Intégration][Link 5]
* **Commentaire Reach :** vous pouvez cibler votre audience selon les commentaires des précédentes notifications Reach via les commentaires Reach dans les sections Annonces, Sondages et Push de données. Cela vous permet de cible toobetter votre audience après que deux ou trois atteindre campagnes que vous pouvez hello première fois. Il peut également être utilisé toofilter les utilisateurs qui ont déjà reçu une notification avec un contenu similaire, en définissant un tooNOT campagne envoyé toousers qui ont déjà reçu une campagne précédente spécifique. Vous pouvez même exclure les utilisateurs faisant partie d’une campagne spécifique toujours active, afin qu’ils ne reçoivent pas de nouvelles notifications Push. **Consultez également :**[Documentation sur l’interface utilisateur - Reach - Contenu Push][Link 29]
* **Installation du suivi :** vous pouvez suivre des informations selon l’emplacement où les utilisateurs ont installé votre application. **Consultez également :**[Documentation sur l’interface utilisateur - Paramètres][Link 20]
* **Profil utilisateur :** vous pouvez cibler en fonction des informations d’utilisateur standard et vous pouvez cible en fonction des informations d’application personnalisée hello que vous avez créés. Cela inclut les utilisateurs qui sont actuellement connectés et les utilisateurs qui ont des questions spécifiques, vous avez demandé les tooset dans l’application hello lui-même au lieu de simplement comment ils ont répondu tooprevious campagnes ayant obtenu une réponse. Toutes les informations définies pour votre application sont indiquées dans cette liste.
* Segments : vous pouvez également cibler votre audience en fonction des segments que vous avez créés suivant le comportement spécifique des utilisateurs et contenant des critères multiples. Tous les segments définis pour votre application sont indiqués dans cette liste. **Consultez également :**[Documentation sur l’interface utilisateur - Segments][Link 18]
* **Informations sur l’application :** Custom application Info balises peuvent être créés à partir de comportement de l’utilisateur tootrack « Paramètres ». **Consultez également :**[Documentation sur l’interface utilisateur - Paramètres][Link 20]

## <a name="example"></a>Exemple :
Si vous voulez toopush un ensemble de sous-système toohello uniquement annonce de vos utilisateurs qui ont effectué dans l’application d’achat action.

1. Atteindre la page de paramètres d’application tooyour et sélectionnez le menu de « Info de l’application » hello « Nouvelle app info »
2. Enregistrez une nouvelle information booléenne relative à l'application appelée « inAppPurchase ».
3. Rendre votre application définir les informations de cette application trop « true » lorsque l’utilisateur de hello effectue avec succès un achat dans l’application (à l’aide de hello sendAppInfo (« inAppPurchase »,...) fonction)
4. Si vous ne souhaitez pas toodo cela à partir de votre application, vous pouvez le faire à partir de votre serveur principal à l’aide des API de l’appareil hello)
5. Ensuite, vous devez simplement toocreate l’annonce, avec un critère de limiter votre toousers public ayant « inAppPurchase » défini trop « true »)

> [!NOTE]
> Ciblage en fonction de critères autres que les balises d’informations sur application nécessite des informations de toogather Azure Mobile Engagement à partir d’appareils de vos utilisateurs avant de push de hello est envoyé et risque d’entraîner un retard. Les options de configuration de notifications Push complexes (telles que la mise à jour des badges) peuvent également entraîner des retards. À l’aide d’une campagne « une seule opération » à partir de l’API de Push de hello est hello absolu push méthode la plus rapide dans Azure Mobile Engagement. L’utilisation d’uniquement les balises d’informations sur application comme critère de push pour une couverture campagne (soit dans hello API couverture ou hello UI) d’est la méthode la plus rapide suivant hello, car les balises info application sont stockés côté serveur de hello. À l’aide d’autres critères de ciblage pour une campagne de push d’est hello méthode la plus souple, mais les plus lents par émission de données, car Azure Mobile Engagement dispose d’appareils de hello tooquery de campagne de commande toosend hello.

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a>Les options de critère s'appliquent à :
* **Informations techniques**     
* Nom du microprogramme : nom du microprogramme
* Version du microprogramme : version du microprogramme
* Modèle de l’appareil : modèle de l’appareil
* Fabricant de l’appareil : fabricant de l’appareil
* Version de l’application : version de l’application
* Nom de l’opérateur : nom de l’opérateur, non défini
* Pays de l’opérateur : pays de l’opérateur, non défini
* Type de réseau : type de réseau
* Paramètres régionaux : paramètres régionaux
* Taille de l’écran : taille de l’écran
* **Emplacement**      
* Dernière région connue : pays, région, localité
* Géofencing en temps réel : liste des POI (points d’intérêts) (nom, actions), POI circulaires (nom, latitude, longitude, rayon en mètres)
* **Commentaire Reach**     
* Commentaire de l’annonce : annonce, commentaire
* Commentaire du sondage : sondage, commentaire
* Commentaire de réponse du sondage : commentaire de réponse du sondage, question, choix
* Commentaire du Push de données : Push de données, commentaire
* **Installation du suivi**     
* Store : Store, non défini
* Source: source, non défini
* **Profil utilisateur**     
* Sexe : masculin ou féminin, non défini
* Date de naissance : opérateur, date, non défini
* Accepter : vrai ou faux, non défini
* **Informations sur l’application**      
* Chaîne : chaîne, non défini
* Date : opérateur, date, non défini
* Entier : opérateur, nombre, non défini
* Booléen : true ou false, non défini
* **Segment**    
* Nom des segments (de la liste déroulante), exclusion (utilisateurs cibles qui ne font pas partie de ce segment).

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

