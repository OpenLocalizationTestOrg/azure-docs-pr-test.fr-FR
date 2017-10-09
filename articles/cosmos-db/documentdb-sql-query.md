---
title: "requêtes aaaSQL pour l’API Azure Cosmos DB DocumentDB | Documents Microsoft"
description: "Obtenez plus d’informations sur la syntaxe SQL, les concepts de bases de données et les requêtes SQL pour Azure Cosmos DB. SQL peut être utilisé comme un langage de requête JSON dans Azure Cosmos DB."
keywords: "syntaxe sql, requête sql, requêtes sql, langage de requête json, concepts de bases de données, requêtes sql et fonctions agrégées"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>Requêtes SQL pour l’API DocumentDB Azure Cosmos DB
Microsoft Azure Cosmos DB prend en charge l’interrogation de documents à l’aide du langage SQL en tant que langage de requête JSON. Cosmos DB n’utilise pas de schéma. En vertu de son engagement toohello JSON modèle de données directement dans le moteur de base de données hello, il fournit l’indexation automatique des documents JSON sans schéma explicite ou la création d’index secondaires. 

Lors de la conception du langage de requête hello pour Cosmos DB, nous avions deux objectifs à l’esprit :

* Au lieu d’un nouveau langage de requête JSON à inventer, nous voulions toosupport SQL. SQL est un des langages de requête plus populaires et familiers hello. Le langage SQL de Cosmos DB fournit un modèle de programmation formel pour créer des requêtes élaborées sur les documents JSON.
* Comme une base de document JSON est capable d’exécuter JavaScript directement dans le moteur de base de données hello, nous voulions modèle de programmation de toouse JavaScript en tant que base de hello pour le langage de requête. Hello DocumentDB API SQL racine se trouve dans le système de type de JavaScript, évaluation de l’expression et l’appel de fonction. En retour, cela fournit un modèle de programmation naturel pour les projections relationnelles, la navigation hiérarchique entre les documents JSON, les jointures réflexives, les requêtes spatiales et l’appel de fonctions définies par l’utilisateur écrites entièrement en JavaScript, entre autres fonctionnalités. 

Nous pensons que ces fonctionnalités sont friction de hello tooreducing clé entre l’application hello et la base de données hello et sont cruciale pour la productivité des développeurs.

Nous vous recommandons de mise en route en regardant hello suivant vidéo, où Aravind Ramachandran montre les fonctionnalités d’interrogation de base de données Cosmos et en vous rendant sur notre [Query Playground](http://www.documentdb.com/sql/demo), où vous pouvez essayer Cosmos DB et exécuter des requêtes SQL sur notre jeu de données.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

Ensuite, retourner l’article toothis, où nous commençons avec un didacticiel de requête SQL qui vous guide à travers certains documents JSON simples et les commandes SQL.

## <a id="GettingStarted"></a>Prise en main des commandes du langage SQL dans Cosmos DB
toosee Cosmos DB SQL au travail, nous allons commencer avec des documents JSON simples et suivre les étapes certaines requêtes simples. Prenez ces deux documents JSON relatifs à deux familles. Avec la base de données Cosmos, nous n’avez pas besoin toocreate les schémas ou un index secondaire explicitement. Nous suffit tooinsert hello JSON documents tooa Cosmos DB collection et de requête par la suite. Ici, nous avons JSON simple document pour hello famille de Andersen, hello parents, enfants (et leurs animaux), adresse et les informations d’inscription. document de Hello possède des chaînes, des nombres, des valeurs booléennes, des tableaux et des propriétés imbriquées. 

**Document**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

Voici un second document comportant une différence subtile : `givenName` et `familyName` sont utilisés au lieu de `firstName` et `lastName`.

**Document**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Désormais tentons des requêtes par rapport à cette toounderstand données hello certains aspects clés du DocumentDB API SQL. Par exemple, suivant de hello requête renvoie des documents hello où correspond au champ de code hello `AndersenFamily`. Dans la mesure où il s’agit d’un `SELECT *`, sortie hello de requête de hello est le document JSON complet hello :

**Requête**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Résultats**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


Considérez maintenant le cas de hello où nous devons tooreformat hello la sortie JSON dans une forme différente. Cette requête avec deux champs sélectionnés, nom et la ville, de l’objet projets un nouveau JSON quand des hello ville a hello même nom en tant qu’état de hello. Dans ce cas, « NY, NY » correspond.

**Requête**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**Résultats**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


les requêtes suivant Hello retourne tous les noms de donné de hello d’enfants dans la famille hello dont l’id correspond à `WakefieldFamily` classés par ville hello de résidence.

**Requête**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**Résultats**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


Nous aimerions tooa d’attention toodraw exemples hello que nous avons vu jusqu'à présent de langage de requête de quelques aspects dignes d’intérêt de hello Cosmos DB :  

* Comme le langage SQL de l’API DocumentDB fonctionne avec les valeurs JSON, il traite des entités d’arborescence au lieu des lignes et des colonnes. Par conséquent, langage de hello permet de faire référence toonodes d’arborescence hello à toute profondeur arbitraire, comme `Node1.Node2.Node3…..Nodem`, similaire toorelational SQL référence toohello deux référence de partie de `<table>.<column>`.   
* Hello structuré fonctionne de langage de requête avec des données sans schéma. Par conséquent, hello type système besoins toobe limite dynamiquement. Hello même expression peut produire des types différents sur des documents. résultat de Hello d’une requête est une valeur JSON valide, mais n’est pas garanti toobe d’un schéma fixe.  
* Cosmos DB prend uniquement en charge les documents JSON stricts. Cela signifie les expressions et système de type hello sont restreinte toodeal uniquement avec les types JSON. Consultez toohello [spécification JSON](http://www.json.org/) pour plus d’informations.  
* Une collection Cosmos DB est un conteneur sans schéma pour vos documents JSON. relations Hello dans les entités dans et entre des documents dans une collection de données sont implicitement capturées par la relation contenant-contenu et non par des relations de clé étrangères et de clé primaire. Il s’agit d’un aspect important de noter abordez jointures intra-document de hello présentés plus loin dans cet article.

## <a id="Indexing"></a> Indexation Cosmos DB
Avant de passer à hello syntaxe DocumentDB API SQL, il convient d’Explorer hello l’indexation de conception dans la base de données Cosmos. 

Hello d’index de base de données vise requêtes tooserve dans leurs diverses formes et les formes avec une consommation minimale des ressources (telles que l’UC et d’entrée/sortie) tout en fournissant un débit relativement élevé et une faible latence. Souvent, les choix hello de l’index de droit hello pour interroger une base de données nécessite beaucoup de planification et d’expérimentation. Cette approche présente une difficulté pour les bases de données sans schéma où les données de salutation tooa stricte de schéma n’est pas conforme et évoluent rapidement. 

Par conséquent, lorsque nous avons conçu sous-système d’indexation de hello Cosmos DB, nous avons défini hello suivant objectifs :

* Indexer les documents sans nécessiter de schéma : hello indexation sous-système ne pas exiger des informations de schéma ou faire d’hypothèses concernant les schémas de documents de hello. 
* Prend en charge pour les requêtes relationnelles et hiérarchiques efficaces et riches : hello index prend en charge le langage de requête Cosmos DB hello efficacement, y compris la prise en charge pour les projections relationnelles et hiérarchiques.
* Prise en charge pour les requêtes cohérents résister à un volume maintenu d’écritures : pour écriture haute débit les charges de travail avec des requêtes cohérents, hello index est mis à jour de façon incrémentielle, efficacement et en ligne en face de hello d’un volume maintenu d’écritures. mise à jour des index cohérent de Hello est cruciale tooserve les requêtes de hello au niveau de cohérence hello dans le service de document hello hello utilisateur configuré.
* Prise en charge d’une architecture mutualisée : Breakfast hello réservation-modèle de gouvernance des ressources locataires, mises à jour de l’index sont effectuées dans budget hello des ressources système (processeur, mémoire et les opérations d’entrée/sortie par seconde) allouée par le réplica. 
* L’efficacité du stockage : de rentabilité, stockage sur disque hello surcharge d’index de hello est limitée et prévisibles. Cela est essentiel car Cosmos DB permet hello développeur toomake basé sur coût compromis traitement des index dans les performances des requêtes toohello relation.  

Consultez toohello [exemples de base de données Azure Cosmos](https://github.com/Azure/azure-documentdb-net) sur MSDN pour obtenir des exemples montrant comment tooconfigure hello stratégie d’indexation pour une collection. Nous allons désormais obtenir les détails de hello de hello syntaxe SQL de base de données Azure Cosmos.

## <a id="Basics"></a>Principes de base d’une requête SQL Azure Cosmos DB
Chaque requête se compose d'une clause SELECT et de clauses FROM et WHERE facultatives conformes aux normes ANSI-SQL. En règle générale, pour chaque requête, source hello dans la clause FROM de hello est énuméré. Hello filtrer dans la clause WHERE est appliquée sur hello source tooretrieve de hello un sous-ensemble de documents JSON. Enfin, la clause SELECT de hello est utilisé tooproject hello demandé la liste de sélection de valeurs JSON dans hello.

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>Clause FROM
Hello `FROM <from_specification>` clause est facultative, sauf si la source de hello est filtrée ou projeté plus loin dans la requête de hello. objectif de Hello de cette clause est source de données toospecify hello sur quel hello requête doit fonctionner. Couramment ensemble de la collection hello est source de hello, mais on peut spécifier un sous-ensemble de la collection de hello à la place. 

Une requête comme `SELECT * FROM Families` indique que l’ensemble des familles hello est source de hello via le tooenumerate. Un identificateur spécial racine peut être la collection de hello toorepresent utilisé au lieu d’utiliser le nom de la collection hello. Hello liste suivante contient des hello règles qui sont appliquées par la requête :

* collection de Hello peut être un alias, tel que `SELECT f.id FROM Families AS f` ou simplement `SELECT f.id FROM Families f`. Ici `f` revient à hello `Families`. `AS`est un identificateur de hello tooalias mot clé facultatif.
* Une fois un alias, source d’origine de hello ne peut pas être lié. Par exemple, `SELECT Families.id FROM Families f` est syntaxiquement non valide, car l’identificateur hello « Familles » ne peut pas être résolu plus.
* Toutes les propriétés qui doivent toobe référencée doivent être qualifiées complet. En absence de hello de respect de la stricte de schéma, il s’agit de tooavoid appliqué toutes les liaisons ambiguës. Par conséquent, `SELECT id FROM Families f` est syntaxiquement incorrecte depuis la propriété de hello `id` n’est pas lié.

### <a name="subdocuments"></a>Sous-documents
Hello source peut également être réduite tooa plus petit sous-ensemble. Par exemple, tooenumerating uniquement une sous-arborescence dans chaque document, subroot de hello pourrait devenir puis hello source, comme indiqué dans hello l’exemple suivant :

**Requête**

    SELECT * 
    FROM Families.children

**Résultats**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

Est hello exemple ci-dessus a utilisé un tableau en tant que source de hello, un objet peut également servir en tant que source de hello, qui est ce que montre hello l’exemple suivant : toute valeur JSON valide (non définie) qui se trouvent dans la source de hello est pris en compte pour l’inclure dans le résultat de hello de requête de Hello. Si vous n’ont pas certaines familles un `address.state` valeur, elles sont exclues dans le résultat de la requête hello.

**Requête**

    SELECT * 
    FROM Families.address.state

**Résultats**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>Clause WHERE
Hello clause WHERE (**`WHERE <filter_condition>`**) est facultatif. Il spécifie hello condition que les documents JSON hello fournies par hello source doivent satisfaire toobe ordre inclus en tant que partie du résultat de hello. N’importe quel document JSON doit évaluer hello spécifié conditions trop « true » toobe pris en compte pour le résultat de hello. Hello où clause est utilisée par couche d’index hello dans l’ordre toodetermine hello absolu plus petit sous-ensemble de documents source qui peuvent faire partie du résultat de hello. 

Hello requête suivante demande des documents qui contiennent une propriété de nom dont la valeur est `AndersenFamily`. Tout autre document qui ne dispose pas d’une propriété de nom, ou lorsque la valeur de hello ne correspond pas à `AndersenFamily` est exclu. 

**Requête**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Résultats**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


Hello l’exemple précédent a montré une requête simple d’égalité. Le langage SQL de l’API DocumentDB prend également en charge plusieurs expressions scalaires. Hello couramment utilisé sont des expressions binaires et unaire. Références de propriété à partir de l’objet JSON hello source sont également des expressions valides. 

Hello après les opérateurs binaires est actuellement pris en charge et peut être utilisé dans les requêtes, comme indiqué dans hello exemple suivant :  

<table>
<tr>
<td>Opérateurs arithmétiques</td>    
<td>+,-,*,/,%</td>
</tr>
<tr>
<td>Opérateurs au niveau du bit</td>    
<td>|, &, ^, <<, >>, >>> (décalage vers la droite avec remplissage de zéros)</td>
</tr>
<tr>
<td>Opérateurs logiques</td>
<td>AND, OR, NOT</td>
</tr>
<tr>
<td>Opérateurs de comparaison</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>String</td>    
<td>|| (concaténer)</td>
</tr>
</table>  


Examinons certaines requêtes utilisant des opérateurs binaires.

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


Hello opérateurs unaires +,-, ~ pas sont également prises en charge et peut être utilisé dans des requêtes, comme indiqué dans hello l’exemple suivant :

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



En outre toobinary et les opérateurs unaires, des références de propriété sont également autorisées. Par exemple, `SELECT * FROM Families f WHERE f.isRegistered` renvoie hello document JSON qui contient la propriété de hello `isRegistered` où la valeur de la propriété hello est égal toohello JSON `true` valeur. Toutes les autres valeurs (false, null, non défini, `<number>`, `<string>`, `<object>`, `<array>`, etc.) entraîne le document de source toohello est exclu de résultat de hello. 

### <a name="equality-and-comparison-operators"></a>Opérateurs d'égalité et de comparaison
Hello tableau suivant montre les résultats hello de comparaisons d’égalité dans DocumentDB API SQL entre deux types JSON.

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>Op</strong>
         </td>
         <td valign="top">
            <strong>Undefined</strong>
         </td>
         <td valign="top">
            <strong>Null</strong>
         </td>
         <td valign="top">
            <strong>Boolean</strong>
         </td>
         <td valign="top">
            <strong>Number</strong>
         </td>
         <td valign="top">
            <strong>String</strong>
         </td>
         <td valign="top">
            <strong>Object</strong>
         </td>
         <td valign="top">
            <strong>Array</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Undefined<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Null<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Boolean<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Number<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>String<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Object<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Array<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
      </tr>
   </tbody>
</table>

Pour les autres opérateurs de comparaison tels que >, > =, ! =, < et < =, hello règles suivantes s’appliquent :   

* Une comparaison entre des types entraîne le résultat Undefined.
* Une comparaison entre deux objets ou deux tableaux entraîne le résultat Undefined.   

Si le résultat hello d’expression scalaire de hello dans le filtre de hello est non défini, document correspondant de hello n'est pas inclus dans le résultat de hello, étant donné que Undefined ne sont logiquement équivalentes trop « true ».

### <a name="between-keyword"></a>Mot clé BETWEEN
Vous pouvez également utiliser hello BETWEEN mot clé tooexpress l’interrogation des plages de valeurs, comme dans ANSI SQL. Vous pouvez utiliser BETWEEN sur des chaînes ou des nombres.

Par exemple, cette requête renvoie tous les documents de famille dans quels hello niveau du premier enfant est compris entre 1-5 (tous deux inclus). 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

Contrairement à dans ANSI-SQL, vous pouvez également utiliser hello BETWEEN clause dans la clause FROM de hello comme Bonjour l’exemple suivant.

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

Pour les temps d’exécution de requête plus rapides, n’oubliez pas de toocreate une stratégie d’indexation qui utilise un type d’index de plage par rapport à toutes les propriétés/chemins d’accès numériques qui sont filtrés dans la clause BETWEEN hello. 

Hello de principale différence entre l’utilisation de BETWEEN dans ANSI SQL et les API DocumentDB est que vous pouvez exprimer des requêtes de plage par rapport aux propriétés de types mixtes : par exemple, avoir « niveau » est un nombre (5) dans des documents et les chaînes dans d’autres (« grade4 »). Dans ce cas, comme dans JavaScript, une comparaison entre deux résultats de différents types de « non définie » et hello document sera ignorée.

### <a name="logical-and-or-and-not-operators"></a>Opérateurs logiques (AND, OR et NOT)
Les opérateurs logiques interviennent sur des valeurs booléennes. tables de vérité logiques Hello pour ces opérateurs sont affichés dans hello les tableaux suivants.

| OU | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |True |True |
| False |True |False |Undefined |
| Undefined |True |Undefined |Undefined |

| AND | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |False |Undefined |
| False |False |False |False |
| Undefined |Undefined |False |Undefined |

| NOT |  |
| --- | --- |
| True |False |
| False |True |
| Undefined |Undefined |

### <a name="in-keyword"></a>Mot clé IN
mot clé IN de Hello peut être utilisé toocheck si une valeur spécifiée correspond à la valeur dans une liste. Par exemple, cette requête retourne tous les documents de famille où id de hello est un des « WakefieldFamily » ou « AndersenFamily ». 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

Cet exemple retourne tous les documents où l’état de hello est hello spécifié les valeurs.

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>Opérateurs Ternary (?) et Coalesce (??)
les opérateurs ternaire et Coalesce Hello peuvent être toobuild utilisées les expressions conditionnelles, toopopular similaire programmation des langages tels que c# et JavaScript. 

opérateur ternaire ( ?) de Hello peut être très utile lors de la construction nouvelles propriétés JSON sur hello vol. Par exemple, maintenant vous pouvez écrire les niveaux de classe de requêtes tooclassify hello dans un format lisible humain comme débutant/intermédiaire/Avancé comme indiqué ci-dessous.

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

Vous pouvez également imbriquer hello appels toohello (opérateur), comme dans la requête hello ci-dessous.

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

Comme avec d’autres opérateurs de requête, si hello propriétés référencées dans une expression conditionnelle hello sont manquantes dans n’importe quel document, ou si les types hello comparés sont différents, puis ces documents sont exclus dans les résultats de la requête hello.

Hello Coalesce ( ?) opérateur peut être utilisé tooefficiently cocher présence hello d’une propriété (aussi appelé) vérifier si elle est définie) dans un document. Cela est utile lors de l'interrogation de données semi-structurées ou de types différents. Par exemple, cette requête renvoie hello « lastName » le cas échéant, ou hello « nom » si elle n’est pas présent.

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>Accesseur de propriété entre guillemets
Vous pouvez également accéder aux propriétés à l’aide d’opérateur de propriété entre guillemets hello `[]`. Par exemple, `SELECT c.grade` and `SELECT c["grade"]` sont équivalentes. Cette syntaxe est utile lorsque vous devez tooescape une propriété qui contient des espaces, des caractères spéciaux, ou qui se passe hello tooshare même nom qu’un mot clé SQL ou un mot réservé.

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>Clause SELECT
clause SELECT de Hello (**`SELECT <select_list>`**) est obligatoire et spécifie que les valeurs sont récupérées à partir de la requête de hello, comme dans ANSI-SQL. sous-ensemble Hello été filtré sur les documents source hello sont passés sur la phase de projection hello, où hello spécifié les valeurs JSON sont récupérés et un nouvel objet JSON est construit, pour chaque entrée passée sur lui. 

Hello, l’exemple suivant montre une requête SELECT classique. 

**Requête**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Résultats**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>Propriétés imbriquées
Bonjour l’exemple suivant, nous allons projection deux propriétés imbriquées `f.address.state` et `f.address.city`.

**Requête**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Résultats**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


Projection prend également en charge les expressions de JSON comme indiqué dans hello l’exemple suivant :

**Requête**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Résultats**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


Examinons le rôle hello `$1` ici. Hello `SELECT` clause doit toocreate un objet JSON et car aucune clé n’est fournie, nous utilisons des noms de variables d’argument implicite en commençant par `$1`. Par exemple, cette requête renvoie 2 variables d’argument implicites, étiquetées `$1` and `$2`.

**Requête**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Résultats**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>Alias
Maintenant nous allons étendre exemple hello ci-dessus rencontreraient explicite de valeurs. EN l’état hello mot clé utilisé pour l’utilisation d’alias. Il est facultatif, comme indiqué lors de la projection hello deuxième valeur en tant que `NameInfo`. 

Au cas où une requête présente deux propriétés hello même nom, alias doit être utilisé toorename une ou les deux hello propriétés afin qu’ils sont de lever l’ambiguïté dans hello projetée résultat.

**Requête**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Résultats**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>Expressions scalaires
En outre tooproperty fait référence à, la clause SELECT de hello prend également en charge les expressions scalaires tels que des constantes, des expressions arithmétiques, des expressions logiques, etc.. Par exemple, voici une requête « Hello World » simple.

**Requête**

    SELECT "Hello World"

**Résultats**

    [{
      "$1": "Hello World"
    }]


Voici un exemple plus complexe utilisant une expression scalaire.

**Requête**

    SELECT ((2 + 11 % 7)-2)/3    

**Résultats**

    [{
      "$1": 1.33333
    }]


Dans l’exemple suivant de hello, résultat hello d’expression scalaire de hello est une valeur booléenne.

**Requête**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**Résultats**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>Création d'objet et de tableau
Une autre fonctionnalité clé du langage SQL de l’API DocumentDB est la possibilité de créer un tableau ou un objet. Dans l’exemple précédent de hello, notez que nous avons créé un nouvel objet JSON. De même, un peut également construire des tableaux comme hello exemple suivant :

**Requête**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**Résultats**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>Mot clé VALUE
Hello **valeur** (mot clé) fournit une valeur de façon tooreturn JSON. Par exemple, les requêtes hello ci-dessous retourne hello scalaire `"Hello World"` au lieu de `{$1: "Hello World"}`.

**Requête**

    SELECT VALUE "Hello World"

**Résultats**

    [
      "Hello World"
    ]


Hello requête suivante renvoie valeur JSON de hello sans hello `"address"` étiquette dans les résultats de hello.

**Requête**

    SELECT VALUE f.address
    FROM Families f    

**Résultats**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

Hello exemple suivant étend cette tooshow comment tooreturn JSON des valeurs de primitives (hello inférieurs d’arborescence JSON hello). 

**Requête**

    SELECT VALUE f.address.state
    FROM Families f    

**Résultats**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>Opérateur *
Bonjour opérateur spécial (*) est document hello tooproject pris en charge-est. Lorsqu’il est utilisé, il doit être hello projetée uniquement le champ. Si une requête comme `SELECT * FROM Families f` est valide, `SELECT VALUE * FROM Families f ` et `SELECT *, f.id FROM Families f ` ne le sont pas.

**Requête**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Résultats**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>Opérateur TOP
mot clé TOP de Hello peut être utilisé numéro de hello toolimit de valeurs à partir d’une requête. Lorsque TOP est utilisé conjointement avec la clause ORDER BY hello, jeu de résultats hello est limitée toohello N premiers de valeurs ordonnés ; Sinon, elle retourne hello N premiers résultats dans un ordre non défini. Comme meilleure pratique, dans une instruction SELECT, toujours utiliser une clause ORDER BY avec la clause TOP de hello. Il s’agit de hello seule façon toopredictably indiquer quelles lignes sont affectées par TOP. 

**Requête**

    SELECT TOP 1 * 
    FROM Families f 

**Résultats**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

L’opérateur TOP peut être utilisé avec une valeur constante (comme indiqué ci-dessus) ou avec une valeur variable à l'aide de requêtes paramétrables. Pour plus d'informations, consultez les requêtes paramétrables ci-dessous.

### <a id="Aggregates"></a>Fonctions d’agrégation
Vous pouvez également effectuer des agrégations Bonjour `SELECT` clause. Les fonctions d’agrégation effectuent un calcul sur un ensemble de valeurs et renvoient une valeur unique. Par exemple, hello requête suivante retourne hello nombre de documents familles au sein de la collection de hello.

**Requête**

    SELECT COUNT(1) 
    FROM Families f 

**Résultats**

    [{
        "$1": 2
    }]

Vous pouvez également retourner la valeur scalaire hello hello d’agrégation à l’aide de hello `VALUE` (mot clé). Par exemple, hello requête suivante retourne hello nombre de valeurs comme un nombre unique :

**Requête**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**Résultats**

    [ 2 ]

Vous pouvez également effectuer des agrégations en appliquant des filtres simultanément. Par exemple, hello requête suivante retourne hello nombre de documents avec l’adresse de hello dans hello état de Washington.

**Requête**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**Résultats**

    [ 1 ]

Hello tableau suivant répertorie hello des fonctions d’agrégation prises en charge dans l’API DocumentDB. `SUM` et `AVG` s’appliquent à des valeurs numériques, tandis que `COUNT`, `MIN`, et `MAX` peuvent être effectuées sur des nombres, des chaînes, des booléens et des valeurs Null. 

| Usage | Description |
|-------|-------------|
| COUNT | Retourne hello nombre d’éléments dans l’expression de hello. |
| SUM   | Retourne hello somme de toutes les valeurs hello dans l’expression de hello. |
| MIN   | Retourne hello valeur minimale dans l’expression de hello. |
| MAX   | Retourne hello valeur maximale dans l’expression de hello. |
| MOY   | Retourne hello moyenne des valeurs hello dans l’expression de hello. |

Agrégats peuvent également être effectuées sur les résultats de hello d’une itération du tableau. Pour en savoir plus, consultez la section relative à [l’itération de tableaux dans les requêtes](#Iteration).

> [!NOTE]
> Lors de l’aide hello Explorer de requête du portail Azure, notez que les requêtes d’agrégation des résultats hello partiellement agrégées sur une page de requête. Hello kits de développement logiciel génère une seule valeur cumulative dans toutes les pages. 
> 
> Ordre tooperform requêtes d’agrégation à l’aide de code, vous avez besoin de kit de développement .NET 1.12.0, Kit de développement logiciel .NET Core 1.1.0 ou kit de développement logiciel Java 1.9.5 ou version ultérieure.    
>

## <a id="OrderByClause"></a>Clause ORDER BY
Comme dans ANSI-SQL, vous pouvez désormais inclure une clause Order By facultative lors d’une interrogation. clause de Hello peut inclure une commande facultative de hello toospecify argument ASC/DESC dans lequel les résultats doivent être récupérées.

Par exemple, voici une requête qui Récupère des familles dans l’ordre du nom de la ville de résidence hello.

**Requête**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**Résultats**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

Et Voici une requête qui Récupère des familles dans l’ordre de date de création, qui est stockée comme un nombre représentant hello date, c'est-à-dire, temps écoulé depuis le 1er janvier 1970, en secondes.

**Requête**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**Résultats**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>Concepts avancés de base de données et requêtes SQL

### <a id="Iteration"></a>Itération
Une nouvelle construction a été ajoutée via hello **IN** mot clé dans la prise en charge de tooprovide DocumentDB API SQL pour itérer sur des tableaux JSON. source de Hello FROM prend en charge pour l’itération. Commençons par hello l’exemple suivant :

**Requête**

    SELECT * 
    FROM Families.children

**Résultats**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

Maintenant nous allons examiner une autre requête qui effectue une itération sur les enfants dans la collection de hello. Notez la différence de hello dans le tableau de sortie hello. Cet exemple fractionne `children` et aplatit les résultats hello dans un seul tableau.  

**Requête**

    SELECT * 
    FROM c IN Families.children

**Résultats**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

Cela peut être plus toofilter utilisé sur chaque écriture du tableau hello comme indiqué dans hello l’exemple suivant :

**Requête**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**Résultats**  

    [{
      "givenName": "Lisa"
    }]

Vous pouvez également effectuer l’agrégation sur le résultat de hello d’itération du tableau. Par exemple, hello requête suivante compte hello nombre d’enfants parmi toutes les familles.

**Requête**

    SELECT COUNT(child) 
    FROM child IN Families.children

**Résultats**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>Jointures
Dans une base de données relationnelle, toojoin besoin de hello dans des tables est important. Il s’agit de schémas de logique toodesigning facultatif normalisée hello. Toothis contraires, API DocumentDB porte sur le modèle de données dénormalisées hello de documents de schéma. Revient à hello logique une « jointure réflexive ».

syntaxe Hello hello langage prend en charge est la jointure de jointure que < from_source2 > < que from_source1 est étendu >... JOIN <from_sourceN>. D’une façon générale, ceci renvoie un ensemble de **N**-tuples (un tuple avec **N** valeurs). Les valeurs de chaque tuple sont produites par l'itération de tous les alias de la collection sur leurs ensembles respectifs. En d’autres termes, il s’agit d’un produit cartésien des jeux hello participant à la jointure de hello.

Hello exemples suivants montrent comment la clause de jointure hello fonctionne. Dans l’exemple suivant de hello, résultat de hello est vide, car hello produit croisé de chaque document à partir de la source et un jeu vide est vide.

**Requête**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**Résultats**  

    [{
    }]


Dans l’exemple suivant de hello, jointure de hello est entre la racine du document hello et hello `children` subroot. Il s'agit d'un produit croisé entre deux objets JSON. faits Hello qu’enfants est un tableau n’est pas efficace hello jointure étant donné que nous avons affaire à une racine unique qui est le tableau des enfants hello. Par conséquent, les résultats hello contient uniquement deux résultats, étant donné que le produit croisé de chaque document par un tableau hello hello produit exactement un seul document.

**Requête**

    SELECT f.id
    FROM Families f
    JOIN f.children

**Résultats**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


Bonjour à l’exemple suivant montre une jointure plus classique :

**Requête**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**Résultats**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



Hello première toonote est que hello `from_source` Hello **joindre** clause est un itérateur. Par conséquent, les flux hello dans ce cas est comme suit :  

* Développez chaque élément enfant **c** dans le tableau de hello.
* Appliquer un produit croisé par la racine du document de hello hello **f** avec chaque élément enfant **c** qui a été aplatie dans la première étape de hello.
* Enfin, projet objet racine de hello **f** uniquement de la propriété name. 

document de première Hello (`AndersenFamily`) contient uniquement un élément enfant, afin de l’ensemble de résultats hello contient uniquement un seul objet toothis document correspondant. document de deuxième Hello (`WakefieldFamily`) contient deux enfants. Par conséquent, hello produit croisé génère un objet distinct pour chaque enfant, ce qui entraîne deux objets, un pour chaque document de toothis enfant correspondant. racine Hello champs dans les deux de ces documents sont identiques, hello simplement comme prévu dans un produit croisé.

Hello réel utilitaire Hello jointure est tooform les tuples à partir du produit croisé hello dans une forme qui est sinon tooproject difficile. En outre, comme nous le voir dans l’exemple hello ci-dessous, vous pouvez filtrer sur combinaison hello d’un tuple hello de permet de cet utilisateur a choisi une condition satisfaite par les tuples hello globale.

**Requête**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**Résultats**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



Cet exemple est un prolongement naturel de hello précédent exemple et effectue une jointure en double. Par conséquent, hello produit croisé peut être considéré comme hello suivant pseudo-code :

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily` a un enfant qui a un animal. Par conséquent, hello produit croisé génère une ligne (1\*1\*1) à partir de cette famille. Cependant, WakefieldFamily a deux enfants, mais seul l'un d'eux, « Jesse », a des animaux. Or, Jesse a deux animaux. Par conséquent, hello produit croisé donne 1\*1\*2 = 2 lignes à partir de cette famille.

Dans l’exemple suivant de hello, il existe un filtre supplémentaire sur `pet`. Cela exclut tous les tuples hello où hello pet nom n’est pas « Clichés instantané ». Notez que nous nous toobuild en mesure des tuples à partir des tableaux, le filtre sur un des éléments hello du tuple de hello et n’importe quelle combinaison d’éléments de hello du projet. 

**Requête**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**Résultats**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>Intégration JavaScript
Azure Cosmos DB fournit un modèle de programmation pour l’exécution de la logique d’application basée sur JavaScript directement sur des collections de hello en termes de procédures stockées et déclencheurs. Ceci permet pour les deux :

* Opérations CRUD transactionnelles de capacité toodo hautes performances et des requêtes sur des documents dans une collection en vertu de l’intégration en profondeur hello du runtime JavaScript directement dans le moteur de base de données hello. 
* Une modélisation naturelle du flux de contrôle, de l'étendue des variables, de l'attribution et de l'intégration des primitives de gestion d'exception avec des transactions de base de données. Pour plus d’informations sur la prise en charge de la base de données Azure Cosmos pour l’intégration de JavaScript, veuillez consultez la documentation de programmabilité du côté serveur du JavaScript toohello.

### <a id="UserDefinedFunctions"></a>Fonctions définies par l’utilisateur
Avec les types hello déjà définis dans cet article, DocumentDB API SQL fournit la prise en charge pour le fonctions défini utilisateur (UDF). En particulier, les fonctions UDF scalaires sont prises en charge dans lesquelles les développeurs de hello peuvent passer de zéro ou plusieurs arguments et retourner un résultat unique argument précédent. La légalité des valeurs JSON de chacun de ces arguments est vérifiée.  

Hello syntaxe SQL d’API DocumentDB est étendue toosupport logique d’application personnalisée à l’aide de ces fonctions définies par l’utilisateur. Ces dernières peuvent être enregistrées avec l’API DocumentDB, puis référencées dans le cadre d’une requête SQL. En fait, hello UDF sont ordinateurs conçu toobe appelé par les requêtes. Comme un choix toothis facultatif, UDF n’ont accès toohello contexte objet qui hello autres JavaScript ont des types (procédures stockées et déclencheurs). Comme les requêtes s'exécutent en lecture seule, elles peuvent démarrer sur des réplicas principaux ou secondaires. Par conséquent, UDF sont conçu toorun sur les réplicas secondaires, contrairement à d’autres types de JavaScript.

Voici un exemple de la façon dont un fichier UDF peut être enregistré à hello Cosmos DB de base de données, en particulier dans une collection de documents.

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

Hello exemple précédent crée une fonction dont le nom est `REGEX_MATCH`. Il accepte deux valeurs de chaîne JSON `input` et `pattern` et vérifie si hello premières correspondances hello modèle défini dans hello ensuite à l’aide de fonction de String.Match () de JavaScript.

Nous pouvons maintenant utiliser cette fonction définie par l'utilisateur dans une requête, dans une projection. UDF doivent être qualifiés par préfixe qui respecte la casse de hello « udf. » quand elles sont appelées à partir de requêtes. 

> [!NOTE]
> Préalable too3/17/2015 Cosmos DB pris en charge les appels UDF sans hello « udf. » comme SELECT REGEX_MATCH(). Ce modèle d'appel est maintenant déconseillé.  
> 
> 

**Requête**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**Résultats**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

Hello UDF peut également servir à l’intérieur d’un filtre comme illustré dans l’exemple hello ci-dessous, également qualifié avec hello « udf. » Préfixe :

**Requête**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**Résultats**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


Fondamentalement, les fonctions définies par l'utilisateur sont des expressions scalaires valides et peuvent être utilisées dans des projections et des filtres. 

tooexpand sous tension hello des UDF, examinons un autre exemple avec une logique conditionnelle :

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


Voici un exemple qu’exercices hello UDF.

**Requête**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**Résultats**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


Comme hello Galerie d’exemples précédents, UDF intégrant power hello du langage JavaScript hello DocumentDB API SQL tooprovide une riche interface programmable toodo procédurale, conditionnelle une logique complexe à l’aide de hello d’intégrés JavaScript runtime fonctionnalités.

DocumentDB API SQL fournit des arguments de hello toohello UDF pour chaque document dans la source de hello stade hello actuel (clause WHERE ou sélectionnez) de traitement hello UDF. résultat Hello est incorporé dans hello pipeline de l’exécution globale en toute transparence. Si les propriétés hello tooby référencé hello UDF paramètres ne sont pas disponibles dans hello valeur JSON, hello paramètre est considéré comme non défini et donc hello appel de fonction est entièrement ignorée. Même si le résultat de hello Hello UDF n’est pas défini, il n’est pas inclus dans le résultat de hello. 

En résumé, UDF sont une logique métier complexe toodo outils sophistiqués en tant que partie de la requête de hello.

### <a name="operator-evaluation"></a>Évaluation d'opérateur
COSMOS DB, en vertu de hello d’en cours d’une base de données JSON, dessine parallels avec JavaScript, opérateurs et sa sémantique d’évaluation. Alors que Cosmos DB tente de la sémantique JavaScript toopreserve en termes de prise en charge JSON, évaluation d’opération hello dévie dans certains cas.

Dans DocumentDB API SQL, contrairement à dans SQL traditionnel, types hello de valeurs sont souvent inconnus jusqu'à ce que les valeurs de hello sont récupérées à partir de la base de données. Dans l’ordre tooefficiently exécuter des requêtes, la plupart des opérateurs de hello ont des exigences de type strict. 

Le langage SQL de l’API DocumentDB n’effectue pas de conversions implicites, contrairement à JavaScript. Par exemple, une requête comme `SELECT * FROM Person p WHERE p.Age = 21` correspond à des documents qui contiennent une propriété Age dont la valeur est 21. Tout autre document dont la propriété Age correspond à la chaîne « 21 » ou à l'une de ses multiples variantes telles que « 021 », « 21.0 », « 0021 », « 00021 », etc. ne sera pas mis en correspondance. Il s’agit en revanche toohello JavaScript où les valeurs de chaîne hello sont implicitement converti toonumbers (basé sur un opérateur, ex : ==). Ce choix est crucial pour une correspondance d’index efficace dans le langage SQL de l’API DocumentDB. 

## <a name="parameterized-sql-queries"></a>Requêtes SQL paramétrables
COSMOS DB prend en charge les requêtes avec paramètres exprimés par hello familier notation @. SQL paramétré fournit une gestion et un échappement robustes de l'entrée utilisateur et empêche l'exposition accidentelle des données par l'intermédiaire de l'injection SQL. 

Par exemple, vous pouvez écrire une requête qui prend le nom et l'état de l'adresse comme paramètres, puis l'exécuter pour différentes valeurs de nom et d'état d'adresse en fonction de l'entrée utilisateur.

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

Cette demande peut ensuite être envoyée tooCosmos DB en tant qu’une requête paramétrable de JSON, comme indiqué ci-dessous.

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

Hello argument tooTOP peut être définie à l’aide de requêtes paramétrables, comme indiqué ci-dessous.

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

Les valeurs de paramètres peuvent être n'importe quel format JSON valide (chaînes, nombres, valeurs booléennes, null, même des tableaux ou des valeurs JSON imbriquées). De plus, comme Cosmos DB est sans schéma, les paramètres ne sont pas validés par rapport à un type.

## <a id="BuiltinFunctions"></a>Fonctions intégrées
Cosmos DB prend également en charge plusieurs fonctions intégrées pour des opérations courantes. Ces fonctions s’utilisent dans les requêtes comme les fonctions définies par l’utilisateur.

| Groupe de fonctions          | Opérations                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Fonctions mathématiques  | ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN et TAN |
| Fonctions de vérification du type | IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED et IS_PRIMITIVE                                                           |
| Fonctions de chaîne        | CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING et UPPER       |
| Fonctions de tableau         | ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH et ARRAY_SLICE                                                                                         |
| Fonctions spatiales       | ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID et ST_ISVALIDDETAILED                                                                           | 

Si vous utilisez actuellement une fonction définie par l’utilisateur (UDF) pour laquelle une fonction intégrée est désormais disponible, vous devez utiliser la fonction intégrée de hello correspondant comme il va toobe les toorun plus rapide et plus efficacement. 

### <a name="mathematical-functions"></a>Fonctions mathématiques
fonctions mathématiques Hello chaque effectuent un calcul, en fonction des valeurs d’entrée qui sont fournies en tant qu’arguments et retournent une valeur numérique. Ce tableau répertorie les fonctions mathématiques intégrées qui sont prises en charge.


| Utilisation | Description |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [[ABS (num_expr)](#bk_abs) | Retourne hello valeur absolue (positive) de hello de l’expression numérique spécifiée. |
| [CEILING (num_expr)](#bk_ceiling) | Retourne hello plus petit entier supérieur à, ou être égal, hello expression numérique spécifiée. |
| [FLOOR (num_expr)](#bk_floor) | Retourne des hello plus grand entier inférieur ou égal toohello l’expression numérique spécifiée. |
| [EXP (num_expr)](#bk_exp) | Exposant de hello retourne Hello l’expression numérique spécifiée. |
| [LOG (num_expr [,base])](#bk_log) | Népérien retourne hello Hello spécifié expression numérique, voire logarithme hello hello à l’aide de base |
| [LOG10 (num_expr)](#bk_log10) | Valeur logarithmique de base 10 hello retourne Hello spécifié expression numérique. |
| [ROUND (num_expr)](#bk_round) | Retourne une valeur numérique, arrondie toohello nombre entier le plus proche. |
| [TRUNC (num_expr)](#bk_trunc) | Retourne une valeur numérique, tronquée toohello nombre entier le plus proche. |
| [SQRT (num_expr)](#bk_sqrt) | Racine carrée retourne hello hello de l’expression numérique spécifiée. |
| [SQUARE (num_expr)](#bk_square) | Hello retourne carrée hello de l’expression numérique spécifiée. |
| [POWER (num_expr, num_expr)](#bk_power) | Puissance hello retourne hello toohello valeur de l’expression numérique spécifiée. |
| [SIGN (num_expr)](#bk_sign) | Retourne hello signe la valeur (-1, 0, 1) de hello de l’expression numérique spécifiée. |
| [ACOS (num_expr)](#bk_acos) | Angle de hello retourne, en radians, dont le cosinus est hello expression numérique spécifiée ; également appelé arc cosinus. |
| [ASIN (num_expr)](#bk_asin) | Angle de hello retourne, en radians, dont le sinus est hello spécifié expression numérique. Cette fonction est également appelée arcsinus. |
| [ATAN (num_expr)](#bk_atan) | Angle de hello retourne, en radians, dont la tangente est hello spécifié expression numérique. Cette fonction est également appelée arctangente. |
| [ATN2 (num_expr)](#bk_atn2) | Retourne hello angle, en radians, entre l’axe des x positif de hello et ray hello à partir du point de toohello origine hello (y, x), où x et y sont des valeurs hello Hello deux expressions de type float spécifiée. |
| [COS (num_expr)](#bk_cos) | Cosinus trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée. |
| [COT (num_expr)](#bk_cot) | Cotangente trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression numérique spécifiée. |
| [DEGREES (num_expr)](#bk_degrees) | Retourne hello angle correspondant en degrés pour un angle spécifié en radians. |
| [PI ()](#bk_pi) | Retourne hello valeur constante de PI. |
| [RADIANS (num_expr)](#bk_radians) | Retourne des radians lorsqu’une expression numérique, en degrés, est entrée. |
| [SIN (num_expr)](#bk_sin) | Sinus trigonométrique de hello retourne Hello spécifié d’angle, en radians, Bonjour de l’expression spécifiée. |
| [TAN (num_expr)](#bk_tan) | Tangente de hello retourne d’expression d’entrée hello dans hello de l’expression spécifiée. |

Par exemple, vous pouvez maintenant exécuter des requêtes hello suivante :

**Requête**

    SELECT VALUE ABS(-4)

**Résultats**

    [4]

Hello principale différence entre tooANSI de fonctions en comparaison de base de données Cosmos SQL est qu’ils sont conçu toowork correctement avec les données de schéma sans schéma et mixte. Par exemple, si vous avez un document dans lequel la propriété Size hello est manquant ou a une valeur non numérique comme « inconnu », puis le document de hello est ignorée, au lieu de retourner une erreur.

### <a name="type-checking-functions"></a>Fonctions de vérification du type
les fonctions de vérification de type Hello vous autorisent toocheck hello ce type d’une expression dans des requêtes SQL. Type de fonctions de vérification peuvent être utilisé type hello de toodetermine des propriétés dans les documents volée hello lorsqu’il est variable ou inconnu. Le tableau répertorie les fonctions de vérification du type intégrées qui sont prises en charge.

<table>
<tr>
  <td><strong>Utilisation</strong></td>
  <td><strong>Description</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></td>
  <td>Retourne une valeur booléenne indiquant si le type hello de valeur de hello est un tableau.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></td>
  <td>Retourne une valeur booléenne indiquant si le type hello de valeur de hello est une valeur booléenne.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></td>
  <td>Retourne une valeur booléenne indiquant si le type hello de valeur de hello est null.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></td>
  <td>Retourne une valeur booléenne indiquant si le type hello de valeur de hello est un nombre.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></td>
  <td>Retourne une valeur booléenne indiquant si le type hello de valeur de hello est un objet JSON.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></td>
  <td>Retourne une valeur booléenne indiquant si le type hello de valeur de hello est une chaîne.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></td>
  <td>Retourne une valeur booléenne indiquant si une valeur a été assignée à la propriété de hello.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></td>
  <td>Retourne une valeur booléenne indiquant si le type hello de valeur de hello est null, nombre, booléen ou chaîne.</td>
</tr>

</table>

L’utilisation de ces fonctions, vous pouvez maintenant exécuter des requêtes hello suivante :

**Requête**

    SELECT VALUE IS_NUMBER(-4)

**Résultats**

    [true]

### <a name="string-functions"></a>Fonctions de chaîne
Bonjour fonctions scalaires suivantes effectuent une opération sur une valeur de chaîne d’entrée et retournent une valeur numérique ou booléenne, une chaîne. Voici un tableau des fonctions de chaîne intégrées :

| Utilisation | Description |
| --- | --- |
| [LENGTH (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |Retourne hello nombre de caractères de hello de l’expression de chaîne spécifiée |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |Retourne une chaîne qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de chaîne. |
| [SUBSTRING (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |Retourne une partie d’une expression de chaîne. |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |Retourne une valeur booléenne indiquant si les première expression de chaîne hello se termine ensuite par hello |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |Retourne une valeur booléenne indiquant si les première expression de chaîne hello se termine ensuite par hello |
| [CONTAINS (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |Retourne une valeur booléenne qui indique si le première expression de chaîne hello contient hello ensuite. |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |Retourne hello position de départ des hello première occurrence de hello deuxième expression de chaîne hello première expression de chaîne spécifiée, ou -1 si la chaîne de hello est introuvable. |
| [LEFT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |Retourne hello partie gauche d’une chaîne avec hello spécifié de caractères. |
| [RIGHT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |Hello retourne à droite dans le cadre d’une chaîne avec hello nombre spécifié de caractères. |
| [LTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |Retourne une expression de chaîne après avoir supprimé les espaces de début. |
| [RTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |Retourne une expression de chaîne après avoir tronqué tous les espaces de fin. |
| [LOWER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |Retourne une expression de chaîne après la conversion de toolowercase de données de caractères majuscules en caractères. |
| [UPPER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |Retourne une expression de chaîne après la conversion de toouppercase de données de caractères en minuscules. |
| [REPLACE (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |Remplace toutes les occurrences d’une valeur de chaîne spécifiée par une autre valeur de chaîne. |
| [REPLICATE (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |Répète une valeur de chaîne un nombre de fois spécifié. |
| [REVERSE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |Retourne l’ordre inverse d’une valeur de chaîne hello. |

À l’aide de ces fonctions, vous pouvez maintenant exécuter des requêtes hello suivante. Par exemple, vous pouvez retourner nom de famille hello en majuscules comme suit :

**Requête**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**Résultats**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

Vous pouvez également concaténer des chaînes, comme dans cet exemple :

**Requête**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**Résultats**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


Fonctions de chaîne permet également de hello où les résultats de toofilter de clause, comme dans hello l’exemple suivant :

**Requête**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**Résultats**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>Fonctions de tableau
Hello suivant des fonctions scalaires effectuent une opération sur une valeur d’entrée de tableau et le retour numérique, la valeur booléenne ou de tableau. Voici un tableau des fonctions de tableau intégrées :

| Utilisation | Description |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |Nombre de hello retourne des éléments de hello spécifié expression de tableau. |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |Retourne un tableau qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de tableau. |
| [ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |Retourne une valeur booléenne qui indique si le tableau de hello contient hello valeur spécifiée. Peut spécifier si la correspondance de hello est complet ou partiel. |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |Retourne une partie d’une expression de tableau. |

Fonctions de tableau peuvent être utilisé toomanipulate des tableaux dans JSON. Par exemple, voici une requête qui retourne tous les documents où un des parents de hello « Robin Wakefield ». 

**Requête**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**Résultats**

    [{
      "id": "WakefieldFamily"
    }]

Vous pouvez spécifier un fragment partiels pour les éléments correspondants dans le tableau de hello. Hello requête suivante recherche tous les parents avec hello `givenName` de `Robin`.

**Requête**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**Résultats**

    [{
      "id": "WakefieldFamily"
    }]


Voici un autre exemple qui utilise ARRAY_LENGTH tooget hello nombre d’enfants par famille.

**Requête**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**Résultats**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>Fonctions spatiales
COSMOS DB prend en charge hello suivant des fonctions intégrées d’Open Geospatial Consortium (OGC) pour l’interrogation de géographiques. 

<table>
<tr>
  <td><strong>Utilisation</strong></td>
  <td><strong>Description</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (point_expr, point_expr)</td>
  <td>Retourne la distance hello entre les expressions LineString, Polygon ou GeoJSON Point hello deux.</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr, polygon_expr)</td>
  <td>Retourne une expression booléenne indiquant si hello premier GeoJSON objet (Point, polygone ou LineString) se trouve dans hello deuxième GeoJSON objet (Point, polygone ou LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Retourne une expression booléenne indiquant si hello deux GeoJSON objets spécifiés (Point, polygone ou LineString) se croisent.</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Retourne une valeur booléenne indiquant si hello spécifiée expression LineString, Polygon ou GeoJSON Point n’est valide.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Retourne une valeur JSON contenant une valeur booléenne si hello de l’expression LineString, Polygon ou GeoJSON Point spécifiée est valide et si elle est non valide, en outre hello motif en tant que valeur de chaîne.</td>
</tr>
</table>

Les fonctions spatiale peuvent être des requêtes de proximité tooperform utilisé par rapport aux données spatiales. Par exemple, voici une requête qui retourne la que famille de tous les documents qu’est 30 kilomètres de hello emplacement spécifié à l’aide de fonctions intégrées de ST_DISTANCE hello. 

**Requête**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Résultats**

    [{
      "id": "WakefieldFamily"
    }]

Pour plus d’informations sur la prise en charge géospatiale dans Cosmos DB, consultez [Working with geospatial data in Azure Cosmos DB (Utilisation de données géospatiales dans Azure Cosmos DB)](geospatial.md). Qui encapsule des fonctions spatiales hello syntaxe SQL pour la base de données Cosmos. Maintenant examinons à présent comment LINQ interrogation fonctionne et comment il interagit avec la syntaxe hello nous avons vu jusqu'à présent.

## <a id="Linq"></a>LINQ tooDocumentDB API SQL
LINQ est un modèle de programmation .NET qui exprime un calcul en tant que requête sur des flux d'objets. COSMOS DB fournit un toointerface bibliothèque côté client avec LINQ grâce à une conversion entre JSON et les objets .NET et un mappage à partir d’un sous-ensemble de LINQ interroge les requêtes tooCosmos DB. 

image Hello ci-dessous montre l’architecture hello de prendre en charge les requêtes LINQ à l’aide de la base de données Cosmos.  À l’aide du client de base de données Cosmos hello, les développeurs peuvent créer un **IQueryable** que directement des requêtes hello Cosmos DB demandez au fournisseur, ce qui traduit par requête LINQ de hello une requête de base de données Cosmos de l’objet. requête de Hello est ensuite transmise toohello tooretrieve de serveur de base de données Cosmos un jeu de résultats au format JSON. Hello retourné les résultats sont désérialisés dans un flux d’objets .NET côté client de hello.

![Architecture de prise en charge des requêtes LINQ avec l’API DocumentDB (syntaxe SQL, langage de requête JSON, concepts de bases de données et requêtes SQL)][1]

### <a name="net-and-json-mapping"></a>Mappage .NET et JSON
mappage de Hello entre les objets .NET et les documents JSON est naturelle - chaque champ de membre de données est mappé tooa JSON objet, où le nom du champ hello est mappé dans « clé » toohello objet de hello et hello « value » est mappée de manière récursive toohello valeur faisant partie d’hello objet. Envisagez de hello l’exemple suivant : objet de famille hello créé est document JSON de toohello mappé comme indiqué ci-dessous. Et vice versa, document JSON de hello mappé tooa arrière .NET objet.

**Classe C#**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>Traduction de tooSQL LINQ
fournisseur de requêtes de base de données Cosmos Hello effectue un mappage de l’effort optimal à partir d’une requête LINQ dans une requête SQL de base de données Cosmos. Bonjour suivant description, nous supposons que lecteur de hello possède une connaissance élémentaire de LINQ.

Tout d’abord, pour le système de type hello, nous prenons en charge tous les types primitifs JSON-types numériques, boolean, string et null. Seuls ces types JSON sont pris en charge. Hello après les expressions scalaires est prises en charge.

* Des valeurs constantes, notamment des valeurs constantes des types de données primitifs hello au moment de hello hello requête est évaluée.
* Expressions d’index de tableau de la propriété – ces expressions font référence de propriété toohello d’un objet ou un élément de tableau.
  
     family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n étant un entier
* Expressions arithmétiques : elles incluent les expressions arithmétiques communes sur les valeurs numériques et booléennes. Pour la liste complète de hello, consultez Spécification de SQL toohello.
  
     2 * family.children[0].grade;    x + y;
* Expression de comparaison de chaîne, notamment les comparer une valeur de chaîne constante de chaîne valeur toosome.  
  
     mother.familyName == "Smith";    child.givenName == s; //s étant une chaîne
* Expressions de création d'objet/tableau : ces expressions renvoient un objet de type de valeur composée ou de type anonyme ou un tableau de tels objets. Ces valeurs peuvent être imbriquées.
  
     new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //type anonyme avec deux champs              
     new int[] { 3, child.grade, 5 };

### <a id="SupportedLinqOperators"></a>Liste des opérateurs LINQ pris en charge
Voici une liste des opérateurs LINQ pris en charge dans le fournisseur LINQ de hello inclus avec hello DocumentDB .NET SDK.

* **Sélectionnez**: Projections traduire toohello SQL SELECT, y compris la construction d’objet
* **Où**: filtres traduire toohello SQL WHERE et prend en charge la traduction entre & &, || et ! opérateurs de toohello SQL
* **SelectMany**: autorise le déroulement de la clause de jointure SQL toohello tableaux. Peut être toofilter d’expressions toochain/imbrication utilisés sur les éléments de tableau
* **OrderBy et OrderByDescending**: traduit tooORDER par ordre croissant ou décroissant
* Les opérateurs **Count**, **Sum**, **Min**, **Max** et **Average** pour l’agrégation, et leurs équivalents asynchrones **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** et **AverageAsync**.
* **CompareTo**: traduit toorange comparaisons. Généralement utilisés pour les chaînes car ils ne sont pas comparables dans .NET
* **Prendre**: traduit toohello SQL TOP pour limiter les résultats d’une requête
* **Fonctions mathématiques**: prend en charge la traduction à partir de. Abs, Acos, Asin de NET, Atan, Ceiling, Cos, Exp, Floor, journal, Log10, Pow, Round, signe, Sin, Sqrt, Tan, tronquer des fonctions intégrées de toohello équivalentes SQL.
* **Fonctions de chaîne**: prend en charge la traduction à partir de. Concat, Contains, EndsWith de NET, IndexOf, nombre, ToLower, TrimStart, Replace, inverse, TrimEnd, StartsWith, SubString, ToUpper toohello équivalent SQL des fonctions intégrées.
* **Fonctions de tableau**: prend en charge la traduction à partir de. Concat, Contains et nombre toohello équivalent SQL fonctions intégrées de NET.
* **Fonctions d’Extension Geospatial**: prend en charge la traduction à partir de la Distance, dans, IsValid, les méthodes stub et IsValidDetailed toohello équivalent SQL des fonctions intégrées.
* **Extension de fonction définie par l’utilisateur**: traduction prend en charge à partir de hello stub de méthode UserDefinedFunctionProvider.Invoke toohello correspondante définie par l’utilisateur (fonction).
* **Divers**: prend en charge la traduction de hello coalesce et des opérateurs conditionnels. Peut traduire Contains tooString CONTAINS, ARRAY_CONTAINS ou hello SQL IN selon le contexte.

### <a name="sql-query-operators"></a>Opérateurs de requête SQL
Voici quelques exemples qui illustrent comment certains des opérateurs de requête LINQ standards hello sont convertis vers le bas des requêtes de base de données tooCosmos.

#### <a name="select-operator"></a>Opérateur Select
syntaxe de Hello est `input.Select(x => f(x))`, où `f` est une expression scalaire.

**Expression Lambda LINQ**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**Expression Lambda LINQ**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**Expression Lambda LINQ**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>Opérateur SelectMany
syntaxe de Hello est `input.SelectMany(x => f(x))`, où `f` est une expression scalaire qui retourne un type de collection.

**Expression Lambda LINQ**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Opérateur Where
syntaxe de Hello est `input.Where(x => f(x))`, où `f` est une expression scalaire, qui retourne une valeur booléenne.

**Expression Lambda LINQ**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**Expression Lambda LINQ**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>Requêtes SQL composites
Hello ci-dessus opérateurs peut être tooform composer des requêtes plus puissantes. Étant donné que Cosmos DB prend en charge les collections imbriquées, composition de hello peut être concaténée ou imbriquée.

#### <a name="concatenation"></a>Concaténation
syntaxe de Hello est `input(.|.SelectMany())(.Select()|.Where())*`. Une requête concaténée peut commencer par une requête `SelectMany` facultative suivie de plusieurs opérateurs `Select` ou `Where`.

**Expression Lambda LINQ**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**Expression Lambda LINQ**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**Expression Lambda LINQ**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**Expression Lambda LINQ**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>Imbrication
syntaxe de Hello est `input.SelectMany(x=>x.Q())` où Q est un `Select`, `SelectMany`, ou `Where` opérateur.

Dans une requête imbriquée, requête interne de hello est élément tooeach appliqué de la collection externe de hello. Une fonctionnalité importante est que cette requête interne hello peut faire référence toohello des champs d’éléments de hello dans la collection externe de hello telles que les jointures réflexives.

**Expression Lambda LINQ**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**Expression Lambda LINQ**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**Expression Lambda LINQ**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>Exécution de requêtes SQL
Cosmos DB expose les ressources par le biais d’une API REST qui peut être appelée par n’importe quel langage capable de créer des requêtes HTTP/HTTPS. Par ailleurs, Cosmos DB propose des bibliothèques de programmation pour plusieurs langages populaires comme .NET, Node.js, JavaScript et Python. Hello API REST et hello différentes bibliothèques prennent en charge interrogation via SQL. Hello .NET SDK prend en charge LINQ interrogation en outre tooSQL.

Hello suivant exemples montrent comment toocreate une requête et l’envoyer par rapport à un compte de base de données de base de données Cosmos.

### <a id="RestAPI"></a>API REST
Cosmos DB fournit un modèle de programmation RESTful ouvert sur HTTP. Vous pouvez approvisionner vos comptes de bases de données en utilisant un abonnement Azure. modèle de ressource de base de données Cosmos Hello se compose d’un ensemble de ressources sous un compte de base de données, chacune d’elles étant adressable en utilisant un URI logique et stable. Un ensemble de ressources est tooas auxquels un flux dans ce document. Un compte de base de données se compose d'un ensemble de bases de données. Chacune d'elles contient plusieurs collections et chaque collection contient des documents, des fonctions définies par l'utilisateur et d'autres types de ressources.

modèle d’interaction de base Hello avec ces ressources est via les verbes hello HTTP GET, PUT, POST et DELETE avec leur interprétation standard. verbe POST de Hello est utilisé pour la création d’une nouvelle ressource, l’exécution d’une procédure stockée ou pour l’émission d’une requête de base de données Cosmos. Les requêtes sont toujours des opérations en lecture seule sans effets secondaires.

Hello exemples suivants montrent un billet pour une requête d’API DocumentDB adressée à une collection contenant hello deux exemples de documents que nous avons examiné jusqu'à présent. requête de Hello a un filtre simple sur la propriété de nom hello JSON. Notez que hello hello `x-ms-documentdb-isquery` et Content-Type : `application/query+json` toodenote en-têtes qui hello opération est une requête.

**Requête**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**Résultats**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


Hello deuxième exemple montre une requête plus complexe qui retourne plusieurs résultats à partir de la jointure de hello.

**Requête**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**Résultats**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


Si les résultats d’une requête ne peut pas tenir dans une seule page de résultats, puis hello API REST retourne un jeton de continuation via hello `x-ms-continuation-token` en-tête de réponse. Les clients peuvent paginer les résultats en incluant l’en-tête de hello dans les résultats suivants. nombre de Hello de résultats par page peut également être contrôlé via hello `x-ms-max-item-count` en-tête du numéro. Si la requête spécifiée de hello possède une fonction d’agrégation comme `COUNT`, puis page hello de la requête peut retourner une valeur de partiellement agrégée sur la page de résultats hello. les clients de Hello doit effectuer une agrégation de second niveau sur ces résultats tooproduce hello finale des résultats, par exemple, somme des nombres hello retournées dans le nombre total de hello des pages individuelles tooreturn hello.

stratégie de la cohérence des données toomanage hello pour les requêtes, utilisez hello `x-ms-consistency-level` en-tête comme toutes les demandes d’API REST. Par souci de cohérence de session, il est plus récente hello d’écho tooalso requis `x-ms-session-token` en-tête Cookie demande de requête hello. Hello stratégie d’indexation de collection interrogée peut également influer sur la cohérence de hello des résultats de la requête. La valeur par défaut hello les paramètres de stratégie d’indexation, pour les collections hello index est toujours en cours avec le contenu du document hello et cohérence hello choisie pour les données de résultat de requête. Si hello stratégie d’indexation est tooLazy souple, requêtes peuvent renvoyer des résultats obsolètes. Pour en savoir plus, voir [Niveaux de cohérence des données paramétrables dans Azure Cosmos DB][consistency-levels].

Si la stratégie d’indexation hello configuré sur la collection de hello ne peut pas prendre en charge la requête spécifiée de hello, le serveur de base de données Azure Cosmos hello retourne 400 » demande incorrecte ». Ce code est renvoyé pour les requêtes de plage par rapport aux chemins d'accès configurés pour les recherches (d'égalité) de hachage et pour les chemins d'accès explicitement exclus de l'indexation. Hello `x-ms-documentdb-query-enable-scan` en-tête peut être spécifié tooallow hello requête tooperform une analyse lorsqu’un index n’est pas disponible.

Vous pouvez obtenir les métriques détaillées sur l’exécution des requêtes en définissant `x-ms-documentdb-populatequerymetrics` en-tête trop`True`. Pour en savoir plus, consultez la section relative aux [métriques de requête SQL pour l’API DocumentDB Azure Cosmos DB](documentdb-sql-query-metrics.md).

### <a id="DotNetSdk"></a>Kit SDK C# (.NET)
Hello .NET SDK prend en charge LINQ et SQL interrogation. Hello suivant montre comment la requête de filtre simple tooperform hello introduit précédemment dans ce document.

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Cet exemple compare l'égalité de deux propriétés dans chaque document et utilise des projections anonymes. 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Hello l’exemple suivant montre des jointures, exprimées par LINQ SelectMany.

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



client .NET de Hello itère automatiquement toutes les pages hello des résultats de requête dans les blocs de foreach hello comme indiqué ci-dessus. requête Hello options introduites dans la section de l’API REST de hello sont également disponibles dans hello .NET SDK à l’aide de hello `FeedOptions` et `FeedResponse` classes Bonjour CreateDocumentQuery méthode. nombre de Hello de pages peut être contrôlé à l’aide de hello `MaxItemCount` paramètre. 

Vous pouvez explicitement contrôler la pagination en créant `IDocumentQueryable` à l’aide de hello `IQueryable` objet, puis en lisant le` ResponseContinuationToken` valeurs et en les passant sauvegarder en tant que `RequestContinuationToken` dans `FeedOptions`. `EnableScanInQuery`peuvent être les analyses de tooenable ensemble lors de la requête de hello ne peut pas être pris en charge par la stratégie d’indexation hello configuré. Pour les collections partitionnées, vous pouvez utiliser `PartitionKey` requête de hello toorun par rapport à une seule partition (bien que Cosmos DB peut extraire automatiquement ce texte de requête hello), et `EnableCrossPartitionQuery` exécuter des requêtes de toorun qui peuvent nécessiter une toobe sur plusieurs partitions. 

Consultez trop[exemples Azure Cosmos DB .NET](https://github.com/Azure/azure-documentdb-net) pour plus d’exemples contenant des requêtes. 

### <a id="JavaScriptServerSideApi"></a>API JavaScript côté serveur
COSMOS DB fournit un modèle de programmation pour l’exécution de la logique d’application basée sur JavaScript directement sur des collections de hello à l’aide de procédures stockées et les déclencheurs. logique de JavaScript Hello inscrite à un niveau de la collection peut alors émettre des opérations de base de données sur les opérations de hello sur des documents de hello Hello étant donné la collection. Ces opérations sont encapsulées dans les transactions ACID ambiantes.

Hello suivant montre comment queryDocuments de hello toouse dans hello JavaScript server API toomake les requêtes provenant à l’intérieur des procédures stockées et déclencheurs.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>Références
1. [Introduction tooAzure Cosmos DB][introduction]
2. [Spécification SQL Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [Exemples .NET Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net)
4. [Niveaux de cohérence de base Azure Cosmos DB][consistency-levels]
5. ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON [http://json.org/](http://json.org/)
7. Spécification Javascript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. Techniques d’évaluation des requêtes pour les bases de données volumineuses [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994
11. Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.
12. Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins : Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.
13. G. Graefe. infrastructure de Cascades Hello pour l’optimisation des requêtes. IEEE Data Eng. Bull., 18(3): 1995.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md