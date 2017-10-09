## <a name="specifying-formats"></a>Spécification des formats
Azure Data Factory prend en charge hello les types de format suivants :

* [Format Texte](#specifying-textformat)
* [Format JSON](#specifying-jsonformat)
* [Format Avro](#specifying-avroformat)
* [Format ORC](#specifying-orcformat)
* [Format Parquet](#specifying-parquetformat)

### <a name="specifying-textformat"></a>Définition de TextFormat
Si vous souhaitez que les fichiers de texte hello tooparse ou écrivez les données de salutation au format texte, la valeur hello `format` `type` propriété trop**TextFormat**. Vous pouvez également spécifier les éléments suivants de hello **facultatif** propriétés Bonjour `format` section. Consultez [TextFormat exemple](#textformat-example) section sur la façon de tooconfigure.

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| columnDelimiter |caractère de Hello utilisé tooseparate colonnes dans un fichier. Vous pouvez envisager d’un caractère non imprimable rares qui se ne trouve pas probablement toouse dans vos données : par exemple, spécifiez « \u0001 » qui représente le début de titre (SOH). |Un seul caractère est autorisé. Hello **par défaut** valeur est **virgule («, »)**. <br/><br/>toouse un caractère Unicode, consultez trop[caractères Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello code correspondant pour celle-ci. |Non |
| rowDelimiter |caractère de Hello utilisé tooseparate lignes dans un fichier. |Un seul caractère est autorisé. Hello **par défaut** valeur est une des valeurs suivantes lors de la lecture de hello : **[« \r\n », « \r », « \n »]** et **« \r\n »** lors de l’écriture. |Non |
| escapeChar |un caractère spécial Hello utilisé tooescape un délimiteur de colonne dans le contenu du fichier d’entrée hello. <br/><br/>Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table. |Un seul caractère est autorisé. Aucune valeur par défaut. <br/><br/>Exemple : Si vous utilisez une virgule («, ») comme délimiteur de colonne hello mais que vous voulez que virgule toohave hello dans le texte hello (exemple : « Hello, world »), vous pouvez définir « $» comme caractère d’échappement hello et utilisez la chaîne « $Hello, world » dans la source de hello. |Non |
| quoteChar |caractère de Hello utilisé tooquote une valeur de chaîne. séparateurs de ligne et de colonne Hello à l’intérieur des guillemets hello sont traités en tant que partie de la valeur de chaîne hello. Cette propriété est applicable tooboth entrée et de sortie des jeux de données.<br/><br/>Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table. |Un seul caractère est autorisé. Aucune valeur par défaut. <br/><br/>Par exemple, si vous utilisez une virgule («, ») comme délimiteur de colonne hello, mais vous voulez que virgule toohave dans le texte hello (exemple : < Hello, world >), vous pouvez définir « (guillemets doubles) comme hello guillemet et utilisez hello chaîne « Hello, world » dans la source de hello. |Non |
| nullValue |Un ou plusieurs caractères utilisés toorepresent une valeur null. |Un ou plusieurs caractères. Hello **par défaut** les valeurs sont **« \N » et « NULL »** lors de la lecture et **« \N »** lors de l’écriture. |Non |
| encodingName |Spécifiez le nom de codage hello. |Une liste de noms d’encodage valides. Consultez : [Propriété Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Exemple : windows-1250 ou shift_jis. Hello **par défaut** valeur est **UTF-8**. |Non |
| firstRowAsHeader |Spécifie si tooconsider hello la première ligne comme un en-tête. Pour un jeu de données d’entrée, Data Factory lit la première ligne comme un en-tête. Pour un jeu de données de sortie, Data Factory écrit la première ligne comme un en-tête. <br/><br/>Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios. |true<br/>**false (valeur par défaut)** |Non |
| skipLineCount |Indique le nombre de hello de lignes tooskip lors de la lecture des données à partir des fichiers d’entrée. Si skipLineCount et firstRowAsHeader sont spécifiés, les lignes de hello sont ignorées tout d’abord, et ensuite les informations d’en-tête hello sont en lecture à partir du fichier d’entrée de hello. <br/><br/>Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios. |Entier  |Non |
| treatEmptyAsNull |Spécifie si la valeur tootreat null ou une chaîne vide comme une valeur null lorsque la lecture des données à partir d’un fichier d’entrée. |**True (valeur par défaut)**<br/>False |Non |

#### <a name="textformat-example"></a>Exemple pour TextFormat
Hello exemple suivant illustre certaines des propriétés de format hello pour TextFormat.

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

toouse un `escapeChar` au lieu de `quoteChar`, remplacez la ligne hello avec `quoteChar` avec hello suivant dont :

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Scénarios d’utilisation de firstRowAsHeader et skipLineCount
* Vous copiez à partir d’un fichier de texte source de fichier non tooa et que vous souhaitez tooadd une ligne d’en-tête contenant des métadonnées de schéma hello (par exemple : schéma SQL). Spécifiez `firstRowAsHeader` comme true dans le dataset de sortie hello pour ce scénario.
* Vous copiez à partir d’un fichier texte contenant un récepteur les fichiers d’en-tête ligne tooa et que vous souhaitez toodrop de ligne. Spécifiez `firstRowAsHeader` comme true dans le jeu de données d’entrée hello.
* Vous copiez à partir d’un fichier texte et que vous souhaitez tooskip quelques lignes au début de hello qui ne contiennent aucune information d’en-tête ou de données. Spécifiez `skipLineCount` nombre de hello tooindicate de lignes toobe ignorés. Si le reste hello du fichier de hello contient une ligne d’en-tête, vous pouvez également spécifier `firstRowAsHeader`. Si les deux `skipLineCount` et `firstRowAsHeader` sont spécifiés, les lignes de hello sont ignorées tout d’abord, et ensuite les informations d’en-tête hello sont en lecture à partir du fichier d’entrée de hello

### <a name="specifying-jsonformat"></a>Définition de JsonFormat
trop**importation/exportation de fichiers JSON en tant que-est dans/à partir de la base de données Azure Cosmos**, consultez [documents JSON d’importation/exportation](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section dans le connecteur de base de données Azure Cosmos hello avec les détails.

Si vous souhaitez que les fichiers JSON tooparse hello ou écrivez des données de salutation au format JSON, définissez hello `format` `type` propriété trop**JsonFormat**. Vous pouvez également spécifier les éléments suivants de hello **facultatif** propriétés Bonjour `format` section. Consultez [JsonFormat exemple](#jsonformat-example) section sur la façon de tooconfigure.

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| filePattern |Indiquer le motif hello des données stockées dans chaque fichier JSON. Les valeurs autorisées sont les suivantes : **setOfObjects** et **arrayOfObjects**. Hello **par défaut** valeur est **setOfObjects**. Consultez la section [Modèles de fichiers JSON](#json-file-patterns) pour en savoir plus sur ces modèles. |Non |
| jsonNodeReference | Si vous souhaitez tooiterate et extrayez des données à partir des objets hello à l’intérieur d’un tableau de champ par hello même modèle, spécifiez le chemin d’accès JSON hello de ce tableau. Cette propriété est uniquement prise en charge lors de la copie de données de fichiers JSON. | Non |
| jsonPathDefinition | Spécifiez l’expression de chemin JSON hello pour chaque mappage de colonne avec un nom de colonne personnalisée (commencent par des minuscules). Cette propriété est uniquement prise en charge lors de la copie de données à partir de fichiers JSON, et vous pouvez extraire des données d’un objet ou d’un tableau. <br/><br/> Pour les champs sous l’objet racine, commencer par $ de la racine ; pour les champs de tableau hello choisi par `jsonNodeReference` propriété, lancement à partir de l’élément de tableau hello. Consultez [JsonFormat exemple](#jsonformat-example) section sur la façon de tooconfigure. | Non |
| encodingName |Spécifiez le nom de codage hello. Pour hello la liste des noms de codage valides, consultez : [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) propriété. Par exemple : windows-1250 ou shift_jis. Hello **par défaut** valeur est : **UTF-8**. |Non |
| nestingSeparator |Caractère utilisé tooseparate des niveaux d’imbrication. Hello la valeur par défaut est «. » (point). |Non |

#### <a name="json-file-patterns"></a>Modèles de fichiers JSON

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

#### <a name="jsonformat-example"></a>Exemple pour JsonFormat

**Cas 1 : Copie de données à partir de fichiers JSON**

Consultez ci-dessous les deux types d’exemples lors de la copie des données à partir de fichiers JSON et hello points générique toonote :

**Exemple 1 : Extraire des données d’objet et de tableau**

Dans cet exemple, vous prévoyez un objet JSON de racine mappe enregistrement toosingle de résultats tabulaire. Si vous disposez d’un fichier JSON avec hello suivant le contenu :  

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
et que vous souhaitez toocopy dans une table SQL Azure suivante de hello mettre en forme, en extrayant les données à partir des objets et de tableau :

| id | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 13/01/2017 11:24:37 |

jeu de données d’entrée Hello avec **JsonFormat** type est défini comme suit : (définition partielle avec uniquement les parties pertinentes hello). Plus précisément :

- `structure`section définit les noms de colonne de hello personnalisé et type de données correspondant hello lors de la conversion des données de tootabular. Cette section est **facultatif** , sauf si vous avez besoin de mappage de colonne toodo. Pour en savoir plus, voir [Spécification de la définition de la structure des jeux de données rectangulaires](#specifying-structure-definition-for-rectangular-datasets).
- `jsonPathDefinition`Spécifie le chemin d’accès JSON hello pour chaque colonne qui indique où tooextract hello des données à partir de. toocopy des données à partir du tableau, vous pouvez utiliser **propriété de tableau [x]** tooextract valeur hello donné de propriété d’objet de x hello, ou vous pouvez utiliser  **tableau [*] propriété** toofind valeur Hello à partir de n’importe quel objet contenant la propriété de ce type.

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

**Exemple 2 : Cross-appliquer plusieurs objets avec hello même modèle de tableau**

Cet exemple, vous prévoyez d’un objet JSON racine tootransform en plusieurs enregistrements dans la table de résultats. Si vous disposez d’un fichier JSON avec hello suivant le contenu :  

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
et vous souhaitez toocopy dans une table SQL Azure suivante de hello mettre en forme, par la mise à plat de données hello à l’intérieur du tableau de hello et cross join avec des informations racine commun hello :

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13. | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

jeu de données d’entrée Hello avec **JsonFormat** type est défini comme suit : (définition partielle avec uniquement les parties pertinentes hello). Plus précisément :

- `structure`section définit les noms de colonne de hello personnalisé et type de données correspondant hello lors de la conversion des données de tootabular. Cette section est **facultatif** , sauf si vous avez besoin de mappage de colonne toodo. Pour en savoir plus, voir [Spécification de la définition de la structure des jeux de données rectangulaires](#specifying-structure-definition-for-rectangular-datasets).
- `jsonNodeReference`Indique tooiterate et extraire des données à partir des objets hello avec hello même motif sous **tableau** orderlines.
- `jsonPathDefinition`Spécifie le chemin d’accès JSON hello pour chaque colonne qui indique où tooextract hello des données à partir de. Dans cet exemple, « ordernumber », « date » et « city » sont sous l’objet racine avec le chemin d’accès JSON en commençant par « $»., alors que « order_pd » et « order_price » sont définies avec le chemin d’accès dérivée de l’élément de tableau hello sans « $»..

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

**Hello Notez les points suivants :**

* Si hello `structure` et `jsonPathDefinition` ne sont pas définis dans le jeu de données Data Factory hello, hello détecte de l’activité de copie hello de schéma à partir du premier objet de hello et aplatir la totalité de l’objet hello.
* Si l’entrée JSON hello possède un tableau, par défaut, hello activité de copie convertit hello tableau entier valeur en une chaîne. Vous pouvez choisir à l’aide de données de tooextract `jsonNodeReference` et/ou `jsonPathDefinition`, ou la passer en ne spécifiant dans `jsonPathDefinition`.
* S’il existe en double noms à hello même niveau, hello activité de copie sélectionne hello dernière.
* Les noms de propriété respectent la casse. Quand deux propriétés de même nom ont une casse différente, elles sont considérées comme deux propriétés distinctes.

**Cas 2 : L’écriture du fichier tooJSON de données**

Vous disposez de la table ci-dessous dans votre base de données SQL :

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3 500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

et pour chaque enregistrement, vous attendez l’objet JSON tooa à toowrite dans au-dessous de format :
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

dataset à l’aide de sortie Hello **JsonFormat** type est défini comme suit : (définition partielle avec uniquement les parties pertinentes hello). Plus spécifiquement, `structure` section définit les noms de propriété hello personnalisé dans le fichier de destination, `nestingSeparator` (valeur par défaut est «. ») sera couche d’imbrication de hello tooidentify utilisé à partir du nom de hello. Cette section est **facultatif** sauf si vous souhaitez que le nom de la propriété hello toochange la comparaison avec le nom de la colonne source, ou imbriquer des propriétés de hello.

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

### <a name="specifying-avroformat"></a>Définition d'AvroFormat
Si vous souhaitez que les fichiers de Avro tooparse hello ou écrivez des données de hello dans le format Avro, la valeur hello `format` `type` propriété trop**AvroFormat**. Il est inutile toospecify toutes les propriétés de la section de Format hello dans la section de typeProperties hello. Exemple :

```json
"format":
{
    "type": "AvroFormat",
}
```

le format Avro toouse dans une table Hive, vous pouvez faire référence trop[didacticiel d’Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Hello Notez les points suivants :  

* [Les types de données complexes](http://avro.apache.org/docs/current/spec.html#schema_complex) ne sont pas pris en charge (enregistrements, enums, tableaux, cartes, unions et fixes).

### <a name="specifying-orcformat"></a>Spécification d’OrcFormat
Si vous souhaitez tooparse hello ORC fichiers ou écrivez des données de hello dans format ORC, définissez hello `format` `type` propriété trop**OrcFormat**. Il est inutile toospecify toutes les propriétés de la section de Format hello dans la section de typeProperties hello. Exemple :

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> Si vous ne copiez pas les fichiers ORC **comme-est** entre locaux et cloud magasins de données, vous devez tooinstall hello 8 de JRE (Java Runtime Environment) sur votre ordinateur de passerelle. La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits. Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605). Choisir hello approprié.
>
>

Hello Notez les points suivants :

* Les types de données complexes ne sont pas pris en charge (STRUCT, MAP, LIST, UNION)
* Le fichier ORC a trois [options liées à la compression](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY. Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés. Il utilise la compression de hello codec est dans les données de salutation métadonnées tooread hello. Toutefois, lors de l’écriture de fichier ORC de tooan, Data Factory choisit ZLIB, qui est la valeur par défaut de hello pour ORC. Il n’existe actuellement aucune toooverride option ce comportement.

### <a name="specifying-parquetformat"></a>Spécification de ParquetFormat
Si vous souhaitez que les fichiers de Parquet tooparse hello ou écrivez des données de hello au format de Parquet, définissez hello `format` `type` propriété trop**ParquetFormat**. Il est inutile toospecify toutes les propriétés de la section de Format hello dans la section de typeProperties hello. Exemple :

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> Si vous ne copiez pas les fichiers Parquet **comme-est** entre locaux et cloud magasins de données, vous devez tooinstall hello 8 de JRE (Java Runtime Environment) sur votre ordinateur de passerelle. La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits. Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605). Choisir hello approprié.
>
>

Hello Notez les points suivants :

* Les types de données complexes ne sont pas pris en charge (MAP, LIST)
* Fichier de parquet a hello liés à la compression des options suivantes : NONE, SNAPPY, GZIP et LZO. Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés. Elle utilise le codec de compression hello dans les données de salutation métadonnées tooread hello. Toutefois, lors de l’écriture du fichier de Parquet tooa, fabrique de données choisit SNAPPY, valeur par défaut de hello pour le format Parquet. Il n’existe actuellement aucune toooverride option ce comportement.
