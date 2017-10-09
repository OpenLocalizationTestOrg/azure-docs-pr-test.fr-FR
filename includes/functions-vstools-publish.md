1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et sélectionnez **publier**. Choisissez **Créer** puis cliquez sur **Publier**. 

    ![Publier une nouvelle application de fonction](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. Si vous n’avez pas déjà connecté Visual Studio tooyour compte Azure, cliquez sur **ajouter un compte...** .  

3. Bonjour **créer un Service application** boîte de dialogue, utilisez hello **hébergement** paramètres comme spécifié dans hello tableau suivant : 

    ![Azure runtime local](./media/functions-vstools-publish/functions-vstools-publish.png)

    | Paramètre      | Valeur suggérée  | Description                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nom de l’application** | Nom globalement unique | Nom qui identifie uniquement votre nouvelle application de fonction. |
    | **Abonnement** | Choisissez votre abonnement | toouse d’abonnement Azure Hello. |
    | **[Groupe de ressources](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  Nom de ressource de hello regrouper dans le toocreate votre application de la fonction. |
    | **[Plan App Service](../articles/azure-functions/functions-scale.md)** | Plan de consommation | Assurez-vous que toochoose hello **consommation** sous **taille** lorsque vous créez un nouveau plan.  |
    | **[Compte de stockage](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | Nom globalement unique | Utilisez un compte de stockage existant ou créez-en un.   |

4. Cliquez sur **créer** toocreate une application de la fonction dans Azure avec ces paramètres. Après l’approvisionnement de hello, prenez note de hello **URL du Site** valeur, qui est l’adresse hello de votre application de la fonction dans Azure. 

    ![Azure runtime local](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
