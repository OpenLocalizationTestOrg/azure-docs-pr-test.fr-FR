
<span data-ttu-id="5ec71-101">Cette section montre comment envoyer les dernières nouvelles sous forme de notifications modèles avec balises à partir de l’application console .NET.</span><span class="sxs-lookup"><span data-stu-id="5ec71-101">This section shows how to send breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="5ec71-102">Si vous utilisez Mobile Apps, reportez-vous au didacticiel [Add push notifications for Mobile Apps] (Ajouter des notifications Push pour Mobile Apps).</span><span class="sxs-lookup"><span data-stu-id="5ec71-102">If you are using Mobile Apps please refer to the [Add push notifications for Mobile Apps] tutorial and select your platform at the top.</span></span>

<span data-ttu-id="5ec71-103">Si vous souhaitez utiliser Java ou PHP, consultez la rubrique [How to use Notification Hubs from Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="5ec71-103">If you want to use Java or PHP refer to [How to use Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="5ec71-104">Vous pouvez envoyer des notifications à partir d’un serveur principal à l’aide de [l’interface REST des Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="5ec71-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="5ec71-105">Ignorez les étapes 1 à 3 si vous avez créé l’application de console pour l’envoi des notifications lorsque vous avez effectué la [prise en main des Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="5ec71-105">Skip steps 1-3 if you created the console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="5ec71-106">Dans Visual Studio, créez une application console Visual C# :</span><span class="sxs-lookup"><span data-stu-id="5ec71-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="5ec71-107">Dans le menu principal de Visual Studio, cliquez sur **Outils**, **Gestionnaire de package de bibliothèques** et **Console du gestionnaire de package**, puis dans la fenêtre de la console, tapez la ligne suivante et appuyez sur **Entrée** :</span><span class="sxs-lookup"><span data-stu-id="5ec71-107">In the Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in the console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="5ec71-108">Cette opération ajoute une référence au Kit de développement logiciel (SDK) Azure Notification Hubs à l’aide du [package NuGet Microsoft.Azure.Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="5ec71-108">This adds a reference to the Azure Notification Hubs SDK using the [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="5ec71-109">Ouvrez le fichier Program.cs et ajoutez l’instruction `using` suivante :</span><span class="sxs-lookup"><span data-stu-id="5ec71-109">Open the file Program.cs and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="5ec71-110">Dans la classe `Program` , ajoutez la méthode suivante ou remplacez-la si elle existe déjà :</span><span class="sxs-lookup"><span data-stu-id="5ec71-110">In the `Program` class, add the following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending the notification as a template notification. All template registrations that contain
            // "messageParam" and the proper tags will receive the notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="5ec71-111">Ce code envoie une notification de modèle pour chacune des six balises du tableau de chaînes.</span><span class="sxs-lookup"><span data-stu-id="5ec71-111">This code sends a template notification for each of the six tags in the string array.</span></span> <span data-ttu-id="5ec71-112">L’utilisation des balises permet d’envoyer les notifications uniquement aux appareils des catégories inscrites.</span><span class="sxs-lookup"><span data-stu-id="5ec71-112">The use of tags makes sure that devices receive notifications only for the registered categories.</span></span>
5. <span data-ttu-id="5ec71-113">Dans le code ci-dessus, remplacez les espaces réservés `<hub name>` et `<connection string with full access>` par le nom de votre hub de notification et par la chaîne de connexion pour *DefaultFullSharedAccessSignature* du tableau de bord de votre hub de notifications.</span><span class="sxs-lookup"><span data-stu-id="5ec71-113">In the above code, replace the `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and the connection  string for *DefaultFullSharedAccessSignature* from the dashboard of your notification hub.</span></span>
6. <span data-ttu-id="5ec71-114">Ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="5ec71-114">Add the following lines in the **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="5ec71-115">Générez l’application console.</span><span class="sxs-lookup"><span data-stu-id="5ec71-115">Build the console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
<span data-ttu-id="5ec71-116">[prise en main des Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="5ec71-116">[Get started with Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="5ec71-117">[l’interface REST des Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span><span class="sxs-lookup"><span data-stu-id="5ec71-117">[Notification Hubs REST interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span></span>
<span data-ttu-id="5ec71-118">[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="5ec71-118">[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="5ec71-119">[How to use Notification Hubs from Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span><span class="sxs-lookup"><span data-stu-id="5ec71-119">[How to use Notification Hubs from Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span></span>
<span data-ttu-id="5ec71-120">[package NuGet Microsoft.Azure.Notification Hubs]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span><span class="sxs-lookup"><span data-stu-id="5ec71-120">[Microsoft.Azure.Notification Hubs NuGet package]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span></span>
