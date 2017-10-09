
Cette section montre comment toosend dernières actualités comme marquées notifications de modèle à partir d’une application de console .NET.

Si vous utilisez des applications mobiles, consultez toohello [ajouter des notifications de push pour les applications mobiles] didacticiel et sélectionner votre plateforme haut hello.

Si vous souhaitez toouse Java ou PHP font référence trop[comment toouse concentrateurs de Notification à partir de Java/PHP]. Vous pouvez envoyer des notifications à partir d’un serveur principal à l’aide de [l’interface REST des Notification Hubs].

Ignorez les étapes 1 à 3 Si vous avez créé l’application de console hello pour envoyer des notifications lorsque vous avez rempli [prise en main des concentrateurs de Notification].

1. Dans Visual Studio, créez une application console Visual C# :
   
       ![][13]
2. Dans le menu principal de hello Visual Studio, cliquez sur **outils**, **Gestionnaire de Package de bibliothèque**, et **Package Manager Console**, puis dans la fenêtre de console hello tapez la commande suivante et appuyez sur **Entrez**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello [package NuGet de concentrateurs Microsoft.Azure.Notification].
3. Ouvrez le fichier de hello Program.cs et ajoutez les éléments suivants de hello `using` instruction :
   
        using Microsoft.Azure.NotificationHubs;
4. Bonjour `Program` classe, ajouter hello suivant de méthode ou remplacez-le si elle existe déjà :
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    Ce code envoie une notification de modèle pour chacun des balises de six hello dans le tableau de chaînes hello. utilisation de Hello de balises permet de s’assurer que les appareils reçoivent des notifications uniquement pour les catégories de hello inscrit.
5. Bonjour au-dessus de code, remplacez hello `<hub name>` et `<connection string with full access>` des espaces réservés avec votre notification hub hello et nom de chaîne de connexion pour *DefaultFullSharedAccessSignature* à partir du tableau de bord hello de votre concentrateur de notification .
6. Ajouter des lignes Bonjour suivantes de hello **Main** méthode :
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Générez l’application de console hello.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[prise en main des concentrateurs de Notification]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[l’interface REST des Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[ajouter des notifications de push pour les applications mobiles]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[comment toouse concentrateurs de Notification à partir de Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[package NuGet de concentrateurs Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
