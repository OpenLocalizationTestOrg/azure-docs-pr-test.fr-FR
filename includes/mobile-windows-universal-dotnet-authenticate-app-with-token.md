
1. <span data-ttu-id="dec49-101">Ouvrez le fichier de projet MainPage.xaml.cs et ajoutez les instructions **using** suivantes :</span><span class="sxs-lookup"><span data-stu-id="dec49-101">In the MainPage.xaml.cs project file, add the following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="dec49-102">Remplacez la méthode **AuthenticateAsync** par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="dec49-102">Replace the **AuthenticateAsync** method with the following code:</span></span>
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses the Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use the PasswordVault to securely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try to get an existing credential from the vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from the stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set the user from the stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check to determine if the token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with the identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store the user credentials.
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
   
    <span data-ttu-id="dec49-103">Dans cette version d’**AuthenticateAsync**, l’application essaie d’utiliser les informations d’identification stockées dans le **coffre de mots de passe** pour accéder au service.</span><span class="sxs-lookup"><span data-stu-id="dec49-103">In this version of **AuthenticateAsync**, the app tries to use credentials stored in the **PasswordVault** to access the service.</span></span> <span data-ttu-id="dec49-104">Une connexion normale est également effectuée quand il n'y a pas d'informations d'identification stockées.</span><span class="sxs-lookup"><span data-stu-id="dec49-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dec49-105">Un jeton en cache peut avoir expiré et l'expiration des jetons peut également survenir après l'authentification, alors que l'application est en cours d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="dec49-105">A cached token may be expired, and token expiration can also occur after authentication when the app is in use.</span></span> <span data-ttu-id="dec49-106">Pour savoir comment déterminer si un jeton est arrivé à expiration, consultez [Rechercher les jetons d'authentification expirés](http://aka.ms/jww5vp).</span><span class="sxs-lookup"><span data-stu-id="dec49-106">To learn how to determine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="dec49-107">Pour une solution permettant de gérer les erreurs d'autorisation liées à des jetons expirés, consultez le post [Mise en cache et gestion des jetons expirés dans le Kit de développement logiciel (SDK) managé d'Azure Mobile Services](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="dec49-107">For a solution to handling authorization errors related to expiring tokens, see the post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="dec49-108">Redémarrez l'application deux fois.</span><span class="sxs-lookup"><span data-stu-id="dec49-108">Restart the app twice.</span></span>
   
    <span data-ttu-id="dec49-109">Notez que lors du premier démarrage, la connexion avec le fournisseur est à nouveau requise.</span><span class="sxs-lookup"><span data-stu-id="dec49-109">Notice that on the first start-up, sign-in with the provider is again required.</span></span> <span data-ttu-id="dec49-110">Cependant, lors du second redémarrage, les informations d'identification mises en cache sont utilisées et l'étape de connexion est ignorée.</span><span class="sxs-lookup"><span data-stu-id="dec49-110">However, on the second restart the cached credentials are used and sign-in is bypassed.</span></span> 

