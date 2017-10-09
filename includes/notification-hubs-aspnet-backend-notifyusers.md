## <a name="create-hello-webapi-project"></a>Créer hello WebAPI projet
Un serveur ASP.NET WebAPI principal est créé dans les sections hello qui suivent, et il aura trois objectifs principaux :

1. **L’authentification de Clients**: un gestionnaire de messages est ajouté les demandes de client tooauthenticate ultérieures et utilisateur hello associer avec la demande de hello.
2. **Les inscriptions de Notification client**: une version ultérieure, vous allez ajouter un contrôleur toohandle nouvelles inscriptions pour les notifications tooreceive appareil d’un client. Hello nom d’utilisateur authentifié est automatiquement ajoutée inscription toohello comme un [balise](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **Envoi de Notifications tooClients**: une version ultérieure, vous ajouterez également un tooprovide contrôleur un moyen pour un utilisateur de tootrigger un toodevices sécurisé par émission de données et les clients associés à hello étiquette. 

Hello suit montrent comment toocreate hello ASP.NET WebAPI serveur principal : 

> [!IMPORTANT]
> Si vous utilisez Visual Studio 2015 ou version antérieure, avant de commencer ce didacticiel, assurez-vous que vous avez installé hello dernière version du Gestionnaire de Package NuGet de hello. toocheck, démarrez Visual Studio. À partir de hello **outils** menu, cliquez sur **Extensions et mises à jour**. Recherchez **Gestionnaire de Package NuGet** pour votre version de Visual Studio et assurez-vous que vous avez hello dernière version. Dans le cas contraire, désinstallez puis réinstallez le Gestionnaire de Package NuGet de hello.
> 
> ![][B4]
> 
> [!NOTE]
> Vérifiez que vous avez installé hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) pour le déploiement de site Web.
> 
> 

1. Démarrez Visual Studio ou Visual Studio Express. Cliquez sur **l’Explorateur de serveurs** et connectez-vous à tooyour compte Azure. Visual Studio signifie que vous devrez signé dans les ressources de site web toocreate hello sur votre compte.
2. Dans Visual Studio, cliquez sur **fichier**, puis cliquez sur **nouveau**, puis **projet**, développez **modèles**, **Visual C#**, puis cliquez sur **Web** et **Application Web ASP.NET**, nom de type hello **AppBackend**, puis cliquez sur **OK**. 
   
    ![][B1]
3. Bonjour **nouveau projet ASP.NET** boîte de dialogue, cliquez sur **API Web**, puis cliquez sur **OK**.
   
    ![][B2]
4. Bonjour **configurer l’application Web Microsoft Azure** boîte de dialogue, choisissez un abonnement et un **plan App Service** vous avez déjà créé. Vous pouvez également choisir **créer un plan de service d’application** et créer un à partir de la boîte de dialogue hello. Vous n'avez pas besoin de base de données pour ce didacticiel. Une fois que vous avez sélectionné votre plan app service, cliquez sur **OK** projet hello de toocreate.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>L’authentification des Clients toohello WebAPI Backend
Dans cette section, vous allez créer une nouvelle classe de gestionnaire de message nommée **AuthenticationTestHandler** pour le serveur principal hello. Cette classe est dérivée de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) ajouté en tant que gestionnaire de messages, afin qu’il peut traiter toutes les demandes entrantes dans hello principal. 

1. Dans l’Explorateur de solutions, cliquez sur hello **AppBackend** de projet, cliquez sur **ajouter**, puis cliquez sur **classe**. Nommez la nouvelle classe de hello **AuthenticationTestHandler.cs**, puis cliquez sur **ajouter** classe hello de toogenerate. Cette classe sera utilisé tooauthenticate les utilisateurs à l’aide de *l’authentification de base* par souci de simplicité. Notez que votre application peut utiliser n’importe quel schéma d’authentification.
2. Dans AuthenticationTestHandler.cs, ajoutez suivant de hello `using` instructions :
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. Dans AuthenticationTestHandler.cs, en remplaçant hello `AuthenticationTestHandler` définition de classe par hello suivant de code. 
   
    Ce gestionnaire permettra la demande de hello lorsque hello trois conditions suivantes est vrai :
   
   * demande Hello inclus un *autorisation* en-tête. 
   * demande de Hello utilise *base* l’authentification. 
   * chaîne de nom d’utilisateur Hello et la chaîne de mot de passe hello sont hello même chaîne.
     
     Dans le cas contraire, demande de hello est rejetée. Cette méthode ne répond pas à une véritable approche d’authentification et d’autorisation. Il s’agit uniquement d’un exemple très simple pour ce didacticiel.
     
     Si le message de demande hello est authentifié et autorisé par hello `AuthenticationTestHandler`, utilisateur de l’authentification de base hello sera attaché toohello la demande en cours sur hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). Les informations utilisateur Bonjour HttpContext seront utilisées par un autre contrôleur (RegisterController) tooadd ultérieure un [balise](https://msdn.microsoft.com/library/azure/dn530749.aspx) demande d’inscription de notification toohello.
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **Note de sécurité**: hello `AuthenticationTestHandler` classe ne fournit pas d’authentification true. Il est utilisé toomimic uniquement l’authentification de base et n’est pas sécurisée. Vous devez mettre en œuvre un mécanisme d’authentification sécurisé dans vos applications de production et vos services.                
     > 
     > 
4. Ajouter hello suivant du code à la fin de hello de hello `Register` méthode Bonjour **App_Start/WebApiConfig.cs** Gestionnaire de messages hello classe tooregister :
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Enregistrez vos modifications.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>Inscription aux Notifications à l’aide de hello WebAPI Backend
Dans cette section, nous allons ajouter qu'un nouveau serveur principal toohandle contrôleur toohello WebAPI demande tooregister un utilisateur et périphérique pour les notifications à l’aide de la bibliothèque cliente de hello pour les concentrateurs de notification. contrôleur de Hello ajoutera une balise de l’utilisateur pour l’utilisateur hello qui a été authentifié et attaché toohello HttpContext par hello `AuthenticationTestHandler`. balise de Hello aura le format de chaîne hello, `"username:<actual username>"`.

1. Dans l’Explorateur de solutions, cliquez sur hello **AppBackend** de projet, puis cliquez sur **gérer les Packages NuGet**.
2. Dans la partie gauche hello, cliquez sur **Online**et recherchez **Microsoft.Azure.NotificationHubs** Bonjour **recherche** boîte.
3. Dans la liste des résultats hello, cliquez sur **Microsoft Azure Notification Hubs**, puis cliquez sur **installer**. Terminer l’installation de hello, puis fermez la fenêtre hello du Gestionnaire de package NuGet.
   
    Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.
4. Nous allons maintenant créer un nouveau fichier de classe qui représente la connexion hello avec notification hub utilisé toosend notifications. Dans l’Explorateur de solutions de hello, avec le bouton droit hello **modèles** dossier, cliquez sur **ajouter**, puis cliquez sur **classe**. Nommez la nouvelle classe de hello **Notifications.cs**, puis cliquez sur **ajouter** classe hello de toogenerate. 
   
    ![][B6]
5. Dans Notifications.cs, ajoutez suivant de hello `using` instruction début hello du fichier de hello :
   
        using Microsoft.Azure.NotificationHubs;
6. Remplacez hello `Notifications` définition avec les éléments suivants de hello de classe et rendre des espaces réservés de hello deux tooreplace vraiment avec chaîne de connexion hello (avec un accès complet) pour votre concentrateur de notification hello nom du concentrateur (disponible à l’adresse [portail classique Azure ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. Nous allons ensuite créer un contrôleur nommé **RegisterController**. Dans l’Explorateur de solutions, cliquez sur hello **contrôleurs** dossier, puis cliquez sur **ajouter**, puis cliquez sur **contrôleur**. Cliquez sur hello **contrôleur 2 d’API Web--vide** d’élément, puis cliquez sur **ajouter**. Nommez la nouvelle classe de hello **RegisterController**, puis cliquez sur **ajouter** à nouveau le contrôleur de hello toogenerate.
   
    ![][B7]
   
    ![][B8]
8. Dans RegisterController.cs, ajoutez suivant de hello `using` instructions :
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Ajouter hello suivant du code à l’intérieur de hello `RegisterController` définition de classe. Notez que dans ce code, nous ajoutons une balise d’utilisateur pour l’utilisateur hello que cela est attaché toohello HttpContext. utilisateur de Hello a été authentifié et attaché toohello HttpContext par nous avons ajouté, le filtre de messages hello `AuthenticationTestHandler`. Vous pouvez également ajouter tooverify vérifications facultatif qui hello utilisateur dispose de droits tooregister pour hello demandé de balises.
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. Enregistrez vos modifications.

## <a name="sending-notifications-from-hello-webapi-backend"></a>Envoi de Notifications à partir de hello WebAPI Backend
Dans cette section vous ajoutez un nouveau contrôleur qui expose une méthode pour toosend des périphériques client une notification basée sur la balise de nom d’utilisateur hello à l’aide de la bibliothèque de gestion des services Azure Notification Hubs Bonjour ASP.NET WebAPI principal.

1. Créez un autre contrôleur nommé **NotificationsController**. Créez-le hello même façon que vous avez créé hello **RegisterController** dans la section précédente de hello.
2. Dans NotificationsController.cs, ajoutez suivant de hello `using` instructions :
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Ajouter hello suivant de méthode toohello **NotificationsController** classe.
   
    Ce code envoie un type de notification en fonction de hello plateforme Notification Service (PNS) `pns` paramètre. Hello valeur `to_tag` est utilisé tooset hello *nom d’utilisateur* balise sur le message de type hello. Cette balise doit correspondre à une balise de nom d’utilisateur d’une inscription de hub de notification active. message de notification Hello est extraite du corps hello de requête de publication hello et mise en forme pour la cible de hello PNS. 
   
    En fonction de la plateforme Notification Service (PNS) que vos appareils pris en charge utilisent tooreceive notifications de hello, différentes notifications sont prises en charge à l’aide de différents formats. Par exemple sur des appareils Windows, vous pouvez utiliser une [notification toast avec WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) qui n'est pas directement prise en charge par un autre service PNS. Vous envisagez de toosupport donc votre serveur principal serait notification de hello tooformat dans une notification pris en charge pour hello PNS de périphériques. Utilisez ensuite les API d’envoi approprié hello sur hello [NotificationHubClient classe](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. Appuyez sur **F5** toorun hello application et tooensure hello précision de votre travail jusqu'à présent. application Hello doit lancer un navigateur web et afficher la page d’accueil ASP.NET hello. 

## <a name="publish-hello-new-webapi-backend"></a>Publier hello nouveau WebAPI Backend
1. Maintenant vous déployez cette application de tooan site Web Azure dans l’ordre toomake accessible à partir de tous les appareils. Avec le bouton droit sur hello **AppBackend** de projet et sélectionnez **publier**.
2. Sélectionnez **Microsoft Azure App Service** comme cible de publication, puis cliquez sur **Publier**. Hello créer un Service application boîte de dialogue qui vous permet de créer tous les hello ressources Azure nécessaires toorun hello web d’application ASP.NET dans Azure s’ouvre.

    ![][B15]
3. Bonjour **créer un Service application** boîte de dialogue, sélectionnez votre compte Azure. Cliquez sur **Modifier le type** et sélectionnez **Application web**. Conserver hello **nom de l’application Web** hello donné et sélectionnez **abonnement**, **groupe de ressources**, et **du Plan App Service**.  Cliquez sur **Créer**.

4. Prenez note de hello **URL du Site** propriété Bonjour **Résumé** section. Nous appelons URL toothis comme votre *point de terminaison principal* plus loin dans ce didacticiel. Cliquez sur **Publier**.

5. Une fois l’Assistant de hello terminé, il publie hello ASP.NET web application tooAzure, et puis lance hello application dans le navigateur par défaut de hello.  Votre application sera visible dans Azure App Services.

URL de Hello utilise le nom d’application hello web que vous avez spécifié précédemment, avec hello format http://<app_name>.azurewebsites.net.

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
