---
title: "Azure Cosmos DB : Développer avec hello API Graph dans .NET | Documents Microsoft"
description: "Découvrez comment toodevelop avec l’API DocumentDB Azure Cosmos DB à l’aide de .NET"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Azure Cosmos DB : Développer avec hello API Graph dans .NET
Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce didacticiel montre comment un compte de base de données Azure Cosmos à l’aide de toocreate hello portail Azure et toocreate une base de données du graphique et un conteneur. application Hello puis crée un réseau social simple avec quatre personnes à l’aide de hello [API Graph](graph-sdk-dotnet.md) (version préliminaire), puis parcourt et interroge le graphique de hello à l’aide de GREMLINE.

Ce didacticiel couvre hello tâches suivantes :

> [!div class="checklist"]
> * Création d’un compte Azure Cosmos DB 
> * Créer une base de données des graphiques et un conteneur
> * Sérialiser des objets de too.NET de sommets et de bords
> * Ajouter des vertex et des bords
> * Graphique de hello la requête à l’aide de GREMLINE

## <a name="graphs-in-azure-cosmos-db"></a>Graphiques dans Azure Cosmos DB
Vous pouvez utiliser la base de données Azure Cosmos toocreate, mise à jour et graphiques de requête à l’aide de hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) bibliothèque. bibliothèque de Microsoft.Azure.Graph Hello fournit une méthode d’extension unique `CreateGremlinQuery<T>` par-dessus hello `DocumentClient` classe les requêtes GREMLINE tooexecute.

Gremlin est un langage de programmation fonctionnel qui prend en charge les opérations d’écriture (DML) et les opérations de requête et de traversée. Nous aborderons quelques exemples dans cet article de tooget votre prise en main avec GREMLINE. Consultez [Requêtes Gremlin](gremlin-support.md) pour une description détaillée des fonctionnalités de Gremlin disponibles dans Azure Cosmos DB. 

## <a name="prerequisites"></a>Composants requis
Vérifiez que vous avez hello suivantes :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [compte gratuit](https://azure.microsoft.com/free/). 
    * Vous pouvez également utiliser hello [Azure DocumentDB émulateur](local-emulator.md) pour ce didacticiel.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-database-account"></a>Créer un compte de base de données

Commençons par la création d’un compte de base de données Azure Cosmos Bonjour portail Azure.  

> [!TIP]
> * Possédez-vous un compte Azure Cosmos DB ? Dans ce cas, passez directement trop[configurer votre solution Visual Studio](#SetupVS)
> * Possédiez-vous un compte Azure DocumentDB ? Si votre compte est maintenant un compte de base de données Azure Cosmos, et que vous pouvez passer trop[configurer votre solution Visual Studio](#SetupVS).  
> * Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre Solution Visual Studio](#SetupVS). 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Configurer votre solution Visual Studio
1. Ouvrez **Visual Studio** sur votre ordinateur.
2. Sur hello **fichier** menu, sélectionnez **nouveau**, puis choisissez **projet**.
3. Bonjour **nouveau projet** boîte de dialogue, sélectionnez **modèles** / **Visual C#** / **l’application Console (.NET Framework)**, nommez votre projet, puis cliquez sur **OK**.
4. Bonjour **l’Explorateur de solutions**, cliquez avec le bouton droit sur votre nouvelle application console qui se trouve sous votre solution Visual Studio, et puis cliquez sur **gérer les Packages NuGet...**
5. Bonjour **NuGet** , cliquez sur **Parcourir**et le type **Microsoft.Azure.Graphs** dans la zone de recherche hello et vérification hello **incluent les versions préliminaires**.
6. Dans les résultats de hello, recherchez **Microsoft.Azure.Graphs** et cliquez sur **installer**.
   
   Si vous obtenez un message sur la vérification des modifications toohello solution, cliquez sur **OK**. Si vous obtenez un message concernant l’acceptation de la licence, cliquez sur **J’accepte**.
   
    Hello `Microsoft.Azure.Graphs` bibliothèque fournit une méthode d’extension unique `CreateGremlinQuery<T>` pour l’exécution d’opérations de GREMLINE. Gremlin est un langage de programmation fonctionnel qui prend en charge les opérations d’écriture (DML) et les opérations de requête et de traversée. Nous aborderons quelques exemples dans cet article de tooget votre prise en main avec GREMLINE. [Requêtes Gremlin](gremlin-support.md) comporte une description détaillée des fonctionnalités de Gremlin disponibles dans Azure Cosmos DB.

## <a id="add-references"></a>Connecter votre application

Ajoutez ces deux constantes et votre variable *client* à votre application. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
Ensuite, head sauvegarde toohello [portail Azure](https://portal.azure.com) tooretrieve votre URL de point de terminaison et la clé primaire. URL de point de terminaison Hello et la clé primaire sont nécessaires pour votre application toounderstand où tooconnect et de base de données Azure Cosmos tootrust connexion de votre application. 

Dans hello portail Azure, accédez de compte de base de données Azure Cosmos tooyour, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**. 

Copiez hello URI à partir du portail de hello et collez-la sur `Endpoint` dans la propriété de point de terminaison hello ci-dessus. Puis copie hello clé primaire à partir du portail de hello et collez-le dans hello `AuthKey` propriété ci-dessus. 

! [Capture d’écran de hello portail Azure utilisée par toocreate de didacticiel hello une application c#. Affiche un hello de compte de base de données Azure Cosmos bouton clés en surbrillance sur hello navigation de base de données Azure Cosmos et valeurs d’URI et la clé primaire hello mis en surbrillance sur hello Panneau de clés] [clés] 
 
## <a id="instantiate"></a>Instancier hello DocumentClient 
Ensuite, créez une nouvelle instance de hello **DocumentClient**.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>Créer une base de données 

À présent, créez une base de données Azure Cosmos [base de données](documentdb-resources.md#databases) à l’aide de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) méthode ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) méthode Hello  **DocumentClient** classe à partir de hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>Créer un graphique 

Ensuite, créez un conteneur graphique à l’aide de hello à l’aide de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) méthode ou [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) méthode Hello **DocumentClient**  classe. Une collection est un conteneur d’entités graphiques. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>Sérialiser des objets de too.NET de sommets et de bords
Base de données Azure Cosmos utilise hello [GraphSON au format câble](gremlin-support.md), qui définit un schéma JSON pour les propriétés, les bords et les sommets. Bonjour Azure Cosmos DB .NET SDK inclut JSON.NET en tant que dépendance, et cela nous permet de désérialiser GraphSON/tooserialize en objets .NET que nous pouvons utiliser dans le code.

Par exemple, nous allons travailler avec un réseau social simple composé de quatre personnes. Nous abordons la façon dont toocreate `Person` sommets, ajouter `Knows` des relations entre eux, puis interroger et parcourir des relations de hello graphique toofind « friend de friend ». 

Hello `Microsoft.Azure.Graphs.Elements` fournit de l’espace de noms `Vertex`, `Edge`, `Property` et `VertexProperty` des classes pour la désérialisation des objets de .NET définis par le toowell GraphSON réponses.

## <a name="run-gremlin-using-creategremlinquery"></a>Exécuter Gremlin à l’aide de CreateGremlinQuery
Gremlin, tout comme SQL, prend en charge les opérations de lecture, d’écriture et d’interrogation. Par exemple, hello extrait de code suivant montre comment toocreate sommets, contours, effectuer quelques exemples de requêtes à l’aide de `CreateGremlinQuery<T>`et de façon asynchrone une itération au sein ces résultats à l’aide `ExecuteNextAsync` et ' HasMoreResults.

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>Ajouter des vertex et des bords

Examinons les instructions de GREMLINE hello illustrées hello précédant la section plus en détail. Nous commençons par créer des vertex à l’aide de la méthode `addV` de Gremlin. Par exemple, hello extrait de code suivant crée un sommet « Thomas Andersen » de type « Person », avec des propriétés pour le prénom, nom et âge.

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

Nous créons ensuite des bords entre ces vertex à l’aide de la méthode `addE` de Gremlin. 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

Nous pouvons mettre à jour un vertex existant à l’aide de l’étape `properties` dans Gremlin. Nous ignorer la requête de hello hello appel tooexecute via `HasMoreResults` et `ExecuteNextAsync` pour obtenir des exemples hello autres hello.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

Vous pouvez supprimer des bords et des vertex en suivant l’étape `drop` de Gremlin. Voici un extrait de code qui montre comment toodelete un sommet et qu’un bord. Notez que la suppression d’un sommet effectue une suppression en cascade de hello associés bords.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>Graphique de requête hello

Gremlin permet également d’effectuer des requêtes et des traversées. Par exemple, hello suivant extrait de code montre comment toocount hello nombre de sommets dans le graphique de hello :

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
Vous pouvez effectuer des filtres à l’aide de GREMLINE `has` et `hasLabel` les étapes et les associer à l’aide de `and`, `or`, et `not` toobuild les filtres plus complexe :

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

Vous pouvez projeter certaines propriétés dans les résultats de la requête hello à l’aide de hello `values` étape :

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

Jusqu’ici, nous avons seulement abordé les opérateurs de requête fonctionnant dans n’importe quelle base de données. Graphiques sont rapides et efficaces pour les opérations de parcours lorsque vous avez besoin toonavigate toorelated arêtes et les sommets. Recherchons à présent tous les amis de Thomas. Pour ce faire, nous à l’aide de GREMLINE `outE` toofind hello tous les out-bords Thomas à partir de l’étape, puis parcourir les sommets dans toohello entre les bords à l’aide de GREMLINE `inV` étape :

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

éditeur de requête suivant de Hello effectue deux sauts toofind tous « Amis de vos amis » de Thomas, en appelant `outE` et `inV` deux fois. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

Vous pouvez générer des requêtes plus complexes et implémenter la logique de parcours puissant de graphique à l’aide de GREMLINE, y compris filtre mélange des expressions, exécution à l’aide de bouclage hello `loop` étape et la navigation conditionnelle implémentation à l’aide de hello `choose` étape. En savoir plus sur ce que la [prise en charge de Gremlin](gremlin-support.md) vous permet de faire !

Ce didacticiel Azure Cosmos DB est maintenant terminé ! 

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, utilisez hello suivant toodelete suit toutes les ressources créées par ce didacticiel Bonjour portail Azure.  

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Créé un compte Azure Cosmos DB 
> * Créer une base de données des graphiques et un conteneur
> * Objets sérialisés too.NET de sommets et de bords
> * Ajouter des vertex et des bords
> * Graphique de hello interrogé à l’aide de GREMLINE

Vous pouvez maintenant générer des requêtes plus complexes et implémenter une logique de traversée de graphique puissante, à l’aide de Gremlin. 

> [!div class="nextstepaction"]
> [Interroger à l’aide de Gremlin](tutorial-query-graph.md)
