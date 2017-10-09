
<span data-ttu-id="d71ff-101">Cette section montre comment toosend dernières actualités comme marquées notifications de modèle à partir d’une application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="d71ff-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="d71ff-102">Si vous utilisez des applications mobiles, consultez toohello [ajouter des notifications de push pour les applications mobiles] didacticiel et sélectionner votre plateforme haut hello.</span><span class="sxs-lookup"><span data-stu-id="d71ff-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="d71ff-103">Si vous souhaitez toouse Java ou PHP font référence trop[comment toouse concentrateurs de Notification à partir de Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="d71ff-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="d71ff-104">Vous pouvez envoyer des notifications à partir d’un serveur principal à l’aide de [l’interface REST des Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="d71ff-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="d71ff-105">Ignorez les étapes 1 à 3 Si vous avez créé l’application de console hello pour envoyer des notifications lorsque vous avez rempli [prise en main des concentrateurs de Notification].</span><span class="sxs-lookup"><span data-stu-id="d71ff-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="d71ff-106">Dans Visual Studio, créez une application console Visual C# :</span><span class="sxs-lookup"><span data-stu-id="d71ff-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="d71ff-107">Dans le menu principal de hello Visual Studio, cliquez sur **outils**, **Gestionnaire de Package de bibliothèque**, et **Package Manager Console**, puis dans la fenêtre de console hello tapez la commande suivante et appuyez sur **Entrez**:</span><span class="sxs-lookup"><span data-stu-id="d71ff-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="d71ff-108">Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello [package NuGet de concentrateurs Microsoft.Azure.Notification].</span><span class="sxs-lookup"><span data-stu-id="d71ff-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="d71ff-109">Ouvrez le fichier de hello Program.cs et ajoutez les éléments suivants de hello `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="d71ff-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="d71ff-110">Bonjour `Program` classe, ajouter hello suivant de méthode ou remplacez-le si elle existe déjà :</span><span class="sxs-lookup"><span data-stu-id="d71ff-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
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
   
    <span data-ttu-id="d71ff-111">Ce code envoie une notification de modèle pour chacun des balises de six hello dans le tableau de chaînes hello.</span><span class="sxs-lookup"><span data-stu-id="d71ff-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="d71ff-112">utilisation de Hello de balises permet de s’assurer que les appareils reçoivent des notifications uniquement pour les catégories de hello inscrit.</span><span class="sxs-lookup"><span data-stu-id="d71ff-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="d71ff-113">Bonjour au-dessus de code, remplacez hello `<hub name>` et `<connection string with full access>` des espaces réservés avec votre notification hub hello et nom de chaîne de connexion pour *DefaultFullSharedAccessSignature* à partir du tableau de bord hello de votre concentrateur de notification .</span><span class="sxs-lookup"><span data-stu-id="d71ff-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="d71ff-114">Ajouter des lignes Bonjour suivantes de hello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="d71ff-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="d71ff-115">Générez l’application de console hello.</span><span class="sxs-lookup"><span data-stu-id="d71ff-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[prise en main des concentrateurs de Notification]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[l’interface REST des Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[ajouter des notifications de push pour les applications mobiles]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[comment toouse concentrateurs de Notification à partir de Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[package NuGet de concentrateurs Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
