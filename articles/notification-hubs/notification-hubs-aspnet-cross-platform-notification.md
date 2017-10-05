---
title: Envoi de notifications interplateformes aux utilisateurs avec Notification Hubs (ASP.NET)
description: "Découvrez comment utiliser des modèles Notification Hubs pour envoyer, dans une même demande, une notification indépendante de la plateforme qui cible toutes les plateformes."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: ef971fcfe68978ea9ce0810c69efbe134bb15f8a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a>Envoi de notifications interplateforme aux utilisateurs avec Notification Hubs
Dans le didacticiel précédent [Notification des utilisateurs avec Notification Hubs], vous avez appris à envoyer des notifications Push à tous les appareils inscrits par un utilisateur authentifié. Dans ce didacticiel, l'envoi d'une notification à chaque plateforme cliente prise en charge nécessitait plusieurs demandes. Notification Hubs prend en charge des modèles qui permettent de spécifier le mode de réception préféré d'un appareil déterminé. Cela simplifie l'envoi de notifications interplateforme. Cette rubrique montre comment exploiter les modèles pour envoyer, dans une même demande, une notification qui cible toutes les plateformes, quelles qu’elles soient. Pour plus d’informations sur les modèles, consultez [Vue d’ensemble d’Azure Notification Hubs][Templates].
> [!IMPORTANT]
> Les projets Windows Phone 8.1 et versions antérieures ne sont pas pris en charge dans Visual Studio 2017. Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Notification Hubs permet à un appareil d’inscrire plusieurs modèles avec la même balise. Dans ce cas, un message entrant ciblant cette balise déclenche l'envoi de plusieurs notifications à destination de l'appareil, une pour chaque modèle. Cela vous permet d'afficher le même message dans plusieurs notifications visuelles, par exemple, sous la forme d'un badge et d'une notification toast dans une application Windows Store.
> 
> 

Pour envoyer des notifications interplateforme à l'aide de modèles, procédez comme suit :

1. Dans l'Explorateur de solutions de Visual Studio, développez le dossier **Controllers** , puis ouvrez le fichier RegisterController.cs.
2. Recherchez le bloc de code dans la méthode **Put** qui crée une inscription. Remplacez le contenu de `switch` par le code suivant :
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    Ce code permet d’appeler la méthode propre à la plateforme pour créer une inscription de modèle et non une inscription native. Les inscriptions existantes n'ont pas besoin d'être modifiées, car les inscriptions de modèle sont dérivées d'inscriptions natives.
3. Dans le contrôleur **Notifications**, remplacez la méthode **sendNotification** par le code suivant :
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Ce code permet d'envoyer une notification à toutes les plateformes à la fois et sans avoir à spécifier de charge utile native. Notification Hubs génère et remet la charge utile appropriée à chaque appareil avec la valeur de *balise* fournie, comme spécifié dans les modèles inscrits.
4. Republiez votre projet principal WebApi.
5. Réexécutez l'application cliente et vérifiez la réussite de l'inscription.
6. (Facultatif) Déployez l'application cliente sur un deuxième appareil, puis exécutez l'application.
   
    À noter qu'une notification s'affiche sur chaque appareil.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez terminé ce didacticiel, vous trouverez des informations supplémentaires sur Notification Hubs et les modèles dans les rubriques suivantes :

* **[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]** <br/>Présente un autre scénario d'utilisation des modèles.
* **[Vue d’ensemble d’Azure Notification Hubs][Templates]**<br/>Rubrique générale offrant des informations plus détaillées sur les modèles.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[Notification des utilisateurs avec Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
