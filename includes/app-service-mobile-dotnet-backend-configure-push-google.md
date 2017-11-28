<span data-ttu-id="b5013-101">Utilisez la procédure ci-dessous correspondant à votre type de projet de serveur principal &mdash; [serveur principal .NET](#dotnet) ou [serveur principal Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="b5013-101">Use the procedure that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="b5013-102"><a name="dotnet"></a>Projet de serveur principal .NET</span><span class="sxs-lookup"><span data-stu-id="b5013-102"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="b5013-103">Dans Visual Studio, cliquez avec le bouton droit sur le projet de serveur, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b5013-103">In Visual Studio, right-click the server project, and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="b5013-104">Recherchez `Microsoft.Azure.NotificationHubs`, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="b5013-104">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="b5013-105">Cette commande installe la bibliothèque cliente Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="b5013-105">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="b5013-106">Dans le dossier Contrôleurs, ouvrez TodoItemController.cs et ajoutez les instructions `using` suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5013-106">In the Controllers folder, open TodoItemController.cs and add the following `using` statements:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. <span data-ttu-id="b5013-107">Remplacez la méthode `PostTodoItem` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="b5013-107">Replace the `PostTodoItem` method with the following code:</span></span>  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
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

            // Android payload
            var androidNotificationPayload = "{ \"data\" : {\"message\":\"" + item.Text + "\"}}";

            try
            {
                // Send the push notification and log the results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write the success result to the logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write the failure result to the logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. <span data-ttu-id="b5013-108">Publier à nouveau le projet de serveur</span><span class="sxs-lookup"><span data-stu-id="b5013-108">Republish the server project.</span></span>

### <span data-ttu-id="b5013-109"><a name="nodejs"></a>Projet de serveur principal Node.js</span><span class="sxs-lookup"><span data-stu-id="b5013-109"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="b5013-110">Si vous ne l’avez pas encore fait, [téléchargez le projet de démarrage rapide](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) ou utilisez [l’éditeur en ligne du Portail Azure](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="b5013-110">If you haven't already done so, [download the quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="b5013-111">Remplacez le code présent dans le fichier todoitem.js par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="b5013-111">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
                if (context.push) {
                    // Send a GCM native notification.
                    context.push.gcm.send(null, payload, function (error) {
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

    <span data-ttu-id="b5013-112">Ce code envoie une notification GCM contenant item.text quand un nouvel élément todo est inséré.</span><span class="sxs-lookup"><span data-stu-id="b5013-112">This sends a GCM notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="b5013-113">Quand vous modifiez le fichier sur votre ordinateur local, republiez le projet serveur.</span><span class="sxs-lookup"><span data-stu-id="b5013-113">When editing the file in your local computer, republish the server project.</span></span>
