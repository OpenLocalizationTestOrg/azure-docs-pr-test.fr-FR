## <a name="create-hello-webapi-project"></a><span data-ttu-id="6765e-101">Créer hello WebAPI projet</span><span class="sxs-lookup"><span data-stu-id="6765e-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="6765e-102">Un serveur ASP.NET WebAPI principal est créé dans les sections hello qui suivent, et il aura trois objectifs principaux :</span><span class="sxs-lookup"><span data-stu-id="6765e-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="6765e-103">**L’authentification de Clients**: un gestionnaire de messages est ajouté les demandes de client tooauthenticate ultérieures et utilisateur hello associer avec la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="6765e-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="6765e-104">**Les inscriptions de Notification client**: une version ultérieure, vous allez ajouter un contrôleur toohandle nouvelles inscriptions pour les notifications tooreceive appareil d’un client.</span><span class="sxs-lookup"><span data-stu-id="6765e-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="6765e-105">Hello nom d’utilisateur authentifié est automatiquement ajoutée inscription toohello comme un [balise](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="6765e-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="6765e-106">**Envoi de Notifications tooClients**: une version ultérieure, vous ajouterez également un tooprovide contrôleur un moyen pour un utilisateur de tootrigger un toodevices sécurisé par émission de données et les clients associés à hello étiquette.</span><span class="sxs-lookup"><span data-stu-id="6765e-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="6765e-107">Hello suit montrent comment toocreate hello ASP.NET WebAPI serveur principal :</span><span class="sxs-lookup"><span data-stu-id="6765e-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6765e-108">Si vous utilisez Visual Studio 2015 ou version antérieure, avant de commencer ce didacticiel, assurez-vous que vous avez installé hello dernière version du Gestionnaire de Package NuGet de hello.</span><span class="sxs-lookup"><span data-stu-id="6765e-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="6765e-109">toocheck, démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6765e-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="6765e-110">À partir de hello **outils** menu, cliquez sur **Extensions et mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="6765e-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="6765e-111">Recherchez **Gestionnaire de Package NuGet** pour votre version de Visual Studio et assurez-vous que vous avez hello dernière version.</span><span class="sxs-lookup"><span data-stu-id="6765e-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="6765e-112">Dans le cas contraire, désinstallez puis réinstallez le Gestionnaire de Package NuGet de hello.</span><span class="sxs-lookup"><span data-stu-id="6765e-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="6765e-113">Vérifiez que vous avez installé hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) pour le déploiement de site Web.</span><span class="sxs-lookup"><span data-stu-id="6765e-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="6765e-114">Démarrez Visual Studio ou Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="6765e-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="6765e-115">Cliquez sur **l’Explorateur de serveurs** et connectez-vous à tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="6765e-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="6765e-116">Visual Studio signifie que vous devrez signé dans les ressources de site web toocreate hello sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="6765e-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="6765e-117">Dans Visual Studio, cliquez sur **fichier**, puis cliquez sur **nouveau**, puis **projet**, développez **modèles**, **Visual C#**, puis cliquez sur **Web** et **Application Web ASP.NET**, nom de type hello **AppBackend**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6765e-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="6765e-118">Bonjour **nouveau projet ASP.NET** boîte de dialogue, cliquez sur **API Web**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6765e-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="6765e-119">Bonjour **configurer l’application Web Microsoft Azure** boîte de dialogue, choisissez un abonnement et un **plan App Service** vous avez déjà créé.</span><span class="sxs-lookup"><span data-stu-id="6765e-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="6765e-120">Vous pouvez également choisir **créer un plan de service d’application** et créer un à partir de la boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="6765e-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="6765e-121">Vous n'avez pas besoin de base de données pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6765e-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="6765e-122">Une fois que vous avez sélectionné votre plan app service, cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="6765e-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="6765e-123">L’authentification des Clients toohello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="6765e-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="6765e-124">Dans cette section, vous allez créer une nouvelle classe de gestionnaire de message nommée **AuthenticationTestHandler** pour le serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="6765e-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="6765e-125">Cette classe est dérivée de [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) ajouté en tant que gestionnaire de messages, afin qu’il peut traiter toutes les demandes entrantes dans hello principal.</span><span class="sxs-lookup"><span data-stu-id="6765e-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="6765e-126">Dans l’Explorateur de solutions, cliquez sur hello **AppBackend** de projet, cliquez sur **ajouter**, puis cliquez sur **classe**.</span><span class="sxs-lookup"><span data-stu-id="6765e-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="6765e-127">Nommez la nouvelle classe de hello **AuthenticationTestHandler.cs**, puis cliquez sur **ajouter** classe hello de toogenerate.</span><span class="sxs-lookup"><span data-stu-id="6765e-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="6765e-128">Cette classe sera utilisé tooauthenticate les utilisateurs à l’aide de *l’authentification de base* par souci de simplicité.</span><span class="sxs-lookup"><span data-stu-id="6765e-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="6765e-129">Notez que votre application peut utiliser n’importe quel schéma d’authentification.</span><span class="sxs-lookup"><span data-stu-id="6765e-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="6765e-130">Dans AuthenticationTestHandler.cs, ajoutez suivant de hello `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="6765e-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="6765e-131">Dans AuthenticationTestHandler.cs, en remplaçant hello `AuthenticationTestHandler` définition de classe par hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="6765e-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="6765e-132">Ce gestionnaire permettra la demande de hello lorsque hello trois conditions suivantes est vrai :</span><span class="sxs-lookup"><span data-stu-id="6765e-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="6765e-133">demande Hello inclus un *autorisation* en-tête.</span><span class="sxs-lookup"><span data-stu-id="6765e-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="6765e-134">demande de Hello utilise *base* l’authentification.</span><span class="sxs-lookup"><span data-stu-id="6765e-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="6765e-135">chaîne de nom d’utilisateur Hello et la chaîne de mot de passe hello sont hello même chaîne.</span><span class="sxs-lookup"><span data-stu-id="6765e-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="6765e-136">Dans le cas contraire, demande de hello est rejetée.</span><span class="sxs-lookup"><span data-stu-id="6765e-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="6765e-137">Cette méthode ne répond pas à une véritable approche d’authentification et d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="6765e-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="6765e-138">Il s’agit uniquement d’un exemple très simple pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6765e-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="6765e-139">Si le message de demande hello est authentifié et autorisé par hello `AuthenticationTestHandler`, utilisateur de l’authentification de base hello sera attaché toohello la demande en cours sur hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="6765e-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="6765e-140">Les informations utilisateur Bonjour HttpContext seront utilisées par un autre contrôleur (RegisterController) tooadd ultérieure un [balise](https://msdn.microsoft.com/library/azure/dn530749.aspx) demande d’inscription de notification toohello.</span><span class="sxs-lookup"><span data-stu-id="6765e-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="6765e-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="6765e-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
       <span data-ttu-id="6765e-142">}</span><span class="sxs-lookup"><span data-stu-id="6765e-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="6765e-143">**Note de sécurité**: hello `AuthenticationTestHandler` classe ne fournit pas d’authentification true.</span><span class="sxs-lookup"><span data-stu-id="6765e-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="6765e-144">Il est utilisé toomimic uniquement l’authentification de base et n’est pas sécurisée.</span><span class="sxs-lookup"><span data-stu-id="6765e-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="6765e-145">Vous devez mettre en œuvre un mécanisme d’authentification sécurisé dans vos applications de production et vos services.</span><span class="sxs-lookup"><span data-stu-id="6765e-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="6765e-146">Ajouter hello suivant du code à la fin de hello de hello `Register` méthode Bonjour **App_Start/WebApiConfig.cs** Gestionnaire de messages hello classe tooregister :</span><span class="sxs-lookup"><span data-stu-id="6765e-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="6765e-147">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="6765e-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="6765e-148">Inscription aux Notifications à l’aide de hello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="6765e-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="6765e-149">Dans cette section, nous allons ajouter qu'un nouveau serveur principal toohandle contrôleur toohello WebAPI demande tooregister un utilisateur et périphérique pour les notifications à l’aide de la bibliothèque cliente de hello pour les concentrateurs de notification.</span><span class="sxs-lookup"><span data-stu-id="6765e-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="6765e-150">contrôleur de Hello ajoutera une balise de l’utilisateur pour l’utilisateur hello qui a été authentifié et attaché toohello HttpContext par hello `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="6765e-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="6765e-151">balise de Hello aura le format de chaîne hello, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="6765e-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="6765e-152">Dans l’Explorateur de solutions, cliquez sur hello **AppBackend** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6765e-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="6765e-153">Dans la partie gauche hello, cliquez sur **Online**et recherchez **Microsoft.Azure.NotificationHubs** Bonjour **recherche** boîte.</span><span class="sxs-lookup"><span data-stu-id="6765e-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="6765e-154">Dans la liste des résultats hello, cliquez sur **Microsoft Azure Notification Hubs**, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="6765e-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="6765e-155">Terminer l’installation de hello, puis fermez la fenêtre hello du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="6765e-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="6765e-156">Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="6765e-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="6765e-157">Nous allons maintenant créer un nouveau fichier de classe qui représente la connexion hello avec notification hub utilisé toosend notifications.</span><span class="sxs-lookup"><span data-stu-id="6765e-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="6765e-158">Dans l’Explorateur de solutions de hello, avec le bouton droit hello **modèles** dossier, cliquez sur **ajouter**, puis cliquez sur **classe**.</span><span class="sxs-lookup"><span data-stu-id="6765e-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="6765e-159">Nommez la nouvelle classe de hello **Notifications.cs**, puis cliquez sur **ajouter** classe hello de toogenerate.</span><span class="sxs-lookup"><span data-stu-id="6765e-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="6765e-160">Dans Notifications.cs, ajoutez suivant de hello `using` instruction début hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="6765e-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="6765e-161">Remplacez hello `Notifications` définition avec les éléments suivants de hello de classe et rendre des espaces réservés de hello deux tooreplace vraiment avec chaîne de connexion hello (avec un accès complet) pour votre concentrateur de notification hello nom du concentrateur (disponible à l’adresse [portail classique Azure ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="6765e-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="6765e-162">Nous allons ensuite créer un contrôleur nommé **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="6765e-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="6765e-163">Dans l’Explorateur de solutions, cliquez sur hello **contrôleurs** dossier, puis cliquez sur **ajouter**, puis cliquez sur **contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="6765e-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="6765e-164">Cliquez sur hello **contrôleur 2 d’API Web--vide** d’élément, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6765e-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="6765e-165">Nommez la nouvelle classe de hello **RegisterController**, puis cliquez sur **ajouter** à nouveau le contrôleur de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="6765e-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="6765e-166">Dans RegisterController.cs, ajoutez suivant de hello `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="6765e-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="6765e-167">Ajouter hello suivant du code à l’intérieur de hello `RegisterController` définition de classe.</span><span class="sxs-lookup"><span data-stu-id="6765e-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="6765e-168">Notez que dans ce code, nous ajoutons une balise d’utilisateur pour l’utilisateur hello que cela est attaché toohello HttpContext.</span><span class="sxs-lookup"><span data-stu-id="6765e-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="6765e-169">utilisateur de Hello a été authentifié et attaché toohello HttpContext par nous avons ajouté, le filtre de messages hello `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="6765e-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="6765e-170">Vous pouvez également ajouter tooverify vérifications facultatif qui hello utilisateur dispose de droits tooregister pour hello demandé de balises.</span><span class="sxs-lookup"><span data-stu-id="6765e-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
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
10. <span data-ttu-id="6765e-171">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="6765e-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="6765e-172">Envoi de Notifications à partir de hello WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="6765e-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="6765e-173">Dans cette section vous ajoutez un nouveau contrôleur qui expose une méthode pour toosend des périphériques client une notification basée sur la balise de nom d’utilisateur hello à l’aide de la bibliothèque de gestion des services Azure Notification Hubs Bonjour ASP.NET WebAPI principal.</span><span class="sxs-lookup"><span data-stu-id="6765e-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="6765e-174">Créez un autre contrôleur nommé **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="6765e-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="6765e-175">Créez-le hello même façon que vous avez créé hello **RegisterController** dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="6765e-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="6765e-176">Dans NotificationsController.cs, ajoutez suivant de hello `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="6765e-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="6765e-177">Ajouter hello suivant de méthode toohello **NotificationsController** classe.</span><span class="sxs-lookup"><span data-stu-id="6765e-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="6765e-178">Ce code envoie un type de notification en fonction de hello plateforme Notification Service (PNS) `pns` paramètre.</span><span class="sxs-lookup"><span data-stu-id="6765e-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="6765e-179">Hello valeur `to_tag` est utilisé tooset hello *nom d’utilisateur* balise sur le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="6765e-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="6765e-180">Cette balise doit correspondre à une balise de nom d’utilisateur d’une inscription de hub de notification active.</span><span class="sxs-lookup"><span data-stu-id="6765e-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="6765e-181">message de notification Hello est extraite du corps hello de requête de publication hello et mise en forme pour la cible de hello PNS.</span><span class="sxs-lookup"><span data-stu-id="6765e-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="6765e-182">En fonction de la plateforme Notification Service (PNS) que vos appareils pris en charge utilisent tooreceive notifications de hello, différentes notifications sont prises en charge à l’aide de différents formats.</span><span class="sxs-lookup"><span data-stu-id="6765e-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="6765e-183">Par exemple sur des appareils Windows, vous pouvez utiliser une [notification toast avec WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) qui n'est pas directement prise en charge par un autre service PNS.</span><span class="sxs-lookup"><span data-stu-id="6765e-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="6765e-184">Vous envisagez de toosupport donc votre serveur principal serait notification de hello tooformat dans une notification pris en charge pour hello PNS de périphériques.</span><span class="sxs-lookup"><span data-stu-id="6765e-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="6765e-185">Utilisez ensuite les API d’envoi approprié hello sur hello [NotificationHubClient classe](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="6765e-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="6765e-186">Appuyez sur **F5** toorun hello application et tooensure hello précision de votre travail jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="6765e-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="6765e-187">application Hello doit lancer un navigateur web et afficher la page d’accueil ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="6765e-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="6765e-188">Publier hello nouveau WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="6765e-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="6765e-189">Maintenant vous déployez cette application de tooan site Web Azure dans l’ordre toomake accessible à partir de tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="6765e-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="6765e-190">Avec le bouton droit sur hello **AppBackend** de projet et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="6765e-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="6765e-191">Sélectionnez **Microsoft Azure App Service** comme cible de publication, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="6765e-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="6765e-192">Hello créer un Service application boîte de dialogue qui vous permet de créer tous les hello ressources Azure nécessaires toorun hello web d’application ASP.NET dans Azure s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="6765e-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="6765e-193">Bonjour **créer un Service application** boîte de dialogue, sélectionnez votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="6765e-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="6765e-194">Cliquez sur **Modifier le type** et sélectionnez **Application web**.</span><span class="sxs-lookup"><span data-stu-id="6765e-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="6765e-195">Conserver hello **nom de l’application Web** hello donné et sélectionnez **abonnement**, **groupe de ressources**, et **du Plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="6765e-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="6765e-196">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6765e-196">Click **Create**.</span></span>

4. <span data-ttu-id="6765e-197">Prenez note de hello **URL du Site** propriété Bonjour **Résumé** section.</span><span class="sxs-lookup"><span data-stu-id="6765e-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="6765e-198">Nous appelons URL toothis comme votre *point de terminaison principal* plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6765e-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="6765e-199">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="6765e-199">Click **Publish**.</span></span>

5. <span data-ttu-id="6765e-200">Une fois l’Assistant de hello terminé, il publie hello ASP.NET web application tooAzure, et puis lance hello application dans le navigateur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="6765e-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="6765e-201">Votre application sera visible dans Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="6765e-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="6765e-202">URL de Hello utilise le nom d’application hello web que vous avez spécifié précédemment, avec hello format http://<app_name>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="6765e-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

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
