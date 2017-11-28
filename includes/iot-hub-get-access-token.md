## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="09e6d-101">Obtenir un jeton Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="09e6d-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="09e6d-102">Azure Active Directory doit authentifier toutes les tâches que vous effectuez sur des ressources à l’aide d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="09e6d-102">Azure Active Directory must authenticate all the tasks that you perform on resources using the Azure Resource Manager.</span></span> <span data-ttu-id="09e6d-103">L’exemple présenté ici utilise une authentification par mot de passe. Pour d’autres approches, consultez [Demandes d’authentification Azure Resource Manager][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="09e6d-103">The example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="09e6d-104">Ajoutez le code suivant à la méthode **Main** dans le fichier Program.cs pour récupérer un jeton d’Azure AD à l’aide de l’ID d’application et d’un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="09e6d-104">Add the following code to the **Main** method in Program.cs to retrieve a token from Azure AD using the application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed to obtain the token");
      return;
    }
    ```
2. <span data-ttu-id="09e6d-105">Créez un objet **ResourceManagementClient** qui utilise le jeton en ajoutant le code suivant à la fin de la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="09e6d-105">Create a **ResourceManagementClient** object that uses the token by adding the following code to the end of the **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="09e6d-106">Créez ou obtenez une référence au groupe de ressources que vous utilisez :</span><span class="sxs-lookup"><span data-stu-id="09e6d-106">Create, or obtain a reference to, the resource group you are using:</span></span>
   
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