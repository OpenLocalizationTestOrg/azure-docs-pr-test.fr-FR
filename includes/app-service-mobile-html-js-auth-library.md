### <span data-ttu-id="5cf55-101"><a name="server-auth"></a>Procédure : authentification auprès d’un fournisseur (flux serveur)</span><span class="sxs-lookup"><span data-stu-id="5cf55-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="5cf55-102">les applications mobiles toohave gérer les processus d’authentification hello dans votre application, vous devez inscrire votre application avec votre fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="5cf55-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="5cf55-103">Dans votre Service d’applications Azure, vous devez tooconfigure ID de l’application hello et secret fournie par votre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="5cf55-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="5cf55-104">Pour plus d’informations, consultez le didacticiel de hello [ajouter l’authentification tooyour application](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="5cf55-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="5cf55-105">Une fois que vous avez enregistré votre fournisseur d’identité, appelez hello `.login()` méthode avec le nom hello de votre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="5cf55-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="5cf55-106">Par exemple, toologin avec Facebook utiliser hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="5cf55-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="5cf55-107">les valeurs valides Hello pour le fournisseur de hello sont 'aad', 'facebook', 'google', 'microsoftaccount' et « twitter ».</span><span class="sxs-lookup"><span data-stu-id="5cf55-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="5cf55-108">L’authentification Google ne fonctionne pour le moment pas via le flux serveur.</span><span class="sxs-lookup"><span data-stu-id="5cf55-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="5cf55-109">tooauthenticate avec Google, vous devez utiliser un [méthode de flux client](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="5cf55-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="5cf55-110">Dans ce cas, du Service d’applications Azure gère les flux d’authentification hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="5cf55-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="5cf55-111">Il affiche la page de connexion hello du fournisseur sélectionné de hello et génère un jeton d’authentification du Service d’applications après l’ouverture de session réussie avec le fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="5cf55-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="5cf55-112">fonction de connexion Hello, lorsque vous avez terminé, retourne un objet JSON qui expose hello ID d’utilisateur et le Service application jeton d’authentification dans les champs de nom d’utilisateur et authenticationToken hello, respectivement.</span><span class="sxs-lookup"><span data-stu-id="5cf55-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="5cf55-113">Ce jeton peut être mis en cache et réutilisé jusqu'à ce qu'il arrive à expiration.</span><span class="sxs-lookup"><span data-stu-id="5cf55-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="5cf55-114"><a name="client-auth"></a>Procédure : authentification auprès d’un fournisseur (flux client)</span><span class="sxs-lookup"><span data-stu-id="5cf55-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="5cf55-115">Votre application peut également indépendamment contactez le fournisseur d’identité hello, puis saisissez hello retourné tooyour jeton du Service d’applications pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="5cf55-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="5cf55-116">Ce flux du client vous permet de tooprovide une expérience d’authentification unique pour les utilisateurs ou les données d’utilisateur supplémentaires tooretrieve hello fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="5cf55-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="5cf55-117">Exemple de base de l’authentification sociale</span><span class="sxs-lookup"><span data-stu-id="5cf55-117">Social Authentication basic example</span></span>

<span data-ttu-id="5cf55-118">Cet exemple utilise le SDK client Facebook pour l'authentification :</span><span class="sxs-lookup"><span data-stu-id="5cf55-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="5cf55-119">Cet exemple suppose que ce jeton hello fournies par le fournisseur de respectifs hello SDK est stocké dans la variable de jeton hello.</span><span class="sxs-lookup"><span data-stu-id="5cf55-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="5cf55-120">Exemple de compte Microsoft</span><span class="sxs-lookup"><span data-stu-id="5cf55-120">Microsoft Account example</span></span>

<span data-ttu-id="5cf55-121">Hello suivant montre comment utiliser hello Live SDK, qui prend en charge authentification unique pour les applications du Windows Store à l’aide de Microsoft Account :</span><span class="sxs-lookup"><span data-stu-id="5cf55-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="5cf55-122">Cet exemple obtient un jeton de Live Connect, qui est fourni tooyour du Service d’applications en appelant la fonction de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="5cf55-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="5cf55-123"><a name="auth-getinfo"></a>Comment : obtenir des informations sur l’utilisateur de hello authentifié</span><span class="sxs-lookup"><span data-stu-id="5cf55-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="5cf55-124">informations d’authentification Hello peuvent être récupérées à partir de hello `/.auth/me` appeler de point de terminaison à l’aide de HTTP avec n’importe quelle bibliothèque AJAX.</span><span class="sxs-lookup"><span data-stu-id="5cf55-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="5cf55-125">Veillez à définir hello `X-ZUMO-AUTH` jeton d’authentification tooyour en-tête.</span><span class="sxs-lookup"><span data-stu-id="5cf55-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="5cf55-126">jeton d’authentification Hello est stocké dans `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="5cf55-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="5cf55-127">Par exemple, toouse hello fetch API :</span><span class="sxs-lookup"><span data-stu-id="5cf55-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="5cf55-128">L’extraction est disponible sous forme de [package npm](https://www.npmjs.com/package/whatwg-fetch) ou de téléchargement par navigateur à partir de [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="5cf55-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="5cf55-129">Vous pouvez également utiliser jQuery ou informations hello de toofetch une autre API AJAX.</span><span class="sxs-lookup"><span data-stu-id="5cf55-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="5cf55-130">Les données sont reçues sous la forme d’un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="5cf55-130">Data is received as a JSON object.</span></span>
