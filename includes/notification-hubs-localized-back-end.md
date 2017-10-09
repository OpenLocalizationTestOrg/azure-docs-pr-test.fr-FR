



Lorsque vous envoyez des notifications de modèle que vous ne devez tooprovide un ensemble de propriétés, dans notre cas nous envoie hello jeu de propriétés contenant version localisée de hello de news en cours de hello, par exemple :

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


Cette section montre comment les notifications de toosend à l’aide d’une application console

Hello inclus code diffusions tooboth Windows Store et les appareils iOS, étant donné que hello principal peut diffuser tooany de périphériques de hello pris en charge.

### <a name="toosend-notifications-using-a-c-console-app"></a>notifications de toosend à l’aide d’une application console c#
Modifier hello `SendTemplateNotificationAsync` méthode dans une application de console hello vous avez créé précédemment par hello suivant de code. Notez que dans ce cas il est sans toosend besoin de plusieurs notifications pour les plateformes et des paramètres régionaux différents.

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


Notez que cet appel simple fournira élément localisée hello news trop**tous les** vos appareils, quel que soit la plateforme de hello, comme votre concentrateur de Notification conçoit et livre hello correct inscrit des appareils de charge utile native tooall hello tooa de balise spécifique.

### <a name="sending-hello-notification-with-mobile-services"></a>Envoi de notification hello avec les Services mobiles
Dans le Planificateur de votre Service Mobile, vous pouvez utiliser hello script suivant :

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


