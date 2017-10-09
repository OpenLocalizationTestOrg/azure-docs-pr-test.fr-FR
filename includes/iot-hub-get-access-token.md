## <a name="obtain-an-azure-resource-manager-token"></a>Obtenir un jeton Azure Resource Manager
Azure Active Directory doit authentifier toutes les tâches hello que vous effectuez sur les ressources à l’aide de hello Azure Resource Manager. Hello exemple indiqué ici utilise l’authentification du mot de passe, pour d’autres approches, consultez [demande d’authentification Azure Resource Manager][lnk-authenticate-arm].

1. Ajouter hello suivant code toohello **Main** méthode dans Program.cs tooretrieve un jeton d’Azure AD à l’aide des id de l’application hello et le mot de passe.
   
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
2. Créer un **ResourceManagementClient** de l’objet qu’utilise hello jeton en ajoutant hello suivant fin toohello de code Hello **Main** méthode :
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. Créer ou obtenir une référence au groupe de ressources hello que vous utilisez :
   
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