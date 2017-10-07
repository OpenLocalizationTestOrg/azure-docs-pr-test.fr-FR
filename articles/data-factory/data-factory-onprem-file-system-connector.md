---
title: "données aaaCopy vers/depuis un système de fichiers à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Découvrez comment tooand de données toocopy à partir d’un système de fichiers local à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Copier des données tooand à partir d’un système de fichiers local à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données de toocopy Azure Data Factory vers/à partir d’un système de fichiers local. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez copier des données **à partir d’un système de fichiers local** toohello suivant des magasins de données :

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Vous pouvez copier des données à partir de hello suivant des magasins de données **tooan local système de fichiers**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Activité de copie ne supprime pas le fichier de source de hello lorsqu’elle est correctement copié toohello destination. Si vous avez besoin de fichier de source de hello toodelete après la copie a réussi, créer un fichier de hello toodelete activité personnalisée et utiliser l’activité hello dans le pipeline de hello. 

## <a name="enabling-connectivity"></a>Activation de la connectivité
Fabrique de données prend en charge la connexion tooand à partir d’un système de fichiers local via **passerelle de gestion des données**. Vous devez installer hello passerelle de gestion des données dans votre environnement local pour hello Data Factory service tooconnect tooany locale prise en charge banque de données, y compris le système de fichiers. toolearn sur la passerelle de gestion des données et pour obtenir des instructions sur la configuration de passerelle de hello, consultez [déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md). En dehors de la passerelle de gestion des données, aucun autre fichier binaire ne devez tooand de toocommunicate toobe installé à partir d’un système de fichiers local. Vous devez installer et utiliser hello passerelle de gestion des données, même si le système de fichiers hello est dans une machine virtuelle IaaS de Azure. Pour plus d’informations sur la passerelle de hello, consultez [passerelle de gestion des données](data-factory-data-management-gateway.md).

toouse un partage de fichiers Linux, installer [Samba](https://www.samba.org/) sur votre serveur Linux et installez passerelle de gestion des données sur un serveur Windows. L’installation de la passerelle de gestion des données sur un serveur Linux n'est pas prise en charge.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis un système de fichiers à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Création d'une **fabrique de données**. Une fabrique de données peut contenir un ou plusieurs pipelines. 
2. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins. Par exemple, si vous copiez des données à partir d’un système de fichiers local tooan Azure blob storage, vous créez deux services liés toolink votre système de fichiers local et la fabrique de données de stockage Azure compte tooyour. Pour les propriétés de service lié qui sont le système de fichiers local tooan spécifiques, consultez [lié des propriétés du service](#linked-service-properties) section.
3. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello. Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello. De plus, vous créez un autre jeu de données toospecify hello dossier et le nom (facultatif) dans votre système de fichiers. Pour le système de fichiers de propriétés du dataset qui sont spécifiques tooon locaux, consultez [propriétés du dataset](#dataset-properties) section.
4. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie. Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et FileSystemSink comme un récepteur pour l’activité de copie hello. De même, si vous copiez à partir de tooAzure de système de fichiers local stockage d’objets Blob, vous utilisez FileSystemSource et BlobSink dans l’activité de copie hello. Pour le système de fichiers de propriétés de l’activité copie tooon-site spécifique, consultez [copier les propriétés de l’activité](#copy-activity-properties) section. Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/depuis un système de fichiers, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-file-system) section de cet article.

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifiques toofile système :

## <a name="linked-service-properties"></a>Propriétés du service lié
Vous pouvez lier une fabrique de données Azure local fichier système tooan avec hello **serveur de fichiers local** service lié. Hello tableau suivant fournit des descriptions pour les éléments JSON qui sont spécifique toohello service serveur de fichiers local lié.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |Assurez-vous que les propriétés de type hello sont définie trop**OnPremisesFileServer**. |Oui |
| host |Spécifie le chemin d’accès racine de hello du dossier hello que vous souhaitez toocopy. Utilisez le caractère d’échappement de hello ' \ ' pour les caractères spéciaux dans la chaîne de hello. Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples. |Oui |
| userId |Spécifiez des ID de hello de serveur d’accès toohello utilisateur hello. |Non (si vous choisissez encryptedcredential) |
| password |Spécifiez le mot de passe hello pour hello (userid). |Non (si vous choisissez encryptedcredential) |
| Encryptedcredential |Spécifiez les informations d’identification de hello chiffré que vous pouvez obtenir en exécutant l’applet de commande New-AzureRmDataFactoryEncryptValue de hello. |Non (si vous choisissez toospecify nom d’utilisateur et mot de passe en texte brut) |
| gatewayName |Spécifie le nom hello de passerelle hello que Data Factory doit utiliser de serveur de fichiers local tooconnect toohello. |Oui |


### <a name="sample-linked-service-and-dataset-definitions"></a>Exemples de définitions de jeux de données et de service liés
| Scénario | Hôte dans la définition du service lié | folderPath dans la définition du jeu de données |
| --- | --- | --- |
| Dossier local sur l’ordinateur passerelle de gestion des données :  <br/><br/>Exemples : D:\\\* ou D:\dossier\sous-dossier\\* |D:\\\\ (pour la passerelle de gestion des données 2.0 et versions ultérieures) <br/><br/> hôte local (pour les versions de la passerelle de gestion des données antérieures à 2.0) |.\\\\ ou dossier\\\\sous-dossier (pour la passerelle de gestion des données 2.0 et versions ultérieures) <br/><br/>D:\\\\ ou D:\\\\dossier\\\\sous-dossier (pour les versions de la passerelle antérieures à 2.0) |
| Dossier partagé distant :  <br/><br/>Exemples : \\\\myserver\\share\\\* ou \\\\myserver\\share\\dossier\\sous-dossier\\* |\\\\\\\\myserver\\\\share |.\\\\ ou dossier\\\\sous-dossier |


### <a name="example-using-username-and-password-in-plain-text"></a>Exemple : utilisation d’un nom d'utilisateur et d’un mot de passe en texte brut

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>Exemple : utilisation de l’élément encryptedcredential

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md). Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.

section de typeProperties Hello est différente pour chaque type de jeu de données. Il fournit des informations telles que l’emplacement de hello et le format de données hello dans le magasin de données hello. section hello le jeu de données de type Hello typeProperties **le partage de fichiers** a hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Spécifie le dossier de toohello sous-chemin hello. Utilisez le caractère d’échappement de hello ' \' pour les caractères spéciaux dans la chaîne de hello. Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.<br/><br/>Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin. |Oui |
| fileName |Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello. Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.<br/><br/>Lorsque **nom de fichier** n’est pas spécifié pour un dataset de sortie et **preserveHierarchy** n’est pas spécifié dans récepteur d’activité, hello nom hello généré est Bonjour suivant le format : <br/><br/>`Data.<Guid>.txt` (Exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Non |
| fileFilter |Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers. <br/><br/>Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).<br/><br/>Exemple 1 : « fileFilter » : « *.log »<br/>Exemple 2 : « fileFilter » : « 2014-1-?.txt »<br/><br/>Remarque : fileFilter s’applique à un jeu de données FileShare d’entrée. |Non |
| partitionedBy |Vous pouvez utiliser partitionedBy toospecify folderPath/nom de fichier dynamique pour les données de série chronologique. Par exemple, folderPath peut être paramétré pour toutes les heures de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

> [!NOTE]
> Vous ne pouvez pas utiliser fileName et fileFilter simultanément.

### <a name="using-partitionedby-property"></a>Utilisation de la propriété partitionedBy
Comme indiqué dans la section précédente de hello, vous pouvez spécifier un folderPath dynamique et le nom de fichier de données de série chronologique par hello **partitionedBy** propriété, [fonctions de la fabrique de données et les variables système hello](data-factory-functions-variables.md).

toounderstand plus d’informations sur les jeux de données de série chronologique, en planifiant et secteurs, consultez [création de datasets](data-factory-create-datasets.md), [de planification et de l’exécution](data-factory-scheduling-and-execution.md), et [création de pipelines](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Exemple 1 :

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Dans cet exemple, {Slice} est remplacé par la valeur hello hello fabrique de données système variable SliceStart au hello format (AAAAMMJJHH). SliceStart fait référence à des temps de toostart de tranche de hello. Hello folderPath est différent pour chaque secteur. Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Exemple 2 :

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

Dans cet exemple, année, mois, jour et l’heure de SliceStart sont extraits dans des variables distinctes qui utilisent des propriétés folderPath et fileName de hello.

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les jeux de données d’entrée et de sortie et les stratégies sont disponibles pour tous les types d’activités. Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité.

Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello. Si vous déplacez des données à partir d’un système de fichiers local, vous définissez type de source de hello dans l’activité de copie hello trop**FileSystemSource**. De même, si vous déplacez des données tooan système de fichiers local, vous définissez le type de récepteur hello dans l’activité de copie hello trop**FileSystemSink**. Cette section fournit une liste de propriétés prises en charge par FileSystemSource et FileSystemSink.

**FileSystemSource** prend en charge hello propriétés suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive des sous-dossiers de hello ou uniquement à partir de dossier spécifié de hello. |True, False (par défaut) |Non |

**FileSystemSink** prend en charge hello propriétés suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| copyBehavior |Définit le comportement de copie de hello lors de la source de hello est BlobSource ou système de fichiers. |**PreserveHierarchy :** conserve la hiérarchie des fichiers dans le dossier cible de hello hello. Autrement dit, chemin d’accès relatif de hello du dossier source de hello source fichier toohello est hello identique au chemin d’accès relatif de hello du dossier cible de hello cible fichier toohello.<br/><br/>**FlattenHierarchy :** tous les fichiers à partir du dossier source hello sont créés dans hello premier niveau du dossier cible. les fichiers cibles Hello sont créés avec un nom généré automatiquement.<br/><br/>**MergeFiles :** fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello. Si le nom de blob/nom de fichier hello est spécifié, nom de fichier fusionné hello désigne hello spécifié. Dans le cas contraire, il s’agit d’un nom de fichier généré automatiquement. |Non |

### <a name="recursive-and-copybehavior-examples"></a>exemples de valeurs recursive et copyBehavior
Cette section décrit le comportement qui en résulte de hello d’opération de copie hello pour différentes combinaisons de valeurs pour les propriétés récursive et copyBehavior hello.

| valeur recursive | valeur copyBehavior | Comportement résultant |
| --- | --- | --- |
| true |preserveHierarchy |Pour un dossier source Dossier1 avec hello suivant la structure,<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>dossier cible de Hello Dossier1 est créée avec hello même structure en tant que source de hello :<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5 |
| true |flattenHierarchy |Pour un dossier source Dossier1 avec hello suivant la structure,<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>cible de Hello Dossier1 est créée avec hello suivant structure : <br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier5 |
| true |mergeFiles |Pour un dossier source Dossier1 avec hello suivant la structure,<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>cible de Hello Dossier1 est créée avec hello suivant structure : <br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 + Fichier3 + Fichier4 + Fichier5 est fusionné dans un fichier avec le nom de fichier généré automatiquement. |
| false |preserveHierarchy |Pour un dossier source Dossier1 avec hello suivant la structure,<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>dossier cible de Hello Dossier1 est créée avec hello suivant structure :<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/><br/>Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés. |
| false |flattenHierarchy |Pour un dossier source Dossier1 avec hello suivant la structure,<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>dossier cible de Hello Dossier1 est créée avec hello suivant structure :<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2<br/><br/>Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés. |
| false |mergeFiles |Pour un dossier source Dossier1 avec hello suivant la structure,<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Fichier2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5<br/><br/>dossier cible de Hello Dossier1 est créée avec hello suivant structure :<br/><br/>Dossier1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 est fusionné dans un fichier avec un nom de fichier généré automatiquement.<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nom généré automatiquement pour Fichier1<br/><br/>Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés. |

## <a name="supported-file-and-compression-formats"></a>Formats de fichier et de compression pris en charge
Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>Exemples JSON pour la copie des données tooand à partir du système de fichiers
Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Elles montrent comment tooand de données toocopy à partir d’un système de fichiers local et le stockage d’objets Blob Azure. Toutefois, vous pouvez copier les données *directement* de n’importe quelle tooany de sources hello de récepteurs hello répertoriés dans [prise en charge des sources et récepteurs](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de l’activité de copie dans Azure Data Factory.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>Exemple : Copier des données à partir d’un tooAzure de système de fichiers local stockage d’objets Blob
Cet exemple montre comment toocopy des données à partir d’un tooAzure de système de fichiers local stockage d’objets Blob. exemple Hello a hello suivant des entités de fabrique de données :

* Un service lié de type [OnPremisesFileServer](#linked-service-properties).
* Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties).
* Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hello suivant l’exemple copie les données de séries chronologiques à partir d’un tooAzure de système de fichiers local stockage d’objets Blob toutes les heures. propriétés JSON Hello qui sont utilisées dans ces exemples sont décrits dans les sections hello après les exemples hello.

Dans un premier temps, configurer la passerelle de gestion des données conformément aux instructions hello dans [déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md).

**Service lié de serveur de fichiers local :**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Nous vous recommandons d’utiliser des hello **encryptedCredential** propriété hello plutôt **userid** et **mot de passe** propriétés. Consultez la page [Service lié de serveur de fichiers](#linked-service-properties) pour plus d’informations sur ce service lié.

**Service lié Azure Storage :**

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

**Jeu de données d’entrée de système de fichiers local :**

Les données sont récupérées à partir d’un nouveau fichier toutes les heures. Hello folderPath et les propriétés de nom de fichier sont déterminées en fonction de l’heure de début hello de tranche de hello.  

Paramètre `"external": "true"` informe fabrique de données de ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

**Jeu de données de sortie Stockage Blob Azure :**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise hello des parties d’année, mois, jour et heure de l’heure de début hello.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Activité de copie dans un pipeline avec une source Système de fichiers et un récepteur blob :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie, et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource**, et **récepteur** type est défini trop**BlobSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>Exemple : Copier des données à partir du système de fichiers de base de données SQL Azure tooan local
Hello ci-dessous illustre d’exemple :

* Un service lié de type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
* Un service lié de type [OnPremisesFileServer](#linked-service-properties).
* Un jeu de données d’entrée de type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
* Un jeu de données de sortie de type [FileShare](#dataset-properties).
* Un pipeline avec une activité de copie qui utilise [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) et [FileSystemSink](#copy-activity-properties).

exemple Hello copie les données de séries chronologiques à partir d’un système de fichiers local de SQL Azure table tooan toutes les heures. les propriétés JSON Hello qui sont utilisées dans ces exemples sont décrits dans les sections après les exemples hello.

**Service lié pour Azure SQL Database :**

```JSON
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

**Service lié de serveur de fichiers local :**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Nous vous recommandons d’utiliser des hello **encryptedCredential** propriété au lieu d’utiliser hello **userid** et **mot de passe** propriétés. Consultez la page [Service lié de système de fichiers](#linked-service-properties) pour plus d’informations sur ce service lié.

**Jeu de données d'entrée SQL Azure :**

exemple Hello part du principe que vous avez créé une table « MyTable » dans SQL Azure, et contient une colonne appelée « timestampcolumn » pour les données de série chronologique.

Paramètre ``“external”: ”true”`` informe fabrique de données de ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```JSON
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

**Jeu de données de sortie de système de fichiers local :**

Données sont copiée tooa nouveau fichier toutes les heures. Hello folderPath et fileName pour l’objet blob de hello sont déterminés en fonction de l’heure de début hello de tranche de hello.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

**Activité de copie dans un pipeline avec une source SQL et un récepteur Système de fichiers :**

Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie, et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource**et hello **récepteur** type est défini trop**FileSystemSink**. la requête SQL Hello qui est spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


Vous pouvez également mapper des colonnes à partir de toocolumns du jeu de données source à partir de récepteur de jeu de données dans la définition d’activité de copie de hello. Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performances et réglage
 toolearn sur la clé de facteurs qui impact hello les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize, consultez hello [guide de paramétrage et de performances de l’activité de copie](data-factory-copy-activity-performance.md).
