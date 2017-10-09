Dans cette section, vous mettez à jour code dans votre toosend de projet de serveur principal Mobile Apps existant une notification push chaque fois qu’un nouvel élément est ajouté. Il est alimenté par hello [modèle](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) fonctionnalité d’Azure Notification Hubs, l’activation de push d’inter-plateformes. différents clients Hello sont inscrits pour les notifications push à l’aide de modèles, et un push universels unique peut obtenir tooall plates-formes clientes.

Choisissez une des hello procédures suivantes qui correspond à votre type de projet de serveur principal&mdash;soit [.NET back-end](#dotnet) ou [Node.js back-end](#nodejs).

### <a name="dotnet"></a>Projet de serveur principal .NET
1. Dans Visual Studio, cliquez sur le projet de serveur hello et cliquez sur **gérer les Packages NuGet**. Recherchez `Microsoft.Azure.NotificationHubs`, puis cliquez sur **Installer**. Bibliothèque de concentrateurs de Notification hello pour envoyer des notifications à partir de votre serveur principal sont ainsi installés.
2. Dans le projet de serveur hello, ouvrez **contrôleurs** > **TodoItemController.cs**et ajoutez hello qui suit à l’aide des instructions :

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

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Envoie une notification de modèle qui contient l’élément de hello. Texte lorsqu’un nouvel élément est inséré.
4. Publiez de nouveau projet de serveur hello.

### <a name="nodejs"></a>Projet de serveur principal Node.js
1. Si vous n’avez pas déjà fait, [télécharger hello quickstart principal projet](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), ou sinon utilisez hello [éditeur en ligne Bonjour Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Remplacez le code existant dans todoitem.js hello suivant de hello :

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
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

    Envoie une notification de modèle qui contient les item.text hello lorsqu’un nouvel élément est inséré.
3. Lorsque vous modifiez le fichier hello sur votre ordinateur local, le projet de serveur hello republier.
