## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="53db0-101">Obtenir un jeton Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="53db0-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="53db0-102">Azure Active Directory doit authentifier toutes les tâches hello que vous effectuez sur les ressources à l’aide de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="53db0-102">Azure Active Directory must authenticate all hello tasks that you perform on resources using hello Azure Resource Manager.</span></span> <span data-ttu-id="53db0-103">Hello exemple indiqué ici utilise l’authentification du mot de passe, pour d’autres approches, consultez [demande d’authentification Azure Resource Manager][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="53db0-103">hello example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="53db0-104">Ajouter hello suivant code toohello **Main** méthode dans Program.cs tooretrieve un jeton d’Azure AD à l’aide des id de l’application hello et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="53db0-104">Add hello following code toohello **Main** method in Program.cs tooretrieve a token from Azure AD using hello application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. <span data-ttu-id="53db0-105">Créer un **ResourceManagementClient** de l’objet qu’utilise hello jeton en ajoutant hello suivant fin toohello de code Hello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="53db0-105">Create a **ResourceManagementClient** object that uses hello token by adding hello following code toohello end of hello **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="53db0-106">Créer ou obtenir une référence au groupe de ressources hello que vous utilisez :</span><span class="sxs-lookup"><span data-stu-id="53db0-106">Create, or obtain a reference to, hello resource group you are using:</span></span>
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx