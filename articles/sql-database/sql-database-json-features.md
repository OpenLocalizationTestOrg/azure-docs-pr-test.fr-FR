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
# <a name="getting-started-with-json-features-in-azure-sql-database"></a>Prise en main des fonctionnalités JSON dans Base de données SQL Azure
Base de données SQL Azure vous permet d’analyser et d’interroger des données représentées au format JavaScript Object Notation [(JSON)](http://www.json.org/) , et d’exporter vos données relationnelles en tant que texte JSON.

JSON est un format de données largement répandu, utilisé pour l’échange de données dans des applications mobiles et web modernes. JSON est également utilisé pour stocker des données semi-structurées dans des fichiers journaux ou des bases de données NoSQL, par exemple [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/). De nombreux services web REST retournent des résultats au format de texte JSON, ou acceptent des données au format JSON. La plupart des services Azure tels que [Recherche Azure](https://azure.microsoft.com/services/search/), [Stockage Azure](https://azure.microsoft.com/services/storage/) et [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) ont des points de terminaison REST qui renvoient ou utilisent des données JSON.

Base de données SQL Azure vous permet de travailler facilement avec des données JSON, et d’intégrer votre base de données avec des services modernes.

## <a name="overview"></a>Vue d'ensemble
Base de données SQL Azure fournit hello suivant des fonctions permettant de travailler avec des données JSON :

![Fonctions JSON](./media/sql-database-json-features/image_1.png)

Si vous avez un texte JSON, vous pouvez extraire des données à partir de JSON ou vérifiez que JSON est correctement formaté à l’aide des fonctions intégrées hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), et [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) . Hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) fonction vous permet de mettre à jour la valeur à l’intérieur du texte JSON. Pour des opérations d’interrogation et d’analyse plus avancées, la fonction [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) peut transformer un tableau d’objets JSON en un ensemble de lignes. Toute requête SQL peut être exécutée sur hello retourné de jeu de résultats. Enfin, il existe une clause [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) qui vous permet de convertir les données stockées dans vos tables relationnelles au format de texte JSON.

## <a name="formatting-relational-data-in-json-format"></a>Conversion de données relationnelles au format JSON
Si vous avez un service web que prend de couche de données à partir de la base de données hello et fournissant une réponse au format JSON de format ou les infrastructures JavaScript côté client ou les bibliothèques qui acceptent des données au format JSON, vous pouvez mettre en forme le contenu de votre base de données au format JSON directement dans une requête SQL. Vous n’avez plus avez le code d’application toowrite qui met en forme les résultats à partir de la base de données SQL Azure au format JSON, ou à incluez des résultats de requête sous forme de tableau JSON sérialisation bibliothèque tooconvert et puis Sérialisez le format de tooJSON d’objets. Au lieu de cela, vous pouvez utiliser hello pour les résultats de la requête SQL tooformat clause JSON au format JSON dans la base de données SQL Azure et utiliser directement dans votre application.

Bonjour l’exemple suivant, les lignes à partir de la table Sales.Customer hello sont au format JSON à l’aide de hello clause FOR JSON :

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

clause FOR JSON PATH de Hello met en forme des résultats de requête de hello hello sous forme de texte JSON. Les noms de colonne sont utilisées comme clés, alors que les valeurs de cellule hello sont générées en tant que valeurs JSON :

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

jeu de résultats Hello est mise en forme en tant que tableau JSON où chaque ligne est mise en forme en tant qu’objet JSON distinct.

Chemin d’accès indique que vous pouvez personnaliser le format de sortie hello de votre résultat de JSON à l’aide de la notation par points dans l’alias de colonne. Bonjour, suivant la requête modifie nom hello de clé « CustomerName » de hello au format JSON de sortie hello et place les numéros de téléphone et de télécopie dans le sous-objet « Contact » hello :

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

sortie Hello de cette requête ressemble à ceci :

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

Dans cet exemple, nous retourner un seul objet JSON au lieu d’un tableau en spécifiant des hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option. Vous pouvez utiliser cette option si vous savez que vous retournez un objet unique en tant que résultat de requête.

valeur principale Hello hello clause FOR JSON est qu’il vous permet de renvoyer des données hiérarchiques complexes à partir de votre base de données sous la forme des objets JSON imbriquées ou des tableaux. Hello suivant montre l’exemple comment tooinclude commandes appartenant toohello client sous forme de tableau imbriqué de commandes :

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

Au lieu d’envoyer les données de client tooget des requêtes distinctes, puis toofetch une liste des commandes associées, vous pouvez obtenir toutes les données nécessaires hello avec une requête unique, comme indiqué dans hello suivant l’exemple de sortie :

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

## <a name="working-with-json-data"></a>Utilisation de données JSON
Si vous n’avez des données structurées strictement, si vous avez des sous-objets complexes, des tableaux ou des données hiérarchiques, ou si vos structures de données au fil du temps, format JSON hello peut vous aider à toorepresent toute structure de données complexes.

JSON est un format texte utilisable comme tout autre type de chaîne dans Base de données SQL Azure. Vous pouvez envoyer ou stocker des données JSON en tant que type NVARCHAR standard :

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

Hello données JSON utilisées dans cet exemple est représentée à l’aide de type nvarchar (max) de hello. JSON peut être inséré dans cette table ou fourni en tant qu’argument de procédure stockée hello à l’aide de la syntaxe Transact-SQL standard comme dans hello l’exemple suivant :

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

Tout langage ou bibliothèque côté client qui fonctionne avec des données de chaîne dans Base de données SQL Azure fonctionne également avec des données JSON. JSON peut être stocké dans une table qui prend en charge le type NVARCHAR hello, par exemple une table mémoire optimisée ou une table avec version système. JSON n’introduit pas de toute contrainte dans le code côté client hello ou dans la couche de base de données hello.

## <a name="querying-json-data"></a>Interrogation de données JSON
Si vous avez des données au format JSON stockées dans des tables SQL Azure, les fonctions JSON vous permettent d’utiliser ces données dans n’importe quelle requête SQL.

Les fonctions JSON disponibles dans Base de données SQL Azure vous permettent de traiter des données au format JSON comme tout autre type de données SQL. Vous pouvez facilement extraire les valeurs de texte JSON de hello et utiliser des données JSON dans n’importe quelle requête :

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

Hello fonction JSON_VALUE extrait une valeur de texte JSON stocké dans la colonne de données hello. Cette fonction utilise un chemin d’accès de type JavaScript de tooreference une valeur tooextract de texte JSON. valeur de Hello extrait peut être utilisée dans n’importe quelle partie de la requête SQL.

Hello fonction JSON_QUERY est tooJSON_VALUE similaire. Contrairement à la fonction JSON_VALUE, cette fonction extrait un sous-objet complexe, tel qu’un tableau ou un objet placés dans le texte JSON.

fonction JSON_MODIFY de Hello vous permet de spécifier le chemin d’accès de hello de valeur de hello dans un texte JSON hello qui doit être mis à jour, ainsi que d’une nouvelle valeur qui remplacera hello ancien. Cette façon vous pouvez facilement mettre à jour un texte JSON sans analyse l’intégralité de la structure hello.

Étant donné que JSON est stocké dans un fichier texte standard, il n’existe aucune garantie que les valeurs hello stockées dans des colonnes de texte sont correctement mis en forme. Vous pouvez vérifier que le texte stocké dans la colonne JSON est correctement formaté à l’aide des contraintes de validation de base de données SQL Azure et hello fonction ISJSON standard :

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

Si le texte d’entrée hello est correctement formaté JSON, hello fonction ISJSON retourne la valeur de hello 1. À chaque insertion ou mise à jour de la colonne JSON, cette contrainte vérifie que nouvelle valeur de texte n’est pas dans du JSON mal formé.

## <a name="transforming-json-into-tabular-format"></a>Conversion de JSON en format tabulaire
Base de données SQL Azure vous permet également de convertir des collections JSON en format tabulaire, ainsi que de charger ou d’interroger des données JSON.

OPENJSON est une fonction table qui analyse le texte JSON, localise un tableau d’objets JSON, itère au sein des éléments de hello du tableau de hello et renvoie une ligne de résultat de la sortie pour chaque élément du tableau de hello hello.

![Format tabulaire JSON](./media/sql-database-json-features/image_2.png)

Dans l’exemple hello ci-dessus, nous pouvons spécifier où toolocate hello tableau JSON doit être ouvert (dans $ hello. Chemin d’accès de commandes), les colonnes doivent être retournés comme résultat, et où toofind hello valeurs JSON qui seront renvoyés en tant que cellules.

Nous pouvons transformer un tableau JSON Bonjour @orders variable dans un ensemble de lignes, analyser ce jeu de résultats, ou insérer des lignes dans une table standard :

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
collection Hello de commandes la forme d’un tableau JSON et fourni comme une procédure stockée de toohello de paramètre peut être analysée et insérée dans la table de commandes hello.

## <a name="next-steps"></a>Étapes suivantes
toolearn comment toointegrate JSON dans votre application, passez en revue ces ressources :

* [Blog TechNet](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [Documentation MSDN](https://msdn.microsoft.com/library/dn921897.aspx)
* [Vidéo Channel 9](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

toolearn sur les différents scénarios d’intégration de JSON dans votre application, consultez les démonstrations hello dans ce [vidéo de Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) ou un scénario qui correspond à votre cas d’usage dans [billets de Blog de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).

