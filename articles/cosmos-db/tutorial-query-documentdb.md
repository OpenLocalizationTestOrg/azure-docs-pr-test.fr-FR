---
title: "tooquery aaaHow avec SQL dans la base de données Azure Cosmos ? | Microsoft Docs"
description: "En savoir plus tooquery avec des données avec SQL dans la base de données Azure Cosmos DocumentDB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Azure Cosmos DB : Comment tooquery à l’aide de SQL ?

Bonjour Azure Cosmos DB [API DocumentDB](documentdb-introduction.md) prend en charge l’interrogation de documents à l’aide de SQL. Cet article fournit un exemple de document et deux exemples de requêtes SQL et de résultats.

Cet article traite des hello tâches suivantes : 

> [!div class="checklist"]
> * Interrogation des données avec SQL

## <a name="sample-document"></a>Exemple de document

les requêtes SQL Hello dans cet article utilisent hello suivant l’exemple de document.

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
## <a name="where-can-i-run-sql-queries"></a>Où puis-je exécuter des requêtes SQL ?

Vous pouvez exécuter des requêtes à l’aide de hello Explorateur de données Bonjour portail Azure, via hello [API REST et les kits de développement logiciel](documentdb-sdk-dotnet.md)et même hello [Query playground](https://www.documentdb.com/sql/demo), qui exécute des requêtes sur un jeu existant d’exemples de données.

Pour plus d’informations sur les requêtes SQL, consultez :
* [Requête SQL et syntaxe SQL](documentdb-sql-query.md)

## <a name="prerequisites"></a>Composants requis

Ce didacticiel suppose que vous ayez un compte et une collection Azure Cosmos DB. Cela n’est pas le cas ? Hello complète [démarrage rapide de 5 minutes](create-mongodb-nodejs.md) ou hello [didacticiel pour développeur](tutorial-develop-mongodb.md) toocreate un compte et la collection.

## <a name="example-query-1"></a>Exemple de requête 1

Hello famille document d’exemple ci-dessus, suivant la requête SQL renvoie des documents hello où correspond au champ de code hello `WakefieldFamily`. Dans la mesure où il s’agit d’un `SELECT *` instruction, sortie hello de requête de hello est le document JSON complet hello :

**Requête**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**Résultats**

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

## <a name="example-query-2"></a>Exemple de requête 2

les requêtes suivant Hello retourne tous les noms de donné de hello d’enfants dans la famille hello dont l’id correspond à `WakefieldFamily` classés par leur qualité.

**Requête**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**Résultats**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Appris comment tooquery à l’aide de SQL  

Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodistribute vos données globalement.

> [!div class="nextstepaction"]
> [Distribuer vos données globalement](tutorial-global-distribution-documentdb.md)

