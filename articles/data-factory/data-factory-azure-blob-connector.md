---
title: "données aaaCopy vers/depuis le stockage d’objets Blob Azure | Documents Microsoft"
description: "Découvrez comment toocopy blob des données dans Azure Data Factory. Utilisez notre exemple : comment tooand de données toocopy à partir de la base de données SQL Azure et de stockage d’objets Blob Azure."
keywords: "données d’objets blob, copie d’objet blob azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>Tooor de données de copie à partir du stockage d’objets Blob Azure à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie dans Azure Data Factory toocopy données tooand à partir du stockage d’objets Blob Azure. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

## <a name="overview"></a>Vue d'ensemble
Vous pouvez copier les données de toute source pris en charge de données tooAzure stockage d’objets Blob de stockage ou à partir des données de récepteur tooany pris en charge de stockage d’objets Blob Azure stockage. Hello tableau suivant fournit une liste des banques de données pris en charge en tant que sources ou récepteurs par l’activité de copie hello. Par exemple, vous pouvez déplacer des données **depuis** une base de données SQL Server ou une base de données Azure SQL Database **vers** un stockage Blob Azure. Et vous pouvez copier des données **depuis** un stockage Blob Azure **vers** un entrepôt Azure SQL Data Warehouse ou une collection Azure Cosmos DB. 

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez copier des données **à partir du stockage d’objets Blob Azure** toohello suivant des magasins de données :

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Vous pouvez copier des données à partir de hello suivant des magasins de données **tooAzure stockage d’objets Blob**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> Activité de copie prend en charge la copie de données à partir de / tooboth le stockage Azure à usage général des comptes et à chaud/refroidir stockage d’objets Blob. prend en charge de l’activité Hello **lors de la lecture à partir de blocs, ajouter ou objets BLOB de pages**, mais prend en charge **l’écriture d’objets BLOB de blocs tooonly**. Le stockage Azure Premium n’est pas pris en charge en tant que récepteur, car il repose sur des objets blob de pages.
> 
> Activité de copie ne supprime pas les données à partir de la source de hello après que hello données sont correctement copié toohello destination. Si vous avez besoin de toodelete source de données après la copie a réussi, créer un [activité personnalisée](data-factory-use-custom-activities.md) toodelete hello des données et utiliser l’activité hello dans le pipeline de hello. Pour obtenir un exemple, consultez hello [exemple d’objet blob ou le dossier Delete sur GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity). 

## <a name="get-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis un stockage blob Azure à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Cet article a une [procédure pas à pas](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) pour la création d’un toocopy de données de pipeline à partir d’un tooanother d’emplacement de stockage d’objets Blob Azure emplacement de stockage d’objets Blob Azure. Pour obtenir un didacticiel sur la création d’un toocopy de données de pipeline à partir d’une base de données SQL de tooAzure stockage d’objets Blob Azure, consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md).

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Création d'une **fabrique de données**. Une fabrique de données peut contenir un ou plusieurs pipelines. 
2. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins. Par exemple, si vous copiez des données à partir d’une base de données SQL Azure de tooan stockage blob Azure, vous créez deux services liés toolink votre compte de stockage et de la fabrique de données de tooyour de base de données SQL Azure. Pour les propriétés de service lié qui sont spécifique tooAzure stockage d’objets Blob, consultez [lié des propriétés du service](#linked-service-properties) section. 
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello. De plus, vous créez une autre table SQL hello toospecify jeu de données dans la base de données SQL Azure hello qui contient les données hello copiées à partir du stockage d’objets blob hello. Pour les propriétés du dataset qui sont spécifique tooAzure stockage d’objets Blob, consultez [propriétés du dataset](#dataset-properties) section.
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et SqlSink comme un récepteur pour l’activité de copie hello. De même, si vous copiez à partir de la base de données SQL Azure tooAzure stockage d’objets Blob, vous utilisez SqlSource et BlobSink dans l’activité de copie hello. Pour les propriétés d’activité de copie sont spécifique tooAzure stockage d’objets Blob, consultez [copier les propriétés de l’activité](#copy-activity-properties) section. Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.  

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/depuis un stockage d’objets Blob Azure, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) section de cet article.

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure stockage d’objets Blob.

## <a name="linked-service-properties"></a>Propriétés du service lié
Il existe deux types de services liés, vous pouvez utiliser toolink une fabrique de données Azure tooan le stockage Azure. Il s’agit des services liés **AzureStorage** et **AzureStorageSas**. Hello service lié Azure Storage fournit la fabrique de données hello avec accès global toohello le stockage Azure. Alors que hello Azure stockage SAS (Shared Access Signature) lié service fournit fabrique de données hello avec l’accès restreint/temps toohello le stockage Azure. Il n'existe aucune différence entre ces deux services liés. Sélectionnez service hello lié qui correspond le mieux à vos besoins. Hello sections suivantes fournissent plus d’informations sur ces deux services liés.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Propriétés du jeu de données
toospecify un toorepresent de jeu de données d’entrée ou de sortie des données dans un stockage d’objets Blob Azure, que vous définissez propriété hello du jeu de données hello : **AzureBlob**. Ensemble hello **linkedServiceName** service lié de propriété du nom de toohello hello dataset Hello le stockage Azure ou SAS de stockage Azure.  propriétés de type Hello du jeu de données hello spécifient hello **conteneur d’objets blob** et hello **dossier** dans le stockage blob hello.

Pour obtenir une liste complète des sections JSON et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Fabrique de données prend en charge hello conforme CLS .NET en fonction des valeurs de type qui fournit des informations de type dans « structure » pour les sources de données de schéma-sur-lecture comme objets blob Azure suivantes : Int16, Int32, Int64, Single, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan. Fabrique de données effectue automatiquement les conversions de type lors du déplacement du magasin de données récepteur tooa du magasin de données à partir des données sources.

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations à propos de l’emplacement de hello, format, etc., de données hello dans le magasin de données hello. jeu de données de type Hello typeProperties section **AzureBlob** dataset a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Conteneur toohello de chemin d’accès et le dossier de stockage d’objets blob hello. Exemple : monconteneurblob\mondossierblob\ |Oui |
| fileName |Nom de l’objet blob de hello. fileName est facultatif et sensible à la casse.<br/><br/>Si vous spécifiez un nom de fichier, le hello activité (y compris la copie) fonctionne sur hello Blob spécifique.<br/><br/>Lorsque le nom de fichier n’est pas spécifié, copie inclut tous les objets BLOB dans folderPath hello pour le jeu de données d’entrée.<br/><br/>Lorsque **nom de fichier** n’est pas spécifié pour un dataset de sortie et **preserveHierarchy** n’est pas spécifié dans le récepteur d’activité, nom hello du fichier de hello généré serait Bonjour sous ce format : données.<Guid>. txt (par exemple : : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Non |
| partitionedBy |partitionedBy est une propriété facultative. Vous pouvez utiliser il toospecify un folderPath dynamique et le nom de fichier de données de série chronologique. Par exemple, folderPath peut être paramétré pour toutes les heures de données. Consultez hello [à l’aide de la section de propriété partitionedBy](#using-partitionedBy-property) pour plus d’informations et des exemples. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

### <a name="using-partitionedby-property"></a>Utilisation de la propriété partitionedBy
Comme indiqué dans la section précédente de hello, vous pouvez spécifier un folderPath dynamique et le nom de fichier de données de série chronologique par hello **partitionedBy** propriété, [fonctions de la fabrique de données et les variables système hello](data-factory-functions-variables.md).

Pour obtenir plus d’informations sur les jeux de données de série chronologique, la planification et les segments, consultez les articles [Création de jeux de données](data-factory-create-datasets.md) et [Planification et exécution](data-factory-scheduling-and-execution.md).

#### <a name="sample-1"></a>Exemple 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Dans cet exemple, {Slice} est remplacé par la valeur hello de fabrique de données variable système SliceStart au format (AAAAMMJJHH) de la hello spécifiée. Hello SliceStart fait référence à des temps de toostart de tranche de hello. Hello folderPath est différent pour chaque secteur. Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Exemple 2

```json
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

Dans cet exemple, l'année, le mois, le jour et l'heure de SliceStart sont extraits dans des variables distinctes qui sont utilisées par les propriétés folderPath et fileName.

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les jeux de données d’entrée et de sortie et les stratégies sont disponibles pour tous les types d’activités. Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello. Si vous déplacez des données à partir d’un stockage d’objets Blob Azure, vous définissez type de source de hello dans l’activité de copie hello trop**BlobSource**. De même, si vous déplacez des données tooan stockage d’objets Blob Azure, vous définir le type de récepteur hello dans l’activité de copie hello trop**BlobSink**. Cette section fournit une liste de propriétés prises en charge par BlobSource et BlobSink.

**BlobSource** prend en charge hello propriétés Bonjour suivantes **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello. |True (valeur par défaut), False |Non |

**BlobSink** prend en charge les propriétés suivantes de hello **typeProperties** section :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| copyBehavior |Définit le comportement de copie de hello lors de la source de hello est BlobSource ou système de fichiers. |<b>PreserveHierarchy</b>: préserve hello hiérarchie de fichiers dans le dossier cible de hello. chemin d’accès relatif de Hello du dossier source du fichier toosource est identique toohello un chemin d’accès relatif du dossier tootarget de fichier cible.<br/><br/><b>FlattenHierarchy</b>: tous les fichiers à partir du dossier source hello sont Bonjour tout d’abord au niveau du dossier cible. les fichiers cibles Hello ont un nom généré automatiquement. <br/><br/><b>MergeFiles</b>: fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello. Si hello nom de fichier/objet Blob est spécifié, le nom de fichier fusionné hello serait nom spécifié de hello ; dans le cas contraire, serait de nom de fichier généré automatiquement. |Non |

**BlobSource** prend également en charge ces deux propriétés pour la compatibilité descendante.

* **treatEmptyAsNull**: Spécifie si tootreat null ou une chaîne vide en tant que valeur null.
* **skipHeaderLineCount** : spécifie le nombre de lignes à ignorer. Applicable uniquement quand le jeu de données d’entrée utilise TextFormat.

De même, **BlobSink** prend en charge hello suivant de propriété pour la compatibilité descendante.

* **blobWriterAddHeader**: Spécifie si le jeu de données de sortie tooadd un en-tête de définitions de colonne lors de l’écriture de tooan.

Hello de prise en charge de jeux de données maintenant les propriétés qui implémentent suivantes hello même fonctionnalité : **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.

Hello tableau suivant fournit des conseils sur l’utilisation des propriétés du nouveau dataset hello à la place de ces propriétés de source/récepteur blob.

| Propriété de l’activité de copie | Propriété du jeu de données |
|:--- |:--- |
| skipHeaderLineCount sur BlobSource |skipLineCount et firstRowAsHeader. Les lignes sont ignorées tout d’abord, et puis première ligne de hello est lu comme un en-tête. |
| treatEmptyAsNull sur BlobSource |treatEmptyAsNull sur le jeu de données d’entrée |
| blobWriterAddHeader sur BlobSink |firstRowAsHeader sur le jeu de données de sortie |

Consultez la section [Définition de TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) pour plus d’informations sur ces propriétés.    

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

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>Procédure pas à pas : Des données de toocopy d’utiliser l’Assistant copie vers/depuis le stockage d’objets Blob
Examinons à présent comment tooquickly copier des données à partir de Azure stockage d’objets blob. Dans cette procédure pas à pas, les banques de données source et de destination sont du type stockage Blob Azure. Hello pipeline dans cette procédure copie les données à partir d’un dossier de tooanother Bonjour même conteneur d’objets blob. Cette procédure pas à pas est volontairement simple tooshow paramètres ou des propriétés lors de l’utilisation du stockage d’objets Blob comme source ou récepteur. 

### <a name="prerequisites"></a>Composants requis
1. Créez un **compte de stockage Azure** à usage général si vous n’en avez pas encore un. Vous utilisez le stockage d’objets blob hello à la fois comme **source** et **destination** stocker des données dans cette procédure pas à pas. Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) toocreate suit un article.
2. Créer un conteneur d’objets blob nommé **adfblobconnector** hello compte de stockage. 
4. Créez un dossier nommé **d’entrée** Bonjour **adfblobconnector** conteneur.
5. Créez un fichier nommé **emp.txt** avec hello suivant de contenu et le télécharger toohello **d’entrée** dossier à l’aide des outils tels que [Explorateur de stockage Azure](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>Créer la fabrique de données hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **+ nouveau** à partir de l’angle supérieur gauche de hello, cliquez sur **Intelligence + analytique**, puis cliquez sur **Data Factory**.
3. Bonjour **nouvelle fabrique de données** panneau :   
    1. Entrez **ADFBlobConnectorDF** pour hello **nom**. nom de Hello de fabrique de données Azure hello doit être globalement unique. Si vous recevez une erreur de hello : `*Data factory name “ADFBlobConnectorDF” is not available`, de modifier le nom hello hello fabrique de données (par exemple, yournameADFBlobConnectorDF) et essayez à nouveau de créer. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.
    2. Sélectionnez votre **abonnement**Azure.
    3. Pour le groupe de ressources, sélectionnez **utiliser l’existant** tooselect un ressource groupe (ou) sélectionnez **nouvel** tooenter un nom pour un groupe de ressources.
    4. Sélectionnez un **emplacement** de fabrique de données hello.
    5. Sélectionnez **toodashboard du code confidentiel** bas hello du Panneau de hello de case à cocher.
    6. Cliquez sur **Créer**.
3. Après la création de hello est terminée, vous voyez hello **Data Factory** panneau comme indiqué dans hello suivant image : ![page d’accueil de fabrique de données](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>Assistant de copie
1. Sur la page d’accueil de Data Factory hello, cliquez sur hello **copier des données [Aperçu]** vignette toolaunch **Assistant copie de données** dans un onglet séparé.    
    
    > [!NOTE]
    >    Si vous voyez ce navigateur hello est bloqué au niveau de « Autorisation... », désactiver/Décochez **bloquer les cookies tiers et les données de site** définition (ou) qu’il soit activé et créer une exception pour **login.microsoftonline.com**, puis essayez de lancer les Assistant hello à nouveau.
2. Bonjour **propriétés** page :
    1. Entrez **CopyPipeline** comme **Nom de la tâche**. nom de tâche Hello est hello du pipeline hello dans votre fabrique de données.
    2. Entrez un **description** pour la tâche hello (facultatif).
    3. Pour **cadence de tâche ou de la planification de la tâche**, conserver hello **exécuter régulièrement selon la planification** option. Si vous souhaitez toorun cette tâche qu’une seule fois au lieu de s’exécuter à plusieurs reprises selon une planification, sélectionnez **exécuter qu’une seule fois maintenant**. Si vous sélectionnez l’option **Run once now (Exécuter une seule fois maintenant)**, un [pipeline à usage unique](data-factory-create-pipelines.md#onetime-pipeline) est créé. 
    4. Conservez les paramètres hello pour **périodique modèle**. Cette tâche s’exécute tous les jours entre hello début et de fin que vous spécifiez dans l’étape suivante de hello.
    5. Hello de modification **date heure de début** trop**21/04/2017**. 
    6. Hello de modification **date heure de fin** trop**25/04/2017**. Vous souhaiterez peut-être date de hello tootype au lieu de parcourir le calendrier de hello.     
    8. Cliquez sur **Suivant**.
      ![Outil de copie - Page Propriétés](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. Sur hello **magasin de données Source** , cliquez sur **stockage d’objets Blob Azure** vignette. Vous utilisez cette banque de données de page toospecify hello source pour la tâche de copie hello. Vous pouvez utiliser un service lié de magasin de données existant (ou) spécifier un nouveau magasin de données. service lié de toouse existant, vous devez sélectionner **de lié SERVICES existants** et sélectionnez hello service lié à droite. 
    ![Outil de copie - Page Banque de données sources](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. Sur hello **spécifier le compte de stockage d’objets Blob Azure hello** page :
   1. Conserver le nom généré automatiquement de hello pour **nom de la connexion**. nom de la connexion Hello est nom hello du service hello lié de type : le stockage Azure. 
   2. Vérifiez que l’option **À partir des abonnements** est sélectionnée pour **Account selection method** (Méthode de sélection du compte).
   3. Sélectionnez votre abonnement Azure ou conservez **Sélectionner tout** pour l’option **Abonnement Azure**.   
   4. Sélectionnez un **compte de stockage Azure** hello à partir de la liste de stockage Azure comptes disponible dans l’abonnement de hello sélectionné. Vous pouvez également choisir tooenter les paramètres de compte de stockage manuellement en sélectionnant **entrer manuellement** option hello **méthode de sélection du compte**.
   5. Cliquez sur **Suivant**. 
      ![Outil Copier - spécifiez le compte de stockage d’objets Blob Azure hello](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. Sur **choisir un fichier d’entrée hello ou un dossier** page :
   1. Double-cliquez sur **adfblobcontainer**.
   2. Sélectionnez **input**, puis cliquez sur **Choisir**. Dans cette procédure pas à pas, vous sélectionnez les dossiers d’entrée hello. Vous pouvez également sélectionner à la place le fichier de emp.txt hello dans le dossier de hello. 
      ![Outil Copier - choisir un fichier d’entrée de hello ou un dossier](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. Sur hello **choisir un fichier d’entrée hello ou un dossier** page :
    1. Vérifiez que hello **fichier ou dossier** est défini trop**adfblobconnector/entrée**. Si les fichiers de hello sont des sous-dossiers, par exemple, 04/01/2017 2017/04/02 et ainsi de suite, entrez adfblobconnector/entrée / {year} / {month} / {day} pour le fichier ou dossier. Lorsque vous appuyez sur TAB en dehors de la zone de texte hello, vous voyez trois formats tooselect de listes déroulantes pour l’année (aaaa), month (MM) et le jour (jj). 
    2. Ne définissez pas **Copy file recursively (Copier le fichier de façon récursive)**. Sélectionnez cette toorecursively option Parcourir de dossiers pour les fichiers toobe copiés toohello destination. 
    3. Ne pas hello **copie binaire** option. Sélectionnez cette option de tooperform une copie binaire de destination toohello du fichier source. Ne sélectionnez pas cette procédure pas à pas afin que vous puissiez voir davantage d’options dans les pages suivantes de hello. 
    4. Vérifiez que hello **le type de Compression** est défini trop**aucun**. Sélectionnez une valeur pour cette option si vos fichiers source sont compressés dans un des formats de hello pris en charge. 
    5. Cliquez sur **Suivant**.
    ![Outil Copier - choisir un fichier d’entrée de hello ou un dossier](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. Sur hello **les paramètres de format de fichier** page, vous voyez les délimiteurs hello et schéma de hello est détecté automatiquement par l’Assistant de hello par l’analyse du fichier de hello. 
    1. Confirmer les options suivantes de hello : un. Hello **format de fichier** est défini trop**au format texte**. Vous pouvez voir tous les formats de hello pris en charge dans la liste déroulante de hello. Exemple : JSON, Avro, ORC, Parquet.
        b. Hello **délimiteur de colonne** est défini trop`Comma (,)`. Vous pouvez voir hello autres séparateurs de colonnes pris en charge par la fabrique de données dans la liste déroulante de hello. Vous pouvez également spécifier un séparateur personnalisé.
        c. Hello **séparateur de lignes** est défini trop`Carriage Return + Line feed (\r\n)`. Vous pouvez voir hello autres séparateurs de lignes pris en charge par la fabrique de données dans la liste déroulante de hello. Vous pouvez également spécifier un séparateur personnalisé.
        d. Hello **ignorer le nombre de lignes** est défini trop**0**. Si vous souhaitez que quelques lignes toobe ignorée haut hello du fichier de hello, entrez le numéro de hello ici.
        e.  Hello **première ligne de données contient des noms de colonne** n’est pas définie. Si les fichiers de sources de hello contiennent des noms de colonnes dans la première ligne de hello, sélectionnez cette option.
        f. Hello **traiter la valeur de la colonne vide comme null** option est définie.
    2. Développez **paramètres avancés** toosee advanced option disponible.
    3. Au bas de hello de page de hello, consultez hello **aperçu** de données à partir du fichier de emp.txt hello.
    4. Cliquez sur **schéma** onglet au schéma de hello hello bas toosee cet Assistant copie de hello déduit en examinant les données de salutation dans le fichier de source de hello.
    5. Cliquez sur **suivant** une fois que vous passez en revue les délimiteurs hello et afficher un aperçu des données.
    ![Outil de copie - Paramètres de format de fichier](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. Sur hello **page de magasin de données de Destination**, sélectionnez **stockage d’objets Blob Azure**, puis cliquez sur **suivant**. Vous utilisez hello stockage d’objets Blob Azure en tant que les deux magasins hello les données source et de destination dans cette procédure pas à pas.    
    ![Outil de copie - Sélectionner la banque de données de destination](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. Sur **spécifier le compte de stockage d’objets Blob Azure hello** page :
   1. Entrez **AzureStorageLinkedService** pour hello **nom de la connexion** champ.
   2. Vérifiez que l’option **À partir des abonnements** est sélectionnée pour **Account selection method** (Méthode de sélection du compte).
   3. Sélectionnez votre **abonnement**Azure.  
   4. Sélectionnez votre compte de stockage Azure. 
   5. Cliquez sur **Suivant**.     
10. Sur hello **fichier ou le dossier de sortie choisir hello** page : 
    6. spécifiez le **chemin d’accès du dossier** **adfblobconnector/output/{année}/{mois}/{jour}**. Entrez **TAB**.
    7. Pourquoi **année**, sélectionnez **aaaa**.
    8. Pourquoi **mois**, vérifiez qu’il est défini trop**MM**.
    9. Pourquoi **jour**, vérifiez qu’il est défini trop**jj**.
    10. Vérifiez que hello **le type de compression** est défini trop**aucun**.
    11. Vérifiez que hello **copier comportement** est défini trop**fusionner les fichiers**. Si la sortie hello fichier avec le même nom existe déjà de hello, hello nouveau contenu est ajouté toohello même fichier à la fin de hello.
    12. Cliquez sur **Suivant**.
    ![Outil de copie - Choisir le fichier ou le dossier de sortie](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. Sur hello **les paramètres de format de fichier** page, passez en revue les paramètres de hello, puis cliquez sur **suivant**. Une des options supplémentaires de hello ici est tooadd un fichier de sortie d’en-tête toohello. Si vous sélectionnez cette option, une ligne d’en-tête est ajoutée avec des noms de colonnes de hello schéma hello de source de hello. Vous pouvez renommer les noms de colonne par défaut hello lors de l’affichage de schéma hello pour la source de hello. Par exemple, vous pouvez modifier hello première colonne tooFirst nom et la deuxième colonne tooLast nom. Puis, le fichier de sortie hello est généré avec un en-tête avec ces noms comme noms de colonne. 
    ![Outil de copie - Paramètres de format de fichier pour la destination](media/data-factory-azure-blob-connector/file-format-destination.png)
12. Sur hello **les paramètres de performances** page, vérifiez que **cloud unités** et **parallèles copies** sont définies trop**automatique**et cliquez sur Suivant. Pour plus d’informations sur ces paramètres, consultez le [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md#parallel-copy).
    ![Outil de copie - Paramètres de performances](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. Sur hello **Résumé** page, passez en revue tous les paramètres (propriétés de la tâche, les paramètres pour la source et de destination et copier les paramètres), puis cliquez sur **suivant**.
    ![Outil de copie - Page Résumé](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. Passez en revue les informations contenues dans hello **Résumé** page, puis cliquez sur **Terminer**. Assistant de Hello crée deux services liés, les deux jeux de données (entrées et sorties) et un seul pipeline dans la fabrique de données hello (à partir de lancement de hello Assistant copie de).
    ![Outil de copie - Page Déploiement](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>Surveiller le pipeline hello (tâche de copie)

1. Cliquez sur le lien de hello `Click here toomonitor copy pipeline` sur hello **déploiement** page. 
2. Vous devez voir hello **surveiller et gérer des applications** dans un onglet séparé.  ![Application Surveiller et gérer](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. Hello de modification **Démarrer** trop de temps en haut de hello`04/19/2017` et **fin** trop de temps`04/27/2017`, puis cliquez sur **appliquer**. 
4. Vous devez voir cinq windows activité Bonjour **WINDOWS de l’activité** liste. Hello **WindowStart** fois doivent couvrir tous les jours à partir de l’heure de fin de pipeline début toopipeline. 
5. Cliquez sur **Actualiser** bouton pour hello **WINDOWS de l’activité** liste plusieurs fois jusqu'à ce que vous voyiez état hello de toutes les fenêtres d’activité hello a la valeur tooReady. 
6. À présent, vérifiez que les fichiers de sortie hello sont générées dans le dossier de sortie hello du conteneur d’adfblobconnector. Vous devez voir hello suivant la structure de dossiers dans le dossier de sortie hello : 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
Pour plus d’informations sur la surveillance et la gestion des fabriques de données, consultez l’article [Monitor and manage Data Factory pipeline (Surveiller et gérer le pipeline Data Factory)](data-factory-monitor-manage-app.md). 
 
### <a name="data-factory-entities"></a>Entités Data Factory
Passez maintenant, onglet toohello retour avec la page d’accueil de Data Factory hello. Notez qu’il existe désormais deux services liés, deux jeux de données et un pipeline dans votre fabrique de données. 

![Page d’accueil Data Factory comportant des entités](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

Cliquez sur **auteur et déployer** toolaunch éditeur Data Factory. 

![Data Factory Editor](media/data-factory-azure-blob-connector/data-factory-editor.png)

Vous devez voir hello suivant des entités de fabrique de données dans votre fabrique de données : 

 - Deux services liés, Un pour la source de hello et hello autre destination de hello. Les deux services hello lié font référence toohello même compte de stockage Azure dans cette procédure pas à pas. 
 - Deux jeux de données, un jeu de données d’entrée et un jeu de données de sortie. Dans cette procédure pas à pas, les deux utilisent hello même conteneur d’objets blob, mais reportez-vous dossiers toodifferent (entrées et sorties).
 - Un pipeline. pipeline de Hello contient une activité de copie qui utilise une source d’objets blob et un objet blob récepteur toocopy des données d’une tooanother d’emplacement d’objets blob Azure emplacement d’objets blob Azure. 

Hello sections suivantes fournissent plus d’informations sur ces entités. 

#### <a name="linked-services"></a>Services liés
Vous devez voir deux services liés, Un pour la source de hello et hello autre destination de hello. Dans cette procédure pas à pas, les deux définitions de regarder hello identiques à l’exception des noms de hello. Hello **type** Hello service lié est défini trop**AzureStorage**. Propriété la plus importante de définition du service lié de hello est hello **connectionString**, qui est utilisé par la fabrique de données tooconnect tooyour compte de stockage Azure lors de l’exécution. Ignorer la propriété hubName de hello dans la définition de hello. 

##### <a name="source-blob-storage-linked-service"></a>Service lié du stockage d’objets blob source
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>Service lié du stockage d’objets blob de destination

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

Pour plus d’informations sur le service lié Stockage Azure, consultez la section [Propriétés du service lié](#linked-service-properties). 

#### <a name="datasets"></a>Groupes de données
Il existe deux jeux de données : un jeu de données d’entrée et un jeu de données de sortie. type Hello du jeu de données hello est défini trop**AzureBlob** pour les deux. 

jeu de données d’entrée Hello pointe toohello **d’entrée** dossier Hello **adfblobconnector** conteneur d’objets blob. Hello **externe** propriété a la valeur trop**true** pour ce jeu de données en tant que hello données ne sont pas produites par le pipeline de hello avec l’activité de copie hello acceptant ce jeu de données en tant qu’entrée. 

Hello sortie dataset points toohello **sortie** dossier Hello même conteneur d’objets blob. Hello dataset de sortie utilise également hello year, month et le jour de hello **SliceStart** toodynamically de variables système évaluer le chemin d’accès de hello pour le fichier de sortie hello. Pour obtenir la liste des fonctions et variables système prises en charge par Data Factory, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md). Hello **externe** propriété a la valeur trop**false** (valeur par défaut), car ce jeu de données est généré par le pipeline de hello. 

Pour plus d’informations sur les propriétés prises en charge par le jeu de données d’objets blob Azure, consultez la section [Propriétés du jeu de données](#dataset-properties).

##### <a name="input-dataset"></a>Jeu de données d'entrée

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>Jeu de données de sortie

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>Pipeline
pipeline de Hello a qu’une seule activité. Hello **type** Hello activité est définie trop**copie**.  Dans les propriétés de type hello pour l’activité de hello, il existe deux sections, une pour la source et hello autre pour le récepteur. type de source de Hello est défini trop**BlobSource** comme activité hello copie des données à partir d’un stockage d’objets blob. Hello le type de récepteur est défini trop**BlobSink** en tant qu’activité hello copie le stockage d’objets blob de données tooa. activité de copie Hello prend InputDataset-z4y en tant qu’entrée de hello et OutputDataset-z4y en tant que sortie de hello. 

Pour plus d’informations sur les propriétés prises en charge par BlobSource et BlobSink, consultez la section [Propriétés de l’activité de copie](#copy-activity-properties). 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>Exemples JSON pour la copie des données tooand depuis le stockage Blob  
Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment tooand de données toocopy à partir de la base de données SQL Azure et de stockage d’objets Blob Azure. Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>Exemple de JSON : Copier les données de stockage d’objets Blob tooSQL de base de données
Hello ci-dessous illustre d’exemple :

1. Un service lié de type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Un service lié de type [AzureStorage](#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](#copy-activity-properties) et [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).

exemple Hello copie les données de série chronologique dans une table de SQL Azure blob Azure tooan toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service lié SQL Azure :**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Service lié Azure Storage :**

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
Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**. Pour hello premier, vous spécifiez la chaîne de connexion hello qui inclut la clé de compte hello et pourquoi une version ultérieure, vous spécifiez hello Uri de Signature d’accès partagé (SAS). Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .  

**Jeu de données d'entrée d'objet Blob Azure :**

Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1). nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello. « external » : « true » paramètre informe Data Factory cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
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
**Jeu de données de sortie SQL Azure :**

exemple Hello copie table tooa de données nommé « MyTable » dans une base de données SQL Azure. Créer la table de hello dans votre base de données SQL Azure hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello. Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Activité de copie dans un pipeline avec une source blob et un récepteur SQL :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>Exemple de JSON : Copier des données à partir de SQL Azure tooAzure Blob
Hello ci-dessous illustre d’exemple :

1. Un service lié de type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Un service lié de type [AzureStorage](#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) et [BlobSink](#copy-activity-properties).

exemple Hello copie toutes les heures des données de séries chronologiques à partir d’un tooan de table SQL Azure blob Azure. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

**Service lié SQL Azure :**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Service lié Azure Storage :**

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
Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**. Pour hello premier, vous spécifiez la chaîne de connexion hello qui inclut la clé de compte hello et pourquoi une version ultérieure, vous spécifiez hello Uri de Signature d’accès partagé (SAS). Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .  

**Jeu de données d'entrée SQL Azure :**

exemple Hello suppose que vous avez créé une table « MyTable » dans SQL Azure, et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.

Paramètre « external » : « true » informe service Data Factory cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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

**Jeu de données de sortie Azure Blob :**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

**Activité de copie dans un pipeline avec une source SQL et un récepteur blob :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource** et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

> [!NOTE]
> colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
