## <a name="webapi-project"></a><span data-ttu-id="2b253-101">Projet WebAPI</span><span class="sxs-lookup"><span data-stu-id="2b253-101">WebAPI Project</span></span>
1. <span data-ttu-id="2b253-102">Dans Visual Studio, ouvrez le projet **AppBackend** que vous avez créé dans le didacticiel **Notification des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2b253-102">In Visual Studio, open the **AppBackend** project that you created in the **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="2b253-103">Dans le fichier Notifications.cs, remplacez la totalité de la classe **Notifications** par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="2b253-103">In Notifications.cs, replace the whole **Notifications** class with the following code.</span></span> <span data-ttu-id="2b253-104">Veillez à remplacer les espaces réservés par la chaîne de connexion (avec accès complet) de votre hub de notification et par le nom de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="2b253-104">Be sure to replace the placeholders with your connection string (with full access) for your notification hub, and the hub name.</span></span> <span data-ttu-id="2b253-105">Ces valeurs sont disponibles dans le [Portail Azure Classic](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2b253-105">You can obtain these values from the [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="2b253-106">Ce module représente maintenant les différentes notifications sécurisées qui seront envoyées.</span><span class="sxs-lookup"><span data-stu-id="2b253-106">This module now represents the different secure notifications that will be sent.</span></span> <span data-ttu-id="2b253-107">Dans les implémentations complètes, les notifications sont stockées dans une base de données. Par souci de simplification, nous les stockons ici en mémoire.</span><span class="sxs-lookup"><span data-stu-id="2b253-107">In a complete implementation, the notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. <span data-ttu-id="2b253-108">Dans le fichier NotificationsController.cs, remplacez le code de la définition de classe **NotificationsController** par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="2b253-108">In NotificationsController.cs, replace the code inside the **NotificationsController** class definition with the following code.</span></span> <span data-ttu-id="2b253-109">Ce composant permet à l'appareil de récupérer la notification en toute sécurité. Dans l'exemple de ce didacticiel, il vous permet également de déclencher une notification push sécurisée sur vos appareils.</span><span class="sxs-lookup"><span data-stu-id="2b253-109">This component implements a way for the device to retrieve the notification securely, and also provides a way (for the purposes of this tutorial) to trigger a secure push to your devices.</span></span> <span data-ttu-id="2b253-110">Notez que la notification envoyée ici au hub de notification est brute puisqu’elle comporte uniquement son ID (sans message) :</span><span class="sxs-lookup"><span data-stu-id="2b253-110">Note that when sending the notification to the notification hub, we only send a raw notification with the ID of the notification (and no actual message):</span></span>
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


<span data-ttu-id="2b253-111">Notez que la méthode `Post` n'envoie pas de notification toast.</span><span class="sxs-lookup"><span data-stu-id="2b253-111">Note that the `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="2b253-112">Elle envoie une notification brute qui contient uniquement l’ID de la notification, sans aucun contenu sensible.</span><span class="sxs-lookup"><span data-stu-id="2b253-112">It sends a raw notification that contains only the notification ID, and not any sensitive content.</span></span> <span data-ttu-id="2b253-113">Veillez également à commenter l'opération d'envoi pour les plateformes pour lesquelles aucune information d'identification n'est configurée sur votre hub de notification, car celles-ci généreront des erreurs.</span><span class="sxs-lookup"><span data-stu-id="2b253-113">Also, make sure to comment the send operation for the platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="2b253-114">Nous allons maintenant redéployer cette application sur un site web Azure afin de la rendre accessible à tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="2b253-114">Now we will re-deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="2b253-115">Cliquez avec le bouton droit sur le projet **AppBackend**, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="2b253-115">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="2b253-116">Sélectionnez Site web Azure comme cible de publication.</span><span class="sxs-lookup"><span data-stu-id="2b253-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="2b253-117">Connectez-vous avec votre compte Azure, sélectionnez un site web (nouveau ou existant), puis notez la valeur de la propriété **URL de destination** sous l’onglet **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="2b253-117">Log in with your Azure account and select an existing or new Website, and make a note of the **destination URL** property in the **Connection** tab.</span></span> <span data-ttu-id="2b253-118">Plus loin dans ce didacticiel, nous utiliserons cette URL comme *point de terminaison principal* .</span><span class="sxs-lookup"><span data-stu-id="2b253-118">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="2b253-119">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="2b253-119">Click **Publish**.</span></span>

