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
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="a0ad1-104">Accélérer l’analytique de données volumineuses en temps réel avec le connecteur de base de données Cosmos hello Spark tooAzure</span><span class="sxs-lookup"><span data-stu-id="a0ad1-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="a0ad1-105">connecteur de base de données Cosmos Hello Spark tooAzure Active tooact de base de données Azure Cosmos en tant qu’entrée source ou récepteur de sortie pour les travaux d’Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="a0ad1-106">Connexion [Spark](http://spark.apache.org/) trop[base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) accélère votre capacité toosolve rapide science des données où vous pouvez utiliser la base de données Azure Cosmos tooquickly les problèmes persistent et interroger des données.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="a0ad1-107">connecteur de base de données Cosmos Hello Spark tooAzure utilise efficacement les index de base de données Azure Cosmos gérés natifs hello.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="a0ad1-108">index de Hello permettent des colonnes modifiables lorsque vous effectuez analytique et prédicat rabat vers le bas le filtrage par rapport à la modification rapide globalement distribués de données, allant des scénarios Internet des objets (IoT) toodata science et analytique.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="a0ad1-109">Pour utiliser Spark GraphX et graphique de GREMLINE hello API de Cosmos base de données Azure, consultez [effectuer analytique de graphique à l’aide de Spark et Apache TinkerPop GREMLINE](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="a0ad1-110">Télécharger</span><span class="sxs-lookup"><span data-stu-id="a0ad1-110">Download</span></span>

<span data-ttu-id="a0ad1-111">tooget démarré, télécharger le connecteur de base de données Cosmos tooAzure hello Spark (version préliminaire) à partir de hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="a0ad1-112">Composants du connecteur</span><span class="sxs-lookup"><span data-stu-id="a0ad1-112">Connector components</span></span>

<span data-ttu-id="a0ad1-113">connecteur de Hello utilise hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="a0ad1-114">[Base de données Azure Cosmos](http://documentdb.com) Active tooprovision de clients et de façon élastique mettre à l’échelle à la fois de débit et de stockage entre plusieurs régions géographiques.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="a0ad1-115">offres de service Hello :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-115">hello service offers:</span></span>
   * <span data-ttu-id="a0ad1-116">[Distribution globale](distribute-data-globally.md) et échelle horizontale clé en main</span><span class="sxs-lookup"><span data-stu-id="a0ad1-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="a0ad1-117">Garantie de latences chiffre à 99e centile de hello</span><span class="sxs-lookup"><span data-stu-id="a0ad1-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * [<span data-ttu-id="a0ad1-118">Différents modèles de cohérence bien définis</span><span class="sxs-lookup"><span data-stu-id="a0ad1-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="a0ad1-119">Haute disponibilité garantie avec capacités d’hébergement multiple</span><span class="sxs-lookup"><span data-stu-id="a0ad1-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="a0ad1-120">Toutes les fonctionnalités sont garanties par des [contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA) complets, les meilleurs du marché.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="a0ad1-121">[Apache Spark](http://spark.apache.org/) est un puissant moteur de traitement Open Source axé sur la vitesse, la facilité d’utilisation et des analyses sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="a0ad1-122">[Apache Spark sur Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) afin que vous puissiez déployer Apache Spark dans cloud hello pour les déploiements stratégiques à l’aide de [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="a0ad1-123">Versions officiellement prises en charge :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-123">Officially supported versions:</span></span>

| <span data-ttu-id="a0ad1-124">Composant</span><span class="sxs-lookup"><span data-stu-id="a0ad1-124">Component</span></span> | <span data-ttu-id="a0ad1-125">Version</span><span class="sxs-lookup"><span data-stu-id="a0ad1-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="a0ad1-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="a0ad1-126">Apache Spark</span></span>|<span data-ttu-id="a0ad1-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="a0ad1-127">2.0+</span></span>|
| <span data-ttu-id="a0ad1-128">Scala</span><span class="sxs-lookup"><span data-stu-id="a0ad1-128">Scala</span></span>| <span data-ttu-id="a0ad1-129">2.11</span><span class="sxs-lookup"><span data-stu-id="a0ad1-129">2.11</span></span>|
| <span data-ttu-id="a0ad1-130">Kit de développement logiciel (SDK) Azure DocumentDB Java</span><span class="sxs-lookup"><span data-stu-id="a0ad1-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="a0ad1-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="a0ad1-131">1.10.0</span></span> |

<span data-ttu-id="a0ad1-132">Cet article vous permet d’exécuter certains exemples simples (via pyDocumentDB) à l’aide de Python et hello Scala interfaces.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="a0ad1-133">Il existe deux approches tooconnect Apache Spark et la base de données Azure Cosmos :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="a0ad1-134">Utilisez pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="a0ad1-135">Création d’un connecteur de Cosmos DB de tooAzure Spark de basée sur Java à l’aide de hello [Kit de développement Java Azure DocumentDB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="a0ad1-136">Implémentation de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="a0ad1-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="a0ad1-137">Hello actuel [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) vous permet de tooconnect Spark tooAzure Cosmos DB comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Spark tooAzure Cosmos DB des flux de données via pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="a0ad1-139">Flux de données de mise en œuvre de hello pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="a0ad1-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="a0ad1-140">flux de données Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="a0ad1-141">nœud de Hello Spark maître connecte à nœud de passerelle de base de données Azure Cosmos toohello via pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="a0ad1-142">Un utilisateur spécifie uniquement aux connexions de hello Spark et de la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="a0ad1-143">Connexions toohello master et passerelle leurs nœuds respectifs sont transparentes toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="a0ad1-144">nœud de passerelle Hello rend la requête de hello sur la base de données Azure Cosmos où hello requête s’exécute par la suite par rapport aux partitions de la collection hello dans les nœuds de données hello.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="a0ad1-145">réponse Hello pour ces requêtes est renvoyé nœud de passerelle toohello et ce jeu de résultats est renvoyé un nœud principal de toohello Spark.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="a0ad1-146">Les requêtes ultérieures (par exemple, sur une trame de données Spark) sont envoyés les nœuds de travail Spark toohello pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="a0ad1-147">Communication entre Spark et de base de données Azure Cosmos est limitée toohello nœud maître de Spark et nœuds de passerelle de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="a0ad1-148">les requêtes Hello accédez aussi rapidement que permet de la couche de transport hello entre ces deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="a0ad1-149">Installer pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="a0ad1-149">Install pyDocumentDB</span></span>
<span data-ttu-id="a0ad1-150">Vous pouvez installer pyDocumentDB sur votre nœud de pilote à l’aide de **pip**, par exemple :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="a0ad1-151">Se connecter tooAzure Spark Cosmos DB via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="a0ad1-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="a0ad1-152">simplicité Hello de transport de communication hello rend l’exécution d’une requête à partir de Spark tooAzure Cosmos DB à l’aide de pyDocumentDB relativement simple.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="a0ad1-153">Hello suivant extrait de code montre comment pyDocumentDB toouse dans un contexte de Spark.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

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

<span data-ttu-id="a0ad1-154">Comme indiqué dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="a0ad1-155">Bonjour Azure Cosmos DB Python SDK (`pyDocumentDB`) contient hello tous hello des paramètres de connexion.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="a0ad1-156">Par exemple, de préférence hello paramètre des emplacements choisit l’ordre de priorité et le réplica de lecture hello.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="a0ad1-157">Importer les bibliothèques nécessaires hello et configurer votre **masterKey** et **hôte** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_ client**).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="a0ad1-158">Exécuter des requêtes Spark via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="a0ad1-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="a0ad1-159">Hello suivant l’instance de base de données Azure Cosmos exemples utilisez hello qui a été créée dans l’extrait de code hello précédente à l’aide de hello spécifié en lecture seule des clés.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="a0ad1-160">Hello extrait de code suivant connecte toohello **airports.codes** collection dans le compte de DoctorWho hello comme spécifié précédemment et exécute un aéroport de hello tooextract requête villes dans l’état de Washington.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

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

<span data-ttu-id="a0ad1-161">Après l’exécution de requête de hello via **requête**, hello résultat est un **query_iterable. QueryIterable** qui est le liste de Python tooa converti.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="a0ad1-162">Une liste de Python peut être facilement converti tooa Spark de trame de données à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="a0ad1-163">Pourquoi utiliser hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="a0ad1-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="a0ad1-164">Connexion tooAzure Spark Cosmos DB à l’aide de pyDocumentDB est généralement pour les scénarios où :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="a0ad1-165">Vous souhaitez toouse Python.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-165">You want toouse Python.</span></span>
* <span data-ttu-id="a0ad1-166">Vous retournez un jeu à partir de la base de données Azure Cosmos tooSpark de résultats relativement faible.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="a0ad1-167">Notez que hello dataset sous-jacent dans la base de données Azure Cosmos peuvent être assez volumineux.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="a0ad1-168">Vous appliquez des filtres, c’est-à-dire que vous exécutez des filtres de prédicat, sur votre source Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="a0ad1-169">Spark tooAzure connecteur Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a0ad1-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="a0ad1-170">connecteur de base de données Cosmos Hello Spark tooAzure utilise hello [Kit de développement Java Azure DocumentDB](https://github.com/Azure/azure-documentdb-java) et déplace les données entre les nœuds de travail Spark hello et la base de données Azure Cosmos comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Flux de données dans le connecteur de base de données Cosmos hello Spark tooAzure](./media/spark-connector/spark-connector.png)

<span data-ttu-id="a0ad1-172">flux de données Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="a0ad1-173">nœud de Hello Spark maître connecte toohello base de données Azure Cosmos passerelle nœud tooobtain hello mappage.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="a0ad1-174">Un utilisateur spécifie uniquement aux connexions de hello Spark et de la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="a0ad1-175">Connexions toohello master et passerelle leurs nœuds respectifs sont transparentes toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="a0ad1-176">Ces informations sont fournies de nœud principal de Spark toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="a0ad1-177">À ce stade, vous devez être en mesure de tooparse hello requête toodetermine hello partitions et les leurs emplacements dans la base de données Azure Cosmos que vous avez besoin de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="a0ad1-178">Ces informations sont transmises toohello Spark de nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="a0ad1-179">nœuds de travail Hello Spark connectent partitions de base de données Azure Cosmos toohello directement tooextract hello des données et retourner des partitions de Spark hello données toohello dans les nœuds de travail hello Spark.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="a0ad1-180">Communication entre Spark et de la base de données Azure Cosmos est nettement plus rapide, car le déplacement des données de hello est entre les nœuds de données de base de données Azure Cosmos hello (partitions) et les nœuds de travail Spark hello.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="a0ad1-181">Créer le connecteur de base de données Cosmos hello Spark tooAzure</span><span class="sxs-lookup"><span data-stu-id="a0ad1-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="a0ad1-182">Actuellement, le projet de connecteur hello utilise maven.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="a0ad1-183">connecteur de hello toobuild sans dépendances, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="a0ad1-184">Vous pouvez également télécharger des versions les plus récentes de hello JAR hello du hello *libère* dossier.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="a0ad1-185">Inclure hello JAR de Spark Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a0ad1-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="a0ad1-186">Avant d’exécuter n’importe quel code, vous devez hello tooinclude JAR de Spark Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="a0ad1-187">Si vous utilisez hello **spark-shell**, vous pouvez inclure hello JAR à l’aide de hello **--fichiers JAR** option.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="a0ad1-188">Si vous souhaitez tooexecute hello JAR sans dépendances, utilisez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="a0ad1-189">Si vous utilisez un service de l’ordinateur portable comme Azure HDInsight Notebook portable, vous pouvez utiliser hello **nouvelles magic** commandes :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="a0ad1-190">Hello **JAR** commande permet de vous tooinclude hello deux fichiers JAR qui sont nécessaires pour **azure-cosmosdb-spark** (lui-même et hello Kit de développement Java Azure DocumentDB) et exclure **scala-refléter** afin qu’elle n’interfère pas avec hello Livy appelle (bloc-notes jupyter > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="a0ad1-191">Se connecter Spark tooAzure à l’aide de base de données Cosmos hello connecteur</span><span class="sxs-lookup"><span data-stu-id="a0ad1-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="a0ad1-192">Bien que le transport de communication hello est un peu plus compliqué, l’exécution d’une requête à partir de Spark tooAzure DB Cosmos à l’aide du connecteur de hello est considérablement plus rapide.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="a0ad1-193">Hello suivant extrait de code montre comment toouse hello connecteur dans un contexte de Spark.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

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

<span data-ttu-id="a0ad1-194">Comme indiqué dans l’extrait de code hello :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="a0ad1-195">**Azure-cosmosdb-spark** contient hello tous hello les paramètres de connexion nécessaires, lesquels incluent des emplacements de hello préféré.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="a0ad1-196">Par exemple, vous pouvez choisir de hello lire l’ordre de priorité et de réplica.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="a0ad1-197">Uniquement les bibliothèques nécessaires hello d’importation et configurer votre client de base de données Azure Cosmos de hello toocreate clé principale et de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="a0ad1-198">Exécuter des requêtes Spark via le connecteur de hello</span><span class="sxs-lookup"><span data-stu-id="a0ad1-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="a0ad1-199">Hello suivant l’instance de base de données Azure Cosmos exemple utilise hello qui a été créé dans l’extrait de code hello précédente à l’aide de hello spécifié en lecture seule des clés.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="a0ad1-200">Hello extrait de code suivant connecte toohello DepartureDelays.flights_pcoll collection (hello compte DoctorWho comme indiqué précédemment) et exécute une requête tooextract hello flight delay d’informations de vols qui sont au départ de Seattle.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="a0ad1-201">Pourquoi utiliser la mise en œuvre de hello Spark tooAzure Cosmos DB connecteur ?</span><span class="sxs-lookup"><span data-stu-id="a0ad1-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="a0ad1-202">Connexion tooAzure Spark Cosmos DB à l’aide du connecteur de hello est généralement pour les scénarios où :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="a0ad1-203">Vous souhaitez toouse Scala et mettre à jour tooinclude un wrapper de Python, comme indiqué dans [problème 3 : wrapper d’ajouter les Python et des exemples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="a0ad1-204">Vous avez une grande quantité de données des tootransfer entre Apache Spark et de la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="a0ad1-205">toogive vous une idée de la différence de performances de requête hello, consultez hello [wiki de séries de tests de requête](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="a0ad1-206">Exemple d’agrégations distribuées</span><span class="sxs-lookup"><span data-stu-id="a0ad1-206">Distributed aggregation example</span></span>
<span data-ttu-id="a0ad1-207">Cette section fournit des exemples montrant comment réaliser des agrégations distribuées et des analyses à l’aide d’Apache Spark et d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="a0ad1-208">Base de données Azure Cosmos prend déjà en charge agrégations, qui est décrite dans hello [agrégats de montée en puissance planète avec la base de données Azure Cosmos blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="a0ad1-209">Voici comment vous pouvez mettre toohello ensuite niveau avec Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="a0ad1-210">Notez que ces agrégations sont dans la référence toohello [bloc-notes de connecteur de base de données Cosmos Spark tooAzure](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="a0ad1-211">Connecter des données d’exemple tooflights</span><span class="sxs-lookup"><span data-stu-id="a0ad1-211">Connect tooflights sample data</span></span>
<span data-ttu-id="a0ad1-212">Ces exemples d’agrégations accèdent à certaines données de performances de vol stockées dans notre base de données Azure Cosmos DB **DoctorWho**.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="a0ad1-213">tooconnect tooit, vous devez hello tooutilize suivant l’extrait de code :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

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

<span data-ttu-id="a0ad1-214">Cet extrait de code, nous sommes également continu toorun une requête de base que les transferts hello ensemble filtré de données à partir de la base de données Azure Cosmos tooSpark où hello ce dernier peut effectuer des agrégats distribuées.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="a0ad1-215">Dans ce cas, nous demandons les vols au départ de Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="a0ad1-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="a0ad1-216">Hello résultats suivants ont été générés en exécutant des requêtes de hello de hello service de bloc-notes Notebook.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="a0ad1-217">Notez que tous les extraits de code hello sont génériques et non spécifiques tooany service.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="a0ad1-218">Exécution des requêtes LIMIT et COUNT</span><span class="sxs-lookup"><span data-stu-id="a0ad1-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="a0ad1-219">Tout comme vous avez utilisé tooin SQL/Spark SQL, nous allons commencer avec un **limite** requête :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Requête LIMIT Spark](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="a0ad1-221">Hello requête suivant est une simple et rapide **nombre** requête :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Requête COUNT Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="a0ad1-223">Requête GROUP BY</span><span class="sxs-lookup"><span data-stu-id="a0ad1-223">GROUP BY query</span></span>
<span data-ttu-id="a0ad1-224">Dans le jeu suivant, nous pouvons facilement exécuter des requêtes **GROUP BY** sur notre base de données Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Graphique de la requête GROUP BY Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="a0ad1-226">Requête DISTINCT, ORDER BY</span><span class="sxs-lookup"><span data-stu-id="a0ad1-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="a0ad1-227">Et voici une requête **DISTINCT, ORDER BY** :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Graphique de la requête GROUP BY Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="a0ad1-229">Continuer l’analyse de données de vol hello</span><span class="sxs-lookup"><span data-stu-id="a0ad1-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="a0ad1-230">Vous pouvez utiliser hello suivant l’exemple d’analyse toocontinue requêtes hello de données de vol :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="a0ad1-231">Les 5 principales destinations (villes) vers lesquelles il y a du retard au départ de Seattle</span><span class="sxs-lookup"><span data-stu-id="a0ad1-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Graphique des retards principaux Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="a0ad1-233">Calculer les retards médians par villes de destination au départ de Seattle</span><span class="sxs-lookup"><span data-stu-id="a0ad1-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Graphique des retards médians Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="a0ad1-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0ad1-235">Next steps</span></span>

<span data-ttu-id="a0ad1-236">Si vous n’avez pas encore, télécharger le connecteur de base de données Cosmos hello Spark tooAzure de hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) référentiel GitHub et Explorer des ressources supplémentaires hello dans le référentiel de hello :</span><span class="sxs-lookup"><span data-stu-id="a0ad1-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* <span data-ttu-id="a0ad1-237">[Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples) (Exemples d’agrégations distribuées)</span><span class="sxs-lookup"><span data-stu-id="a0ad1-237">[Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)</span></span>
* <span data-ttu-id="a0ad1-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples) (Exemples de scripts et blocs-notes)</span><span class="sxs-lookup"><span data-stu-id="a0ad1-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)</span></span>

<span data-ttu-id="a0ad1-239">Vous pouvez également vous tooreview hello [Apache Spark SQL, les trames de données et les jeux de données Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) et hello [Apache Spark sur Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="a0ad1-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
