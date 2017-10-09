### <a name="prerequisites"></a>Composants requis
* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [compte de stockage d’objets Blob Azure](../articles/storage/common/storage-create-storage-account.md) , y compris le nom de compte de stockage hello et sa clé d’accès. Ces informations sont répertoriées dans les propriétés de hello hello du compte de stockage Bonjour portail Azure. Pour en savoir plus, consultez [Introduction à Azure Storage](../articles/storage/common/storage-introduction.md).

Avant d’utiliser votre compte de stockage d’objets Blob Azure dans une application logique, connectez le compte de stockage d’objets Blob Azure de tooyour. Vous pouvez effectuer cela facilement au sein de votre application logique sur hello portail Azure.  

Se connecter tooyour compte de stockage d’objets Blob Azure à l’aide de hello comme suit :  

1. Créez une application logique. Dans le concepteur hello Logic Apps, ajouter un déclencheur, puis ajoutez une action. Sélectionnez **Microsoft d’afficher les API managées** Bonjour liste déroulante, puis entrez « blob » dans la zone de recherche hello. Sélectionnez une des actions de hello :  
   
    ![Étape de création de la connexion au stockage d’objets blob Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. Si vous n’avez pas précédemment créé toutes les connexions tooAzure stockage, vous êtes invité hello détails de connexion :   
   
    ![Étape de création de la connexion au stockage d’objets blob Azure](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. Entrez les détails de compte de stockage hello. Les propriétés marquées d’un astérisque sont obligatoires.
   
   | Propriété | Détails |
   | --- | --- |
   | Nom de connexion * |Entrez un nom pour votre connexion. |
   | Nom du compte de stockage Azure * |Entrez le nom de compte de stockage hello. nom de compte de stockage Hello s’affiche dans les propriétés de stockage hello Bonjour portail Azure. |
   | Clé d’accès au compte de stockage * |Entrez la clé de compte de stockage hello. clés d’accès Hello sont affichent dans les propriétés de stockage hello Bonjour portail Azure. |
   
    Ces informations d’identification sont utilisée tooauthorize votre tooconnect d’application logique et accéder à vos données. 
4. Sélectionnez **Créer**.
5. Avis hello connexion a été créée. Maintenant, hello autres étapes dans votre logique d’application : 
   
    ![Étape de création de la connexion au stockage d’objets blob Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

