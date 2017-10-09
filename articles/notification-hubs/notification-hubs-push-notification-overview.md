---
title: aaaAzure concentrateurs de Notification
description: "Découvrez comment tooadd push avec Azure Notification Hubs, les fonctionnalités de notification."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: 
ms.assetid: fcfb0ce8-0e19-4fa8-b777-6b9f9cdda178
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 1/17/2017
ms.author: yuaxu
ms.openlocfilehash: 78ce34b6b094b560c8002ab9652f7ba4563c5c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs"></a>Azure Notification Hubs
## <a name="overview"></a>Vue d’ensemble
Azure Notification Hubs offre un moteur Push facile à utiliser, multi-plateforme et mis à l’échelle. Avec un appel d’API multi-plateforme unique, vous pouvez facilement envoyer plateforme mobile de tooany de notifications push ciblés et personnalisés à partir de n’importe quel principal de cloud ou localement.

Notification Hubs est parfaitement adapté lors de scénarios d’entreprise et de clients. Voici quelques exemples de clients utilisant Notification Hubs pour :

* Envoyer avec rupture nouvelles notifications toomillions avec une faible latence.
* Envoyer des segments d’utilisateurs toointerested basée sur l’emplacement des coupons.
* Envoyer des notifications relatives aux événements toousers ou des groupes pour les applications de support/sport/finance/jeu.
* Push toocustomers tooengage et de marché du tooapps contenu publicitaire.
* informer les utilisateurs d’événements d’entreprise tels que des nouveaux messages et des éléments de travail ;
* envoyer des codes pour l’authentification MFA.

## <a name="what-are-push-notifications"></a>Présentation des notifications Push
Les notifications Push sont une forme de communication entre l’application et l’utilisateur dans laquelle les utilisateurs d’applications mobiles sont avertis de certaines informations choisies, le plus souvent via une fenêtre contextuelle ou une boîte de dialogue. Les utilisateurs peuvent généralement choisir tooview ou ignorer le message de type hello et ancienne de hello ouvrira hello des applications mobiles que vous avaient communiqué de notification de hello.

Les notifications Push sont essentielles pour les applications clients en vue d’augmenter l’engagement envers l’application et l’utilisation. Pour les applications d’entreprise, elles permettent de communiquer des informations commerciales à jour. Il est communication application à l’utilisateur de la meilleure hello, car il est faible consommation d’énergie pour les appareils mobiles, flexibles pour les expéditeurs de notifications hello et disponibles tandis que les applications correspondantes ne sont pas actifs.

Pour plus d’informations sur les notifications Push des plateformes les plus populaires, voir :
* [iOS](https://developer.apple.com/notifications/)
* [Android](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [Windows](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a>Fonctionnement des notifications Push
Les notifications Push sont diffusées par l’intermédiaire d’infrastructures spécifiques à des plateformes appelées *Platform Notification Systems* (PNS). Ils offrent des fonctionnalités de push notre appareil de tooa toodelivery message avec un gérer et n’ont aucune interface commune. une notification de toosend clients tooall entre hello iOS, Android et Windows versions d’une application, développeur de hello doive travailler avec APNS (Apple Push Notification Service), FCM (Firebase de messagerie Cloud) et WNS (Service de Notification de Windows), pendant le traitement par lot Hello envoie.

À un niveau élevé, voici comment fonctionnent les notifications Push :

1. Hello client application décide qu’il souhaite tooreceive exécute un push donc hello contacts correspondant PNS tooretrieve son handle par émission de données unique et temporaires. type de handle Hello dépend du système hello (ex. WNS a URI tandis que APNS a des jetons).
2. Hello client application stocke ce handle dans hello application principal ou le fournisseur.
3. toosend une notification push, hello application back-end contacte hello PNS à l’aide de hello handle tootarget une application cliente spécifique.
4. Hello PNS transmet un périphérique de toohello notification hello spécifié par le handle de hello.

![][0]

## <a name="hello-challenges-of-push-notifications"></a>Hello défis de Notifications Push
PNSes sont puissants, ils laissent de développeur d’applications toohello travail dans l’ordre tooimplement même push notification les scénarios courants, tels que la diffusion ou de l’envoi des notifications toosegmented les utilisateurs par émission de données.

Push est un des hello plus fonctionnalités demandées dans services mobiles cloud, car son utilisation requiert des infrastructures complexes qui sont indépendants toohello logique d’application principal de l’entreprise. Certains des problèmes d’infrastructure hello sont :

* **Dépendance de la plateforme** : 

  * Hello principal doit toohave complexe et difficile à gérer la logique dépend de la plateforme toosend notifications toodevices sur différentes plateformes comme PNSes ne sont pas unifiés.
* **Mise à l’échelle** :

  * Selon les instructions de PNS, les jetons des appareils doivent être actualisés chaque fois que l’application est lancée. Cela signifie simplement les jetons hello tookeep à jour d’accès de base de données et hello principal traite avec une grande quantité de trafic. Lorsque toohundreds et des milliers de millions a atteint le nombre de hello d’appareils, coût hello de la création et la gestion de cette infrastructure est énorme.
  * La plupart des PNSes ne gèrent pas diffusion toomultiple périphériques. Cela signifie une simple tooa de diffusion des résultats de millions d’appareils dans les appels d’un million toohello PNSes. La mise à l’échelle de cette quantité de trafic avec une latence minimale est complexe.
* **Routage** :
  
  * Que PNSes fournissent un toodevices de messages de façon toosend, la plupart des notifications d’applications sont ciblées sur les utilisateurs ou groupes d’intérêt. Cela signifie hello principal doit maintenir un périphériques tooassociate de Registre avec des groupes d’intérêt, les utilisateurs, les propriétés, etc.. Cette surcharge ajoute des coûts de maintenance et toomarket de temps d’une application toohello.

## <a name="why-use-notification-hubs"></a>Pourquoi utiliser Notification Hubs ?
Notification Hubs élimine toutes les difficultés liées à l’activation des notifications Push par vous-même. Son infrastructure de notifications Push multi-plateforme et mise à l’échelle réduit les codes Push et simplifie votre serveur principal. Avec Notification Hubs, les appareils sont simplement responsables de l’inscription de leurs handles PNS avec un concentrateur, tandis que hello principal envoie des messages toousers ou des groupes d’intérêt, comme indiqué dans la figure suivante de hello :

![][1]

Concentrateurs de notification est votre moteur de push de prêt à l’emploi avec hello suivant avantages :

* **Multi-plateforme**

  * Prise en charge de toutes les plateformes Push principales, dont iOS, Android, Windows, Kindle et Baidu.
  * Une interface toopush tooall plates-formes courantes dans des formats spécifiques à une plateforme ou indépendant de la plateforme sans aucun travail spécifique à la plateforme.
  * Gestion centralisée du handle de l’appareil.
* **Entre les serveurs principaux**
  
  * Cloud ou local
  * .NET, Node.js, Java, etc.
* **Ensemble complet de modèles de remise**:

  * *Diffusion tooone ou plusieurs plateformes*: vous pouvez diffuser instantanément les toomillions de périphériques sur plusieurs plateformes avec un seul appel d’API.
  * *Push toodevice*: vous pouvez cibler des appareils de tooindividual de notifications.
  * *Push toouser*: fonctionnalités de modèles et les balises vous aider à atteindre tous les appareils inter-plateformes d’un utilisateur.
  * *Push toosegment avec balises dynamiques*: fonctionnalité balises vous permet de segmenter les appareils et push toothem selon les besoins de tooyour, si vous envoyez tooone segment ou une expression de segments (par exemple, active et réside dans le nouvel utilisateur Seattle pas). Au lieu d’être restreint toopub-sub, vous pouvez mettre à jour n’importe où les balises de périphérique et à tout moment.
  * *Notification Push localisée* : la fonctionnalité de modèles permet d’obtenir la localisation sans affecter le code principal.
  * *En mode silencieux push*: vous pouvez permet de modèle de pousser à tirer de hello en envoyant des notifications en mode silencieux toodevices et leur déclenchement toocomplete des extractions ou des actions.
  * *Push planifié*: vous pouvez planifier toosend des notifications à tout moment.
  * *Direct push*: vous pouvez ignorer l’inscription d’appareils avec notre service et la liste de tooa de push de lot de handles du périphérique directement.
  * *Notification Push personnalisée* : les variables des notifications Push des appareils vous permettent d’envoyer des notifications Push personnalisées propres à l’appareil avec des paires clé-valeur personnalisées.
* **Télémétrie enrichie**
  
  * Télémétrie général de push, appareil, erreur et d’opération n’est disponible dans hello portail Azure et par programme.
  * Par assure le suivi de Message télémétrie chaque émission de données de votre service de tooour appel demande initiale avec succès le traitement par lot hello pousse.
  * Commentaires de système de Notification de plateforme communique les évaluations des tooassist de systèmes de Notification de plateforme dans le débogage.
* **Extensibilité** 
  
  * Envoyer toomillions messages rapide des périphériques sans partitionnement réorganisation ou de périphérique.
* **Sécurité**

  * Secret d’accès partagé ou authentification fédérée.

## <a name="integration-with-app-service-mobile-apps"></a>Intégration d’App Service Mobile Apps
toofacilitate une expérience transparente et unificateur entre les services Azure, [Application de Service Mobile Apps] a une prise en charge intégrée pour les notifications push à l’aide de concentrateurs de Notification. [Application de Service Mobile Apps] offre une plateforme de développement d’applications mobiles hautement évolutifs et disponibles pour les développeurs d’entreprise et aux intégrateurs qui fournit un riche ensemble de capacités toomobile développeurs.

Les développeurs d’applications mobiles peuvent utiliser des concentrateurs de Notification avec hello suivant du flux de travail :

1. Récupération du handle PNS de l’appareil
2. Enregistrez l’appareil avec Notification Hubs grâce à l’API d’enregistrement de Kit de développement logiciel (SDK) client Mobile Apps adapté.
   * Notez que Mobile Apps supprime tous les mots clés des inscriptions pour des raisons de sécurité. Utiliser concentrateurs de Notification à partir de votre serveur principal directement tooassociate balises avec les appareils.
3. Envoyez des notifications de votre serveur principal d’application avec Notification Hubs

Voici quelques avantages mis toodevelopers avec cette intégration :

* **Kits de développement Client mobile Apps**: ces kits de développement logiciel multi-plateformes fournissent une API simple pour l’inscription et communiquer avec le hub de notification toohello lié aux applications mobiles de hello automatiquement. Les développeurs ne doivent toodig via les informations d’identification de concentrateurs de Notification et travailler avec un service supplémentaire.

  * *Push toouser*: kits de développement logiciel hello automatiquement la balise hello donné d’appareil Mobile Apps authentifié pseudo tooenable push toouser scénario.
  * *Push toodevice*: hello kits de développement logiciel automatiquement servir hello ID d’Installation Mobile Apps tooregister GUID avec Notification Hubs, évite aux développeurs des difficultés à hello de maintenir plusieurs GUID de service.
* **Modèle d’installation**: applications mobiles fonctionne avec dernière push modèle toorepresent des concentrateurs de Notification tous les push des propriétés associées à un périphérique dans une Installation de JSON qui s’aligne avec les Services de Notification Push et est toouse facile.
* **Flexibilité**: les développeurs peuvent choisir toujours toowork avec Notification Hubs directement même avec l’intégration de hello en place.
* **Expérience dans intégrée [portail Azure]**: Push comme une fonctionnalité est représentée visuellement dans les applications mobiles et les développeurs peuvent facilement travailler avec le hub de notification associé hello via des applications mobiles.

## <a name="next-steps"></a>Étapes suivantes
Vous trouverez d’autres informations sur Notification Hubs dans les rubriques suivantes :

* **[Comment les clients utilisent Notification Hubs]**
* **[Didacticiels et guides sur Notification Hubs]**
* **Didacticiels de prise en main de Notification Hubs** : [iOS], [Android], [Windows Universel], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
[Comment les clients utilisent Notification Hubs]: http://azure.microsoft.com/services/notification-hubs
[Didacticiels et guides sur Notification Hubs]: http://azure.microsoft.com/documentation/services/notification-hubs
[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started
[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started
[Windows Universel]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started
[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started
[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started
[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started
[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
[Application de Service Mobile Apps]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/
[templates]: notification-hubs-templates-cross-platform-push-messages.md
[portail Azure]: https://portal.azure.com
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
