## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a>Préparation de l’authentification des demandes d’Azure Resource Manager
Vous devez authentifier toutes les opérations que vous effectuez sur des ressources à l’aide d’[Azure Resource Manager][lnk-authenticate-arm] avec Azure Active Directory (AD). La manière la plus simple de configurer cela consiste à utiliser PowerShell ou l’interface de ligne de commande Azure.

Avant toute chose, installez les [applets de commande Azure PowerShell][lnk-powershell-install].

Les étapes suivantes montrent comment configurer l’authentification par mot de passe pour une application Active Directory à l’aide de PowerShell. Vous pouvez exécuter ces commandes dans le cadre d’une session PowerShell standard.

1. Pour vous connecter à votre abonnement Azure, exécutez la commande suivante :

    ```powershell
    Login-AzureRmAccount
    ```

1. Si vous possédez plusieurs abonnements Azure, la connexion à Azure vous donne accès à tous les abonnements Azure associés à vos informations d’identification. Utilisez la commande suivante pour répertorier les abonnements Azure que vous pouvez utiliser :

    ```powershell
    Get-AzureRMSubscription
    ```

    Utilisez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser afin d'exécuter les commandes pour gérer votre IoT Hub. Vous pouvez utiliser le nom de l’abonnement ou l’ID de la sortie de la commande précédente :

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Prenez note des valeurs **TenantId** et **SubscriptionId**. Vous en aurez besoin ultérieurement.
3. Créez une application Azure Active Directory à l’aide de la commande suivante, en remplaçant les espaces réservés :
   
   * **{Nom d’affichage} :** nom d’affichage pour votre application, par exemple, **MySampleApp**
   * **{URL de la page d’accueil} :** URL de la page d’accueil de votre application, par exemple, **http://mysampleapp/home**. Cette URL n’a pas besoin de pointer vers une application réelle.
   * **{Identificateur d’application} :** identificateur unique, par exemple, **http://mysampleapp**. Cette URL n’a pas besoin de pointer vers une application réelle.
   * **{Mot de passe} :** mot de passe que vous utiliserez pour vous authentifier dans votre application.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Prenez note de l’ **ApplicationId** de l’application que vous avez créée. Vous en aurez besoin ultérieurement.
5. Créez un principal de service à l’aide de la commande suivante, en remplaçant **{MyApplicationId}** par **l’ApplicationId** de l’étape précédente :
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Configurez une attribution de rôle à l’aide de la commande suivante, en remplaçant **{MyApplicationId}** par votre **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Vous avez maintenant créé l’application Azure AD qui vous permet de vous authentifier à partir de votre application C#. Vous aurez besoin des valeurs suivantes plus loin dans ce didacticiel :

* TenantId
* SubscriptionId
* ApplicationId
* Mot de passe

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
