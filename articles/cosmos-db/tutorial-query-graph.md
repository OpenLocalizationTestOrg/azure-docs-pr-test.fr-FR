---
title: "aaaHow tooquery graphique des données dans la base de données Azure Cosmos ? | Microsoft Docs"
description: "En savoir plus tooquery un graphique des données dans la base de données Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>Azure Cosmos DB : Comment tooquery avec hello l’API Graph (aperçu) ?

Bonjour Azure Cosmos DB [API Graph](graph-introduction.md) (version préliminaire) prend en charge [GREMLINE](https://docs.mongodb.com/manual/tutorial/query-documents/) requêtes. Cet article fournit des exemples de documents et des requêtes tooget que vous avez démarré. Informations de référence détaillées GREMLINE sont fournie dans hello [prise en charge GREMLINE](gremlin-support.md) l’article.

Cet article traite des hello tâches suivantes : 

> [!div class="checklist"]
> * Interrogation des données avec Gremlin

## <a name="prerequisites"></a>Composants requis

Pour ces requêtes toowork, vous devez disposer d’un compte de base de données Azure Cosmos et un graphique des données dans le conteneur de hello. Cela n’est pas le cas ? Hello complète [démarrage rapide de 5 minutes](create-graph-dotnet.md) ou hello [didacticiel pour développeur](tutorial-query-graph.md) toocreate un compte et le remplir votre base de données. Vous pouvez exécuter hello suivant des requêtes à l’aide de hello [bibliothèque graph de Azure Cosmos DB .NET](graph-sdk-dotnet.md), [console de GREMLINE](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), ou votre pilote GREMLINE favori.

## <a name="count-vertices-in-hello-graph"></a>Nombre des sommets dans le graphique de hello

Hello suivant extrait de code montre comment toocount hello nombre de sommets dans le graphique de hello :

```
g.V().count()
```

## <a name="filters"></a>Filtres

Vous pouvez effectuer des filtres à l’aide de GREMLINE `has` et `hasLabel` les étapes et les associer à l’aide de `and`, `or`, et `not` toobuild les filtres plus complexe. Azure Cosmos DB propose une indexation sans schéma de toutes les propriétés au sein de vos vertex et degrés pour les requêtes rapides :

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Projection

Vous pouvez projeter certaines propriétés dans les résultats de la requête hello à l’aide de hello `values` étape :

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>Rechercher des vertex et des bords associés

Jusqu’ici, nous avons seulement abordé les opérateurs de requête fonctionnant dans n’importe quelle base de données. Graphiques sont rapides et efficaces pour les opérations de parcours lorsque vous avez besoin toonavigate toorelated arêtes et les sommets. Recherchons à présent tous les amis de Thomas. Pour ce faire, nous à l’aide de GREMLINE `outE` toofind hello tous les out-bords Thomas à partir de l’étape, puis parcourir les sommets dans toohello entre les bords à l’aide de GREMLINE `inV` étape :

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

éditeur de requête suivant de Hello effectue deux sauts toofind tous « Amis de vos amis » de Thomas, en appelant `outE` et `inV` deux fois. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

Vous pouvez générer des requêtes plus complexes et implémenter la logique de parcours puissant de graphique à l’aide de GREMLINE, y compris filtre mélange des expressions, exécution à l’aide de bouclage hello `loop` étape et la navigation conditionnelle implémentation à l’aide de hello `choose` étape. En savoir plus sur ce que la [prise en charge de Gremlin](gremlin-support.md) vous permet de faire !

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Appris comment tooquery à l’aide du graphique 

Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodistribute vos données globalement.

> [!div class="nextstepaction"]
> [Distribuer vos données globalement](tutorial-global-distribution-documentdb.md)