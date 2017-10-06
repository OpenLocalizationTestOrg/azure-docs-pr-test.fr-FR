---
title: aaaAzure prise en charge de Cosmos DB GREMLINE | Documents Microsoft
description: "En savoir plus sur hello langue GREMLINE TinkerPop Apache, fonctionnalités et les étapes et disponible dans la base de données Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Prise en charge des graphes Azure Cosmos DB Gremlin
Azure Cosmos DB prend en charge le langage de traversée de graphe [d’Apache Tinkerpop](http://tinkerpop.apache.org), [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps). Il s’agit d’une API Graph qui permet de créer des entités de graphes et d’effectuer des opérations de requête de graphe. Vous pouvez utiliser hello GREMLINE langage toocreate graphique des entités (sommets et bords), modifier les propriétés au sein de ces entités, exécuter des requêtes et parcours et supprimer des entités. 

Base de données Azure Cosmos apporte des fonctionnalités de l’entreprise toograph de bases de données. Cela inclut la distribution globale, la mise à l’échelle indépendante du stockage et du débit, les latences prévisibles de quelques millisecondes, l’indexation automatique et les contrats de niveau de service de disponibilité à 99,99 %. Azure Cosmos DB prenant en charge TinkerPop/GREMLINE, vous pouvez facilement migrer des applications écrites à l’aide d’une autre base de données du graphique sans avoir toomake les modifications du code. En outre, en vertu de la prise en charge de Gremlin, Azure Cosmos DB intègre parfaitement les infrastructures d’analyse compatibles avec TinkerPop comme [Apache Spark GraphX](http://spark.apache.org/graphx/). 

Dans cet article, nous fournir une présentation rapide de GREMLINE et énumérer des fonctionnalités de GREMLINE hello et celles qui sont prises en charge dans l’aperçu hello de prise en charge de l’API Graph.

## <a name="gremlin-by-example"></a>Gremlin par l’exemple
Nous allons utiliser un toounderstand de graphique d’exemple comment les requêtes peuvent être exprimées dans GREMLINE. Hello figure suivante illustre une application métier qui gère les données sur les utilisateurs, les intérêts et les périphériques sous forme de hello d’un graphique.  

![Exemple de base de données montrant des personnes, des appareils et des centres d’intérêt](./media/gremlin-support/sample-graph.png) 

Ce graphique présente hello les types de sommets (appelés « étiquette » dans GREMLINE) suivants :

- Personnes : graphique de hello a trois personnes, Ben (Round Robin) et Thomas
- Centres d’intérêt : leur intérêt, dans cet exemple, hello de Football
- Périphériques : hello les périphériques qui utilisent des personnes
- Les systèmes d’exploitation : les systèmes d’exploitation hello fonctionnant sur des appareils hello

Nous représentent les relations entre ces entités via hello suivant les types/étiquettes du bord hello :

- Connaît : par exemple, « Thomas connaît Robin »
- Intéressées : toorepresent hello centres d’intérêt de personnes hello dans notre graphique, par exemple, « Ben s’intéresse Football »
- RunsOS : Ordinateur portable exécute hello du système d’exploitation Windows
- Utilise : toorepresent quel périphérique une personne utilise. Par exemple, Robin utilise un téléphone Motorola dont le numéro de série est 77

Nous allons exécuter certaines opérations sur ce graphique à l’aide de hello [GREMLINE Console](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console). Vous pouvez également effectuer ces opérations à l’aide des pilotes de GREMLINE dans la plateforme hello de votre choix (Java, Node.js, Python ou .NET).  Avant d’examiner ce qui est pris en charge dans la base de données Azure Cosmos, examinons quelques tooget exemples familiarisé avec la syntaxe hello.

En premier lieu, examinons CRUD. Hello GREMLINE instruction suivante insère hello sommet de « Thomas » dans le graphique de hello :

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

Ensuite, hello après l’instruction de GREMLINE insère un bord « connaît » entre Thomas et (Round Robin).

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

Hello requête suivante retourne sommets de « person » hello dans l’ordre décroissant de leur prénom :
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

Où graphiques brillance est lorsque vous devez tooanswer questions du type « quels systèmes d’exploitation amis de Thomas utilisent-elles ? ». Vous pouvez exécuter ce simple tooget de parcours GREMLINE ces informations à partir du graphique de hello :

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
Nous allons maintenant voir ce qu’Azure Cosmos DB offre aux développeurs Gremlin.

## <a name="gremlin-features"></a>Fonctionnalités de Gremlin
TinkerPop est une norme qui couvre un large éventail de technologies de graphes. Par conséquent, il a standard terminologie toodescribe quelles fonctionnalités sont fournies par un fournisseur de graphique. Azure Cosmos DB fournit une base de données de graphes permanente, concurrentielle et accessible en écriture qui peut être partitionnée entre plusieurs serveurs ou clusters. 

Hello tableau suivant répertorie les fonctionnalités de TinkerPop hello qui sont implémentées par la base de données Azure Cosmos : 

| Catégorie | Implémentation d’Azure Cosmos DB |  Remarques | 
| --- | --- | --- |
| Fonctionnalités de graphe | Fournit la persistance et ConcurrentAccess dans la version préliminaire. Conçue toosupport de Transactions | Méthodes de l’ordinateur peuvent être implémentées via le connecteur de Spark hello. |
| Fonctionnalités variables | Prend en charge les valeurs booléennes, entières, byte, doubles, flottantes, longues et de chaîne | Prend en charge les types primitifs, et est compatible avec des types complexes via un modèle de données |
| Fonctionnalités de vertex | Prend en charge RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty  | Prend en charge la création, la modification et la suppression de vertex |
| Fonctionnalités de propriétés de vertex | StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Prend en charge la création, la modification et la suppression des propriétés vertex |
| Fonctionnalités de bords | AddEges, RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty | Prend en charge la création, la modification et la suppression de bords |
| Fonctionnalités de propriétés de bords | Properties, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Prend en charge la création, la modification et la suppression de bords |

## <a name="gremlin-wire-format-graphson"></a>Format de câble Gremlin : GraphSON

Base de données Azure Cosmos utilise hello [GraphSON format](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) lors du retour de résultats d’opérations de GREMLINE. GraphSON est le format standard de GREMLINE hello pour représenter les sommets, les bords et les propriétés (unique et à valeurs multiples) à l’aide de JSON. 

Par exemple, hello extrait de code suivant montre une représentation sous forme de GraphSON d’un sommet *retourné toohello client* à partir de la base de données Azure Cosmos. 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

propriétés Hello utilisées par GraphSON pour les sommets sont les suivants de hello :

| Propriété | Description |
| --- | --- |
| id | ID de Hello pour les vertex hello. Doit être unique (en combinaison avec la valeur de hello de _partition le cas échéant) |
| label | étiquette Hello du sommet de hello. Il s’agit de type d’entité hello toodescribe facultatives et utilisées. |
| type | Sommets toodistinguish utilisé à partir de documents de graphique non |
| properties | Sac de propriétés définies par l’utilisateur associé au sommet de hello. Chaque propriété peut avoir plusieurs valeurs. |
| _partition (configurable) | clé de partition Hello du sommet de hello. Peut être utilisé tooscale les graphiques toomultiple serveurs |
| outE | Contient une liste des bords extérieurs d’un vertex. Le stockage des informations de contiguïté hello avec sommets permet une exécution rapide de parcours. Les bords sont regroupés en fonction de leurs labels. |

Et bord de hello contient hello suivant toohelp informations avec des parties de tooother de navigation du graphique de hello.

| Propriété | Description |
| --- | --- |
| id | ID de Hello pour edge de hello. Doit être unique (en combinaison avec la valeur de hello de _partition le cas échéant) |
| label | étiquette Hello du bord de hello. Cette propriété est un type de relation hello toodescribe facultatives et utilisées. |
| inV | Contient une liste des vertex d’entrée pour un bord. Le stockage d’informations de contiguïté hello avec le bord de hello permet une exécution rapide de parcours. Les vertex sont regroupés en fonction de leurs labels. |
| properties | Sac de propriétés définies par l’utilisateur associé au bord de hello. Chaque propriété peut avoir plusieurs valeurs. |

Chaque propriété peut stocker plusieurs valeurs dans un tableau. 

| Propriété | Description |
| --- | --- |
| value | valeur Hello de propriété de hello

## <a name="gremlin-partitioning"></a>Partitionnement de Gremlin

Dans Azure Cosmos DB, les graphes sont stockés dans des conteneurs qui peuvent évoluer indépendamment en termes de stockage et de débit (valeurs exprimées en termes de demandes normalisées par seconde). Chaque conteneur doit définir une propriété de clé de partition facultative mais recommandée, qui détermine une limite de partition logique pour les données associées. Chaque vertex/bord doit posséder une propriété `id` unique pour les entités au sein de cette valeur de clé de partition. Détails de Hello sont couverts dans [partitionnement dans la base de données Azure Cosmos](partition-data.md).

Les opérations Gremlin fonctionnent parfaitement entre les données de graphe qui s’étendent sur plusieurs partitions dans Azure Cosmos DB. Toutefois, il est recommandé de toochoose une clé de partition pour vos graphiques qui est couramment utilisé comme un filtre dans les requêtes, a le nombre de valeurs distinctes et fréquence similaire d’accéder à ces valeurs. 

## <a name="gremlin-steps"></a>Étapes de Gremlin
Maintenant examinons hello étapes GREMLINE pris en charge par la base de données Azure Cosmos. Pour des références complètes sur Gremlin, consultez [Référence TinkerPop](http://tinkerpop.apache.org/docs/current/reference).

| étape | Description | Documentation TinkerPop 3.2 | Remarques |
| --- | --- | --- | --- |
| `addE` | Ajoute un bord reliant deux vertex | [étape addE](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | Ajoute un graphique de toohello de sommets | [étape addV](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | Ensurest que tous les parcours hello retournent une valeur | [étape and](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | Un tooassign de modulateur étape une variable toohello de sortie d’une étape | [étape as](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | Un modulateur d’étape utilisé avec `group` et `order` | [étape by](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | Retourne la traversée de première hello qui retourne un résultat | [étape coalesce](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | Renvoie une valeur constante. Utilisé avec `coalesce`| [étape constant](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | Nombre de hello retourne à partir de la traversée de hello | [étape count](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | Retourne hello valeurs en supprimant les doublons hello | [étape dedup](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | Suppressions hello valeurs (vertex/edge) | [étape drop](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | Agit comme une barrière qui calcule l’agrégat hello de résultats| [étape fold](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | Groupes hello valeurs basées sur les étiquettes hello spécifiés| [étape group](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | Les propriétés utilisées toofilter, sommets et des arêtes. Prend en charge `hasLabel`, `hasId`, `hasNot`, et les variantes `has`. | [étape has](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | Injecter des valeurs dans un flux de données| [étape inject](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | Utilisé tooperform un filtre à l’aide d’une expression booléenne | [étape is](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | Utilisé nombre toolimit d’éléments dans le parcours de hello| [étape limit](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | Local encapsule une section d’une sous-requête tooa parcourue, comme | [étape local](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | Utilisé la négation de hello tooproduce d’un filtre | [étape not](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | Retourne hello résultat de hello spécifié traversée si elle génère un résultat else, il retourne hello élément appelant | [étape optional](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | Garantit au moins une des parcours de hello retourne une valeur | [étape or](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | Renvoie les résultats dans hello spécifié l’ordre de tri | [étape order](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | Chemin d’accès complet retourne hello de parcours de hello | [étape path](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | Projets hello propriétés comme une carte | [étape project](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Retourne les propriétés hello pour hello spécifié des étiquettes | [étape properties](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | Filtres toohello spécifié la plage de valeurs| [étape range](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Étape de hello se répète pour hello spécifié le nombre de fois. Permet d’effectuer des boucles | [répétez l’étape](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | Utilisé toosample les résultats à partir de la traversée de hello | [étape sample](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | Utilisé tooproject les résultats à partir de la traversée de hello |  [étape select](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | Utilisée pour les agrégats non bloquant de parcours de hello | [étape store](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | Chemins d’accès d’agrégation à partir d’un vertex dans une arborescence | [étape tree](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | Dérouler un itérateur comme une étape| [étape unfold](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | Fusionner les résultats à partir de plusieurs traversées| [étape union](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | Inclut les étapes hello nécessaires pour le parcours entre les bords et les sommets `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, et `otherV` pour | [étapes vertex](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | Utilisé toofilter les résultats à partir de la traversée de hello. Prend en charge les opérateurs `eq`, `neq`, `lt`, `lte`, `gt`, `gte` et `between`  | [étape where](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

Le moteur optimisé pour l’écriture d’Azure Cosmos DB prend en charge l’indexation automatique de toutes les propriétés au sein des vertex et des bords par défaut. Par conséquent, les requêtes avec des filtres, plage de requêtes, le tri ou les agrégats sur n’importe quelle propriété sont traitées à partir de l’index de hello et pris en charge efficacement. Pour plus d’informations sur la façon dont fonctionne l’indexation dans Azure Cosmos DB, consultez notre article sur [l’indexation indépendante du schéma](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf).

## <a name="next-steps"></a>Étapes suivantes
* Commencez par créer une application de graphe [à l’aide de nos kits SDK](create-graph-dotnet.md) 
* En savoir plus sur [la prise en charge des graphes par Azure Cosmos DB](graph-introduction.md)
