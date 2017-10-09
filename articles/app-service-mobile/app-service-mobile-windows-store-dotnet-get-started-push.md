---
title: application de plateforme Windows universelle (UWP) aaaAdd push notifications tooyour | Documents Microsoft
description: "Découvrez comment toouse Azure App Service Mobile Apps et Azure Notification Hubs toosend push application de plateforme Windows universelle (UWP) tooyour des notifications."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a>Ajouter une application Windows de push notifications tooyour
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Vue d'ensemble
Dans ce didacticiel, vous allez ajouter toohello de notifications push [démarrage rapide Windows](app-service-mobile-windows-store-dotnet-get-started.md) projet afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.

Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez serez hello package d’extension de notification push. Consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.

## <a name="configure-hub"></a>Configurer un nouveau hub de notification
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>Inscription de votre application pour les notifications Push
Vous devez toosubmit votre toohello d’application du Windows Store, puis configurez votre toointegrate de project server avec les Services de Notification de Windows (WNS) toosend push.

1. Dans l’Explorateur de solutions Visual Studio, projet d’application hello UWP avec le bouton droit, cliquez sur **magasin** > **associer application hello Store...** .

    ![Associer une application au Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. Dans l’Assistant de hello, cliquez sur **suivant**, connectez-vous avec votre compte Microsoft, tapez un nom pour votre application dans **réserver un nouveau nom de l’application**, puis cliquez sur **réserve**.
3. Une fois l’inscription d’une application hello nouveau nom d’application a été créé correctement, sélectionnez hello, cliquez sur **suivant**, puis cliquez sur **associer**. Cela ajoute le manifeste d’application d’enregistrement d’informations toohello hello requis du Windows Store.  
4. Accédez toohello [centre de développement Windows](https://dev.windows.com/en-us/overview), connectez-vous avec votre compte Microsoft, cliquez sur nouvelle inscription d’application hello dans **mes applications**, puis développez **Services**  >  **Des notifications push**.
5. Bonjour **des notifications Push** , cliquez sur **site des Services Live** sous **Microsoft Azure Mobile Services**.
6. Dans la page d’inscription de hello, prenez note de la valeur hello sous **secrets d’Application** et hello **SID du Package**, qui vous allez ensuite utiliser tooconfigure service principal de votre application mobile.

    ![Associer une application au Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > question secrète du client Hello et le SID du package sont des informations d’identification de sécurité importantes. Ne partagez pas ces valeurs avec quiconque et ne les distribuez pas avec votre application. Hello **Id d’Application** est utilisé avec l’authentification de Microsoft Account hello tooconfigure secret principal.
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>Configurer les notifications de push toosend hello principal
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>Mettre à jour des notifications push de hello server toosend
Utilisez hello procédure ci-dessous qui correspond à votre type de projet principal&mdash;soit [service principal .NET](#dotnet) ou [Node.js principal](#nodejs).

### <a name="dotnet"></a>Projet de serveur principal .NET
1. Dans Visual Studio, cliquez sur le projet de serveur hello et cliquez sur **gérer les Packages NuGet**, recherchez Microsoft.Azure.NotificationHubs, puis cliquez sur **installer**. Bibliothèque cliente de concentrateurs de Notification hello sont ainsi installés.
2. Développez **contrôleurs**, ouvrez TodoItemController.cs et ajoutez hello qui suit à l’aide des instructions :

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. Bonjour **PostTodoItem** (méthode), ajouter hello suivant code après appel de hello trop**InsertAsync**:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Ce code indique à hello notification hub toosend une notification une fois un nouvel élément de l’insertion.
4. Publiez de nouveau projet de serveur hello.

### <a name="nodejs"></a>Projet de back-end Node.js
1. Si vous n’avez pas déjà fait, [télécharger le projet de démarrage rapide de hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) ou sinon utilisez hello [éditeur en ligne Bonjour Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Remplacez le code existant dans le fichier de todoitem.js hello hello suivant de hello :

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    Envoie une notification toast WNS contenant hello item.text lors de l’insertion d’un nouvel élément de tâche.
3. Lorsque vous modifiez le fichier hello sur votre ordinateur local, le projet de serveur hello republier.

## <a id="update-app"></a>Ajouter une application de tooyour de notifications push
Ensuite, votre application doit s’inscrire pour les notifications Push au démarrage. Lorsque vous avez déjà activé l’authentification, assurez-vous que l’utilisateur hello se connecte en avant d’essayer de tooregister pour les notifications push.

1. Ouvrez hello **App.xaml.cs** fichier projet et ajoutez hello suit `using` instructions :

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. Dans hello du même fichier, ajoutez hello **InitNotificationsAsync** toohello de définition de méthode **application** classe :

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    Ce code récupère hello ChannelURI pour l’application hello WNS et inscrit ce ChannelURI avec votre application de Service d’applications mobiles.
3. En haut de hello Hello **OnLaunched** Gestionnaire d’événements dans **App.xaml.cs**, ajouter hello **async** définition de méthode modificateur toohello et ajoutez suivant de hello appeler denouveautoohello **InitNotificationsAsync** méthode, comme dans hello l’exemple suivant :

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    Cela garantit que hello que channeluri de courte durée de vie est enregistré à chaque lancement de l’application hello.
4. Recréez votre projet d’application UWP. Votre application est maintenant prêt tooreceive des notifications de toast.

## <a id="test"></a>Tester les notifications push dans votre application
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>Étapes suivantes
Apprenez-en plus sur les notifications Push :

* [Comment toouse hello gérées client pour les applications mobiles Azure](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  Les modèles vous permettent de push de flexibilité toosend inter-plateformes et push localisée. Découvrez comment tooregister modèles.
* [Diagnostiquer les problèmes de notification Push](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Il existe différentes raisons pour lesquelles les notifications peuvent être perdues ou n’arrivent pas sur les appareils. Cette rubrique vous montre comment tooanalyze et déterminer la racine de hello provoquent des erreurs de notification push.

Envisagez de continuer sur tooone Hello suivant didacticiels :

* [Ajouter une application de tooyour d’authentification](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Découvrez comment tooauthenticate les utilisateurs de votre application avec un fournisseur d’identité.
* [Activer la synchronisation hors connexion pour votre application](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Découvrez comment tooadd hors connexion prennent en charge votre application à l’aide d’un serveur principal de l’application Mobile. Synchronisation hors connexion permet de toointeract les utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau.

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
