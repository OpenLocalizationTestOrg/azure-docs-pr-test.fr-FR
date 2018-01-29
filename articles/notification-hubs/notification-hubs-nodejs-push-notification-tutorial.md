---
title: Envoi de notifications Push avec Azure Notification Hubs et Node.js
description: "Découvrez comment utiliser Notification Hubs pour envoyer des notifications Push à partir d’une application Node.js."
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
ms.openlocfilehash: ff2dd0c2ededa3664c48b5ff77b05466fceb4b3f
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/12/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Envoi de notifications Push avec Azure Notification Hubs et Node.js
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Vue d'ensemble
> [!IMPORTANT]
> Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).
> 
> 

Ce guide montre comment envoyer des notifications Push à l’aide d’Azure Notification Hubs directement à partir d’une application Node.js. 

Les scénarios traités incluent l’envoi de notifications Push à des applications sur les plateformes suivantes :

* Android
* iOS
* Windows Phone
* Plateforme Windows universelle 

Pour plus d'informations sur les concentrateurs de notification, consultez la section [Étapes suivantes](#next) .

## <a name="what-are-notification-hubs"></a>Présentation de Notification Hubs
Azure Notification Hubs offre une infrastructure multiplateforme extensible et conviviale pour l’envoi de notifications Push à des appareils mobiles. Pour plus d’informations sur l’infrastructure de service, voir la page [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) .

## <a name="create-a-nodejs-application"></a>Création d’une application Node.js
La première étape de ce didacticiel consiste à créer une application Node.js vide. Pour des instructions sur la création d’une application Node.js, consultez [Création et déploiement d’une application Node.js dans un site web Azure][nodejswebsite], [Service cloud Node.js][Node.js Cloud Service] avec Windows PowerShell ou [Site web avec WebMatrix].

## <a name="configure-your-application-to-use-notification-hubs"></a>Configuration de l’application pour utiliser Notification Hubs
Pour utiliser Azure Notification Hubs, vous devez télécharger et utiliser le [package Azure](https://www.npmjs.com/package/azure)Node.js, qui inclut un ensemble intégré de bibliothèques d’aide qui communiquent avec les services REST de notification Push.

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a>Utilisation de Node Package Manager (NPM) pour obtenir le package
1. Utilisez une interface de ligne de commande telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Linux) pour accéder au dossier dans lequel vous avez créé votre application vide.
2. Tapez **npm install azure-sb** dans la fenêtre de commande.
3. Vous pouvez exécuter manuellement la commande **ls** ou **dir** pour vérifier que le dossier **node\_modules** a été créé. Dans ce dossier, recherchez le package **azure** qui contient les bibliothèques nécessaires pour accéder à Notification Hubs.

> [!NOTE]
> Pour plus d’informations sur l’installation de NPM, consultez le [Blog NPM](http://blog.npmjs.org/post/85484771375/how-to-install-npm)officiel. 
> 
> 

### <a name="import-the-module"></a>Importation du module
À l'aide d'un éditeur de texte, ajoutez la commande suivante au début du fichier **server.js** de l'application :

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Configuration d’une connexion Azure Notification Hubs
L'objet **NotificationHubService** vous permet d'utiliser les hubs de notification. Le code suivant crée un objet **NotificationHubService** pour le Notification Hub nommé **hubname**. Ajoutez-le vers le début du fichier **server.js** , après l'instruction relative à l'importation du module Azure :

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Pour obtenir la valeur de connexion **connectionstring** à partir du [portail Azure] , procédez comme suit :

1. Dans le volet de navigation de gauche, cliquez sur **Parcourir**.
2. Sélectionnez **Notification Hubs**, puis recherchez le hub à utiliser pour l’exemple. Si vous avez besoin d’aide pour créer un hub de notification, vous pouvez consulter le [Didacticiel de prise en main de Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) .
3. Sélectionnez **Paramètres**.
4. Cliquez sur **Stratégies d’accès**. Vous pouvez voir les chaînes de connexion d’accès total et partagé.

![Portail Azure - Notification Hubs](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> Vous pouvez également extraire la chaîne de connexion à l’aide de l’applet de commande **Get-AzureSbNamespace** fournie par [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou de la commande **azure sb namespace show** avec [l’interface de ligne de commande Azure (Azure CLI)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Architecture générale
L’objet **NotificationHubService** expose les instances d’objet suivantes pour l’envoi de notifications Push à des appareils et applications spécifiques :

* **Android** : utilisez l’objet **GcmService**, disponible au niveau de **notificationHubService.gcm**
* **iOS** : utilisez l’objet **ApnsService**, disponible au niveau de **notificationHubService.apns**
* **Windows Phone** : utilisez l’objet **MpnsService**, disponible au niveau de **notificationHubService.mpns**
* **Plateforme Windows universelle** : utilisez l’objet **WnsService**, disponible au niveau de **notificationHubService.wns**

### <a name="how-to-send-push-notifications-to-android-applications"></a>Envoi de notifications Push à des applications Android
L’objet **GcmService** fournit une méthode **d’envoi** que vous pouvez utiliser pour envoyer des notifications Push à des applications Android. Cette méthode d' **envoi** accepte les paramètres suivants :

* **Tags** : identifiant de balise. Si aucune balise n’est fournie, la notification est envoyée à tous les clients.
* **Payload** : charge utile JSON ou de chaîne brute du message.
* **Callback** : fonction de rappel.

Pour plus d’informations sur le format de charge utile, consultez la section **Charge utile** du document relatif à [l’implémentation du serveur GCM](http://developer.android.com/google/gcm/server.html#payload) .

Le code suivant utilise l’instance **GcmService** exposée par **NotificationHubService** pour envoyer une notification Push à tous les clients inscrits.

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

### <a name="how-to-send-push-notifications-to-ios-applications"></a>Envoi de notifications Push à des applications iOS
Comme pour les applications Android décrites ci-dessus, l’objet **ApnsService** fournit une méthode **d’envoi** permettant d’envoyer des notifications Push à des applications iOS. Cette méthode d' **envoi** accepte les paramètres suivants :

* **Tags** : identifiant de balise. Si aucune balise n’est fournie, la notification est envoyée à tous les clients.
* **Payload** : charge utile JSON ou de chaîne du message.
* **Callback** : fonction de rappel.

Pour plus d’informations sur le format de charge utile, voir la section **Charge utile de notification** du [Guide de programmation des notifications locales et Push](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) .

Le code suivant utilise l’instance **ApnsService** exposée par **NotificationHubService** pour envoyer un message d’alerte à tous les clients :

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-windows-phone-applications"></a>Envoi de notifications Push à des applications Windows Phone
L’objet **MpnsService** fournit une méthode **d’envoi** permettant d’envoyer des notifications Push à des applications Windows Phone. Cette méthode d' **envoi** accepte les paramètres suivants :

* **Tags** : identifiant de balise. Si aucune balise n’est fournie, la notification est envoyée à tous les clients.
* **Payload** : charge utile XML du message.
* **TargetName** - `toast` pour les notifications toast. `token` pour les notifications par vignette.
* **NotificationClass** : priorité de la notification. Pour les valeurs valides, consultez la section **Éléments d’en-tête HTTP** de l’article [Notifications Push d’un serveur](http://msdn.microsoft.com/library/hh221551.aspx) .
* **Options** : en-têtes de demande facultatifs.
* **Callback** : fonction de rappel.

Pour la liste des options **TargetName**, **NotificationClass** et d’en-tête valides, consultez [Notifications Push](http://msdn.microsoft.com/library/hh221551.aspx).

L’exemple de code suivant utilise l’instance **MpnsService** exposée par **NotificationHubService** pour envoyer une notification Push :

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-universal-windows-platform-uwp-applications"></a>Envoi de notifications Push à des applications de la plate-forme Windows universelle (UWP)
L’objet **WnsService** fournit une méthode **d’envoi** permettant d’envoyer des notifications Push à des applications de la plateforme Windows universelle.  Cette méthode d' **envoi** accepte les paramètres suivants :

* **Tags** : identifiant de balise. Si aucune balise n’est fournie, la notification est envoyée à tous les clients inscrits.
* **Payload** : charge utile XML du message.
* **Type** : type de notification.
* **Options** : en-têtes de demande facultatifs.
* **Callback** : fonction de rappel.

Pour obtenir la liste des types et en-têtes de demande valides, consultez [En-têtes de demande et de réponse des services de notifications Push](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Le code suivant utilise l’instance **WnsService** exposée par **NotificationHubService** pour envoyer une notification Push toast à une application UWP :

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Étapes suivantes
Les exemples d’extrait de code ci-dessus permettent de créer facilement une infrastructure de service pour remettre des notifications Push à un vaste éventail d’appareils. À présent que vous avez appris les bases de l’utilisation de Notification Hubs avec node.js, suivez les liens suivants pour en savoir plus sur l’extension de ces fonctionnalités.

* Consultez la référence MSDN pour [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Pour d’autres exemples et des détails d’implémentation, visitez le dépôt [SDK Azure pour Node] sur GitHub.

[SDK Azure pour Node]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain the Default Management Credentials for the Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application to Use Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages to a Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[Site web avec WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[portail Azure]: https://portal.azure.com
