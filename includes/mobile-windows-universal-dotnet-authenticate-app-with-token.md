
1. <span data-ttu-id="15205-101">Dans le fichier de projet hello MainPage.xaml.cs, ajoutez hello qui suit **à l’aide de** instructions :</span><span class="sxs-lookup"><span data-stu-id="15205-101">In hello MainPage.xaml.cs project file, add hello following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="15205-102">Remplacez hello **AuthenticateAsync** méthode avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="15205-102">Replace hello **AuthenticateAsync** method with hello following code:</span></span>
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    <span data-ttu-id="15205-103">Dans cette version de **AuthenticateAsync**, application hello tente d’informations d’identification de toouse stockées Bonjour **PasswordVault** tooaccess hello service.</span><span class="sxs-lookup"><span data-stu-id="15205-103">In this version of **AuthenticateAsync**, hello app tries toouse credentials stored in hello **PasswordVault** tooaccess hello service.</span></span> <span data-ttu-id="15205-104">Une connexion normale est également effectuée quand il n'y a pas d'informations d'identification stockées.</span><span class="sxs-lookup"><span data-stu-id="15205-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="15205-105">Un jeton mis en cache a peut-être expiré, et d’expiration du jeton peut également se produire après l’authentification lors de l’application hello est en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="15205-105">A cached token may be expired, and token expiration can also occur after authentication when hello app is in use.</span></span> <span data-ttu-id="15205-106">toolearn toodetermine si un jeton a expiré, voir [vérifier les jetons d’authentification a expiré](http://aka.ms/jww5vp).</span><span class="sxs-lookup"><span data-stu-id="15205-106">toolearn how toodetermine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="15205-107">Pour une erreur d’autorisation de toohandling solution tooexpiring connexes jetons, consultez hello [mise en cache et la gestion des jetons expirés dans Azure Mobile Services gérés SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="15205-107">For a solution toohandling authorization errors related tooexpiring tokens, see hello post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="15205-108">Redémarrez application hello à deux reprises.</span><span class="sxs-lookup"><span data-stu-id="15205-108">Restart hello app twice.</span></span>
   
    <span data-ttu-id="15205-109">Notez que sur le démarrage du premier hello, connectez-vous avec un fournisseur de hello est à nouveau requis.</span><span class="sxs-lookup"><span data-stu-id="15205-109">Notice that on hello first start-up, sign-in with hello provider is again required.</span></span> <span data-ttu-id="15205-110">Toutefois, lors du redémarrage de deuxième hello les informations d’identification de hello mis en cache sont utilisées et connectez-vous est ignorée.</span><span class="sxs-lookup"><span data-stu-id="15205-110">However, on hello second restart hello cached credentials are used and sign-in is bypassed.</span></span> 

