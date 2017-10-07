---
title: "Azure Notification Hubs : Forum aux Questions (FAQ) | Microsoft Docs"
description: "FAQ sur la conception et l'implémentation de solutions sur Notification Hubs"
services: notification-hubs
documentationcenter: mobile
author: ysxu
manager: erikre
keywords: notification push, notifications push, notifications push iOS, notifications push android, push ios, push android
editor: 
ms.assetid: 7b385713-ef3b-4f01-8b1f-ffe3690bbd40
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 01/19/2017
ms.author: yuaxu
ms.openlocfilehash: a70efa7fc5954966847d5a173e9b10accf4b737e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="push-notifications-with-azure-notification-hubs-frequently-asked-questions"></a>Notifications Push avec Azure Notification Hubs : Forum aux Questions
## <a name="general"></a>Généralités
### <a name="what-is-hello-resource-structure-of-notification-hubs"></a>Quelle est la structure des ressources hello de concentrateurs de Notification ?

Azure Notification Hubs a deux niveaux de ressources : les concentrateurs et les espaces de noms. Un concentrateur est une ressource unique par envoi de données qui peut contenir des informations d’inter-plateformes push hello d’une application. Un espace de noms est une collection de concentrateurs dans une région.

Le mappage recommandé consiste à mettre en correspondance un espace de noms et une application. Dans un espace de noms, vous pouvez avoir un concentrateur de production qui fonctionne avec votre application de production, un concentrateur de test qui fonctionne avec votre application de test, etc.

### <a name="what-is-hello-price-model-for-notification-hubs"></a>Qu’est le modèle de prix hello pour les concentrateurs de Notification ?
Hello dernière tarification se trouvent sur hello [tarification des Hubs de Notification] page. Concentrateurs de notification est facturée au niveau d’espace de noms hello. (Pour la définition d’un espace de noms de hello, consultez « Nouveautés structure des ressources hello de concentrateurs de Notification ») Concentrateurs de notification propose trois niveaux :

* **Gratuit** : ce niveau est un bon point de départ pour explorer les fonctionnalités Push. Il n’est pas recommandé pour les applications de production. Vous obtenez 500 appareils et 1 million de notifications Push inclus par espace de noms par mois, sans garantie de contrat de niveau de service.
* **Base**: ce niveau (ou hello Standard) est recommandé pour les applications de production plus petites. Vous obtenez 200 000 appareils et 10 millions de notifications Push inclus par espace de noms par mois comme point de départ. Les options d’augmentation de quota sont incluses.
* **Standard**: ce niveau est recommandé pour les applications de production toolarge moyennes. Vous obtenez 10 millions d’appareils et 10 millions de notifications Push inclus par espace de noms par mois comme point de départ. Les options d’augmentation de quota et les fonctionnalités de télémétrie enrichies sont incluses.

Fonctionnalités du niveau standard :
* **Télémétrie élaborée**: vous pouvez utiliser des concentrateurs de Notification par Message télémétrie tootrack un push des demandes et les commentaires de système de Notification de plateforme pour le débogage.
* **Architecture mutualisée** : vous pouvez travailler avec les informations d’identification PNS (Platform Notification System) au niveau de l’espace de noms. Cette option permet de vous tooeasily fractionner des locataires en concentrateurs dans hello même espace de noms.
* **Push planifié**: vous pouvez planifier toobe notifications envoyée à tout moment.

### <a name="what-is-hello-notification-hubs-sla"></a>Nouveautés hello SLA de concentrateurs de Notification
Pour les niveaux de base et les concentrateurs de Notification Standard, les applications correctement configurées peuvent envoyer des notifications push ou effectuer des opérations de gestion de l’inscription au moins 99,9 % du temps de hello. toolearn plus d’informations sur les SLA hello, accédez toohello [SLA de concentrateurs de Notification](https://azure.microsoft.com/support/legal/sla/notification-hubs/) page.

> [!NOTE]
> Notifications push dépend des systèmes de Notification de plateforme de tiers (par exemple, APNS d’Apple et Google FCM), il n’existe aucune garantie du contrat SLA pour la remise de ces messages hello. Une fois les concentrateurs de Notification envoie des lots de hello tooPlatform des systèmes de Notification (SLA garanti), il est exécute un push de responsabilité hello Hello de toodeliver de systèmes de Notification de plateforme hello (aucun contrat SLA garanti).

### <a name="which-customers-are-using-notification-hubs"></a>Quels sont vos clients du service Notification Hubs ?
De nombreux clients utilisent Notification Hubs. Parmi les plus importants figurent les suivants :

* Sochi 2014 : Des centaines de groupes d’intérêt, plus de 3 millions d’appareils et plus de 150 millions de notifications distribuées en deux semaines. [Étude de cas : Sochi]
* Skanska : [Étude de cas : Skanska]
* Seattle Times : [Étude de cas : Seattle Times]
* Mural.ly : [Étude de cas : Mural.ly]
* 7Digital : [Étude de cas : 7Digital]
* Applications Bing : des dizaines de millions d’appareils envoient trois millions de notifications par jour.

### <a name="how-do-i-upgrade-or-downgrade-my-hub-or-namespace-tooa-different-tier"></a>Comment mettre à niveau ou mettre à niveau mon espace de noms ou le hub tooa autre niveau ?
Accédez toohello  **[portail Azure]** > **espaces de noms de concentrateurs de Notification** ou **concentrateurs de Notification**. Sélectionnez souhaité tooupdate, accédez à trop de ressources hello**niveau tarifaire**. Notez hello suivant les exigences :

* Hello niveau tarifaire mis à jour s’applique également*tous les* hubs dans l’espace de noms hello avec lequel vous travaillez.
* Si votre nombre de périphérique dépasse la limite hello du niveau hello vers que vous êtes mise à niveau, vous devez les appareils toodelete avant à la rétrogradation.


## <a name="design-and-development"></a>Conception et développement
### <a name="which-server-side-platforms-do-you-support"></a>Quelles plateformes côté service prenez-vous en charge ?
Des kits de développement logiciel (SDK) sur serveur pour .NET, Java, Node.js, PHP et Python sont disponibles. En outre, les API de Notification Hubs reposent sur les interfaces REST. Vous pouvez donc choisir de travailler directement avec les API REST si vous utilisez différentes plateformes ou si vous ne souhaitez pas de dépendance supplémentaire. Pour plus d’informations, consultez toohello [API REST de concentrateurs de Notification] page.

### <a name="which-client-platforms-do-you-support"></a>Quelles plateformes clientes prenez-vous en charge ?
Les notifications Push sont prises en charge pour [iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md), [Android](notification-hubs-android-push-notification-google-gcm-get-started.md), [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), [Windows Phone](notification-hubs-windows-mobile-push-notifications-mpns.md), [Kindle](notification-hubs-kindle-amazon-adm-push-notification.md), [Android China (par Baidu)](notification-hubs-baidu-china-android-notifications-get-started.md), Xamarin ([iOS](xamarin-notification-hubs-ios-push-notification-apns-get-started.md) et[Android](xamarin-notification-hubs-push-notifications-android-gcm.md)), [Chrome Apps](notification-hubs-chrome-push-notifications-get-started.md) et [Safari](https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSafari). Pour plus d’informations, consultez toohello [Notification Hubs prise en main des didacticiels] page.

### <a name="do-you-support-text-message-email-or-web-notifications"></a>Prenez-vous en charge les SMS, les emails ou les notifications web ?
Concentrateurs de notification est principalement des applications conçues toosend notifications toomobile. Il ne propose pas de fonctionnalités de courrier électronique ou de SMS. Toutefois, les plateformes tierces qui fournissent ces fonctionnalités peuvent être intégrés à des notifications push natif de toosend de concentrateurs de Notification à l’aide de [Mobile Apps].

Concentrateurs de notification n’assure pas un service de remise de notification par émission de données dans un navigateur prédéfinies hello. Les clients peuvent implémenter cette fonctionnalité à l’aide de SignalR sur les plateformes de côté serveur hello pris en charge. Si vous souhaitez que les applications toobrowser toosend notifications dans le bac à sable de hello Chrome, consultez hello [didacticiel de Chrome applications].

### <a name="how-are-mobile-apps-and-azure-notification-hubs-related-and-when-do-i-use-them"></a>Dans quelle mesure les applications mobiles et Azure Notification Hubs sont liées et quand les utiliser ?
Si vous disposez d’un mobile application précédent se terminer et vous souhaitez tooadd uniquement hello capacité toosend des notifications push, vous pouvez utiliser Azure Notification Hubs. Si vous souhaitez tooset de votre application mobile back-end à partir de zéro, envisagez d’utiliser la fonctionnalité des applications mobiles hello du Service d’applications Azure. Une application mobile configure automatiquement un concentrateur de notification afin que vous pouvez aisément envoyer des notifications push à partir de hello application mobile back-end. Tarification pour les applications mobiles inclut des frais de base hello pour un concentrateur de notification. Vous payez uniquement lorsque vous dépassez hello inclus exécute un push. Pour plus d’informations sur les coûts, accédez à toohello [tarification de Service application] page.

### <a name="how-many-devices-can-i-support-if-i-send-push-notifications-via-notification-hubs"></a>Combien d’appareils puis-je prendre en charge si j’envoie des notifications Push via Notification Hubs ?
Consultez toohello [tarification des Hubs de Notification] page pour plus d’informations sur le nombre de hello d’appareils pris en charge.

Si vous devez prendre en charge plus de 10 millions d’appareils inscrits, veuillez [nous contacter](https://azure.microsoft.com/overview/contact-us/) directement afin que nous vous aidions à mettre à l’échelle votre solution.

### <a name="how-many-push-notifications-can-i-send-out"></a>Combien de notifications Push puis-je envoyer ?
Selon le niveau sélectionné de hello, Azure Notification Hubs automatiquement augmente en fonction de nombre de hello de notifications transitant via le système de hello.

> [!NOTE]
> Hello coût d’utilisation peut augmenter en fonction de nombre hello de notifications push a été fournie. Assurez-vous que vous êtes conscient des limites de niveau hello présentées sur hello [tarification des Hubs de Notification] page.
> 
> 

Nos clients utilisent Notification Hubs toosend des millions de notifications push quotidiennement. Vous n’avez pas toodo rien de spécial tooscale hello atteindre de vos notifications push, que vous utilisez Azure Notification Hubs.

### <a name="how-long-does-it-take-for-sent-push-notifications-tooreach-my-device"></a>Combien de temps take pour envoyé tooreach de notifications push mon appareil ?
Dans un scénario d’utilisation normale, où la charge entrante de hello est cohérent et même, Azure Notification Hubs peut traiter au moins *1 million de notifications push envoie une minute*. Ce taux peut-être varier selon le nombre de hello de balises, nature hello d’envois d’entrants hello et d’autres facteurs externes.

Au cours de l’heure de remise hello estimé, service de hello calcule les cibles de hello par la plateforme et achemine toohello de messages du Service de Notification Push (PNS) en fonction de hello inscrit balises ou des expressions de balises. Il incombe hello du périphérique de toohello hello PNS toosend des notifications.

Hello PNS ne garantit pas que n’importe quel contrat SLA de livraison des notifications. Toutefois, la plupart des notifications push sont remises tootarget périphériques quelques minutes (en général pendant les 10 minutes) à partir de l’heure hello que leur envoi tooNotification concentrateurs. Certaines notifications peuvent prendre plus de temps.

> [!NOTE]
> Azure Notification Hubs utilise une stratégie en place toodrop de notifications push qui ne sont pas remises toohello PNS dans les 30 minutes. Ce délai peut se produire pour de nombreuses raisons, mais la plupart des couramment car hello PNS limite votre application.
> 
> 

### <a name="is-there-any-latency-guarantee"></a>Y a-t-il une garantie de latence ?
En raison de hello de notifications push (ils sont remis par une solution externe, spécifique à la plateforme), il n’existe aucune garantie de latence. En règle générale, la majorité hello de notifications push sont remis dans quelques minutes.

### <a name="what-do-i-need-tooconsider-when-designing-a-solution-with-namespaces-and-notification-hubs"></a>Comment dois-je tooconsider lors de la conception d’une solution avec les espaces de noms et de notification hubs ?
#### <a name="mobile-appenvironment"></a>Application mobile/Environnement
* Utilisez un hub de notification par application mobile et par environnement.
* Dans un scénario d’architecture mutualisée, chaque locataire doit disposer d’un concentrateur distinct.
* Jamais partage hello même concentrateur de notification pour les environnements de production et de test. Cela peut entraîner des problèmes lors de l’envoi de notifications. Apple fournit des points de terminaison Push pour les environnements de bac à sable (sandbox) et de production, chaque environnement étant défini avec des informations d’identification distinctes.
* Par défaut, vous pouvez envoyer des notifications test tooyour inscrit des appareils via hello portail Azure ou hello Azure composant intégré dans Visual Studio. seuil de Hello a la valeur too10 les périphériques qui sont sélectionnées de manière aléatoire à partir du pool de l’inscription de hello.

> [!NOTE]
> Si votre concentrateur a été initialement configurée avec un certificat de bac à sable Apple et puis a été reconfiguré toouse à un certificat de production d’Apple, les jetons d’appareil hello d’origine ne sont pas valides. Jetons non valides provoquent push toofail. Séparez vos environnements de test et de production et utilisez des hubs différents pour chaque environnement.
> 
> 

#### <a name="pns-credentials"></a>Informations d’identification du PNS
Lorsqu’une application mobile est inscrite via un portail des développeurs de plate-forme (par exemple, Apple ou Google), un identificateur d’application et des jetons de sécurité sont envoyés. Hello application back-end fournit ces PNS jetons toohello plateforme toodevices peuvent être envoyées à des notifications push. Les jetons de sécurité peuvent être sous forme de hello de certificats (par exemple, Apple iOS ou Windows Phone) ou des clés de sécurité (par exemple, Google Android ou Windows). Ils doivent être configurés dans hubs de notification. La configuration est généralement effectuée au niveau du concentrateur de notification hello, mais elle peut également être effectuée au niveau d’espace de noms hello dans un scénario d’architecture mutualisé.

#### <a name="namespaces"></a>Espaces de noms
Des espaces de noms peuvent être utilisés dans le cadre du regroupement de déploiement. Ils peuvent également être utilisé toorepresent tous les concentrateurs de notification pour tous les clients de hello même application dans un scénario d’architecture mutualisée.

#### <a name="geo-distribution"></a>Géo-distribution
La géo-distribution n’est pas toujours indispensable dans les scénarios de notification Push. PNSes différents (par exemple, APNS ou GCM) qui fournissent des toodevices de notifications push ne sont pas distribuées uniformément.

Si vous avez une application qui est utilisée de manière globale, vous pouvez créer des hubs dans différents espaces de noms à l’aide du service de Notification Hubs hello dans différentes régions Azure monde hello.

> [!NOTE]
> Cette disposition est déconseillée car elle augmente le coût de gestion, en particulier pour les inscriptions. Elle doit être utilisée uniquement en cas de besoin.
> 
> 

### <a name="should-i-do-registrations-from-hello-app-back-end-or-directly-through-client-devices"></a>Faire des enregistrements à partir de hello application back-end ou directement via le client appareils ?
Les enregistrements de hello application back-end sont utiles lorsque vous avez des clients de tooauthenticate avant de créer l’enregistrement de hello. Ils sont également utiles lorsque vous avez des balises qui doivent être créés ou modifiés par hello application back-end basée sur la logique d’application. Pour plus d’informations, consultez toohello [Guide d’inscription principale] et [Guide d’inscription principale 2] pages.

### <a name="what-is-hello-push-notification-delivery-security-model"></a>Qu’est le modèle de sécurité de remise hello push notification ?
Azure Notification Hubs utilise un modèle de sécurité basé sur une [signature d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md). Vous pouvez utiliser des jetons de signature d’accès hello partagé au niveau d’espace de noms racine hello ou au niveau de concentrateur de notification granulaire hello. Jetons de signature d’accès partagé peuvent être ensemble toofollow d’autorisation différentes règles, par exemple, les autorisations sur les messages toosend ou toolisten pour les autorisations de notification. Pour plus d’informations, consultez hello [modèle de sécurité de concentrateurs de Notification] document.

### <a name="how-should-i-handle-sensitive-payload-in-push-notifications"></a>Comment gérer une charge utile sensible dans des notifications Push ?
Toutes les notifications sont remises tootarget périphériques à PNS la plate-forme hello. Lorsqu’une notification est envoyée tooAzure Notification Hubs, il est traité et passé toohello PNS respectifs.

Toutes les connexions à partir de hello expéditeur toohello Azure Notification Hubs toohello PNS, utilisent le protocole HTTPS.

> [!NOTE]
> Azure Notification Hubs n’enregistre pas la charge utile de hello de messages en aucune façon.
> 
> 

toosend de charges utiles sensibles, nous vous recommandons d’utilisation d’un modèle Secure Push. expéditeur de Hello remet une notification de test ping avec un périphérique de toohello message identificateur sans la charge utile de sensibles hello. Lors de l’application hello sur l’appareil de hello reçoit la charge utile de hello, application hello appelle une API sécurisée directement toofetch hello détails du message. Pour obtenir un guide sur la façon dont les tooimplement ce modèle, accédez à toohello [didacticiel de Notification Hubs Secure Push] page.

## <a name="operations"></a>Opérations
### <a name="what-support-is-provided-for-disaster-recovery"></a>Quelle prise en charge est fournie pour la récupération d’urgence ?
Nous fournirons la couverture de récupération d’urgence de métadonnées de notre côté (nom de concentrateurs de Notification hello, chaîne de connexion hello et autres informations critiques). Lorsqu’un scénario de récupération d’urgence est déclenché, les données d’inscription sont hello *segment uniquement* de l’infrastructure de Notification Hubs hello est perdue. Vous devez tooimplement une toorepopulate solution ces données dans votre nouvelle postérieures à la récupération hub :

1. Créez un hub de notification secondaire dans un autre centre de données. Nous vous recommandons de créer un à partir de hello début tooshield vous à partir d’un événement de récupération d’urgence qui peut-être affecter vos fonctionnalités de gestion. Vous pouvez également créer un lors de reprise après sinistre hello hello.

2. Remplir le hub de notification secondaire hello avec des enregistrements à partir de votre concentrateur de notification principal hello. Nous ne vous recommandons de la tentative d’inscriptions toomaintain sur les deux concentrateurs et restent synchronisés qu’interviennent les inscriptions. Cette pratique ne fonctionne pas correctement en raison de la tendance inhérente hello d’inscriptions tooexpire sur hello côté de la solution. Les inscriptions sont supprimées de Notification Hubs lorsque le PNS nous signale qu’elles ont expiré ou qu’elles ne sont plus valides.  

Nous avons deux recommandations pour le serveur principal d’applications :

* Utilisez un serveur principal d’applications qui gère un ensemble donné d’inscriptions de son côté. Il peut ensuite effectuer une insertion en bloc à un concentrateur de notification secondaire hello.

* Utilisez une application back-end qui obtient un vidage régulière des enregistrements à partir du hub de notification principal hello en tant que sauvegarde. Il peut ensuite effectuer une insertion en bloc à un concentrateur de notification secondaire hello.

> [!NOTE]
> Fonctionnalité d’exportation/importation inscriptions disponible dans le niveau Standard de hello est décrite hello [inscriptions exportation/importation] document.
> 
> 

Si vous n’avez pas un serveur principal, au démarrage de l’application hello sur appareils cibles, ils effectuent une nouvelle inscription dans le hub de notification secondaire hello. Finalement hello hub de notification secondaire aura tous les périphériques actifs hello inscrit.

Pendant une certaine période, les appareils sur lesquels aucune application n’est ouverte ne reçoivent pas de notifications.

### <a name="is-there-audit-log-capability"></a>Existe-t-il une fonctionnalité de journal d’audit ?
Toutes les opérations de gestion de concentrateurs de Notification accédez toooperation journaux, qui sont exposées dans hello [portail Azure classic].

## <a name="monitoring-and-troubleshooting"></a>Surveillance et dépannage
### <a name="what-troubleshooting-capabilities-are-available"></a>Quelles sont les fonctionnalités proposées pour faciliter la résolution des problèmes ?
Azure Notification Hubs fournit plusieurs fonctionnalités pour le dépannage, en particulier pour le scénario le plus courant de notifications déposés hello. Pour plus d’informations, consultez hello [la résolution des problèmes de concentrateurs de Notification] livre blanc.

### <a name="what-telemetry-features-are-available"></a>Quelles sont les fonctionnalités de télémétrie proposées ?
Azure permet de concentrateurs de Notification consulter les données de télémétrie hello [portail Azure classic]. Détails de métriques de hello sont disponibles sur hello [métriques de concentrateurs de Notification] page.

> [!NOTE]
> Notifications réussies signifient simplement que des notifications push ont été remises toohello PNS externe (par exemple, APNS d’Apple) ou GCM pour Google. Il incombe hello hello PNS toodeliver hello notifications tootarget des appareils. En règle générale, hello PNS n’expose pas les parties de toothird de métriques de remise.  
> 
> 

Nous fournissons également des données de télémétrie hello capacité tooexport hello par programmation (dans le niveau Standard de hello). Pour plus d’informations, consultez hello [exemple de métriques de concentrateurs de Notification].

[portail Azure classic]: https://manage.windowsazure.com
[tarification des Hubs de Notification]: http://azure.microsoft.com/pricing/details/notification-hubs/
[Notification Hubs SLA]: http://azure.microsoft.com/support/legal/sla/
[Étude de cas : Sochi]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=7942
[Étude de cas : Skanska]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5847
[Étude de cas : Seattle Times]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=8354
[Étude de cas : Mural.ly]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=11592
[Étude de cas : 7Digital]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=3684
[API REST de concentrateurs de Notification]: https://msdn.microsoft.com/library/azure/dn530746.aspx
[Notification Hubs prise en main des didacticiels]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[didacticiel de Chrome applications]: http://azure.microsoft.com/documentation/articles/notification-hubs-chrome-get-started/
[Mobile Services Pricing]: http://azure.microsoft.com/pricing/details/mobile-services/
[Guide d’inscription principale]: https://msdn.microsoft.com/library/azure/dn743807.aspx
[Guide d’inscription principale 2]: https://msdn.microsoft.com/library/azure/dn530747.aspx
[modèle de sécurité de concentrateurs de Notification]: https://msdn.microsoft.com/library/azure/dn495373.aspx
[didacticiel de Notification Hubs Secure Push]: http://azure.microsoft.com/documentation/articles/notification-hubs-aspnet-backend-ios-secure-push/
[la résolution des problèmes de concentrateurs de Notification]: http://azure.microsoft.com/documentation/articles/notification-hubs-diagnosing/
[métriques de concentrateurs de Notification]: https://msdn.microsoft.com/library/dn458822.aspx
[exemple de métriques de concentrateurs de Notification]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
[inscriptions exportation/importation]: https://msdn.microsoft.com/library/dn790624.aspx
[portail Azure]: https://portal.azure.com
[complete samples]: https://github.com/Azure/azure-notificationhubs-samples
[Mobile Apps]: https://azure.microsoft.com/services/app-service/mobile/
[tarification de Service application]: https://azure.microsoft.com/pricing/details/app-service/
