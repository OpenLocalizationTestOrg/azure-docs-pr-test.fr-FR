---
title: Formats de fichier pris en charge dans Azure Data Factory | Microsoft Docs
description: "Cette rubrique décrit les formats de fichier et les codes de compression pris en charge par les connecteurs basés sur des fichiers dans Azure Data Factory."
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.topic: article
ms.date: 11/21/2017
ms.author: jingwang
ms.openlocfilehash: e583c6952e02c4a93f56594f6392f1d9a260dce0
ms.sourcegitcommit: 62eaa376437687de4ef2e325ac3d7e195d158f9f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/22/2017
---
# <a name="supported-file-formats-and-compression-codecs-in-azure-data-factory"></a>Formats de fichier et codecs de compression pris en charge dans Azure Data Factory

*Cette rubrique s’applique aux connecteurs suivants : [Amazon S3](connector-amazon-simple-storage-service.md), [Blob Azure](connector-azure-blob-storage.md), [Azure Data Lake Store](connector-azure-data-lake-store.md), [Stockage Fichier Azure](connector-azure-file-storage.md), [Système de fichiers](connector-file-system.md), [FTP](connector-ftp.md), [HDFS](connector-hdfs.md), [HTTP](connector-http.md) et [SFTP](connector-sftp.md).*

Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie. Si vous souhaitez **analyser ou générer des fichiers dans un format spécifique**, Azure Data Factory prend en charge les types de format de fichier suivants :

* [Format Texte](#text-format)
* [Format JSON](#json-format)
* [Format Avro](#avro-format)
* [Format ORC](#orc-format)
* [Format Parquet](#parquet-format)

> [!NOTE]
> Cet article s’applique à la version 2 de Data Factory, actuellement en préversion. Si vous utilisez la version 1 du service Data Factory, qui est généralement disponible, consultez [Fichier et formats de compression pris en charge dans Data Factory version 1](v1//data-factory-supported-file-and-compression-formats.md).

> [!TIP]
> Découvrez comment l'activité mappe vos données source au récepteur à l'aide de la [Mappage de schéma dans l’activité de copie](copy-activity-schema-and-type-mapping.md), et comment les métadonnées sont déterminées en fonction de vos paramètres de format de fichier et des conseils sur la spécification de la section du [jeu de données`structure`](concepts-datasets-linked-services.md#dataset-structure).

## <a name="text-format"></a>Format Texte

Si vous souhaitez lire ou écrire des données dans un fichier texte, définissez la propriété `type` dans la section `format` du jeu de données sur **TextFormat**. Vous pouvez également spécifier les propriétés **facultatives** suivantes, dans la section `format`. Consultez la section [Exemple pour TextFormat](#textformat-example) pour en savoir plus sur la méthode de configuration à suivre.

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| columnDelimiter |Caractère utilisé pour séparer les colonnes dans un fichier. Vous pouvez envisager d’utiliser un caractère non imprimable rare qui n’existe pas dans vos données. Par exemple, spécifiez « \u0001 », qui représente le début d’en-tête (SOH). |Un seul caractère est autorisé. La valeur **par défaut** est la **virgule (,)**. <br/><br/>Pour utiliser un caractère Unicode, reportez-vous à l’article sur les [caractères Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) pour obtenir le code correspondant. |Non |
| rowDelimiter |Caractère utilisé pour séparer les lignes dans un fichier. |Un seul caractère est autorisé. La valeur **par défaut** est l’une des suivantes : **[« \r\n », « \r », « \n »]** en lecture et **« \r\n »** en écriture. |Non |
| escapeChar |Caractère spécial utilisé pour échapper au délimiteur de colonnes dans le contenu du fichier d’entrée. <br/><br/>Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table. |Un seul caractère est autorisé. Aucune valeur par défaut. <br/><br/>Par exemple, si vous avez une virgule (,) comme séparateur de colonnes mais que vous voulez avoir le caractère virgule dans le texte (par exemple : « Hello, world »), vous pouvez définir « $ » comme caractère d’échappement et utiliser la chaîne « Hello$, world » dans la source. |Non |
| quoteChar |Le caractère utilisé pour entourer de guillemets une valeur de chaîne. Les séparateurs de colonnes et de lignes à l'intérieur des caractères de guillemets sont considérés comme faisant partie de la valeur de la chaîne. Cette propriété s’applique aux jeux de données d’entrée et de sortie.<br/><br/>Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table. |Un seul caractère est autorisé. Aucune valeur par défaut. <br/><br/>Par exemple, si vous avez une virgule (,) comme séparateur de colonnes mais que vous voulez avoir le caractère virgule dans le texte (par exemple : « Hello, world »), vous pouvez définir " (guillemet droit) comme caractère de guillemet et utiliser la chaîne "Hello, world" dans la source. |Non |
| nullValue |Un ou plusieurs caractères utilisés pour représenter une valeur null. |Un ou plusieurs caractères. Les valeurs **par défaut** sont **« \N » et « NULL »** en lecture, et **« \N »** en écriture. |Non |
| encodingName |Spécifier le nom d'encodage. |Une liste de noms d’encodage valides. Consultez : [Propriété Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Exemple : windows-1250 ou shift_jis. La valeur **par défaut** est **UTF-8**. |Non |
| firstRowAsHeader |Spécifie si la première ligne doit être considérée comme un en-tête. Pour un jeu de données d’entrée, Data Factory lit la première ligne comme un en-tête. Pour un jeu de données de sortie, Data Factory écrit la première ligne comme un en-tête. <br/><br/>Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios. |true<br/><b>false (valeur par défaut)</b> |Non |
| skipLineCount |Indique le nombre de lignes à ignorer lors de la lecture des données à partir des fichiers d’entrée. Si skipLineCount et firstRowAsHeader sont spécifiés, les lignes sont d’abord ignorées, puis les informations d’en-tête sont lues à partir du fichier d’entrée. <br/><br/>Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios. |Entier  |Non |
| treatEmptyAsNull |Spécifie si une chaîne null ou vide doit être traitée comme une valeur null lors de la lecture des données à partir d’un fichier d’entrée. |**True (valeur par défaut)**<br/>False |Non |

### <a name="textformat-example"></a>Exemple pour TextFormat

Dans la définition JSON suivante d’un jeu de données, certaines propriétés facultatives sont spécifiées.

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

Pour utiliser un caractère `escapeChar` au lieu de `quoteChar`, remplacez la ligne par `quoteChar`, avec le caractère escapeChar suivant :

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Scénarios d’utilisation de firstRowAsHeader et skipLineCount

* Vous copiez à partir d’une source hors fichier vers un fichier texte et vous souhaitez ajouter une ligne d’en-tête qui contient les métadonnées de schéma (par exemple : schéma SQL). Définissez le paramètre `firstRowAsHeader` sur true dans le jeu de données de sortie pour ce scénario.
* Vous copiez à partir d’un fichier texte contenant une ligne d’en-tête vers un récepteur hors fichier et souhaitez supprimer cette ligne. Définissez le paramètre `firstRowAsHeader` sur true dans le jeu de données d’entrée.
* Vous copiez à partir d’un fichier texte et souhaitez ignorer quelques lignes au début, qui ne contiennent ni données, ni informations d’en-tête. Spécifiez le paramètre `skipLineCount` pour indiquer le nombre de lignes à ignorer. Si le reste du fichier contient une ligne d’en-tête, vous pouvez également spécifier `firstRowAsHeader`. Si les paramètres `skipLineCount` et `firstRowAsHeader` sont tous deux spécifiés, les lignes sont d’abord ignorées, puis les informations d’en-tête sont lues à partir du fichier d’entrée.

## <a name="json-format"></a>Format JSON

Pour en savoir plus sur **l’importation ou l’exportation de fichiers JSON en l’état dans ou à partir d’Azure Cosmos DB**, consultez la section Importation/exportation de documents JSON de l’article [Déplacer des données vers et depuis Azure Cosmos DB](connector-azure-cosmos-db.md).

Si vous souhaitez analyser des fichiers JSON ou écrire des données au format JSON, définissez la propriété `type` de la section `format` sur **JsonFormat**. Vous pouvez également spécifier les propriétés **facultatives** suivantes, dans la section `format`. Consultez la section [Exemple pour JsonFormat](#jsonformat-example) pour en savoir plus sur la méthode de configuration à suivre.

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| filePattern |Indiquez le modèle des données stockées dans chaque fichier JSON. Les valeurs autorisées sont les suivantes : **setOfObjects** et **arrayOfObjects**. La valeur **par défaut** est **setOfObjects**. Consultez la section [Modèles de fichiers JSON](#json-file-patterns) pour en savoir plus sur ces modèles. |Non |
| jsonNodeReference | Si vous souhaitez effectuer une itération et extraire des données à partir des objets situés à l’intérieur d’un champ de tableau présentant le même modèle, spécifiez le chemin d’accès JSON de ce tableau. Cette propriété est uniquement prise en charge lors de la copie de données de fichiers JSON. | Non |
| jsonPathDefinition | Spécifiez l’expression de chemin JSON pour chaque mappage de colonne avec un nom de colonne personnalisé (commencez par une lettre minuscule). Cette propriété est uniquement prise en charge lors de la copie de données à partir de fichiers JSON, et vous pouvez extraire des données d’un objet ou d’un tableau. <br/><br/> Pour les champs situés sous l’objet racine, commencez par $ racine ; pour ceux qui se trouvent dans le tableau sélectionné par la propriété `jsonNodeReference`, commencez par l’élément de tableau. Consultez la section [Exemple pour JsonFormat](#jsonformat-example) pour en savoir plus sur la méthode de configuration à suivre. | Non |
| encodingName |Spécifiez le nom du codage. Pour obtenir une liste des noms d’encodage valides, consultez la propriété [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) . Par exemple : windows-1250 ou shift_jis. La valeur **par défaut** est : **UTF-8**. |Non |
| nestingSeparator |Caractère utilisé pour séparer les niveaux d'imbrication. La valeur par défaut est . (point). |Non |

### <a name="json-file-patterns"></a>Modèles de fichiers JSON

L’activité de copie peut analyser les modèles de fichiers JSON ci-dessous :

- **Type I : setOfObjects**

    Chaque fichier contient un objet unique, ou plusieurs objets concaténés/délimités par des lignes. Quand cette option est sélectionnée dans un jeu de données de sortie, l’activité de copie produit un seul fichier JSON contenant un objet par ligne (format délimité par des lignes).

    * **Exemple de fichier JSON à un seul objet**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **Exemple de fichier JSON incluant des objets délimités par des lignes**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **Exemple de fichier JSON incluant des objets concaténés**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **Type II : arrayOfObjects**

    Chaque fichier contient un tableau d’objets.

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a>Exemple pour JsonFormat

**Cas 1 : Copie de données à partir de fichiers JSON**

Consultez les deux exemples suivants lors de la copie des données à partir de fichiers JSON. Voici quelques points généraux à prendre en compte :

**Exemple 1 : Extraire des données d’objet et de tableau**

Dans cet exemple, un objet JSON racine doit correspondre à un seul enregistrement dans la table de résultats. Prenons un fichier JSON avec le contenu suivant :  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```

Vous voulez copier ce contenu dans un tableau SQL Azure au format suivant, en extrayant les données des objets et du tableau :

| ID | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 13/01/2017 11:24:37 |

Le jeu de données d’entrée présentant le type **JsonFormat** est défini comme suit : (définition partielle présentant uniquement les éléments pertinents). Plus précisément :

- La section `structure` définit les noms de colonne personnalisés et le type de données correspondant lors de la conversion des données au format tabulaire. Cette section est **facultative**, sauf si vous avez besoin d’effectuer un mappage de colonne. Pour plus d’informations, consultez [Mapper des colonnes d’un jeu de données source sur des colonnes d’un jeu de données de destination](copy-activity-schema-and-type-mapping.md).
- Le paramètre `jsonPathDefinition` indique le chemin JSON de chaque colonne indiquant l’emplacement à partir duquel les données sont extraites. Pour copier les données d’un tableau, vous pouvez utiliser `array[x].property` afin d’extraire la valeur de la propriété spécifiée de l’objet `xth`, ou vous pouvez utiliser `array[*].property` afin de trouver la valeur de tout objet contenant cette propriété.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}
        }
    }
}
```

**Exemple 2 : application croisée de plusieurs objets avec le même modèle à partir d’un tableau**

Dans cet exemple, vous voulez transformer un objet JSON racine en plusieurs enregistrements dans la table de résultats. Prenons un fichier JSON avec le contenu suivant :

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```

Vous souhaitez copier ce fichier dans une table SQL Azure au format suivant, en mettant à plat les données se trouvant dans le tableau et en effectuant une jointure croisée avec les informations racines communes :

| `ordernumber` | `orderdate` | `order_pd` | `order_price` | `city` |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | `[{"sanmateo":"No 1"}]` |
| 01 | 20170122 | P2 | 13. | `[{"sanmateo":"No 1"}]` |
| 01 | 20170122 | P3 | 231 | `[{"sanmateo":"No 1"}]` |


Le jeu de données d’entrée présentant le type **JsonFormat** est défini comme suit : (définition partielle présentant uniquement les éléments pertinents). Plus précisément :

- La section `structure` définit les noms de colonne personnalisés et le type de données correspondant lors de la conversion des données au format tabulaire. Cette section est **facultative**, sauf si vous avez besoin d’effectuer un mappage de colonne. Pour plus d’informations, consultez [Mapper des colonnes d’un jeu de données source sur des colonnes d’un jeu de données de destination](copy-activity-schema-and-type-mapping.md).
- Le paramètre `jsonNodeReference` indique que les données doivent être itérées et extraites des objets présentant le même modèle sous `orderlines` dans le **tableau**.
- Le paramètre `jsonPathDefinition` indique le chemin JSON de chaque colonne indiquant l’emplacement à partir duquel les données sont extraites. Dans cet exemple, les éléments `ordernumber`, `orderdate` et `city` se trouvent sous l’objet racine associé au chemin JSON commençant par `$.`, tandis que les éléments `order_pd` et `order_price` sont définis avec le chemin dérivé de l’élément de tableau sans `$.`.

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}
        }
    }
}
```

**Notez les points suivants :**

* Si les éléments `structure` et `jsonPathDefinition` ne sont pas définis dans le jeu de données Data Factory, l’activité de copie détecte le schéma à partir du premier objet et aplatit l’objet entier.
* Si l’entrée JSON contient un tableau, l’activité de copie convertit la valeur du tableau entier en une chaîne, par défaut. Vous pouvez choisir d’extraire des données de cette dernière à l’aide de `jsonNodeReference` et/ou `jsonPathDefinition`, ou ignorer cette opération en ne la spécifiant pas dans `jsonPathDefinition`.
* S’il y a plusieurs noms identiques au même niveau, l’activité de copie sélectionne le dernier nom.
* Les noms de propriété respectent la casse. Quand deux propriétés de même nom ont une casse différente, elles sont considérées comme deux propriétés distinctes.

**Cas 2 : Écriture de données dans un fichier JSON**

Vous disposez de la table suivante dans votre base de données SQL :

| ID | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3 500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

Pour chaque enregistrement, vous voulez écrire des données dans un objet JSON, en utilisant le format suivant :

```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

Le jeu de données de sortie présentant le type **JsonFormat** est défini comme suit : (définition partielle présentant uniquement les éléments pertinents). Plus précisément, la section `structure` définit les noms de propriété personnalisés dans le fichier de destination ; le paramètre `nestingSeparator` (valeur par défaut : «. ») vous permet d’identifier la couche d’imbrication à partir du nom. Cette section est **facultative**, sauf si vous souhaitez modifier le nom de propriété par rapport au nom de la colonne source, ou imbriquer certaines propriétés.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a>Format AVRO

Si vous souhaitez analyser des fichiers Avro ou écrire des données au format Avro, définissez la propriété `format` `type` sur **AvroFormat**. Il est inutile de spécifier des propriétés dans la partie Format de la section typeProperties. Exemple :

```json
"format":
{
    "type": "AvroFormat",
}
```

Pour utiliser le format Avro dans une table Hive, vous pouvez faire référence au [didacticiel Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Notez les points suivants :

* [Les types de données complexes](http://avro.apache.org/docs/current/spec.html#schema_complex) ne sont pas pris en charge (enregistrements, enums, tables, cartes, unions et fixes).

## <a name="orc-format"></a>Format ORC

Si vous souhaitez analyser des fichiers ORC ou écrire des données au format ORC, définissez la propriété `format` `type` sur **OrcFormat**. Il est inutile de spécifier des propriétés dans la partie Format de la section typeProperties. Exemple :

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> Si vous ne copiez pas les fichiers ORC **tels quels** entre les magasins de données locaux et cloud, vous devez installer JRE 8 (Java Runtime Environment) sur votre machine de passerelle. La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits. Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605). Sélectionnez la bonne version.
>

Notez les points suivants :

* Les types de données complexes ne sont pas pris en charge (STRUCT, MAP, LIST, UNION)
* Le fichier ORC a trois [options liées à la compression](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY. Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés. Il utilise le codec de compression se trouvant dans les métadonnées pour lire les données. Toutefois, lors de l’écriture dans un fichier ORC, Data Factory choisit ZLIB, qui est la valeur par défaut pour ORC. Actuellement, il n’existe aucune option permettant de remplacer ce comportement.

## <a name="parquet-format"></a>Format Parquet

Si vous souhaitez analyser des fichiers Parquet ou écrire des données au format Parquet, définissez la propriété `format` `type` sur **ParquetFormat**. Il est inutile de spécifier des propriétés dans la partie Format de la section typeProperties. Exemple :

```json
"format":
{
    "type": "ParquetFormat"
}
```

> [!IMPORTANT]
> Si vous ne copiez pas les fichiers Parquet **tels quels** entre les magasins de données locaux et cloud, vous devez installer JRE 8 (Java Runtime Environment) sur votre machine de passerelle. La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits. Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605). Sélectionnez la bonne version.
>

Notez les points suivants :

* Les types de données complexes ne sont pas pris en charge (MAP, LIST)
* Le fichier Parquet offre les options de compression suivantes : NONE, SNAPPY, GZIP et LZO. Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés. Il utilise le codec de compression se trouvant dans les métadonnées pour lire les données. Toutefois, lors de l’écriture dans un fichier Parquet, Data Factory choisit SNAPPY, qui est la valeur par défaut pour le format Parquet. Actuellement, il n’existe aucune option permettant de remplacer ce comportement.

## <a name="compression-support"></a>Prise en charge de la compression

Azure Data Factory prend en charge la compression/décompression des données pendant la copie. Quand vous spécifiez la propriété `compression` dans un jeu de données d’entrée, l’activité de copie lit les données compressées à partir de la source, puis les décompresse. Quand vous spécifiez la propriété dans un jeu de données de sortie, l’activité de copie compresse les données, puis les écrit dans le récepteur. Voici quelques exemples de scénarios :

* Lire les données compressées GZIP à partir d’un objet blob Azure, les décompresser et écrire des données du résultat dans une base de données SQL Azure. Vous définissez le jeu de données d’objets Blob Azure d’entrée avec la propriété `compression` `type` au format GZIP.
* Lire les données d’un fichier de texte brut dans le système de fichiers local, les compresser en utilisant le format GZIP et écrire les données compressées dans un objet blob Azure. Vous définissez un jeu de données d’objets Blob Azure de sortie avec la propriété `compression` `type` au format GZIP.
* Lire le fichier .zip à partir du serveur FTP, le décompresser pour accéder aux fichiers qu’il contient et placer ces derniers dans Azure Data Lake Store. Vous définissez le jeu de données FTP d’entrée avec la propriété `compression` `type` au format ZipDeflate.
* Lire les données compressées au format GZIP à partir d’un objet blob Azure, les décompresser, les compresser en utilisant le format BZIP2 et écrire les données résultantes dans un objet blob Azure. Vous définissez le jeu de données d’objet blob Azure d’entrée avec le paramètre `compression` `type` défini sur GZIP et le jeu de données de sortie avec le paramètre `compression` `type` défini sur BZIP2.

Pour spécifier la compression pour un jeu de données, utilisez la propriété **compression** du jeu de données JSON, comme dans l'exemple suivant :   

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": {
            "referenceName": "StorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "fileName": "pagecounts.csv.gz",
            "folderPath": "compression/file/",
            "format": {
                "type": "TextFormat"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

La section **compression** a deux propriétés :

* **Type** : le codec de compression, qui peut être **GZIP**, **Deflate**, **BZIP2** ou **ZipDeflate**.
* **Level** : le taux de compression, qui peut être **Optimal** ou **Fastest**.

  * **Fastest** : l'opération de compression doit se terminer le plus rapidement possible, même si le fichier résultant n'est pas compressé de façon optimale.
  * **Optimal**: l'opération de compression doit aboutir à une compression optimale, même si l'opération prend plus de temps.

    Pour plus d’informations, consultez la rubrique [Niveau de compression](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .

> [!NOTE]
> Les paramètres de compression ne sont pas pris en charge pour les données au format **AvroFormat**, **OrcFormat** ou **ParquetFormat**. Data Factory détecte et utilise le codec de compression se trouvant dans les métadonnées pour lire des fichiers présentant ces formats. Lors de l’écriture dans des fichiers présentant ces formats, Data Factory choisit le code de la compression par défaut pour ce format. Par exemple, ZLIB pour OrcFormat et SNAPPY pour ParquetFormat.

## <a name="next-steps"></a>Étapes suivantes

Consultez les articles suivants pour connaître les magasins de données basés sur un fichier qui sont pris en charge par Azure Data Factory :

- [Connecteur Stockage Blob Azure](connector-azure-blob-storage.md)
- [Connecteur Azure Data Lake Store](connector-azure-data-lake-store.md)
- [Connecteur Amazon S3](connector-amazon-simple-storage-service.md)
- [Connecteur de système de fichiers](connector-file-system.md)
- [Connecteur FTP](connector-ftp.md)
- [Connecteur SFTP](connector-sftp.md)
- [Connecteur HDFS](connector-hdfs.md)
- [Connecteur HTTP](connector-http.md)