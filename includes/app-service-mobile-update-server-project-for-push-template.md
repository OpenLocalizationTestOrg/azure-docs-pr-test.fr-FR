<span data-ttu-id="42dde-101">Dans cette section, vous mettez à jour code dans votre toosend de projet de serveur principal Mobile Apps existant une notification push chaque fois qu’un nouvel élément est ajouté.</span><span class="sxs-lookup"><span data-stu-id="42dde-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="42dde-102">Il est alimenté par hello [modèle](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) fonctionnalité d’Azure Notification Hubs, l’activation de push d’inter-plateformes.</span><span class="sxs-lookup"><span data-stu-id="42dde-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="42dde-103">différents clients Hello sont inscrits pour les notifications push à l’aide de modèles, et un push universels unique peut obtenir tooall plates-formes clientes.</span><span class="sxs-lookup"><span data-stu-id="42dde-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="42dde-104">Choisissez une des hello procédures suivantes qui correspond à votre type de projet de serveur principal&mdash;soit [.NET back-end](#dotnet) ou [Node.js back-end](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="42dde-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="42dde-105"><a name="dotnet"></a>Projet de serveur principal .NET</span><span class="sxs-lookup"><span data-stu-id="42dde-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="42dde-106">Dans Visual Studio, cliquez sur le projet de serveur hello et cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="42dde-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="42dde-107">Recherchez `Microsoft.Azure.NotificationHubs`, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="42dde-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="42dde-108">Bibliothèque de concentrateurs de Notification hello pour envoyer des notifications à partir de votre serveur principal sont ainsi installés.</span><span class="sxs-lookup"><span data-stu-id="42dde-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="42dde-109">Dans le projet de serveur hello, ouvrez **contrôleurs** > **TodoItemController.cs**et ajoutez hello qui suit à l’aide des instructions :</span><span class="sxs-lookup"><span data-stu-id="42dde-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="42dde-110">Bonjour **PostTodoItem** (méthode), ajouter hello suivant code après appel de hello trop**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="42dde-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

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

    <span data-ttu-id="42dde-111">Envoie une notification de modèle qui contient l’élément de hello. Texte lorsqu’un nouvel élément est inséré.</span><span class="sxs-lookup"><span data-stu-id="42dde-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="42dde-112">Publiez de nouveau projet de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="42dde-112">Republish hello server project.</span></span>

### <span data-ttu-id="42dde-113"><a name="nodejs"></a>Projet de serveur principal Node.js</span><span class="sxs-lookup"><span data-stu-id="42dde-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="42dde-114">Si vous n’avez pas déjà fait, [télécharger hello quickstart principal projet](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), ou sinon utilisez hello [éditeur en ligne Bonjour Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="42dde-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="42dde-115">Remplacez le code existant dans todoitem.js hello suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="42dde-115">Replace hello existing code in todoitem.js with hello following:</span></span>

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

    <span data-ttu-id="42dde-116">Envoie une notification de modèle qui contient les item.text hello lorsqu’un nouvel élément est inséré.</span><span class="sxs-lookup"><span data-stu-id="42dde-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="42dde-117">Lorsque vous modifiez le fichier hello sur votre ordinateur local, le projet de serveur hello republier.</span><span class="sxs-lookup"><span data-stu-id="42dde-117">When editing hello file on your local computer, republish hello server project.</span></span>
