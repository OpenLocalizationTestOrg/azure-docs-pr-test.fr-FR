## <a name="specifying-structure-definition-for-rectangular-datasets"></a>Spécification de la définition de la structure des jeux de données rectangulaires
Bonjour section structure dans les jeux de données hello JSON est un **facultatif** section pour les tables rectangulaires (avec des lignes et colonnes) et contient une collection de colonnes de table de hello. Vous allez utiliser la section de structure hello pour des informations de type en fournissant des conversions de type ou du mappage de colonnes. Hello les sections suivantes décrire ces fonctionnalités en détail. 

Chaque colonne contient hello propriétés suivantes :

| Propriété | Description | Requis |
| --- | --- | --- |
| name |Nom de colonne de hello. |Oui |
| type |Type de données de colonne de hello. Pour plus d’informations sur le moment où vous devez spécifier les informations de type, consultez la section des conversions de type ci-dessous. |Non |
| culture |.NET basée toobe culture utilisée lorsque le type est spécifié et qu’il est de type .NET Datetime ou Datetimeoffset. La valeur par défaut est « fr-fr ». |Non |
| format |Mettre en forme toobe de chaîne utilisé lorsque le type est spécifié et qu’il est de type .NET Datetime ou Datetimeoffset. |Non |

Hello exemple suivant illustre le section hello structure JSON pour une table qui comporte trois colonnes nom d’utilisateur, le nom et lastlogindate.

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

Utilisez hello suivant les instructions pour l’information de « structure » tooinclude et quelles tooinclude Bonjour **structure** section.

* **Pour les sources de données structurées** qui stockent des informations de schéma et de type de données ainsi que les données hello lui-même (sources comme table de Azure de SQL Server, Oracle, etc.), vous devez spécifier la section « structure » de hello uniquement si vous voulez faire mappage de colonnes spécifiques les colonnes sources sont des colonnes toospecific dans leurs noms et de récepteur ne Hello pas identiques (voir les détails dans la section de mappage de colonne ci-dessous). 
  
    Comme indiqué ci-dessus, les informations de type hello sont facultatives dans la section « structure ». Pour les sources structurés, les informations de type sont déjà disponibles dans le cadre de la définition de dataset dans le magasin de données hello, par conséquent, n’incluez pas les informations de type lorsque vous incluez la section « structure » de hello.
* **Pour le schéma sur les sources de données de lecture (en particulier les blob Azure)** vous pouvez choisir les données toostore sans stocker toutes les informations de type ou de schéma avec des données hello. Pour ces types de sources de données, vous devez inclure « structure » Bonjour suivant 2 cas :
  * Vous souhaitez que le mappage de colonnes toodo.
  * Lorsque hello le jeu de données est une source dans une activité de copie, vous pouvez fournir des informations de type dans « structure » et la fabrique de données utilisera ces informations de type pour la conversion des types de toonative pour le récepteur de hello. Consultez [déplacer tooand de données à partir d’objets Blob Azure](../articles/data-factory/data-factory-azure-blob-connector.md) article pour plus d’informations.

### <a name="supported-net-based-types"></a>Types .NET pris en charge
Données fabrique prend en charge hello suivant .NET de conforme CLS en fonction des valeurs de type qui fournit des informations de type dans « structure » pour le schéma sur les sources de données en lecture comme objets blob Azure.

* Int16
* Int32 
* Int64
* Single
* Double
* DÉCIMAL
* Byte[]
* Bool
* String 
* Guid
* Datetime
* Datetimeoffset
* Timespan 

Pour Datetime et Datetimeoffset vous pouvez spécifier « culture » et « format » chaîne toofacilitate d’analyse de votre chaîne de date/heure personnalisé. Consultez l’exemple de conversion de type ci-dessous.

