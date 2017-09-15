<span data-ttu-id="e4843-101">Dans cette section, vous mettez à jour le code dans votre projet de serveur principal Mobile Apps existant pour envoyer une notification Push chaque fois qu’un nouvel élément est ajouté.</span><span class="sxs-lookup"><span data-stu-id="e4843-101">In this section, you update code in your existing Mobile Apps back-end project to send a push notification every time a new item is added.</span></span> <span data-ttu-id="e4843-102">Cette opération est rendue possible par la fonctionnalité [modèle](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) d’Azure Notification Hubs, qui autorise l’envoi de notifications Push multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="e4843-102">This is powered by the [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="e4843-103">Les différents clients sont inscrits pour les notifications Push à l’aide de modèles, et une notification Push universelle unique peut accéder à toutes les plates-formes clientes.</span><span class="sxs-lookup"><span data-stu-id="e4843-103">The various clients are registered for push notifications using templates, and a single universal push can get to all client platforms.</span></span>

<span data-ttu-id="e4843-104">Choisissez l’une des procédures ci-après correspondant au type de votre projet de serveur principal &mdash; [projet de serveur principal .NET](#dotnet) ou [projet de serveur principal Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="e4843-104">Choose one of the following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="e4843-105"><a name="dotnet"></a>Projet de serveur principal .NET</span><span class="sxs-lookup"><span data-stu-id="e4843-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="e4843-106">Dans Visual Studio, cliquez avec le bouton droit sur le projet de serveur, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e4843-106">In Visual Studio, right-click the server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="e4843-107">Recherchez `Microsoft.Azure.NotificationHubs`, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="e4843-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="e4843-108">Cette opération installe la bibliothèque Notification Hubs pour l’envoi de notifications à partir de votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4843-108">This installs the Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="e4843-109">Dans le projet de serveur, ouvrez **Contrôleurs** > **TodoItemController.cs** et ajoutez les instructions using suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4843-109">In the server project, open **Controllers** > **TodoItemController.cs**, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="e4843-110">Dans la méthode **PostTodoItem**, ajoutez le code suivant après l’appel à **InsertAsync** :</span><span class="sxs-lookup"><span data-stu-id="e4843-110">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>  

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending the message so that all template registrations that contain "messageParam"
        // will receive the notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added to the list.";

        try
        {
            // Send the push notification and log the results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="e4843-111">Une notification de modèle contenant item.Text est ensuite envoyée quand un nouvel élément est inséré.</span><span class="sxs-lookup"><span data-stu-id="e4843-111">This sends a template notification that contains the item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="e4843-112">Publier à nouveau le projet de serveur</span><span class="sxs-lookup"><span data-stu-id="e4843-112">Republish the server project.</span></span>

### <span data-ttu-id="e4843-113"><a name="nodejs"></a>Projet de serveur principal Node.js</span><span class="sxs-lookup"><span data-stu-id="e4843-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="e4843-114">Si vous ne l’avez pas encore fait, [téléchargez le projet de serveur principal de démarrage rapide](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) ou utilisez [l’éditeur en ligne du Portail Azure](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="e4843-114">If you haven't already done so, [download the quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="e4843-115">Remplacez le code présent dans todoitem.js par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="e4843-115">Replace the existing code in todoitem.js with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="e4843-116">Une notification de modèle contenant item.Text est ensuite envoyée quand un nouvel élément est inséré.</span><span class="sxs-lookup"><span data-stu-id="e4843-116">This sends a template notification that contains the item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="e4843-117">Quand vous modifiez le fichier sur votre ordinateur local, republiez le projet serveur.</span><span class="sxs-lookup"><span data-stu-id="e4843-117">When editing the file on your local computer, republish the server project.</span></span>
