---
title: aaaSending des notifications de push avec Azure Notification Hubs et Node.js
description: "Découvrez comment toouse concentrateurs de Notification toosend des notifications push à partir d’une application Node.js."
keywords: notification push,notifications push,node.js push, ios push
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Envoi de notifications Push avec Azure Notification Hubs et Node.js
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Vue d'ensemble
> [!IMPORTANT]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).
> 
> 

Ce guide vous explique comment toosend push notifications aide hello d’Azure Notification Hubs directement à partir d’une application Node.js. 

Hello scénarios couverts : envoi tooapplications de notifications push sur hello suivant plateformes

* Android
* iOS
* Windows Phone
* Plateforme Windows universelle 

Pour plus d’informations sur les concentrateurs de notification, consultez hello [étapes](#next) section.

## <a name="what-are-notification-hubs"></a>Présentation de Notification Hubs
Azure Notification Hubs fournit une infrastructure facile à utiliser, multiplateforme et évolutive pour l’envoi des périphériques toomobile de notifications push. Pour plus d’informations sur l’infrastructure de service hello, consultez hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.

## <a name="create-a-nodejs-application"></a>Création d'une application Node.js
Hello première étape de ce didacticiel crée une nouvelle application Node.js vide. Pour obtenir des instructions sur la création d’une application Node.js, consultez [créer et déployer un tooAzure d’application Node.js Site Web][nodejswebsite], [Service de cloud computing Node.js] [ Node.js Cloud Service] à l’aide de Windows PowerShell, ou [Site Web avec WebMatrix].

## <a name="configure-your-application-toouse-notification-hubs"></a>Configurer votre Application tooUse Notification Hubs
toouse Azure Notification Hubs, vous devez toodownload et utilisez hello Node.js [package azure](https://www.npmjs.com/package/azure), qui inclut un ensemble prédéfini de bibliothèques d’assistance qui communiquent avec les services de REST de notification push hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package
1. Utiliser une interface de ligne de commande comme **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Linux) et accédez dossier toohello où vous avez créé votre application vide .
2. Type **npm installer azure-sb** dans la fenêtre de commande hello.
3. Vous pouvez exécuter manuellement hello **ls** ou **dir** tooverify de commande qui un **nœud\_modules** dossier a été créé. Dans ce dossier, recherche hello **azure** package qui contient les bibliothèques hello vous devez tooaccess hello Hub de Notification.

> [!NOTE]
> Plus d’informations sur l’installation NPM sur officielle de hello [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm). 
> 
> 

### <a name="import-hello-module"></a>Module d’importation hello
À l’aide d’un éditeur de texte, ajoutez hello suivant en haut de toohello de hello **server.js** fichier de l’application hello :

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Configuration d’une connexion Azure Notification Hubs
Hello **NotificationHubService** objet vous permet de travailler avec des concentrateurs de notification. Hello de code suivant crée un **NotificationHubService** objet pour le hub de notification hello nommé **hubname**. Ajoutez-le haut hello Hello **server.js** fichier, après le module de hello instruction tooimport hello azure :

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Hello connexion **connectionstring** peut être obtenue à partir de hello [portail Azure] en effectuant hello comme suit :

1. Dans le volet de navigation gauche hello, cliquez sur **Parcourir**.
2. Sélectionnez **concentrateurs de Notification**, puis rechercher hello hub vous souhaitez toouse pour l’exemple hello et. Vous pouvez faire référence toohello [Windows Store prise en main de didacticiel](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) si vous avez besoin d’aide pour créer un concentrateur de Notification.
3. Sélectionnez **Paramètres**.
4. Cliquez sur **Stratégies d’accès**. Vous pouvez voir les chaînes de connexion d’accès total et partagé.

![Portail Azure - Notification Hubs](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> Vous pouvez également récupérer la chaîne de connexion hello à l’aide de hello **Get-AzureSbNamespace** applet de commande fournie par [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello **afficher d’espace de noms service bus azure** avec Hello [Azure Interface de ligne (Azure)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Architecture générale
Hello **NotificationHubService** objet expose hello suivant des instances d’objet pour l’envoi de push notifications toospecific appareils et applications :

* **Android** -utilisez hello **GcmService** objet, qui est disponible à l’adresse **notificationHubService.gcm**
* **iOS** -utilisez hello **ApnsService** objet, qui est accessible à **notificationHubService.apns**
* **Windows Phone** -utilisez hello **MpnsService** objet, qui est disponible à l’adresse **notificationHubService.mpns**
* **Plateforme Windows universelle** -utilisez hello **WnsService** objet, qui est disponible à l’adresse **notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>Comment : envoyer des applications tooAndroid de notifications push
Hello **GcmService** objet fournit une **envoyer** (méthode) qui peut être utilisés toosend push notifications tooAndroid applications. Hello **envoyer** méthode accepte hello paramètres suivants :

* **Balises** -hello identificateur de balise. Si aucune balise n’est fourni, notification de hello est envoyée tooall clients.
* **Charge utile** -hello JSON ou la charge utile de chaîne brute du message.
* **Rappel** -hello la fonction de rappel.

Pour plus d’informations sur le format de charge utile hello, consultez hello **charge utile** section Hello [implémentation d’un serveur GCM](http://developer.android.com/google/gcm/server.html#payload) document.

Hello de code suivant utilise hello **GcmService** instance exposée par hello **NotificationHubService** toosend un tooall de notification push inscrit les clients.

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>Comment : envoyer des applications tooiOS de notifications push
Même comme avec les applications Android décrite ci-dessus, hello **ApnsService** objet fournit une **envoyer** (méthode) qui peut être utilisés toosend push notifications tooiOS applications. Hello **envoyer** méthode accepte hello paramètres suivants :

* **Balises** -hello identificateur de balise. Si aucune balise n’est fourni, notification de hello est envoyée tooall clients.
* **Charge utile** - hello JSON du message ou charge utile de la chaîne.
* **Rappel** -hello la fonction de rappel.

Pour le format de charge utile hello plus d’informations, consultez hello **charge utile de Notification** section Hello [Local et le Guide de programmation de Notification Push](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.

Hello de code suivant utilise hello **ApnsService** instance exposée par hello **NotificationHubService** toosend une alerte de message tooall clients :

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>Comment : envoyer des applications de téléphone tooWindows des notifications push
Hello **MpnsService** objet fournit une **envoyer** méthode qui peut être utilisé toosend push notifications tooWindows applications téléphoniques. Hello **envoyer** méthode accepte hello paramètres suivants :

* **Balises** -hello identificateur de balise. Si aucune balise n’est fourni, notification de hello est envoyée tooall clients.
* **Charge utile** -hello la charge utile XML du message.
* **TargetName** - `toast` pour les notifications toast. `token` pour les notifications par vignette.
* **Classe de notification** -hello priorité de notification de hello. Consultez hello **éléments d’en-tête HTTP** section Hello [des notifications Push à partir d’un serveur](http://msdn.microsoft.com/library/hh221551.aspx) document pour les valeurs valides.
* **Options** : en-têtes de demande facultatifs.
* **Rappel** -hello la fonction de rappel.

Pour obtenir la liste de valide **TargetName**, **classe de notification** et options d’en-tête, consultez hello [des notifications Push à partir d’un serveur](http://msdn.microsoft.com/library/hh221551.aspx) page.

Hello suivant l’exemple de code utilise hello **MpnsService** instance exposée par hello **NotificationHubService** toosend une notification toast :

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>Comment : envoyer des applications de Windows Platform (UWP) tooUniversal de notifications push
Hello **WnsService** objet fournit une **envoyer** méthode qui peut être des applications de plateforme Windows tooUniversal toosend utilisé push notifications.  Hello **envoyer** méthode accepte hello paramètres suivants :

* **Balises** -hello identificateur de balise. Si aucune balise n’est fourni, notification de hello est envoyée tooall inscrit clients.
* **Charge utile** -charge utile du message XML hello.
* **Type** -hello du type de notification.
* **Options** : en-têtes de demande facultatifs.
* **Rappel** -hello la fonction de rappel.

Pour obtenir la liste des types et en-têtes de demande valides, consultez [En-têtes de demande et de réponse des services de notifications Push](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Hello de code suivant utilise hello **WnsService** instance exposée par hello **NotificationHubService** toosend une application UWP de toast push notification tooa :

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Étapes suivantes
Hello exemple des extraits de code ci-dessus permettent de vous tooeasily build service infrastructure toodeliver push notifications tooa large gamme de périphériques. Maintenant que vous avez appris les notions de base de hello de l’utilisation des concentrateurs de Notification avec node.js, suivez ces liens de toolearn plus d’informations sur la manière d’étendre ces fonctionnalités supplémentaires.

* Consultez hello référence MSDN pour [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Visitez hello [Azure SDK pour le nœud] référentiel sur GitHub pour plus d’exemples et les détails d’implémentation.

[Azure SDK pour le nœud]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[Site Web avec WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[portail Azure]: https://portal.azure.com
