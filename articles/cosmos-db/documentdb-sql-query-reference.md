---
<span data-ttu-id="43293-101">titre : aaa « API de DocumentDB de base de données Azure Cosmos : syntaxe SQL | Description de Microsoft Docs » : consultez la documentation pour hello langage de requête Azure Cosmos API DB DocumentDB SQL.</span><span class="sxs-lookup"><span data-stu-id="43293-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="43293-102">Services : cosmos-db auteur : Gestionnaire de mimig1 : jhubbard éditeur : mimig documentationcenter : ».</span><span class="sxs-lookup"><span data-stu-id="43293-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="43293-103">MS.AssetId : ms.service : cosmos-db ms.workload : services de données ms.tgt_pltfrm : na ms.devlang : na ms.topic : référence ms.date : 06/13/2017 ms.author : mimig</span><span class="sxs-lookup"><span data-stu-id="43293-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="43293-104">API DocumentDB Azure Cosmos DB : référence de syntaxe SQL</span><span class="sxs-lookup"><span data-stu-id="43293-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="43293-105">Hello Azure Cosmos DB DocumentDB API prend en charge des documents interrogation à l’aide d’un familière de type SQL (Structured Query Language) grammaire sur des documents JSON hiérarchiques sans schéma explicite ou la création d’index secondaires.</span><span class="sxs-lookup"><span data-stu-id="43293-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="43293-106">Cette rubrique fournit la documentation de référence pour hello langage de requête SQL d’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="43293-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="43293-107">Pour une procédure pas à pas de hello langage de requête DocumentDB API SQL, consultez [requêtes SQL pour l’API Azure Cosmos DB DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="43293-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="43293-108">Nous vous invitons également toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) où vous pouvez essayer de base de données Azure Cosmos et exécuter des requêtes SQL sur notre jeu de données.</span><span class="sxs-lookup"><span data-stu-id="43293-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="43293-109">Requête SELECT</span><span class="sxs-lookup"><span data-stu-id="43293-109">SELECT query</span></span>  
<span data-ttu-id="43293-110">Récupère les documents JSON à partir de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="43293-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="43293-111">Prend en charge d’évaluation d’expressions, les projections, le filtrage et les jointures.</span><span class="sxs-lookup"><span data-stu-id="43293-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="43293-112">les conventions de Hello utilisées pour décrire les instructions SELECT hello sont sous forme de tableau dans la section conventions de syntaxe de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="43293-113">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="43293-114">**Notes**</span><span class="sxs-lookup"><span data-stu-id="43293-114">**Remarks**</span></span>  
  
 <span data-ttu-id="43293-115">Pour plus d’informations sur chaque clause, consultez les sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="43293-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="43293-116">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="43293-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="43293-117">Clause FROM</span><span class="sxs-lookup"><span data-stu-id="43293-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="43293-118">Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="43293-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="43293-119">Clause ORDER BY</span><span class="sxs-lookup"><span data-stu-id="43293-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="43293-120">clauses Hello dans l’instruction SELECT de hello doivent être classés comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="43293-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="43293-121">L’une des clauses facultatives de hello peut être omise.</span><span class="sxs-lookup"><span data-stu-id="43293-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="43293-122">Mais lorsque clauses facultatives sont utilisées, elles doivent apparaître dans le bon ordre de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="43293-123">**Ordre logique de traitement de l’instruction SELECT de hello**</span><span class="sxs-lookup"><span data-stu-id="43293-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="43293-124">commande Hello dans lequel les clauses sont traités est la suivante :</span><span class="sxs-lookup"><span data-stu-id="43293-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="43293-125">Clause FROM</span><span class="sxs-lookup"><span data-stu-id="43293-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="43293-126">Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="43293-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="43293-127">Clause ORDER BY</span><span class="sxs-lookup"><span data-stu-id="43293-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="43293-128">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="43293-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="43293-129">Notez que cela est différent de hello dans lequel ils apparaissent dans la syntaxe de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="43293-130">classement de Hello est telle que tous les nouveaux symboles introduits par une clause traitée sont visibles et peuvent être utilisés dans des clauses traitées ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="43293-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="43293-131">Par exemple, les alias déclarés dans une clause FROM sont accessibles dans les clauses WHERE et SELECT.</span><span class="sxs-lookup"><span data-stu-id="43293-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="43293-132">**Commentaires et espaces blancs**</span><span class="sxs-lookup"><span data-stu-id="43293-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="43293-133">Tous les espaces blancs qui ne font pas partie d’une chaîne entre guillemets ou identificateur entre guillemets ne font pas partie de la grammaire du langage hello et sont ignorés lors de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="43293-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="43293-134">langage de requête Hello prend en charge les commentaires de style T-SQL comme</span><span class="sxs-lookup"><span data-stu-id="43293-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="43293-135">Instruction SQL `-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="43293-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="43293-136">Alors que commentaires et espaces blancs n’ont pas d’importance dans la grammaire de hello, ils doivent être des jetons tooseparate utilisé.</span><span class="sxs-lookup"><span data-stu-id="43293-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="43293-137">Par exemple : `-1e5` est un jeton à numéro unique, alors que `: – 1 e5` est un jeton moins suivi du chiffre 1 et de l’identificateur e5.</span><span class="sxs-lookup"><span data-stu-id="43293-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="43293-138"><a name="bk_select_query"></a> Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="43293-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="43293-139">clauses Hello dans l’instruction SELECT de hello doivent être classés comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="43293-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="43293-140">L’une des clauses facultatives de hello peut être omise.</span><span class="sxs-lookup"><span data-stu-id="43293-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="43293-141">Mais lorsque clauses facultatives sont utilisées, elles doivent apparaître dans le bon ordre de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="43293-142">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="43293-143">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="43293-144">Toobe propriétés ou la valeur sélectionnée pour le résultat de hello définie.</span><span class="sxs-lookup"><span data-stu-id="43293-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="43293-145">Spécifie que la valeur de hello doit être récupérée sans apporter de modifications.</span><span class="sxs-lookup"><span data-stu-id="43293-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="43293-146">En particulier si la valeur de hello traité est un objet, toutes les propriétés seront récupérées.</span><span class="sxs-lookup"><span data-stu-id="43293-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="43293-147">Spécifie la liste hello de toobe propriétés récupérée.</span><span class="sxs-lookup"><span data-stu-id="43293-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="43293-148">Chaque valeur retournée sera un objet avec les propriétés hello spécifiées.</span><span class="sxs-lookup"><span data-stu-id="43293-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="43293-149">Spécifie que la valeur JSON hello doit être récupéré au lieu de l’objet JSON complet de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="43293-150">Cela, contrairement à `<property_list>` n’encapsule pas de valeur de hello projeté dans un objet.</span><span class="sxs-lookup"><span data-stu-id="43293-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="43293-151">Expression représentant hello valeur toobe calculée.</span><span class="sxs-lookup"><span data-stu-id="43293-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="43293-152">Consultez la section [Expressions scalaires](#bk_scalar_expressions) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="43293-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="43293-153">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="43293-153">**Remarks**</span></span>  
  
<span data-ttu-id="43293-154">Hello `SELECT *` syntaxe est valide uniquement si la clause FROM a déclaré un seul alias.</span><span class="sxs-lookup"><span data-stu-id="43293-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="43293-155">`SELECT *` fournit une projection d’identité, ce qui peut être utile si aucune projection n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="43293-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="43293-156">SELECT * est valide uniquement si la clause FROM est spécifiée et n’a introduit qu’une seule source d’entrée.</span><span class="sxs-lookup"><span data-stu-id="43293-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="43293-157">Notez que `SELECT <select_list>` et `SELECT *` sont ce qu’on appelle du « sucre syntaxique » et que vous pouvez également les exprimer à l’aide d’instructions SELECT simples, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="43293-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="43293-158">équivaut à :</span><span class="sxs-lookup"><span data-stu-id="43293-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="43293-159">équivaut à :</span><span class="sxs-lookup"><span data-stu-id="43293-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="43293-160">**Voir aussi**</span><span class="sxs-lookup"><span data-stu-id="43293-160">**See Also**</span></span>  
  
[<span data-ttu-id="43293-161">Expressions scalaires</span><span class="sxs-lookup"><span data-stu-id="43293-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="43293-162">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="43293-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="43293-163"><a name="bk_from_clause"></a> Clause FROM</span><span class="sxs-lookup"><span data-stu-id="43293-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="43293-164">Spécifie les hello ou les sources jointes.</span><span class="sxs-lookup"><span data-stu-id="43293-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="43293-165">Hello FROM clause est facultative.</span><span class="sxs-lookup"><span data-stu-id="43293-165">hello FROM clause is optional.</span></span> <span data-ttu-id="43293-166">Si elle n’est pas spécifiée, les autres clauses sont exécutées comme si la clause FROM fournissait un document unique.</span><span class="sxs-lookup"><span data-stu-id="43293-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="43293-167">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-167">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="43293-168">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="43293-169">Spécifie une source de données, avec ou sans alias.</span><span class="sxs-lookup"><span data-stu-id="43293-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="43293-170">Si aucun alias n’est spécifié, il est déduit de hello `<collection_expression>` à l’aide de règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="43293-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="43293-171">Si l’expression de hello est collection_name, puis nom_collection servira en tant qu’alias.</span><span class="sxs-lookup"><span data-stu-id="43293-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="43293-172">Si l’expression de hello est `<collection_expression>`, property_name, property_name sera utilisée en tant qu’alias.</span><span class="sxs-lookup"><span data-stu-id="43293-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="43293-173">Si l’expression de hello est collection_name, puis nom_collection servira en tant qu’alias.</span><span class="sxs-lookup"><span data-stu-id="43293-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="43293-174">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="43293-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="43293-175">Spécifie que hello `input_alias` est un ensemble de valeurs renvoyées par hello sous-jacent expression de collection.</span><span class="sxs-lookup"><span data-stu-id="43293-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="43293-176">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="43293-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="43293-177">Spécifie que hello `input_alias` doit représenter l’ensemble de hello des valeurs obtenues en effectuant une itération sur tous les éléments du tableau de chaque tableau retourné par hello sous-jacent expression de collection.</span><span class="sxs-lookup"><span data-stu-id="43293-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="43293-178">Toute valeur retournée par l’expression de collection sous-jacente qui n’est pas un tableau est ignorée.</span><span class="sxs-lookup"><span data-stu-id="43293-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="43293-179">Spécifie tooretrieve hello documents utilisés par hello collection expression toobe.</span><span class="sxs-lookup"><span data-stu-id="43293-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="43293-180">Spécifie qu’un document doit être récupéré à partir de hello collection par défaut, actuellement connectée.</span><span class="sxs-lookup"><span data-stu-id="43293-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="43293-181">Spécifie qu’un document doit être récupéré à partir de la collection de hello fourni.</span><span class="sxs-lookup"><span data-stu-id="43293-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="43293-182">nom Hello de collection de hello doit correspondre au nom hello de collection hello actuellement connectée.</span><span class="sxs-lookup"><span data-stu-id="43293-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="43293-183">Spécifie qu’un document doit être récupéré à partir de hello autre source définie par l’alias de hello fourni.</span><span class="sxs-lookup"><span data-stu-id="43293-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="43293-184">Spécifie qu’un document doit être récupéré en accédant à hello `property_name` élément de tableau de propriété ou array_index pour tous les documents récupérés par l’expression de la collection spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="43293-185">Spécifie qu’un document doit être récupéré en accédant à hello `property_name` élément de tableau de propriété ou array_index pour tous les documents récupérés par l’expression de la collection spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="43293-186">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="43293-186">**Remarks**</span></span>  
  
<span data-ttu-id="43293-187">Tous les alias fournis ou déduits dans hello `<from_source>(`s) doivent être uniques.</span><span class="sxs-lookup"><span data-stu-id="43293-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="43293-188">Hello syntaxe `<collection_expression>.`property_name est hello identique `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="43293-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="43293-189">Toutefois, la syntaxe de cette dernière de hello peut être utilisée si un nom de propriété contient des caractères non-identifiants.</span><span class="sxs-lookup"><span data-stu-id="43293-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="43293-190">**Gestion des propriétés manquantes, des éléments de tableau manquants et des valeurs non définies**</span><span class="sxs-lookup"><span data-stu-id="43293-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="43293-191">Si une expression de collection accède à des propriétés ou éléments de tableau et que la valeur n’existe pas, cette valeur sera ignorée et n’est plus traitée.</span><span class="sxs-lookup"><span data-stu-id="43293-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="43293-192">**Étendue de contexte d’expression de collection**</span><span class="sxs-lookup"><span data-stu-id="43293-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="43293-193">Une expression de collection peut avoir une étendue de document ou de collection :</span><span class="sxs-lookup"><span data-stu-id="43293-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="43293-194">Une expression est étendue à une collection, si hello source sous-jacente de l’expression de collection hello est ROOT ou `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="43293-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="43293-195">Une telle expression représente un ensemble de documents récupérés directement à partir de la collection de hello et n’est pas dépendante de traitement hello d’autres expressions de collection.</span><span class="sxs-lookup"><span data-stu-id="43293-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="43293-196">Une expression est étendu à un document, si hello source sous-jacente de l’expression de collection hello `input_alias` introduit précédemment dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="43293-197">Une telle expression représente un ensemble de documents obtenus en évaluant l’expression de collection hello dans la portée de hello de chaque document appartenant ensemble toohello associée hello alias collection.</span><span class="sxs-lookup"><span data-stu-id="43293-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="43293-198">Hello résultante sera une union de jeux obtenus en évaluant l’expression de collection hello pour chacun des documents hello Bonjour sous-jacent ensemble.</span><span class="sxs-lookup"><span data-stu-id="43293-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="43293-199">**Jointures**</span><span class="sxs-lookup"><span data-stu-id="43293-199">**Joins**</span></span>  
  
<span data-ttu-id="43293-200">Dans la version actuelle de hello, base de données Azure Cosmos prend en charge les jointures internes.</span><span class="sxs-lookup"><span data-stu-id="43293-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="43293-201">Des fonctionnalités de jointure supplémentaires sont à venir.</span><span class="sxs-lookup"><span data-stu-id="43293-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="43293-202">Les jeux de résultats des jointures internes dans un produit croisé complet de hello participant à la jointure de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="43293-203">résultat de Hello d’une jointure N-way est un jeu de tuples de N éléments, où chaque valeur dans le tuple de hello est associé à un alias de hello définir participant dans une jointure de hello et sont accessibles en référençant cet alias dans d’autres clauses.</span><span class="sxs-lookup"><span data-stu-id="43293-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="43293-204">évaluation de Hello de jointure de hello dépend de la portée du contexte hello Hello participant à des jeux :</span><span class="sxs-lookup"><span data-stu-id="43293-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="43293-205">Une jointure entre un jeu de collection A et un jeu à étendue de collection B aboutit à un produit croisé de tous les éléments des jeux A et B.</span><span class="sxs-lookup"><span data-stu-id="43293-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="43293-206">Une jointure entre le jeu A et le jeu à étendue de document B aboutit à une union de tous les jeux obtenus en évaluant le jeu à étendue de document B pour chaque document du jeu A.</span><span class="sxs-lookup"><span data-stu-id="43293-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="43293-207">Dans la version actuelle de hello, un maximum d’une expression à une collection est pris en charge par le processeur de requêtes hello.</span><span class="sxs-lookup"><span data-stu-id="43293-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="43293-208">**Exemples de jointures :**</span><span class="sxs-lookup"><span data-stu-id="43293-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="43293-209">Examinons hello après la clause FROM :`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="43293-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="43293-210">Laissez chaque source définir `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="43293-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="43293-211">La close FROM renvoie un ensemble de N-tuples (un tuple avec N valeurs).</span><span class="sxs-lookup"><span data-stu-id="43293-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="43293-212">Les valeurs de chaque tuple sont produites par l'itération de tous les alias de la collection sur leurs ensembles respectifs.</span><span class="sxs-lookup"><span data-stu-id="43293-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="43293-213">*Exemple de JOIN 1, avec 2 sources :*</span><span class="sxs-lookup"><span data-stu-id="43293-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="43293-214">Laissez `<from_source1>` être étendu à une collection et représenter le jeu {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="43293-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="43293-215">Laissez `<from_source2>` être étendu à un document référençant input_alias1 et représenter les jeux :</span><span class="sxs-lookup"><span data-stu-id="43293-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="43293-216">{1, 2} pour `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="43293-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="43293-217">{3} pour `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="43293-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="43293-218">{4, 5} pour `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="43293-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="43293-219">Bonjour à partir de la clause `<from_source1> JOIN <from_source2>` entraîne hello suivant tuples :</span><span class="sxs-lookup"><span data-stu-id="43293-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="43293-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="43293-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="43293-221">*Exemple de JOIN 2, avec 3 sources :*</span><span class="sxs-lookup"><span data-stu-id="43293-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="43293-222">Laissez `<from_source1>` être étendu à une collection et représenter le jeu {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="43293-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="43293-223">Laissez `<from_source2>` être étendu à un document référençant input_`input_alias1` et représenter les jeux :</span><span class="sxs-lookup"><span data-stu-id="43293-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="43293-224">{1, 2} pour `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="43293-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="43293-225">{3} pour `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="43293-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="43293-226">{4, 5} pour `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="43293-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="43293-227">Laissez `<from_source3>` être étendu à un document référençant input_`input_alias2` et représenter les jeux :</span><span class="sxs-lookup"><span data-stu-id="43293-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="43293-228">{100, 200} pour `input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="43293-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="43293-229">{300} pour `input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="43293-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="43293-230">Bonjour à partir de la clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` entraîne hello suivant tuples :</span><span class="sxs-lookup"><span data-stu-id="43293-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="43293-231">(input_alias1, input_alias2, input_alias3) :</span><span class="sxs-lookup"><span data-stu-id="43293-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="43293-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="43293-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="43293-233">Absence de tuples pour d’autres valeurs de `input_alias1`, `input_alias2`, pour quels hello `<from_source3>` n’a pas retourné de toutes les valeurs.</span><span class="sxs-lookup"><span data-stu-id="43293-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="43293-234">*Exemple de JOIN 3, avec 3 sources :*</span><span class="sxs-lookup"><span data-stu-id="43293-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="43293-235">Laissez <from_source1> être étendu à une collection et représenter le jeu {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="43293-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="43293-236">Laissez `<from_source1>` être étendu à une collection et représenter le jeu {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="43293-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="43293-237">Laissez <from_source2> être étendu à un document référençant input_source1 et représenter les jeux :</span><span class="sxs-lookup"><span data-stu-id="43293-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="43293-238">{1, 2} pour `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="43293-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="43293-239">{3} pour `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="43293-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="43293-240">{4, 5} pour `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="43293-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="43293-241">Laisser `<from_source3>` étendu trop`input_alias1` et représente des jeux :</span><span class="sxs-lookup"><span data-stu-id="43293-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="43293-242">{100, 200} pour `input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="43293-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="43293-243">{300} pour `input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="43293-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="43293-244">Bonjour à partir de la clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` entraîne hello suivant tuples :</span><span class="sxs-lookup"><span data-stu-id="43293-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="43293-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="43293-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="43293-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="43293-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="43293-247">Cela a abouti à un produit croisé entre `<from_source2>` et `<from_source3>` , car les deux sont incluses dans l’étendue toohello même `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="43293-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="43293-248">Cela a about à 4 (2 x 2) tuples de valeur A, 0 tuple de valeur B (1 x 0) et 2 (2 x 1) tuples de valeur C.</span><span class="sxs-lookup"><span data-stu-id="43293-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="43293-249">**Voir aussi**</span><span class="sxs-lookup"><span data-stu-id="43293-249">**See also**</span></span>  
  
 [<span data-ttu-id="43293-250">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="43293-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="43293-251"><a name="bk_where_clause"></a> Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="43293-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="43293-252">Spécifie la condition de recherche hello pour les documents hello retourné par la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="43293-253">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="43293-254">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="43293-255">Spécifie les hello toobe de condition remplie pour hello documents toobe est retourné.</span><span class="sxs-lookup"><span data-stu-id="43293-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="43293-256">Expression représentant hello valeur toobe calculée.</span><span class="sxs-lookup"><span data-stu-id="43293-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="43293-257">Consultez hello [expressions scalaires](#bk_scalar_expressions) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="43293-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="43293-258">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="43293-258">**Remarks**</span></span>  
  
 <span data-ttu-id="43293-259">Dans l’ordre pour hello document toobe retourné une expression spécifiée comme condition de filtre doit évaluer tootrue.</span><span class="sxs-lookup"><span data-stu-id="43293-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="43293-260">Seule la valeur booléenne true satisfait la condition de hello, toute autre valeur : undefined, null, la valeur est false, nombre, un tableau ou objet, ne satisfait pas la condition de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="43293-261"><a name="bk_orderby_clause"></a> Clause ORDER BY</span><span class="sxs-lookup"><span data-stu-id="43293-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="43293-262">Spécifie les hello ordre de tri des résultats retournés par la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="43293-263">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="43293-264">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="43293-265">Spécifie une propriété ou une expression sur laquelle l’ensemble de résultats de requête toosort hello.</span><span class="sxs-lookup"><span data-stu-id="43293-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="43293-266">Une colonne de tri peut être spécifiée comme un alias de nom ou de la colonne.</span><span class="sxs-lookup"><span data-stu-id="43293-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="43293-267">Plusieurs colonnes de tri peuvent être spécifiées.</span><span class="sxs-lookup"><span data-stu-id="43293-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="43293-268">Les noms de colonne doivent être uniques.</span><span class="sxs-lookup"><span data-stu-id="43293-268">Column names must be unique.</span></span> <span data-ttu-id="43293-269">séquence Hello hello des colonnes de tri dans la clause ORDER BY hello définit organisation hello hello triée de jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="43293-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="43293-270">Autrement dit, jeu de résultats hello est triée par la propriété de première hello et ensuite cette liste triée est triée par la deuxième propriété de hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="43293-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="43293-271">noms des colonnes référencées dans la clause ORDER BY hello Hello doivent correspondre tooeither une colonne Bonjour sélectionner la colonne de liste ou tooa définie dans une table spécifiée dans la clause FROM de hello sans ambiguïté.</span><span class="sxs-lookup"><span data-stu-id="43293-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="43293-272">Spécifie une propriété unique ou une expression sur le jeu de résultats de requête toosort hello.</span><span class="sxs-lookup"><span data-stu-id="43293-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="43293-273">Consultez hello [expressions scalaires](#bk_scalar_expressions) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="43293-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="43293-274">Spécifie que les valeurs hello dans la colonne spécifiée de hello doivent être triées dans l’ordre croissant ou décroissant.</span><span class="sxs-lookup"><span data-stu-id="43293-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="43293-275">ASC effectue le tri de hello la plus petite valeur toohighest.</span><span class="sxs-lookup"><span data-stu-id="43293-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="43293-276">DESC effectue le tri de la plus grande valeur toolowest.</span><span class="sxs-lookup"><span data-stu-id="43293-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="43293-277">ASC est l’ordre de tri par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="43293-277">ASC is hello default sort order.</span></span> <span data-ttu-id="43293-278">Les valeurs NULL sont traitées comme valeurs possibles de hello plus bas.</span><span class="sxs-lookup"><span data-stu-id="43293-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="43293-279">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="43293-279">**Remarks**</span></span>  
  
 <span data-ttu-id="43293-280">Grammaire de requête hello prend en charge plusieurs ordre par les propriétés, exécution de requête de base de données Azure Cosmos hello prend en charge le tri uniquement par rapport à une seule propriété et uniquement sur les noms de propriété, autrement dit, pas sur les propriétés calculées.</span><span class="sxs-lookup"><span data-stu-id="43293-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="43293-281">Tri requiert également que hello stratégie d’indexation inclut un index de plage pour la propriété de hello et hello spécifié type, avec une précision maximale de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="43293-282">Consultez toohello l’indexation de documentation pour plus d’informations sur les stratégies.</span><span class="sxs-lookup"><span data-stu-id="43293-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="43293-283"><a name="bk_scalar_expressions"></a> Expressions scalaires</span><span class="sxs-lookup"><span data-stu-id="43293-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="43293-284">Une expression scalaire est une combinaison de symboles et opérateurs qui peuvent être évalués tooobtain une valeur unique.</span><span class="sxs-lookup"><span data-stu-id="43293-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="43293-285">Les expressions simples peuvent être des constantes, des références de propriété, des références d’élément de tableau, des références d’alias ou des appels de fonction.</span><span class="sxs-lookup"><span data-stu-id="43293-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="43293-286">Les expressions simples peuvent être combinées dans des expressions complexes utilisant des opérateurs.</span><span class="sxs-lookup"><span data-stu-id="43293-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="43293-287">Pour plus d’informations sur les valeurs qu’une expression scalaire peut avoir, consultez la section [constantes](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="43293-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="43293-288">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-288">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="43293-289">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="43293-290">Représente une valeur constante.</span><span class="sxs-lookup"><span data-stu-id="43293-290">Represents a constant value.</span></span> <span data-ttu-id="43293-291">Consultez la section [Constantes](#bk_constants) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="43293-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="43293-292">Représente une valeur définie par hello `input_alias` introduite dans hello `FROM` clause.</span><span class="sxs-lookup"><span data-stu-id="43293-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="43293-293">Cette valeur est garantie toonot être **non défini** –**non défini** les valeurs dans l’entrée de hello sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="43293-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="43293-294">Représente une valeur de propriété hello d’un objet.</span><span class="sxs-lookup"><span data-stu-id="43293-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="43293-295">Si hello propriété n’existe pas ou est référencée sur une valeur qui n’est pas un objet, puis hello expression évalue trop**non défini** valeur.</span><span class="sxs-lookup"><span data-stu-id="43293-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="43293-296">Représente une valeur de propriété hello portant le nom `property_name` ou élément de tableau avec l’index `array_index` d’un objet/tableau.</span><span class="sxs-lookup"><span data-stu-id="43293-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="43293-297">Si l’index de tableau de la propriété hello n’existe pas ou les index de tableau de la propriété hello est référencée sur une valeur qui n’est pas un objet/tableau, l’expression de hello évalue tooundefined valeur.</span><span class="sxs-lookup"><span data-stu-id="43293-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="43293-298">Représente un opérateur est appliqué tooa une seule valeur.</span><span class="sxs-lookup"><span data-stu-id="43293-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="43293-299">Consultez la section [Opérateurs](#bk_operators) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="43293-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="43293-300">Représente un opérateur est appliqué tootwo valeurs.</span><span class="sxs-lookup"><span data-stu-id="43293-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="43293-301">Consultez la section [Opérateurs](#bk_operators) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="43293-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="43293-302">Représente une valeur définie par le résultat d’un appel de fonction.</span><span class="sxs-lookup"><span data-stu-id="43293-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="43293-303">Fonction scalaire définie par le nom d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="43293-304">Nom de fonction scalaire intégrée de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="43293-305">Représente une valeur obtenue en créant un nouvel objet avec les propriétés spécifiées et leurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="43293-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="43293-306">Représente une valeur obtenue en créant un nouveau tableau avec les valeurs spécifiées en tant qu’éléments</span><span class="sxs-lookup"><span data-stu-id="43293-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="43293-307">Représente une valeur de nom de paramètre spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="43293-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="43293-308">Les noms de paramètres doivent avoir un seul @ comme premier caractère de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="43293-309">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="43293-309">**Remarks**</span></span>  
  
 <span data-ttu-id="43293-310">Lors de l’appel à une fonction scalaire intégrée ou définie par l’utilisateur, tous les arguments doivent être définis.</span><span class="sxs-lookup"><span data-stu-id="43293-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="43293-311">Si un des arguments de hello n’est pas défini, fonction hello ne sera pas appelée et le résultat de hello n’est pas défini.</span><span class="sxs-lookup"><span data-stu-id="43293-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="43293-312">Lorsque vous créez un objet, n’importe quelle propriété de valeur indéfinie est ignorée et pas incluse dans hello créé l’objet.</span><span class="sxs-lookup"><span data-stu-id="43293-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="43293-313">Lorsque la création d’un tableau, toute valeur de l’élément qui est attribué **non défini** valeur sera ignorée et pas inclus dans l’objet de hello créé.</span><span class="sxs-lookup"><span data-stu-id="43293-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="43293-314">Cela entraîne hello ensuite défini élément tootake la place de manière à ce tableau hello créé ne sera pas ont index ignoré.</span><span class="sxs-lookup"><span data-stu-id="43293-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="43293-315"><a name="bk_operators"></a> Opérateurs</span><span class="sxs-lookup"><span data-stu-id="43293-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="43293-316">Cette section décrit les opérateurs hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="43293-316">This section describes hello supported operators.</span></span> <span data-ttu-id="43293-317">Chaque opérateur peut être attribué tooexactly une catégorie.</span><span class="sxs-lookup"><span data-stu-id="43293-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="43293-318">Consultez le tableau **Catégories d’opérateurs** ci-dessous pour plus d’informations sur la gestion des valeurs **Undefined**, des exigences de type pour les valeurs d’entrée et la gestion des valeurs sans types correspondants.</span><span class="sxs-lookup"><span data-stu-id="43293-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="43293-319">**Catégories d’opérateurs :**</span><span class="sxs-lookup"><span data-stu-id="43293-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="43293-320">**Catégorie**</span><span class="sxs-lookup"><span data-stu-id="43293-320">**Category**</span></span>|<span data-ttu-id="43293-321">**Détails**</span><span class="sxs-lookup"><span data-stu-id="43293-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="43293-322">**Opérateurs arithmétiques**</span><span class="sxs-lookup"><span data-stu-id="43293-322">**arithmetic**</span></span>|<span data-ttu-id="43293-323">L’opérateur attend que les entrées toobe numéro (s).</span><span class="sxs-lookup"><span data-stu-id="43293-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="43293-324">La sortie est également un nombre.</span><span class="sxs-lookup"><span data-stu-id="43293-324">Output is also a Number.</span></span> <span data-ttu-id="43293-325">Si une des entrées de hello est **non défini** ou type de résultat de nombre, hello est **non défini**.</span><span class="sxs-lookup"><span data-stu-id="43293-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="43293-326">**Opérateurs au niveau du bit**</span><span class="sxs-lookup"><span data-stu-id="43293-326">**bitwise**</span></span>|<span data-ttu-id="43293-327">L’opérateur attend que les entrées entier signé de 32 bits toobe numéro (s).</span><span class="sxs-lookup"><span data-stu-id="43293-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="43293-328">La sortie est également un nombre entier signé 32 bits.</span><span class="sxs-lookup"><span data-stu-id="43293-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="43293-329">Toute valeur non entière est arrondie.</span><span class="sxs-lookup"><span data-stu-id="43293-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="43293-330">Les valeurs positives sont arrondies vers le bas, et les valeurs négatives vers le haut.</span><span class="sxs-lookup"><span data-stu-id="43293-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="43293-331">Toute valeur qui est en dehors de la plage d’entiers 32 bits et hello sera converti, en prenant les derniers 32 bits de ses deux notation de complément.</span><span class="sxs-lookup"><span data-stu-id="43293-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="43293-332">Si une des entrées de hello est **non défini** ou de type autre qu’un nombre, il en résulte hello **non défini**.</span><span class="sxs-lookup"><span data-stu-id="43293-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="43293-333">**Remarque :** hello au-dessus de comportement est compatible avec le comportement de l’opérateur au niveau du bit JavaScript.</span><span class="sxs-lookup"><span data-stu-id="43293-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="43293-334">**Opérateurs logiques**</span><span class="sxs-lookup"><span data-stu-id="43293-334">**logical**</span></span>|<span data-ttu-id="43293-335">L’opérateur attend que les entrées toobe des valeurs booléennes.</span><span class="sxs-lookup"><span data-stu-id="43293-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="43293-336">La sortie est également une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="43293-337">Si une des entrées de hello est **non défini** ou autre qu’une valeur booléenne de type hello résultat sera **non défini**.</span><span class="sxs-lookup"><span data-stu-id="43293-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="43293-338">**Opérateurs de comparaison**</span><span class="sxs-lookup"><span data-stu-id="43293-338">**comparison**</span></span>|<span data-ttu-id="43293-339">L’opérateur attend que les entrées toohave hello même type et non définies.</span><span class="sxs-lookup"><span data-stu-id="43293-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="43293-340">La sortie est une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="43293-341">Si une des entrées de hello est **non défini** ou entrées de hello ont des types différents, puis il en résulte hello **non défini**.</span><span class="sxs-lookup"><span data-stu-id="43293-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="43293-342">Consultez le tableau **Classement des valeurs pour comparaison** pour plus de détails sur le classement des valeurs.</span><span class="sxs-lookup"><span data-stu-id="43293-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="43293-343">**string**</span><span class="sxs-lookup"><span data-stu-id="43293-343">**string**</span></span>|<span data-ttu-id="43293-344">L’opérateur attend que les entrées toobe ou les chaînes.</span><span class="sxs-lookup"><span data-stu-id="43293-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="43293-345">La sortie est également une chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-345">Output is also a String.</span></span><br /><span data-ttu-id="43293-346">Si une des entrées de hello est **non défini** ou type de résultat de chaîne puis hello est **non défini**.</span><span class="sxs-lookup"><span data-stu-id="43293-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="43293-347">**Opérateurs unaires :**</span><span class="sxs-lookup"><span data-stu-id="43293-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="43293-348">**Name**</span><span class="sxs-lookup"><span data-stu-id="43293-348">**Name**</span></span>|<span data-ttu-id="43293-349">**Opérateur**</span><span class="sxs-lookup"><span data-stu-id="43293-349">**Operator**</span></span>|<span data-ttu-id="43293-350">**Détails**</span><span class="sxs-lookup"><span data-stu-id="43293-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="43293-351">**Opérateurs arithmétiques**</span><span class="sxs-lookup"><span data-stu-id="43293-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="43293-352">Retourne la valeur nombre hello.</span><span class="sxs-lookup"><span data-stu-id="43293-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="43293-353">Négation au niveau du bit.</span><span class="sxs-lookup"><span data-stu-id="43293-353">Bitwise negation.</span></span> <span data-ttu-id="43293-354">Retourne une valeur numérique avec négation.</span><span class="sxs-lookup"><span data-stu-id="43293-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="43293-355">**Opérateurs au niveau du bit**</span><span class="sxs-lookup"><span data-stu-id="43293-355">**bitwise**</span></span>|~|<span data-ttu-id="43293-356">Complément d’une valeur.</span><span class="sxs-lookup"><span data-stu-id="43293-356">Ones' complement.</span></span> <span data-ttu-id="43293-357">Retourne un complément d’une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="43293-358">**Opérateurs logiques**</span><span class="sxs-lookup"><span data-stu-id="43293-358">**Logical**</span></span>|<span data-ttu-id="43293-359">**NOT**</span><span class="sxs-lookup"><span data-stu-id="43293-359">**NOT**</span></span>|<span data-ttu-id="43293-360">Négation.</span><span class="sxs-lookup"><span data-stu-id="43293-360">Negation.</span></span> <span data-ttu-id="43293-361">Retourne une valeur booléenne avec négation.</span><span class="sxs-lookup"><span data-stu-id="43293-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="43293-362">**Opérateurs binaires :**</span><span class="sxs-lookup"><span data-stu-id="43293-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="43293-363">**Name**</span><span class="sxs-lookup"><span data-stu-id="43293-363">**Name**</span></span>|<span data-ttu-id="43293-364">**Opérateur**</span><span class="sxs-lookup"><span data-stu-id="43293-364">**Operator**</span></span>|<span data-ttu-id="43293-365">**Détails**</span><span class="sxs-lookup"><span data-stu-id="43293-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="43293-366">**Opérateurs arithmétiques**</span><span class="sxs-lookup"><span data-stu-id="43293-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="43293-367">Addition.</span><span class="sxs-lookup"><span data-stu-id="43293-367">Addition.</span></span><br /><br /> <span data-ttu-id="43293-368">Soustraction.</span><span class="sxs-lookup"><span data-stu-id="43293-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="43293-369">Multiplication.</span><span class="sxs-lookup"><span data-stu-id="43293-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="43293-370">Division.</span><span class="sxs-lookup"><span data-stu-id="43293-370">Division.</span></span><br /><br /> <span data-ttu-id="43293-371">Modulation.</span><span class="sxs-lookup"><span data-stu-id="43293-371">Modulation.</span></span>|  
|<span data-ttu-id="43293-372">**Opérateurs au niveau du bit**</span><span class="sxs-lookup"><span data-stu-id="43293-372">**bitwise**</span></span>|<span data-ttu-id="43293-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="43293-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="43293-374">Opérateur OR au niveau du bit.</span><span class="sxs-lookup"><span data-stu-id="43293-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="43293-375">Opérateur AND au niveau du bit.</span><span class="sxs-lookup"><span data-stu-id="43293-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="43293-376">XOR au niveau du bit.</span><span class="sxs-lookup"><span data-stu-id="43293-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="43293-377">Décalage vers la gauche.</span><span class="sxs-lookup"><span data-stu-id="43293-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="43293-378">Décalage vers la droite.</span><span class="sxs-lookup"><span data-stu-id="43293-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="43293-379">Décalage vers la droite avec remplissage de zéros.</span><span class="sxs-lookup"><span data-stu-id="43293-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="43293-380">**Opérateurs logiques**</span><span class="sxs-lookup"><span data-stu-id="43293-380">**logical**</span></span>|<span data-ttu-id="43293-381">**AND**</span><span class="sxs-lookup"><span data-stu-id="43293-381">**AND**</span></span><br /><br /> <span data-ttu-id="43293-382">**OR**</span><span class="sxs-lookup"><span data-stu-id="43293-382">**OR**</span></span>|<span data-ttu-id="43293-383">Conjonction logique.</span><span class="sxs-lookup"><span data-stu-id="43293-383">Logical conjunction.</span></span> <span data-ttu-id="43293-384">Retourne **true** si les deux arguments sont **true**, retourne **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="43293-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="43293-385">Conjonction logique.</span><span class="sxs-lookup"><span data-stu-id="43293-385">Logical conjunction.</span></span> <span data-ttu-id="43293-386">Retourne **true** si les deux arguments sont **true**, retourne **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="43293-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="43293-387">**Opérateurs de comparaison**</span><span class="sxs-lookup"><span data-stu-id="43293-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="43293-388">**!=, &lt;&gt;**</span><span class="sxs-lookup"><span data-stu-id="43293-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="43293-389">**??**</span><span class="sxs-lookup"><span data-stu-id="43293-389">**??**</span></span>|<span data-ttu-id="43293-390">Égal à.</span><span class="sxs-lookup"><span data-stu-id="43293-390">Equals.</span></span> <span data-ttu-id="43293-391">Retourne **true** si les arguments sont égaux, **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="43293-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="43293-392">Non égal à.</span><span class="sxs-lookup"><span data-stu-id="43293-392">Not equal to.</span></span> <span data-ttu-id="43293-393">Retourne **true** si les arguments ne sont pas égaux, **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="43293-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="43293-394">Supérieur à.</span><span class="sxs-lookup"><span data-stu-id="43293-394">Greater Than.</span></span> <span data-ttu-id="43293-395">Retourne **true** si le premier argument est supérieure à hello deuxième **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="43293-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="43293-396">Supérieur ou égal à.</span><span class="sxs-lookup"><span data-stu-id="43293-396">Greater Than or Equal To.</span></span> <span data-ttu-id="43293-397">Retourne **true** si le premier argument est supérieur ou égal à un deuxième toohello, retourner **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="43293-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="43293-398">Inférieur à.</span><span class="sxs-lookup"><span data-stu-id="43293-398">Less Than.</span></span> <span data-ttu-id="43293-399">Retourne **true** si le premier argument est inférieur au hello deuxième **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="43293-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="43293-400">Inférieur ou égal à.</span><span class="sxs-lookup"><span data-stu-id="43293-400">Less Than or Equal To.</span></span> <span data-ttu-id="43293-401">Retourne **true** si le premier argument est inférieur ou égal toohello seconde un retour **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="43293-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="43293-402">Coalesce.</span><span class="sxs-lookup"><span data-stu-id="43293-402">Coalesce.</span></span> <span data-ttu-id="43293-403">Retourne hello deuxième argument si hello premier argument est un **non défini** valeur.</span><span class="sxs-lookup"><span data-stu-id="43293-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="43293-404">**Chaîne**</span><span class="sxs-lookup"><span data-stu-id="43293-404">**String**</span></span>|<span data-ttu-id="43293-405">**&amp;#124;&amp;#124;**</span><span class="sxs-lookup"><span data-stu-id="43293-405">**&#124;&#124;**</span></span>|<span data-ttu-id="43293-406">Concaténation.</span><span class="sxs-lookup"><span data-stu-id="43293-406">Concatenation.</span></span> <span data-ttu-id="43293-407">Renvoie une concaténation de deux arguments.</span><span class="sxs-lookup"><span data-stu-id="43293-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="43293-408">**Opérateurs ternaires :**</span><span class="sxs-lookup"><span data-stu-id="43293-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="43293-409">Opérateur ternaire</span><span class="sxs-lookup"><span data-stu-id="43293-409">Ternary operator</span></span>|<span data-ttu-id="43293-410">?</span><span class="sxs-lookup"><span data-stu-id="43293-410">?</span></span>|<span data-ttu-id="43293-411">Retourne hello deuxième argument si le premier argument de hello évalue trop**true**; retourne le troisième argument de hello dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="43293-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="43293-412">**Ordre des valeurs pour comparaison**</span><span class="sxs-lookup"><span data-stu-id="43293-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="43293-413">**Type**</span><span class="sxs-lookup"><span data-stu-id="43293-413">**Type**</span></span>|<span data-ttu-id="43293-414">**Ordre des valeurs**</span><span class="sxs-lookup"><span data-stu-id="43293-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="43293-415">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="43293-415">**Undefined**</span></span>|<span data-ttu-id="43293-416">Non comparables.</span><span class="sxs-lookup"><span data-stu-id="43293-416">Not comparable.</span></span>|  
|<span data-ttu-id="43293-417">**Null**</span><span class="sxs-lookup"><span data-stu-id="43293-417">**Null**</span></span>|<span data-ttu-id="43293-418">Valeur unique : **null**</span><span class="sxs-lookup"><span data-stu-id="43293-418">Single value: **null**</span></span>|  
|<span data-ttu-id="43293-419">**Nombre**</span><span class="sxs-lookup"><span data-stu-id="43293-419">**Number**</span></span>|<span data-ttu-id="43293-420">Nombre réel naturel.</span><span class="sxs-lookup"><span data-stu-id="43293-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="43293-421">La valeur d’infini négatif est inférieure à toute autre valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="43293-422">La valeur d’infini positif est supérieure à toute autre valeur numérique. La valeur **NaN** n’est pas comparable.</span><span class="sxs-lookup"><span data-stu-id="43293-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="43293-423">La comparaison avec **NaN** entraîne une valeur **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="43293-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="43293-424">**Chaîne**</span><span class="sxs-lookup"><span data-stu-id="43293-424">**String**</span></span>|<span data-ttu-id="43293-425">Ordre lexicographique.</span><span class="sxs-lookup"><span data-stu-id="43293-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="43293-426">**Tableau**</span><span class="sxs-lookup"><span data-stu-id="43293-426">**Array**</span></span>|<span data-ttu-id="43293-427">Aucun ordre, mais équitable.</span><span class="sxs-lookup"><span data-stu-id="43293-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="43293-428">**Object**</span><span class="sxs-lookup"><span data-stu-id="43293-428">**Object**</span></span>|<span data-ttu-id="43293-429">Aucun ordre, mais équitable.</span><span class="sxs-lookup"><span data-stu-id="43293-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="43293-430">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="43293-430">**Remarks**</span></span>  
  
 <span data-ttu-id="43293-431">Dans la base de données Azure Cosmos, types hello de valeurs sont souvent inconnus jusqu'à ce qu’ils soient effectivement récupérés à partir de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="43293-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="43293-432">Dans l’ordre toosupport une exécution efficace des requêtes, la plupart des opérateurs de hello ont des exigences de type strict.</span><span class="sxs-lookup"><span data-stu-id="43293-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="43293-433">De plus, les opérateurs n’effectuent pas de conversions implicites eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="43293-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="43293-434">Cela signifie qu’une requête, tels que : sélectionnez * FROM ROOT r WHERE r.Age = 21 retourne uniquement les documents dont la propriété nombre de toohello égal âge 21.</span><span class="sxs-lookup"><span data-stu-id="43293-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="43293-435">Documents avec la propriété Age toohello égal chaîne « 21 » ou hello « 0021 » ne correspondent pas, comme l’expression hello « 21 » = 21 produit une valeur tooundefined.</span><span class="sxs-lookup"><span data-stu-id="43293-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="43293-436">Cela permet une meilleure utilisation des index, car recherche hello d’une valeur spécifique (c'est-à-dire le numéro 21) est plus rapide que la recherche d’un nombre indéfini de correspondances potentielles (nombre 21 ou chaînes « 21 », « 021 », « 21.0 »...).</span><span class="sxs-lookup"><span data-stu-id="43293-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="43293-437">Cela est différent de la manière dont JavaScript évalue les opérateurs sur les valeurs de types différents.</span><span class="sxs-lookup"><span data-stu-id="43293-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="43293-438">**Comparaison et égalité pour les objets et tableaux**</span><span class="sxs-lookup"><span data-stu-id="43293-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="43293-439">La comparaison des valeurs de tableau ou d’objet à l’aide des opérateurs de plage (>, > =, <, < =) entraînera un résultat Undefined, car il n’existe pas d’ordre défini sur les valeurs d’objet ou de tableau.</span><span class="sxs-lookup"><span data-stu-id="43293-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="43293-440">Toutefois, l’utilisation d’opérateurs d’égalité/inégalité (=, ! =, <>) est prise en charge et les valeurs seront comparées structurellement.</span><span class="sxs-lookup"><span data-stu-id="43293-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="43293-441">Les tableaux sont égaux si les deux tableaux ont le même nombre d’éléments et que les éléments aux positions correspondantes sont également égaux.</span><span class="sxs-lookup"><span data-stu-id="43293-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="43293-442">Si la comparaison d’une paire d’éléments entraîne des résultats hello non défini, de comparaison de tableau est indéfini.</span><span class="sxs-lookup"><span data-stu-id="43293-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="43293-443">Les objets sont égaux si les deux objets ont les mêmes propriétés définies, et si les valeurs des propriétés correspondantes sont également égales.</span><span class="sxs-lookup"><span data-stu-id="43293-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="43293-444">Si la comparaison d’une paire de valeurs de propriété entraîne des résultats hello non défini, de comparaison de l’objet est indéfini.</span><span class="sxs-lookup"><span data-stu-id="43293-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="43293-445"><a name="bk_constants"></a> Constantes</span><span class="sxs-lookup"><span data-stu-id="43293-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="43293-446">Une constante, également appelée un littéral ou une valeur scalaire, est un symbole représentant une valeur de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="43293-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="43293-447">format Hello d’une constante varie selon le type de données hello de valeur hello qu’il représente.</span><span class="sxs-lookup"><span data-stu-id="43293-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="43293-448">**Prise en charge des types de données scalaires :**</span><span class="sxs-lookup"><span data-stu-id="43293-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="43293-449">**Type**</span><span class="sxs-lookup"><span data-stu-id="43293-449">**Type**</span></span>|<span data-ttu-id="43293-450">**Ordre des valeurs**</span><span class="sxs-lookup"><span data-stu-id="43293-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="43293-451">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="43293-451">**Undefined**</span></span>|<span data-ttu-id="43293-452">Valeur unique : **Undefined**</span><span class="sxs-lookup"><span data-stu-id="43293-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="43293-453">**Null**</span><span class="sxs-lookup"><span data-stu-id="43293-453">**Null**</span></span>|<span data-ttu-id="43293-454">Valeur unique : **null**</span><span class="sxs-lookup"><span data-stu-id="43293-454">Single value: **null**</span></span>|  
|<span data-ttu-id="43293-455">**Booléen**</span><span class="sxs-lookup"><span data-stu-id="43293-455">**Boolean**</span></span>|<span data-ttu-id="43293-456">Valeurs : **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="43293-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="43293-457">**Nombre**</span><span class="sxs-lookup"><span data-stu-id="43293-457">**Number**</span></span>|<span data-ttu-id="43293-458">Un nombre à virgule flottante double précision répondant à la norme IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="43293-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="43293-459">**Chaîne**</span><span class="sxs-lookup"><span data-stu-id="43293-459">**String**</span></span>|<span data-ttu-id="43293-460">Une séquence de zéro ou plusieurs caractères Unicode.</span><span class="sxs-lookup"><span data-stu-id="43293-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="43293-461">Les chaînes doivent figurer entre guillemets simples ou doubles.</span><span class="sxs-lookup"><span data-stu-id="43293-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="43293-462">**Tableau**</span><span class="sxs-lookup"><span data-stu-id="43293-462">**Array**</span></span>|<span data-ttu-id="43293-463">Une séquence de zéro ou plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="43293-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="43293-464">Chaque élément peut être une valeur de tout type de données scalaires, à l’exception de Undefined.</span><span class="sxs-lookup"><span data-stu-id="43293-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="43293-465">**Object**</span><span class="sxs-lookup"><span data-stu-id="43293-465">**Object**</span></span>|<span data-ttu-id="43293-466">Un jeu non ordonné de zéro ou plusieurs paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="43293-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="43293-467">Le nom est une chaîne Unicode, la valeur peut être de n’importe quel type de données scalaire, sauf **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="43293-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="43293-468">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-468">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="43293-469">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="43293-470">Représente la valeur undefined du type Undefined.</span><span class="sxs-lookup"><span data-stu-id="43293-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="43293-471">Représente la valeur **null** du type **Null**.</span><span class="sxs-lookup"><span data-stu-id="43293-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="43293-472">Représente une constante de type booléen.</span><span class="sxs-lookup"><span data-stu-id="43293-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="43293-473">Représente une valeur **false** de type booléen.</span><span class="sxs-lookup"><span data-stu-id="43293-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="43293-474">Représente une valeur **true** de type booléen.</span><span class="sxs-lookup"><span data-stu-id="43293-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="43293-475">Représente une constante.</span><span class="sxs-lookup"><span data-stu-id="43293-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="43293-476">Les littéraux décimaux sont représentés à l’aide de la notation décimale, ou de la notation scientifique.</span><span class="sxs-lookup"><span data-stu-id="43293-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="43293-477">Les littéraux hexadécimaux sont représentés à l’aide du préfixe « 0 x », suivi d’un ou plusieurs chiffres hexadécimaux.</span><span class="sxs-lookup"><span data-stu-id="43293-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="43293-478">Représente une constante de type chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="43293-479">Les littéraux de chaîne sont des chaînes Unicode représentées par une séquence de zéro ou plusieurs caractères Unicode ou séquences d’échappement.</span><span class="sxs-lookup"><span data-stu-id="43293-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="43293-480">Les littéraux de chaîne sont placés entre guillemets simples (apostrophes, ’) ou guillemets doubles (").</span><span class="sxs-lookup"><span data-stu-id="43293-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="43293-481">Les séquences d’échappement suivantes sont autorisées :</span><span class="sxs-lookup"><span data-stu-id="43293-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="43293-482">**Séquence d’échappement**</span><span class="sxs-lookup"><span data-stu-id="43293-482">**Escape sequence**</span></span>|<span data-ttu-id="43293-483">**Description**</span><span class="sxs-lookup"><span data-stu-id="43293-483">**Description**</span></span>|<span data-ttu-id="43293-484">**Caractères Unicode**</span><span class="sxs-lookup"><span data-stu-id="43293-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="43293-485">\\'</span><span class="sxs-lookup"><span data-stu-id="43293-485">\\'</span></span>|<span data-ttu-id="43293-486">apostrophe (')</span><span class="sxs-lookup"><span data-stu-id="43293-486">apostrophe (')</span></span>|<span data-ttu-id="43293-487">U+0027</span><span class="sxs-lookup"><span data-stu-id="43293-487">U+0027</span></span>|  
|<span data-ttu-id="43293-488">\\"</span><span class="sxs-lookup"><span data-stu-id="43293-488">\\"</span></span>|<span data-ttu-id="43293-489">guillemet (")</span><span class="sxs-lookup"><span data-stu-id="43293-489">quotation mark (")</span></span>|<span data-ttu-id="43293-490">U+0022</span><span class="sxs-lookup"><span data-stu-id="43293-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="43293-491">barre oblique inversée (\\)</span><span class="sxs-lookup"><span data-stu-id="43293-491">reverse solidus (\\)</span></span>|<span data-ttu-id="43293-492">U+005C</span><span class="sxs-lookup"><span data-stu-id="43293-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="43293-493">barre oblique (/)</span><span class="sxs-lookup"><span data-stu-id="43293-493">solidus (/)</span></span>|<span data-ttu-id="43293-494">U+002F</span><span class="sxs-lookup"><span data-stu-id="43293-494">U+002F</span></span>|  
|<span data-ttu-id="43293-495">\b</span><span class="sxs-lookup"><span data-stu-id="43293-495">\b</span></span>|<span data-ttu-id="43293-496">retour arrière</span><span class="sxs-lookup"><span data-stu-id="43293-496">backspace</span></span>|<span data-ttu-id="43293-497">U+0008</span><span class="sxs-lookup"><span data-stu-id="43293-497">U+0008</span></span>|  
|<span data-ttu-id="43293-498">\f</span><span class="sxs-lookup"><span data-stu-id="43293-498">\f</span></span>|<span data-ttu-id="43293-499">saut de page</span><span class="sxs-lookup"><span data-stu-id="43293-499">form feed</span></span>|<span data-ttu-id="43293-500">U+000C</span><span class="sxs-lookup"><span data-stu-id="43293-500">U+000C</span></span>|  
|\n|<span data-ttu-id="43293-501">saut de ligne</span><span class="sxs-lookup"><span data-stu-id="43293-501">line feed</span></span>|<span data-ttu-id="43293-502">U+000A</span><span class="sxs-lookup"><span data-stu-id="43293-502">U+000A</span></span>|  
|<span data-ttu-id="43293-503">\r</span><span class="sxs-lookup"><span data-stu-id="43293-503">\r</span></span>|<span data-ttu-id="43293-504">retour chariot</span><span class="sxs-lookup"><span data-stu-id="43293-504">carriage return</span></span>|<span data-ttu-id="43293-505">U+000D</span><span class="sxs-lookup"><span data-stu-id="43293-505">U+000D</span></span>|  
|<span data-ttu-id="43293-506">\t</span><span class="sxs-lookup"><span data-stu-id="43293-506">\t</span></span>|<span data-ttu-id="43293-507">tab</span><span class="sxs-lookup"><span data-stu-id="43293-507">tab</span></span>|<span data-ttu-id="43293-508">U+0009</span><span class="sxs-lookup"><span data-stu-id="43293-508">U+0009</span></span>|  
|<span data-ttu-id="43293-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="43293-509">\uXXXX</span></span>|<span data-ttu-id="43293-510">Un caractère Unicode défini par 4 chiffres hexadécimaux.</span><span class="sxs-lookup"><span data-stu-id="43293-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="43293-511">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="43293-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="43293-512"><a name="bk_query_perf_guidelines"></a> Instructions relatives aux performances de requête</span><span class="sxs-lookup"><span data-stu-id="43293-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="43293-513">Dans l’ordre pour un toobe de requête exécutée efficacement pour une grande collection, elle doit utiliser des filtres qui peuvent être servis via un ou plusieurs index.</span><span class="sxs-lookup"><span data-stu-id="43293-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="43293-514">Hello, suivant les filtres est considéré comme pour la recherche d’index :</span><span class="sxs-lookup"><span data-stu-id="43293-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="43293-515">Utilisez l’opérateur d’égalité (=) avec une expression de chemin d’accès de document et une constante.</span><span class="sxs-lookup"><span data-stu-id="43293-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="43293-516">Utilisez les opérateurs de plage (<, \<=, >, > =) avec une expression de chemin d’accès de document et des constantes numériques.</span><span class="sxs-lookup"><span data-stu-id="43293-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="43293-517">Expression de chemin d’accès de document remplace toute expression qui identifie un chemin d’accès constant dans les documents hello à partir de la collection de base de données hello référencé.</span><span class="sxs-lookup"><span data-stu-id="43293-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="43293-518">**Expression de chemin d’accès à un document**</span><span class="sxs-lookup"><span data-stu-id="43293-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="43293-519">Les expressions de chemin d’accès à un document sont des expressions qu’un chemin d’accès de propriété ou indexeur de tableau évalue sur un document provenant des documents de la collecte de base de données.</span><span class="sxs-lookup"><span data-stu-id="43293-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="43293-520">Ce chemin d’accès peut être emplacement de hello tooidentify utilisées de valeurs référencées dans un filtre directement dans des documents dans la collection de base de données hello hello.</span><span class="sxs-lookup"><span data-stu-id="43293-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="43293-521">Pour une expression toobe considérée comme une expression de chemin d’accès de document, il doit :</span><span class="sxs-lookup"><span data-stu-id="43293-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="43293-522">Référence hello racine de la collection directement.</span><span class="sxs-lookup"><span data-stu-id="43293-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="43293-523">Référencer la propriété ou l’indexeur de tableau de constantes d’une expression de chemin d’accès de document</span><span class="sxs-lookup"><span data-stu-id="43293-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="43293-524">Faire référence à un alias, qui représente une expression de chemin d’accès de document.</span><span class="sxs-lookup"><span data-stu-id="43293-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="43293-525">**Conventions de syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="43293-526">Hello tableau suivant décrit la syntaxe de toodescribe hello conventions utilisées dans la référence du langage de requête API DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="43293-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="43293-527">**Convention**</span><span class="sxs-lookup"><span data-stu-id="43293-527">**Convention**</span></span>|<span data-ttu-id="43293-528">**Utilisé pour**</span><span class="sxs-lookup"><span data-stu-id="43293-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="43293-529">MAJUSCULES</span><span class="sxs-lookup"><span data-stu-id="43293-529">UPPERCASE</span></span>|<span data-ttu-id="43293-530">Mots-clés non sensibles à la casse.</span><span class="sxs-lookup"><span data-stu-id="43293-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="43293-531">minuscules</span><span class="sxs-lookup"><span data-stu-id="43293-531">lowercase</span></span>|<span data-ttu-id="43293-532">Mots-clés sensibles à la casse.</span><span class="sxs-lookup"><span data-stu-id="43293-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="43293-533">\<nonterminal&gt;</span><span class="sxs-lookup"><span data-stu-id="43293-533">\<nonterminal></span></span>|<span data-ttu-id="43293-534">Non terminal, défini séparément.</span><span class="sxs-lookup"><span data-stu-id="43293-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="43293-535">\<nonterminal&gt; ::=</span><span class="sxs-lookup"><span data-stu-id="43293-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="43293-536">Définition de la syntaxe de l’élément non terminal hello.</span><span class="sxs-lookup"><span data-stu-id="43293-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="43293-537">other_terminal</span><span class="sxs-lookup"><span data-stu-id="43293-537">other_terminal</span></span>|<span data-ttu-id="43293-538">Terminal (jeton), décrit en détail par des mots.</span><span class="sxs-lookup"><span data-stu-id="43293-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="43293-539">identificateur</span><span class="sxs-lookup"><span data-stu-id="43293-539">identifier</span></span>|<span data-ttu-id="43293-540">Identificateur.</span><span class="sxs-lookup"><span data-stu-id="43293-540">Identifier.</span></span> <span data-ttu-id="43293-541">Autorise uniquement les caractères suivants : a-z A-Z 0-9 _ Le premier caractère ne peut pas être un chiffre.</span><span class="sxs-lookup"><span data-stu-id="43293-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="43293-542">"chaîne"</span><span class="sxs-lookup"><span data-stu-id="43293-542">"string"</span></span>|<span data-ttu-id="43293-543">Chaîne entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="43293-543">Quoted string.</span></span> <span data-ttu-id="43293-544">Autorise n’importe quelle chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-544">Allows any valid string.</span></span> <span data-ttu-id="43293-545">Consultez la description de string_literal.</span><span class="sxs-lookup"><span data-stu-id="43293-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="43293-546">'symbole'</span><span class="sxs-lookup"><span data-stu-id="43293-546">'symbol'</span></span>|<span data-ttu-id="43293-547">Symbole littéral qui fait partie de la syntaxe de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="43293-548">&#124; (barre verticale)</span><span class="sxs-lookup"><span data-stu-id="43293-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="43293-549">Alternatives aux éléments de syntaxe.</span><span class="sxs-lookup"><span data-stu-id="43293-549">Alternatives for syntax items.</span></span> <span data-ttu-id="43293-550">Vous pouvez utiliser uniquement un des éléments de hello spécifiés.</span><span class="sxs-lookup"><span data-stu-id="43293-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="43293-551">[ ] /(crochets)</span><span class="sxs-lookup"><span data-stu-id="43293-551">[ ] /(brackets)</span></span>|<span data-ttu-id="43293-552">Les crochets entourent un ou plusieurs éléments facultatifs.</span><span class="sxs-lookup"><span data-stu-id="43293-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="43293-553">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="43293-553">[ ,...n ]</span></span>|<span data-ttu-id="43293-554">Indique hello précédant l’élément peut être répété n fois.</span><span class="sxs-lookup"><span data-stu-id="43293-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="43293-555">occurrences de Hello sont séparées par des virgules.</span><span class="sxs-lookup"><span data-stu-id="43293-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="43293-556">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="43293-556">[ ...n ]</span></span>|<span data-ttu-id="43293-557">Indique hello précédant l’élément peut être répété n fois.</span><span class="sxs-lookup"><span data-stu-id="43293-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="43293-558">occurrences de Hello sont séparées par des espaces.</span><span class="sxs-lookup"><span data-stu-id="43293-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="43293-559"><a name="bk_built_in_functions"></a> Fonctions intégrées</span><span class="sxs-lookup"><span data-stu-id="43293-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="43293-560">Azure Cosmos DB fournit de nombreuses fonctions SQL intégrées.</span><span class="sxs-lookup"><span data-stu-id="43293-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="43293-561">catégories de Hello de fonctions intégrées sont répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="43293-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="43293-562">Fonction</span><span class="sxs-lookup"><span data-stu-id="43293-562">Function</span></span>|<span data-ttu-id="43293-563">Description</span><span class="sxs-lookup"><span data-stu-id="43293-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="43293-564">Fonctions mathématiques</span><span class="sxs-lookup"><span data-stu-id="43293-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="43293-565">fonctions mathématiques Hello chaque effectuent un calcul, généralement basé sur des valeurs d’entrée qui sont fournies en tant qu’arguments et retournent une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="43293-566">Fonctions de vérification du type</span><span class="sxs-lookup"><span data-stu-id="43293-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="43293-567">les fonctions de vérification de type Hello vous autorisent toocheck hello ce type d’une expression dans des requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="43293-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="43293-568">Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="43293-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="43293-569">fonctions de chaîne Hello effectuent une opération sur une valeur de chaîne d’entrée et retournent une valeur numérique ou booléenne, une chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="43293-570">Fonctions de tableau</span><span class="sxs-lookup"><span data-stu-id="43293-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="43293-571">fonctions de tableau Hello effectuent une opération sur une valeur d’entrée de tableau et de retour numérique, une valeur booléenne ou de tableau.</span><span class="sxs-lookup"><span data-stu-id="43293-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="43293-572">Fonctions spatiales</span><span class="sxs-lookup"><span data-stu-id="43293-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="43293-573">les fonctions spatiales Hello effectuent une opération sur une valeur d’entrée d’objet spatial et retournent une valeur numérique ou booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="43293-574"><a name="bk_mathematical_functions"></a> Fonctions mathématiques</span><span class="sxs-lookup"><span data-stu-id="43293-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="43293-575">Hello fonctions mathématiques suivantes effectuent un calcul, généralement basé sur des valeurs d’entrée qui sont fournies en tant qu’arguments et retournent une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="43293-576">ABS</span><span class="sxs-lookup"><span data-stu-id="43293-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="43293-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="43293-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="43293-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="43293-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="43293-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="43293-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="43293-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="43293-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="43293-581">CEILING</span><span class="sxs-lookup"><span data-stu-id="43293-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="43293-582">COS</span><span class="sxs-lookup"><span data-stu-id="43293-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="43293-583">COT</span><span class="sxs-lookup"><span data-stu-id="43293-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="43293-584">DEGREES</span><span class="sxs-lookup"><span data-stu-id="43293-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="43293-585">EXP</span><span class="sxs-lookup"><span data-stu-id="43293-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="43293-586">FLOOR</span><span class="sxs-lookup"><span data-stu-id="43293-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="43293-587">LOG</span><span class="sxs-lookup"><span data-stu-id="43293-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="43293-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="43293-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="43293-589">PI</span><span class="sxs-lookup"><span data-stu-id="43293-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="43293-590">POWER</span><span class="sxs-lookup"><span data-stu-id="43293-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="43293-591">RADIANS</span><span class="sxs-lookup"><span data-stu-id="43293-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="43293-592">ROUND</span><span class="sxs-lookup"><span data-stu-id="43293-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="43293-593">SIN</span><span class="sxs-lookup"><span data-stu-id="43293-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="43293-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="43293-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="43293-595">SQUARE</span><span class="sxs-lookup"><span data-stu-id="43293-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="43293-596">SIGN</span><span class="sxs-lookup"><span data-stu-id="43293-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="43293-597">TAN</span><span class="sxs-lookup"><span data-stu-id="43293-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="43293-598">TRUNC</span><span class="sxs-lookup"><span data-stu-id="43293-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="43293-599"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="43293-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="43293-600">Retourne hello valeur absolue (positive) de hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="43293-601">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-602">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-603">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-604">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-604">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-605">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-606">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-606">**Examples**</span></span>  
  
 <span data-ttu-id="43293-607">Hello suivant montre les résultats de hello de l’utilisation de la fonction hello ABS sur trois nombres différents.</span><span class="sxs-lookup"><span data-stu-id="43293-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="43293-608">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="43293-609"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="43293-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="43293-610">Angle de hello retourne, en radians, dont le cosinus est hello expression numérique spécifiée ; également appelé arc cosinus.</span><span class="sxs-lookup"><span data-stu-id="43293-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="43293-611">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-612">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-613">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-614">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-614">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-615">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-616">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-616">**Examples**</span></span>  
  
 <span data-ttu-id="43293-617">Hello exemple ci-dessous retourne hello ACOS de -1.</span><span class="sxs-lookup"><span data-stu-id="43293-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="43293-618">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="43293-619"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="43293-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="43293-620">Angle de hello retourne, en radians, dont le sinus est hello spécifié expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="43293-621">Cette fonction est également appelée arcsinus.</span><span class="sxs-lookup"><span data-stu-id="43293-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="43293-622">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-623">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-624">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-625">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-625">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-626">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-627">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-627">**Examples**</span></span>  
  
 <span data-ttu-id="43293-628">Hello exemple ci-dessous retourne hello ASIN de -1.</span><span class="sxs-lookup"><span data-stu-id="43293-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="43293-629">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="43293-630"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="43293-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="43293-631">Angle de hello retourne, en radians, dont la tangente est hello spécifié expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="43293-632">Cette fonction est également appelée arctangente.</span><span class="sxs-lookup"><span data-stu-id="43293-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="43293-633">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-634">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-635">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-636">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-636">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-637">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-638">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-638">**Examples**</span></span>  
  
 <span data-ttu-id="43293-639">Hello exemple retourne hello ATAN de hello suivant la valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="43293-640">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="43293-641"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="43293-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="43293-642">Retourne la valeur principal hello hello arc tangente de y / x, exprimée en radians.</span><span class="sxs-lookup"><span data-stu-id="43293-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="43293-643">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="43293-644">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-645">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-646">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-646">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-647">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-648">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-648">**Examples**</span></span>  
  
 <span data-ttu-id="43293-649">exemple Hello calcule hello ATN2 pour hello spécifié x et y des composants.</span><span class="sxs-lookup"><span data-stu-id="43293-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="43293-650">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="43293-651"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="43293-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="43293-652">Retourne hello plus petit entier supérieur à, ou être égal, hello expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="43293-653">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-654">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-655">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-656">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-656">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-657">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-658">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-658">**Examples**</span></span>  
  
 <span data-ttu-id="43293-659">Hello l’exemple suivant montre numériques positives, négatives, et les valeurs zéro avec hello fonction CEILING.</span><span class="sxs-lookup"><span data-stu-id="43293-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="43293-660">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="43293-661"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="43293-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="43293-662">Cosinus trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="43293-663">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-664">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-665">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-666">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-666">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-667">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-668">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-668">**Examples**</span></span>  
  
 <span data-ttu-id="43293-669">Bonjour à l’exemple suivant calcule hello COS de hello spécifié angle.</span><span class="sxs-lookup"><span data-stu-id="43293-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="43293-670">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="43293-671"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="43293-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="43293-672">Cotangente trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="43293-673">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-674">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-675">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-676">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-676">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-677">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-678">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-678">**Examples**</span></span>  
  
 <span data-ttu-id="43293-679">Bonjour à l’exemple suivant calcule hello COT de l’angle spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="43293-680">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="43293-681"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="43293-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="43293-682">Retourne hello angle correspondant en degrés pour un angle spécifié en radians.</span><span class="sxs-lookup"><span data-stu-id="43293-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="43293-683">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-684">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-685">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-686">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-686">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-687">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-688">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-688">**Examples**</span></span>  
  
 <span data-ttu-id="43293-689">Hello exemple suivant retourne hello nombre de degrés d’un angle de PI/2 radians.</span><span class="sxs-lookup"><span data-stu-id="43293-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="43293-690">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="43293-691"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="43293-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="43293-692">Retourne des hello plus grand entier inférieur ou égal toohello l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="43293-693">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-694">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-695">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-696">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-696">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-697">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-698">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-698">**Examples**</span></span>  
  
 <span data-ttu-id="43293-699">Hello, l’exemple suivant montre numériques positives, négatives, et les valeurs zéro avec hello FLOOR (fonction).</span><span class="sxs-lookup"><span data-stu-id="43293-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="43293-700">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="43293-701"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="43293-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="43293-702">Hello retourne la valeur exponentielle de hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="43293-703">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-704">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-705">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-706">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-706">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-707">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-708">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="43293-708">**Remarks**</span></span>  
  
 <span data-ttu-id="43293-709">constante de Hello **e** (2,718281...), est hello base des logarithmes naturels.</span><span class="sxs-lookup"><span data-stu-id="43293-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="43293-710">constante de hello est Hello exposant d’un nombre **e** déclenché toohello puissance hello.</span><span class="sxs-lookup"><span data-stu-id="43293-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="43293-711">Par exemple EXP(1.0) = e ^ 1,0 = 2,71828182845905 et EXP(10) = e ^ 10 = 22026,4657948067.</span><span class="sxs-lookup"><span data-stu-id="43293-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="43293-712">Hello valeur exponentielle du logarithme naturel de hello d’un nombre est le nombre hello lui-même : EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="43293-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="43293-713">Et hello logarithme népérien de hello exponentielle d’un nombre est nombre hello lui-même : EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="43293-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="43293-714">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-714">**Examples**</span></span>  
  
 <span data-ttu-id="43293-715">Hello exemple suivant déclare une variable et renvoie la valeur exponentielle de hello de hello (10).</span><span class="sxs-lookup"><span data-stu-id="43293-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="43293-716">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="43293-717">Hello exemple suivant renvoie hello valeur exponentielle du logarithme naturel de hello de 20 et le logarithme népérien de hello Hello exponentielle de 20.</span><span class="sxs-lookup"><span data-stu-id="43293-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="43293-718">Étant donné que ces fonctions sont l’inverse d’une autre, hello valeur renvoyée pour les opérations mathématiques dans les deux cas est de 20 de virgule flottante.</span><span class="sxs-lookup"><span data-stu-id="43293-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="43293-719">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="43293-720"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="43293-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="43293-721">Népérien retourne hello Hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="43293-722">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="43293-723">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-724">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="43293-725">Argument numérique facultatif qui définit hello base logarithme de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="43293-726">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-726">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-727">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-728">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="43293-728">**Remarks**</span></span>  
  
 <span data-ttu-id="43293-729">Par défaut, LOG() renvoie le logarithme népérien de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="43293-730">Vous pouvez modifier la base hello de valeur de hello logarithme tooanother à l’aide du paramètre de base facultatif hello.</span><span class="sxs-lookup"><span data-stu-id="43293-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="43293-731">Logarithme népérien de Hello est hello toohello de logarithme base **e**, où **e** est un too2.718281828 approximativement égale constante irrationnelle.</span><span class="sxs-lookup"><span data-stu-id="43293-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="43293-732">Logarithme népérien de Hello Hello exponentielle d’un nombre est nombre hello lui-même : EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="43293-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="43293-733">Et hello valeur exponentielle du logarithme naturel de hello d’un nombre est le nombre hello lui-même : EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="43293-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="43293-734">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-734">**Examples**</span></span>  
  
 <span data-ttu-id="43293-735">Hello exemple suivant déclare une variable et retourne la valeur du logarithme hello de hello (10).</span><span class="sxs-lookup"><span data-stu-id="43293-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="43293-736">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="43293-737">Hello exemple suivant calcule hello journal exposant hello d’un nombre.</span><span class="sxs-lookup"><span data-stu-id="43293-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="43293-738">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="43293-739"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="43293-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="43293-740">Logarithme de base 10 retourne hello Hello spécifié expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="43293-741">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-742">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-743">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-744">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-744">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-745">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-746">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="43293-746">**Remarks**</span></span>  
  
 <span data-ttu-id="43293-747">Hello LOG10 et fonctions de puissance sont inversement connexe tooone une autre.</span><span class="sxs-lookup"><span data-stu-id="43293-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="43293-748">Par exemple, 10 ^ LOG10 (n) = n.</span><span class="sxs-lookup"><span data-stu-id="43293-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="43293-749">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-749">**Examples**</span></span>  
  
 <span data-ttu-id="43293-750">Hello exemple suivant déclare une variable et renvoie la valeur LOG10 de hello de variable spécifié de hello (100).</span><span class="sxs-lookup"><span data-stu-id="43293-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="43293-751">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="43293-752"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="43293-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="43293-753">Retourne hello valeur constante de PI.</span><span class="sxs-lookup"><span data-stu-id="43293-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="43293-754">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="43293-755">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-756">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-757">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-757">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-758">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-759">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-759">**Examples**</span></span>  
  
 <span data-ttu-id="43293-760">Hello suivant l’exemple hello retourne la valeur de PI.</span><span class="sxs-lookup"><span data-stu-id="43293-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="43293-761">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="43293-762"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="43293-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="43293-763">Retourne hello valeur Hello spécifié expression toohello de puissance spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="43293-764">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="43293-765">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-766">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="43293-767">Est hello power toowhich tooraise `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="43293-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="43293-768">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-768">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-769">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-770">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-770">**Examples**</span></span>  
  
 <span data-ttu-id="43293-771">Bonjour à l’exemple suivant montre le déclenchement d’une nombre toohello puissance 3 (cube hello du nombre de hello).</span><span class="sxs-lookup"><span data-stu-id="43293-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="43293-772">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="43293-773"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="43293-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="43293-774">Retourne des radians lorsqu’une expression numérique, en degrés, est entrée.</span><span class="sxs-lookup"><span data-stu-id="43293-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="43293-775">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-776">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-777">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-778">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-778">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-779">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-780">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-780">**Examples**</span></span>  
  
 <span data-ttu-id="43293-781">Hello exemple suivant utilise plusieurs angles comme entrée et retourne leurs valeurs en radians correspondant.</span><span class="sxs-lookup"><span data-stu-id="43293-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="43293-782">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="43293-783"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="43293-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="43293-784">Retourne une valeur numérique, arrondie toohello nombre entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="43293-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="43293-785">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-786">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-787">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-788">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-788">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-789">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-790">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-790">**Examples**</span></span>  
  
 <span data-ttu-id="43293-791">Hello exemple suivant arrondit hello suivant toohello de nombres positifs et négatifs entière la plus proche.</span><span class="sxs-lookup"><span data-stu-id="43293-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="43293-792">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="43293-793"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="43293-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="43293-794">Retourne hello positif (+ 1), zéro (0), ou un signe négatif (-1) de hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="43293-795">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-796">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-797">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-798">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-798">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-799">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-800">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-800">**Examples**</span></span>  
  
 <span data-ttu-id="43293-801">Hello exemple suivant retourne les valeurs hello signe des nombres de-2 too2.</span><span class="sxs-lookup"><span data-stu-id="43293-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="43293-802">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="43293-803"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="43293-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="43293-804">Sinus trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="43293-805">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-806">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-807">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-808">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-808">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-809">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-810">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-810">**Examples**</span></span>  
  
 <span data-ttu-id="43293-811">Bonjour à l’exemple suivant calcule hello SIN de l’angle spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="43293-812">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="43293-813"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="43293-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="43293-814">Racine carrée retourne hello hello la valeur numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="43293-815">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-816">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-817">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-818">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-818">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-819">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-820">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-820">**Examples**</span></span>  
  
 <span data-ttu-id="43293-821">Hello exemple ci-dessous retourne racines carrées de hello de 1 à 3.</span><span class="sxs-lookup"><span data-stu-id="43293-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="43293-822">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="43293-823"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="43293-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="43293-824">Hello retourne carrée hello la valeur numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="43293-825">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-826">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-827">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-828">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-828">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-829">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-830">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-830">**Examples**</span></span>  
  
 <span data-ttu-id="43293-831">Hello exemple suivant renvoie les carrés hello de 1 à 3.</span><span class="sxs-lookup"><span data-stu-id="43293-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="43293-832">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="43293-833"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="43293-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="43293-834">Tangente de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="43293-835">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-836">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-837">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-838">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-838">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-839">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-840">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-840">**Examples**</span></span>  
  
 <span data-ttu-id="43293-841">Hello exemple suivant calcule la tangente de PI () hello / 2.</span><span class="sxs-lookup"><span data-stu-id="43293-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="43293-842">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="43293-843"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="43293-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="43293-844">Retourne une valeur numérique, tronquée toohello nombre entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="43293-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="43293-845">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="43293-846">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="43293-847">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-848">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-848">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-849">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-850">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-850">**Examples**</span></span>  
  
 <span data-ttu-id="43293-851">Bonjour à l’exemple suivant tronque hello suivant toohello de nombres positifs et négatifs plus proche de la valeur entière.</span><span class="sxs-lookup"><span data-stu-id="43293-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="43293-852">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="43293-853"><a name="bk_type_checking_functions"></a> Fonctions de vérification du type</span><span class="sxs-lookup"><span data-stu-id="43293-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="43293-854">Hello fonctions suivantes prennent en charge de vérification par rapport aux valeurs d’entrée de type, et renvoient une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="43293-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="43293-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="43293-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="43293-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="43293-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="43293-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="43293-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="43293-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="43293-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="43293-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="43293-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="43293-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="43293-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="43293-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="43293-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="43293-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="43293-863"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="43293-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="43293-864">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un tableau.</span><span class="sxs-lookup"><span data-stu-id="43293-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="43293-865">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="43293-866">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="43293-867">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="43293-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="43293-868">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-868">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-869">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-870">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-870">**Examples**</span></span>  
  
 <span data-ttu-id="43293-871">Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_ARRAY de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="43293-872">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="43293-873"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="43293-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="43293-874">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="43293-875">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="43293-876">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="43293-877">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="43293-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="43293-878">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-878">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-879">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-880">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-880">**Examples**</span></span>  
  
 <span data-ttu-id="43293-881">Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_BOOL de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="43293-882">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="43293-883"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="43293-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="43293-884">Retourne une valeur booléenne indiquant si une valeur a été assignée à la propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="43293-885">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="43293-886">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="43293-887">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="43293-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="43293-888">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-888">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-889">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-890">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-890">**Examples**</span></span>  
  
 <span data-ttu-id="43293-891">Hello contrôles exemple présence hello d’une propriété dans hello spécifié document JSON.</span><span class="sxs-lookup"><span data-stu-id="43293-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="43293-892">tout d’abord Hello retourne true, car « a » est présent, mais hello deuxième retourne la valeur false, car « b » est absent.</span><span class="sxs-lookup"><span data-stu-id="43293-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="43293-893">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="43293-894"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="43293-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="43293-895">Retourne une valeur booléenne indiquant si le type hello Hello spécifié expression est null.</span><span class="sxs-lookup"><span data-stu-id="43293-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="43293-896">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="43293-897">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="43293-898">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="43293-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="43293-899">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-899">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-900">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-901">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-901">**Examples**</span></span>  
  
 <span data-ttu-id="43293-902">Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_NULL de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="43293-903">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="43293-904"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="43293-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="43293-905">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un nombre.</span><span class="sxs-lookup"><span data-stu-id="43293-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="43293-906">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="43293-907">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="43293-908">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="43293-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="43293-909">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-909">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-910">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-911">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-911">**Examples**</span></span>  
  
 <span data-ttu-id="43293-912">Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_NULL de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="43293-913">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="43293-914"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="43293-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="43293-915">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="43293-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="43293-916">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="43293-917">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="43293-918">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="43293-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="43293-919">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-919">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-920">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-921">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-921">**Examples**</span></span>  
  
 <span data-ttu-id="43293-922">Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_OBJECT de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="43293-923">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="43293-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="43293-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="43293-925">Retourne une valeur booléenne indiquant si le type hello Hello spécifié expression est un type primitif (chaîne, booléen, numérique ou null).</span><span class="sxs-lookup"><span data-stu-id="43293-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="43293-926">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="43293-927">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="43293-928">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="43293-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="43293-929">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-929">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-930">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-931">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-931">**Examples**</span></span>  
  
 <span data-ttu-id="43293-932">Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_PRIMITIVE de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="43293-933">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="43293-934"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="43293-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="43293-935">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est une chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="43293-936">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="43293-937">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="43293-938">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="43293-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="43293-939">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-939">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-940">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-941">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-941">**Examples**</span></span>  
  
 <span data-ttu-id="43293-942">Hello exemple suivant vérifie les objets JSON booléen, nombre, chaîne, null, objet, tableau et les types non définis à l’aide de la fonction IS_STRING de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="43293-943">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="43293-944"><a name="bk_string_functions"></a> Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="43293-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="43293-945">Bonjour fonctions scalaires suivantes effectuent une opération sur une valeur de chaîne d’entrée et retournent une valeur numérique ou booléenne, une chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="43293-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="43293-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="43293-947">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="43293-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="43293-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="43293-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="43293-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="43293-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="43293-950">LEFT</span><span class="sxs-lookup"><span data-stu-id="43293-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="43293-951">LENGTH</span><span class="sxs-lookup"><span data-stu-id="43293-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="43293-952">LOWER</span><span class="sxs-lookup"><span data-stu-id="43293-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="43293-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="43293-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="43293-954">REPLACE</span><span class="sxs-lookup"><span data-stu-id="43293-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="43293-955">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="43293-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="43293-956">REVERSE</span><span class="sxs-lookup"><span data-stu-id="43293-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="43293-957">RIGHT</span><span class="sxs-lookup"><span data-stu-id="43293-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="43293-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="43293-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="43293-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="43293-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="43293-960">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="43293-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="43293-961">UPPER</span><span class="sxs-lookup"><span data-stu-id="43293-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="43293-962"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="43293-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="43293-963">Retourne une chaîne qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="43293-964">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="43293-965">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-966">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-967">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-967">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-968">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-969">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-969">**Examples**</span></span>  
  
 <span data-ttu-id="43293-970">Hello suivant l’exemple retourne la chaîne hello concaténé de hello les valeurs spécifiées.</span><span class="sxs-lookup"><span data-stu-id="43293-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="43293-971">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="43293-972"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="43293-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="43293-973">Retourne une valeur booléenne qui indique si le première expression de chaîne hello contient hello ensuite.</span><span class="sxs-lookup"><span data-stu-id="43293-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="43293-974">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="43293-975">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-976">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-977">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-977">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-978">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-979">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-979">**Examples**</span></span>  
  
 <span data-ttu-id="43293-980">Hello exemple suivant vérifie si « abc » contient « ab » contient « d ».</span><span class="sxs-lookup"><span data-stu-id="43293-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="43293-981">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="43293-982"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="43293-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="43293-983">Retourne une valeur booléenne indiquant si les première expression de chaîne hello se termine ensuite par hello.</span><span class="sxs-lookup"><span data-stu-id="43293-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="43293-984">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="43293-985">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-986">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-987">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-987">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-988">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-989">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-989">**Examples**</span></span>  
  
 <span data-ttu-id="43293-990">Hello exemple ci-dessous retourne hello « abc » se termine par « b » et « bc ».</span><span class="sxs-lookup"><span data-stu-id="43293-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="43293-991">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="43293-992"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="43293-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="43293-993">Retourne hello position de départ des hello première occurrence de hello deuxième expression de chaîne hello première expression de chaîne spécifiée, ou -1 si la chaîne de hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="43293-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="43293-994">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="43293-995">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-996">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-997">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-997">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-998">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-999">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-999">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1000">Hello exemple suivant retourne les index hello de différentes sous-chaînes à l’intérieur de « abc ».</span><span class="sxs-lookup"><span data-stu-id="43293-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="43293-1001">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="43293-1002"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="43293-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="43293-1003">Retourne hello partie gauche d’une chaîne avec hello spécifié de caractères.</span><span class="sxs-lookup"><span data-stu-id="43293-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="43293-1004">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="43293-1005">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1006">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="43293-1007">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="43293-1008">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1009">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1010">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1010">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1011">Hello exemple ci-dessous retourne hello gauche de « abc » pour différentes valeurs de longueur.</span><span class="sxs-lookup"><span data-stu-id="43293-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="43293-1012">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="43293-1013"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="43293-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="43293-1014">Retourne hello nombre de caractères de hello spécifié l’expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="43293-1015">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="43293-1016">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1017">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-1018">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1019">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1020">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1020">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1021">Hello exemple suivant retourne la longueur d’une chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="43293-1022">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="43293-1023"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="43293-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="43293-1024">Retourne une expression de chaîne après la conversion de toolowercase de données de caractères majuscules en caractères.</span><span class="sxs-lookup"><span data-stu-id="43293-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="43293-1025">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="43293-1026">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1027">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-1028">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1029">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1030">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1030">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1031">Hello suivant montre l’exemple de comment toouse inférieur dans une requête.</span><span class="sxs-lookup"><span data-stu-id="43293-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="43293-1032">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="43293-1033"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="43293-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="43293-1034">Retourne une expression de chaîne après avoir supprimé les espaces de début.</span><span class="sxs-lookup"><span data-stu-id="43293-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="43293-1035">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="43293-1036">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1037">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-1038">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1039">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1040">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1040">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1041">Hello suivant montre l’exemple de comment toouse LTRIM à l’intérieur d’une requête.</span><span class="sxs-lookup"><span data-stu-id="43293-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="43293-1042">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="43293-1043"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="43293-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="43293-1044">Remplace toutes les occurrences d’une valeur de chaîne spécifiée par une autre valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="43293-1045">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="43293-1046">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1047">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-1048">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1049">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1050">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1050">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1051">Bonjour à l’exemple suivant montre comment remplacer des toouse dans une requête.</span><span class="sxs-lookup"><span data-stu-id="43293-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="43293-1052">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="43293-1053"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="43293-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="43293-1054">Répète une valeur de chaîne un nombre de fois spécifié.</span><span class="sxs-lookup"><span data-stu-id="43293-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="43293-1055">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="43293-1056">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1057">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="43293-1058">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="43293-1059">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1060">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1061">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1061">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1062">Bonjour à l’exemple suivant montre comment répliquer des toouse dans une requête.</span><span class="sxs-lookup"><span data-stu-id="43293-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="43293-1063">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="43293-1064"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="43293-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="43293-1065">Retourne l’ordre inverse d’une valeur de chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="43293-1066">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="43293-1067">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1068">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-1069">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1070">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1071">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1071">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1072">Bonjour à l’exemple suivant montre comment toouse inverse dans une requête.</span><span class="sxs-lookup"><span data-stu-id="43293-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="43293-1073">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="43293-1074"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="43293-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="43293-1075">Hello retourne à droite dans le cadre d’une chaîne avec hello nombre spécifié de caractères.</span><span class="sxs-lookup"><span data-stu-id="43293-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="43293-1076">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="43293-1077">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1078">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="43293-1079">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="43293-1080">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1081">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1082">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1082">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1083">Hello exemple suivant retourne hello de partie droite de « abc » pour différentes valeurs de longueur.</span><span class="sxs-lookup"><span data-stu-id="43293-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="43293-1084">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="43293-1085"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="43293-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="43293-1086">Retourne une expression de chaîne après avoir supprimé les espaces de fin.</span><span class="sxs-lookup"><span data-stu-id="43293-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="43293-1087">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="43293-1088">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1089">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-1090">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1091">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1092">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1092">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1093">Hello suivant montre l’exemple de comment toouse RTRIM à l’intérieur d’une requête.</span><span class="sxs-lookup"><span data-stu-id="43293-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="43293-1094">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="43293-1095"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="43293-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="43293-1096">Retourne une valeur booléenne indiquant si les première expression de chaîne hello commence par hello ensuite.</span><span class="sxs-lookup"><span data-stu-id="43293-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="43293-1097">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="43293-1098">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1099">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-1100">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1101">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-1102">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1102">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1103">Hello exemple suivant vérifie si hello de chaîne « abc » commence par « b » et « a ».</span><span class="sxs-lookup"><span data-stu-id="43293-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="43293-1104">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="43293-1105"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="43293-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="43293-1106">Retourne dans une expression de chaîne commençant à hello spécifié le caractère de base zéro et continue toohello spécifié longueur, ou à la fin de toohello de chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="43293-1107">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="43293-1108">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1109">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="43293-1110">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="43293-1111">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1112">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1113">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1113">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1114">Hello exemple suivant retourne hello sous-chaîne de « abc » commençant à 1 pour une longueur de 1 caractère.</span><span class="sxs-lookup"><span data-stu-id="43293-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="43293-1115">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="43293-1116"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="43293-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="43293-1117">Retourne une expression de chaîne après la conversion de toouppercase de données de caractères en minuscules.</span><span class="sxs-lookup"><span data-stu-id="43293-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="43293-1118">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="43293-1119">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="43293-1120">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="43293-1121">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1122">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="43293-1123">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1123">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1124">Hello suivant montre l’exemple de comment toouse supérieur dans une requête</span><span class="sxs-lookup"><span data-stu-id="43293-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="43293-1125">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="43293-1126"><a name="bk_array_functions"></a> Fonctions de tableau</span><span class="sxs-lookup"><span data-stu-id="43293-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="43293-1127">Hello suivant des fonctions scalaires effectuent une opération sur une valeur d’entrée de tableau et le retour numérique, la valeur booléenne ou de tableau</span><span class="sxs-lookup"><span data-stu-id="43293-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="43293-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="43293-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="43293-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="43293-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="43293-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="43293-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="43293-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="43293-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="43293-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="43293-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="43293-1133">Retourne un tableau qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de tableau.</span><span class="sxs-lookup"><span data-stu-id="43293-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="43293-1134">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="43293-1135">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="43293-1136">Peut être toute expression de tableau valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="43293-1137">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1138">Retourne une expression de tableau.</span><span class="sxs-lookup"><span data-stu-id="43293-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="43293-1139">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1139">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1140">Bonjour selon exemple comment tooconcatenate deux tableaux.</span><span class="sxs-lookup"><span data-stu-id="43293-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="43293-1141">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="43293-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="43293-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="43293-1143">Retourne une valeur booléenne qui indique si le tableau de hello contient hello valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43293-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="43293-1144">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="43293-1145">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="43293-1146">Peut être toute expression de tableau valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="43293-1147">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="43293-1148">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1149">Retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="43293-1150">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1150">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1151">Bonjour à l’exemple suivant comment toocheck l’appartenance dans un tableau à l’aide de ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="43293-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="43293-1152">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="43293-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="43293-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="43293-1154">Nombre de hello retourne des éléments de hello spécifié expression de tableau.</span><span class="sxs-lookup"><span data-stu-id="43293-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="43293-1155">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="43293-1156">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="43293-1157">Peut être toute expression de tableau valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="43293-1158">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1159">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="43293-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="43293-1160">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1160">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1161">Bonjour selon exemple comment tooget hello longueur d’un tableau à l’aide de ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="43293-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="43293-1162">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="43293-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="43293-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="43293-1164">Retourne une partie d’une expression de tableau.</span><span class="sxs-lookup"><span data-stu-id="43293-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="43293-1165">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="43293-1166">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="43293-1167">Peut être toute expression de tableau valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="43293-1168">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="43293-1169">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1170">Retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="43293-1171">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1171">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1172">Bonjour à l’exemple suivant comment tooget une partie d’un tableau à l’aide de ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="43293-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="43293-1173">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="43293-1174"><a name="bk_spatial_functions"></a> Fonctions spatiales</span><span class="sxs-lookup"><span data-stu-id="43293-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="43293-1175">Bonjour fonctions scalaires suivantes effectuent une opération sur une valeur d’entrée d’objet spatial et retournent une valeur numérique ou booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="43293-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="43293-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="43293-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="43293-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="43293-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="43293-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="43293-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="43293-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="43293-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="43293-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="43293-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="43293-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="43293-1182">Retourne la distance hello entre les expressions LineString, Polygon ou GeoJSON Point hello deux.</span><span class="sxs-lookup"><span data-stu-id="43293-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="43293-1183">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="43293-1184">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="43293-1185">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="43293-1186">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1187">Retourne une expression numérique qui contient la distance hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="43293-1188">Elle est exprimée en mètres pour le système de référence par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="43293-1189">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1189">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1190">Hello suivant montre l’exemple de comment tooreturn tous les documents familles 30 km de hello l’emplacement à l’aide de la fonction intégrée de hello ST_DISTANCE spécifié.</span><span class="sxs-lookup"><span data-stu-id="43293-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="43293-1191">.</span><span class="sxs-lookup"><span data-stu-id="43293-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="43293-1192">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="43293-1193"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="43293-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="43293-1194">Retourne une expression booléenne indiquant si hello GeoJSON l’objet (Point, polygone ou LineString) spécifié dans le premier argument de hello est dans hello GeoJSON (Point, polygone ou LineString) dans le deuxième argument de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="43293-1195">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="43293-1196">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="43293-1197">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="43293-1198">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="43293-1199">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1200">Retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="43293-1201">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1201">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1202">Bonjour à l’exemple suivant montre comment toofind famille tous les documents d’un polygone à l’aide de ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="43293-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="43293-1203">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="43293-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="43293-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="43293-1205">Retourne une expression booléenne indiquant si hello GeoJSON l’objet (Point, polygone ou LineString) spécifié dans le premier argument de hello croise hello GeoJSON (Point, polygone ou LineString) dans le deuxième argument de hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="43293-1206">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="43293-1207">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="43293-1208">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="43293-1209">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="43293-1210">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1211">Retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="43293-1212">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1212">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1213">Hello suivant montre l’exemple de comment toofind toutes les zones croise hello donné polygone.</span><span class="sxs-lookup"><span data-stu-id="43293-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="43293-1214">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="43293-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="43293-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="43293-1216">Retourne une valeur booléenne indiquant si hello spécifiée expression LineString, Polygon ou GeoJSON Point n’est valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="43293-1217">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="43293-1218">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="43293-1219">Est toute expression GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="43293-1220">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1221">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="43293-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="43293-1222">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1222">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1223">Hello suivant montre l’exemple de comment toocheck si un point est valide à l’aide de ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="43293-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="43293-1224">Par exemple, ce point a une valeur de latitude qui n’est pas hello plage de valeurs valide [-90, 90], donc hello requête retourne false.</span><span class="sxs-lookup"><span data-stu-id="43293-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="43293-1225">Pour les polygones, hello GeoJSON spécification requiert que hello dernière paire de coordonnées fourni doit être hello même comme hello les toocreate tout d’abord, une forme fermée.</span><span class="sxs-lookup"><span data-stu-id="43293-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="43293-1226">Les points dans un polygone doivent être spécifiés dans le sens antihoraire.</span><span class="sxs-lookup"><span data-stu-id="43293-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="43293-1227">Un polygone spécifié dans le sens horaire représente inverse hello de région de hello qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="43293-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="43293-1228">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="43293-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="43293-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="43293-1230">Retourne une valeur JSON contenant une valeur booléenne si hello de l’expression LineString, Polygon ou GeoJSON Point spécifiée est valide et si elle est non valide, en outre hello motif en tant que valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="43293-1231">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="43293-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="43293-1232">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="43293-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="43293-1233">Peut être toute expression GeoJSON Point ou Polygon valide.</span><span class="sxs-lookup"><span data-stu-id="43293-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="43293-1234">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="43293-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="43293-1235">Retourne une valeur JSON contenant une valeur booléenne si hello spécifié GeoJSON point ou expression de polygone est valide et si elle est non valide, en outre hello motif en tant que valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="43293-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="43293-1236">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="43293-1236">**Examples**</span></span>  
  
 <span data-ttu-id="43293-1237">Hello, l’exemple suivant la validité toocheck (avec les détails) à l’aide de ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="43293-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="43293-1238">Voici le jeu de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="43293-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="43293-1239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43293-1239">Next steps</span></span>  
 <span data-ttu-id="43293-1240">[Syntaxe SQL et requête SQL pour Azure Cosmos DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="43293-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="43293-1241">Documentation Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="43293-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
