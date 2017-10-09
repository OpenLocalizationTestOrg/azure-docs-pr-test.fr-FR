
<span data-ttu-id="61763-101">Hello l’exemple précédent a montré une standard sign-in, ce qui nécessite hello client toocontact deux hello identité fournisseur et hello Azure service principal chaque démarrage d’application hello.</span><span class="sxs-lookup"><span data-stu-id="61763-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="61763-102">Cette méthode est inefficace, et vous pouvez avoir des problèmes liés à l’utilisation si de nombreux clients essaient de toostart votre application simultanément.</span><span class="sxs-lookup"><span data-stu-id="61763-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="61763-103">Une meilleure approche est le jeton d’autorisation toocache hello retournées par hello service Azure et try toouse cela tout d’abord avant d’utiliser un fournisseur connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="61763-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="61763-104">Vous pouvez mettre en cache jeton hello émis par hello principaux services Azure, quelle que soit la que vous utilisez l’authentification de client géré ou par le service.</span><span class="sxs-lookup"><span data-stu-id="61763-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="61763-105">Ce didacticiel utilise cette dernière.</span><span class="sxs-lookup"><span data-stu-id="61763-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="61763-106">Ouvrir le fichier de ToDoActivity.java hello et ajouter hello suivant les instructions d’importation :</span><span class="sxs-lookup"><span data-stu-id="61763-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="61763-107">Ajouter hello suivant membres toohello `ToDoActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="61763-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="61763-108">Dans le fichier de ToDoActivity.java hello, ajouter hello définition pourquoi `cacheUserToken` (méthode).</span><span class="sxs-lookup"><span data-stu-id="61763-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="61763-109">Cette méthode stocke hello ID d’utilisateur et le jeton dans un fichier de préférence qui est marqué comme privé.</span><span class="sxs-lookup"><span data-stu-id="61763-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="61763-110">Cela doit protéger accès toohello cache afin que les autres applications sur l’appareil de hello n’ont pas de jeton d’accès toohello.</span><span class="sxs-lookup"><span data-stu-id="61763-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="61763-111">préférence de Hello est sandbox pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="61763-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="61763-112">Toutefois, si quelqu'un a dispositif toohello d’accès, il est possible peut bénéficier des accès cache de jeton toohello par d’autres moyens.</span><span class="sxs-lookup"><span data-stu-id="61763-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="61763-113">Vous pouvez renforcer la protection jeton hello avec le chiffrement, si les données tooyour de jeton d’accès sont considéré comme hautement confidentielles et un utilisateur peut vous faire gagner DISPOSITIF toohello d’accès.</span><span class="sxs-lookup"><span data-stu-id="61763-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="61763-114">Une solution entièrement sécurisée est abordée dans ce didacticiel, hello et dépend de vos exigences de sécurité.</span><span class="sxs-lookup"><span data-stu-id="61763-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="61763-115">Dans le fichier de ToDoActivity.java hello, ajouter hello définition pourquoi `loadUserTokenCache` (méthode).</span><span class="sxs-lookup"><span data-stu-id="61763-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

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
5. <span data-ttu-id="61763-116">Bonjour *ToDoActivity.java* de fichiers, remplacez hello `authenticate` méthode avec hello suivant de méthode, qui utilise un cache de jeton.</span><span class="sxs-lookup"><span data-stu-id="61763-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="61763-117">Modifier le fournisseur de connexion hello si vous voulez toouse un compte autre que Google.</span><span class="sxs-lookup"><span data-stu-id="61763-117">Change hello login provider if you want toouse an account other than Google.</span></span>

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
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
6. <span data-ttu-id="61763-118">Générez hello application et tester l’authentification à l’aide d’un compte valide.</span><span class="sxs-lookup"><span data-stu-id="61763-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="61763-119">Exécutez ceci au moins deux fois.</span><span class="sxs-lookup"><span data-stu-id="61763-119">Run it at least twice.</span></span> <span data-ttu-id="61763-120">Pendant hello exécutez d’abord, vous devez recevoir une invite de commandes toosign dans et créer le cache de jeton hello.</span><span class="sxs-lookup"><span data-stu-id="61763-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="61763-121">Après cela, chaque série de tentatives tooload hello cache de jetons pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="61763-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="61763-122">Vous ne devez pas être toosign requis dans.</span><span class="sxs-lookup"><span data-stu-id="61763-122">You should not be required toosign in.</span></span>
