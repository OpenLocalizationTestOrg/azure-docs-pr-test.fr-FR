



<span data-ttu-id="4df02-101">Lorsque vous envoyez des notifications de modèle que vous ne devez tooprovide un ensemble de propriétés, dans notre cas nous envoie hello jeu de propriétés contenant version localisée de hello de news en cours de hello, par exemple :</span><span class="sxs-lookup"><span data-stu-id="4df02-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="4df02-102">Cette section montre comment les notifications de toosend à l’aide d’une application console</span><span class="sxs-lookup"><span data-stu-id="4df02-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="4df02-103">Hello inclus code diffusions tooboth Windows Store et les appareils iOS, étant donné que hello principal peut diffuser tooany de périphériques de hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4df02-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="4df02-104">notifications de toosend à l’aide d’une application console c#</span><span class="sxs-lookup"><span data-stu-id="4df02-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="4df02-105">Modifier hello `SendTemplateNotificationAsync` méthode dans une application de console hello vous avez créé précédemment par hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="4df02-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="4df02-106">Notez que dans ce cas il est sans toosend besoin de plusieurs notifications pour les plateformes et des paramètres régionaux différents.</span><span class="sxs-lookup"><span data-stu-id="4df02-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


<span data-ttu-id="4df02-107">Notez que cet appel simple fournira élément localisée hello news trop**tous les** vos appareils, quel que soit la plateforme de hello, comme votre concentrateur de Notification conçoit et livre hello correct inscrit des appareils de charge utile native tooall hello tooa de balise spécifique.</span><span class="sxs-lookup"><span data-stu-id="4df02-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="4df02-108">Envoi de notification hello avec les Services mobiles</span><span class="sxs-lookup"><span data-stu-id="4df02-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="4df02-109">Dans le Planificateur de votre Service Mobile, vous pouvez utiliser hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="4df02-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


