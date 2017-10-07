---
title: aaaSending des notifications de push avec Azure Notification Hubs sur Windows Phone | Documents Microsoft
description: Dans ce didacticiel, vous apprendrez comment des notifications de toouse Azure Notification Hubs toopush tooa Windows Phone 8 ou Windows Phone 8.1 Silverlight application.
services: notification-hubs
documentationcenter: windows
keywords: notification push,notification push,push windows phone
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Envoi de notifications Push avec Azure Notification Hubs sur Windows Phone
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).
> 
> 

Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 ou Windows Phone 8.1 Silverlight une application. Si vous ciblez Windows Phone 8.1 (non Silverlight), puis consultez toohello [Windows universel](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.
Dans ce didacticiel, vous créez une application Windows Phone 8 vide qui reçoit des notifications push à l’aide de hello services de notifications Push Microsoft (MPNS). Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution.

> [!NOTE]
> Hello Notification Hubs Windows Phone SDK ne prend pas en charge à l’aide de hello services de notifications Push Windows (WNS) avec les applications Windows Phone 8.1 Silverlight. toouse WNS (au lieu de MPNS) avec les applications Windows Phone 8.1 Silverlight, suivez hello [Notification Hubs - didacticiel de Windows Phone Silverlight], qui utilise l’API REST.
> 
> 

didacticiel de Hello montre le scénario de diffusion simple hello dans à l’aide de concentrateurs de Notification.

## <a name="prerequisites"></a>Composants requis
Ce didacticiel requiert hello qui suit :

* [Visual Studio 2012 Express pour Windows Phone]ou version ultérieure.

Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels concernant les Notification Hubs pour les applications Windows Phone 8.

## <a name="create-your-notification-hub"></a>Création de votre hub de notification
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Cliquez sur hello <b>Notification Services</b> section (dans <i>paramètres</i>), cliquez sur <b>Windows Phone (MPNS)</b> puis cliquez sur hello <b>activer push non authentifiées </b> case à cocher.</p>
</li>
</ol>

&emsp;&emsp;![Portail Azure - Activez les notifications Push non authentifiées](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

Votre concentrateur est maintenant créé et configuré toosend non authentifié de notification pour Windows Phone.

> [!NOTE]
> Ce didacticiel utilise MPNS en mode non authentifié. Le mode MPNS non authentifié est fourni avec des restrictions sur les notifications que vous pouvez envoyer tooeach canal. Prend en charge les concentrateurs de notification [MPNS authentifié mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) en vous tooupload votre certificat.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>Connectez votre concentrateur de notification d’application toohello
1. Dans Visual Studio, créez une application Windows Phone 8.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    Dans Visual Studio 2013 Update 2 ou version ultérieure, vous créez plutôt une application Silverlight Windows Phone.
   
    ![Visual Studio - Nouveau projet - Application vide - Windows Phone Silverlight][11]
2. Dans Visual Studio, cliquez sur la solution de hello, puis cliquez sur **gérer les Packages NuGet**.
   
    Cela affiche hello **gérer les Packages NuGet** boîte de dialogue.
3. Recherchez `WindowsAzure.Messaging.Managed` et cliquez sur **installer**, puis acceptez les conditions d’utilisation de hello.
   
    ![Visual Studio - Gestionnaire de packages NuGet][20]
   
    Il télécharge, installe et ajoute une bibliothèque de messagerie Azure référence toohello pour Windows à l’aide de hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">package NuGet de WindowsAzure.Messaging.Managed</a>.
4. Ouvrez le fichier de hello App.xaml.cs et ajoutez les éléments suivants de hello `using` instructions :
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. Ajouter hello suivant code haut hello **Application_Launching** méthode dans App.xaml.cs :
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > valeur de Hello **MyPushChannel** est un index qui est utilisé toolookup un canal existant Bonjour [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection. S’il n’y en a aucun, créez une entrée portant ce nom.
   > 
   > 
   
    Assurez-vous que le nom de hello tooinsert de votre chaîne de connexion de concentrateur et hello appelé **DefaultListenSharedAccessSignature** que vous avez obtenu dans la section précédente de hello.
    Ce code récupère l’URI de canal hello pour une application hello de MPNS et inscrit ce canal URI avec votre concentrateur de notification. Elle garantit également que ce canal hello QU'URI est enregistré dans votre concentrateur de notification que chaque application hello de temps est lancée.
   
   > [!NOTE]
   > Ce didacticiel envoie un périphérique toohello de notification toast. Lorsque vous envoyez une notification de vignette, vous devez appeler hello **BindToShellTile** méthode sur le canal de hello. toosupport des notifications toast et vignette, appeler à la fois **BindToShellTile** et **BindToShellToast**.
   > 
   > 
6. Dans l’Explorateur de solutions, développez **propriétés**, ouvrez hello `WMAppManifest.xml` de fichiers, cliquez sur hello **fonctionnalités** onglet et vérifiez que ce hello **ID_CAP_PUSH_NOTIFICATION** fonctionnalité est activée.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. Hello de presse `F5` toorun clé hello application.
   
    Un message d’inscription s’affiche dans l’application hello.
8. Hello fermer l’application.  
   
   > [!NOTE]
   > tooreceive une notification toast, application hello ne doit pas exécuter de premier plan de hello.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>Envoi de notifications Push à partir de votre serveur principal
Vous pouvez envoyer des notifications push à l’aide de concentrateurs de Notification à partir de n’importe quel serveur principal via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a>. Ce didacticiel montre comment envoyer des notifications Push à l’aide d’une application de console .NET. 

Pour obtenir un exemple de comment toosend des notifications push à partir d’un serveur principal ASP.NET WebAPI intégré avec Notification Hubs, consultez [Azure Notification Hubs d’avertir les utilisateurs avec le serveur principal .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).  

Pour obtenir un exemple de comment toosend les notifications push à l’aide de hello [API REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), extraire [comment toouse concentrateurs de Notification à partir de Java](notification-hubs-java-push-notification-tutorial.md) et [comment toouse concentrateurs de Notification à partir de PHP](notification-hubs-php-push-notification-tutorial.md) .

1. Solution de hello avec le bouton droit, sélectionnez **ajouter** et **nouveau projet...** , puis sous **Visual C#**, cliquez sur **Windows** et **Application Console**, puis cliquez sur **OK**.
   
       ![Visual Studio - New Project - Console Application][6]
   
    Cette opération ajoute une nouvelle Visual C# toohello solution d’application console. Vous pouvez également réaliser cette opération dans une solution distincte.
2. Cliquez sur **Outils**, sur **Library Package Manager**, puis sur **Console du gestionnaire de package**.
   
    Cette opération affiche hello Console du Gestionnaire de Package.
3. Bonjour **Package Manager Console** fenêtre, jeu hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.
4. Ouvrez hello `Program.cs` et ajoutez les suivant hello `using` instruction :
   
        using Microsoft.Azure.NotificationHubs;
5. Bonjour `Program` de classe, ajoutez hello suivant de méthode :
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    Assurez-vous que tooreplace hello `<hub name>` espace réservé par nom de hello du hub de notification hello qui apparaît dans le portail de hello. En outre, remplacez espace réservé de chaîne hello connexion avec la chaîne de connexion hello appelé **DefaultFullSharedAccessSignature** que vous avez obtenu dans la section de hello « Configurer votre concentrateur de notification ».
   
   > [!NOTE]
   > Assurez-vous que vous utilisez avec la chaîne de connexion de hello **complète** accéder, pas **écouter** accès. chaîne d’accès à l’écoute de Hello n’a pas de notifications push de toosend autorisations.
   > 
   > 
6. Ajouter hello ligne dans votre `Main` méthode :
   
         SendNotificationAsync();
         Console.ReadLine();
7. Avec votre Windows Phone émulateur en cours d’exécution et votre projet d’application de console application hello fermé, définissez comme hello par défaut du projet de démarrage, puis appuyez sur hello `F5` toorun clé hello application.
   
    Vous recevrez une notification Push toast. En appuyant sur la bannière de toast hello charge application hello.

Vous pouvez trouver toutes les charges utiles de possibles hello Bonjour [catalogue de toast] et [vignette catalogue] rubriques sur MSDN.

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple simple, vous diffusées tooall de notifications push à vos appareils Windows Phone 8. 

Dans l’ordre tootarget des utilisateurs spécifiques, consultez toohello [utiliser Notification Hubs toopush notifications toousers] didacticiel. 

Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez lire [toosend utiliser Notification Hubs actualités]. 

En savoir plus sur la façon toouse Notification Hubs dans [des conseils de concentrateurs de Notification].

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express pour Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[des conseils de concentrateurs de Notification]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[utiliser Notification Hubs toopush notifications toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend utiliser Notification Hubs actualités]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[catalogue de toast]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[vignette catalogue]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs - didacticiel de Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

