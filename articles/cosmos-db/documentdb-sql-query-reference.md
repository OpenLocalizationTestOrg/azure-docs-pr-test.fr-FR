---
title: 'API DocumentDB Azure Cosmos DB : syntaxe SQL | Microsoft Docs'
description: "Documentation de référence pour le langage de requête API DocumentDB Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 06/13/2017
ms.author: mimig
ms.openlocfilehash: 63b2d20c74df4fd6173994ee1a727594ba8afba3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="abde8-103">API DocumentDB Azure Cosmos DB : référence de syntaxe SQL</span><span class="sxs-lookup"><span data-stu-id="abde8-103">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="abde8-104">L’API DocumentDB Azure Cosmos DB prend en charge l’interrogation de documents à l’aide d’une grammaire familière de type SQL (Structured Query Language) sur des documents JSON hiérarchiques sans nécessiter de schéma explicite ou de création d’index secondaires.</span><span class="sxs-lookup"><span data-stu-id="abde8-104">The Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="abde8-105">Cette rubrique fournit la documentation de référence pour le langage de requête SQL de l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="abde8-105">This topic provides reference documentation for the DocumentDB API SQL query language.</span></span>

<span data-ttu-id="abde8-106">Pour une procédure pas à pas du langage de requête SQL de l’API DocumentDB, consultez [Requêtes SQL pour l’API DocumentDB Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="abde8-106">For a walkthrough of the DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="abde8-107">Nous vous invitons également à visiter le [Query Playground](http://www.documentdb.com/sql/demo), où vous pouvez essayer Azure Cosmos DB et exécuter des requêtes SQL sur notre jeu de données.</span><span class="sxs-lookup"><span data-stu-id="abde8-107">We also invite you to visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="abde8-108">Requête SELECT</span><span class="sxs-lookup"><span data-stu-id="abde8-108">SELECT query</span></span>  
<span data-ttu-id="abde8-109">Récupère les documents JSON à partir de la base de données.</span><span class="sxs-lookup"><span data-stu-id="abde8-109">Retrieves JSON documents from the database.</span></span> <span data-ttu-id="abde8-110">Prend en charge d’évaluation d’expressions, les projections, le filtrage et les jointures.</span><span class="sxs-lookup"><span data-stu-id="abde8-110">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="abde8-111">Les conventions utilisées pour décrire les instructions SELECT sont présentées sous forme de tableau dans la section Conventions de syntaxe.</span><span class="sxs-lookup"><span data-stu-id="abde8-111">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span>  
  
<span data-ttu-id="abde8-112">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-112">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="abde8-113">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-113">**Remarks**</span></span>  
  
 <span data-ttu-id="abde8-114">Pour plus d’informations sur chaque clause, consultez les sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="abde8-114">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="abde8-115">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="abde8-115">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="abde8-116">Clause FROM</span><span class="sxs-lookup"><span data-stu-id="abde8-116">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="abde8-117">Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="abde8-117">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="abde8-118">Clause ORDER BY</span><span class="sxs-lookup"><span data-stu-id="abde8-118">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="abde8-119">Les clauses de l’instruction SELECT doivent être classées comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="abde8-119">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="abde8-120">N’importe laquelle des clauses facultatives peut être omise.</span><span class="sxs-lookup"><span data-stu-id="abde8-120">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="abde8-121">Mais lorsque des clauses facultatives sont utilisées, elles doivent apparaître dans le bon ordre.</span><span class="sxs-lookup"><span data-stu-id="abde8-121">But when optional clauses are used, they must appear in the right order.</span></span>  
  
<span data-ttu-id="abde8-122">**Ordre logique de traitement de l’instruction SELECT**</span><span class="sxs-lookup"><span data-stu-id="abde8-122">**Logical Processing Order of the SELECT statement**</span></span>  
  
<span data-ttu-id="abde8-123">L’ordre dans lequel les clauses sont traitées est le suivant :</span><span class="sxs-lookup"><span data-stu-id="abde8-123">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="abde8-124">Clause FROM</span><span class="sxs-lookup"><span data-stu-id="abde8-124">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="abde8-125">Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="abde8-125">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="abde8-126">Clause ORDER BY</span><span class="sxs-lookup"><span data-stu-id="abde8-126">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="abde8-127">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="abde8-127">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="abde8-128">Notez que cela diffère de l’ordre dans lequel elles apparaissent dans la syntaxe.</span><span class="sxs-lookup"><span data-stu-id="abde8-128">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="abde8-129">Le classement se fait de telle façon que tous les nouveaux symboles introduits par une clause traitée sont visibles et peuvent être utilisés dans des clauses traitées ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="abde8-129">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="abde8-130">Par exemple, les alias déclarés dans une clause FROM sont accessibles dans les clauses WHERE et SELECT.</span><span class="sxs-lookup"><span data-stu-id="abde8-130">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="abde8-131">**Commentaires et espaces blancs**</span><span class="sxs-lookup"><span data-stu-id="abde8-131">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="abde8-132">Tous les espaces blancs qui ne font pas partie d’une chaîne entre guillemets ou d’un identificateur entre guillemets ne font pas partie de la grammaire du langage et sont ignorés lors de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="abde8-132">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="abde8-133">Le langage de requête prend en charge les commentaires de style T-SQL, comme</span><span class="sxs-lookup"><span data-stu-id="abde8-133">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="abde8-134">Instruction SQL `-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="abde8-134">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="abde8-135">Bien que les commentaires et espaces blancs n’ont pas d’importance dans la grammaire, ils doivent être utilisés pour séparer les jetons.</span><span class="sxs-lookup"><span data-stu-id="abde8-135">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="abde8-136">Par exemple : `-1e5` est un jeton à numéro unique, alors que `: – 1 e5` est un jeton moins suivi du chiffre 1 et de l’identificateur e5.</span><span class="sxs-lookup"><span data-stu-id="abde8-136">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="abde8-137"><a name="bk_select_query"></a> Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="abde8-137"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="abde8-138">Les clauses de l’instruction SELECT doivent être classées comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="abde8-138">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="abde8-139">N’importe laquelle des clauses facultatives peut être omise.</span><span class="sxs-lookup"><span data-stu-id="abde8-139">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="abde8-140">Mais lorsque des clauses facultatives sont utilisées, elles doivent apparaître dans le bon ordre.</span><span class="sxs-lookup"><span data-stu-id="abde8-140">But when optional clauses are used, they must appear in the right order.</span></span>  

<span data-ttu-id="abde8-141">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-141">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="abde8-142">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-142">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="abde8-143">Propriétés ou valeur à sélectionner pour le jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="abde8-143">Properties or value to be selected for the result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="abde8-144">Spécifie que la valeur doit être récupérée sans apporter de modifications.</span><span class="sxs-lookup"><span data-stu-id="abde8-144">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="abde8-145">Plus spécifiquement, si la valeur traitée est un objet, toutes les propriétés sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="abde8-145">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="abde8-146">Spécifie la liste des propriétés à récupérer.</span><span class="sxs-lookup"><span data-stu-id="abde8-146">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="abde8-147">Chaque valeur retournée sera un objet avec les propriétés spécifiées.</span><span class="sxs-lookup"><span data-stu-id="abde8-147">Each returned value will be an object with the properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="abde8-148">Spécifie que la valeur JSON doit être récupérée au lieu de l’objet JSON complet.</span><span class="sxs-lookup"><span data-stu-id="abde8-148">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="abde8-149">Cela, contrairement à `<property_list>`, n’encapsule pas la valeur projetée dans un objet.</span><span class="sxs-lookup"><span data-stu-id="abde8-149">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="abde8-150">Expression représentant la valeur à calculer.</span><span class="sxs-lookup"><span data-stu-id="abde8-150">Expression representing the value to be computed.</span></span> <span data-ttu-id="abde8-151">Consultez la section [Expressions scalaires](#bk_scalar_expressions) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="abde8-151">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="abde8-152">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-152">**Remarks**</span></span>  
  
<span data-ttu-id="abde8-153">La syntaxe `SELECT *` est valide uniquement si la clause FROM a déclaré exactement un alias.</span><span class="sxs-lookup"><span data-stu-id="abde8-153">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="abde8-154">`SELECT *` fournit une projection d’identité, ce qui peut être utile si aucune projection n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="abde8-154">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="abde8-155">SELECT * est valide uniquement si la clause FROM est spécifiée et n’a introduit qu’une seule source d’entrée.</span><span class="sxs-lookup"><span data-stu-id="abde8-155">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="abde8-156">Notez que `SELECT <select_list>` et `SELECT *` sont ce qu’on appelle du « sucre syntaxique » et que vous pouvez également les exprimer à l’aide d’instructions SELECT simples, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="abde8-156">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="abde8-157">équivaut à :</span><span class="sxs-lookup"><span data-stu-id="abde8-157">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="abde8-158">équivaut à :</span><span class="sxs-lookup"><span data-stu-id="abde8-158">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="abde8-159">**Voir aussi**</span><span class="sxs-lookup"><span data-stu-id="abde8-159">**See Also**</span></span>  
  
[<span data-ttu-id="abde8-160">Expressions scalaires</span><span class="sxs-lookup"><span data-stu-id="abde8-160">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="abde8-161">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="abde8-161">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="abde8-162"><a name="bk_from_clause"></a> Clause FROM</span><span class="sxs-lookup"><span data-stu-id="abde8-162"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="abde8-163">Spécifie la ou les sources de jointure.</span><span class="sxs-lookup"><span data-stu-id="abde8-163">Specifies the source or joined sources.</span></span> <span data-ttu-id="abde8-164">La clause FROM est facultative.</span><span class="sxs-lookup"><span data-stu-id="abde8-164">The FROM clause is optional.</span></span> <span data-ttu-id="abde8-165">Si elle n’est pas spécifiée, les autres clauses sont exécutées comme si la clause FROM fournissait un document unique.</span><span class="sxs-lookup"><span data-stu-id="abde8-165">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="abde8-166">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-166">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="abde8-167">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-167">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="abde8-168">Spécifie une source de données, avec ou sans alias.</span><span class="sxs-lookup"><span data-stu-id="abde8-168">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="abde8-169">Si aucun alias n’est spécifié, il est déduit à partir de `<collection_expression>` à l’aide des règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="abde8-169">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="abde8-170">Si l’expression est un collection_name, collection_name sera être utilisé en tant qu’alias.</span><span class="sxs-lookup"><span data-stu-id="abde8-170">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="abde8-171">Si l’expression est `<collection_expression>`, puis property_name, alors property_name sera être utilisé en tant qu’alias.</span><span class="sxs-lookup"><span data-stu-id="abde8-171">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="abde8-172">Si l’expression est un collection_name, collection_name sera être utilisé en tant qu’alias.</span><span class="sxs-lookup"><span data-stu-id="abde8-172">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="abde8-173">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="abde8-173">AS `input_alias`</span></span>  
  
<span data-ttu-id="abde8-174">Spécifie que `input_alias` est un ensemble de valeurs renvoyées par l’expression de collection sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="abde8-174">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
<span data-ttu-id="abde8-175">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="abde8-175">`input_alias` IN</span></span>  
  
<span data-ttu-id="abde8-176">Spécifie que `input_alias` doit représenter l’ensemble des valeurs obtenues en effectuant une itération sur tous les éléments de tableau de chaque tableau retourné par l’expression de collection sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="abde8-176">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="abde8-177">Toute valeur retournée par l’expression de collection sous-jacente qui n’est pas un tableau est ignorée.</span><span class="sxs-lookup"><span data-stu-id="abde8-177">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="abde8-178">Spécifie l’expression de collection à utiliser pour récupérer les documents.</span><span class="sxs-lookup"><span data-stu-id="abde8-178">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="abde8-179">Spécifie qu’un document doit être récupéré à partir de la collection par défaut, actuellement connectée.</span><span class="sxs-lookup"><span data-stu-id="abde8-179">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="abde8-180">Spécifie qu’un document doit être récupéré à partir de la collection fournie.</span><span class="sxs-lookup"><span data-stu-id="abde8-180">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="abde8-181">Le nom de la collection doit correspondre au nom de la collection actuellement connectée.</span><span class="sxs-lookup"><span data-stu-id="abde8-181">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="abde8-182">Spécifie que le document doit être récupéré à partir de l’autre source définie par l’alias fourni.</span><span class="sxs-lookup"><span data-stu-id="abde8-182">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="abde8-183">Spécifie que le document doit être récupéré en accédant à la propriété `property_name` ou à l’élément de tableau array_index pour tous les documents récupérés par l’expression de collection spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-183">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="abde8-184">Spécifie que le document doit être récupéré en accédant à la propriété `property_name` ou à l’élément de tableau array_index pour tous les documents récupérés par l’expression de collection spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-184">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="abde8-185">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-185">**Remarks**</span></span>  
  
<span data-ttu-id="abde8-186">Tous les alias fournis ou déduits dans la ou les `<from_source>(` doivent être uniques.</span><span class="sxs-lookup"><span data-stu-id="abde8-186">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="abde8-187">La syntaxe `<collection_expression>.`property_name est identique à `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="abde8-187">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="abde8-188">Toutefois, cette dernière syntaxe peut être utilisée si un nom de propriété contient des caractères hors identificateur.</span><span class="sxs-lookup"><span data-stu-id="abde8-188">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="abde8-189">**Gestion des propriétés manquantes, des éléments de tableau manquants et des valeurs non définies**</span><span class="sxs-lookup"><span data-stu-id="abde8-189">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="abde8-190">Si une expression de collection accède à des propriétés ou éléments de tableau et que la valeur n’existe pas, cette valeur sera ignorée et n’est plus traitée.</span><span class="sxs-lookup"><span data-stu-id="abde8-190">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="abde8-191">**Étendue de contexte d’expression de collection**</span><span class="sxs-lookup"><span data-stu-id="abde8-191">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="abde8-192">Une expression de collection peut avoir une étendue de document ou de collection :</span><span class="sxs-lookup"><span data-stu-id="abde8-192">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="abde8-193">Une expression est étendue à une collection si la source sous-jacente de l’expression de collection est ROOT ou `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="abde8-193">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="abde8-194">Une telle expression représente un ensemble de documents récupérés directement à partir de la collection, et n’est pas dépendante du traitement d’autres expressions de collection.</span><span class="sxs-lookup"><span data-stu-id="abde8-194">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="abde8-195">Une expression est étendue à un document si la source sous-jacente de l’expression de collection est `input_alias`, introduit plus tôt dans la requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-195">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="abde8-196">Une telle expression représente un ensemble de documents obtenus en évaluant l’expression de collection dans l’étendue de chaque document appartenant au jeu associé à la collection avec alias.</span><span class="sxs-lookup"><span data-stu-id="abde8-196">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="abde8-197">Le jeu résultant sera une union de jeux obtenus en évaluant l’expression de collection pour chacun des documents du jeu sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="abde8-197">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
<span data-ttu-id="abde8-198">**Jointures**</span><span class="sxs-lookup"><span data-stu-id="abde8-198">**Joins**</span></span>  
  
<span data-ttu-id="abde8-199">Dans la version actuelle, Azure Cosmos DB prend en charge les jointures internes.</span><span class="sxs-lookup"><span data-stu-id="abde8-199">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="abde8-200">Des fonctionnalités de jointure supplémentaires sont à venir.</span><span class="sxs-lookup"><span data-stu-id="abde8-200">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="abde8-201">Les jointures internes aboutissent à un produit croisé complet des ensembles participants à la jointure.</span><span class="sxs-lookup"><span data-stu-id="abde8-201">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="abde8-202">Le résultat d’une jointure à N voies est un jeu de tuples à N éléments, où chaque valeur dans le tuple est associée à l’alias défini participant à la jointure et est accessible en référençant cet alias dans d’autres clauses.</span><span class="sxs-lookup"><span data-stu-id="abde8-202">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="abde8-203">L’évaluation de la jointure dépend de l’étendue du contexte des jeux qui participent :</span><span class="sxs-lookup"><span data-stu-id="abde8-203">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="abde8-204">Une jointure entre un jeu de collection A et un jeu à étendue de collection B aboutit à un produit croisé de tous les éléments des jeux A et B.</span><span class="sxs-lookup"><span data-stu-id="abde8-204">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="abde8-205">Une jointure entre le jeu A et le jeu à étendue de document B aboutit à une union de tous les jeux obtenus en évaluant le jeu à étendue de document B pour chaque document du jeu A.</span><span class="sxs-lookup"><span data-stu-id="abde8-205">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="abde8-206">Dans la version actuelle, un maximum d’une expression à étendue de collection est pris en charge par le processeur de requêtes.</span><span class="sxs-lookup"><span data-stu-id="abde8-206">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
<span data-ttu-id="abde8-207">**Exemples de jointures :**</span><span class="sxs-lookup"><span data-stu-id="abde8-207">**Examples of joins:**</span></span>  
  
<span data-ttu-id="abde8-208">Examinons la clause FROM suivante : `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="abde8-208">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="abde8-209">Laissez chaque source définir `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="abde8-209">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="abde8-210">La close FROM renvoie un ensemble de N-tuples (un tuple avec N valeurs).</span><span class="sxs-lookup"><span data-stu-id="abde8-210">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="abde8-211">Les valeurs de chaque tuple sont produites par l'itération de tous les alias de la collection sur leurs ensembles respectifs.</span><span class="sxs-lookup"><span data-stu-id="abde8-211">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="abde8-212">*Exemple de JOIN 1, avec 2 sources :*</span><span class="sxs-lookup"><span data-stu-id="abde8-212">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="abde8-213">Laissez `<from_source1>` être étendu à une collection et représenter le jeu {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="abde8-213">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="abde8-214">Laissez `<from_source2>` être étendu à un document référençant input_alias1 et représenter les jeux :</span><span class="sxs-lookup"><span data-stu-id="abde8-214">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="abde8-215">{1, 2} pour `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="abde8-215">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="abde8-216">{3} pour `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="abde8-216">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="abde8-217">{4, 5} pour `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="abde8-217">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="abde8-218">La clause FROM `<from_source1> JOIN <from_source2>` engendre les tuples suivants :</span><span class="sxs-lookup"><span data-stu-id="abde8-218">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="abde8-219">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="abde8-219">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="abde8-220">*Exemple de JOIN 2, avec 3 sources :*</span><span class="sxs-lookup"><span data-stu-id="abde8-220">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="abde8-221">Laissez `<from_source1>` être étendu à une collection et représenter le jeu {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="abde8-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="abde8-222">Laissez `<from_source2>` être étendu à un document référençant input_`input_alias1` et représenter les jeux :</span><span class="sxs-lookup"><span data-stu-id="abde8-222">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="abde8-223">{1, 2} pour `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="abde8-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="abde8-224">{3} pour `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="abde8-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="abde8-225">{4, 5} pour `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="abde8-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="abde8-226">Laissez `<from_source3>` être étendu à un document référençant input_`input_alias2` et représenter les jeux :</span><span class="sxs-lookup"><span data-stu-id="abde8-226">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="abde8-227">{100, 200} pour `input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="abde8-227">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="abde8-228">{300} pour `input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="abde8-228">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="abde8-229">La clause FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` engendre les tuples suivants :</span><span class="sxs-lookup"><span data-stu-id="abde8-229">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="abde8-230">(input_alias1, input_alias2, input_alias3) :</span><span class="sxs-lookup"><span data-stu-id="abde8-230">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="abde8-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="abde8-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="abde8-232">Absence de tuples pour les autres valeurs de `input_alias1`, `input_alias2`, pour lesquelles `<from_source3>` n’a retourné aucune valeur.</span><span class="sxs-lookup"><span data-stu-id="abde8-232">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="abde8-233">*Exemple de JOIN 3, avec 3 sources :*</span><span class="sxs-lookup"><span data-stu-id="abde8-233">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="abde8-234">Laissez <from_source1> être étendu à une collection et représenter le jeu {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="abde8-234">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="abde8-235">Laissez `<from_source1>` être étendu à une collection et représenter le jeu {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="abde8-235">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="abde8-236">Laissez <from_source2> être étendu à un document référençant input_source1 et représenter les jeux :</span><span class="sxs-lookup"><span data-stu-id="abde8-236">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="abde8-237">{1, 2} pour `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="abde8-237">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="abde8-238">{3} pour `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="abde8-238">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="abde8-239">{4, 5} pour `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="abde8-239">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="abde8-240">Laissez `<from_source3>` être étendu à `input_alias1` et représenter les jeux :</span><span class="sxs-lookup"><span data-stu-id="abde8-240">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="abde8-241">{100, 200} pour `input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="abde8-241">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="abde8-242">{300} pour `input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="abde8-242">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="abde8-243">La clause FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` engendre les tuples suivants :</span><span class="sxs-lookup"><span data-stu-id="abde8-243">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="abde8-244">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="abde8-244">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="abde8-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300), (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="abde8-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="abde8-246">Cela a abouti à un produit croisé entre `<from_source2>` et `<from_source3>`, car les deux sont étendus à la même `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="abde8-246">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="abde8-247">Cela a about à 4 (2 x 2) tuples de valeur A, 0 tuple de valeur B (1 x 0) et 2 (2 x 1) tuples de valeur C.</span><span class="sxs-lookup"><span data-stu-id="abde8-247">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="abde8-248">**Voir aussi**</span><span class="sxs-lookup"><span data-stu-id="abde8-248">**See also**</span></span>  
  
 [<span data-ttu-id="abde8-249">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="abde8-249">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="abde8-250"><a name="bk_where_clause"></a> Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="abde8-250"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="abde8-251">Spécifie la condition de recherche pour les documents renvoyés par la requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-251">Specifies the search condition for the documents returned by the query.</span></span>  
  
 <span data-ttu-id="abde8-252">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-252">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="abde8-253">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-253">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="abde8-254">Spécifie la condition à remplir pour les documents à retourner.</span><span class="sxs-lookup"><span data-stu-id="abde8-254">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="abde8-255">Expression représentant la valeur à calculer.</span><span class="sxs-lookup"><span data-stu-id="abde8-255">Expression representing the value to be computed.</span></span> <span data-ttu-id="abde8-256">Consultez la section [Expressions scalaires](#bk_scalar_expressions) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="abde8-256">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="abde8-257">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-257">**Remarks**</span></span>  
  
 <span data-ttu-id="abde8-258">Pour que le document soit retourné, une expression spécifiée en tant que filtre de condition doit correspondre à la valeur true.</span><span class="sxs-lookup"><span data-stu-id="abde8-258">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="abde8-259">Seule la valeur booléenne true satisfait la condition. Les autres valeurs : undefined, null, false, nombre, tableau ou objet ne satisfont pas la condition.</span><span class="sxs-lookup"><span data-stu-id="abde8-259">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <span data-ttu-id="abde8-260"><a name="bk_orderby_clause"></a> Clause ORDER BY</span><span class="sxs-lookup"><span data-stu-id="abde8-260"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="abde8-261">Spécifie l’ordre de tri des résultats retournés par la requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-261">Specifies the sorting order for results returned by the query.</span></span>  
  
 <span data-ttu-id="abde8-262">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-262">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="abde8-263">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-263">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="abde8-264">Spécifie une propriété ou expression sur laquelle trier le jeu de résultats de requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-264">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="abde8-265">Une colonne de tri peut être spécifiée comme un alias de nom ou de la colonne.</span><span class="sxs-lookup"><span data-stu-id="abde8-265">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="abde8-266">Plusieurs colonnes de tri peuvent être spécifiées.</span><span class="sxs-lookup"><span data-stu-id="abde8-266">Multiple sort columns can be specified.</span></span> <span data-ttu-id="abde8-267">Les noms de colonne doivent être uniques.</span><span class="sxs-lookup"><span data-stu-id="abde8-267">Column names must be unique.</span></span> <span data-ttu-id="abde8-268">La séquence des colonnes de tri dans la clause ORDER BY détermine l’organisation du jeu de résultats trié.</span><span class="sxs-lookup"><span data-stu-id="abde8-268">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="abde8-269">Autrement dit, le jeu de résultats est trié par la première propriété, puis cette liste triée est triée par la deuxième propriété, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="abde8-269">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="abde8-270">Les noms de colonnes référencés dans la clause ORDER BY doivent correspondre à une colonne dans la liste de sélection ou à une colonne définie dans une table spécifiée dans la clause FROM sans ambiguïté.</span><span class="sxs-lookup"><span data-stu-id="abde8-270">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="abde8-271">Spécifie une propriété ou expression unique sur laquelle trier le jeu de résultats de requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-271">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="abde8-272">Consultez la section [Expressions scalaires](#bk_scalar_expressions) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="abde8-272">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="abde8-273">Spécifie que les valeurs dans la colonne spécifiée doivent être triées dans l’ordre croissant ou décroissant.</span><span class="sxs-lookup"><span data-stu-id="abde8-273">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="abde8-274">ASC effectue le tri de la valeur la plus basse à la valeur la plus élevée.</span><span class="sxs-lookup"><span data-stu-id="abde8-274">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="abde8-275">DESC effectue le tri de la valeur la plus élevée à la valeur la plus basse.</span><span class="sxs-lookup"><span data-stu-id="abde8-275">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="abde8-276">ASC est l’ordre de tri par défaut.</span><span class="sxs-lookup"><span data-stu-id="abde8-276">ASC is the default sort order.</span></span> <span data-ttu-id="abde8-277">Les valeurs NULL sont traitées comme les valeurs les plus basses possible.</span><span class="sxs-lookup"><span data-stu-id="abde8-277">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="abde8-278">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-278">**Remarks**</span></span>  
  
 <span data-ttu-id="abde8-279">Même si la grammaire de la requête prend en charge plusieurs propriétés Order by, l’exécution de la requête Azure Cosmos DB prend seulement en charge le tri sur une seule propriété et uniquement sur les noms de propriété (autrement dit, pas sur les propriétés calculées).</span><span class="sxs-lookup"><span data-stu-id="abde8-279">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="abde8-280">Le tri requiert également que la stratégie d’indexation comprenne un index de plage pour la propriété et le type spécifiés, avec la précision maximale.</span><span class="sxs-lookup"><span data-stu-id="abde8-280">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="abde8-281">Consultez la documentation sur la stratégie d’indexation pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="abde8-281">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="abde8-282"><a name="bk_scalar_expressions"></a> Expressions scalaires</span><span class="sxs-lookup"><span data-stu-id="abde8-282"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="abde8-283">Une expression scalaire est une combinaison de symboles et d’opérateurs qui peut être évaluée pour obtenir une valeur unique.</span><span class="sxs-lookup"><span data-stu-id="abde8-283">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="abde8-284">Les expressions simples peuvent être des constantes, des références de propriété, des références d’élément de tableau, des références d’alias ou des appels de fonction.</span><span class="sxs-lookup"><span data-stu-id="abde8-284">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="abde8-285">Les expressions simples peuvent être combinées dans des expressions complexes utilisant des opérateurs.</span><span class="sxs-lookup"><span data-stu-id="abde8-285">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="abde8-286">Pour plus d’informations sur les valeurs qu’une expression scalaire peut avoir, consultez la section [constantes](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="abde8-286">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="abde8-287">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-287">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="abde8-288">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-288">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="abde8-289">Représente une valeur constante.</span><span class="sxs-lookup"><span data-stu-id="abde8-289">Represents a constant value.</span></span> <span data-ttu-id="abde8-290">Consultez la section [Constantes](#bk_constants) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="abde8-290">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="abde8-291">Représente une valeur définie par le `input_alias` introduit dans la clause `FROM`.</span><span class="sxs-lookup"><span data-stu-id="abde8-291">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="abde8-292">Cette valeur est assurée de ne pas être **Undefined**, car les valeurs **Undefined** dans l’entrée sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="abde8-292">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="abde8-293">Représente une valeur de la propriété d’un objet.</span><span class="sxs-lookup"><span data-stu-id="abde8-293">Represents a value of the property of an object.</span></span> <span data-ttu-id="abde8-294">Si la propriété n’existe pas ou est référencée sur une valeur qui n’est pas un objet, alors l’expression évaluée présente la valeur **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="abde8-294">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="abde8-295">Représente une valeur de la propriété portant le nom `property_name` ou l’élément de tableau avec l’index `array_index` d’un objet/tableau.</span><span class="sxs-lookup"><span data-stu-id="abde8-295">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="abde8-296">Si la propriété/l’index de tableau n’existe pas ou est référencée sur une valeur qui n’est pas un objet/tableau, alors l’expression évaluée présente la valeur Undefined.</span><span class="sxs-lookup"><span data-stu-id="abde8-296">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="abde8-297">Représente un opérateur appliqué à une valeur unique.</span><span class="sxs-lookup"><span data-stu-id="abde8-297">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="abde8-298">Consultez la section [Opérateurs](#bk_operators) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="abde8-298">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="abde8-299">Représente un opérateur appliqué à deux valeurs.</span><span class="sxs-lookup"><span data-stu-id="abde8-299">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="abde8-300">Consultez la section [Opérateurs](#bk_operators) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="abde8-300">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="abde8-301">Représente une valeur définie par le résultat d’un appel de fonction.</span><span class="sxs-lookup"><span data-stu-id="abde8-301">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="abde8-302">Nom de la fonction scalaire définie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="abde8-302">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="abde8-303">Nom de la fonction scalaire intégrée.</span><span class="sxs-lookup"><span data-stu-id="abde8-303">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="abde8-304">Représente une valeur obtenue en créant un nouvel objet avec les propriétés spécifiées et leurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="abde8-304">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="abde8-305">Représente une valeur obtenue en créant un nouveau tableau avec les valeurs spécifiées en tant qu’éléments</span><span class="sxs-lookup"><span data-stu-id="abde8-305">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="abde8-306">Représente une valeur du nom de paramètre spécifié.</span><span class="sxs-lookup"><span data-stu-id="abde8-306">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="abde8-307">Les noms de paramètre doivent avoir un @ unique comme premier caractère.</span><span class="sxs-lookup"><span data-stu-id="abde8-307">Parameter names must have a single @ as the first character.</span></span>  
  
 <span data-ttu-id="abde8-308">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-308">**Remarks**</span></span>  
  
 <span data-ttu-id="abde8-309">Lors de l’appel à une fonction scalaire intégrée ou définie par l’utilisateur, tous les arguments doivent être définis.</span><span class="sxs-lookup"><span data-stu-id="abde8-309">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="abde8-310">Si un des arguments n’est pas défini, la fonction n’est pas appelée et le résultat est Undefined.</span><span class="sxs-lookup"><span data-stu-id="abde8-310">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="abde8-311">Lorsque vous créez un objet, toute propriété à laquelle est affectée une valeur Undefined est ignorée et n’est pas incluse dans l’objet créé.</span><span class="sxs-lookup"><span data-stu-id="abde8-311">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="abde8-312">Lorsque vous créez un tableau, toute valeur d’élément à laquelle est affectée une valeur **Undefined** est ignorée et n’est pas incluse dans l’objet créé.</span><span class="sxs-lookup"><span data-stu-id="abde8-312">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="abde8-313">Dans ce cas, l’élément défini suivant prend sa place de telle sorte que le tableau créé n’aura pas d’index ignorés.</span><span class="sxs-lookup"><span data-stu-id="abde8-313">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="abde8-314"><a name="bk_operators"></a> Opérateurs</span><span class="sxs-lookup"><span data-stu-id="abde8-314"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="abde8-315">Cette section décrit les opérateurs pris en charge.</span><span class="sxs-lookup"><span data-stu-id="abde8-315">This section describes the supported operators.</span></span> <span data-ttu-id="abde8-316">Chaque opérateur peut être affecté à exactement une catégorie.</span><span class="sxs-lookup"><span data-stu-id="abde8-316">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="abde8-317">Consultez le tableau **Catégories d’opérateurs** ci-dessous pour plus d’informations sur la gestion des valeurs **Undefined**, des exigences de type pour les valeurs d’entrée et la gestion des valeurs sans types correspondants.</span><span class="sxs-lookup"><span data-stu-id="abde8-317">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="abde8-318">**Catégories d’opérateurs :**</span><span class="sxs-lookup"><span data-stu-id="abde8-318">**Operator categories:**</span></span>  
  
|<span data-ttu-id="abde8-319">**Catégorie**</span><span class="sxs-lookup"><span data-stu-id="abde8-319">**Category**</span></span>|<span data-ttu-id="abde8-320">**Détails**</span><span class="sxs-lookup"><span data-stu-id="abde8-320">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="abde8-321">**Opérateurs arithmétiques**</span><span class="sxs-lookup"><span data-stu-id="abde8-321">**arithmetic**</span></span>|<span data-ttu-id="abde8-322">L’opérateur attend des entrées de type nombre.</span><span class="sxs-lookup"><span data-stu-id="abde8-322">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="abde8-323">La sortie est également un nombre.</span><span class="sxs-lookup"><span data-stu-id="abde8-323">Output is also a Number.</span></span> <span data-ttu-id="abde8-324">Si une des entrées est **Undefined** ou d’un type autre qu’un nombre, le résultat est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="abde8-324">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="abde8-325">**Opérateurs au niveau du bit**</span><span class="sxs-lookup"><span data-stu-id="abde8-325">**bitwise**</span></span>|<span data-ttu-id="abde8-326">L’opérateur attend des entrées de type nombre entier 32 bits signé.</span><span class="sxs-lookup"><span data-stu-id="abde8-326">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="abde8-327">La sortie est également un nombre entier signé 32 bits.</span><span class="sxs-lookup"><span data-stu-id="abde8-327">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="abde8-328">Toute valeur non entière est arrondie.</span><span class="sxs-lookup"><span data-stu-id="abde8-328">Any non-integer value will be rounded.</span></span> <span data-ttu-id="abde8-329">Les valeurs positives sont arrondies vers le bas, et les valeurs négatives vers le haut.</span><span class="sxs-lookup"><span data-stu-id="abde8-329">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="abde8-330">Toute valeur qui se trouve en dehors de la plage d’entiers 32 bits sera convertie, en prenant les derniers 32 bits de ses deux notations de complément.</span><span class="sxs-lookup"><span data-stu-id="abde8-330">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="abde8-331">Si une des entrées est **Undefined** ou d’un type autre qu’un nombre, le résultat est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="abde8-331">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="abde8-332">**Remarque :** le comportement ci-dessus est compatible avec le comportement de l’opérateur de niveau de bit de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="abde8-332">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="abde8-333">**Opérateurs logiques**</span><span class="sxs-lookup"><span data-stu-id="abde8-333">**logical**</span></span>|<span data-ttu-id="abde8-334">L’opérateur attend des entrées de type booléen.</span><span class="sxs-lookup"><span data-stu-id="abde8-334">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="abde8-335">La sortie est également une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-335">Output is also a Boolean.</span></span><br /><span data-ttu-id="abde8-336">Si une des entrées est **Undefined** ou d’un type autre qu’un booléen, le résultat est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="abde8-336">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="abde8-337">**Opérateurs de comparaison**</span><span class="sxs-lookup"><span data-stu-id="abde8-337">**comparison**</span></span>|<span data-ttu-id="abde8-338">L’opérateur attend que des entrées du même type et n’étant pas Undefined.</span><span class="sxs-lookup"><span data-stu-id="abde8-338">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="abde8-339">La sortie est une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-339">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="abde8-340">Si une des entrées est **Undefined** ou que les entrées ont des types différents, le résultat est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="abde8-340">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="abde8-341">Consultez le tableau **Classement des valeurs pour comparaison** pour plus de détails sur le classement des valeurs.</span><span class="sxs-lookup"><span data-stu-id="abde8-341">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="abde8-342">**string**</span><span class="sxs-lookup"><span data-stu-id="abde8-342">**string**</span></span>|<span data-ttu-id="abde8-343">L’opérateur attend des entrées de type chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-343">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="abde8-344">La sortie est également une chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-344">Output is also a String.</span></span><br /><span data-ttu-id="abde8-345">Si une des entrées est **Undefined** ou d’un type autre qu’une chaîne, le résultat est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="abde8-345">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="abde8-346">**Opérateurs unaires :**</span><span class="sxs-lookup"><span data-stu-id="abde8-346">**Unary operators:**</span></span>  
  
|<span data-ttu-id="abde8-347">**Name**</span><span class="sxs-lookup"><span data-stu-id="abde8-347">**Name**</span></span>|<span data-ttu-id="abde8-348">**Opérateur**</span><span class="sxs-lookup"><span data-stu-id="abde8-348">**Operator**</span></span>|<span data-ttu-id="abde8-349">**Détails**</span><span class="sxs-lookup"><span data-stu-id="abde8-349">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="abde8-350">**Opérateurs arithmétiques**</span><span class="sxs-lookup"><span data-stu-id="abde8-350">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="abde8-351">Retourne la valeur de nombre.</span><span class="sxs-lookup"><span data-stu-id="abde8-351">Returns the number value.</span></span><br /><br /> <span data-ttu-id="abde8-352">Négation au niveau du bit.</span><span class="sxs-lookup"><span data-stu-id="abde8-352">Bitwise negation.</span></span> <span data-ttu-id="abde8-353">Retourne une valeur numérique avec négation.</span><span class="sxs-lookup"><span data-stu-id="abde8-353">Returns negated number value.</span></span>|  
|<span data-ttu-id="abde8-354">**Opérateurs au niveau du bit**</span><span class="sxs-lookup"><span data-stu-id="abde8-354">**bitwise**</span></span>|~|<span data-ttu-id="abde8-355">Complément d’une valeur.</span><span class="sxs-lookup"><span data-stu-id="abde8-355">Ones' complement.</span></span> <span data-ttu-id="abde8-356">Retourne un complément d’une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-356">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="abde8-357">**Opérateurs logiques**</span><span class="sxs-lookup"><span data-stu-id="abde8-357">**Logical**</span></span>|<span data-ttu-id="abde8-358">**NOT**</span><span class="sxs-lookup"><span data-stu-id="abde8-358">**NOT**</span></span>|<span data-ttu-id="abde8-359">Négation.</span><span class="sxs-lookup"><span data-stu-id="abde8-359">Negation.</span></span> <span data-ttu-id="abde8-360">Retourne une valeur booléenne avec négation.</span><span class="sxs-lookup"><span data-stu-id="abde8-360">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="abde8-361">**Opérateurs binaires :**</span><span class="sxs-lookup"><span data-stu-id="abde8-361">**Binary operators:**</span></span>  
  
|<span data-ttu-id="abde8-362">**Name**</span><span class="sxs-lookup"><span data-stu-id="abde8-362">**Name**</span></span>|<span data-ttu-id="abde8-363">**Opérateur**</span><span class="sxs-lookup"><span data-stu-id="abde8-363">**Operator**</span></span>|<span data-ttu-id="abde8-364">**Détails**</span><span class="sxs-lookup"><span data-stu-id="abde8-364">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="abde8-365">**Opérateurs arithmétiques**</span><span class="sxs-lookup"><span data-stu-id="abde8-365">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="abde8-366">Addition.</span><span class="sxs-lookup"><span data-stu-id="abde8-366">Addition.</span></span><br /><br /> <span data-ttu-id="abde8-367">Soustraction.</span><span class="sxs-lookup"><span data-stu-id="abde8-367">Subtraction.</span></span><br /><br /> <span data-ttu-id="abde8-368">Multiplication.</span><span class="sxs-lookup"><span data-stu-id="abde8-368">Multiplication.</span></span><br /><br /> <span data-ttu-id="abde8-369">Division.</span><span class="sxs-lookup"><span data-stu-id="abde8-369">Division.</span></span><br /><br /> <span data-ttu-id="abde8-370">Modulation.</span><span class="sxs-lookup"><span data-stu-id="abde8-370">Modulation.</span></span>|  
|<span data-ttu-id="abde8-371">**Opérateurs au niveau du bit**</span><span class="sxs-lookup"><span data-stu-id="abde8-371">**bitwise**</span></span>|<span data-ttu-id="abde8-372">&#124;</span><span class="sxs-lookup"><span data-stu-id="abde8-372">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="abde8-373">Opérateur OR au niveau du bit.</span><span class="sxs-lookup"><span data-stu-id="abde8-373">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="abde8-374">Opérateur AND au niveau du bit.</span><span class="sxs-lookup"><span data-stu-id="abde8-374">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="abde8-375">XOR au niveau du bit.</span><span class="sxs-lookup"><span data-stu-id="abde8-375">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="abde8-376">Décalage vers la gauche.</span><span class="sxs-lookup"><span data-stu-id="abde8-376">Left Shift.</span></span><br /><br /> <span data-ttu-id="abde8-377">Décalage vers la droite.</span><span class="sxs-lookup"><span data-stu-id="abde8-377">Right Shift.</span></span><br /><br /> <span data-ttu-id="abde8-378">Décalage vers la droite avec remplissage de zéros.</span><span class="sxs-lookup"><span data-stu-id="abde8-378">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="abde8-379">**Opérateurs logiques**</span><span class="sxs-lookup"><span data-stu-id="abde8-379">**logical**</span></span>|<span data-ttu-id="abde8-380">**AND**</span><span class="sxs-lookup"><span data-stu-id="abde8-380">**AND**</span></span><br /><br /> <span data-ttu-id="abde8-381">**OR**</span><span class="sxs-lookup"><span data-stu-id="abde8-381">**OR**</span></span>|<span data-ttu-id="abde8-382">Conjonction logique.</span><span class="sxs-lookup"><span data-stu-id="abde8-382">Logical conjunction.</span></span> <span data-ttu-id="abde8-383">Retourne **true** si les deux arguments sont **true**, retourne **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-383">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="abde8-384">Conjonction logique.</span><span class="sxs-lookup"><span data-stu-id="abde8-384">Logical conjunction.</span></span> <span data-ttu-id="abde8-385">Retourne **true** si les deux arguments sont **true**, retourne **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-385">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="abde8-386">**Opérateurs de comparaison**</span><span class="sxs-lookup"><span data-stu-id="abde8-386">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="abde8-387">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="abde8-387">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="abde8-388">**??**</span><span class="sxs-lookup"><span data-stu-id="abde8-388">**??**</span></span>|<span data-ttu-id="abde8-389">Égal à.</span><span class="sxs-lookup"><span data-stu-id="abde8-389">Equals.</span></span> <span data-ttu-id="abde8-390">Retourne **true** si les arguments sont égaux, **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-390">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="abde8-391">Non égal à.</span><span class="sxs-lookup"><span data-stu-id="abde8-391">Not equal to.</span></span> <span data-ttu-id="abde8-392">Retourne **true** si les arguments ne sont pas égaux, **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-392">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="abde8-393">Supérieur à.</span><span class="sxs-lookup"><span data-stu-id="abde8-393">Greater Than.</span></span> <span data-ttu-id="abde8-394">Retourne **true** si le premier argument est supérieur au second, **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-394">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="abde8-395">Supérieur ou égal à.</span><span class="sxs-lookup"><span data-stu-id="abde8-395">Greater Than or Equal To.</span></span> <span data-ttu-id="abde8-396">Retourne **true** si le premier argument est supérieur ou égal au second, **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-396">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="abde8-397">Inférieur à.</span><span class="sxs-lookup"><span data-stu-id="abde8-397">Less Than.</span></span> <span data-ttu-id="abde8-398">Retourne **true** si le premier argument est inférieur au second, **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-398">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="abde8-399">Inférieur ou égal à.</span><span class="sxs-lookup"><span data-stu-id="abde8-399">Less Than or Equal To.</span></span> <span data-ttu-id="abde8-400">Retourne **true** si le premier argument est inférieur ou égal au second, **false** dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-400">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="abde8-401">Coalesce.</span><span class="sxs-lookup"><span data-stu-id="abde8-401">Coalesce.</span></span> <span data-ttu-id="abde8-402">Retourne le deuxième argument si le premier argument est une valeur **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="abde8-402">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="abde8-403">**Chaîne**</span><span class="sxs-lookup"><span data-stu-id="abde8-403">**String**</span></span>|<span data-ttu-id="abde8-404">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="abde8-404">**&#124;&#124;**</span></span>|<span data-ttu-id="abde8-405">Concaténation.</span><span class="sxs-lookup"><span data-stu-id="abde8-405">Concatenation.</span></span> <span data-ttu-id="abde8-406">Renvoie une concaténation de deux arguments.</span><span class="sxs-lookup"><span data-stu-id="abde8-406">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="abde8-407">**Opérateurs ternaires :**</span><span class="sxs-lookup"><span data-stu-id="abde8-407">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="abde8-408">Opérateur ternaire</span><span class="sxs-lookup"><span data-stu-id="abde8-408">Ternary operator</span></span>|<span data-ttu-id="abde8-409">?</span><span class="sxs-lookup"><span data-stu-id="abde8-409">?</span></span>|<span data-ttu-id="abde8-410">Retourne le deuxième argument si le premier argument prend la valeur **true**, ou le troisième argument dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-410">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="abde8-411">**Ordre des valeurs pour comparaison**</span><span class="sxs-lookup"><span data-stu-id="abde8-411">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="abde8-412">**Type**</span><span class="sxs-lookup"><span data-stu-id="abde8-412">**Type**</span></span>|<span data-ttu-id="abde8-413">**Ordre des valeurs**</span><span class="sxs-lookup"><span data-stu-id="abde8-413">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="abde8-414">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="abde8-414">**Undefined**</span></span>|<span data-ttu-id="abde8-415">Non comparables.</span><span class="sxs-lookup"><span data-stu-id="abde8-415">Not comparable.</span></span>|  
|<span data-ttu-id="abde8-416">**Null**</span><span class="sxs-lookup"><span data-stu-id="abde8-416">**Null**</span></span>|<span data-ttu-id="abde8-417">Valeur unique : **null**</span><span class="sxs-lookup"><span data-stu-id="abde8-417">Single value: **null**</span></span>|  
|<span data-ttu-id="abde8-418">**Nombre**</span><span class="sxs-lookup"><span data-stu-id="abde8-418">**Number**</span></span>|<span data-ttu-id="abde8-419">Nombre réel naturel.</span><span class="sxs-lookup"><span data-stu-id="abde8-419">Natural real number.</span></span><br /><br /> <span data-ttu-id="abde8-420">La valeur d’infini négatif est inférieure à toute autre valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-420">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="abde8-421">La valeur d’infini positif est supérieure à toute autre valeur numérique. La valeur **NaN** n’est pas comparable.</span><span class="sxs-lookup"><span data-stu-id="abde8-421">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="abde8-422">La comparaison avec **NaN** entraîne une valeur **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="abde8-422">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="abde8-423">**Chaîne**</span><span class="sxs-lookup"><span data-stu-id="abde8-423">**String**</span></span>|<span data-ttu-id="abde8-424">Ordre lexicographique.</span><span class="sxs-lookup"><span data-stu-id="abde8-424">Lexicographical order.</span></span>|  
|<span data-ttu-id="abde8-425">**Tableau**</span><span class="sxs-lookup"><span data-stu-id="abde8-425">**Array**</span></span>|<span data-ttu-id="abde8-426">Aucun ordre, mais équitable.</span><span class="sxs-lookup"><span data-stu-id="abde8-426">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="abde8-427">**Object**</span><span class="sxs-lookup"><span data-stu-id="abde8-427">**Object**</span></span>|<span data-ttu-id="abde8-428">Aucun ordre, mais équitable.</span><span class="sxs-lookup"><span data-stu-id="abde8-428">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="abde8-429">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-429">**Remarks**</span></span>  
  
 <span data-ttu-id="abde8-430">Dans la base de données Azure Cosmos, les types des valeurs sont souvent inconnus jusqu'à leur récupération effective à partir de la base de données.</span><span class="sxs-lookup"><span data-stu-id="abde8-430">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="abde8-431">Afin d’assurer l’exécution des requêtes de manière efficace, la plupart des opérateurs ont des exigences de type strictes.</span><span class="sxs-lookup"><span data-stu-id="abde8-431">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="abde8-432">De plus, les opérateurs n’effectuent pas de conversions implicites eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="abde8-432">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="abde8-433">Cela signifie qu’une requête, comme : SELECT * FROM ROOT r WHERE r.Age = 21 retourne uniquement les documents dont la propriété Age est égale au nombre 21.</span><span class="sxs-lookup"><span data-stu-id="abde8-433">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="abde8-434">Les documents dont la propriété Age est égale à la chaîne "21" ou à la chaîne "0021" ne correspondent pas, car l’expression "21" = 21 produit le résultat Undefined.</span><span class="sxs-lookup"><span data-stu-id="abde8-434">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="abde8-435">Cela permet une meilleure utilisation des index, car la recherche d’une valeur spécifique (c'est-à-dire le numéro 21) est plus rapide que la recherche d’un nombre indéfini de correspondances potentielles (à savoir le nombre 21 ou des chaînes de type "21", "021", "21.0"...).</span><span class="sxs-lookup"><span data-stu-id="abde8-435">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="abde8-436">Cela est différent de la manière dont JavaScript évalue les opérateurs sur les valeurs de types différents.</span><span class="sxs-lookup"><span data-stu-id="abde8-436">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="abde8-437">**Comparaison et égalité pour les objets et tableaux**</span><span class="sxs-lookup"><span data-stu-id="abde8-437">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="abde8-438">La comparaison des valeurs de tableau ou d’objet à l’aide des opérateurs de plage (>, > =, <, < =) entraînera un résultat Undefined, car il n’existe pas d’ordre défini sur les valeurs d’objet ou de tableau.</span><span class="sxs-lookup"><span data-stu-id="abde8-438">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="abde8-439">Toutefois, l’utilisation d’opérateurs d’égalité/inégalité (=, ! =, <>) est prise en charge et les valeurs seront comparées structurellement.</span><span class="sxs-lookup"><span data-stu-id="abde8-439">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="abde8-440">Les tableaux sont égaux si les deux tableaux ont le même nombre d’éléments et que les éléments aux positions correspondantes sont également égaux.</span><span class="sxs-lookup"><span data-stu-id="abde8-440">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="abde8-441">Si la comparaison d’une paire d’éléments produit un résultat Undefined, le résultat de la comparaison de tableaux est Undefined.</span><span class="sxs-lookup"><span data-stu-id="abde8-441">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="abde8-442">Les objets sont égaux si les deux objets ont les mêmes propriétés définies, et si les valeurs des propriétés correspondantes sont également égales.</span><span class="sxs-lookup"><span data-stu-id="abde8-442">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="abde8-443">Si la comparaison d’une paire de valeurs de propriété produit un résultat Undefined, le résultat de la comparaison d’objets est Undefined.</span><span class="sxs-lookup"><span data-stu-id="abde8-443">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="abde8-444"><a name="bk_constants"></a> Constantes</span><span class="sxs-lookup"><span data-stu-id="abde8-444"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="abde8-445">Une constante, également appelée un littéral ou une valeur scalaire, est un symbole représentant une valeur de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="abde8-445">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="abde8-446">Le format d’une constante dépend du type de données de la valeur qu’elle représente.</span><span class="sxs-lookup"><span data-stu-id="abde8-446">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="abde8-447">**Prise en charge des types de données scalaires :**</span><span class="sxs-lookup"><span data-stu-id="abde8-447">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="abde8-448">**Type**</span><span class="sxs-lookup"><span data-stu-id="abde8-448">**Type**</span></span>|<span data-ttu-id="abde8-449">**Ordre des valeurs**</span><span class="sxs-lookup"><span data-stu-id="abde8-449">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="abde8-450">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="abde8-450">**Undefined**</span></span>|<span data-ttu-id="abde8-451">Valeur unique : **Undefined**</span><span class="sxs-lookup"><span data-stu-id="abde8-451">Single value: **undefined**</span></span>|  
|<span data-ttu-id="abde8-452">**Null**</span><span class="sxs-lookup"><span data-stu-id="abde8-452">**Null**</span></span>|<span data-ttu-id="abde8-453">Valeur unique : **null**</span><span class="sxs-lookup"><span data-stu-id="abde8-453">Single value: **null**</span></span>|  
|<span data-ttu-id="abde8-454">**Booléen**</span><span class="sxs-lookup"><span data-stu-id="abde8-454">**Boolean**</span></span>|<span data-ttu-id="abde8-455">Valeurs : **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="abde8-455">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="abde8-456">**Nombre**</span><span class="sxs-lookup"><span data-stu-id="abde8-456">**Number**</span></span>|<span data-ttu-id="abde8-457">Un nombre à virgule flottante double précision répondant à la norme IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="abde8-457">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="abde8-458">**Chaîne**</span><span class="sxs-lookup"><span data-stu-id="abde8-458">**String**</span></span>|<span data-ttu-id="abde8-459">Une séquence de zéro ou plusieurs caractères Unicode.</span><span class="sxs-lookup"><span data-stu-id="abde8-459">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="abde8-460">Les chaînes doivent figurer entre guillemets simples ou doubles.</span><span class="sxs-lookup"><span data-stu-id="abde8-460">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="abde8-461">**Tableau**</span><span class="sxs-lookup"><span data-stu-id="abde8-461">**Array**</span></span>|<span data-ttu-id="abde8-462">Une séquence de zéro ou plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="abde8-462">A sequence of zero or more elements.</span></span> <span data-ttu-id="abde8-463">Chaque élément peut être une valeur de tout type de données scalaires, à l’exception de Undefined.</span><span class="sxs-lookup"><span data-stu-id="abde8-463">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="abde8-464">**Object**</span><span class="sxs-lookup"><span data-stu-id="abde8-464">**Object**</span></span>|<span data-ttu-id="abde8-465">Un jeu non ordonné de zéro ou plusieurs paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="abde8-465">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="abde8-466">Le nom est une chaîne Unicode, la valeur peut être de n’importe quel type de données scalaire, sauf **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="abde8-466">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="abde8-467">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-467">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="abde8-468">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-468">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="abde8-469">Représente la valeur undefined du type Undefined.</span><span class="sxs-lookup"><span data-stu-id="abde8-469">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="abde8-470">Représente la valeur **null** du type **Null**.</span><span class="sxs-lookup"><span data-stu-id="abde8-470">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="abde8-471">Représente une constante de type booléen.</span><span class="sxs-lookup"><span data-stu-id="abde8-471">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="abde8-472">Représente une valeur **false** de type booléen.</span><span class="sxs-lookup"><span data-stu-id="abde8-472">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="abde8-473">Représente une valeur **true** de type booléen.</span><span class="sxs-lookup"><span data-stu-id="abde8-473">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="abde8-474">Représente une constante.</span><span class="sxs-lookup"><span data-stu-id="abde8-474">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="abde8-475">Les littéraux décimaux sont représentés à l’aide de la notation décimale, ou de la notation scientifique.</span><span class="sxs-lookup"><span data-stu-id="abde8-475">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="abde8-476">Les littéraux hexadécimaux sont représentés à l’aide du préfixe « 0 x », suivi d’un ou plusieurs chiffres hexadécimaux.</span><span class="sxs-lookup"><span data-stu-id="abde8-476">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="abde8-477">Représente une constante de type chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-477">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="abde8-478">Les littéraux de chaîne sont des chaînes Unicode représentées par une séquence de zéro ou plusieurs caractères Unicode ou séquences d’échappement.</span><span class="sxs-lookup"><span data-stu-id="abde8-478">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="abde8-479">Les littéraux de chaîne sont placés entre guillemets simples (apostrophes, ’) ou guillemets doubles (").</span><span class="sxs-lookup"><span data-stu-id="abde8-479">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="abde8-480">Les séquences d’échappement suivantes sont autorisées :</span><span class="sxs-lookup"><span data-stu-id="abde8-480">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="abde8-481">**Séquence d’échappement**</span><span class="sxs-lookup"><span data-stu-id="abde8-481">**Escape sequence**</span></span>|<span data-ttu-id="abde8-482">**Description**</span><span class="sxs-lookup"><span data-stu-id="abde8-482">**Description**</span></span>|<span data-ttu-id="abde8-483">**Caractères Unicode**</span><span class="sxs-lookup"><span data-stu-id="abde8-483">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="abde8-484">\\'</span><span class="sxs-lookup"><span data-stu-id="abde8-484">\\'</span></span>|<span data-ttu-id="abde8-485">apostrophe (')</span><span class="sxs-lookup"><span data-stu-id="abde8-485">apostrophe (')</span></span>|<span data-ttu-id="abde8-486">U+0027</span><span class="sxs-lookup"><span data-stu-id="abde8-486">U+0027</span></span>|  
|<span data-ttu-id="abde8-487">\\"</span><span class="sxs-lookup"><span data-stu-id="abde8-487">\\"</span></span>|<span data-ttu-id="abde8-488">guillemet (")</span><span class="sxs-lookup"><span data-stu-id="abde8-488">quotation mark (")</span></span>|<span data-ttu-id="abde8-489">U+0022</span><span class="sxs-lookup"><span data-stu-id="abde8-489">U+0022</span></span>|  
|\\\|<span data-ttu-id="abde8-490">barre oblique inversée (\\)</span><span class="sxs-lookup"><span data-stu-id="abde8-490">reverse solidus (\\)</span></span>|<span data-ttu-id="abde8-491">U+005C</span><span class="sxs-lookup"><span data-stu-id="abde8-491">U+005C</span></span>|  
|\\/|<span data-ttu-id="abde8-492">barre oblique (/)</span><span class="sxs-lookup"><span data-stu-id="abde8-492">solidus (/)</span></span>|<span data-ttu-id="abde8-493">U+002F</span><span class="sxs-lookup"><span data-stu-id="abde8-493">U+002F</span></span>|  
|<span data-ttu-id="abde8-494">\b</span><span class="sxs-lookup"><span data-stu-id="abde8-494">\b</span></span>|<span data-ttu-id="abde8-495">retour arrière</span><span class="sxs-lookup"><span data-stu-id="abde8-495">backspace</span></span>|<span data-ttu-id="abde8-496">U+0008</span><span class="sxs-lookup"><span data-stu-id="abde8-496">U+0008</span></span>|  
|<span data-ttu-id="abde8-497">\f</span><span class="sxs-lookup"><span data-stu-id="abde8-497">\f</span></span>|<span data-ttu-id="abde8-498">saut de page</span><span class="sxs-lookup"><span data-stu-id="abde8-498">form feed</span></span>|<span data-ttu-id="abde8-499">U+000C</span><span class="sxs-lookup"><span data-stu-id="abde8-499">U+000C</span></span>|  
|\n|<span data-ttu-id="abde8-500">saut de ligne</span><span class="sxs-lookup"><span data-stu-id="abde8-500">line feed</span></span>|<span data-ttu-id="abde8-501">U+000A</span><span class="sxs-lookup"><span data-stu-id="abde8-501">U+000A</span></span>|  
|<span data-ttu-id="abde8-502">\r</span><span class="sxs-lookup"><span data-stu-id="abde8-502">\r</span></span>|<span data-ttu-id="abde8-503">retour chariot</span><span class="sxs-lookup"><span data-stu-id="abde8-503">carriage return</span></span>|<span data-ttu-id="abde8-504">U+000D</span><span class="sxs-lookup"><span data-stu-id="abde8-504">U+000D</span></span>|  
|<span data-ttu-id="abde8-505">\t</span><span class="sxs-lookup"><span data-stu-id="abde8-505">\t</span></span>|<span data-ttu-id="abde8-506">tab</span><span class="sxs-lookup"><span data-stu-id="abde8-506">tab</span></span>|<span data-ttu-id="abde8-507">U+0009</span><span class="sxs-lookup"><span data-stu-id="abde8-507">U+0009</span></span>|  
|<span data-ttu-id="abde8-508">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="abde8-508">\uXXXX</span></span>|<span data-ttu-id="abde8-509">Un caractère Unicode défini par 4 chiffres hexadécimaux.</span><span class="sxs-lookup"><span data-stu-id="abde8-509">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="abde8-510">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="abde8-510">U+XXXX</span></span>|  
  
##  <span data-ttu-id="abde8-511"><a name="bk_query_perf_guidelines"></a> Instructions relatives aux performances de requête</span><span class="sxs-lookup"><span data-stu-id="abde8-511"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="abde8-512">Pour qu’une requête puisse s’exécuter efficacement sur une grande collection, elle doit utiliser des filtres qui peuvent être appliqués via un ou plusieurs index.</span><span class="sxs-lookup"><span data-stu-id="abde8-512">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="abde8-513">Les filtres suivants sont considérés pour la recherche d’index :</span><span class="sxs-lookup"><span data-stu-id="abde8-513">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="abde8-514">Utilisez l’opérateur d’égalité (=) avec une expression de chemin d’accès de document et une constante.</span><span class="sxs-lookup"><span data-stu-id="abde8-514">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="abde8-515">Utilisez les opérateurs de plage (<, \<=, >, > =) avec une expression de chemin d’accès de document et des constantes numériques.</span><span class="sxs-lookup"><span data-stu-id="abde8-515">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="abde8-516">L’expression de chemin d’accès de document représente toute expression qui identifie un chemin d’accès constant dans les documents de la collecte de base de données référencée.</span><span class="sxs-lookup"><span data-stu-id="abde8-516">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="abde8-517">**Expression de chemin d’accès à un document**</span><span class="sxs-lookup"><span data-stu-id="abde8-517">**Document path expression**</span></span>  
  
 <span data-ttu-id="abde8-518">Les expressions de chemin d’accès à un document sont des expressions qu’un chemin d’accès de propriété ou indexeur de tableau évalue sur un document provenant des documents de la collecte de base de données.</span><span class="sxs-lookup"><span data-stu-id="abde8-518">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="abde8-519">Ce chemin d’accès peut être utilisé pour identifier l’emplacement des valeurs référencées dans un filtre directement dans les documents de la collection de la base de données.</span><span class="sxs-lookup"><span data-stu-id="abde8-519">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="abde8-520">Pour qu’une expression soit considérée comme une expression de chemin d’accès de document, elle doit :</span><span class="sxs-lookup"><span data-stu-id="abde8-520">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="abde8-521">Faire référence directement à la racine de la collection.</span><span class="sxs-lookup"><span data-stu-id="abde8-521">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="abde8-522">Référencer la propriété ou l’indexeur de tableau de constantes d’une expression de chemin d’accès de document</span><span class="sxs-lookup"><span data-stu-id="abde8-522">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="abde8-523">Faire référence à un alias, qui représente une expression de chemin d’accès de document.</span><span class="sxs-lookup"><span data-stu-id="abde8-523">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="abde8-524">**Conventions de syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-524">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="abde8-525">Le tableau suivant décrit les conventions utilisées pour décrire la syntaxe dans la référence du langage de requête de l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="abde8-525">The following table describes the conventions used to describe syntax in the DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="abde8-526">**Convention**</span><span class="sxs-lookup"><span data-stu-id="abde8-526">**Convention**</span></span>|<span data-ttu-id="abde8-527">**Utilisé pour**</span><span class="sxs-lookup"><span data-stu-id="abde8-527">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="abde8-528">MAJUSCULES</span><span class="sxs-lookup"><span data-stu-id="abde8-528">UPPERCASE</span></span>|<span data-ttu-id="abde8-529">Mots-clés non sensibles à la casse.</span><span class="sxs-lookup"><span data-stu-id="abde8-529">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="abde8-530">minuscules</span><span class="sxs-lookup"><span data-stu-id="abde8-530">lowercase</span></span>|<span data-ttu-id="abde8-531">Mots-clés sensibles à la casse.</span><span class="sxs-lookup"><span data-stu-id="abde8-531">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="abde8-532">\<nonterminal></span><span class="sxs-lookup"><span data-stu-id="abde8-532">\<nonterminal></span></span>|<span data-ttu-id="abde8-533">Non terminal, défini séparément.</span><span class="sxs-lookup"><span data-stu-id="abde8-533">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="abde8-534">\<nonterminal> ::=</span><span class="sxs-lookup"><span data-stu-id="abde8-534">\<nonterminal> ::=</span></span>|<span data-ttu-id="abde8-535">Définition de la syntaxe de l’élément nonterminal.</span><span class="sxs-lookup"><span data-stu-id="abde8-535">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="abde8-536">other_terminal</span><span class="sxs-lookup"><span data-stu-id="abde8-536">other_terminal</span></span>|<span data-ttu-id="abde8-537">Terminal (jeton), décrit en détail par des mots.</span><span class="sxs-lookup"><span data-stu-id="abde8-537">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="abde8-538">identificateur</span><span class="sxs-lookup"><span data-stu-id="abde8-538">identifier</span></span>|<span data-ttu-id="abde8-539">Identificateur.</span><span class="sxs-lookup"><span data-stu-id="abde8-539">Identifier.</span></span> <span data-ttu-id="abde8-540">Autorise uniquement les caractères suivants : a-z A-Z 0-9 _ Le premier caractère ne peut pas être un chiffre.</span><span class="sxs-lookup"><span data-stu-id="abde8-540">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="abde8-541">"chaîne"</span><span class="sxs-lookup"><span data-stu-id="abde8-541">"string"</span></span>|<span data-ttu-id="abde8-542">Chaîne entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="abde8-542">Quoted string.</span></span> <span data-ttu-id="abde8-543">Autorise n’importe quelle chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-543">Allows any valid string.</span></span> <span data-ttu-id="abde8-544">Consultez la description de string_literal.</span><span class="sxs-lookup"><span data-stu-id="abde8-544">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="abde8-545">'symbole'</span><span class="sxs-lookup"><span data-stu-id="abde8-545">'symbol'</span></span>|<span data-ttu-id="abde8-546">Symbole littéral qui fait partie de la syntaxe.</span><span class="sxs-lookup"><span data-stu-id="abde8-546">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="abde8-547">&#124; (barre verticale)</span><span class="sxs-lookup"><span data-stu-id="abde8-547">&#124; (vertical bar)</span></span>|<span data-ttu-id="abde8-548">Alternatives aux éléments de syntaxe.</span><span class="sxs-lookup"><span data-stu-id="abde8-548">Alternatives for syntax items.</span></span> <span data-ttu-id="abde8-549">Vous pouvez utiliser seulement un des éléments spécifiés.</span><span class="sxs-lookup"><span data-stu-id="abde8-549">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="abde8-550">[ ] /(crochets)</span><span class="sxs-lookup"><span data-stu-id="abde8-550">[ ] /(brackets)</span></span>|<span data-ttu-id="abde8-551">Les crochets entourent un ou plusieurs éléments facultatifs.</span><span class="sxs-lookup"><span data-stu-id="abde8-551">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="abde8-552">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="abde8-552">[ ,...n ]</span></span>|<span data-ttu-id="abde8-553">Indique que l’élément précédent peut être répété n fois.</span><span class="sxs-lookup"><span data-stu-id="abde8-553">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="abde8-554">Les occurrences sont séparées par des virgules.</span><span class="sxs-lookup"><span data-stu-id="abde8-554">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="abde8-555">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="abde8-555">[ ...n ]</span></span>|<span data-ttu-id="abde8-556">Indique que l’élément précédent peut être répété n fois.</span><span class="sxs-lookup"><span data-stu-id="abde8-556">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="abde8-557">Les occurrences sont séparées par des espaces.</span><span class="sxs-lookup"><span data-stu-id="abde8-557">The occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="abde8-558"><a name="bk_built_in_functions"></a> Fonctions intégrées</span><span class="sxs-lookup"><span data-stu-id="abde8-558"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="abde8-559">Azure Cosmos DB fournit de nombreuses fonctions SQL intégrées.</span><span class="sxs-lookup"><span data-stu-id="abde8-559">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="abde8-560">Les catégories de fonctions intégrées sont répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="abde8-560">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="abde8-561">Fonction</span><span class="sxs-lookup"><span data-stu-id="abde8-561">Function</span></span>|<span data-ttu-id="abde8-562">Description</span><span class="sxs-lookup"><span data-stu-id="abde8-562">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="abde8-563">Fonctions mathématiques</span><span class="sxs-lookup"><span data-stu-id="abde8-563">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="abde8-564">Chaque fonction mathématique effectue un calcul, généralement basé sur les valeurs d'entrée fournies comme arguments, et retourne une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-564">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="abde8-565">Fonctions de vérification du type</span><span class="sxs-lookup"><span data-stu-id="abde8-565">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="abde8-566">Les fonctions de vérification du type vous permettent de vérifier le type d'une expression donnée dans les requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="abde8-566">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="abde8-567">Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="abde8-567">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="abde8-568">Les fonctions de chaîne effectuent une opération sur une valeur d’entrée de chaîne et retournent une valeur de type chaîne, une valeur numérique ou une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-568">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="abde8-569">Fonctions de tableau</span><span class="sxs-lookup"><span data-stu-id="abde8-569">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="abde8-570">Les fonctions de tableau effectuent une opération sur une valeur d’entrée de tableau et retournent une valeur numérique, une valeur booléenne ou une valeur de tableau.</span><span class="sxs-lookup"><span data-stu-id="abde8-570">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="abde8-571">Fonctions spatiales</span><span class="sxs-lookup"><span data-stu-id="abde8-571">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="abde8-572">Les fonctions spatiales effectuent une opération sur une valeur d’entrée de chaîne et retournent une valeur d’entrée d’objet spatial, une valeur numérique ou une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-572">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="abde8-573"><a name="bk_mathematical_functions"></a> Fonctions mathématiques</span><span class="sxs-lookup"><span data-stu-id="abde8-573"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="abde8-574">Les fonctions suivantes effectuent un calcul, généralement basé sur les valeurs d'entrée fournies comme arguments, et retournent une valeur numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-574">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="abde8-575">ABS</span><span class="sxs-lookup"><span data-stu-id="abde8-575">ABS</span></span>](#bk_abs)|[<span data-ttu-id="abde8-576">ACOS</span><span class="sxs-lookup"><span data-stu-id="abde8-576">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="abde8-577">ASIN</span><span class="sxs-lookup"><span data-stu-id="abde8-577">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="abde8-578">ATAN</span><span class="sxs-lookup"><span data-stu-id="abde8-578">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="abde8-579">ATN2</span><span class="sxs-lookup"><span data-stu-id="abde8-579">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="abde8-580">CEILING</span><span class="sxs-lookup"><span data-stu-id="abde8-580">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="abde8-581">COS</span><span class="sxs-lookup"><span data-stu-id="abde8-581">COS</span></span>](#bk_cos)|[<span data-ttu-id="abde8-582">COT</span><span class="sxs-lookup"><span data-stu-id="abde8-582">COT</span></span>](#bk_cot)|[<span data-ttu-id="abde8-583">DEGREES</span><span class="sxs-lookup"><span data-stu-id="abde8-583">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="abde8-584">EXP</span><span class="sxs-lookup"><span data-stu-id="abde8-584">EXP</span></span>](#bk_exp)|[<span data-ttu-id="abde8-585">FLOOR</span><span class="sxs-lookup"><span data-stu-id="abde8-585">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="abde8-586">LOG</span><span class="sxs-lookup"><span data-stu-id="abde8-586">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="abde8-587">LOG10</span><span class="sxs-lookup"><span data-stu-id="abde8-587">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="abde8-588">PI</span><span class="sxs-lookup"><span data-stu-id="abde8-588">PI</span></span>](#bk_pi)|[<span data-ttu-id="abde8-589">POWER</span><span class="sxs-lookup"><span data-stu-id="abde8-589">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="abde8-590">RADIANS</span><span class="sxs-lookup"><span data-stu-id="abde8-590">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="abde8-591">ROUND</span><span class="sxs-lookup"><span data-stu-id="abde8-591">ROUND</span></span>](#bk_round)|[<span data-ttu-id="abde8-592">SIN</span><span class="sxs-lookup"><span data-stu-id="abde8-592">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="abde8-593">SQRT</span><span class="sxs-lookup"><span data-stu-id="abde8-593">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="abde8-594">SQUARE</span><span class="sxs-lookup"><span data-stu-id="abde8-594">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="abde8-595">SIGN</span><span class="sxs-lookup"><span data-stu-id="abde8-595">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="abde8-596">TAN</span><span class="sxs-lookup"><span data-stu-id="abde8-596">TAN</span></span>](#bk_tan)|[<span data-ttu-id="abde8-597">TRUNC</span><span class="sxs-lookup"><span data-stu-id="abde8-597">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="abde8-598"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="abde8-598"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="abde8-599">Retourne la valeur (positive) absolue de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-599">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-600">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-600">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-601">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-601">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-602">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-602">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-603">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-603">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-604">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-604">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-605">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-605">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-606">L’exemple suivant montre les résultats de l’utilisation de la fonction ABS sur trois nombres différents.</span><span class="sxs-lookup"><span data-stu-id="abde8-606">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="abde8-607">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-607">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="abde8-608"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="abde8-608"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="abde8-609">Retourne l’angle, en radians, dont le cosinus est l’expression numérique spécifiée ; également appelée arccosinus.</span><span class="sxs-lookup"><span data-stu-id="abde8-609">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="abde8-610">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-610">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-611">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-611">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-612">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-612">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-613">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-613">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-614">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-614">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-615">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-615">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-616">L’exemple suivant retourne la valeur ACOS de -1.</span><span class="sxs-lookup"><span data-stu-id="abde8-616">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="abde8-617">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-617">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="abde8-618"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="abde8-618"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="abde8-619">Retourne l’angle, en radians, dont le sinus est l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-619">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="abde8-620">Cette fonction est également appelée arcsinus.</span><span class="sxs-lookup"><span data-stu-id="abde8-620">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="abde8-621">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-621">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-622">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-622">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-623">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-623">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-624">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-624">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-625">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-625">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-626">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-626">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-627">L’exemple suivant retourne la valeur ASIN de -1.</span><span class="sxs-lookup"><span data-stu-id="abde8-627">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="abde8-628">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-628">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="abde8-629"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="abde8-629"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="abde8-630">Retourne l’angle, en radians, dont la tangente est l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="abde8-631">Cette fonction est également appelée arctangente.</span><span class="sxs-lookup"><span data-stu-id="abde8-631">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="abde8-632">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-632">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-633">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-633">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-634">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-634">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-635">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-635">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-636">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-636">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-637">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-637">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-638">L’exemple suivant renvoie l’ATAN de la valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-638">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="abde8-639">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-639">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="abde8-640"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="abde8-640"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="abde8-641">Retourne la valeur principale de l’arc tangente de y/x, exprimée en radians.</span><span class="sxs-lookup"><span data-stu-id="abde8-641">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="abde8-642">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-642">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-643">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-643">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-644">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-644">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-645">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-645">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-646">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-646">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-647">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-647">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-648">L’exemple suivant calcule l’ATN2 pour les composants x et y spécifiés.</span><span class="sxs-lookup"><span data-stu-id="abde8-648">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="abde8-649">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-649">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="abde8-650"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="abde8-650"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="abde8-651">Retourne le plus petit nombre entier qui est supérieur ou égal à l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-651">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-652">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-652">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-653">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-653">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-654">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-654">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-655">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-655">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-656">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-656">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-657">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-657">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-658">L’exemple suivant montre des valeurs numériques positives, négatives et nulles avec la fonction CEILING.</span><span class="sxs-lookup"><span data-stu-id="abde8-658">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="abde8-659">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-659">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="abde8-660"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="abde8-660"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="abde8-661">Retourne le cosinus trigonométrique de l’angle spécifié, en radians, dans l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-661">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="abde8-662">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-662">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-663">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-663">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-664">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-664">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-665">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-665">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-666">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-666">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-667">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-667">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-668">L’exemple suivant calcule le COS de l’angle spécifié.</span><span class="sxs-lookup"><span data-stu-id="abde8-668">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="abde8-669">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-669">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="abde8-670"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="abde8-670"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="abde8-671">Retourne la cotangente trigonométrique de l’angle spécifié, en radians, dans l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-671">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-672">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-672">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-673">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-673">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-674">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-674">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-675">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-675">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-676">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-676">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-677">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-677">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-678">L’exemple suivant calcule la COT (cotangente) de l’angle spécifié.</span><span class="sxs-lookup"><span data-stu-id="abde8-678">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="abde8-679">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-679">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="abde8-680"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="abde8-680"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="abde8-681">Retourne l’angle correspondant en degrés d’un angle spécifié en radians.</span><span class="sxs-lookup"><span data-stu-id="abde8-681">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="abde8-682">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-682">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-683">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-683">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-684">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-684">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-685">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-685">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-686">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-686">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-687">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-687">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-688">L’exemple suivant retourne le nombre de degrés d’un angle de PI/2 radians.</span><span class="sxs-lookup"><span data-stu-id="abde8-688">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="abde8-689">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-689">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="abde8-690"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="abde8-690"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="abde8-691">Retourne le plus grand nombre entier qui est inférieur ou égal à l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-691">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-692">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-692">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-693">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-693">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-694">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-694">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-695">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-695">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-696">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-696">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-697">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-697">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-698">L’exemple suivant montre des valeurs numériques positives, négatives et nulles avec la fonction FLOOR.</span><span class="sxs-lookup"><span data-stu-id="abde8-698">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="abde8-699">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-699">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="abde8-700"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="abde8-700"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="abde8-701">Retourne la valeur exponentielle de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-701">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-702">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-702">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-703">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-703">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-704">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-704">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-705">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-705">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-706">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-706">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-707">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-707">**Remarks**</span></span>  
  
 <span data-ttu-id="abde8-708">La constante **e** (2,718281...), est la base des logarithmes naturels.</span><span class="sxs-lookup"><span data-stu-id="abde8-708">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="abde8-709">L’exposant d’un nombre correspond à la constante **e** élevée à la puissance du nombre.</span><span class="sxs-lookup"><span data-stu-id="abde8-709">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="abde8-710">Par exemple EXP(1.0) = e ^ 1,0 = 2,71828182845905 et EXP(10) = e ^ 10 = 22026,4657948067.</span><span class="sxs-lookup"><span data-stu-id="abde8-710">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="abde8-711">La valeur exponentielle du logarithme naturel d’un nombre est le nombre lui-même : EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="abde8-711">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="abde8-712">Et le logarithme naturel de la valeur exponentielle d’un nombre est le nombre lui-même : LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="abde8-712">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="abde8-713">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-713">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-714">L’exemple suivant déclare une variable et renvoie la valeur exponentielle de la variable spécifiée (10).</span><span class="sxs-lookup"><span data-stu-id="abde8-714">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="abde8-715">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-715">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="abde8-716">L’exemple suivant retourne la valeur exponentielle du logarithme naturel de 20 et le logarithme naturel de la valeur exponentielle de 20.</span><span class="sxs-lookup"><span data-stu-id="abde8-716">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="abde8-717">Étant donné que ces fonctions sont l’inverse l’une de l’autre, la valeur renvoyée avec arrondi pour les opérations mathématiques à virgule flottante dans les deux cas est 20.</span><span class="sxs-lookup"><span data-stu-id="abde8-717">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="abde8-718">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-718">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="abde8-719"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="abde8-719"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="abde8-720">Retourne le logarithme naturel de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-720">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-721">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-721">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="abde8-722">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-722">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-723">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-723">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="abde8-724">L’argument numérique facultatif qui définit la base du logarithme.</span><span class="sxs-lookup"><span data-stu-id="abde8-724">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="abde8-725">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-725">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-726">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-726">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-727">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-727">**Remarks**</span></span>  
  
 <span data-ttu-id="abde8-728">Par défaut, LOG() renvoie le logarithme naturel.</span><span class="sxs-lookup"><span data-stu-id="abde8-728">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="abde8-729">Vous pouvez modifier la base du logarithme avec une autre valeur en utilisant le paramètre de base facultatif.</span><span class="sxs-lookup"><span data-stu-id="abde8-729">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="abde8-730">Le logarithme naturel est le logarithme de base **e**, où **e** est une constante irrationnelle approximativement égale à 2,718281828.</span><span class="sxs-lookup"><span data-stu-id="abde8-730">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="abde8-731">Le logarithme naturel de la valeur exponentielle d’un nombre est le nombre lui-même : LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="abde8-731">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="abde8-732">Et la valeur exponentielle du logarithme naturel d’un nombre est le nombre lui-même : EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="abde8-732">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="abde8-733">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-733">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-734">L’exemple suivant déclare une variable et renvoie la valeur du logarithme de la variable spécifiée (10).</span><span class="sxs-lookup"><span data-stu-id="abde8-734">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="abde8-735">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-735">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="abde8-736">L’exemple suivant calcule le LOG pour l’exposant d’un nombre.</span><span class="sxs-lookup"><span data-stu-id="abde8-736">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="abde8-737">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-737">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="abde8-738"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="abde8-738"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="abde8-739">Retourne le logarithme en base 10 de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-739">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-740">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-740">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-741">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-741">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-742">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-742">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-743">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-743">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-744">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-744">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-745">**Notes**</span><span class="sxs-lookup"><span data-stu-id="abde8-745">**Remarks**</span></span>  
  
 <span data-ttu-id="abde8-746">Les fonctions LOG10 et POWER sont inversement liées entre elles.</span><span class="sxs-lookup"><span data-stu-id="abde8-746">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="abde8-747">Par exemple, 10 ^ LOG10 (n) = n.</span><span class="sxs-lookup"><span data-stu-id="abde8-747">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="abde8-748">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-748">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-749">L’exemple suivant déclare une variable et renvoie la valeur de LOG10 de la variable spécifiée (100).</span><span class="sxs-lookup"><span data-stu-id="abde8-749">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="abde8-750">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-750">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="abde8-751"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="abde8-751"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="abde8-752">Retourne la valeur constante de PI.</span><span class="sxs-lookup"><span data-stu-id="abde8-752">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="abde8-753">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-753">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="abde8-754">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-754">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-755">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-755">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-756">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-756">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-757">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-757">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-758">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-758">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-759">L’exemple suivant retourne la valeur de PI.</span><span class="sxs-lookup"><span data-stu-id="abde8-759">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="abde8-760">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-760">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="abde8-761"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="abde8-761"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="abde8-762">Retourne la valeur de l’expression spécifiée élevée à la puissance spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-762">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="abde8-763">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-763">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="abde8-764">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-764">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-765">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-765">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="abde8-766">La puissance à laquelle élever `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="abde8-766">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="abde8-767">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-767">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-768">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-768">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-769">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-769">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-770">L’exemple suivant montre l’élévation d’un nombre à la puissance 3 (le cube du nombre).</span><span class="sxs-lookup"><span data-stu-id="abde8-770">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="abde8-771">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-771">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="abde8-772"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="abde8-772"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="abde8-773">Retourne des radians lorsqu’une expression numérique, en degrés, est entrée.</span><span class="sxs-lookup"><span data-stu-id="abde8-773">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="abde8-774">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-774">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-775">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-775">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-776">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-776">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-777">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-777">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-778">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-778">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-779">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-779">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-780">L’exemple suivant prend plusieurs angles comme entrée et retourne les valeurs correspondantes en radians.</span><span class="sxs-lookup"><span data-stu-id="abde8-780">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="abde8-781">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-781">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="abde8-782"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="abde8-782"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="abde8-783">Retourne une valeur numérique, arrondie au nombre entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="abde8-783">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="abde8-784">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-784">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-785">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-785">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-786">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-786">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-787">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-787">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-788">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-788">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-789">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-789">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-790">L’exemple suivant arrondit les nombres positifs et négatifs suivants à l’entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="abde8-790">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="abde8-791">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-791">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="abde8-792"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="abde8-792"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="abde8-793">Retourne le signe positif (+1), nul (0) ou négatif (-1) de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-793">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-794">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-794">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-795">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-795">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-796">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-796">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-797">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-797">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-798">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-798">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-799">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-799">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-800">L’exemple suivant renvoie les valeurs SIGN des nombres de -2 à 2.</span><span class="sxs-lookup"><span data-stu-id="abde8-800">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="abde8-801">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-801">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="abde8-802"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="abde8-802"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="abde8-803">Retourne le sinus trigonométrique de l’angle spécifié, en radians, dans l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-803">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="abde8-804">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-804">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-805">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-805">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-806">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-806">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-807">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-807">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-808">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-808">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-809">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-809">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-810">L’exemple suivant calcule le SIN de l’angle spécifié.</span><span class="sxs-lookup"><span data-stu-id="abde8-810">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="abde8-811">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-811">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="abde8-812"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="abde8-812"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="abde8-813">Retourne la racine carrée de la valeur numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-813">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="abde8-814">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-814">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-815">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-815">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-816">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-816">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-817">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-817">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-818">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-818">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-819">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-819">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-820">L’exemple suivant renvoie les racines carrées des nombres de 1 à 3.</span><span class="sxs-lookup"><span data-stu-id="abde8-820">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="abde8-821">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-821">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="abde8-822"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="abde8-822"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="abde8-823">Retourne le carré de la valeur numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-823">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="abde8-824">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-824">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-825">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-825">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-826">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-826">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-827">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-827">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-828">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-828">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-829">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-829">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-830">L’exemple suivant renvoie les carrés des nombres de 1 à 3.</span><span class="sxs-lookup"><span data-stu-id="abde8-830">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="abde8-831">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-831">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="abde8-832"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="abde8-832"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="abde8-833">Retourne la tangente de l’angle spécifié, en radians, dans l’expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-833">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="abde8-834">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-834">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-835">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-835">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-836">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-836">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-837">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-837">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-838">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-838">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-839">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-839">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-840">L’exemple suivant calcule la tangente de PI()/ 2.</span><span class="sxs-lookup"><span data-stu-id="abde8-840">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="abde8-841">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-841">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="abde8-842"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="abde8-842"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="abde8-843">Retourne une valeur numérique, tronquée au nombre entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="abde8-843">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="abde8-844">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-844">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="abde8-845">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-845">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="abde8-846">Est une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-846">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-847">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-847">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-848">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-848">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-849">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-849">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-850">L’exemple suivant tronque les nombres positifs et négatifs suivants à la valeur entière la plus proche.</span><span class="sxs-lookup"><span data-stu-id="abde8-850">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="abde8-851">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-851">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="abde8-852"><a name="bk_type_checking_functions"></a> Fonctions de vérification du type</span><span class="sxs-lookup"><span data-stu-id="abde8-852"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="abde8-853">Les fonctions suivantes prennent en charge la vérification de type par rapport aux valeurs d’entrée, et chacune renvoie une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-853">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="abde8-854">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="abde8-854">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="abde8-855">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="abde8-855">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="abde8-856">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="abde8-856">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="abde8-857">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="abde8-857">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="abde8-858">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="abde8-858">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="abde8-859">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="abde8-859">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="abde8-860">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="abde8-860">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="abde8-861">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="abde8-861">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="abde8-862"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="abde8-862"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="abde8-863">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type tableau.</span><span class="sxs-lookup"><span data-stu-id="abde8-863">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="abde8-864">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-864">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="abde8-865">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-865">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="abde8-866">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-866">Is any valid expression.</span></span>  
  
 <span data-ttu-id="abde8-867">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-867">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-868">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-868">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-869">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-869">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-870">L’exemple suivant vérifie les objets des types JSON booléen, nombre, chaîne, null, objet, tableau et non défini à l’aide de la fonction IS_ARRAY.</span><span class="sxs-lookup"><span data-stu-id="abde8-870">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="abde8-871">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-871">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="abde8-872"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="abde8-872"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="abde8-873">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type booléen.</span><span class="sxs-lookup"><span data-stu-id="abde8-873">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="abde8-874">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-874">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="abde8-875">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-875">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="abde8-876">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-876">Is any valid expression.</span></span>  
  
 <span data-ttu-id="abde8-877">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-877">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-878">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-878">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-879">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-879">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-880">L’exemple suivant vérifie les objets des types JSON booléen, nombre, chaîne, null, objet, tableau et non défini à l’aide de la fonction IS_BOOL.</span><span class="sxs-lookup"><span data-stu-id="abde8-880">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="abde8-881">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-881">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="abde8-882"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="abde8-882"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="abde8-883">Retourne une valeur booléenne indiquant si une valeur a été attribuée à la propriété.</span><span class="sxs-lookup"><span data-stu-id="abde8-883">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="abde8-884">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-884">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="abde8-885">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-885">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="abde8-886">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-886">Is any valid expression.</span></span>  
  
 <span data-ttu-id="abde8-887">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-887">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-888">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-888">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-889">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-889">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-890">L’exemple suivant vérifie la présence d’une propriété dans le document JSON spécifié.</span><span class="sxs-lookup"><span data-stu-id="abde8-890">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="abde8-891">La première fonction retourne la valeur true, car « a » est présent, mais la seconde retourne false, car « b » est absent.</span><span class="sxs-lookup"><span data-stu-id="abde8-891">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="abde8-892">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-892">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="abde8-893"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="abde8-893"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="abde8-894">Retourne une valeur booléenne indiquant si l’expression spécifiée est de type null.</span><span class="sxs-lookup"><span data-stu-id="abde8-894">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="abde8-895">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-895">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="abde8-896">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-896">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="abde8-897">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-897">Is any valid expression.</span></span>  
  
 <span data-ttu-id="abde8-898">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-898">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-899">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-899">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-900">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-900">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-901">L’exemple suivant vérifie les objets des types JSON booléen, nombre, chaîne, null, objet, tableau et non défini à l’aide de la fonction IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="abde8-901">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="abde8-902">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-902">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="abde8-903"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="abde8-903"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="abde8-904">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type nombre.</span><span class="sxs-lookup"><span data-stu-id="abde8-904">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="abde8-905">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-905">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="abde8-906">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-906">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="abde8-907">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-907">Is any valid expression.</span></span>  
  
 <span data-ttu-id="abde8-908">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-908">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-909">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-909">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-910">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-910">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-911">L’exemple suivant vérifie les objets des types JSON booléen, nombre, chaîne, null, objet, tableau et non défini à l’aide de la fonction IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="abde8-911">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="abde8-912">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-912">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="abde8-913"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="abde8-913"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="abde8-914">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type objet JSON.</span><span class="sxs-lookup"><span data-stu-id="abde8-914">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="abde8-915">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-915">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="abde8-916">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-916">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="abde8-917">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-917">Is any valid expression.</span></span>  
  
 <span data-ttu-id="abde8-918">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-918">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-919">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-919">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-920">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-920">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-921">L’exemple suivant vérifie les objets des types JSON booléen, nombre, chaîne, null, objet, tableau et non défini à l’aide de la fonction IS_OBJECT.</span><span class="sxs-lookup"><span data-stu-id="abde8-921">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="abde8-922">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-922">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="abde8-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="abde8-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="abde8-924">Retourne une valeur booléenne indiquant si l’expression spécifiée est de type primitif (chaîne, booléen, numérique ou null).</span><span class="sxs-lookup"><span data-stu-id="abde8-924">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="abde8-925">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-925">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="abde8-926">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-926">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="abde8-927">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-927">Is any valid expression.</span></span>  
  
 <span data-ttu-id="abde8-928">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-928">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-929">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-929">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-930">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-930">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-931">L’exemple suivant vérifie les objets des types JSON booléen, nombre, chaîne, null, objet, tableau et non défini à l’aide de la fonction IS_PRIMITIVE.</span><span class="sxs-lookup"><span data-stu-id="abde8-931">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="abde8-932">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-932">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="abde8-933"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="abde8-933"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="abde8-934">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-934">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="abde8-935">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-935">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="abde8-936">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-936">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="abde8-937">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-937">Is any valid expression.</span></span>  
  
 <span data-ttu-id="abde8-938">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-938">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-939">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-939">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-940">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-940">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-941">L’exemple suivant vérifie les objets des types JSON booléen, nombre, chaîne, null, objet, tableau et non défini à l’aide de la fonction IS_STRING.</span><span class="sxs-lookup"><span data-stu-id="abde8-941">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="abde8-942">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-942">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="abde8-943"><a name="bk_string_functions"></a> Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="abde8-943"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="abde8-944">Les fonctions scalaires suivantes effectuent une opération sur une valeur d’entrée de chaîne et retournent une valeur de type chaîne, une valeur numérique ou une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-944">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="abde8-945">CONCAT</span><span class="sxs-lookup"><span data-stu-id="abde8-945">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="abde8-946">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="abde8-946">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="abde8-947">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="abde8-947">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="abde8-948">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="abde8-948">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="abde8-949">LEFT</span><span class="sxs-lookup"><span data-stu-id="abde8-949">LEFT</span></span>](#bk_left)|[<span data-ttu-id="abde8-950">LENGTH</span><span class="sxs-lookup"><span data-stu-id="abde8-950">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="abde8-951">LOWER</span><span class="sxs-lookup"><span data-stu-id="abde8-951">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="abde8-952">LTRIM</span><span class="sxs-lookup"><span data-stu-id="abde8-952">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="abde8-953">REPLACE</span><span class="sxs-lookup"><span data-stu-id="abde8-953">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="abde8-954">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="abde8-954">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="abde8-955">REVERSE</span><span class="sxs-lookup"><span data-stu-id="abde8-955">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="abde8-956">RIGHT</span><span class="sxs-lookup"><span data-stu-id="abde8-956">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="abde8-957">RTRIM</span><span class="sxs-lookup"><span data-stu-id="abde8-957">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="abde8-958">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="abde8-958">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="abde8-959">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="abde8-959">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="abde8-960">UPPER</span><span class="sxs-lookup"><span data-stu-id="abde8-960">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="abde8-961"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="abde8-961"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="abde8-962">Retourne une chaîne qui est le résultat de la concaténation d’au moins deux valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-962">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="abde8-963">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-963">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="abde8-964">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-964">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-965">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-965">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-966">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-966">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-967">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-967">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-968">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-968">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-969">L’exemple suivant renvoie la chaîne concaténée des valeurs spécifiées.</span><span class="sxs-lookup"><span data-stu-id="abde8-969">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="abde8-970">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-970">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="abde8-971"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="abde8-971"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="abde8-972">Retourne une valeur booléenne indiquant si la première expression de chaîne contient la seconde.</span><span class="sxs-lookup"><span data-stu-id="abde8-972">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="abde8-973">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-973">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="abde8-974">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-974">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-975">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-975">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-976">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-976">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-977">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-977">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-978">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-978">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-979">L’exemple suivant vérifie si « abc » contient « ab » et « d ».</span><span class="sxs-lookup"><span data-stu-id="abde8-979">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="abde8-980">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-980">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="abde8-981"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="abde8-981"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="abde8-982">Retourne une valeur booléenne indiquant si la première expression de chaîne se termine par la seconde.</span><span class="sxs-lookup"><span data-stu-id="abde8-982">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="abde8-983">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-983">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="abde8-984">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-984">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-985">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-985">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-986">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-986">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-987">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-987">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-988">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-988">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-989">L’exemple suivant indique si « abc » se termine par « b » et « bc ».</span><span class="sxs-lookup"><span data-stu-id="abde8-989">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="abde8-990">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-990">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="abde8-991"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="abde8-991"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="abde8-992">Retourne la position de départ de la première occurrence de la seconde expression de chaîne dans la première expression de chaîne spécifiée, ou -1 si la chaîne est introuvable.</span><span class="sxs-lookup"><span data-stu-id="abde8-992">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="abde8-993">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-993">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="abde8-994">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-994">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-995">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-995">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-996">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-996">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-997">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-997">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-998">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-998">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-999">L’exemple suivant retourne l’index de diverses sous-chaînes à l’intérieur de « abc ».</span><span class="sxs-lookup"><span data-stu-id="abde8-999">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="abde8-1000">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1000">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="abde8-1001"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="abde8-1001"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="abde8-1002">Retourne la partie gauche d’une chaîne avec le nombre de caractères spécifié.</span><span class="sxs-lookup"><span data-stu-id="abde8-1002">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="abde8-1003">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1003">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="abde8-1004">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1004">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1005">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1005">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="abde8-1006">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1006">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-1007">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1007">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1008">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1008">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1009">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1009">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1010">L’exemple suivant retourne la partie gauche de « abc » pour différentes valeurs de longueur.</span><span class="sxs-lookup"><span data-stu-id="abde8-1010">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="abde8-1011">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1011">Here is the result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="abde8-1012"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="abde8-1012"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="abde8-1013">Retourne le nombre de caractères de l’expression de chaîne spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-1013">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="abde8-1014">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1014">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="abde8-1015">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1015">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1016">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1016">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-1017">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1017">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1018">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1018">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1019">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1019">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1020">L’exemple suivant retourne la longueur d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1020">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="abde8-1021">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1021">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="abde8-1022"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="abde8-1022"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="abde8-1023">Retourne une expression de chaîne après la conversion des caractères majuscules en caractères minuscules.</span><span class="sxs-lookup"><span data-stu-id="abde8-1023">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="abde8-1024">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1024">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="abde8-1025">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1025">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1026">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1026">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-1027">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1027">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1028">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1028">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1029">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1029">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1030">L’exemple suivant explique comment utiliser LOWER dans une requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-1030">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="abde8-1031">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1031">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="abde8-1032"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="abde8-1032"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="abde8-1033">Retourne une expression de chaîne après avoir supprimé les espaces de début.</span><span class="sxs-lookup"><span data-stu-id="abde8-1033">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="abde8-1034">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1034">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="abde8-1035">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1035">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1036">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1036">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-1037">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1037">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1038">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1038">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1039">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1039">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1040">L’exemple suivant montre comment utiliser LTRIM dans une requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-1040">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="abde8-1041">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1041">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="abde8-1042"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="abde8-1042"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="abde8-1043">Remplace toutes les occurrences d’une valeur de chaîne spécifiée par une autre valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1043">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="abde8-1044">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1044">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="abde8-1045">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1045">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1046">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1046">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-1047">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1047">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1048">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1048">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1049">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1049">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1050">L’exemple suivant montre comment utiliser REPLACE dans une requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-1050">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="abde8-1051">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1051">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="abde8-1052"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="abde8-1052"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="abde8-1053">Répète une valeur de chaîne un nombre de fois spécifié.</span><span class="sxs-lookup"><span data-stu-id="abde8-1053">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="abde8-1054">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1054">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="abde8-1055">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1055">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1056">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1056">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="abde8-1057">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1057">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-1058">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1058">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1059">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1059">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1060">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1060">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1061">L’exemple suivant montre comment utiliser REPLICATE dans une requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-1061">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="abde8-1062">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1062">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="abde8-1063"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="abde8-1063"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="abde8-1064">Retourne l’ordre inverse d’une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1064">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="abde8-1065">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1065">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="abde8-1066">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1066">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1067">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1067">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-1068">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1068">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1069">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1069">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1070">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1070">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1071">L’exemple suivant montre comment utiliser REVERSE dans une requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-1071">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="abde8-1072">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1072">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="abde8-1073"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="abde8-1073"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="abde8-1074">Retourne la partie droite d’une chaîne avec le nombre de caractères spécifié.</span><span class="sxs-lookup"><span data-stu-id="abde8-1074">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="abde8-1075">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1075">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="abde8-1076">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1076">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1077">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1077">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="abde8-1078">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1078">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-1079">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1079">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1080">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1080">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1081">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1081">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1082">L’exemple suivant retourne la partie droite de « abc » pour différentes valeurs de longueur.</span><span class="sxs-lookup"><span data-stu-id="abde8-1082">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="abde8-1083">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1083">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="abde8-1084"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="abde8-1084"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="abde8-1085">Retourne une expression de chaîne après avoir supprimé les espaces de fin.</span><span class="sxs-lookup"><span data-stu-id="abde8-1085">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="abde8-1086">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1086">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="abde8-1087">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1087">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1088">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1088">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-1089">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1089">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1090">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1090">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1091">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1091">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1092">L’exemple suivant montre comment utiliser RTRIM dans une requête.</span><span class="sxs-lookup"><span data-stu-id="abde8-1092">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="abde8-1093">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1093">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="abde8-1094"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="abde8-1094"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="abde8-1095">Retourne une valeur booléenne indiquant si la première expression de chaîne commence par la seconde.</span><span class="sxs-lookup"><span data-stu-id="abde8-1095">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="abde8-1096">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1096">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="abde8-1097">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1097">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1098">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1098">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-1099">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1099">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1100">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1100">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-1101">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1101">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1102">L’exemple suivant vérifie si la chaîne « abc » commence par « b » et « a ».</span><span class="sxs-lookup"><span data-stu-id="abde8-1102">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="abde8-1103">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1103">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="abde8-1104"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="abde8-1104"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="abde8-1105">Renvoie une partie d’une expression de chaîne commençant à la position de caractère spécifiée (avec base zéro) et se poursuit jusqu'à la longueur spécifiée ou à la fin de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1105">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="abde8-1106">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1106">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="abde8-1107">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1107">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1108">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1108">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="abde8-1109">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1109">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-1110">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1110">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1111">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1111">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1112">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1112">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1113">L’exemple suivant retourne la sous-chaîne de « abc » commençant à 1 pour une longueur de 1 caractère.</span><span class="sxs-lookup"><span data-stu-id="abde8-1113">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="abde8-1114">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1114">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="abde8-1115"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="abde8-1115"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="abde8-1116">Retourne une expression de chaîne après la conversion des caractères minuscules en caractères majuscules.</span><span class="sxs-lookup"><span data-stu-id="abde8-1116">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="abde8-1117">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1117">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="abde8-1118">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1118">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="abde8-1119">Peut être toute expression de chaîne valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1119">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="abde8-1120">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1120">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1121">Retourne une expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1121">Returns a string expression.</span></span>  
  
 <span data-ttu-id="abde8-1122">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1122">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1123">L’exemple suivant explique comment utiliser UPPER dans une requête</span><span class="sxs-lookup"><span data-stu-id="abde8-1123">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="abde8-1124">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1124">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="abde8-1125"><a name="bk_array_functions"></a> Fonctions de tableau</span><span class="sxs-lookup"><span data-stu-id="abde8-1125"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="abde8-1126">Les fonctions scalaires suivantes effectuent une opération sur une valeur d’entrée de tableau et retournent une valeur numérique, une valeur booléenne ou une valeur de tableau</span><span class="sxs-lookup"><span data-stu-id="abde8-1126">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="abde8-1127">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="abde8-1127">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="abde8-1128">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="abde8-1128">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="abde8-1129">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="abde8-1129">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="abde8-1130">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="abde8-1130">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="abde8-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="abde8-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="abde8-1132">Retourne un tableau qui est le résultat de la concaténation d’au moins deux valeurs de tableau.</span><span class="sxs-lookup"><span data-stu-id="abde8-1132">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="abde8-1133">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1133">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="abde8-1134">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1134">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="abde8-1135">Peut être toute expression de tableau valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1135">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="abde8-1136">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1136">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1137">Retourne une expression de tableau.</span><span class="sxs-lookup"><span data-stu-id="abde8-1137">Returns an array expression.</span></span>  
  
 <span data-ttu-id="abde8-1138">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1138">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1139">L’exemple suivant montre comment concaténer deux tableaux.</span><span class="sxs-lookup"><span data-stu-id="abde8-1139">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="abde8-1140">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1140">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="abde8-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="abde8-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="abde8-1142">Retourne une valeur booléenne qui indique si le tableau contient la valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-1142">Returns a Boolean indicating whether the array contains the specified value.</span></span>  
  
 <span data-ttu-id="abde8-1143">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1143">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="abde8-1144">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1144">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="abde8-1145">Peut être toute expression de tableau valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1145">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="abde8-1146">Peut être toute expression valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1146">Is any valid expression.</span></span>  
  
 <span data-ttu-id="abde8-1147">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1147">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1148">Retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1148">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="abde8-1149">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1149">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1150">L’exemple suivant montre comment vérifier l’appartenance à un tableau avec ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="abde8-1150">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="abde8-1151">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1151">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="abde8-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="abde8-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="abde8-1153">Retourne le nombre d’éléments de l’expression de tableau spécifiée.</span><span class="sxs-lookup"><span data-stu-id="abde8-1153">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="abde8-1154">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1154">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="abde8-1155">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1155">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="abde8-1156">Peut être toute expression de tableau valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1156">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="abde8-1157">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1157">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1158">Renvoie une expression numérique.</span><span class="sxs-lookup"><span data-stu-id="abde8-1158">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-1159">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1159">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1160">L’exemple suivant comment obtenir la longueur d’un tableau avec ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="abde8-1160">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="abde8-1161">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1161">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="abde8-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="abde8-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="abde8-1163">Retourne une partie d’une expression de tableau.</span><span class="sxs-lookup"><span data-stu-id="abde8-1163">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="abde8-1164">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1164">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="abde8-1165">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1165">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="abde8-1166">Peut être toute expression de tableau valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1166">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="abde8-1167">Est une expression numérique valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1167">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="abde8-1168">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1168">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1169">Retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1169">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="abde8-1170">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1170">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1171">L’exemple suivant comment obtenir une partie d’un tableau avec ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="abde8-1171">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="abde8-1172">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1172">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="abde8-1173"><a name="bk_spatial_functions"></a> Fonctions spatiales</span><span class="sxs-lookup"><span data-stu-id="abde8-1173"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="abde8-1174">Les fonctions scalaires suivantes effectuent une opération sur une valeur d’entrée de chaîne et retournent une valeur d’entrée d’objet spatial, une valeur numérique ou une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1174">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="abde8-1175">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="abde8-1175">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="abde8-1176">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="abde8-1176">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="abde8-1177">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="abde8-1177">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="abde8-1178">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="abde8-1178">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="abde8-1179">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="abde8-1179">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="abde8-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="abde8-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="abde8-1181">Retourne la distance entre les deux expressions Point, Polygone ou LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="abde8-1181">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="abde8-1182">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1182">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="abde8-1183">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1183">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="abde8-1184">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1184">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="abde8-1185">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1185">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1186">Retourne une expression numérique contenant la distance.</span><span class="sxs-lookup"><span data-stu-id="abde8-1186">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="abde8-1187">Elle est exprimée en mètres pour le système de référence par défaut.</span><span class="sxs-lookup"><span data-stu-id="abde8-1187">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="abde8-1188">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1188">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1189">L’exemple suivant vous montre comment retourner tous les documents de famille se trouvant dans un rayon de 30 kilomètres de l'emplacement spécifié à l'aide de la fonction intégrée ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="abde8-1189">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="abde8-1190">.</span><span class="sxs-lookup"><span data-stu-id="abde8-1190">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="abde8-1191">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1191">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="abde8-1192"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="abde8-1192"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="abde8-1193">Retourne une expression booléenne indiquant si l’objet GeoJSON (Point, Polygone ou LineString) spécifié dans le premier argument se trouve dans le GeoJSON (Point, Polygone ou LineString) du deuxième argument.</span><span class="sxs-lookup"><span data-stu-id="abde8-1193">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="abde8-1194">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1194">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="abde8-1195">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1195">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="abde8-1196">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1196">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="abde8-1197">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="abde8-1198">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1198">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1199">Retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1199">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="abde8-1200">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1200">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1201">L’exemple suivant montre comment rechercher tous les documents de famille d’un polygone avec ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="abde8-1201">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="abde8-1202">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1202">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="abde8-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="abde8-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="abde8-1204">Retourne une expression booléenne indiquant si l’objet GeoJSON (Point, Polygon ou LineString) spécifié dans le premier argument croise le GeoJSON (Point, Polygon ou LineString) du deuxième argument.</span><span class="sxs-lookup"><span data-stu-id="abde8-1204">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="abde8-1205">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1205">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="abde8-1206">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1206">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="abde8-1207">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1207">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="abde8-1208">Est toute expression d’objet GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="abde8-1209">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1209">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1210">Retourne une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1210">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="abde8-1211">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1211">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1212">L’exemple suivant montre comment rechercher toutes les zones ayant une intersection avec le polygone donné.</span><span class="sxs-lookup"><span data-stu-id="abde8-1212">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="abde8-1213">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1213">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="abde8-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="abde8-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="abde8-1215">Renvoie une valeur booléenne indiquant si l’expression Point, Polygone ou LineString GeoJSON spécifiée est valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1215">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="abde8-1216">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1216">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="abde8-1217">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1217">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="abde8-1218">Est toute expression GeoJSON Point, Polygon ou LineString valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1218">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="abde8-1219">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1219">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1220">Retourne une expression booléenne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1220">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="abde8-1221">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1221">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1222">L’exemple suivant montre comment vérifier si un point est valide avec ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="abde8-1222">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="abde8-1223">Par exemple, ce point a une valeur de latitude qui n’est pas dans la plage valide de valeurs [-90, 90]. Par conséquent, la requête retourne false.</span><span class="sxs-lookup"><span data-stu-id="abde8-1223">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="abde8-1224">La spécification GeoJSON impose que, pour les polygones, la dernière paire de coordonnées fournie soit identique à la première, pour créer une forme fermée.</span><span class="sxs-lookup"><span data-stu-id="abde8-1224">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="abde8-1225">Les points dans un polygone doivent être spécifiés dans le sens antihoraire.</span><span class="sxs-lookup"><span data-stu-id="abde8-1225">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="abde8-1226">Un polygone spécifié dans le sens horaire représente l'inverse de la région qu'il contient.</span><span class="sxs-lookup"><span data-stu-id="abde8-1226">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="abde8-1227">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1227">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="abde8-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="abde8-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="abde8-1229">Renvoie une valeur JSON contenant une valeur booléenne si l’expression Point, Polygone ou LineString GeoJSON spécifiée est valide et, dans le cas contraire, le motif sous forme de valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1229">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="abde8-1230">**Syntaxe**</span><span class="sxs-lookup"><span data-stu-id="abde8-1230">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="abde8-1231">**Arguments**</span><span class="sxs-lookup"><span data-stu-id="abde8-1231">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="abde8-1232">Peut être toute expression GeoJSON Point ou Polygon valide.</span><span class="sxs-lookup"><span data-stu-id="abde8-1232">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="abde8-1233">**Types de retour**</span><span class="sxs-lookup"><span data-stu-id="abde8-1233">**Return Types**</span></span>  
  
 <span data-ttu-id="abde8-1234">Renvoie une valeur JSON contenant une valeur booléenne si l'expression de points ou de polygones GeoJSON spécifiée est valide et si elle est non valide, le motif sous forme de valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="abde8-1234">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="abde8-1235">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="abde8-1235">**Examples**</span></span>  
  
 <span data-ttu-id="abde8-1236">L’exemple suivant montre comment vérifier la validité (avec détails) avec ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="abde8-1236">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="abde8-1237">Voici le jeu de résultats obtenu.</span><span class="sxs-lookup"><span data-stu-id="abde8-1237">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="abde8-1238">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="abde8-1238">Next steps</span></span>  
 <span data-ttu-id="abde8-1239">[Syntaxe SQL et requête SQL pour Azure Cosmos DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="abde8-1239">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="abde8-1240">Documentation Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="abde8-1240">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
