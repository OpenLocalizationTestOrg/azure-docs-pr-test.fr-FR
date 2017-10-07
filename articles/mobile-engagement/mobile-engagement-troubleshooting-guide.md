---
title: "aaaAzure Mobile Engagement dépannage des repères"
description: "Guide de dépannage pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 31134a29-a513-4e5e-b626-f6cf6fe04769
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: dd69bfd7019907c3e1da8df590db3b5f61606173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---troubleshooting-guide"></a>Azure Mobile Engagement - Guide de dépannage
## <a name="introduction"></a>Introduction
Hello suivant le guide de dépannage vous aidera à comprendre les causes principales de certains problèmes couramment affichées et vous permettent de tootroubleshoot vous-même. 

## <a name="general"></a>Généralités
En règle générale, vous devez toujours vous assurer suivant de hello :

1. Vérifiez que vous avez parcouru toutes les étapes de hello requis pour l’intégration, comme décrit dans notre [didacticiels de mise en route](mobile-engagement-windows-store-dotnet-get-started.md)
2. Vous utilisez la version la plus récente de développement platform SDK hello hello. 
3. Tester sur un appareil réel et un émulateur, car certains problèmes sont tooemulator spécifique uniquement. 
4. que vous n’atteignez pas les limites/seuils d’Engagement Mobile qui sont mentionnés [ici](../azure-subscription-service-limits.md)
5. Si vous n’êtes pas en mesure de tooconnect toohello Mobile Engagement service principal ou voir les données ne pas chargées en continu, puis vérifiez qu’il n’y a aucun incident de service en cours en vérifiant [ici](https://azure.microsoft.com/status/)

## <a name="monitor-issues"></a>problèmes d’« Analyse »
### <a name="i-am-not-seeing-my-device-showing-up-on-hello-monitor-tab"></a>Je ne vois pas mon appareil apparaît sur l’onglet de surveillance hello
Onglet surveiller montre la plateforme Mobile Engagement de hello périphériques connectés tooyour en temps réel. Si vous procédez à un débogage sur un émulateur et un périphérique, vous devez voir au moins une session ici. Si l’application hello a été distribuée, vous verrez hello jauge reflètent les dispositifs de hello plateforme toohello connectés en temps réel de Sessions actives. 

Si vous ne voyez pas votre appareil sur l’onglet de surveillance hello, il est probablement un problème d’intégration du Kit de développement logiciel. Certaines tootroubleshoot de tootake étapes courantes sont les suivantes :

1. Assurez-vous que vous utilisez la chaîne de connexion correcte hello dans les applications mobiles hello et il est à partir de la section « clés » hello Kit de développement logiciel pas hello API section « clés ». chaîne de connexion Hello connecte à votre instance de toohello application mobile de l’application Mobile Engagement de hello dans lequel vous verrez votre appareil sur l’onglet de surveillance hello. 
2. Pour la plateforme Windows - si votre page substitue hello `OnNavigatedTo` (méthode), vérifiez les toocall que `base.OnNavigatedTo(e)`.
3. Si vous intégrez Mobile Engagement dans une application mobile existante, vous pouvez également vous assurer qu’il ne manque toutes les étapes en examinant hello avancé des étapes d’intégration [ici](mobile-engagement-windows-store-integrate-engagement.md)
4. Assurez-vous de vous envoyez au moins un/activité à l’écran en substituant page hello avec EngagementActivity selon la plateforme hello vous travaillez comme décrit dans hello [prise en main des didacticiels](mobile-engagement-windows-store-dotnet-get-started.md).

### <a name="i-am-seeing-hello-monitor-tab-showing-a-session-even-when-i-have-disconnected-or-closed-my-app-emulator"></a>J’obtiens un onglet de surveillance hello montrant une session même lorsque j’ai déconnecté ou fermé mon application / émulateur.
Si vous êtes seule plateforme de toohello connecté hello à ce stade et que vous utilisez une application de hello émulateur tooopen cela est probablement dû tooemulator quirks. En général, vous devez tooensure que vous revenez écran d’accueil du toohello sur l’émulateur hello pour hello application session toodisconnect avec succès. En outre, sur la plateforme Windows, pendant le débogage avec Visual Studio, vous devrez peut-être tooensure que dans Visual Studio, vous allez toohello **les événements du cycle de vie** barre de menus et cliquez sur **Suspend** tooreally fermer session de Hello. Voir [Didacticiel Windows](mobile-engagement-windows-store-dotnet-get-started.md) pour plus de détails. 

## <a name="analytics-issues"></a>Problèmes d’« Analyse »
### <a name="i-am-not-seeing-any-data-refreshed-data-on-analytics-tab"></a>Je ne vois pas de données/de données actualisées sur l’onglet Analyse
Les données d’analyse sont recalculées régulièrement et l’actualisation peut prendre jusqu’à 24 heures. Ces données ne sont pas extraites en temps réel et elles seront actualisées pendant cette période de 24 heures.
Assurez-vous cependant que vous envoyez au moins un écran ou activité toohello plateforme principale d’une substitution au moins une page avec `EngagementActivity` ou en appelant `SendActivity` explicitement. 

### <a name="i-am-seeing-incorrectly-captured-datetime-for-a-device-on-hello-analytics-tab"></a>J’obtiens incorrectement capturée date/heure pour un périphérique sur l’onglet d’Analytique hello
Hello laps de temps pour l’Analytique est basée sur la date hello à partir des paramètres de périphérique hello utilisateurs. Par conséquent, vérifiez que hello périphérique a date de hello correctement définie. 

## <a name="segment-issues"></a>Problèmes « Segment »
### <a name="i-created-a-segment-and-it-is-showing-up-as-greyed-out-or-not-showing-any-data"></a>J’ai créé un segment et il s’affiche en grisé, ou il n’affiche pas toutes les données
Création de segment n’est pas en temps réel au moment de hello. Il est calculé à hello en que même temps que les données analytique hello sont agrégées et par conséquent, il peut prendre jusqu'à 24 heures. Vous devez revenir plus tard, mais en attendant vous devez également vous assurer que vos applications mobiles sont en effet envoie des données de la hello sur base hello dont vous former des segments de hello. Par exemple, Si un événement dites « foo » n’est pas envoyé par n’importe quel appareil mobile, puis il ne serait pas toutes les données de segment pour un segment créé avec EventName = foo comme critère de hello. Vous devez également vérifier votre tooensure d’intégration du Kit de développement logiciel votre application mobile envoie des données de hello correctement. 

## <a name="reach-or-push-notifications-issues"></a>Problèmes de notifications Push ou « Reach »
### <a name="my-push-messages-are-not-being-delivered"></a>Mes messages Push ne sont pas remis
1. Essayez d’envoyer des notifications tooa test appareil premier tooensure que tous les composants de hello - application mobile, le service SDK et hello sont toodeliver correctement connectés et en mesure des notifications push. 
2. Toujours notifier hello la plus simple ' hors de l’application ' abord via une campagne qui n’est pas programmée et ni n’importe quel critère d’audience spécifié. C’est encore tooprove que la connectivité de notification fonctionne correctement. 
3. Si vous rencontrez des problèmes à remettre les notifications dans l’application, puis il est également une bonne première étape tootry envoi d’une notification de la sortie de l’application tout d’abord. 
4. Vérifiez que hello 'Push' Native' est correctement configuré pour votre application mobile. En fonction de la plateforme de hello qu’il soit implique clés (Android, Windows) ou des certificats (iOS). Voir [Interface utilisateur - Paramètres](mobile-engagement-user-interface-settings.md)
5. Hors de l’application notifications peut également être bloquées par hello utilisateur via hello que système d’exploitation mobile par conséquent, vérifiez que ce n’est pas le cas de hello. 
6. Assurez-vous que vous ne définissez pas hello *ignorer Audience, push seront envoyés toousers via hello API* option Bonjour **campagne** section d’une couverture de campagne, car cela permet de garantir que push notifications uniquement envoyés via des API. 
7. Assurez-vous que vous testez votre campagne push avec à la fois un appareil connecté via le Wi-Fi et téléphone opérateur réseau tooeliminate hello connexion réseau comme une source possible de problèmes.
8. Vous assurer que hello système date/heure sur votre appareil/émulateur est correct, car n’importe quel appareil synchronisé sera également interférer avec les notifications toodeliver de hello services de notifications Push capacité. 

Vous trouverez d’autres instructions de dépannage spécifiques de plateforme ci-dessous :

1. **iOS** 
   
   * Assurez-vous que les certificats de hello sont valides et non expirées pour iOS, des Notifications Push. 
   * Vérifiez que vous configurez correctement un certificat de *Production* dans votre application Mobile Engagement. 
   * Assurez-vous d’effectuer le test sur un *périphérique physique réel.* Simulateur iOS de Hello ne peut pas traiter les messages push.
   * Vérifiez que hello Qu'identificateur de lot est correctement configuré dans les applications mobiles hello. Consultez les instructions de hello [ici](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
   * Lors du test, utilisez la distribution « Ad Hoc » dans votre profil d’approvisionnement mobile. Vous ne serez pas en mesure de tooreceive notification si votre application est compilée à l’aide de « Debug »
2. **Android**
   
   * Assurez-vous que vous avez spécifié le nombre de projet hello correct dans le fichier AndroidManifest.xml de votre application mobile qui est suivi par le caractère \n. 
     
           <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
   * Vérifiez que vous ne sont pas manquant ou mal configuré des autorisations dans le fichier de manifeste Android hello 
   * Assurez-vous que le numéro de projet hello vous ajoutez tooyour client application est à partir de hello même compte où vous avez obtenu hello GCM clé du serveur. Une incompatibilité entre les hello deux empêchera votre push sortantes. 
   * Si vous recevez le système des notifications mais pas dans l’application puis passez en revue hello [spécifier une icône pour la section notifications](mobile-engagement-android-get-started.md) comme probablement que vous ne spécifiez pas les icônes corrects hello dans le fichier de manifeste Android hello. 
   * Si vous envoyez une notification BigPicture, puis de sorte que, si vous disposez de serveurs de l’image externe, puis ils ont besoin toosupport en mesure de toobe HTTP « GET » et « HEAD ».
3. **Windows**
   
   * Assurez-vous que vous avez associé application hello à une application du Windows Store valide. Dans Visual Studio - avoir tooright sur le projet hello et sélectionnez option de « Associer avec magasin d’applications » et application hello sélectionnez que vous avez créé dans hello du Windows Store. Cette application du Windows Store doit être hello même d’où vous avez obtenu tooconfigure d’informations d’identification hello push natif dans le portail Mobile Engagement de hello.
   * Si vous recevez des notifications Push hors application, mais pas dans les applications avec l’intégration `EngagementOverlay` , assurez-vous qu’il existe un élément de grille racine dans votre page. EngagementOverlay utilise le premier élément « Grille » hello, qu'il se trouve dans votre xaml fichier tooadd deux affichages web sur votre page. Si vous souhaitez toolocate où seront définies affichages web, vous pouvez définir une grille nommée « EngagementGrid » comme suit, toutefois, vous devez tooensure est suffisamment hauteur et largeur de hello suivantes deux vues qui affiche la notification de hello et hello suivant web annonce de notification dans l’application :
     
           <Grid x:Name="EngagementGrid"></Grid>

### <a name="i-created-a-push-notificationannouncement-campaign-and-even-after-it-sent-me-hello-notification-it-is-showing-as-active-what-does-it-mean"></a>J’ai créé une annonce de notification push / / de campagne et même après qu’il me hello notification envoyée, il est affiché en tant que 'Active'. Qu’est-ce que cela signifie ?
Hello **campagne** que vous avez créé dans Mobile Engagement est appelé, car il est une longue signification de notification push plateforme mobile engagement de tooyour de connexion de nouveaux périphériques, ils seront automatiquement envoyés notification de hello vous configurez ici, tant qu’ils répondent à critère hello que vous définissez de campagne de hello. Il ne s’agit pas d’une notification unique, émise une fois pour toutes. Vous devez toomanually cliquez sur hello **Terminer** bouton campagne de hello tooterminate afin qu’il n’envoie plus les notifications. 

### <a name="i-created-a-push-campaign-and-i-am-receiving-notifications-successfully-however-whenever-i-open-up-hello-app-i-get-hello-same-notification-even-when-i-had-actioned-it-before"></a>J’ai créé une campagne push et je reçois des notifications correctement toutefois chaque fois que vous ouvrez l’application hello, j’obtiens hello même notification même lorsque j’avais déclenchée avant ?
Il s’agit probablement toohappen pendant le test et si vous utilisez des émulateurs ou une infrastructure de test comme TestFlight. Que se passe-t-il ici est qu’à chaque application d’exécuter l’instance, il est l’acquisition d’un nouvel ID d’appareil et en l’envoyant principal tooour provoquent tootreat de plateforme Mobile Engagement hello en tant qu’un nouveau périphérique et l’envoi de notification de hello. 

## <a name="getting-support"></a>Obtenir une assistance
Si vous êtes vous-même problème de hello tooresolve impossible, vous pouvez :

1. Recherchez votre problème dans les threads existants hello sur StackOverflow forum et [forum MSDN](https://social.msdn.microsoft.com/Forums/windows/en-US/home?forum=azuremobileengagement) et si pas puis poser une question. 
2. Si vous trouvez une fonctionnalité manquante ajouter/vote puis pour demande de hello sur notre [UserVoice forum](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. Si vous avez ouvert de Microsoft prennent en charge un incident de support en fournissant hello les détails suivants : 
   * ID d’abonnement Azure
   * Plate-forme (par exemple, iOS, Android etc.)
   * ID d'application
   * ID de campagne (pour les problèmes de notification Push)
   * ID de périphérique
   * Version du kit de développement logiciel Mobile Engagement (par exemple, le kit de développement logiciel Android v2.1.0)
   * Détails de l’erreur avec message d’erreur exact et scénario

