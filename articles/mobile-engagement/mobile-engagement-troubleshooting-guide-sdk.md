---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: "Résolution des problèmes d’intégration du Kit de développement logiciel (SDK) dans Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>Guide de dépannage pour les problèmes d’intégration du Kit de développement logiciel (SDK)
Hello Voici les problèmes possibles, que vous pouvez rencontrer avec l’intégration de Azure Mobile Engagement dans votre application.

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>Problèmes du Kit de développement logiciel (SDK) découverts par un échec dans une autre partie de votre application
### <a name="issue"></a>Problème
* Échec de la collecte de données de l'interface utilisateur (dans Analyse, Surveillance, Segmentation ou Tableaux de bord).
* Échec push (push ne fonctionne pas dans l'application, en dehors de l'application, ou les deux).
* Échecs de composants avancés (le suivi, la géolocalisation ou les push spécifiques à une plateforme ne fonctionnent pas).
* Échecs d'API (les API échouent souvent en mode silencieux sans afficher de message d'erreur).
* Défaillances du service (aucun élément d'Azure Mobile Engagement ne fonctionne avec votre application).

### <a name="causes"></a>Causes
* La plupart des problèmes nécessitant toobe résolu par hello Azure Mobile Engagement SDK sera découvert par un échec dans votre application (par exemple, un échec de collecte des données de l’interface utilisateur, Échec de transmission, Échec de la fonctionnalité avancée, Échec de l’API, Application tombe en panne ou service apparent panne).  
* Si une fonctionnalité particulière d’Azure Mobile Engagement n’a jamais travaillé dans votre application avant, vous devez l’intégration toocomplete hello. 
* Si une fonctionnalité particulière d’Azure Mobile Engagement a été fonctionne et s’est arrêté, vous devrez peut-être tooupgrade toohello la dernière version avec hello Kit de développement logiciel Azure Mobile Engagement. N’oubliez pas qu’il existe une autre version du Kit de développement logiciel Azure Mobile Engagement de hello pour chaque plateforme prise en charge par Azure Mobile Engagement (Android, iOS, Windows et Windows Phone).

#### <a name="sdk-integration"></a>Intégration du Kit de développement logiciel (SDK)
* Azure Mobile Engagement n'est pas correctement intégré dans le Kit de développement logiciel (Analyse).
* Reach n'est pas correctement intégré dans le Kit de développement logiciel (push dans l'application et en dehors de l'application).
* Certificat expiré ou PROD et DEV incorrects (iOS uniquement).
* GCM ou ADM n'est pas correctement intégré dans le Kit de développement logiciel (Android uniquement - Push spécifique au service).
* Le suivi n'est pas correctement intégré dans le Kit de développement logiciel (installer le suivi de magasin).
* Intégration incorrecte de l'emplacement tardif ou de l'emplacement GPS dans le Kit de développement logiciel (ciblage par emplacement géographique).

**Voir aussi :**

* [Documentation du Kit de développement logiciel (SDK) - Guide d’intégration][Link 5] 
* [Guide de résolution des problèmes - Push][Link 23]

#### <a name="sdk-upgrade"></a>Mise à niveau du Kit de développement logiciel (SDK) :
* Peut-être des problèmes de tooresolve tooupgrade Kit de développement logiciel avec les versions antérieures du Kit de développement logiciel (souvent connexes toonewer versions de système d’exploitation du périphérique hello) de hello.
* Désinstallez toutes les versions précédentes de votre application à partir de votre appareil et réinstallez la version la plus récente de votre application hello, hello réinscrire votre ID d’appareil à partir de tooconfirm de l’interface utilisateur de Azure Mobile Engagement hello que votre appareil utilise la version la plus récente de votre application hello.

**Voir aussi :**

* [Documentation du Kit de développement logiciel (SDK) - Notes de publication](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [Documentation du Kit de développement logiciel - Guides de mise à niveau](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>Kit de développement logiciel (SDK), autres :
* Erreurs dans le manifeste d’Application « AndroidManifest.xml » peuvent entraîner Azure Mobile Engagement pas toowork (Android uniquement).
* Un problème courant avec l’intégration du Kit de développement logiciel et l’utilisation de l’API est tooconfuse hello clé du SDK et hello clé API.

**Voir aussi :**

* [Concepts - Glossaire][Link 6]

## <a name="advanced-coding-issues"></a>Problèmes de codage avancé
### <a name="issue"></a>Problème
* Le code de plate-forme spécifique pas directement liées tooAzure que Mobile Engagement peut entraîner des problèmes sur iOS, Android et Windows Phone.

### <a name="causes"></a>Causes
* Nombreux avancée des problèmes de codage avec Azure Mobile Engagement sont provoquées par la plateforme écrite de manière incorrecte un code spécifique pas directement liées tooAzure Mobile Engagement. Vous devez tooconsult documentation spécifique toohello plate-forme de que développement pour de plus documentation de Mobile Engagement tooAzure (Android, iOS, Web, Windows et Windows Phone).
* Configurez pas correctement les « catégories », empêche la liaison à partir d’un emplacement de tooanother de notification à l’intérieur ou en dehors de l’application hello (Android uniquement). 
* Vous ne définissez ne pas « UIKit.framework » trop « facultatif » dans votre code iOS, affiche un « Symbole introuvable » ou se bloque sur les anciens appareils iOS (iOS uniquement).
* Les certificats expirés ou n’est pas correctement à l’aide de hello développement ou la version de production du certificat de hello, push de causes émet (iOS uniquement).
* Il existe certains plate-forme limitations inhérentes tooa Azure Mobile Engagement ne peut pas contrôler (par exemple, le fonctionne de centre de système hello pour hors de l’application exécute un push dans Android et iOS).
* Azure Mobile Engagement publie une liste complète des packages de hello interne utilisé par Azure Mobile Engagement pour iOS et Android à titre de référence. Gardez à l’esprit que certaines fonctionnalités d’Azure Mobile Engagement sont plateforme toohello spécifique (Android, iOS, Web, Windows et Windows Phone).

### <a name="see-also"></a>Voir aussi
* [Guide de résolution des problèmes - Push][Link 23] 
* [Documentation du Kit de développement logiciel (SDK) - Notes de publication][Link 5]
* [Documentation du Kit de développement logiciel (SDK) - Guides de mise à niveau][Link 5]

## <a name="application-crashes"></a>Blocage de l’application
### <a name="issue"></a>Problème
* Votre application se bloque sur l’appareil des utilisateurs finaux hello.

### <a name="causes"></a>Causes
* Les informations de blocage peuvent être consultées dans hello *Analytique UI* ou hello *Analytique API*
* Vous pouvez trouver hello ID de périphérique de votre appareil de test et prendre hello même action qui a provoqué toocrash de votre application pour un utilisateur final de toohelp identifier la cause hello de votre incident.
* Problèmes connus avec hello Kit de développement logiciel Azure Mobile Engagement qui provoquent des applications toocrash sont parfois résolus en mettant à niveau de la version la plus récente du Kit de développement logiciel de hello toohello. Assurez-vous que toocheck hello notes de publication sur votre plateforme lorsque vous recherchez des pannes.

### <a name="see-also"></a>Voir aussi
* [Documentation du Kit de développement logiciel (SDK) - Notes de publication][Link 5]
* [Documentation du Kit de développement logiciel (SDK) - Guides de mise à niveau][Link 5]

## <a name="app-store-upload-failures"></a>Échecs de téléchargement App Store
### <a name="issue"></a>Problème
* Erreurs liées toouploading hello dernière version de votre application tooApple, Google ou magasin de l’application Windows hello.

### <a name="causes"></a>Causes
* Application stocke parfois bloquer des applications avec certaines fonctionnalités activées (par exemple hello Apple Store empêche utilisation hello de IDFV d’applications dans le magasin de hello et magasin de GooglePlay hello hello partage des informations entre les applications de l’application). 
* Vérifiez que les notes de publication hello sur votre plateforme et la version actuelle du Kit de développement logiciel de hello si vous avez des difficultés à télécharger un magasin d’applications toohello.

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
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

