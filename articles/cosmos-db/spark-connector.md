---
title: "Connexion d’Apache Spark à Azure Cosmos DB | Microsoft Docs"
description: "Grâce à ce didacticiel, vous en apprendrez davantage sur le connecteur Spark-Azure Cosmos DB, qui vous permet de connecter Apache Spark à Azure Cosmos DB pour réaliser des agrégations distribuées et des opérations de sciences des données sur le système de base de données mutualisé conçu pour le cloud de Microsoft, qui est distribué dans le monde entier."
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
ms.openlocfilehash: 8ecbb478c81cde25bbd0d1c9ee07ae02b07f8cc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="67f56-104">Accélérer l’analyse en temps réel des données volumineuses grâce au connecteur Spark-Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="67f56-104">Accelerate real-time big-data analytics with the Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="67f56-105">Le connecteur Spark-Azure Cosmos DB permet à Azure Cosmos DB de jouer le rôle de source d’entrée ou de récepteur de sortie pour les tâches Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-105">The Spark to Azure Cosmos DB connector enables Azure Cosmos DB to act as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="67f56-106">Connecter [Spark](http://spark.apache.org/) à [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accélère votre capacité à résoudre les problèmes liés aux opérations de sciences de données dynamiques, sachant que vous pouvez utiliser Azure Cosmos DB pour conserver et interroger rapidement des données.</span><span class="sxs-lookup"><span data-stu-id="67f56-106">Connecting [Spark](http://spark.apache.org/) to [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability to solve fast-moving data science problems where you can use Azure Cosmos DB to quickly persist and query data.</span></span> <span data-ttu-id="67f56-107">Le connecteur Spark-Azure Cosmos DB utilise efficacement les index gérés natifs d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="67f56-107">The Spark to Azure Cosmos DB connector efficiently utilizes the native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="67f56-108">Les index activent des colonnes modifiables lorsque vous effectuez des analyses et opérez un filtrage de prédicat sur des données globalement distribuées qui changent rapidement, allant de l’Internet des objets (IoT) aux scénarios de sciences et d’analyse des données.</span><span class="sxs-lookup"><span data-stu-id="67f56-108">The indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) to data science and analytics scenarios.</span></span>

<span data-ttu-id="67f56-109">Pour utiliser Spark GraphX et les API Graph Gremlin d’Azure Cosmos DB, voir [Exécuter des analyses graphiques à l’aide de Spark et d’Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="67f56-109">For working with Spark GraphX and the Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="67f56-110">Télécharger</span><span class="sxs-lookup"><span data-stu-id="67f56-110">Download</span></span>

<span data-ttu-id="67f56-111">Pour commencer, télécharger le connecteur Spark-Azure Cosmos DB (préversion) à partir du référentiel [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="67f56-111">To get started, download the Spark to Azure Cosmos DB connector (preview) from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="67f56-112">Composants du connecteur</span><span class="sxs-lookup"><span data-stu-id="67f56-112">Connector components</span></span>

<span data-ttu-id="67f56-113">Le connecteur utilise les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="67f56-113">The connector utilizes the following components:</span></span>

* <span data-ttu-id="67f56-114">[Azure Cosmos DB](http://documentdb.com) permet à ses utilisateurs d’approvisionner et d’adapter de façon élastique leurs capacités de débit et de stockage partout dans le monde.</span><span class="sxs-lookup"><span data-stu-id="67f56-114">[Azure Cosmos DB](http://documentdb.com) enables customers to provision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="67f56-115">Le service offre ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="67f56-115">The service offers:</span></span>
   * <span data-ttu-id="67f56-116">[Distribution globale](distribute-data-globally.md) et échelle horizontale clé en main</span><span class="sxs-lookup"><span data-stu-id="67f56-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="67f56-117">Latences à un chiffre dans 99 pour cent des cas</span><span class="sxs-lookup"><span data-stu-id="67f56-117">Guaranteed single digit latencies at the 99th percentile</span></span>
   * [<span data-ttu-id="67f56-118">Différents modèles de cohérence bien définis</span><span class="sxs-lookup"><span data-stu-id="67f56-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="67f56-119">Haute disponibilité garantie avec capacités d’hébergement multiple</span><span class="sxs-lookup"><span data-stu-id="67f56-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="67f56-120">Toutes les fonctionnalités sont garanties par des [contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA) complets, les meilleurs du marché.</span><span class="sxs-lookup"><span data-stu-id="67f56-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="67f56-121">[Apache Spark](http://spark.apache.org/) est un puissant moteur de traitement Open Source axé sur la vitesse, la facilité d’utilisation et des analyses sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="67f56-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="67f56-122">[Apache Spark sur Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) qui vous permet de déployer Apache Spark dans le cloud pour les déploiements stratégiques à l’aide d’[Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="67f56-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in the cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="67f56-123">Versions officiellement prises en charge :</span><span class="sxs-lookup"><span data-stu-id="67f56-123">Officially supported versions:</span></span>

| <span data-ttu-id="67f56-124">Composant</span><span class="sxs-lookup"><span data-stu-id="67f56-124">Component</span></span> | <span data-ttu-id="67f56-125">Version</span><span class="sxs-lookup"><span data-stu-id="67f56-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="67f56-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="67f56-126">Apache Spark</span></span>|<span data-ttu-id="67f56-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="67f56-127">2.0+</span></span>|
| <span data-ttu-id="67f56-128">Scala</span><span class="sxs-lookup"><span data-stu-id="67f56-128">Scala</span></span>| <span data-ttu-id="67f56-129">2.11</span><span class="sxs-lookup"><span data-stu-id="67f56-129">2.11</span></span>|
| <span data-ttu-id="67f56-130">Kit de développement logiciel (SDK) Azure DocumentDB Java</span><span class="sxs-lookup"><span data-stu-id="67f56-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="67f56-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="67f56-131">1.10.0</span></span> |

<span data-ttu-id="67f56-132">Cet article vous permet d’exécuter quelques exemples simples à l’aide de Python (via pyDocumentDB) et des interfaces Scala.</span><span class="sxs-lookup"><span data-stu-id="67f56-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and the Scala interfaces.</span></span>

<span data-ttu-id="67f56-133">Vous pouvez choisir entre deux approches pour connecter Apache Spark et Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="67f56-133">There are two approaches to connect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="67f56-134">Utiliser pyDocumentDB via le [Kit de développement logiciel (SDK) Azure DocumentDB Python](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="67f56-134">Use pyDocumentDB via the [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="67f56-135">Créer un connecteur Spark-Azure Cosmos DB basé sur Java en utilisant le [Kit SDK Azure DocumentDB Java](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="67f56-135">Create a Java-based Spark to Azure Cosmos DB connector by utilizing the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="67f56-136">Implémentation de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="67f56-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="67f56-137">Le [Kit SDK pyDocumentDB](https://github.com/Azure/azure-documentdb-python) actuel permet de connecter Spark à Azure Cosmos DB, comme illustré dans le diagramme suivant :</span><span class="sxs-lookup"><span data-stu-id="67f56-137">The current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you to connect Spark to Azure Cosmos DB as shown in the following diagram:</span></span>

![Flux de données Spark-Azure Cosmos DB via pyDocumentDB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-the-pydocumentdb-implementation"></a><span data-ttu-id="67f56-139">Flux de données de l’implémentation de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="67f56-139">Data flow of the pyDocumentDB implementation</span></span>

<span data-ttu-id="67f56-140">Le flux de données est le suivant :</span><span class="sxs-lookup"><span data-stu-id="67f56-140">The data flow is as follows:</span></span>

1. <span data-ttu-id="67f56-141">Le nœud principal Spark se connecte au nœud de passerelle Azure Cosmos DB via pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="67f56-141">The Spark master node connects to the Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="67f56-142">Un utilisateur spécifie uniquement les connexions Spark et Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="67f56-142">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="67f56-143">Les connexions aux nœuds principal et de passerelle sont transparentes pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="67f56-143">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="67f56-144">Le nœud de passerelle effectue la requête sur Azure Cosmos DB, sachant que la requête s’exécute par la suite sur les partitions de la collection dans les nœuds de données.</span><span class="sxs-lookup"><span data-stu-id="67f56-144">The gateway node makes the query against Azure Cosmos DB where the query subsequently runs against the collection's partitions in the data nodes.</span></span> <span data-ttu-id="67f56-145">La réponse à ces requêtes est renvoyée au nœud de passerelle, puis le jeu de résultats est retourné au nœud principal Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-145">The response for those queries is sent back to the gateway node, and that result set is returned to the Spark master node.</span></span>
3. <span data-ttu-id="67f56-146">Toutes les requêtes suivantes (par exemple, sur une tramedonnées Spark) sont envoyées aux nœuds worker Spark à des fins de traitement.</span><span class="sxs-lookup"><span data-stu-id="67f56-146">Subsequent queries (for example, against a Spark DataFrame) are sent to the Spark worker nodes for processing.</span></span>

<span data-ttu-id="67f56-147">La communication entre Spark et Azure Cosmos DB est limitée au nœud principal Spark et aux nœuds de passerelle Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="67f56-147">Communication between Spark and Azure Cosmos DB is limited to the Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="67f56-148">Les requêtes sont opérées aussi rapidement que la couche de transport entre ces deux nœuds le permet.</span><span class="sxs-lookup"><span data-stu-id="67f56-148">The queries go as fast as the transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="67f56-149">Installer pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="67f56-149">Install pyDocumentDB</span></span>
<span data-ttu-id="67f56-150">Vous pouvez installer pyDocumentDB sur votre nœud de pilote à l’aide de **pip**, par exemple :</span><span class="sxs-lookup"><span data-stu-id="67f56-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-to-azure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="67f56-151">Connecter Spark à Azure Cosmos DB via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="67f56-151">Connect Spark to Azure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="67f56-152">La simplicité du transport de communication rend relativement simple l’exécution d’une requête de Spark à Azure Cosmos DB à l’aide de pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="67f56-152">The simplicity of the communication transport makes execution of a query from Spark to Azure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="67f56-153">L’extrait de code suivant montre comment utiliser pyDocumentDB dans un contexte Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-153">The following code snippet shows how to use pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring the connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys to connect to Azure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="67f56-154">Comme indiqué dans l’extrait de code :</span><span class="sxs-lookup"><span data-stu-id="67f56-154">As noted in the code snippet:</span></span>

* <span data-ttu-id="67f56-155">Le Kit SDK Python d’Azure DB Cosmos (`pyDocumentDB`) contient tous les paramètres de connexion nécessaires.</span><span class="sxs-lookup"><span data-stu-id="67f56-155">The Azure Cosmos DB Python SDK (`pyDocumentDB`) contains the all the necessary connection parameters.</span></span> <span data-ttu-id="67f56-156">Par exemple, le paramètre des emplacements par défaut choisit le réplica en lecture et l’ordre de priorité.</span><span class="sxs-lookup"><span data-stu-id="67f56-156">For example, the preferred locations parameter chooses the read replica and priority order.</span></span>
*  <span data-ttu-id="67f56-157">Importez les bibliothèques nécessaires et configurez votre **masterKey** et **host** pour créer le *client* Azure Cosmos DB (**pydocumentdb.document_client**).</span><span class="sxs-lookup"><span data-stu-id="67f56-157">Import the necessary libraries and configure your **masterKey** and **host** to create the Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="67f56-158">Exécuter des requêtes Spark via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="67f56-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="67f56-159">Les exemples suivants utilisent l’instance Azure Cosmos DB créée dans l’extrait de code précédent en utilisant les clés en lecture seule spécifiées.</span><span class="sxs-lookup"><span data-stu-id="67f56-159">The following examples use the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="67f56-160">L’extrait de code suivant se connecte à la collection **airports.codes** dans le compte DoctorWho comme indiqué précédemment, puis exécute une requête pour extraire les villes de l’État de Washington disposant d’un aéroport.</span><span class="sxs-lookup"><span data-stu-id="67f56-160">The following code snippet connects to the **airports.codes** collection in the DoctorWho account as specified earlier and runs a query to extract the airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations the Azure Cosmos DB client will use to connect to the database and collection
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

<span data-ttu-id="67f56-161">Une fois la requête exécutée via **query**, le résultat est un élément **query_iterable. QueryIterable** qui est converti en une liste Python.</span><span class="sxs-lookup"><span data-stu-id="67f56-161">After the query has been executed via **query**, the result is a **query_iterable.QueryIterable** that is converted to a Python list.</span></span> <span data-ttu-id="67f56-162">Une liste Python peut être aisément convertie en une tramedonnées Spark à l’aide du code suivant :</span><span class="sxs-lookup"><span data-stu-id="67f56-162">A Python list can be easily converted to a Spark DataFrame by using the following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-the-pydocumentdb-to-connect-spark-to-azure-cosmos-db"></a><span data-ttu-id="67f56-163">Pourquoi utiliser pyDocumentDB pour connecter Spark à Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="67f56-163">Why use the pyDocumentDB to connect Spark to Azure Cosmos DB?</span></span>
<span data-ttu-id="67f56-164">pyDocumentDB est généralement utilisé pour connecter Spark à Azure Cosmos DB dans les scénarios où :</span><span class="sxs-lookup"><span data-stu-id="67f56-164">Connecting Spark to Azure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="67f56-165">Vous souhaitez utiliser Python.</span><span class="sxs-lookup"><span data-stu-id="67f56-165">You want to use Python.</span></span>
* <span data-ttu-id="67f56-166">Un jeu de résultats relativement petit est retourné d’Azure Cosmos DB à Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-166">You are returning a relatively small result set from Azure Cosmos DB to Spark.</span></span> <span data-ttu-id="67f56-167">Notez que le jeu de données sous-jacent dans Azure Cosmos DB peut être très volumineux.</span><span class="sxs-lookup"><span data-stu-id="67f56-167">Note that the underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="67f56-168">Vous appliquez des filtres, c’est-à-dire que vous exécutez des filtres de prédicat, sur votre source Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="67f56-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="67f56-169">Connecteur Spark-Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="67f56-169">Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="67f56-170">Le connecteur Spark-Azure Cosmos DB utilise le [kit SDK Azure DocumentDB Java](https://github.com/Azure/azure-documentdb-java) et déplace les données entre les nœuds worker Spark et Azure Cosmos DB, comme indiqué dans le diagramme suivant :</span><span class="sxs-lookup"><span data-stu-id="67f56-170">The Spark to Azure Cosmos DB connector utilizes the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between the Spark worker nodes and Azure Cosmos DB as shown in the following diagram:</span></span>

![Flux de données dans le connecteur Spark-Azure Cosmos DB](./media/spark-connector/spark-connector.png)

<span data-ttu-id="67f56-172">Le flux de données est le suivant :</span><span class="sxs-lookup"><span data-stu-id="67f56-172">The data flow is as follows:</span></span>

1. <span data-ttu-id="67f56-173">Le nœud principal Spark se connecte au nœud de passerelle Azure Cosmos DB pour obtenir le mappage de partitions.</span><span class="sxs-lookup"><span data-stu-id="67f56-173">The Spark master node connects to the Azure Cosmos DB gateway node to obtain the partition map.</span></span> <span data-ttu-id="67f56-174">Un utilisateur spécifie uniquement les connexions Spark et Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="67f56-174">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="67f56-175">Les connexions aux nœuds principal et de passerelle sont transparentes pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="67f56-175">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="67f56-176">Ces informations sont renvoyées au nœud maître Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-176">This information is provided back to the Spark master node.</span></span>  <span data-ttu-id="67f56-177">À ce stade, vous devez être en mesure d’analyser la requête pour déterminer les partitions (et leurs emplacements) auxquelles vous devez accéder dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="67f56-177">At this point, you should be able to parse the query to determine the partitions and their locations in Azure Cosmos DB that you need to access.</span></span>
3. <span data-ttu-id="67f56-178">Ces informations sont transmises aux nœuds worker Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-178">This information is transmitted to the Spark worker nodes.</span></span>
4. <span data-ttu-id="67f56-179">Les nœuds worker Spark se connectent directement aux partitions Azure Cosmos DB pour extraire les données et les retourner aux partitions Spark dans les nœuds worker Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-179">The Spark worker nodes connect to the Azure Cosmos DB partitions directly to extract the data and return the data to the Spark partitions in the Spark worker nodes.</span></span>

<span data-ttu-id="67f56-180">La communication entre Spark et Azure Cosmos DB est beaucoup plus rapide, car les données sont déplacées entre les nœuds worker Spark et les nœuds de données Azure Cosmos DB (partitions).</span><span class="sxs-lookup"><span data-stu-id="67f56-180">Communication between Spark and Azure Cosmos DB is significantly faster because the data movement is between the Spark worker nodes and the Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="67f56-181">Créer le connecteur Spark-Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="67f56-181">Build the Spark to Azure Cosmos DB connector</span></span>
<span data-ttu-id="67f56-182">Actuellement, le projet de connecteur utilise maven.</span><span class="sxs-lookup"><span data-stu-id="67f56-182">Currently, the connector project uses maven.</span></span> <span data-ttu-id="67f56-183">Pour créer le connecteur sans dépendances, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="67f56-183">To build the connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="67f56-184">Vous pouvez également télécharger les dernières versions du fichier JAR à partir du dossier *releases*.</span><span class="sxs-lookup"><span data-stu-id="67f56-184">You can also download the latest versions of the JAR from the *releases* folder.</span></span>

### <a name="include-the-azure-cosmos-db-spark-jar"></a><span data-ttu-id="67f56-185">Inclure le JAR Azure Cosmos DB Spark</span><span class="sxs-lookup"><span data-stu-id="67f56-185">Include the Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="67f56-186">Avant d’exécuter quelque code que ce sot, vous devez inclure le JAR Azure Cosmos DB Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-186">Before you execute any code, you need to include the Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="67f56-187">Si vous utilisez le **spark-shell**, vous pouvez inclure le JAR à l’aide de l’option **--jars**.</span><span class="sxs-lookup"><span data-stu-id="67f56-187">If you are using the **spark-shell**, then you can include the JAR by using the **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="67f56-188">Si vous souhaitez exécuter le JAR sans dépendances, utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="67f56-188">If you want to execute the JAR without dependencies, use the following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="67f56-189">Si vous utilisez un service de bloc-notes comme le bloc-notes Jupyter Azure HDInsight, vous pouvez utiliser les commandes **spark magic** :</span><span class="sxs-lookup"><span data-stu-id="67f56-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use the **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="67f56-190">La commande **jars** vous permet d’inclure les deux fichiers JAR nécessaires pour **azure-cosmosdb-spark** (lui-même et le Kit de développement logiciel (SDK) Azure DocumentDB Java) et d’exclure **scala-reflect** afin qu’il n’interfère pas avec les appels Livy (bloc-notes Jupyter > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="67f56-190">The **jars** command enables you to include the two JARs that are needed for **azure-cosmosdb-spark** (itself and the Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with the Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-to-azure-cosmos-db-using-the-connector"></a><span data-ttu-id="67f56-191">Connecter Spark à Azure Cosmos DB à l’aide du connecteur</span><span class="sxs-lookup"><span data-stu-id="67f56-191">Connect Spark to Azure Cosmos DB using the connector</span></span>
<span data-ttu-id="67f56-192">Si le transport de communication est un peu plus complexe, l’exécution d’une requête de Spark à Azure Cosmos DB à l’aide du connecteur est très rapide.</span><span class="sxs-lookup"><span data-stu-id="67f56-192">Although the communication transport is a little more complicated, executing a query from Spark to Azure Cosmos DB by using the connector is significantly faster.</span></span>

<span data-ttu-id="67f56-193">L’extrait de code suivant décrit comment utiliser le connecteur dans un contexte Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-193">The following code snippet shows how to use the connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection to your collection
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

<span data-ttu-id="67f56-194">Comme indiqué dans l’extrait de code :</span><span class="sxs-lookup"><span data-stu-id="67f56-194">As noted in the code snippet:</span></span>

- <span data-ttu-id="67f56-195">**Azure-cosmosdb-spark** contient tous les paramètres de connexion nécessaires, dont les emplacements par défaut.</span><span class="sxs-lookup"><span data-stu-id="67f56-195">**azure-cosmosdb-spark** contains the all the necessary connection parameters, which include the preferred locations.</span></span> <span data-ttu-id="67f56-196">Par exemple, vous pouvez choisir le réplica en lecture et l’ordre de priorité.</span><span class="sxs-lookup"><span data-stu-id="67f56-196">For example, you can choose the read replica and priority order.</span></span>
- <span data-ttu-id="67f56-197">Importez simplement les bibliothèques nécessaires et configurez votre masterKey et host pour créer le client Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="67f56-197">Just import the necessary libraries and configure your masterKey and host to create the Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-the-connector"></a><span data-ttu-id="67f56-198">Exécuter les requêtes Spark via le connecteur</span><span class="sxs-lookup"><span data-stu-id="67f56-198">Execute Spark queries via the connector</span></span>

<span data-ttu-id="67f56-199">L’exemple suivant utilise l’instance Azure Cosmos DB créée dans l’extrait de code précédent à l’aide des clés en lecture seule spécifiées.</span><span class="sxs-lookup"><span data-stu-id="67f56-199">The following example uses the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="67f56-200">L’extrait de code suivant se connecte à la collection DepartureDelays.flights_pcoll (dans le compte DoctorWho, comme indiqué précédemment), puis exécute une requête pour extraire les informations de retard des vols au départ de Seattle.</span><span class="sxs-lookup"><span data-stu-id="67f56-200">The following code snippet connects to the DepartureDelays.flights_pcoll collection (in the DoctorWho account as specified earlier) and runs a query to extract the flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-the-spark-to-azure-cosmos-db-connector-implementation"></a><span data-ttu-id="67f56-201">Pourquoi utiliser l’implémentation du connecteur Spark-Azure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="67f56-201">Why use the Spark to Azure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="67f56-202">La connexion de Spark à Azure Cosmos DB à l’aide du connecteur est généralement destinée aux scénarios où :</span><span class="sxs-lookup"><span data-stu-id="67f56-202">Connecting Spark to Azure Cosmos DB by using the connector is typically for scenarios where:</span></span>

* <span data-ttu-id="67f56-203">Vous souhaitez utiliser Scala et le mettre à jour pour inclure un wrapper Python, comme indiqué dans [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3) (Problème n° 3 : Ajouter un wrapper Python et des exemples).</span><span class="sxs-lookup"><span data-stu-id="67f56-203">You want to use Scala and update it to include a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="67f56-204">Vous avez une grande quantité de données à transférer entre Apache Spark et Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="67f56-204">You have a large amount of data to transfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="67f56-205">Pour vous donner une idée de la différence des performances de requête, consultez la [wiki sur les exécutions de tests de requête](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="67f56-205">To give you an idea of the query performance difference, see the [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="67f56-206">Exemple d’agrégations distribuées</span><span class="sxs-lookup"><span data-stu-id="67f56-206">Distributed aggregation example</span></span>
<span data-ttu-id="67f56-207">Cette section fournit des exemples montrant comment réaliser des agrégations distribuées et des analyses à l’aide d’Apache Spark et d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="67f56-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="67f56-208">Azure Cosmos DB prend déjà en charge les agrégations, comme décrit dans le blog [Planet scale aggregates with Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/) (agrégats de mise à l’échelle Planet avec Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="67f56-208">Azure Cosmos DB already supports aggregations, which is discussed in the [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="67f56-209">Voici comment le mener au niveau suivant avec Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="67f56-209">Here is how you can take it to the next level with Apache Spark.</span></span>

<span data-ttu-id="67f56-210">Notez que ces agrégations font référence au [bloc-notes de connecteur Spark-Azure Cosmos DB](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="67f56-210">Note that these aggregations are in reference to the [Spark to Azure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-to-flights-sample-data"></a><span data-ttu-id="67f56-211">Se connecter aux exemples de données de vols</span><span class="sxs-lookup"><span data-stu-id="67f56-211">Connect to flights sample data</span></span>
<span data-ttu-id="67f56-212">Ces exemples d’agrégations accèdent à certaines données de performances de vol stockées dans notre base de données Azure Cosmos DB **DoctorWho**.</span><span class="sxs-lookup"><span data-stu-id="67f56-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="67f56-213">Pour vous connecter à celle-ci, vous devez utiliser l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="67f56-213">To connect to it, you need to utilize the following code snippet:</span></span>

```
// Import Spark to Azure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect to Azure Cosmos DB Database
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

<span data-ttu-id="67f56-214">Avec cet extrait de code, nous allons également exécuter une requête de base qui transfère l’ensemble de données filtré d’Azure Cosmos DB à Spark (où ce dernier peut réaliser des agrégats distribués).</span><span class="sxs-lookup"><span data-stu-id="67f56-214">With this snippet, we are also going to run a base query that transfers the filtered set of data from Azure Cosmos DB to Spark where the latter can perform distributed aggregates.</span></span> <span data-ttu-id="67f56-215">Dans ce cas, nous demandons les vols au départ de Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="67f56-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="67f56-216">Les résultats suivants ont été générés par l’exécution des requêtes à partir du service de bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="67f56-216">The following results were generated by running the queries from the Jupyter notebook service.</span></span>  <span data-ttu-id="67f56-217">Notez que tous les extraits de code sont génériques et non spécifiques à un service.</span><span class="sxs-lookup"><span data-stu-id="67f56-217">Note that all the code snippets are generic and not specific to any service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="67f56-218">Exécution des requêtes LIMIT et COUNT</span><span class="sxs-lookup"><span data-stu-id="67f56-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="67f56-219">Comme vous y êtes habitué dans SQL/Spark SQL, commençons par une requête **LIMIT** :</span><span class="sxs-lookup"><span data-stu-id="67f56-219">Just like you're used to in SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Requête LIMIT Spark](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="67f56-221">La requête suivante est une requête **COUNT** simple et rapide :</span><span class="sxs-lookup"><span data-stu-id="67f56-221">The next query is a simple and fast **COUNT** query:</span></span>

![Requête COUNT Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="67f56-223">Requête GROUP BY</span><span class="sxs-lookup"><span data-stu-id="67f56-223">GROUP BY query</span></span>
<span data-ttu-id="67f56-224">Dans le jeu suivant, nous pouvons facilement exécuter des requêtes **GROUP BY** sur notre base de données Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="67f56-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Graphique de la requête GROUP BY Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="67f56-226">Requête DISTINCT, ORDER BY</span><span class="sxs-lookup"><span data-stu-id="67f56-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="67f56-227">Et voici une requête **DISTINCT, ORDER BY** :</span><span class="sxs-lookup"><span data-stu-id="67f56-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Graphique de la requête GROUP BY Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-the-flight-data-analysis"></a><span data-ttu-id="67f56-229">Continuer l’analyse des données de vol</span><span class="sxs-lookup"><span data-stu-id="67f56-229">Continue the flight data analysis</span></span>
<span data-ttu-id="67f56-230">Vous pouvez utiliser les exemples de requête suivants pour continuer l’analyse des données de vol :</span><span class="sxs-lookup"><span data-stu-id="67f56-230">You can use the following example queries to continue analysis of the flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="67f56-231">Les 5 principales destinations (villes) vers lesquelles il y a du retard au départ de Seattle</span><span class="sxs-lookup"><span data-stu-id="67f56-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Graphique des retards principaux Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="67f56-233">Calculer les retards médians par villes de destination au départ de Seattle</span><span class="sxs-lookup"><span data-stu-id="67f56-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Graphique des retards médians Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="67f56-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="67f56-235">Next steps</span></span>

<span data-ttu-id="67f56-236">Si vous ne l’avez pas encore fait, téléchargez le connecteur Spark-Azure Cosmos DB à partir du dépôt GitHub [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) et explorez les ressources supplémentaires dans le dépôt :</span><span class="sxs-lookup"><span data-stu-id="67f56-236">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore the additional resources in the repo:</span></span>

* <span data-ttu-id="67f56-237">[Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples) (Exemples d’agrégations distribuées)</span><span class="sxs-lookup"><span data-stu-id="67f56-237">[Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)</span></span>
* <span data-ttu-id="67f56-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples) (Exemples de scripts et blocs-notes)</span><span class="sxs-lookup"><span data-stu-id="67f56-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)</span></span>

<span data-ttu-id="67f56-239">Vous pouvez également consulter [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) (Guide sur Apache Spark SQL, les tableaux de données et les jeux de données) et l’article [Apache Spark sur Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="67f56-239">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
