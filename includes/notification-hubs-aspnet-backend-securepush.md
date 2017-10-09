## <a name="webapi-project"></a>Projet WebAPI
1. Dans Visual Studio, ouvrez hello **AppBackend** projet que vous avez créé dans hello **avertir les utilisateurs** didacticiel.
2. Dans Notifications.cs, hello remplacer toute **Notifications** classe avec hello suivant de code. Être des espaces réservés de hello tooreplace que votre chaîne de connexion pour votre concentrateur de notification et le nom de hub hello (avec un accès complet). Vous pouvez obtenir ces valeurs à partir de hello [portail classique Azure](http://manage.windowsazure.com). Ce module représente maintenant hello différentes notifications sécurisées qui seront envoyées. Dans une implémentation complète, les notifications hello seront stockées dans une base de données ; par souci de simplicité, dans ce cas nous les stocker en mémoire.
   
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

1. Dans NotificationsController.cs, remplacez le code hello hello **NotificationsController** définition de classe par hello suivant de code. Ce composant implémente un moyen pour la notification de hello tooretrieve hello appareil en toute sécurité et fournit également un tootrigger de façon (à des fins de hello de ce didacticiel) une unité de tooyour par émission de données sécurisée. Notez que lors de l’envoi de hub de notification hello notification toohello, nous envoyer uniquement une notification brute avec l’ID de hello de notification de hello (et aucun message réel) :
   
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


Notez que hello `Post` méthode maintenant n’envoie pas d’une notification de toast. Il envoie une notification brute contenant uniquement les ID de notification hello et pas de contenu sensible. Vérifiez également que toocomment hello opération pour les plateformes hello pour lequel il est inutile informations d’identification configurées sur votre concentrateur de notification, comme ils provoquera des erreurs d’envoi.

1. Maintenant nous sera redéployer cette application de tooan site Web Azure dans l’ordre toomake accessible à partir de tous les appareils. Avec le bouton droit sur hello **AppBackend** de projet et sélectionnez **publier**.
2. Sélectionnez Site web Azure comme cible de publication. Connectez-vous avec votre compte Azure, sélectionnez un site Web existant ou nouveau et prenez note de hello **URL de destination** propriété Bonjour **connexion** onglet. Nous appelons URL toothis comme votre *point de terminaison principal* plus loin dans ce didacticiel. Cliquez sur **Publier**.

