---
title: "tooand de données aaaCopy à partir d’Azure Data Lake Store | Documents Microsoft"
description: "Découvrez comment toocopy tooand de données à partir de Data Lake Store à l’aide d’Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>Copier des données tooand à partir de Data Lake Store à l’aide de Data Factory
Cet article explique comment toouse l’activité de copie dans Azure Data Factory toomove données tooand à partir d’Azure Data Lake Store. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) de l’article, une vue d’ensemble du mouvement des données avec l’activité de copie.

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez copier des données **à partir d’Azure Data Lake Store** toohello suivant des magasins de données :

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Vous pouvez copier des données à partir de hello suivant des magasins de données **tooAzure Data Lake Store**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Créez un compte Data Lake Store avant de créer un pipeline avec activité de copie. Pour plus d’informations, consultez [Prise en main d’Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a>Types d’authentification pris en charge
connecteur de Data Lake Store Hello prend en charge ces types d’authentification :
* Authentification d’un principal du service
* Utilisation de l’authentification des informations d’identification utilisateur (OAuth) 

Nous vous recommandons d’utiliser l’authentification de principal du service, en particulier pour une copie planifiée des données. Un comportement d’expiration de jeton peut se produire avec l’authentification par informations d’identification utilisateur. Pour plus d’informations, consultez hello [lié des propriétés du service](#linked-service-properties) section.

## <a name="get-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers ou à partir d’Azure Data Lake Store à l’aide de différents outils/API.

toocreate de façon plus simple Hello une données toocopy de pipeline est toouse hello **Assistant copie de**. Pour obtenir un didacticiel sur la création d’un pipeline à l’aide d’Assistant copie de hello, consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md).

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Création d'une **fabrique de données**. Une fabrique de données peut contenir un ou plusieurs pipelines. 
2. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins. Par exemple, si vous copiez des données à partir d’un tooan de stockage d’objets blob Azure Azure Data Lake Store, vous créez deux services liés toolink votre compte de stockage et de la fabrique de données Azure Data Lake store tooyour. Pour les propriétés de service lié qui sont spécifique tooAzure Data Lake Store, consultez [lié des propriétés du service](#linked-service-properties) section. 
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello. De plus, vous créez un autre jeu de données toospecify hello dossier et le fichier de chemin d’accès dans le magasin Data Lake hello qui contient les données hello copiées à partir du stockage d’objets blob hello. Pour les propriétés du dataset qui sont spécifique tooAzure Data Lake Store, consultez [propriétés du dataset](#dataset-properties) section.
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et AzureDataLakeStoreSink comme un récepteur pour l’activité de copie hello. De même, si vous copiez à partir d’Azure Data Lake Store tooAzure stockage d’objets Blob, vous utilisez AzureDataLakeStoreSource et BlobSink dans l’activité de copie hello. Pour les propriétés d’activité de copie qui sont spécifique tooAzure Data Lake Store, consultez [copier les propriétés de l’activité](#copy-activity-properties) section. Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.  

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/depuis une Azure Data Lake Store, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) section de cet article.

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisé toodefine Data Factory entités spécifiques tooData Lake Store.

## <a name="linked-service-properties"></a>Propriétés du service lié
Un service lié lie une fabrique de données de tooa de magasin de données. Vous créez un service lié de type **AzureDataLakeStore** toolink votre fabrique de données tooyour données Data Lake Store. Hello tableau suivant décrit les services JSON éléments spécifiques tooData Lake Store lié. Vous pouvez choisir entre une authentification par principal de service et par informations d’identification utilisateur.

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| **type** | propriété de type Hello doit être définie trop**AzureDataLakeStore**. | Oui |
| **dataLakeStoreUri** | Informations sur hello compte Azure Data Lake Store. Ces informations prennent l’une des hello suivant formats : `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`. | Oui |
| **subscriptionId** | Hello de toowhich ID abonnement Azure compte Data Lake Store appartient. | Requis pour le récepteur |
| **resourceGroupName** | Hello de toowhich de nom de groupe ressource Azure compte Data Lake Store appartient. | Requis pour le récepteur |

### <a name="service-principal-authentication-recommended"></a>Authentification d’un principal du service (recommandée)
authentification principale du service toouse, inscrire une entité de l’application dans Azure Active Directory (Azure AD) et accordez à elle hello accéder à tooData Lake Store. Consultez la page [Authentification de service à service](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) pour des instructions détaillées. Prenez note de hello après les valeurs que vous pouvez utiliser toodefine hello de service lié :
* ID de l'application
* Clé de l'application 
* ID client

> [!IMPORTANT]
> Si vous utilisez des pipelines de données hello Assistant copie tooauthor, assurez-vous que vous accordez principal du service hello au moins un **lecteur** rôle dans le contrôle d’accès (gestion des identités et des accès) pour le compte de hello Data Lake Store. En outre, au moins accorder principal du service hello **lecture + Execute** racine de Data Lake Store tooyour autorisation (« / ») et ses enfants. Dans le cas contraire, vous pouvez voir le message de salutation « hello informations d’identification fournies ne sont pas valides. »<br/><br/>
Une fois que vous créez ou mettez à jour un principal de service dans Azure AD, il peut prendre quelques minutes pour effet de tootake modifications hello. Vérifiez le principal du service hello et configurations de liste (ACL) du contrôle de l’accès Data Lake Store. Si vous voyez toujours le message « hello informations d’identification fournies ne sont pas valides » de type hello, patientez et réessayez.

Utilisez l’authentification principale du service en spécifiant hello propriétés suivantes :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| **servicePrincipalId** | Spécifiez l’ID client de. l’application hello | Oui |
| **servicePrincipalKey** | Spécifiez la clé de l’application hello. | Oui |
| **client** | Spécifiez les informations de locataire hello (ID client ou le nom de domaine) dans lequel réside votre application. Vous pouvez le récupérer par pointage de souris hello dans le coin supérieur droit de hello Hello portail Azure. | Oui |

**Exemple : authentification du principal de service**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Authentification des informations d’identification utilisateur
Ou bien, vous pouvez utiliser des toocopy de l’authentification des informations d’identification utilisateur à partir d’ou tooData Lake Store en spécifiant hello propriétés suivantes :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| **authorization** | Cliquez sur hello **Authorize** bouton Bonjour éditeur Data Factory et entrez vos informations d’identification qui affecte le propriété toothis URL hello générées automatiquement d’autorisation. | Oui |
| **sessionId** | ID de session OAuth à partir de la session de d’autorisation OAuth hello. Chaque ID de session est unique et ne peut être utilisé qu’une seule fois. Ce paramètre est automatiquement généré lorsque vous utilisez hello éditeur Data Factory. | Oui |

**Exemple : authentification des informations d’identification utilisateur**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiration du jeton
Hello code d’autorisation que vous avez généré à l’aide de hello **Authorize** bouton expire après un certain temps. Hello suivant message signifie que ce jeton d’authentification hello a expiré :

Credential operation error: invalid_grant - AADSTS70002: Error validating credentials. AADSTS70008 : hello fourni octroi d’accès est expiré ou révoqué. Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.

Hello tableau suivant montre des délais d’expiration hello de différents types de comptes d’utilisateur :


| Type d’utilisateur | Expire après |
|:--- |:--- |
| Comptes d’utilisateurs *non* gérés par Azure Active Directory (par exemple @hotmail.com ou @live.com) |12 heures |
| Comptes d’utilisateurs gérés par Azure Active Directory |exécution de 14 jours après la dernière tranche de hello <br/><br/>90 jours, si une tranche basée sur un service lié OAuth est exécutée au moins une fois tous les 14 jours |

Si vous modifiez votre mot de passe avant l’heure d’expiration du jeton de hello, jeton de hello expire immédiatement. Vous verrez un message de type hello mentionné plus haut dans cette section.

Vous pouvez autoriser à nouveau le compte de hello à l’aide de hello **Authorize** bouton lors de l’expiration du jeton d’hello tooredeploy hello de service lié. Vous pouvez également générer des valeurs pour hello **sessionId** et **autorisation** propriétés par programme à l’aide hello code suivant :


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
Pour plus d’informations sur les classes de fabrique de données hello utilisées dans le code hello, consultez hello [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), et [ Classe de AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) rubriques. Ajouter une référence tooversion `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` pour hello `WindowsFormsWebAuthenticationDialog` classe utilisée dans le code hello.

## <a name="dataset-properties"></a>Propriétés du jeu de données
toospecify un toorepresent jeu de données d’entrée de données dans un magasin Data Lake Store, vous définissez hello **type** propriété du jeu de données hello trop**AzureDataLakeStore**. Ensemble hello **linkedServiceName** service lié de propriété du nom de toohello hello dataset Hello Data Lake Store. Pour obtenir une liste complète des sections JSON et les propriétés disponibles pour la définition de jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections d’un jeu de données en JSON, comme la **structure**, la **disponibilité** et la **stratégie** sont similaires pour tous les types de jeux de données (par exemple, Azure SQL Database, Azure Blob et Azure Table). Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations telles que l’emplacement et le format de données hello dans le magasin de données hello. 

Hello **typeProperties** section pour un jeu de données de type **AzureDataLakeStore** contient hello propriétés suivantes :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| **folderPath** |Conteneur toohello de chemin d’accès et le dossier de Data Lake Store. |Oui |
| **fileName** |Nom du fichier hello dans Azure Data Lake Store. Hello **nom de fichier** propriété est facultative et respecte la casse. <br/><br/>Si vous spécifiez **nom de fichier**, activité hello (y compris la copie) fonctionne sur un fichier spécifique hello.<br/><br/>Lorsque **nom de fichier** n’est pas spécifié, copie inclut tous les fichiers dans **folderPath** hello de jeu de données d’entrée.<br/><br/>Lorsque **nom de fichier** n’est pas spécifié pour un dataset de sortie et **preserveHierarchy** n’est pas spécifié dans le récepteur d’activité, nom hello du fichier de hello généré est au format de hello données. _GUID_.txt ». Par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt. |Non |
| **partitionedBy** |Hello **partitionedBy** propriété est facultative. Vous pouvez l’utiliser toospecify un chemin d’accès dynamique et le nom de fichier de données de série chronologique. Par exemple, **folderPath** peut être paramétré pour toutes les heures de données. Pour plus d’informations et d’exemples, consultez [hello partitionedBy propriété](#using-partitionedby-property). |Non |
| **format** | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, et  **ParquetFormat**. Ensemble hello **type** propriété sous **format** tooone de ces valeurs. Pour plus d’informations, consultez hello [au format texte](data-factory-supported-file-and-compression-formats.md#text-format), [format JSON](data-factory-supported-file-and-compression-formats.md#json-format), [le format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format ORC](data-factory-supported-file-and-compression-formats.md#orc-format), et [Parquet Format ](data-factory-supported-file-and-compression-formats.md#parquet-format) sections Bonjour [les formats de fichiers et de compression pris en charge par Azure Data Factory](data-factory-supported-file-and-compression-formats.md) l’article. <br><br> Si vous souhaitez que les fichiers toocopy » en tant que-est « entre des magasins basée sur le fichier (copie binaire), ignorer hello `format` section dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| **compression** | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

### <a name="hello-partitionedby-property"></a>propriété de partitionedBy Hello
Vous pouvez spécifier dynamique **folderPath** et **nom de fichier** propriétés pour les données de série chronologique par hello **partitionedBy** propriété, les fonctions de la fabrique de données et système variables. Pour plus d’informations, consultez hello [Azure Data Factory - fonctions et variables système](data-factory-functions-variables.md) l’article.


Bonjour, l’exemple suivant `{Slice}` est remplacée par la valeur hello de variable de système de Data Factory hello `SliceStart` au format hello spécifié (`yyyyMMddHH`). nom de Hello `SliceStart` fait référence toohello heure de début de la tranche de hello. Hello `folderPath` propriété est différente pour chaque secteur, comme dans `wikidatagateway/wikisampledataout/2014100103` ou `wikidatagateway/wikisampledataout/2014100104`.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Bonjour suivant l’exemple, hello année, mois, jour et temps de `SliceStart` sont extraits dans des variables distinctes qui sont utilisés par hello `folderPath` et `fileName` propriétés :
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Pour plus d’informations sur les jeux de données de série chronologique, en planifiant et en secteurs, consultez hello [jeux de données dans Azure Data Factory](data-factory-create-datasets.md) et [planification de la fabrique de données et l’exécution](data-factory-scheduling-and-execution.md) articles. 


## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.

Hello propriétés disponibles dans hello **typeProperties** section d’une activité varient selon chaque type d’activité. Pour une activité de copie, ils varient selon les types de sources et récepteurs hello.

**AzureDataLakeStoreSource** prend en charge hello suivant propriété Bonjour **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| **recursive** |Indique si les données de salutation sont lu de manière récursive des sous-dossiers de hello ou uniquement à partir de dossier spécifié de hello. |True (valeur par défaut), False |Non |


**AzureDataLakeStoreSink** prend en charge hello propriétés Bonjour suivantes **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| **copyBehavior** |Spécifie le comportement de copie hello. |<b>PreserveHierarchy</b>: préserve la hiérarchie des fichiers dans le dossier cible de hello hello. chemin d’accès relatif de Hello du dossier source du fichier toosource est identique toohello un chemin d’accès relatif du dossier tootarget de fichier cible.<br/><br/><b>FlattenHierarchy</b>: tous les fichiers à partir du dossier source hello sont créés dans hello premier niveau du dossier cible de hello. les fichiers cibles Hello sont créés avec des noms générés automatiquement.<br/><br/><b>MergeFiles</b>: fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello. Si hello nom de fichier ou un objet blob est spécifié, nom de fichier fusionné hello désigne hello spécifié. Dans le cas contraire, le nom de fichier hello est généré automatiquement. |Non |

### <a name="recursive-and-copybehavior-examples"></a>exemples de valeurs recursive et copyBehavior
Cette section décrit le comportement qui en résulte de hello d’opération de copie hello pour différentes combinaisons de valeurs récursive et copyBehavior.

| recursive | copyBehavior | Comportement résultant |
| --- | --- | --- |
| true |preserveHierarchy |Pour un dossier source Dossier1 avec hello suivant structure : <br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>dossier cible de Hello Dossier1 est créée avec hello même structure en tant que source de hello<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5. |
| true |flattenHierarchy |Pour un dossier source Dossier1 avec hello suivant structure : <br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>cible de Hello Dossier1 est créée avec hello suivant structure : <br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier5 |
| true |mergeFiles |Pour un dossier source Dossier1 avec hello suivant structure : <br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>cible de Hello Dossier1 est créée avec hello suivant structure : <br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 + Fichier3 + Fichier4 + Fichier5 est fusionné dans un fichier avec le nom de fichier généré automatiquement |
| false |preserveHierarchy |Pour un dossier source Dossier1 avec hello suivant structure : <br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>dossier cible de Hello Dossier1 est créée avec hello suivant de structure<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/><br/><br/>Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés. |
| false |flattenHierarchy |Pour un dossier source Dossier1 avec hello suivant structure :<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>dossier cible de Hello Dossier1 est créée avec hello suivant de structure<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2<br/><br/><br/>Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés. |
| false |mergeFiles |Pour un dossier source Dossier1 avec hello suivant structure :<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>dossier cible de Hello Dossier1 est créée avec hello suivant de structure<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 est fusionné dans un fichier avec le nom de fichier généré automatiquement. nom généré automatiquement pour Fichier1<br/><br/>Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés. |

## <a name="supported-file-and-compression-formats"></a>Formats de fichier et de compression pris en charge
Pour plus d’informations, consultez hello [des formats de fichiers et de compression dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md) l’article.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>Exemples JSON pour la copie des données tooand Data Lake Store
Hello exemple suivant fournit des exemples de définitions de JSON. Vous pouvez utiliser ces toocreate de définitions exemple un pipeline à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hello exemples montrent comment tooand de données toocopy à partir du stockage Data Lake Store et les objets Blob Azure. Toutefois, les données peuvent être copiées _directement_ de n’importe quelle tooany de sources hello de récepteurs de hello pris en charge. Pour plus d’informations, consultez la section hello « magasins de données pris en charge et formats » dans hello [déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md) l’article.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>Exemple : Copier des données à partir de tooAzure de stockage d’objets Blob Azure Data Lake Store
exemple de code Hello dans cette section montre :

* Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un service lié de type [AzureDataLakeStore](#linked-service-properties).
* Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureDataLakeStore](#dataset-properties).
* Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [AzureDataLakeStoreSink](#copy-activity-properties).

Hello exemples montrent comment série chronologique de données à partir du stockage d’objets Blob Azure sont copiés tooData Lake Store toutes les heures. 

**Service lié Azure Storage**

```JSON
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

**Service lié Azure Data Lake Store**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> Pour plus d’informations, consultez hello [lié des propriétés du service](#linked-service-properties) section.
>

**Jeu de données d'entrée d'objet Blob Azure**

Dans l’exemple suivant de hello, données sont récupérées à partir d’un nouvel objet blob toutes les heures (`"frequency": "Hour", "interval": 1`). nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise hello year, month et composante jour d’heure de début hello. nom de fichier Hello utilise heure hello heure de début de la partie de hello. Hello `"external": true` paramètre informe le service de fabrique de données hello cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Jeu de données de sortie Azure Data Lake Store**

Hello suivant exemple copies données tooData Lake Store. Les nouvelles données sont copiées tooData Lake Store toutes les heures.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Activité de copie dans un pipeline avec une source Blob et un récepteur Data Lake Store**

Dans l’exemple suivant de hello, pipeline de hello contient une activité de copie qui est configurée toouse hello des jeux de données d’entrée et de sortie. activité de copie Hello est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello `source` type est défini trop`BlobSource`et hello `sink` type est défini trop`AzureDataLakeStoreSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
        ]
    }
}
```

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>Exemple : Copier des données à partir d’Azure Data Lake Store tooan objets blob Azure
exemple de code Hello dans cette section montre :

* Un service lié de type [AzureDataLakeStore](#linked-service-properties).
* Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureDataLakeStore](#dataset-properties).
* Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [AzureDataLakeStoreSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

code de Hello copie les données de série chronologique Data Lake Store tooan objets blob Azure toutes les heures. 

**Service lié Azure Data Lake Store**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> Pour plus d’informations, consultez hello [lié des propriétés du service](#linked-service-properties) section.
>

**Service lié Azure Storage**

```JSON
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
**Jeu de données Azure Data Lake de sortie**

Dans cet exemple, le paramètre `"external"` trop`true` informe le service de fabrique de données hello cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
        "policy": {
              "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
              }
        }
      }
}
```
**Jeu de données de sortie d’objet Blob Azure**

Bonjour l’exemple suivant, les données sont écrites tooa nouvel objet blob toutes les heures (`"frequency": "Hour", "interval": 1`). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise hello année, mois, jour et heures d’heure de début hello.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Activité de copie dans un pipeline avec une source Azure Data Lake Store et un récepteur Blob**

Dans l’exemple suivant de hello, pipeline de hello contient une activité de copie qui est configurée toouse hello des jeux de données d’entrée et de sortie. activité de copie Hello est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello `source` type est défini trop`AzureDataLakeStoreSource`et hello `sink` type est défini trop`BlobSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

Dans la définition d’activité hello copie, vous pouvez également mapper des colonnes de hello toocolumns de jeu de données source dans le jeu de données récepteur hello. Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performances et réglage
toolearn sur les facteurs hello qui affectent les performances de l’activité de copie et la manière dont toooptimize, consultez hello [l’activité de copie guide des performances et paramétrage](data-factory-copy-activity-performance.md) l’article.
