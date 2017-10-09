---
title: aaaConnecting Apache Spark tooAzure Cosmos DB | Documents Microsoft
description: "Utilisez ce didacticiel toolearn sur le connecteur Azure Cosmos DB Spark hello qui vous permet des agrégations tooperform distribué Cosmos DB tooconnect Apache Spark tooAzure et sciences de données sur le système de base de données distribués internationalement mutualisée hello à partir de Microsoft qui est conçu pour le cloud de hello."
keywords: apache spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a>Accélérer l’analytique de données volumineuses en temps réel avec le connecteur de base de données Cosmos hello Spark tooAzure

connecteur de base de données Cosmos Hello Spark tooAzure Active tooact de base de données Azure Cosmos en tant qu’entrée source ou récepteur de sortie pour les travaux d’Apache Spark. Connexion [Spark](http://spark.apache.org/) trop[base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) accélère votre capacité toosolve rapide science des données où vous pouvez utiliser la base de données Azure Cosmos tooquickly les problèmes persistent et interroger des données. connecteur de base de données Cosmos Hello Spark tooAzure utilise efficacement les index de base de données Azure Cosmos gérés natifs hello. index de Hello permettent des colonnes modifiables lorsque vous effectuez analytique et prédicat rabat vers le bas le filtrage par rapport à la modification rapide globalement distribués de données, allant des scénarios Internet des objets (IoT) toodata science et analytique.

Pour utiliser Spark GraphX et graphique de GREMLINE hello API de Cosmos base de données Azure, consultez [effectuer analytique de graphique à l’aide de Spark et Apache TinkerPop GREMLINE](spark-connector-graph.md).

## <a name="download"></a>Télécharger

tooget démarré, télécharger le connecteur de base de données Cosmos tooAzure hello Spark (version préliminaire) à partir de hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) référentiel sur GitHub.

## <a name="connector-components"></a>Composants du connecteur

connecteur de Hello utilise hello suivant des composants :

* [Base de données Azure Cosmos](http://documentdb.com) Active tooprovision de clients et de façon élastique mettre à l’échelle à la fois de débit et de stockage entre plusieurs régions géographiques. offres de service Hello :
   * [Distribution globale](distribute-data-globally.md) et échelle horizontale clé en main
   * Garantie de latences chiffre à 99e centile de hello
   * [Différents modèles de cohérence bien définis](consistency-levels.md)
   * Haute disponibilité garantie avec capacités d’hébergement multiple
   * Toutes les fonctionnalités sont garanties par des [contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA) complets, les meilleurs du marché.

* [Apache Spark](http://spark.apache.org/) est un puissant moteur de traitement Open Source axé sur la vitesse, la facilité d’utilisation et des analyses sophistiquées.

* [Apache Spark sur Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) afin que vous puissiez déployer Apache Spark dans cloud hello pour les déploiements stratégiques à l’aide de [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Versions officiellement prises en charge :

| Composant | Version |
|---------|-------|
|Apache Spark|2.0+|
| Scala| 2.11|
| Kit de développement logiciel (SDK) Azure DocumentDB Java | 1.10.0 |

Cet article vous permet d’exécuter certains exemples simples (via pyDocumentDB) à l’aide de Python et hello Scala interfaces.

Il existe deux approches tooconnect Apache Spark et la base de données Azure Cosmos :
- Utilisez pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).
- Création d’un connecteur de Cosmos DB de tooAzure Spark de basée sur Java à l’aide de hello [Kit de développement Java Azure DocumentDB](https://github.com/Azure/azure-documentdb-java).

## <a name="pydocumentdb-implementation"></a>Implémentation de pyDocumentDB
Hello actuel [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) vous permet de tooconnect Spark tooAzure Cosmos DB comme indiqué dans hello suivant schéma :

![Spark tooAzure Cosmos DB des flux de données via pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a>Flux de données de mise en œuvre de hello pyDocumentDB

flux de données Hello est comme suit :

1. nœud de Hello Spark maître connecte à nœud de passerelle de base de données Azure Cosmos toohello via pyDocumentDB. Un utilisateur spécifie uniquement aux connexions de hello Spark et de la base de données Azure Cosmos. Connexions toohello master et passerelle leurs nœuds respectifs sont transparentes toohello utilisateur.
2. nœud de passerelle Hello rend la requête de hello sur la base de données Azure Cosmos où hello requête s’exécute par la suite par rapport aux partitions de la collection hello dans les nœuds de données hello. réponse Hello pour ces requêtes est renvoyé nœud de passerelle toohello et ce jeu de résultats est renvoyé un nœud principal de toohello Spark.
3. Les requêtes ultérieures (par exemple, sur une trame de données Spark) sont envoyés les nœuds de travail Spark toohello pour le traitement.

Communication entre Spark et de base de données Azure Cosmos est limitée toohello nœud maître de Spark et nœuds de passerelle de base de données Azure Cosmos.  les requêtes Hello accédez aussi rapidement que permet de la couche de transport hello entre ces deux nœuds.

### <a name="install-pydocumentdb"></a>Installer pyDocumentDB
Vous pouvez installer pyDocumentDB sur votre nœud de pilote à l’aide de **pip**, par exemple :

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a>Se connecter tooAzure Spark Cosmos DB via pyDocumentDB
simplicité Hello de transport de communication hello rend l’exécution d’une requête à partir de Spark tooAzure Cosmos DB à l’aide de pyDocumentDB relativement simple.

Hello suivant extrait de code montre comment pyDocumentDB toouse dans un contexte de Spark.

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

Comme indiqué dans l’extrait de code hello :

* Bonjour Azure Cosmos DB Python SDK (`pyDocumentDB`) contient hello tous hello des paramètres de connexion. Par exemple, de préférence hello paramètre des emplacements choisit l’ordre de priorité et le réplica de lecture hello.
*  Importer les bibliothèques nécessaires hello et configurer votre **masterKey** et **hôte** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_ client**).


### <a name="execute-spark-queries-via-pydocumentdb"></a>Exécuter des requêtes Spark via pyDocumentDB
Hello suivant l’instance de base de données Azure Cosmos exemples utilisez hello qui a été créée dans l’extrait de code hello précédente à l’aide de hello spécifié en lecture seule des clés. Hello extrait de code suivant connecte toohello **airports.codes** collection dans le compte de DoctorWho hello comme spécifié précédemment et exécute un aéroport de hello tooextract requête villes dans l’état de Washington.

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

Après l’exécution de requête de hello via **requête**, hello résultat est un **query_iterable. QueryIterable** qui est le liste de Python tooa converti. Une liste de Python peut être facilement converti tooa Spark de trame de données à l’aide de hello suivant de code :

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a>Pourquoi utiliser hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB ?
Connexion tooAzure Spark Cosmos DB à l’aide de pyDocumentDB est généralement pour les scénarios où :

* Vous souhaitez toouse Python.
* Vous retournez un jeu à partir de la base de données Azure Cosmos tooSpark de résultats relativement faible. Notez que hello dataset sous-jacent dans la base de données Azure Cosmos peuvent être assez volumineux. Vous appliquez des filtres, c’est-à-dire que vous exécutez des filtres de prédicat, sur votre source Azure Cosmos DB.  

## <a name="spark-tooazure-cosmos-db-connector"></a>Spark tooAzure connecteur Cosmos DB

connecteur de base de données Cosmos Hello Spark tooAzure utilise hello [Kit de développement Java Azure DocumentDB](https://github.com/Azure/azure-documentdb-java) et déplace les données entre les nœuds de travail Spark hello et la base de données Azure Cosmos comme indiqué dans hello suivant schéma :

![Flux de données dans le connecteur de base de données Cosmos hello Spark tooAzure](./media/spark-connector/spark-connector.png)

flux de données Hello est comme suit :

1. nœud de Hello Spark maître connecte toohello base de données Azure Cosmos passerelle nœud tooobtain hello mappage. Un utilisateur spécifie uniquement aux connexions de hello Spark et de la base de données Azure Cosmos. Connexions toohello master et passerelle leurs nœuds respectifs sont transparentes toohello utilisateur.
2. Ces informations sont fournies de nœud principal de Spark toohello précédent.  À ce stade, vous devez être en mesure de tooparse hello requête toodetermine hello partitions et les leurs emplacements dans la base de données Azure Cosmos que vous avez besoin de tooaccess.
3. Ces informations sont transmises toohello Spark de nœuds de travail.
4. nœuds de travail Hello Spark connectent partitions de base de données Azure Cosmos toohello directement tooextract hello des données et retourner des partitions de Spark hello données toohello dans les nœuds de travail hello Spark.

Communication entre Spark et de la base de données Azure Cosmos est nettement plus rapide, car le déplacement des données de hello est entre les nœuds de données de base de données Azure Cosmos hello (partitions) et les nœuds de travail Spark hello.

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a>Créer le connecteur de base de données Cosmos hello Spark tooAzure
Actuellement, le projet de connecteur hello utilise maven. connecteur de hello toobuild sans dépendances, vous pouvez exécuter :
```
mvn clean package
```
Vous pouvez également télécharger des versions les plus récentes de hello JAR hello du hello *libère* dossier.

### <a name="include-hello-azure-cosmos-db-spark-jar"></a>Inclure hello JAR de Spark Azure Cosmos DB
Avant d’exécuter n’importe quel code, vous devez hello tooinclude JAR de Spark Azure Cosmos DB.  Si vous utilisez hello **spark-shell**, vous pouvez inclure hello JAR à l’aide de hello **--fichiers JAR** option.  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

Si vous souhaitez tooexecute hello JAR sans dépendances, utilisez hello suivant de code :

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

Si vous utilisez un service de l’ordinateur portable comme Azure HDInsight Notebook portable, vous pouvez utiliser hello **nouvelles magic** commandes :

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

Hello **JAR** commande permet de vous tooinclude hello deux fichiers JAR qui sont nécessaires pour **azure-cosmosdb-spark** (lui-même et hello Kit de développement Java Azure DocumentDB) et exclure **scala-refléter** afin qu’elle n’interfère pas avec hello Livy appelle (bloc-notes jupyter > Livy > Spark).

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a>Se connecter Spark tooAzure à l’aide de base de données Cosmos hello connecteur
Bien que le transport de communication hello est un peu plus compliqué, l’exécution d’une requête à partir de Spark tooAzure DB Cosmos à l’aide du connecteur de hello est considérablement plus rapide.

Hello suivant extrait de code montre comment toouse hello connecteur dans un contexte de Spark.

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Comme indiqué dans l’extrait de code hello :

- **Azure-cosmosdb-spark** contient hello tous hello les paramètres de connexion nécessaires, lesquels incluent des emplacements de hello préféré. Par exemple, vous pouvez choisir de hello lire l’ordre de priorité et de réplica.
- Uniquement les bibliothèques nécessaires hello d’importation et configurer votre client de base de données Azure Cosmos de hello toocreate clé principale et de l’hôte.

### <a name="execute-spark-queries-via-hello-connector"></a>Exécuter des requêtes Spark via le connecteur de hello

Hello suivant l’instance de base de données Azure Cosmos exemple utilise hello qui a été créé dans l’extrait de code hello précédente à l’aide de hello spécifié en lecture seule des clés. Hello extrait de code suivant connecte toohello DepartureDelays.flights_pcoll collection (hello compte DoctorWho comme indiqué précédemment) et exécute une requête tooextract hello flight delay d’informations de vols qui sont au départ de Seattle.

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a>Pourquoi utiliser la mise en œuvre de hello Spark tooAzure Cosmos DB connecteur ?

Connexion tooAzure Spark Cosmos DB à l’aide du connecteur de hello est généralement pour les scénarios où :

* Vous souhaitez toouse Scala et mettre à jour tooinclude un wrapper de Python, comme indiqué dans [problème 3 : wrapper d’ajouter les Python et des exemples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).
* Vous avez une grande quantité de données des tootransfer entre Apache Spark et de la base de données Azure Cosmos.

toogive vous une idée de la différence de performances de requête hello, consultez hello [wiki de séries de tests de requête](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).

## <a name="distributed-aggregation-example"></a>Exemple d’agrégations distribuées
Cette section fournit des exemples montrant comment réaliser des agrégations distribuées et des analyses à l’aide d’Apache Spark et d’Azure Cosmos DB. Base de données Azure Cosmos prend déjà en charge agrégations, qui est décrite dans hello [agrégats de montée en puissance planète avec la base de données Azure Cosmos blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/). Voici comment vous pouvez mettre toohello ensuite niveau avec Apache Spark.

Notez que ces agrégations sont dans la référence toohello [bloc-notes de connecteur de base de données Cosmos Spark tooAzure](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).

### <a name="connect-tooflights-sample-data"></a>Connecter des données d’exemple tooflights
Ces exemples d’agrégations accèdent à certaines données de performances de vol stockées dans notre base de données Azure Cosmos DB **DoctorWho**. tooconnect tooit, vous devez hello tooutilize suivant l’extrait de code :

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Cet extrait de code, nous sommes également continu toorun une requête de base que les transferts hello ensemble filtré de données à partir de la base de données Azure Cosmos tooSpark où hello ce dernier peut effectuer des agrégats distribuées. Dans ce cas, nous demandons les vols au départ de Seattle (SEA).

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

Hello résultats suivants ont été générés en exécutant des requêtes de hello de hello service de bloc-notes Notebook.  Notez que tous les extraits de code hello sont génériques et non spécifiques tooany service.

### <a name="running-limit-and-count-queries"></a>Exécution des requêtes LIMIT et COUNT
Tout comme vous avez utilisé tooin SQL/Spark SQL, nous allons commencer avec un **limite** requête :

![Requête LIMIT Spark](./media/spark-connector/spark-sql-query.png)

Hello requête suivant est une simple et rapide **nombre** requête :

![Requête COUNT Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a>Requête GROUP BY
Dans le jeu suivant, nous pouvons facilement exécuter des requêtes **GROUP BY** sur notre base de données Azure Cosmos DB :

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Graphique de la requête GROUP BY Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a>Requête DISTINCT, ORDER BY
Et voici une requête **DISTINCT, ORDER BY** :

![Graphique de la requête GROUP BY Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a>Continuer l’analyse de données de vol hello
Vous pouvez utiliser hello suivant l’exemple d’analyse toocontinue requêtes hello de données de vol :

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a>Les 5 principales destinations (villes) vers lesquelles il y a du retard au départ de Seattle
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Graphique des retards principaux Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a>Calculer les retards médians par villes de destination au départ de Seattle
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Graphique des retards médians Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a>Étapes suivantes

Si vous n’avez pas encore, télécharger le connecteur de base de données Cosmos hello Spark tooAzure de hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) référentiel GitHub et Explorer des ressources supplémentaires hello dans le référentiel de hello :

* [Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples) (Exemples d’agrégations distribuées)
* [Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples) (Exemples de scripts et blocs-notes)

Vous pouvez également vous tooreview hello [Apache Spark SQL, les trames de données et les jeux de données Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) et hello [Apache Spark sur Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) l’article.
