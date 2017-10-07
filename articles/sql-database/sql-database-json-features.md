---
title: "fonctionnalités de JSON de base de données SQL aaaAzure | Documents Microsoft"
description: "Base de données SQL Azure vous permet de tooparse, de requête et des données au format de notation de JavaScript Objet Notation (JSON)."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="87687-103">Prise en main des fonctionnalités JSON dans Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="87687-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="87687-104">Base de données SQL Azure vous permet d’analyser et d’interroger des données représentées au format JavaScript Object Notation [(JSON)](http://www.json.org/) , et d’exporter vos données relationnelles en tant que texte JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="87687-105">JSON est un format de données largement répandu, utilisé pour l’échange de données dans des applications mobiles et web modernes.</span><span class="sxs-lookup"><span data-stu-id="87687-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="87687-106">JSON est également utilisé pour stocker des données semi-structurées dans des fichiers journaux ou des bases de données NoSQL, par exemple [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="87687-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="87687-107">De nombreux services web REST retournent des résultats au format de texte JSON, ou acceptent des données au format JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="87687-108">La plupart des services Azure tels que [Recherche Azure](https://azure.microsoft.com/services/search/), [Stockage Azure](https://azure.microsoft.com/services/storage/) et [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) ont des points de terminaison REST qui renvoient ou utilisent des données JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="87687-109">Base de données SQL Azure vous permet de travailler facilement avec des données JSON, et d’intégrer votre base de données avec des services modernes.</span><span class="sxs-lookup"><span data-stu-id="87687-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="87687-110">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="87687-110">Overview</span></span>
<span data-ttu-id="87687-111">Base de données SQL Azure fournit hello suivant des fonctions permettant de travailler avec des données JSON :</span><span class="sxs-lookup"><span data-stu-id="87687-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![Fonctions JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="87687-113">Si vous avez un texte JSON, vous pouvez extraire des données à partir de JSON ou vérifiez que JSON est correctement formaté à l’aide des fonctions intégrées hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), et [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) .</span><span class="sxs-lookup"><span data-stu-id="87687-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="87687-114">Hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) fonction vous permet de mettre à jour la valeur à l’intérieur du texte JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="87687-115">Pour des opérations d’interrogation et d’analyse plus avancées, la fonction [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) peut transformer un tableau d’objets JSON en un ensemble de lignes.</span><span class="sxs-lookup"><span data-stu-id="87687-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="87687-116">Toute requête SQL peut être exécutée sur hello retourné de jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="87687-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="87687-117">Enfin, il existe une clause [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) qui vous permet de convertir les données stockées dans vos tables relationnelles au format de texte JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="87687-118">Conversion de données relationnelles au format JSON</span><span class="sxs-lookup"><span data-stu-id="87687-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="87687-119">Si vous avez un service web que prend de couche de données à partir de la base de données hello et fournissant une réponse au format JSON de format ou les infrastructures JavaScript côté client ou les bibliothèques qui acceptent des données au format JSON, vous pouvez mettre en forme le contenu de votre base de données au format JSON directement dans une requête SQL.</span><span class="sxs-lookup"><span data-stu-id="87687-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="87687-120">Vous n’avez plus avez le code d’application toowrite qui met en forme les résultats à partir de la base de données SQL Azure au format JSON, ou à incluez des résultats de requête sous forme de tableau JSON sérialisation bibliothèque tooconvert et puis Sérialisez le format de tooJSON d’objets.</span><span class="sxs-lookup"><span data-stu-id="87687-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="87687-121">Au lieu de cela, vous pouvez utiliser hello pour les résultats de la requête SQL tooformat clause JSON au format JSON dans la base de données SQL Azure et utiliser directement dans votre application.</span><span class="sxs-lookup"><span data-stu-id="87687-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="87687-122">Bonjour l’exemple suivant, les lignes à partir de la table Sales.Customer hello sont au format JSON à l’aide de hello clause FOR JSON :</span><span class="sxs-lookup"><span data-stu-id="87687-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="87687-123">clause FOR JSON PATH de Hello met en forme des résultats de requête de hello hello sous forme de texte JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="87687-124">Les noms de colonne sont utilisées comme clés, alors que les valeurs de cellule hello sont générées en tant que valeurs JSON :</span><span class="sxs-lookup"><span data-stu-id="87687-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="87687-125">jeu de résultats Hello est mise en forme en tant que tableau JSON où chaque ligne est mise en forme en tant qu’objet JSON distinct.</span><span class="sxs-lookup"><span data-stu-id="87687-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="87687-126">Chemin d’accès indique que vous pouvez personnaliser le format de sortie hello de votre résultat de JSON à l’aide de la notation par points dans l’alias de colonne.</span><span class="sxs-lookup"><span data-stu-id="87687-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="87687-127">Bonjour, suivant la requête modifie nom hello de clé « CustomerName » de hello au format JSON de sortie hello et place les numéros de téléphone et de télécopie dans le sous-objet « Contact » hello :</span><span class="sxs-lookup"><span data-stu-id="87687-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="87687-128">sortie Hello de cette requête ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="87687-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="87687-129">Dans cet exemple, nous retourner un seul objet JSON au lieu d’un tableau en spécifiant des hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span><span class="sxs-lookup"><span data-stu-id="87687-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="87687-130">Vous pouvez utiliser cette option si vous savez que vous retournez un objet unique en tant que résultat de requête.</span><span class="sxs-lookup"><span data-stu-id="87687-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="87687-131">valeur principale Hello hello clause FOR JSON est qu’il vous permet de renvoyer des données hiérarchiques complexes à partir de votre base de données sous la forme des objets JSON imbriquées ou des tableaux.</span><span class="sxs-lookup"><span data-stu-id="87687-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="87687-132">Hello suivant montre l’exemple comment tooinclude commandes appartenant toohello client sous forme de tableau imbriqué de commandes :</span><span class="sxs-lookup"><span data-stu-id="87687-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="87687-133">Au lieu d’envoyer les données de client tooget des requêtes distinctes, puis toofetch une liste des commandes associées, vous pouvez obtenir toutes les données nécessaires hello avec une requête unique, comme indiqué dans hello suivant l’exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="87687-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a><span data-ttu-id="87687-134">Utilisation de données JSON</span><span class="sxs-lookup"><span data-stu-id="87687-134">Working with JSON data</span></span>
<span data-ttu-id="87687-135">Si vous n’avez des données structurées strictement, si vous avez des sous-objets complexes, des tableaux ou des données hiérarchiques, ou si vos structures de données au fil du temps, format JSON hello peut vous aider à toorepresent toute structure de données complexes.</span><span class="sxs-lookup"><span data-stu-id="87687-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="87687-136">JSON est un format texte utilisable comme tout autre type de chaîne dans Base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="87687-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="87687-137">Vous pouvez envoyer ou stocker des données JSON en tant que type NVARCHAR standard :</span><span class="sxs-lookup"><span data-stu-id="87687-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

<span data-ttu-id="87687-138">Hello données JSON utilisées dans cet exemple est représentée à l’aide de type nvarchar (max) de hello.</span><span class="sxs-lookup"><span data-stu-id="87687-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="87687-139">JSON peut être inséré dans cette table ou fourni en tant qu’argument de procédure stockée hello à l’aide de la syntaxe Transact-SQL standard comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="87687-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="87687-140">Tout langage ou bibliothèque côté client qui fonctionne avec des données de chaîne dans Base de données SQL Azure fonctionne également avec des données JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="87687-141">JSON peut être stocké dans une table qui prend en charge le type NVARCHAR hello, par exemple une table mémoire optimisée ou une table avec version système.</span><span class="sxs-lookup"><span data-stu-id="87687-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="87687-142">JSON n’introduit pas de toute contrainte dans le code côté client hello ou dans la couche de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="87687-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="87687-143">Interrogation de données JSON</span><span class="sxs-lookup"><span data-stu-id="87687-143">Querying JSON data</span></span>
<span data-ttu-id="87687-144">Si vous avez des données au format JSON stockées dans des tables SQL Azure, les fonctions JSON vous permettent d’utiliser ces données dans n’importe quelle requête SQL.</span><span class="sxs-lookup"><span data-stu-id="87687-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="87687-145">Les fonctions JSON disponibles dans Base de données SQL Azure vous permettent de traiter des données au format JSON comme tout autre type de données SQL.</span><span class="sxs-lookup"><span data-stu-id="87687-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="87687-146">Vous pouvez facilement extraire les valeurs de texte JSON de hello et utiliser des données JSON dans n’importe quelle requête :</span><span class="sxs-lookup"><span data-stu-id="87687-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="87687-147">Hello fonction JSON_VALUE extrait une valeur de texte JSON stocké dans la colonne de données hello.</span><span class="sxs-lookup"><span data-stu-id="87687-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="87687-148">Cette fonction utilise un chemin d’accès de type JavaScript de tooreference une valeur tooextract de texte JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="87687-149">valeur de Hello extrait peut être utilisée dans n’importe quelle partie de la requête SQL.</span><span class="sxs-lookup"><span data-stu-id="87687-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="87687-150">Hello fonction JSON_QUERY est tooJSON_VALUE similaire.</span><span class="sxs-lookup"><span data-stu-id="87687-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="87687-151">Contrairement à la fonction JSON_VALUE, cette fonction extrait un sous-objet complexe, tel qu’un tableau ou un objet placés dans le texte JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="87687-152">fonction JSON_MODIFY de Hello vous permet de spécifier le chemin d’accès de hello de valeur de hello dans un texte JSON hello qui doit être mis à jour, ainsi que d’une nouvelle valeur qui remplacera hello ancien.</span><span class="sxs-lookup"><span data-stu-id="87687-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="87687-153">Cette façon vous pouvez facilement mettre à jour un texte JSON sans analyse l’intégralité de la structure hello.</span><span class="sxs-lookup"><span data-stu-id="87687-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="87687-154">Étant donné que JSON est stocké dans un fichier texte standard, il n’existe aucune garantie que les valeurs hello stockées dans des colonnes de texte sont correctement mis en forme.</span><span class="sxs-lookup"><span data-stu-id="87687-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="87687-155">Vous pouvez vérifier que le texte stocké dans la colonne JSON est correctement formaté à l’aide des contraintes de validation de base de données SQL Azure et hello fonction ISJSON standard :</span><span class="sxs-lookup"><span data-stu-id="87687-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="87687-156">Si le texte d’entrée hello est correctement formaté JSON, hello fonction ISJSON retourne la valeur de hello 1.</span><span class="sxs-lookup"><span data-stu-id="87687-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="87687-157">À chaque insertion ou mise à jour de la colonne JSON, cette contrainte vérifie que nouvelle valeur de texte n’est pas dans du JSON mal formé.</span><span class="sxs-lookup"><span data-stu-id="87687-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="87687-158">Conversion de JSON en format tabulaire</span><span class="sxs-lookup"><span data-stu-id="87687-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="87687-159">Base de données SQL Azure vous permet également de convertir des collections JSON en format tabulaire, ainsi que de charger ou d’interroger des données JSON.</span><span class="sxs-lookup"><span data-stu-id="87687-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="87687-160">OPENJSON est une fonction table qui analyse le texte JSON, localise un tableau d’objets JSON, itère au sein des éléments de hello du tableau de hello et renvoie une ligne de résultat de la sortie pour chaque élément du tableau de hello hello.</span><span class="sxs-lookup"><span data-stu-id="87687-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![Format tabulaire JSON](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="87687-162">Dans l’exemple hello ci-dessus, nous pouvons spécifier où toolocate hello tableau JSON doit être ouvert (dans $ hello. Chemin d’accès de commandes), les colonnes doivent être retournés comme résultat, et où toofind hello valeurs JSON qui seront renvoyés en tant que cellules.</span><span class="sxs-lookup"><span data-stu-id="87687-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="87687-163">Nous pouvons transformer un tableau JSON Bonjour @orders variable dans un ensemble de lignes, analyser ce jeu de résultats, ou insérer des lignes dans une table standard :</span><span class="sxs-lookup"><span data-stu-id="87687-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
<span data-ttu-id="87687-164">collection Hello de commandes la forme d’un tableau JSON et fourni comme une procédure stockée de toohello de paramètre peut être analysée et insérée dans la table de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="87687-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87687-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87687-165">Next steps</span></span>
<span data-ttu-id="87687-166">toolearn comment toointegrate JSON dans votre application, passez en revue ces ressources :</span><span class="sxs-lookup"><span data-stu-id="87687-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="87687-167">Blog TechNet</span><span class="sxs-lookup"><span data-stu-id="87687-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="87687-168">Documentation MSDN</span><span class="sxs-lookup"><span data-stu-id="87687-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="87687-169">Vidéo Channel 9</span><span class="sxs-lookup"><span data-stu-id="87687-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="87687-170">toolearn sur les différents scénarios d’intégration de JSON dans votre application, consultez les démonstrations hello dans ce [vidéo de Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) ou un scénario qui correspond à votre cas d’usage dans [billets de Blog de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="87687-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

