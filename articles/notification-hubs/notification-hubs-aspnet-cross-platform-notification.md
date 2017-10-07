---
title: aaaSend inter-plateformes notifications toousers avec Notification Hubs (ASP.NET)
description: "Découvrez comment toosend de modèles de Notification Hubs toouse, dans une requête unique, une notification de plateforme agnostique ciblant toutes les plateformes."
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
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>Envoyer toousers inter-plateformes notifications avec Notification Hubs
Dans le cadre du didacticiel précédent hello [avertir les utilisateurs avec des concentrateurs de Notification], vous avez appris comment les appareils tooall toopush notifications inscrit par un utilisateur authentifié spécifique. Dans ce didacticiel, plusieurs requêtes ont été toosend requis une plateforme de client de notification tooeach pris en charge. Notification Hubs prend en charge les modèles qui vous permettent de spécifier comment un périphérique spécifique veut tooreceive notifications. Cela simplifie l'envoi de notifications interplateforme. Cette rubrique montre comment parti tootake de toosend de modèles, dans une requête unique, une notification de plateforme agnostique ciblant toutes les plateformes. Pour plus d’informations sur les modèles, consultez [Vue d’ensemble d’Azure Notification Hubs][Templates].
> [!IMPORTANT]
> Les projets Windows Phone 8.1 et versions antérieures ne sont pas pris en charge dans Visual Studio 2017. Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Concentrateurs de notification permet un tooregister appareil plusieurs modèles hello même balise. Dans ce cas, un message entrant de ciblage que balise génère plusieurs notifications remis toohello périphérique, un pour chaque modèle. Cela permet de vous toodisplay hello même message dans plusieurs notifications visual, tels que les deux comme un badge et comme une notification toast dans une application Windows Store.
> 
> 

Terminer hello suivant notifications étapes toosend inter-plateformes à l’aide de modèles :

1. Dans l’Explorateur de solutions dans Visual Studio de hello, développez hello **contrôleurs** dossier, puis fichier RegisterController.cs de hello ouvert.
2. Localisez le bloc hello de code Bonjour **Put** méthode qui crée une inscription remplacer hello `switch` avec hello suivant de code :
   
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
   
    Ce code appelle hello spécifique à la plateforme méthode toocreate une inscription de modèle au lieu d’une inscription native. Les inscriptions existantes n'ont pas besoin d'être modifiées, car les inscriptions de modèle sont dérivées d'inscriptions natives.
3. Bonjour **Notifications** contrôleur, remplacer hello **sendNotification** méthode avec hello suivant de code :
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Ce code envoie une notification tooall plateformes à hello même temps et sans devoir toospecify une charge utile native. Génère des concentrateurs de notification et remet hello appareil tooevery de charge utile correct avec hello fourni *balise* valeur, comme indiqué dans les modèles de hello inscrit.
4. Republiez votre projet principal WebApi.
5. Réexécutez l’application cliente de hello et vérifier que l’inscription réussit.
6. (Facultatif) Deuxième appareil hello client application tooa de déployer, puis exécuter l’application hello.
   
    À noter qu'une notification s'affiche sur chaque appareil.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez terminé ce didacticiel, vous trouverez des informations supplémentaires sur Notification Hubs et les modèles dans les rubriques suivantes :

* **[Utilisez toosend concentrateurs de Notification dernières actualités]** <br/>Présente un autre scénario d'utilisation des modèles.
* **[Vue d’ensemble d’Azure Notification Hubs][Templates]**<br/>Rubrique générale offrant des informations plus détaillées sur les modèles.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Utilisez toosend concentrateurs de Notification dernières actualités]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[avertir les utilisateurs avec des concentrateurs de Notification]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
