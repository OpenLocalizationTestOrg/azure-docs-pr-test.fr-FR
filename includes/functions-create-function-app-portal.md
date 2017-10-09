1. Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

1. Cliquez sur **Calcul** > **Function App**, sélectionnez votre **Abonnement**. Ensuite, utilisez les paramètres de l’application hello fonction comme spécifié dans la table de hello.

    ![Créer l’application de la fonction Bonjour portail Azure](./media/functions-create-function-app-portal/function-app-create-flow.png)

    | Paramètre      | Valeur suggérée  | Description                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nom de l’application** | Nom globalement unique | Nom qui identifie votre nouvelle Function App. | 
    | **[Groupe de ressources](../articles/azure-resource-manager/resource-group-overview.md)** |  myResourceGroup | Nom de votre application de la fonction pour hello nouveau groupe de ressources dans le toocreate. | 
    | **[Plan d’hébergement](../articles/azure-functions/functions-scale.md)** |   Plan de consommation | Plan d’hébergement qui définit comment les ressources sont allouées tooyour fonction app. Dans la valeur par défaut hello **consommation Plan**, les ressources sont ajoutées dynamiquement comme requis par vos fonctions. Vous payez uniquement pour hello exécution de vos fonctions.   |
    | **Emplacement** | Europe de l’Ouest | Choisissez un emplacement près de chez vous ou près d’autres services auxquels vos fonctions accéderont. |
    | **[Compte de stockage](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** |  Nom globalement unique |  Nom du nouveau compte de stockage hello utilisé par votre application de la fonction. Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres. Vous pouvez également utiliser un compte existant. |

1. Cliquez sur **créer** tooprovision et déployer la nouvelle application de fonction hello.
