---
title: "Azure Cosmos DB : Comment à l’aide de tooquery hello des API DocumentDB ? | Microsoft Docs"
description: "En savoir plus tooquery avec hello API DocumentDB de base de données Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a>Azure Cosmos DB : Comment tooquery avec l’API pour MongoDB ?

Bonjour Azure Cosmos DB [API pour MongoDB](mongodb-introduction.md) prend en charge [requêtes de shell MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/). 

Cet article traite des hello tâches suivantes : 

> [!div class="checklist"]
> * Interrogation des données avec MongoDB

## <a name="sample-document"></a>Exemple de document

les requêtes de Hello dans cet article utilisent hello suivant l’exemple de document.

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
## <a id="examplequery1"></a> Exemple de requête 1 

Étant donné hello famille document d’exemple ci-dessus, renvoie des documents hello où correspond au champ de code hello de requête suivante de hello `WakefieldFamily`.

**Requête**
    
    db.families.find({ id: “WakefieldFamily”})

**Résultats**

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
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
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <a id="examplequery2"></a>Exemple de requête 2 

les requêtes suivant Hello retourne tous les enfants de hello dans la famille de hello. 

**Requête**
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

**Résultats**

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
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
    ]
    }


## <a id="examplequery3"></a>Exemple de requête 3 

les requêtes suivant Hello retourne toutes les familles de hello qui sont inscrits. 

**Requête**
    
    db.families.find( { "isRegistered" : true })
**Résultats** aucun document ne sera renvoyé. 

## <a id="examplequery4"></a>Exemple de requête 4

les requêtes suivant Hello retourne toutes les familles de hello qui ne sont pas enregistrés. 

**Requête**
    
    db.families.find( { "isRegistered" : false })
**Résultats**

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
}

## <a id="examplequery5"></a>Exemple de requête 5

les requêtes suivant Hello retourne toutes les familles de hello qui ne sont pas enregistrés et l’état est NY. 

**Requête**
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

**Résultats**

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
}


## <a id="examplequery6"></a>Exemple de requête 6

les requêtes suivant Hello retourne toutes les familles de hello où les classes enfants sont 8.

**Requête**
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

**Résultats**

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
}

## <a id="examplequery7"></a>Exemple de requête 7

les requêtes suivant Hello retourne toutes les familles de hello où la taille du tableau des enfants est 3.

**Requête**
  
      db.Family.find( {children: { $size:3} } )

**Résultats**

Aucun résultat n’est renvoyé car aucune n’a plus de 2 enfants. Uniquement lorsque le paramètre est 2 cette requête se réussissent et complète pour le document hello.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Appris comment tooquery à l’aide de MongoDB 

Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodistribute vos données globalement.

> [!div class="nextstepaction"]
> [Distribuer vos données globalement](tutorial-global-distribution-documentdb.md)

