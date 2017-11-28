
<span data-ttu-id="d9e2d-101">L’exemple précédent présentait une connexion standard, qui nécessite que le client contacte le fournisseur d’identité et le service principal Azure à chaque démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-101">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the back-end Azure service every time the app starts.</span></span> <span data-ttu-id="d9e2d-102">Cette méthode est inefficace et risque de vous poser des problèmes d’utilisation si de nombreux clients tentent de démarrer votre application simultanément.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-102">This method is inefficient, and you can have usage-related issues if many customers try to start your app simultaneously.</span></span> <span data-ttu-id="d9e2d-103">Une meilleure approche consiste à mettre en cache le jeton d’autorisation renvoyé par le service Azure et à tenter de l’utiliser avant de recourir à une connexion basée sur un fournisseur.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-103">A better approach is to cache the authorization token returned by the Azure service, and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="d9e2d-104">Vous pouvez mettre en cache le jeton émis par le service principal Azure, que vous utilisiez l’authentification gérée par le client ou gérée par le service.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-104">You can cache the token issued by the back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="d9e2d-105">Ce didacticiel utilise cette dernière.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="d9e2d-106">Ouvrez le fichier ToDoActivity.java, puis ajoutez les instructions import suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9e2d-106">Open the ToDoActivity.java file and add the following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="d9e2d-107">Ajoutez les membres suivants à la classe `ToDoActivity` :</span><span class="sxs-lookup"><span data-stu-id="d9e2d-107">Add the following members to the `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="d9e2d-108">Dans le fichier ToDoActivity.java, ajoutez la définition ci-après pour la méthode `cacheUserToken`.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-108">In the ToDoActivity.java file, add the following definition for the `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="d9e2d-109">Cette méthode stocke l’identificateur d’utilisateur et le jeton dans un fichier de préférences marqué comme privé.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-109">This method stores the user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="d9e2d-110">Cette opération doit protéger l’accès au cache afin que les autres applications de l’appareil n’aient pas accès au jeton.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-110">This should protect access to the cache so that other apps on the device do not have access to the token.</span></span> <span data-ttu-id="d9e2d-111">La préférence est exécutée dans le bac à sable (sandbox) de l’application.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-111">The preference is sandboxed for the app.</span></span> <span data-ttu-id="d9e2d-112">Toutefois, si une personne tente d'accéder à l'appareil, il est possible qu'elle puisse accéder au cache du jeton par d'autres moyens.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-112">However, if someone gains access to the device, it is possible that they may gain access to the token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d9e2d-113">Vous pouvez protéger davantage le jeton avec un chiffrement si l’accès du jeton à vos données est considéré comme très sensible et que quelqu’un peut accéder à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-113">You can further protect the token with encryption, if token access to your data is considered highly sensitive and someone may gain access to the device.</span></span> <span data-ttu-id="d9e2d-114">Une solution complètement sécurisée sort du cadre de ce didacticiel et dépend de vos besoins en matière de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-114">A completely secure solution is beyond the scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="d9e2d-115">Dans le fichier ToDoActivity.java, ajoutez la définition ci-après pour la méthode `loadUserTokenCache`.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-115">In the ToDoActivity.java file, add the following definition for the `loadUserTokenCache` method.</span></span>

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. <span data-ttu-id="d9e2d-116">Dans le fichier *ToDoActivity.java*, remplacez la méthode `authenticate` par la méthode ci-après qui utilise un cache de jetons.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-116">In the *ToDoActivity.java* file, replace the `authenticate` method with the following method, which uses a token cache.</span></span> <span data-ttu-id="d9e2d-117">Modifiez le fournisseur de connexion si vous voulez utiliser un compte autre que Google.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-117">Change the login provider if you want to use an account other than Google.</span></span>

        private void authenticate() {
            // We first try to load a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed to load a token cache, login and create a token cache
            else
            {
                // Login using the Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. <span data-ttu-id="d9e2d-118">Générez l'application et testez l'authentification à l'aide d'un compte valide.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-118">Build the app and test authentication using a valid account.</span></span> <span data-ttu-id="d9e2d-119">Exécutez ceci au moins deux fois.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-119">Run it at least twice.</span></span> <span data-ttu-id="d9e2d-120">À la première exécution, vous devez recevoir une invite vous indiquant de vous connecter et de créer le cache de jetons.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-120">During the first run, you should receive a prompt to sign in and create the token cache.</span></span> <span data-ttu-id="d9e2d-121">Après cela, chaque exécution tente de charger le cache de jetons pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-121">After that, each run attempts to load the token cache for authentication.</span></span> <span data-ttu-id="d9e2d-122">Vous ne devriez plus être invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="d9e2d-122">You should not be required to sign in.</span></span>
