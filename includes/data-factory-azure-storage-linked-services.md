### <a name="azure-storage-linked-service"></a>Service lié Stockage Azure
Hello **service lié Azure Storage** vous permet de toolink une fabrique de données Azure tooan compte stockage Azure à l’aide de hello **clé de compte**, fournit une fabrique de données hello avec accès global toohello Azure Stockage. Hello tableau suivant fournit la description pour JSON éléments tooAzure spécifique lié Storage service.

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type |propriété de type Hello doit indiquer : **AzureStorage** |Oui |
| connectionString |Spécifiez les informations nécessaires tooconnect tooAzure stockage pour la propriété connectionString de hello. |Oui |

Consultez hello suivant de l’article pour la clé de compte hello étapes tooview/copie pour un stockage Azure : [afficher, copier et régénérer stockage clés d’accès](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).

**Exemple :**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Service lié SAP Azure Storage
Une signature d’accès partagé (SAS) fournit tooresources accès délégué dans votre compte de stockage. Il permet de vous toogrant un client limitée tooobjects autorisations dans votre compte de stockage pour une période de temps et avec un jeu d’autorisations, spécifié sans avoir tooshare vos clés d’accès de compte. Hello SAS est un URI qui englobe dans ses paramètres de requête, toutes les informations de hello nécessaires pour la ressource de stockage tooa un accès authentifié. tooaccess des ressources de stockage avec hello SAS, hello client a uniquement besoin toopass dans le constructeur approprié de hello SAS toohello ou la méthode. Pour plus d’informations sur SAS, consultez [Signatures d’accès partagé : hello de présentation modèle SAP](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> Azure Data Factory prend maintenant uniquement en charge la **signature d’accès partagé SAS**, et pas la signature d’accès partagé du compte. Consultez [Types de Signatures d’accès partagé](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) pour plus d’informations sur ces deux types et comment tooconstruct. Remarque : hello URL SAS generable à partir du portail Azure ou l’Explorateur de stockage est un compte SAP, ce qui n’est pas pris en charge.
> 

Hello SAS de stockage Azure lié service vous permet de toolink une fabrique de données Azure tooan compte de stockage Azure à l’aide d’une Signature d’accès partagé (SAS). Il fournit des fabrique de données hello avec l’accès restreint/limitées dans le temps de tooall/spécifiques des ressources (objet blob/conteneur) dans le stockage hello. Hello tableau suivant fournit la description pour JSON éléments tooAzure spécifique SAS de stockage lié service. 

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| type |propriété de type Hello doit indiquer : **AzureStorageSas** |Oui |
| sasUri |Spécifier des ressources de stockage Azure toohello URI de Signature d’accès partagé comme objet blob, conteneur ou une table.  |Oui |

**Exemple :**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

Lorsque vous créez un **URI SAS**, envisagez suivant de hello :  

* Définir en lecture/écriture appropriées **autorisations** sur les objets en fonction de comment hello lié service (lecture, écriture, lecture/écriture) est utilisé dans votre fabrique de données.
* Définissez le paramètre **Heure d’expiration** correctement. Assurez-vous que les objets de stockage hello accès tooAzure n’expire pas pendant la période active hello pipeline de hello.
* URI doit être créé en hello droite conteneur/blob ou le niveau de Table en fonction de hello nécessaire. Un objet blob Azure de tooan Uri SAS permet hello Data Factory service tooaccess cet objet blob particulier. Un conteneur d’objets blob Azure de tooan Uri SAS permet hello Data Factory service tooiterate via des objets BLOB dans le conteneur. Si vous avez besoin de tooprovide accès plus/moins d’objets plus tard, ou de mise à jour hello SAS URI, n’oubliez pas de service de hello lié tooupdate avec hello nouvel URI.   

