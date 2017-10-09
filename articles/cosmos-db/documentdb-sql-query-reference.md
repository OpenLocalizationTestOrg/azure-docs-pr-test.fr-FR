---
titre : aaa « API de DocumentDB de base de données Azure Cosmos : syntaxe SQL | Description de Microsoft Docs » : consultez la documentation pour hello langage de requête Azure Cosmos API DB DocumentDB SQL.
Services : cosmos-db auteur : Gestionnaire de mimig1 : jhubbard éditeur : mimig documentationcenter : ».

MS.AssetId : ms.service : cosmos-db ms.workload : services de données ms.tgt_pltfrm : na ms.devlang : na ms.topic : référence ms.date : 06/13/2017 ms.author : mimig

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a>API DocumentDB Azure Cosmos DB : référence de syntaxe SQL

Hello Azure Cosmos DB DocumentDB API prend en charge des documents interrogation à l’aide d’un familière de type SQL (Structured Query Language) grammaire sur des documents JSON hiérarchiques sans schéma explicite ou la création d’index secondaires. Cette rubrique fournit la documentation de référence pour hello langage de requête SQL d’API DocumentDB.

Pour une procédure pas à pas de hello langage de requête DocumentDB API SQL, consultez [requêtes SQL pour l’API Azure Cosmos DB DocumentDB](documentdb-sql-query.md).  
  
Nous vous invitons également toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) où vous pouvez essayer de base de données Azure Cosmos et exécuter des requêtes SQL sur notre jeu de données.  
  
## <a name="select-query"></a>Requête SELECT  
Récupère les documents JSON à partir de la base de données hello. Prend en charge d’évaluation d’expressions, les projections, le filtrage et les jointures.  les conventions de Hello utilisées pour décrire les instructions SELECT hello sont sous forme de tableau dans la section conventions de syntaxe de hello.  
  
**Syntaxe**  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 **Notes**  
  
 Pour plus d’informations sur chaque clause, consultez les sections suivantes :  
  
-   [Clause SELECT](#bk_select_query)  
  
-   [Clause FROM](#bk_from_clause)  
  
-   [Clause WHERE](#bk_where_clause)  
  
-   [Clause ORDER BY](#bk_orderby_clause)  
  
clauses Hello dans l’instruction SELECT de hello doivent être classés comme indiqué ci-dessus. L’une des clauses facultatives de hello peut être omise. Mais lorsque clauses facultatives sont utilisées, elles doivent apparaître dans le bon ordre de hello.  
  
**Ordre logique de traitement de l’instruction SELECT de hello**  
  
commande Hello dans lequel les clauses sont traités est la suivante :  

1.  [Clause FROM](#bk_from_clause)  
2.  [Clause WHERE](#bk_where_clause)  
3.  [Clause ORDER BY](#bk_orderby_clause)  
4.  [Clause SELECT](#bk_select_query)  

Notez que cela est différent de hello dans lequel ils apparaissent dans la syntaxe de hello. classement de Hello est telle que tous les nouveaux symboles introduits par une clause traitée sont visibles et peuvent être utilisés dans des clauses traitées ultérieurement. Par exemple, les alias déclarés dans une clause FROM sont accessibles dans les clauses WHERE et SELECT.  

**Commentaires et espaces blancs**  

Tous les espaces blancs qui ne font pas partie d’une chaîne entre guillemets ou identificateur entre guillemets ne font pas partie de la grammaire du langage hello et sont ignorés lors de l’analyse.  

langage de requête Hello prend en charge les commentaires de style T-SQL comme  

-   Instruction SQL `-- comment text [newline]`  

Alors que commentaires et espaces blancs n’ont pas d’importance dans la grammaire de hello, ils doivent être des jetons tooseparate utilisé. Par exemple : `-1e5` est un jeton à numéro unique, alors que `: – 1 e5` est un jeton moins suivi du chiffre 1 et de l’identificateur e5.  

##  <a name="bk_select_query"></a> Clause SELECT  
clauses Hello dans l’instruction SELECT de hello doivent être classés comme indiqué ci-dessus. L’une des clauses facultatives de hello peut être omise. Mais lorsque clauses facultatives sont utilisées, elles doivent apparaître dans le bon ordre de hello.  

**Syntaxe**  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 **Arguments**  
  
 `<select_specification>`  
  
 Toobe propriétés ou la valeur sélectionnée pour le résultat de hello définie.  
  
 `'*'`  
  
Spécifie que la valeur de hello doit être récupérée sans apporter de modifications. En particulier si la valeur de hello traité est un objet, toutes les propriétés seront récupérées.  
  
 `<object_property_list>`  
  
Spécifie la liste hello de toobe propriétés récupérée. Chaque valeur retournée sera un objet avec les propriétés hello spécifiées.  
  
`VALUE`  
  
Spécifie que la valeur JSON hello doit être récupéré au lieu de l’objet JSON complet de hello. Cela, contrairement à `<property_list>` n’encapsule pas de valeur de hello projeté dans un objet.  
  
`<scalar_expression>`  
  
Expression représentant hello valeur toobe calculée. Consultez la section [Expressions scalaires](#bk_scalar_expressions) pour plus d’informations.  
  
**Remarques**  
  
Hello `SELECT *` syntaxe est valide uniquement si la clause FROM a déclaré un seul alias. `SELECT *` fournit une projection d’identité, ce qui peut être utile si aucune projection n’est nécessaire. SELECT * est valide uniquement si la clause FROM est spécifiée et n’a introduit qu’une seule source d’entrée.  
  
Notez que `SELECT <select_list>` et `SELECT *` sont ce qu’on appelle du « sucre syntaxique » et que vous pouvez également les exprimer à l’aide d’instructions SELECT simples, comme indiqué ci-dessous.  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     équivaut à :  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     équivaut à :  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
**Voir aussi**  
  
[Expressions scalaires](#bk_scalar_expressions)  
[Clause SELECT](#bk_select_query)  
  
##  <a name="bk_from_clause"></a> Clause FROM  
Spécifie les hello ou les sources jointes. Hello FROM clause est facultative. Si elle n’est pas spécifiée, les autres clauses sont exécutées comme si la clause FROM fournissait un document unique.  
  
**Syntaxe**  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
**Arguments**  
  
`<from_source>`  
  
Spécifie une source de données, avec ou sans alias. Si aucun alias n’est spécifié, il est déduit de hello `<collection_expression>` à l’aide de règles suivantes :  
  
-   Si l’expression de hello est collection_name, puis nom_collection servira en tant qu’alias.  
  
-   Si l’expression de hello est `<collection_expression>`, property_name, property_name sera utilisée en tant qu’alias. Si l’expression de hello est collection_name, puis nom_collection servira en tant qu’alias.  
  
AS `input_alias`  
  
Spécifie que hello `input_alias` est un ensemble de valeurs renvoyées par hello sous-jacent expression de collection.  
 
`input_alias` IN  
  
Spécifie que hello `input_alias` doit représenter l’ensemble de hello des valeurs obtenues en effectuant une itération sur tous les éléments du tableau de chaque tableau retourné par hello sous-jacent expression de collection. Toute valeur retournée par l’expression de collection sous-jacente qui n’est pas un tableau est ignorée.  
  
`<collection_expression>`  
  
Spécifie tooretrieve hello documents utilisés par hello collection expression toobe.  
  
`ROOT`  
  
Spécifie qu’un document doit être récupéré à partir de hello collection par défaut, actuellement connectée.  
  
`collection_name`  
  
Spécifie qu’un document doit être récupéré à partir de la collection de hello fourni. nom Hello de collection de hello doit correspondre au nom hello de collection hello actuellement connectée.  
  
`input_alias`  
  
Spécifie qu’un document doit être récupéré à partir de hello autre source définie par l’alias de hello fourni.  
  
`<collection_expression> '.' property_`  
  
Spécifie qu’un document doit être récupéré en accédant à hello `property_name` élément de tableau de propriété ou array_index pour tous les documents récupérés par l’expression de la collection spécifiée.  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
Spécifie qu’un document doit être récupéré en accédant à hello `property_name` élément de tableau de propriété ou array_index pour tous les documents récupérés par l’expression de la collection spécifiée.  
  
**Remarques**  
  
Tous les alias fournis ou déduits dans hello `<from_source>(`s) doivent être uniques. Hello syntaxe `<collection_expression>.`property_name est hello identique `<collection_expression>' ['"property_name"']'`. Toutefois, la syntaxe de cette dernière de hello peut être utilisée si un nom de propriété contient des caractères non-identifiants.  
  
**Gestion des propriétés manquantes, des éléments de tableau manquants et des valeurs non définies**  
  
Si une expression de collection accède à des propriétés ou éléments de tableau et que la valeur n’existe pas, cette valeur sera ignorée et n’est plus traitée.  
  
**Étendue de contexte d’expression de collection**  
  
Une expression de collection peut avoir une étendue de document ou de collection :  
  
-   Une expression est étendue à une collection, si hello source sous-jacente de l’expression de collection hello est ROOT ou `collection_name`. Une telle expression représente un ensemble de documents récupérés directement à partir de la collection de hello et n’est pas dépendante de traitement hello d’autres expressions de collection.  
  
-   Une expression est étendu à un document, si hello source sous-jacente de l’expression de collection hello `input_alias` introduit précédemment dans la requête de hello. Une telle expression représente un ensemble de documents obtenus en évaluant l’expression de collection hello dans la portée de hello de chaque document appartenant ensemble toohello associée hello alias collection.  Hello résultante sera une union de jeux obtenus en évaluant l’expression de collection hello pour chacun des documents hello Bonjour sous-jacent ensemble.  
  
**Jointures**  
  
Dans la version actuelle de hello, base de données Azure Cosmos prend en charge les jointures internes. Des fonctionnalités de jointure supplémentaires sont à venir.

Les jeux de résultats des jointures internes dans un produit croisé complet de hello participant à la jointure de hello. résultat de Hello d’une jointure N-way est un jeu de tuples de N éléments, où chaque valeur dans le tuple de hello est associé à un alias de hello définir participant dans une jointure de hello et sont accessibles en référençant cet alias dans d’autres clauses.  
  
évaluation de Hello de jointure de hello dépend de la portée du contexte hello Hello participant à des jeux :  
  
-  Une jointure entre un jeu de collection A et un jeu à étendue de collection B aboutit à un produit croisé de tous les éléments des jeux A et B.
  
-   Une jointure entre le jeu A et le jeu à étendue de document B aboutit à une union de tous les jeux obtenus en évaluant le jeu à étendue de document B pour chaque document du jeu A.  
  
 Dans la version actuelle de hello, un maximum d’une expression à une collection est pris en charge par le processeur de requêtes hello.  
  
**Exemples de jointures :**  
  
Examinons hello après la clause FROM :`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`  
  
 Laissez chaque source définir `input_alias1, input_alias2, …, input_aliasN`. La close FROM renvoie un ensemble de N-tuples (un tuple avec N valeurs). Les valeurs de chaque tuple sont produites par l'itération de tous les alias de la collection sur leurs ensembles respectifs.  
  
*Exemple de JOIN 1, avec 2 sources :*  
  
- Laissez `<from_source1>` être étendu à une collection et représenter le jeu {A, B, C}.  
  
- Laissez `<from_source2>` être étendu à un document référençant input_alias1 et représenter les jeux :  
  
    {1, 2} pour `input_alias1 = A,`  
  
    {3} pour `input_alias1 = B,`  
  
    {4, 5} pour `input_alias1 = C,`  
  
- Bonjour à partir de la clause `<from_source1> JOIN <from_source2>` entraîne hello suivant tuples :  
  
    (`input_alias1, input_alias2`):  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
*Exemple de JOIN 2, avec 3 sources :*  
  
- Laissez `<from_source1>` être étendu à une collection et représenter le jeu {A, B, C}.  
  
- Laissez `<from_source2>` être étendu à un document référençant input_`input_alias1` et représenter les jeux :  
  
    {1, 2} pour `input_alias1 = A,`  
  
    {3} pour `input_alias1 = B,`  
  
    {4, 5} pour `input_alias1 = C,`  
  
- Laissez `<from_source3>` être étendu à un document référençant input_`input_alias2` et représenter les jeux :  
  
    {100, 200} pour `input_alias2 = 1,`  
  
    {300} pour `input_alias2 = 3,`  
  
- Bonjour à partir de la clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` entraîne hello suivant tuples :  
  
    (input_alias1, input_alias2, input_alias3) :  
  
    (A, 1, 100), (A, 1, 200), (B, 3, 300)  
  
> [!NOTE]
> Absence de tuples pour d’autres valeurs de `input_alias1`, `input_alias2`, pour quels hello `<from_source3>` n’a pas retourné de toutes les valeurs.  
  
*Exemple de JOIN 3, avec 3 sources :*  
  
- Laissez <from_source1> être étendu à une collection et représenter le jeu {A, B, C}.  
  
- Laissez `<from_source1>` être étendu à une collection et représenter le jeu {A, B, C}.  
  
- Laissez <from_source2> être étendu à un document référençant input_source1 et représenter les jeux :  
  
    {1, 2} pour `input_alias1 = A,`  
  
    {3} pour `input_alias1 = B,`  
  
    {4, 5} pour `input_alias1 = C,`  
  
- Laisser `<from_source3>` étendu trop`input_alias1` et représente des jeux :  
  
    {100, 200} pour `input_alias2 = A,`  
  
    {300} pour `input_alias2 = C,`  
  
- Bonjour à partir de la clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` entraîne hello suivant tuples :  
  
    (`input_alias1, input_alias2, input_alias3`):  
  
    (A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)  
  
> [!NOTE]
> Cela a abouti à un produit croisé entre `<from_source2>` et `<from_source3>` , car les deux sont incluses dans l’étendue toohello même `<from_source1>`.  Cela a about à 4 (2 x 2) tuples de valeur A, 0 tuple de valeur B (1 x 0) et 2 (2 x 1) tuples de valeur C.  
  
**Voir aussi**  
  
 [Clause SELECT](#bk_select_query)  
  
##  <a name="bk_where_clause"></a> Clause WHERE  
 Spécifie la condition de recherche hello pour les documents hello retourné par la requête de hello.  
  
 **Syntaxe**  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 **Arguments**  
  
-   `<filter_condition>`  
  
     Spécifie les hello toobe de condition remplie pour hello documents toobe est retourné.  
  
-   `<scalar_expression>`  
  
     Expression représentant hello valeur toobe calculée. Consultez hello [expressions scalaires](#bk_scalar_expressions) pour plus d’informations.  
  
 **Remarques**  
  
 Dans l’ordre pour hello document toobe retourné une expression spécifiée comme condition de filtre doit évaluer tootrue. Seule la valeur booléenne true satisfait la condition de hello, toute autre valeur : undefined, null, la valeur est false, nombre, un tableau ou objet, ne satisfait pas la condition de hello.  
  
##  <a name="bk_orderby_clause"></a> Clause ORDER BY  
 Spécifie les hello ordre de tri des résultats retournés par la requête de hello.  
  
 **Syntaxe**  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 **Arguments**  
  
-   `<sort_specification>`  
  
     Spécifie une propriété ou une expression sur laquelle l’ensemble de résultats de requête toosort hello. Une colonne de tri peut être spécifiée comme un alias de nom ou de la colonne.  
  
     Plusieurs colonnes de tri peuvent être spécifiées. Les noms de colonne doivent être uniques. séquence Hello hello des colonnes de tri dans la clause ORDER BY hello définit organisation hello hello triée de jeu de résultats. Autrement dit, jeu de résultats hello est triée par la propriété de première hello et ensuite cette liste triée est triée par la deuxième propriété de hello et ainsi de suite.  
  
     noms des colonnes référencées dans la clause ORDER BY hello Hello doivent correspondre tooeither une colonne Bonjour sélectionner la colonne de liste ou tooa définie dans une table spécifiée dans la clause FROM de hello sans ambiguïté.  
  
-   `<sort_expression>`  
  
     Spécifie une propriété unique ou une expression sur le jeu de résultats de requête toosort hello.  
  
-   `<scalar_expression>`  
  
     Consultez hello [expressions scalaires](#bk_scalar_expressions) pour plus d’informations.  
  
-   `ASC | DESC`  
  
     Spécifie que les valeurs hello dans la colonne spécifiée de hello doivent être triées dans l’ordre croissant ou décroissant. ASC effectue le tri de hello la plus petite valeur toohighest. DESC effectue le tri de la plus grande valeur toolowest. ASC est l’ordre de tri par défaut hello. Les valeurs NULL sont traitées comme valeurs possibles de hello plus bas.  
  
 **Remarques**  
  
 Grammaire de requête hello prend en charge plusieurs ordre par les propriétés, exécution de requête de base de données Azure Cosmos hello prend en charge le tri uniquement par rapport à une seule propriété et uniquement sur les noms de propriété, autrement dit, pas sur les propriétés calculées. Tri requiert également que hello stratégie d’indexation inclut un index de plage pour la propriété de hello et hello spécifié type, avec une précision maximale de hello. Consultez toohello l’indexation de documentation pour plus d’informations sur les stratégies.  
  
##  <a name="bk_scalar_expressions"></a> Expressions scalaires  
 Une expression scalaire est une combinaison de symboles et opérateurs qui peuvent être évalués tooobtain une valeur unique. Les expressions simples peuvent être des constantes, des références de propriété, des références d’élément de tableau, des références d’alias ou des appels de fonction. Les expressions simples peuvent être combinées dans des expressions complexes utilisant des opérateurs.  
  
 Pour plus d’informations sur les valeurs qu’une expression scalaire peut avoir, consultez la section [constantes](#bk_constants).  
  
 **Syntaxe**  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 **Arguments**  
  
-   `<constant>`  
  
     Représente une valeur constante. Consultez la section [Constantes](#bk_constants) pour plus d’informations.  
  
-   `input_alias`  
  
     Représente une valeur définie par hello `input_alias` introduite dans hello `FROM` clause.  
    Cette valeur est garantie toonot être **non défini** –**non défini** les valeurs dans l’entrée de hello sont ignorées.  
  
-   `<scalar_expression>.property_name`  
  
     Représente une valeur de propriété hello d’un objet. Si hello propriété n’existe pas ou est référencée sur une valeur qui n’est pas un objet, puis hello expression évalue trop**non défini** valeur.  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     Représente une valeur de propriété hello portant le nom `property_name` ou élément de tableau avec l’index `array_index` d’un objet/tableau. Si l’index de tableau de la propriété hello n’existe pas ou les index de tableau de la propriété hello est référencée sur une valeur qui n’est pas un objet/tableau, l’expression de hello évalue tooundefined valeur.  
  
-   `unary_operator <scalar_expression>`  
  
     Représente un opérateur est appliqué tooa une seule valeur. Consultez la section [Opérateurs](#bk_operators) pour plus d’informations.  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     Représente un opérateur est appliqué tootwo valeurs. Consultez la section [Opérateurs](#bk_operators) pour plus d’informations.  
  
-   `<scalar_function_expression>`  
  
     Représente une valeur définie par le résultat d’un appel de fonction.  
  
-   `udf_scalar_function`  
  
     Fonction scalaire définie par le nom d’utilisateur de hello.  
  
-   `builtin_scalar_function`  
  
     Nom de fonction scalaire intégrée de hello.  
  
-   `<create_object_expression>`  
  
     Représente une valeur obtenue en créant un nouvel objet avec les propriétés spécifiées et leurs valeurs.  
  
-   `<create_array_expression>`  
  
     Représente une valeur obtenue en créant un nouveau tableau avec les valeurs spécifiées en tant qu’éléments  
  
-   `parameter_name`  
  
     Représente une valeur de nom de paramètre spécifié hello. Les noms de paramètres doivent avoir un seul @ comme premier caractère de hello.  
  
 **Remarques**  
  
 Lors de l’appel à une fonction scalaire intégrée ou définie par l’utilisateur, tous les arguments doivent être définis. Si un des arguments de hello n’est pas défini, fonction hello ne sera pas appelée et le résultat de hello n’est pas défini.  
  
 Lorsque vous créez un objet, n’importe quelle propriété de valeur indéfinie est ignorée et pas incluse dans hello créé l’objet.  
  
 Lorsque la création d’un tableau, toute valeur de l’élément qui est attribué **non défini** valeur sera ignorée et pas inclus dans l’objet de hello créé. Cela entraîne hello ensuite défini élément tootake la place de manière à ce tableau hello créé ne sera pas ont index ignoré.  
  
##  <a name="bk_operators"></a> Opérateurs  
 Cette section décrit les opérateurs hello pris en charge. Chaque opérateur peut être attribué tooexactly une catégorie.  
  
 Consultez le tableau **Catégories d’opérateurs** ci-dessous pour plus d’informations sur la gestion des valeurs **Undefined**, des exigences de type pour les valeurs d’entrée et la gestion des valeurs sans types correspondants.  
  
 **Catégories d’opérateurs :**  
  
|**Catégorie**|**Détails**|  
|-|-|  
|**Opérateurs arithmétiques**|L’opérateur attend que les entrées toobe numéro (s). La sortie est également un nombre. Si une des entrées de hello est **non défini** ou type de résultat de nombre, hello est **non défini**.|  
|**Opérateurs au niveau du bit**|L’opérateur attend que les entrées entier signé de 32 bits toobe numéro (s). La sortie est également un nombre entier signé 32 bits.<br /><br /> Toute valeur non entière est arrondie. Les valeurs positives sont arrondies vers le bas, et les valeurs négatives vers le haut.<br /><br /> Toute valeur qui est en dehors de la plage d’entiers 32 bits et hello sera converti, en prenant les derniers 32 bits de ses deux notation de complément.<br /><br /> Si une des entrées de hello est **non défini** ou de type autre qu’un nombre, il en résulte hello **non défini**.<br /><br /> **Remarque :** hello au-dessus de comportement est compatible avec le comportement de l’opérateur au niveau du bit JavaScript.|  
|**Opérateurs logiques**|L’opérateur attend que les entrées toobe des valeurs booléennes. La sortie est également une valeur booléenne.<br />Si une des entrées de hello est **non défini** ou autre qu’une valeur booléenne de type hello résultat sera **non défini**.|  
|**Opérateurs de comparaison**|L’opérateur attend que les entrées toohave hello même type et non définies. La sortie est une valeur booléenne.<br /><br /> Si une des entrées de hello est **non défini** ou entrées de hello ont des types différents, puis il en résulte hello **non défini**.<br /><br /> Consultez le tableau **Classement des valeurs pour comparaison** pour plus de détails sur le classement des valeurs.|  
|**string**|L’opérateur attend que les entrées toobe ou les chaînes. La sortie est également une chaîne.<br />Si une des entrées de hello est **non défini** ou type de résultat de chaîne puis hello est **non défini**.|  
  
 **Opérateurs unaires :**  
  
|**Name**|**Opérateur**|**Détails**|  
|-|-|-|  
|**Opérateurs arithmétiques**|+<br /><br /> -|Retourne la valeur nombre hello.<br /><br /> Négation au niveau du bit. Retourne une valeur numérique avec négation.|  
|**Opérateurs au niveau du bit**|~|Complément d’une valeur. Retourne un complément d’une valeur numérique.|  
|**Opérateurs logiques**|**NOT**|Négation. Retourne une valeur booléenne avec négation.|  
  
 **Opérateurs binaires :**  
  
|**Name**|**Opérateur**|**Détails**|  
|-|-|-|  
|**Opérateurs arithmétiques**|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|Addition.<br /><br /> Soustraction.<br /><br /> Multiplication.<br /><br /> Division.<br /><br /> Modulation.|  
|**Opérateurs au niveau du bit**|&#124;<br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|Opérateur OR au niveau du bit.<br /><br /> Opérateur AND au niveau du bit.<br /><br /> XOR au niveau du bit.<br /><br /> Décalage vers la gauche.<br /><br /> Décalage vers la droite.<br /><br /> Décalage vers la droite avec remplissage de zéros.|  
|**Opérateurs logiques**|**AND**<br /><br /> **OR**|Conjonction logique. Retourne **true** si les deux arguments sont **true**, retourne **false** dans le cas contraire.<br /><br /> Conjonction logique. Retourne **true** si les deux arguments sont **true**, retourne **false** dans le cas contraire.|  
|**Opérateurs de comparaison**|**=**<br /><br /> **!=, &lt;&gt;**<br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> **??**|Égal à. Retourne **true** si les arguments sont égaux, **false** dans le cas contraire.<br /><br /> Non égal à. Retourne **true** si les arguments ne sont pas égaux, **false** dans le cas contraire.<br /><br /> Supérieur à. Retourne **true** si le premier argument est supérieure à hello deuxième **false** dans le cas contraire.<br /><br /> Supérieur ou égal à. Retourne **true** si le premier argument est supérieur ou égal à un deuxième toohello, retourner **false** dans le cas contraire.<br /><br /> Inférieur à. Retourne **true** si le premier argument est inférieur au hello deuxième **false** dans le cas contraire.<br /><br /> Inférieur ou égal à. Retourne **true** si le premier argument est inférieur ou égal toohello seconde un retour **false** dans le cas contraire.<br /><br /> Coalesce. Retourne hello deuxième argument si hello premier argument est un **non défini** valeur.|  
|**Chaîne**|**&amp;#124;&amp;#124;**|Concaténation. Renvoie une concaténation de deux arguments.|  
  
 **Opérateurs ternaires :**  
  
|Opérateur ternaire|?|Retourne hello deuxième argument si le premier argument de hello évalue trop**true**; retourne le troisième argument de hello dans le cas contraire.|  
|-|-|-|  
  
 **Ordre des valeurs pour comparaison**  
  
|**Type**|**Ordre des valeurs**|  
|-|-|  
|**Undefined**|Non comparables.|  
|**Null**|Valeur unique : **null**|  
|**Nombre**|Nombre réel naturel.<br /><br /> La valeur d’infini négatif est inférieure à toute autre valeur numérique.<br /><br /> La valeur d’infini positif est supérieure à toute autre valeur numérique. La valeur **NaN** n’est pas comparable. La comparaison avec **NaN** entraîne une valeur **Undefined**.|  
|**Chaîne**|Ordre lexicographique.|  
|**Tableau**|Aucun ordre, mais équitable.|  
|**Object**|Aucun ordre, mais équitable.|  
  
 **Remarques**  
  
 Dans la base de données Azure Cosmos, types hello de valeurs sont souvent inconnus jusqu'à ce qu’ils soient effectivement récupérés à partir de la base de données hello. Dans l’ordre toosupport une exécution efficace des requêtes, la plupart des opérateurs de hello ont des exigences de type strict. De plus, les opérateurs n’effectuent pas de conversions implicites eux-mêmes.  
  
 Cela signifie qu’une requête, tels que : sélectionnez * FROM ROOT r WHERE r.Age = 21 retourne uniquement les documents dont la propriété nombre de toohello égal âge 21. Documents avec la propriété Age toohello égal chaîne « 21 » ou hello « 0021 » ne correspondent pas, comme l’expression hello « 21 » = 21 produit une valeur tooundefined. Cela permet une meilleure utilisation des index, car recherche hello d’une valeur spécifique (c'est-à-dire le numéro 21) est plus rapide que la recherche d’un nombre indéfini de correspondances potentielles (nombre 21 ou chaînes « 21 », « 021 », « 21.0 »...). Cela est différent de la manière dont JavaScript évalue les opérateurs sur les valeurs de types différents.  
  
 **Comparaison et égalité pour les objets et tableaux**  
  
 La comparaison des valeurs de tableau ou d’objet à l’aide des opérateurs de plage (>, > =, <, < =) entraînera un résultat Undefined, car il n’existe pas d’ordre défini sur les valeurs d’objet ou de tableau. Toutefois, l’utilisation d’opérateurs d’égalité/inégalité (=, ! =, <>) est prise en charge et les valeurs seront comparées structurellement.  
  
 Les tableaux sont égaux si les deux tableaux ont le même nombre d’éléments et que les éléments aux positions correspondantes sont également égaux. Si la comparaison d’une paire d’éléments entraîne des résultats hello non défini, de comparaison de tableau est indéfini.  
  
 Les objets sont égaux si les deux objets ont les mêmes propriétés définies, et si les valeurs des propriétés correspondantes sont également égales. Si la comparaison d’une paire de valeurs de propriété entraîne des résultats hello non défini, de comparaison de l’objet est indéfini.  
  
##  <a name="bk_constants"></a> Constantes  
 Une constante, également appelée un littéral ou une valeur scalaire, est un symbole représentant une valeur de données spécifique. format Hello d’une constante varie selon le type de données hello de valeur hello qu’il représente.  
  
 **Prise en charge des types de données scalaires :**  
  
|**Type**|**Ordre des valeurs**|  
|-|-|  
|**Undefined**|Valeur unique : **Undefined**|  
|**Null**|Valeur unique : **null**|  
|**Booléen**|Valeurs : **false**, **true**.|  
|**Nombre**|Un nombre à virgule flottante double précision répondant à la norme IEEE 754.|  
|**Chaîne**|Une séquence de zéro ou plusieurs caractères Unicode. Les chaînes doivent figurer entre guillemets simples ou doubles.|  
|**Tableau**|Une séquence de zéro ou plusieurs éléments. Chaque élément peut être une valeur de tout type de données scalaires, à l’exception de Undefined.|  
|**Object**|Un jeu non ordonné de zéro ou plusieurs paires nom/valeur. Le nom est une chaîne Unicode, la valeur peut être de n’importe quel type de données scalaire, sauf **Undefined**.|  
  
 **Syntaxe**  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 **Arguments**  
  
1.  `<undefined_constant>; undefined`  
  
     Représente la valeur undefined du type Undefined.  
  
2.  `<null_constant>; null`  
  
     Représente la valeur **null** du type **Null**.  
  
3.  `<boolean_constant>`  
  
     Représente une constante de type booléen.  
  
4.  `false`  
  
     Représente une valeur **false** de type booléen.  
  
5.  `true`  
  
     Représente une valeur **true** de type booléen.  
  
6.  `<number_constant>`  
  
     Représente une constante.  
  
7.  `decimal_literal`  
  
     Les littéraux décimaux sont représentés à l’aide de la notation décimale, ou de la notation scientifique.  
  
8.  `hexadecimal_literal`  
  
     Les littéraux hexadécimaux sont représentés à l’aide du préfixe « 0 x », suivi d’un ou plusieurs chiffres hexadécimaux.  
  
9. `<string_constant>`  
  
     Représente une constante de type chaîne.  
  
10. `string _literal`  
  
     Les littéraux de chaîne sont des chaînes Unicode représentées par une séquence de zéro ou plusieurs caractères Unicode ou séquences d’échappement. Les littéraux de chaîne sont placés entre guillemets simples (apostrophes, ’) ou guillemets doubles (").  
  
 Les séquences d’échappement suivantes sont autorisées :  
  
|**Séquence d’échappement**|**Description**|**Caractères Unicode**|  
|-|-|-|  
|\\'|apostrophe (')|U+0027|  
|\\"|guillemet (")|U+0022|  
|\\\|barre oblique inversée (\\)|U+005C|  
|\\/|barre oblique (/)|U+002F|  
|\b|retour arrière|U+0008|  
|\f|saut de page|U+000C|  
|\n|saut de ligne|U+000A|  
|\r|retour chariot|U+000D|  
|\t|tab|U+0009|  
|\uXXXX|Un caractère Unicode défini par 4 chiffres hexadécimaux.|U+XXXX|  
  
##  <a name="bk_query_perf_guidelines"></a> Instructions relatives aux performances de requête  
 Dans l’ordre pour un toobe de requête exécutée efficacement pour une grande collection, elle doit utiliser des filtres qui peuvent être servis via un ou plusieurs index.  
  
 Hello, suivant les filtres est considéré comme pour la recherche d’index :  
  
-   Utilisez l’opérateur d’égalité (=) avec une expression de chemin d’accès de document et une constante.  
  
-   Utilisez les opérateurs de plage (<, \<=, >, > =) avec une expression de chemin d’accès de document et des constantes numériques.  
  
-   Expression de chemin d’accès de document remplace toute expression qui identifie un chemin d’accès constant dans les documents hello à partir de la collection de base de données hello référencé.  
  
 **Expression de chemin d’accès à un document**  
  
 Les expressions de chemin d’accès à un document sont des expressions qu’un chemin d’accès de propriété ou indexeur de tableau évalue sur un document provenant des documents de la collecte de base de données. Ce chemin d’accès peut être emplacement de hello tooidentify utilisées de valeurs référencées dans un filtre directement dans des documents dans la collection de base de données hello hello.  
  
 Pour une expression toobe considérée comme une expression de chemin d’accès de document, il doit :  
  
1.  Référence hello racine de la collection directement.  
  
2.  Référencer la propriété ou l’indexeur de tableau de constantes d’une expression de chemin d’accès de document  
  
3.  Faire référence à un alias, qui représente une expression de chemin d’accès de document.  
  
     **Conventions de syntaxe**  
  
     Hello tableau suivant décrit la syntaxe de toodescribe hello conventions utilisées dans la référence du langage de requête API DocumentDB hello.  
  
    |**Convention**|**Utilisé pour**|  
    |-|-|    
    |MAJUSCULES|Mots-clés non sensibles à la casse.|  
    |minuscules|Mots-clés sensibles à la casse.|  
    |\<nonterminal&gt;|Non terminal, défini séparément.|  
    |\<nonterminal&gt; ::=|Définition de la syntaxe de l’élément non terminal hello.|  
    |other_terminal|Terminal (jeton), décrit en détail par des mots.|  
    |identificateur|Identificateur. Autorise uniquement les caractères suivants : a-z A-Z 0-9 _ Le premier caractère ne peut pas être un chiffre.|  
    |"chaîne"|Chaîne entre guillemets. Autorise n’importe quelle chaîne valide. Consultez la description de string_literal.|  
    |'symbole'|Symbole littéral qui fait partie de la syntaxe de hello.|  
    |&#124; (barre verticale)|Alternatives aux éléments de syntaxe. Vous pouvez utiliser uniquement un des éléments de hello spécifiés.|  
    |[ ] /(crochets)|Les crochets entourent un ou plusieurs éléments facultatifs.|  
    |[ ,...n ]|Indique hello précédant l’élément peut être répété n fois. occurrences de Hello sont séparées par des virgules.|  
    |[ ...n ]|Indique hello précédant l’élément peut être répété n fois. occurrences de Hello sont séparées par des espaces.|  
  
##  <a name="bk_built_in_functions"></a> Fonctions intégrées  
 Azure Cosmos DB fournit de nombreuses fonctions SQL intégrées. catégories de Hello de fonctions intégrées sont répertoriées ci-dessous.  
  
|Fonction|Description|  
|--------------|-----------------|  
|[Fonctions mathématiques](#bk_mathematical_functions)|fonctions mathématiques Hello chaque effectuent un calcul, généralement basé sur des valeurs d’entrée qui sont fournies en tant qu’arguments et retournent une valeur numérique.|  
|[Fonctions de vérification du type](#bk_type_checking_functions)|les fonctions de vérification de type Hello vous autorisent toocheck hello ce type d’une expression dans des requêtes SQL.|  
|[Fonctions de chaîne](#bk_string_functions)|fonctions de chaîne Hello effectuent une opération sur une valeur de chaîne d’entrée et retournent une valeur numérique ou booléenne, une chaîne.|  
|[Fonctions de tableau](#bk_array_functions)|fonctions de tableau Hello effectuent une opération sur une valeur d’entrée de tableau et de retour numérique, une valeur booléenne ou de tableau.|  
|[Fonctions spatiales](#bk_spatial_functions)|les fonctions spatiales Hello effectuent une opération sur une valeur d’entrée d’objet spatial et retournent une valeur numérique ou booléenne.|  
  
###  <a name="bk_mathematical_functions"></a> Fonctions mathématiques  
 Hello fonctions mathématiques suivantes effectuent un calcul, généralement basé sur des valeurs d’entrée qui sont fournies en tant qu’arguments et retournent une valeur numérique.  
  
||||  
|-|-|-|  
|[ABS](#bk_abs)|[ACOS](#bk_acos)|[ASIN](#bk_asin)|  
|[ATAN](#bk_atan)|[ATN2](#bk_atn2)|[CEILING](#bk_ceiling)|  
|[COS](#bk_cos)|[COT](#bk_cot)|[DEGREES](#bk_degrees)|  
|[EXP](#bk_exp)|[FLOOR](#bk_floor)|[LOG](#bk_log)|  
|[LOG10](#bk_log10)|[PI](#bk_pi)|[POWER](#bk_power)|  
|[RADIANS](#bk_radians)|[ROUND](#bk_round)|[SIN](#bk_sin)|  
|[SQRT](#bk_sqrt)|[SQUARE](#bk_square)|[SIGN](#bk_sign)|  
|[TAN](#bk_tan)|[TRUNC](#bk_trunc)||  
  
####  <a name="bk_abs"></a> ABS  
 Retourne hello valeur absolue (positive) de hello de l’expression numérique spécifiée.  
  
 **Syntaxe**  
  
```  
ABS (<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello suivant montre les résultats de hello de l’utilisation de la fonction hello ABS sur trois nombres différents.  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a> ACOS  
 Angle de hello retourne, en radians, dont le cosinus est hello expression numérique spécifiée ; également appelé arc cosinus.  
  
 **Syntaxe**  
  
```  
ACOS(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple ci-dessous retourne hello ACOS de -1.  
  
```  
SELECT ACOS(-1)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a> ASIN  
 Angle de hello retourne, en radians, dont le sinus est hello spécifié expression numérique. Cette fonction est également appelée arcsinus.  
  
 **Syntaxe**  
  
```  
ASIN(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple ci-dessous retourne hello ASIN de -1.  
  
```  
SELECT ASIN(-1)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a> ATAN  
 Angle de hello retourne, en radians, dont la tangente est hello spécifié expression numérique. Cette fonction est également appelée arctangente.  
  
 **Syntaxe**  
  
```  
ATAN(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple retourne hello ATAN de hello suivant la valeur spécifiée.  
  
```  
SELECT ATAN(-45.01)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a> ATN2  
 Retourne la valeur principal hello hello arc tangente de y / x, exprimée en radians.  
  
 **Syntaxe**  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 exemple Hello calcule hello ATN2 pour hello spécifié x et y des composants.  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a> CEILING  
 Retourne hello plus petit entier supérieur à, ou être égal, hello expression numérique spécifiée.  
  
 **Syntaxe**  
  
```  
CEILING (<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello l’exemple suivant montre numériques positives, négatives, et les valeurs zéro avec hello fonction CEILING.  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a> COS  
 Cosinus trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée.  
  
 **Syntaxe**  
  
```  
COS(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant calcule hello COS de hello spécifié angle.  
  
```  
SELECT COS(14.78)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a> COT  
 Cotangente trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression numérique spécifiée.  
  
 **Syntaxe**  
  
```  
COT(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant calcule hello COT de l’angle spécifié de hello.  
  
```  
SELECT COT(124.1332)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a> DEGREES  
 Retourne hello angle correspondant en degrés pour un angle spécifié en radians.  
  
 **Syntaxe**  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple suivant retourne hello nombre de degrés d’un angle de PI/2 radians.  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a> FLOOR  
 Retourne des hello plus grand entier inférieur ou égal toohello l’expression numérique spécifiée.  
  
 **Syntaxe**  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello, l’exemple suivant montre numériques positives, négatives, et les valeurs zéro avec hello FLOOR (fonction).  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a> EXP  
 Hello retourne la valeur exponentielle de hello de l’expression numérique spécifiée.  
  
 **Syntaxe**  
  
```  
EXP (<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Remarques**  
  
 constante de Hello **e** (2,718281...), est hello base des logarithmes naturels.  
  
 constante de hello est Hello exposant d’un nombre **e** déclenché toohello puissance hello. Par exemple EXP(1.0) = e ^ 1,0 = 2,71828182845905 et EXP(10) = e ^ 10 = 22026,4657948067.  
  
 Hello valeur exponentielle du logarithme naturel de hello d’un nombre est le nombre hello lui-même : EXP (LOG (n)) = n. Et hello logarithme népérien de hello exponentielle d’un nombre est nombre hello lui-même : EXP (LOG (n)) = n.  
  
 **Exemples**  
  
 Hello exemple suivant déclare une variable et renvoie la valeur exponentielle de hello de hello (10).  
  
```  
SELECT EXP(10)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 Hello exemple suivant renvoie hello valeur exponentielle du logarithme naturel de hello de 20 et le logarithme népérien de hello Hello exponentielle de 20. Étant donné que ces fonctions sont l’inverse d’une autre, hello valeur renvoyée pour les opérations mathématiques dans les deux cas est de 20 de virgule flottante.  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a> LOG  
 Népérien retourne hello Hello de l’expression numérique spécifiée.  
  
 **Syntaxe**  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
-   `base`  
  
     Argument numérique facultatif qui définit hello base logarithme de hello.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Remarques**  
  
 Par défaut, LOG() renvoie le logarithme népérien de hello. Vous pouvez modifier la base hello de valeur de hello logarithme tooanother à l’aide du paramètre de base facultatif hello.  
  
 Logarithme népérien de Hello est hello toohello de logarithme base **e**, où **e** est un too2.718281828 approximativement égale constante irrationnelle.  
  
 Logarithme népérien de Hello Hello exponentielle d’un nombre est nombre hello lui-même : EXP (LOG (n)) = n. Et hello valeur exponentielle du logarithme naturel de hello d’un nombre est le nombre hello lui-même : EXP (LOG (n)) = n.  
  
 **Exemples**  
  
 Hello exemple suivant déclare une variable et retourne la valeur du logarithme hello de hello (10).  
  
```  
SELECT LOG(10)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 Hello exemple suivant calcule hello journal exposant hello d’un nombre.  
  
```  
SELECT EXP(LOG(10))  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a> LOG10  
 Logarithme de base 10 retourne hello Hello spécifié expression numérique.  
  
 **Syntaxe**  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Remarques**  
  
 Hello LOG10 et fonctions de puissance sont inversement connexe tooone une autre. Par exemple, 10 ^ LOG10 (n) = n.  
  
 **Exemples**  
  
 Hello exemple suivant déclare une variable et renvoie la valeur LOG10 de hello de variable spécifié de hello (100).  
  
```  
SELECT LOG10(100)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a> PI  
 Retourne hello valeur constante de PI.  
  
 **Syntaxe**  
  
```  
PI ()  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello suivant l’exemple hello retourne la valeur de PI.  
  
```  
SELECT PI()  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a> POWER  
 Retourne hello valeur Hello spécifié expression toohello de puissance spécifiée.  
  
 **Syntaxe**  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
-   `y`  
  
     Est hello power toowhich tooraise `numeric_expression`.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant montre le déclenchement d’une nombre toohello puissance 3 (cube hello du nombre de hello).  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a> RADIANS  
 Retourne des radians lorsqu’une expression numérique, en degrés, est entrée.  
  
 **Syntaxe**  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple suivant utilise plusieurs angles comme entrée et retourne leurs valeurs en radians correspondant.  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a> ROUND  
 Retourne une valeur numérique, arrondie toohello nombre entier le plus proche.  
  
 **Syntaxe**  
  
```  
ROUND(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple suivant arrondit hello suivant toohello de nombres positifs et négatifs entière la plus proche.  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a> SIGN  
 Retourne hello positif (+ 1), zéro (0), ou un signe négatif (-1) de hello de l’expression numérique spécifiée.  
  
 **Syntaxe**  
  
```  
SIGN(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple suivant retourne les valeurs hello signe des nombres de-2 too2.  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a> SIN  
 Sinus trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée.  
  
 **Syntaxe**  
  
```  
SIN(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant calcule hello SIN de l’angle spécifié de hello.  
  
```  
SELECT SIN(45.175643)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a> SQRT  
 Racine carrée retourne hello hello la valeur numérique spécifiée.  
  
 **Syntaxe**  
  
```  
SQRT(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple ci-dessous retourne racines carrées de hello de 1 à 3.  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a> SQUARE  
 Hello retourne carrée hello la valeur numérique spécifiée.  
  
 **Syntaxe**  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple suivant renvoie les carrés hello de 1 à 3.  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a> TAN  
 Tangente de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée.  
  
 **Syntaxe**  
  
```  
TAN (<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple suivant calcule la tangente de PI () hello / 2.  
  
```  
SELECT TAN(PI()/2);  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a> TRUNC  
 Retourne une valeur numérique, tronquée toohello nombre entier le plus proche.  
  
 **Syntaxe**  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 **Arguments**  
  
-   `numeric_expression`  
  
     Est une expression numérique.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant tronque hello suivant toohello de nombres positifs et négatifs plus proche de la valeur entière.  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a> Fonctions de vérification du type  
 Hello fonctions suivantes prennent en charge de vérification par rapport aux valeurs d’entrée de type, et renvoient une valeur booléenne.  
  
||||  
|-|-|-|  
|[IS_ARRAY](#bk_is_array)|[IS_BOOL](#bk_is_bool)|[IS_DEFINED](#bk_is_defined)|  
|[IS_NULL](#bk_is_null)|[IS_NUMBER](#bk_is_number)|[IS_OBJECT](#bk_is_object)|  
|[IS_PRIMITIVE](#bk_is_primitive)|[IS_STRING](#bk_is_string)||  
  
####  <a name="bk_is_array"></a> IS_ARRAY  
 Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un tableau.  
  
 **Syntaxe**  
  
```  
IS_ARRAY(<expression>)  
```  
  
 **Arguments**  
  
-   `expression`  
  
     Peut être toute expression valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_ARRAY de hello.  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a> IS_BOOL  
 Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est une valeur booléenne.  
  
 **Syntaxe**  
  
```  
IS_BOOL(<expression>)  
```  
  
 **Arguments**  
  
-   `expression`  
  
     Peut être toute expression valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_BOOL de hello.  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a> IS_DEFINED  
 Retourne une valeur booléenne indiquant si une valeur a été assignée à la propriété de hello.  
  
 **Syntaxe**  
  
```  
IS_DEFINED(<expression>)  
```  
  
 **Arguments**  
  
-   `expression`  
  
     Peut être toute expression valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello contrôles exemple présence hello d’une propriété dans hello spécifié document JSON. tout d’abord Hello retourne true, car « a » est présent, mais hello deuxième retourne la valeur false, car « b » est absent.  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a> IS_NULL  
 Retourne une valeur booléenne indiquant si le type hello Hello spécifié expression est null.  
  
 **Syntaxe**  
  
```  
IS_NULL(<expression>)  
```  
  
 **Arguments**  
  
-   `expression`  
  
     Peut être toute expression valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_NULL de hello.  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a> IS_NUMBER  
 Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un nombre.  
  
 **Syntaxe**  
  
```  
IS_NUMBER(<expression>)  
```  
  
 **Arguments**  
  
-   `expression`  
  
     Peut être toute expression valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_NULL de hello.  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a> IS_OBJECT  
 Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un objet JSON.  
  
 **Syntaxe**  
  
```  
IS_OBJECT(<expression>)  
```  
  
 **Arguments**  
  
-   `expression`  
  
     Peut être toute expression valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_OBJECT de hello.  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a> IS_PRIMITIVE  
 Retourne une valeur booléenne indiquant si le type hello Hello spécifié expression est un type primitif (chaîne, booléen, numérique ou null).  
  
 **Syntaxe**  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 **Arguments**  
  
-   `expression`  
  
     Peut être toute expression valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_PRIMITIVE de hello.  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a> IS_STRING  
 Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est une chaîne.  
  
 **Syntaxe**  
  
```  
IS_STRING(<expression>)  
```  
  
 **Arguments**  
  
-   `expression`  
  
     Peut être toute expression valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_STRING de hello.  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a> Fonctions de chaîne  
 Bonjour fonctions scalaires suivantes effectuent une opération sur une valeur de chaîne d’entrée et retournent une valeur numérique ou booléenne, une chaîne.  
  
||||  
|-|-|-|  
|[CONCAT](#bk_concat)|[CONTAINS](#bk_contains)|[ENDSWITH](#bk_endswith)|  
|[INDEX_OF](#bk_index_of)|[LEFT](#bk_left)|[LENGTH](#bk_length)|  
|[LOWER](#bk_lower)|[LTRIM](#bk_ltrim)|[REPLACE](#bk_replace)|  
|[REPLICATE](#bk_replicate)|[REVERSE](#bk_reverse)|[RIGHT](#bk_right)|  
|[RTRIM](#bk_rtrim)|[STARTSWITH](#bk_startswith)|[SUBSTRING](#bk_substring)|  
|[UPPER](#bk_upper)|||  
  
####  <a name="bk_concat"></a> CONCAT  
 Retourne une chaîne qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de chaîne.  
  
 **Syntaxe**  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Hello suivant l’exemple retourne la chaîne hello concaténé de hello les valeurs spécifiées.  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a> CONTAINS  
 Retourne une valeur booléenne qui indique si le première expression de chaîne hello contient hello ensuite.  
  
 **Syntaxe**  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple suivant vérifie si « abc » contient « ab » contient « d ».  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a> ENDSWITH  
 Retourne une valeur booléenne indiquant si les première expression de chaîne hello se termine ensuite par hello.  
  
 **Syntaxe**  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple ci-dessous retourne hello « abc » se termine par « b » et « bc ».  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a> INDEX_OF  
 Retourne hello position de départ des hello première occurrence de hello deuxième expression de chaîne hello première expression de chaîne spécifiée, ou -1 si la chaîne de hello est introuvable.  
  
 **Syntaxe**  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Hello exemple suivant retourne les index hello de différentes sous-chaînes à l’intérieur de « abc ».  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a> LEFT  
 Retourne hello partie gauche d’une chaîne avec hello spécifié de caractères.  
  
 **Syntaxe**  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
-   `num_expr`  
  
     Est une expression numérique valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Hello exemple ci-dessous retourne hello gauche de « abc » pour différentes valeurs de longueur.  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a> LENGTH  
 Retourne hello nombre de caractères de hello spécifié l’expression de chaîne.  
  
 **Syntaxe**  
  
```  
LENGTH(<str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Hello exemple suivant retourne la longueur d’une chaîne hello.  
  
```  
SELECT LENGTH("abc")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a> LOWER  
 Retourne une expression de chaîne après la conversion de toolowercase de données de caractères majuscules en caractères.  
  
 **Syntaxe**  
  
```  
LOWER(<str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Hello suivant montre l’exemple de comment toouse inférieur dans une requête.  
  
```  
SELECT LOWER("Abc")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a> LTRIM  
 Retourne une expression de chaîne après avoir supprimé les espaces de début.  
  
 **Syntaxe**  
  
```  
LTRIM(<str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Hello suivant montre l’exemple de comment toouse LTRIM à l’intérieur d’une requête.  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a> REPLACE  
 Remplace toutes les occurrences d’une valeur de chaîne spécifiée par une autre valeur de chaîne.  
  
 **Syntaxe**  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant montre comment remplacer des toouse dans une requête.  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a> REPLICATE  
 Répète une valeur de chaîne un nombre de fois spécifié.  
  
 **Syntaxe**  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
-   `num_expr`  
  
     Est une expression numérique valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant montre comment répliquer des toouse dans une requête.  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a> REVERSE  
 Retourne l’ordre inverse d’une valeur de chaîne hello.  
  
 **Syntaxe**  
  
```  
REVERSE(<str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant montre comment toouse inverse dans une requête.  
  
```  
SELECT REVERSE("Abc")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a> RIGHT  
 Hello retourne à droite dans le cadre d’une chaîne avec hello nombre spécifié de caractères.  
  
 **Syntaxe**  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
-   `num_expr`  
  
     Est une expression numérique valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Hello exemple suivant retourne hello de partie droite de « abc » pour différentes valeurs de longueur.  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a> RTRIM  
 Retourne une expression de chaîne après avoir supprimé les espaces de fin.  
  
 **Syntaxe**  
  
```  
RTRIM(<str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Hello suivant montre l’exemple de comment toouse RTRIM à l’intérieur d’une requête.  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a> STARTSWITH  
 Retourne une valeur booléenne indiquant si les première expression de chaîne hello commence par hello ensuite.  
  
 **Syntaxe**  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello exemple suivant vérifie si hello de chaîne « abc » commence par « b » et « a ».  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a> SUBSTRING  
 Retourne dans une expression de chaîne commençant à hello spécifié le caractère de base zéro et continue toohello spécifié longueur, ou à la fin de toohello de chaîne de hello.  
  
 **Syntaxe**  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
-   `num_expr`  
  
     Est une expression numérique valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Hello exemple suivant retourne hello sous-chaîne de « abc » commençant à 1 pour une longueur de 1 caractère.  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "b"}]  
```  
  
####  <a name="bk_upper"></a> UPPER  
 Retourne une expression de chaîne après la conversion de toouppercase de données de caractères en minuscules.  
  
 **Syntaxe**  
  
```  
UPPER(<str_expr>)  
```  
  
 **Arguments**  
  
-   `str_expr`  
  
     Peut être toute expression de chaîne valide.  
  
 **Types de retour**  
  
 Retourne une expression de chaîne.  
  
 **Exemples**  
  
 Hello suivant montre l’exemple de comment toouse supérieur dans une requête  
  
```  
SELECT UPPER("Abc")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a> Fonctions de tableau  
 Hello suivant des fonctions scalaires effectuent une opération sur une valeur d’entrée de tableau et le retour numérique, la valeur booléenne ou de tableau  
  
||||  
|-|-|-|  
|[ARRAY_CONCAT](#bk_array_concat)|[ARRAY_CONTAINS](#bk_array_contains)|[ARRAY_LENGTH](#bk_array_length)|  
|[ARRAY_SLICE](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a> ARRAY_CONCAT  
 Retourne un tableau qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de tableau.  
  
 **Syntaxe**  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 **Arguments**  
  
-   `arr_expr`  
  
     Peut être toute expression de tableau valide.  
  
 **Types de retour**  
  
 Retourne une expression de tableau.  
  
 **Exemples**  
  
 Bonjour selon exemple comment tooconcatenate deux tableaux.  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a> ARRAY_CONTAINS  
 Retourne une valeur booléenne qui indique si le tableau de hello contient hello valeur spécifiée.  
  
 **Syntaxe**  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 **Arguments**  
  
-   `arr_expr`  
  
     Peut être toute expression de tableau valide.  
  
-   `expr`  
  
     Peut être toute expression valide.  
  
 **Types de retour**  
  
 Retourne une valeur booléenne.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant comment toocheck l’appartenance dans un tableau à l’aide de ARRAY_CONTAINS.  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_array_length"></a> ARRAY_LENGTH  
 Nombre de hello retourne des éléments de hello spécifié expression de tableau.  
  
 **Syntaxe**  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 **Arguments**  
  
-   `arr_expr`  
  
     Peut être toute expression de tableau valide.  
  
 **Types de retour**  
  
 Renvoie une expression numérique.  
  
 **Exemples**  
  
 Bonjour selon exemple comment tooget hello longueur d’un tableau à l’aide de ARRAY_LENGTH.  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a> ARRAY_SLICE  
 Retourne une partie d’une expression de tableau.
  
 **Syntaxe**  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Arguments**  
  
-   `arr_expr`  
  
     Peut être toute expression de tableau valide.  
  
-   `num_expr`  
  
     Est une expression numérique valide.  
  
 **Types de retour**  
  
 Retourne une valeur booléenne.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant comment tooget une partie d’un tableau à l’aide de ARRAY_SLICE.  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a> Fonctions spatiales  
 Bonjour fonctions scalaires suivantes effectuent une opération sur une valeur d’entrée d’objet spatial et retournent une valeur numérique ou booléenne.  
  
||||  
|-|-|-|  
|[ST_DISTANCE](#bk_st_distance)|[ST_WITHIN](#bk_st_within)|[ST_INTERSECTS](#bk_st_intersects)|[ST_ISVALID](#bk_st_isvalid)|  
|[ST_ISVALIDDETAILED](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a> ST_DISTANCE  
 Retourne la distance hello entre les expressions LineString, Polygon ou GeoJSON Point hello deux.  
  
 **Syntaxe**  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 **Arguments**  
  
-   `spatial_expr`  
  
     Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.  
  
 **Types de retour**  
  
 Retourne une expression numérique qui contient la distance hello. Elle est exprimée en mètres pour le système de référence par défaut hello.  
  
 **Exemples**  
  
 Hello suivant montre l’exemple de comment tooreturn tous les documents familles 30 km de hello l’emplacement à l’aide de la fonction intégrée de hello ST_DISTANCE spécifié. .  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a> ST_WITHIN  
 Retourne une expression booléenne indiquant si hello GeoJSON l’objet (Point, polygone ou LineString) spécifié dans le premier argument de hello est dans hello GeoJSON (Point, polygone ou LineString) dans le deuxième argument de hello.  
  
 **Syntaxe**  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 **Arguments**  
  
-   `spatial_expr`  
  
     Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.  
 
-   `spatial_expr`  
  
     Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.  
  
 **Types de retour**  
  
 Retourne une valeur booléenne.  
  
 **Exemples**  
  
 Bonjour à l’exemple suivant montre comment toofind famille tous les documents d’un polygone à l’aide de ST_WITHIN.  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a> ST_INTERSECTS  
 Retourne une expression booléenne indiquant si hello GeoJSON l’objet (Point, polygone ou LineString) spécifié dans le premier argument de hello croise hello GeoJSON (Point, polygone ou LineString) dans le deuxième argument de hello.  
  
 **Syntaxe**  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 **Arguments**  
  
-   `spatial_expr`  
  
     Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.  
 
-   `spatial_expr`  
  
     Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.  
  
 **Types de retour**  
  
 Retourne une valeur booléenne.  
  
 **Exemples**  
  
 Hello suivant montre l’exemple de comment toofind toutes les zones croise hello donné polygone.  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a> ST_ISVALID  
 Retourne une valeur booléenne indiquant si hello spécifiée expression LineString, Polygon ou GeoJSON Point n’est valide.  
  
 **Syntaxe**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Arguments**  
  
-   `spatial_expr`  
  
     Est toute expression GeoJSON Point, Polygon ou LineString valide.  
  
 **Types de retour**  
  
 Retourne une expression booléenne.  
  
 **Exemples**  
  
 Hello suivant montre l’exemple de comment toocheck si un point est valide à l’aide de ST_VALID.  
  
 Par exemple, ce point a une valeur de latitude qui n’est pas hello plage de valeurs valide [-90, 90], donc hello requête retourne false.  
  
 Pour les polygones, hello GeoJSON spécification requiert que hello dernière paire de coordonnées fourni doit être hello même comme hello les toocreate tout d’abord, une forme fermée. Les points dans un polygone doivent être spécifiés dans le sens antihoraire. Un polygone spécifié dans le sens horaire représente inverse hello de région de hello qu’il contient.  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED  
 Retourne une valeur JSON contenant une valeur booléenne si hello de l’expression LineString, Polygon ou GeoJSON Point spécifiée est valide et si elle est non valide, en outre hello motif en tant que valeur de chaîne.  
  
 **Syntaxe**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Arguments**  
  
-   `spatial_expr`  
  
     Peut être toute expression GeoJSON Point ou Polygon valide.  
  
 **Types de retour**  
  
 Retourne une valeur JSON contenant une valeur booléenne si hello spécifié GeoJSON point ou expression de polygone est valide et si elle est non valide, en outre hello motif en tant que valeur de chaîne.  
  
 **Exemples**  
  
 Hello, l’exemple suivant la validité toocheck (avec les détails) à l’aide de ST_ISVALIDDETAILED.  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 Voici le jeu de résultats hello.  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a>Étapes suivantes  
 [Syntaxe SQL et requête SQL pour Azure Cosmos DB](documentdb-sql-query.md)   
 [Documentation Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
