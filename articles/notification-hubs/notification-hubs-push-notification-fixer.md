---
title: aaaAzure Notification Hubs - recommandations de diagnostic
description: "Instructions sur comment toodiagnose commun problèmes avec Azure Notification Hubs."
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Azure Notification Hubs : instructions relatives au diagnostic
## <a name="overview"></a>Vue d'ensemble
Une des questions les plus fréquentes hello soumises par nos clients d’Azure Notification Hubs est comment toofigure out pourquoi ils ne voient pas une notification envoyée à partir de leur serveur principal d’application s’affichent sur l’appareil client de hello, où et pourquoi les notifications ont été supprimées et comment toofix cela. Dans cet article nous allons examiner hello différentes raisons pour lesquelles des notifications peuvent être perdues ou ne se terminent pas sur les appareils hello. Nous allons également des manières dans laquelle vous pouvez analyser et déterminer la cause première hello. 

Tout d’abord, il est critique toounderstand comment Azure Notification Hubs pousse les appareils toohello des notifications.
![][0]

Dans un flux de notification d’envoi par défaut, le message de type hello est envoyé de hello **principale** trop**Azure Notification Hub (NH)** qui est à son tour un traitement sur toutes les inscriptions hello tenant hello du compte configuré autrement dit, toutes les inscriptions de hello nécessitant une notification push de hello tooreceive balises & toodetermine expressions de balise « cibles ». Ces inscriptions peuvent s’étendre sur tout ou partie de nos plateformes prises en charge : iOS, Google, Windows, Windows Phone, Kindle et Baidu pour Android en Chine. Une fois que les cibles de hello sont établies, NH puis push notifications, divisé en plusieurs lots d’inscriptions, toohello périphérique spécifiques à la plateforme **du Service de Notification Push (PNS)** -par exemple, APNS d’Apple, GCM pour Google etc.. NH authentifie avec hello que PNS respectifs basé sur les informations d’identification hello que vous définissez Bonjour portail classique Azure sur la page Configurer un concentrateur de Notification de hello. Hello PNS transmet ensuite respectifs hello-notifications-toohello **les périphériques clients**. Il s’agit de plateforme hello recommandé des notifications push de façon toodeliver et Remarque qu’hello dernier tronçon de remise de notification a lieu entre la plateforme de hello PNS et de périphérique de hello. Il y a donc quatre composants principaux (*client*, *serveur principal d’application*, *Azure Notification Hubs (NH)* et *services de notification Push [PNS]*), chacun d’eux pouvant être à l’origine de la perte de notifications. Plus de détails sur cette architecture sont disponibles sur la page [Vue d’ensemble de Notification Hubs].

Toodeliver échec notifications peuvent se produire au cours de hello initiale intermédiaires/test phase qui peut indiquer un problème de configuration ou il peut se produire en production où tout ou partie des hello notifications peut-être être mise en route supprimée indiquant une application plus approfondie la messagerie ou problème de modèle. Dans la section de hello, ci-dessous nous allons examiner différents scénarios de notifications déposé allant toohello plus rare type courant, que certains d'entre eux vous souhaiterez peut-être évident et d’autres pas bien. 

## <a name="azure-notifications-hub-mis-configuration"></a>Mauvaise configuration d’Azure Notification Hubs
Azure Notification Hubs doit tooauthenticate lui-même dans le contexte de hello de toohello de développeur hello application toobe toosuccessfully peut envoyer des notifications PNS respectifs. Ceci est rendu possible par le développeur hello création d’un compte de développeur dans un appel de respectifs hello (Google, Apple, etc. de Windows) et puis inscrire leur application où obtenir des informations d’identification qui doivent toobe configuré dans le portail hello sous Notification Section de configuration de concentrateurs. Si aucune notification n’apportez via la première étape doit être tooensure que les informations d’identification correctes hello sont configurées dans hello Hub de Notification leur mise en correspondance avec l’application hello créé sous son compte de développeur spécifique de plate-forme. Vous trouverez notre [didacticiels de mise en route] toogo utile sur ce processus de manière étape par étape. Voici certaines configurations erronées communes :

1. **Généralités**
   
    a) Vérifiez que que votre nom de hub de notification (sans les fautes de frappe) est hello même :
   
   * Lorsque vous inscrivez à partir du client de hello, 
   * Où vous envoyez des notifications à partir du serveur principal hello,  
   * Où vous avez configuré les informations d’identification PNS de hello et 
   * Dont informations d’identification SAP que vous avez configuré sur hello client et hello principal. 
     
     (b) Vérifiez que vous utilisez hello SAS configuration chaînes sur le client de hello et principal d’application hello. En règle générale, vous devez utiliser hello **DefaultListenSharedAccessSignature** sur le client de hello et **DefaultFullSharedAccessSignature** sur le serveur principal d’application hello (ce qui donne l’autorisation toobe toohello de notification en mesure de toosend NH)
2. **Configuration d’Apple Push Notification Service (APNS)**
   
    Vous devez disposer de deux hubs différents : un pour la production et un autre pour vos essais. Cela signifie que le téléchargement de certificat hello que vous allez toouse dans concentrateur indépendant de bac à sable environnement tooa et certificat hello que vous allez toouse dans le hub de production tooa distinct. N’essayez pas de tooupload différents types de certificats toohello même concentrateur telle qu’elle peut entraîner des échecs de notification vers le bas de la ligne de hello. Si vous trouvez vous-même dans un emplacement où vous avez téléchargé par inadvertance les différents types de certificat toohello même concentrateur, il est recommandé concentrateur de hello toodelete et les frais de début. Si, pour une raison quelconque, vous n’êtes pas toodelete en mesure de concentrateur de hello puis à hello très moins, vous devez supprimer toutes les inscriptions existantes hello du concentrateur de hello. 
3. **Configuration de Google Cloud Messaging (GCM)** 
   
    a) Assurez-vous que vous activez « Google Cloud Messaging pour Android » dans votre projet cloud. 
   
    ![][2]
   
    (b) Vérifiez que vous créez une clé « serveur » lors de l’obtention des informations d’identification hello quels NH utilisera tooauthenticate avec GCM. 
   
    ![][3]
   
    (c) Vérifiez que vous devez configurer « ID de projet » sur le client hello qui est une entité entièrement numérique que vous pouvez obtenir à partir du tableau de bord hello :
   
    ![][1]

## <a name="application-issues"></a>Problèmes de l’application
1) **Balises/expressions de balises**

Si vous utilisez des balises ou toosegment d’expressions de balise votre public, il est toujours possible que lorsque vous envoyez des notifications de hello, il n’existe aucune cible n’a été trouvée basées sur des expressions de balises/balise hello que vous spécifiez dans votre appel d’envoi. Il est préférable de tooreview votre tooensure les enregistrements qu’il existe des balises qui correspondent lorsque vous envoyez une notification et vérifiez accusé de réception hello uniquement à partir de clients hello avec ces enregistrements. Par exemple, Si tous les enregistrements avec NH ont été réalisés avec par exemple la balise « Politique » et que vous envoyez une notification avec la balise « Sports », il ne sera pas envoyé tooany appareil. Un cas complexe peut impliquer des expressions de balises où vous n’êtes inscrit qu’avec « Balise A » OR « Balise B », mais les expressions de balises que vous ciblez lors de l’envoi de notifications sont « Balise A && Balise B ». Bonjour diagnostiquer automatiquement section conseils ci-dessous, il existe dans laquelle vous pouvez consulter vos enregistrements, ainsi que les balises hello qu’ils ont des méthodes. 

2) **Problèmes liés aux modèles**

Si vous utilisez des modèles, assurez-vous que vous suivez les indications hello décrites à [des conseils de modèle]. 

3) **Inscriptions non valides**

En supposant que hello que Hub de Notification a été correctement configuré et toutes les expressions de balises/balises ont été utilisées correctement résultant dans la zone Rechercher hello de cibles valides des notifications de hello toowhich doivent toobe envoyé, NH déclenche de plusieurs lots de traitement en parallèle - chaque lot envoi de messages ensemble tooa d’inscriptions. 

> [!NOTE]
> Étant donné que nous hello du traitement en parallèle, nous ne garantissent pas commande hello dans le hello notifications seront remises. 
> 
> 

Azure Notifications Hub est optimisé pour un modèle de remise de message « au plus une fois ». Cela signifie que nous tentons une déduplication afin qu’aucune notification n’est remise tooa périphérique plusieurs fois. tooensure cela nous via les inscriptions hello et assurez-vous qu’un seul message est envoyé par l’identificateur de l’appareil avant envoi réellement toohello de message hello PNS. Comme chaque lot est envoyé toohello PNS, qui à son tour est d’accepter et valider les enregistrements de hello, il est possible que hello PNS détecte une erreur avec un ou plusieurs des inscriptions de hello dans un lot, renvoie une erreur de tooAzure NH et arrête le traitement et la suppression qui traitement par lots complètement. Cela est particulièrement vrai pour un APNS qui utilise un protocole de flux TCP. Bien que nous sommes optimisé au plus une fois remise, dans ce cas, nous supprimons hello défaillant d’inscription à partir de notre base de données, puis les nouvelles tentatives de remise des notifications pour reste hello d’appareils hello dans ce lot.

Vous pouvez obtenir des informations sur l’erreur de tentative de remise a échoué hello par rapport à une inscription à l’aide de hello API REST de Azure Notification Hubs : [par Message télémétrie : obtenir de télémétrie de Message de Notification](https://msdn.microsoft.com/library/azure/mt608135.aspx) et [PNS commentaires](https://msdn.microsoft.com/library/azure/mt705560.aspx). Consultez hello [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) par exemple de code.

## <a name="pns-issues"></a>Problèmes de PNS
Une fois que le message de notification d’appel a été reçu par Bonjour PNS respectifs, il s’agit de sa responsabilité toodeliver hello toohello de périphérique de notification. Azure Notification Hubs est en dehors de l’image hello ici et n’a aucun contrôle quand ou si la notification de hello est en train de toobe remis toohello appareil. Étant donné que les services de notification de plateforme hello sont assez fiables, notifications généralement des appareils tooreach hello en quelques secondes de hello PNS. Si hello PNS toutefois limite Azure Notification Hubs applique une stratégie d’interruption exponentielle et si hello PNS reste inaccessible pendant 30 minutes, nous avoir une stratégie de placer tooexpire et supprimer définitivement les ces messages. 

Si un système PNS tente toodeliver une notification mais hello appareil est hors connexion, notification de hello est stockée par hello PNS pour une période de temps limitée et remise toohello appareil lorsqu’il est disponible. Seule une notification récente est stockée pour une application donnée. Si plusieurs notifications sont envoyées à l’appareil de hello est hors connexion, chaque nouvelle notification provoque la notification préalable de hello toobe ignoré. Ce comportement de conserver uniquement les notifications les plus récents hello est tooas auxquels des notifications dans APNS de fusion et de réduction dans GCM (qui utilise une clé de réduction). Si l’appareil de hello reste hors connexion pendant une longue période, les notifications qui ont été stockées pour celle-ci sont ignorées. Source : [Aide sur APNs] & [Aide sur GCM]

Avec Azure Notification Hubs - vous pouvez transmettre une clé de fusion via un en-tête HTTP à l’aide de hello générique `SendNotification` API (par exemple, pour le Kit de développement logiciel .NET – `SendNotificationAsync`) qui accepte également les en-têtes HTTP qui sont passées en tant qu’est toohello PNS respectifs. 

## <a name="self-diagnose-tips"></a>Conseils pour le diagnostic personnel
Ici, nous allons examiner hello différents moyens toodiagnose et racine provoquent des problèmes de concentrateur de Notification :

### <a name="verify-credentials"></a>Vérification des informations d’identification
1. **Portail des développeurs PNS**
   
    Les vérifier au hello respectifs PNS developer portal (APNS, GCM, WNS, etc.) à l’aide de notre [didacticiels de mise en route].
2. **Portail Azure Classic**
   
    Accédez toohello configurer onglet tooreview et correspondent aux informations d’identification hello avec ceux obtenus à partir du portail des développeurs hello PNS. 
   
    ![][4]

### <a name="verify-registrations"></a>Vérification des inscriptions
1. **Visual Studio**
   
    Si vous utilisez Visual Studio pour le développement vous pouvez connecter tooMicrosoft Azure et afficher et gérer un ensemble de services Azure, y compris le Hub de Notifications à partir de « Explorateur de serveurs ». Cela est particulièrement utile pour votre environnement de développement et de test. 
   
    ![][9]
   
    Vous pouvez afficher et gérer toutes les inscriptions hello dans votre concentrateur qui sont classées correctement pour l’inscription de plateforme, natif ou modèle de toutes les balises, identificateur de la solution, date d’expiration hello et les id d’enregistrement. Vous pouvez également modifier une inscription volée hello - ce qui est utile par exemple si vous souhaitez tooedit de balises. 
   
    ![][8]
   
   > [!NOTE]
   > Inscriptions tooedit de fonctionnalités Visual Studio doivent uniquement être utilisées pendant le développement et de test avec un nombre limité d’enregistrements. Envisagez de vos enregistrements en bloc, s’il se produit une toofix nécessaire à l’aide des fonctionnalités de l’inscription d’exportation/importation hello décrites ici - [les enregistrements d’exportation/importation](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **Explorateur Service Bus**
   
    De nombreux clients utilisent l’explorateur ServiceBus, décrit ici : [Explorateur ServiceBus] , pour afficher et gérer leur hub de notification. C’est un projet open source disponible sur code.microsoft.com : [Code de l’explorateur ServiceBus]

### <a name="verify-message-notifications"></a>Vérification des notifications de messages
1. **Portail Azure Classic**
   
    Vous pouvez accéder toohello « Debug » onglet toosend test notifications tooyour les clients sans avoir besoin de n’importe quel serveur principal de service des et en cours d’exécution. 
   
    ![][7]
2. **Visual Studio**
   
    Vous pouvez également envoyer des notifications de test à partir de confort hello de Visual Studio :
   
    ![][10]
   
    Vous pouvez en savoir plus sur hello Visual Studio Notification Hub Azure explorer les fonctionnalités ici : 
   
   * [Vue d’ensemble de l’Explorateur de serveurs Visual Studio]
   * [Billet de blog concernant l’Explorateur de serveurs de Visual Studio : 1]
   * [Billet de blog concernant l’Explorateur de serveurs de Visual Studio : 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>Débogage de notifications ayant échoué/analyse des résultats de notification
**Propriété EnableTestSend**

Lorsque vous envoyez une notification via des concentrateurs de Notification, initialement il simplement Obtient la file d’attente pour toodo NH traitement toofigure out toutes ses cibles, puis finalement NH envoie celui-ci toohello PNS. Cela signifie que lorsque vous utilisez l’API REST ou des clients de hello SDK, hello retour réussi de votre envoi appel seul moyen qui hello message a été correctement la file d’attente avec le Hub de Notification. Il ne donne pas une idée de ce qui s’est produite lors de la NH obtenu au final toosend hello message tooPNS. Si votre notification n’est pas arrivée au périphérique de client hello, il est possible que lorsque NH essayées toodeliver hello message tooPNS, erreur lors de la taille de charge utile par exemple hello dépassé hello nombre maximum par hello PNS ou sont des informations d’identification de hello configurées dans NH tooget etc. non valide une idée des erreurs PNS hello, nous avons introduit une propriété appelée [EnableTestSend fonctionnalité]. Cette propriété est automatiquement activée lorsque vous envoyez le test des messages à partir de portail de hello ou client Visual Studio et vous permet de toosee détaillée les informations de débogage. Vous pouvez utiliser cette fonction via des API prenant l’exemple hello Hello .NET SDK, où il n’est disponible actuellement et serez ajouté tooall kits de développement logiciel client par la suite. toouse avec l’appel REST hello, simplement ajouter un paramètre de chaîne de requête appelé « test » à fin hello de votre appel d’envoi, par exemple 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*Exemple (Kit de développement logiciel (SDK) .NET)*

Supposons que vous utilisez le Kit de développement .NET toosend une notification toast natif :

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`sera simplement état `Enqueued` à fin hello d’exécution hello sans idée tout ce qui est devenu tooyour push. Vous pouvez désormais utiliser hello `EnableTestSend` propriété booléenne lors de l’initialisation hello `NotificationHubClient` et vous pouvez obtenir l’état détaillé sur les erreurs PNS hello rencontré lors de l’envoi de notification de hello. appel d’envoi Hello ici prendra plus de temps tooreturn, car elle renvoie uniquement une fois NH a remis le résultat hello toodetermine hello notification tooPNS. 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*Exemple de sortie*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

Ce message indique les informations d’identification non valides sont configurées dans le hub de notification hello ou un problème avec les enregistrements de hello sur le concentrateur de hello et hello recommandé cours seraient toodelete cette inscription et permettent de client de hello recréer avant l’envoi de hello Message. 

> [!NOTE]
> Notez que l’utilisation de cette propriété hello est très limitée et par conséquent, vous devez uniquement l’utiliser dans un environnement de développement et de test avec un ensemble limité d’inscriptions. Nous envoyer uniquement les notifications de débogage too10 périphériques. Nous avons également une limite de traitement du débogage envoie toobe 10 par minute. 
> 
> 

### <a name="review-telemetry"></a>Révision de la télémétrie
1. **Utiliser le portail Azure Classic**
   
    portail de Hello vous permet de tooget un aperçu rapide de toutes les activités de hello sur votre concentrateur de Notification. 
   
    un) à partir de l’onglet de « tableau de bord » hello, vous pouvez afficher une vue agrégée des inscriptions de hello, notifications ainsi que des erreurs par la plateforme. 
   
    ![][5]
   
    (b) vous pouvez également ajouter plusieurs autres métriques spécifique de plate-forme à partir de l’onglet tootake étudier plus particulièrement en toute erreur spécifique PNS retournée quand NH tente toosend hello notification toohello PNS de hello « Analyse ». 
   
    ![][6]
   
    c) vous devez commencer par examiner les hello **les Messages entrants**, **opérations d’inscription**, **Notifications réussies** et passez hello de tooreview onglet tooper plateforme Erreurs spécifiques PNS. 
   
    d) si vous avez notification hello hub mal configuré avec les paramètres d’authentification hello puis vous verrez l’erreur d’authentification PNS. Il s’agit d’une bonne indication toocheck hello PNS des informations de. 

2) **Accès par programme**

Plus de détails ici : 

* [Accès par programme à la télémétrie]
* [Exemple d’accès à la télémétrie via les API] 

> [!NOTE]
> Plusieurs fonctionnalités liées à la télémétrie, comme **l’Exportation/importation des enregistrements**, **l’accès à la télémétrie au moyen des API**, etc., sont uniquement disponibles en niveau Standard. Si vous essayez de toouse ces fonctionnalités si vous êtes dans gratuit ou de niveau de base puis vous obtiendrez l’effet de toothis exception message lors de l’utilisation de hello SDK et un HTTP 403 (interdit) lors de leur utilisation directement à partir de l’API REST de hello. Assurez-vous que vous avez déplacé des tooStandard niveau via le portail classique Azure.  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[Vue d’ensemble de Notification Hubs]: notification-hubs-push-notification-overview.md
[didacticiels de mise en route]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[des conseils de modèle]: https://msdn.microsoft.com/library/dn530748.aspx 
[Aide sur APNs]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[Aide sur GCM]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[Explorateur ServiceBus]: http://msdn.microsoft.com/library/dn530751.aspx
[Code de l’explorateur ServiceBus]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[Vue d’ensemble de l’Explorateur de serveurs Visual Studio]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[Billet de blog concernant l’Explorateur de serveurs de Visual Studio : 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[Billet de blog concernant l’Explorateur de serveurs de Visual Studio : 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend fonctionnalité]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[Accès par programme à la télémétrie]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[Exemple d’accès à la télémétrie via les API]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

