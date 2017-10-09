## <a name="webapi-project"></a><span data-ttu-id="c7332-101">Projet WebAPI</span><span class="sxs-lookup"><span data-stu-id="c7332-101">WebAPI Project</span></span>
1. <span data-ttu-id="c7332-102">Dans Visual Studio, ouvrez hello **AppBackend** projet que vous avez créé dans hello **avertir les utilisateurs** didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c7332-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="c7332-103">Dans Notifications.cs, hello remplacer toute **Notifications** classe avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="c7332-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="c7332-104">Être des espaces réservés de hello tooreplace que votre chaîne de connexion pour votre concentrateur de notification et le nom de hub hello (avec un accès complet).</span><span class="sxs-lookup"><span data-stu-id="c7332-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="c7332-105">Vous pouvez obtenir ces valeurs à partir de hello [portail classique Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c7332-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="c7332-106">Ce module représente maintenant hello différentes notifications sécurisées qui seront envoyées.</span><span class="sxs-lookup"><span data-stu-id="c7332-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="c7332-107">Dans une implémentation complète, les notifications hello seront stockées dans une base de données ; par souci de simplicité, dans ce cas nous les stocker en mémoire.</span><span class="sxs-lookup"><span data-stu-id="c7332-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
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

1. <span data-ttu-id="c7332-108">Dans NotificationsController.cs, remplacez le code hello hello **NotificationsController** définition de classe par hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="c7332-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="c7332-109">Ce composant implémente un moyen pour la notification de hello tooretrieve hello appareil en toute sécurité et fournit également un tootrigger de façon (à des fins de hello de ce didacticiel) une unité de tooyour par émission de données sécurisée.</span><span class="sxs-lookup"><span data-stu-id="c7332-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="c7332-110">Notez que lors de l’envoi de hub de notification hello notification toohello, nous envoyer uniquement une notification brute avec l’ID de hello de notification de hello (et aucun message réel) :</span><span class="sxs-lookup"><span data-stu-id="c7332-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
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


<span data-ttu-id="c7332-111">Notez que hello `Post` méthode maintenant n’envoie pas d’une notification de toast.</span><span class="sxs-lookup"><span data-stu-id="c7332-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="c7332-112">Il envoie une notification brute contenant uniquement les ID de notification hello et pas de contenu sensible.</span><span class="sxs-lookup"><span data-stu-id="c7332-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="c7332-113">Vérifiez également que toocomment hello opération pour les plateformes hello pour lequel il est inutile informations d’identification configurées sur votre concentrateur de notification, comme ils provoquera des erreurs d’envoi.</span><span class="sxs-lookup"><span data-stu-id="c7332-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="c7332-114">Maintenant nous sera redéployer cette application de tooan site Web Azure dans l’ordre toomake accessible à partir de tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="c7332-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="c7332-115">Avec le bouton droit sur hello **AppBackend** de projet et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="c7332-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="c7332-116">Sélectionnez Site web Azure comme cible de publication.</span><span class="sxs-lookup"><span data-stu-id="c7332-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="c7332-117">Connectez-vous avec votre compte Azure, sélectionnez un site Web existant ou nouveau et prenez note de hello **URL de destination** propriété Bonjour **connexion** onglet. Nous appelons URL toothis comme votre *point de terminaison principal* plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c7332-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="c7332-118">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="c7332-118">Click **Publish**.</span></span>

