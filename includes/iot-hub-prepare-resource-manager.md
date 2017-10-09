## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Préparer tooauthenticate demande du Gestionnaire de ressources Azure
Vous devez vous authentifier toutes les opérations de hello que vous effectuez sur les ressources à l’aide de hello [Azure Resource Manager] [ lnk-authenticate-arm] avec Azure Active Directory (AD). Hello tooconfigure de façon plus simple Voici toouse PowerShell ou CLI d’Azure.

Installer hello [applets de commande Azure PowerShell] [ lnk-powershell-install] avant de continuer.

Hello suivant les étapes indiquent comment tooset l’authentification du mot de passe pour une application AD à l’aide de PowerShell. Vous pouvez exécuter ces commandes dans le cadre d’une session PowerShell standard.

1. Ouvrez une session dans tooyour abonnement Azure à l’aide de hello de commande suivante :

    ```powershell
    Login-AzureRmAccount
    ```

1. Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello Azure abonnements associés à vos informations d’identification. Utilisez hello toolist hello abonnements Azure disponibles pour vous toouse de commande suivante :

    ```powershell
    Get-AzureRMSubscription
    ```

    Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toomanage votre hub IoT. Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Prenez note des valeurs **TenantId** et **SubscriptionId**. Vous en aurez besoin ultérieurement.
3. Créer une nouvelle application Azure Active Directory à l’aide de hello commande suivante, en remplaçant les espaces réservés hello :
   
   * **{Nom d’affichage} :** nom d’affichage pour votre application, par exemple, **MySampleApp**
   * **{URL de la page d’accueil} :** hello telles que les URL de page d’accueil hello de votre application **http://mysampleapp/home**. Cette URL ne doit pas toopoint tooa véritable application.
   * **{Identificateur d’application} :** identificateur unique, par exemple, **http://mysampleapp**. Cette URL ne doit pas toopoint tooa véritable application.
   * **{Password} :** un mot de passe que vous utilisez tooauthenticate avec votre application.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Prenez note de hello **ApplicationId** de l’application hello que vous avez créé. Vous en aurez besoin ultérieurement.
5. Créer une nouvelle entité de service à l’aide de hello commande suivante, en remplaçant **{MyApplicationId}** avec hello **ApplicationId** à partir de l’étape précédente de hello :
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Configurer une attribution de rôle à l’aide de hello commande suivante, en remplaçant **{MyApplicationId}** avec votre **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Vous avez terminé de création d’application Azure AD hello qui vous permet de tooauthenticate à partir de votre application c# personnalisée. Vous devez hello valeurs suivantes plus loin dans ce didacticiel :

* TenantId
* SubscriptionId
* ApplicationId
* Mot de passe

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
