---
title: "aaaGet main d’Azure Notification Hubs pour les applications Windows universelles plateforme | Documents Microsoft"
description: Dans ce didacticiel, vous apprendrez comment toouse Azure Notification Hubs toopush notifications tooa application de plateforme universelle Windows.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Prise en main de Notification Hubs pour les applications de plateforme Windows universelle
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application de plateforme Windows universelle (UWP) tooa des notifications.

Dans ce didacticiel, vous créez une application du Windows Store vide qui reçoit des notifications push à l’aide de hello services de notifications Push Windows (WNS). Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution.

## <a name="before-you-begin"></a>Avant de commencer
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

code Hello terminée pour ce didacticiel se trouve sur GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).

## <a name="prerequisites"></a>Composants requis
Ce didacticiel requiert hello qui suit :

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) ou version ultérieure
* [Outils de développement d’applications Windows universelles installés](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* Un compte Azure actif  <br/>Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).
* Un compte Windows Store actif

Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Notification Hubs pour les applications de plateforme Windows universelle.

## <a name="register-your-app-for-hello-windows-store"></a>Inscrire votre application pour hello du Windows Store
applications de tooUWP toosend push notifications, vous devez associer votre toohello d’application du Windows Store. Vous devez ensuite configurer votre toointegrate de concentrateur de notification avec WNS.

1. Si vous n’avez pas encore inscrit votre application, accédez à toohello [centre de développement Windows](https://dev.windows.com/overview), connectez-vous avec votre compte Microsoft, puis cliquez sur **créer une application**.

2. Saisissez un nom pour votre application et cliquez sur **Réserver le nom d’application**. La nouvelle inscription au Windows Store pour votre application est créée.

3. Dans Visual Studio, créez un projet de Visual C# applications du Windows Store à l’aide de hello Windows universel **application vide** modèle et cliquez sur **OK**.

4. Acceptez les valeurs par défaut de hello pour cible de hello et les versions de plateforme minimales.

5. Dans l’Explorateur de solutions, projet d’application hello du Windows Store avec le bouton droit, cliquez sur **magasin**, puis cliquez sur **associer application hello Store...** . hello **associer votre application du Windows Store de hello** Assistant s’affiche.

6. Dans l’Assistant de hello, connectez-vous avec votre compte Microsoft.

7. Cliquez sur l’application hello que vous avez enregistré à l’étape 2, cliquez sur **suivant**, puis cliquez sur **associer**. Cela ajoute le manifeste d’application d’enregistrement d’informations toohello hello requis du Windows Store.

8. Retour sur hello [centre de développement Windows](http://dev.windows.com/overview) pour votre nouvelle application, cliquez sur **Services**, cliquez sur **des notifications Push**, puis cliquez sur **WNS/MPNS**.

9. Cliquez sur **Nouvelle notification**.

10. Cliquez sur le modèle **Blank (Toast)** (Vide (Toast), puis sur **OK**.

11. Saisissez un **nom** et un message de **contexte** Visual pour la notification. Cliquez ensuite sur **Enregistrer en tant que brouillon**.

12. Accédez toohello [portail de l’enregistrement d’Application](http://apps.dev.microsoft.com) et connectez-vous.

13. Cliquez sur le nom de votre application. Prenez note de hello **Secret d’Application** hello et le mot de passe **Package SID (security identifier)** situé dans hello **du Windows Store** paramètres de plateforme.

     > [AZURE.WARNING]
    secret d’application Hello et le SID du package sont des informations d’identification de sécurité importantes. Ne partagez pas ces valeurs avec quiconque et ne les distribuez pas avec votre application.

## <a name="configure-your-notification-hub"></a>Configuration de votre hub de notification
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Sélectionnez hello <b>Notification Services</b> option et hello <b>Windows (WNS)</b> option. Puis entrez hello <b>secret d’Application</b> mot de passe dans hello <b>clé de sécurité</b> champ. Entrez votre <b>SID du Package</b> valeur obtenue à partir de WNS dans la section précédente de hello, puis cliquez sur <b>enregistrer</b>.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

Votre concentrateur de notification est maintenant configuré toowork avec WNS, et vous avez tooregister de chaînes de connexion hello votre application et envoyez des notifications.

## <a name="connect-your-app-toohello-notification-hub"></a>Se connecter à votre hub de notification d’application toohello
1. Dans Visual Studio, cliquez sur la solution de hello, puis cliquez sur **gérer les Packages NuGet**.
   
    Cela affiche hello **gérer les Packages NuGet** boîte de dialogue.
2. Recherchez `WindowsAzure.Messaging.Managed` et cliquez sur **installer**et acceptez les conditions d’utilisation de hello.
   
    ![][20]
   
    Il télécharge, installe et ajoute une bibliothèque de messagerie Azure référence toohello pour Windows à l’aide de hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">package NuGet de WindowsAzure.Messaging.Managed</a>.
3. Ouvrez le fichier de projet App.xaml.cs hello et ajoutez hello suit `using` instructions. 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. Également, dans App.xaml.cs, ajoutez le code suivant de hello **InitNotificationsAsync** toohello de définition de méthode **application** classe :
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    Ce code récupère les URI de canal hello pour une application hello WNS et inscrit ce canal URI avec votre concentrateur de notification.
   
   > [!NOTE]
   > Assurez-vous que tooreplace hello espace réservé de « nom de votre concentrateur » avec le nom hello du concentrateur de notification hello qui s’affiche dans hello portail Azure. Remplacez également espace réservé chaîne de connexion hello hello **DefaultListenSharedAccessSignature** chaîne de connexion que vous avez obtenue à partir de hello **stratégies d’accès** page de votre concentrateur de Notification dans un section précédente.
   > 
   > 
5. En haut de hello Hello **OnLaunched** Gestionnaire d’événements dans App.xaml.cs, ajouter hello suivant toohello appel nouvelle **InitNotificationsAsync** méthode :
   
        InitNotificationsAsync();
   
    Cela garantit ce canal hello QU'URI est enregistré dans votre concentrateur de notification que chaque application hello de temps est lancée.
6. Hello de presse **F5** toorun clé hello application. Une boîte de dialogue contextuelle qui contient la clé d’inscription de hello s’affiche.

Votre application est maintenant prêt tooreceive des notifications de toast.

## <a name="send-notifications"></a>Envoi de notifications
Vous pouvez tester rapidement la réception de notifications dans votre application en envoyant des notifications Bonjour [Azure Portal](https://portal.azure.com/) à l’aide de hello **envoi Test** bouton sur le concentrateur de notification hello, comme indiqué dans l’écran hello ci-dessous.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible. Vous pouvez également utiliser les API REST de hello directement les messages de notification de toosend si une bibliothèque n’est pas disponible pour votre serveur principal. 

Dans ce didacticiel, nous plus de simplicité et simplement montrent le test de votre application cliente en envoyant des notifications à l’aide de hello SDK .NET pour les concentrateurs de notification dans une application console à la place d’un service principal. Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers] didacticiel en tant qu’étape suivante de hello pour envoyer des notifications à partir d’un serveur principal d’ASP.NET. Toutefois, hello méthodes suivantes peut servir pour envoyer des notifications :

* **Interface REST**: peut prendre en charge notification sur toute plateforme principale à l’aide de hello [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Kit de développement logiciel Microsoft Azure Notification Hubs .NET**: Bonjour Gestionnaire de Package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [comment toouse concentrateurs de Notification à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Azure Mobile Apps**: pour obtenir un exemple de notifications toosend à partir d’une application Mobile Azure qui est intégré avec Notification Hubs, consultez [ajouter des notifications de push pour les applications mobiles](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: pour obtenir un exemple de comment toosend des notifications à l’aide de hello API REST, consultez « Comment toouse concentrateurs de Notification à partir de Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(Facultatif) Envoi de notifications à partir d’une application de console
toosend des notifications à l’aide d’une application console .NET procédez comme suit. 

1. Solution de hello avec le bouton droit, sélectionnez **ajouter** et **nouveau projet...** , puis sous **Visual C#**, cliquez sur **Windows** et **Application Console**, puis cliquez sur **OK**.
   
    Cette opération ajoute une nouvelle Visual C# toohello solution d’application console. Vous pouvez également réaliser cette opération dans une solution distincte.

2. Dans Visual Studio, cliquez successivement sur **Outils**, **Gestionnaire de package NuGet** et **Console du gestionnaire de package**.
   
    Cela affiche hello Package Manager Console dans Visual Studio.
3. Dans la fenêtre de Console du Gestionnaire de Package de hello, définissez hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Ouvrez le fichier Program.cs de hello et ajoutez hello suit `using` instruction :
   
        using Microsoft.Azure.NotificationHubs;
5. Bonjour **programme** de classe, ajoutez hello suivant de méthode :
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > Assurez-vous que vous utilisez chaîne de connexion hello a **complète** accéder, pas **écouter** accès. chaîne d’accès à l’écoute de Hello n’a pas de notifications de toosend d’autorisations.
   > 
   > 
6. Ajouter des lignes Bonjour suivantes de hello **Main** méthode :
   
         SendNotificationAsync();
         Console.ReadLine();
7. Cliquez sur le projet d’application console hello dans Visual Studio, puis cliquez sur **définir comme projet de démarrage** tooset en tant que projet de démarrage hello. Appuyez sur hello **F5** application hello de toorun de clé.
   
    Vous recevrez une notification toast sur tous les appareils enregistrés. Bannière de toast hello cliquant ou appuyant sur charge application hello.

Vous pouvez trouver toutes les charges utiles de hello pris en charge dans hello [catalogue de toast], [vignette catalogue], et [vue d’ensemble de badge] rubriques sur MSDN.

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple simple, vous avez envoyé notifications diffusion tooall vos appareils Windows à l’aide du portail de hello ou une application console. Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers] didacticiel en tant qu’étape suivante de hello. Il va vous montrer comment les notifications toosend à partir d’un serveur principal ASP.NET à l’aide de balises tootarget des utilisateurs spécifiques.

Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, consultez [toosend utiliser Notification Hubs actualités]. 

toolearn plus d’informations sur les concentrateurs de Notification, consultez [des conseils de concentrateurs de Notification](notification-hubs-push-notification-overview.md).

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[utiliser Notification Hubs toopush notifications toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend utiliser Notification Hubs actualités]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[catalogue de toast]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[vignette catalogue]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[vue d’ensemble de badge]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
