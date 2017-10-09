---
title: "Azure Cosmos DB : Exécuter des analyses graphiques à l’aide de Spark et d’Apache TinkerPop Gremlin | Microsoft Docs"
description: "Cet article présente les instructions de configuration et d’exécution des analyses graphiques et du calcul parallèle dans Azure Cosmos DB avec Spark et TinkerPop SparkGraphComputer."
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="a35d0-103">Azure Cosmos DB : Exécuter des analyses graphiques à l’aide de Spark et d’Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="a35d0-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="a35d0-104">[Base de données Azure Cosmos](introduction.md) est hello service de base de données distribués internationalement, comportant plusieurs modèles à partir de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a35d0-104">[Azure Cosmos DB](introduction.md) is hello globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="a35d0-105">Vous pouvez créer et interroger des bases de données de graphique, de bénéficier de fonctionnalités de distribution globale et à l’échelle horizontale de hello au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="a35d0-105">You can create and query document, key/value, and graph databases, all of which benefit from hello global-distribution and horizontal-scale capabilities at hello core of Azure Cosmos DB.</span></span> <span data-ttu-id="a35d0-106">Azure Cosmos DB prend en charge les charges de travail graphiques OLTP (traitement des transactions en ligne) qui utilisent [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a35d0-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="a35d0-107">[Spark](http://spark.apache.org/) est un projet Apache Software Foundation consacré au traitement des données OLAP (traitement analytique en ligne) à usage général.</span><span class="sxs-lookup"><span data-stu-id="a35d0-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="a35d0-108">Spark fournit un hybride dans-mémoire/basée sur disque modèle informatique distribué qui est similaire toohello Hadoop MapReduce modèle.</span><span class="sxs-lookup"><span data-stu-id="a35d0-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar toohello Hadoop MapReduce model.</span></span> <span data-ttu-id="a35d0-109">Vous pouvez déployer Apache Spark dans le cloud de hello en utilisant [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="a35d0-109">You can deploy Apache Spark in hello cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="a35d0-110">En associant Azure Cosmos DB et Spark, vous pouvez exécuter des charges de travail OLTP et OLAP lorsque vous utilisez Gremlin.</span><span class="sxs-lookup"><span data-stu-id="a35d0-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="a35d0-111">Cet article de démarrage rapide montre comment des requêtes par rapport à la base de données Azure Cosmos toorun GREMLINE sur un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="a35d0-111">This quick-start article demonstrates how toorun Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a35d0-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a35d0-112">Prerequisites</span></span>

<span data-ttu-id="a35d0-113">Avant de pouvoir exécuter cet exemple, vous devez disposer de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="a35d0-113">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="a35d0-114">Cluster Azure HDInsight Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="a35d0-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="a35d0-115">JDK 1.8 + (exécutez `apt-get install default-jdk` si vous ne possédez pas JDK)</span><span class="sxs-lookup"><span data-stu-id="a35d0-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="a35d0-116">Maven (exécutez `apt-get install maven` si vous ne possédez pas Maven)</span><span class="sxs-lookup"><span data-stu-id="a35d0-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="a35d0-117">Un abonnement Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="a35d0-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="a35d0-118">Pour plus d’informations sur la façon tooset configuration d’un cluster Azure HDInsight Spark, consultez [HDInsight de configuration des clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a35d0-118">For information about how tooset up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="a35d0-119">Créer un compte de base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a35d0-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="a35d0-120">Commencez par créer un compte de base de données avec hello API Graph de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="a35d0-120">First, create a database account with hello Graph API by doing hello following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="a35d0-121">Ajouter une collection</span><span class="sxs-lookup"><span data-stu-id="a35d0-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="a35d0-122">Obtenir Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="a35d0-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="a35d0-123">Obtenir Apache TinkerPop de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="a35d0-123">Get Apache TinkerPop by doing hello following:</span></span>

1. <span data-ttu-id="a35d0-124">Toohello à distance le nœud principal du cluster HDInsight de hello `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-124">Remote toohello master node of hello HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="a35d0-125">Clone de code source de TinkerPop3 hello, générez-le localement et installez-le tooMaven cache.</span><span class="sxs-lookup"><span data-stu-id="a35d0-125">Clone hello TinkerPop3 source code, build it locally, and install it tooMaven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="a35d0-126">Installer hello Spark-GREMLINE plug-in</span><span class="sxs-lookup"><span data-stu-id="a35d0-126">Install hello Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="a35d0-127">a.</span><span class="sxs-lookup"><span data-stu-id="a35d0-127">a.</span></span> <span data-ttu-id="a35d0-128">installation de Hello Hello plug-in est gérée par raisins.</span><span class="sxs-lookup"><span data-stu-id="a35d0-128">hello installation of hello plug-in is handled by Grape.</span></span> <span data-ttu-id="a35d0-129">Remplir les informations de référentiels hello pour raisins afin de pouvoir télécharger le plug-in de hello et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="a35d0-129">Populate hello repositories information for Grape so it can download hello plug-in and its dependencies.</span></span> 

      <span data-ttu-id="a35d0-130">Créer le fichier de configuration raisins hello si elle n’est pas présent à `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-130">Create hello grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="a35d0-131">Utilisez hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="a35d0-131">Use hello following settings:</span></span>

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    <span data-ttu-id="a35d0-132">b.</span><span class="sxs-lookup"><span data-stu-id="a35d0-132">b.</span></span> <span data-ttu-id="a35d0-133">Démarrez la console Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="a35d0-134">c.</span><span class="sxs-lookup"><span data-stu-id="a35d0-134">c.</span></span> <span data-ttu-id="a35d0-135">Installer hello Spark-GREMLINE plug-in avec version 3.3.0-SNAPSHOT, que vous avez construit dans les étapes précédentes hello :</span><span class="sxs-lookup"><span data-stu-id="a35d0-135">Install hello Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in hello previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. <span data-ttu-id="a35d0-136">Vérifiez si les toosee `Hadoop-Gremlin` est activé avec `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-136">Check toosee whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="a35d0-137">Désactiver ce plug-in, car il peut interférer avec hello Spark-GREMLINE plug-in `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-137">Disable this plug-in, because it could interfere with hello Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="a35d0-138">Préparer les dépendances TinkerPop3</span><span class="sxs-lookup"><span data-stu-id="a35d0-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="a35d0-139">Lorsque vous avez généré TinkerPop3 à l’étape précédente de hello, processus de hello également extrait toutes les dépendances de fichier jar pour Spark et Hadoop dans le répertoire cible de hello.</span><span class="sxs-lookup"><span data-stu-id="a35d0-139">When you built TinkerPop3 in hello previous step, hello process also pulled all jar dependencies for Spark and Hadoop in hello target directory.</span></span> <span data-ttu-id="a35d0-140">Utilisez les fichiers JAR hello est pré-installé HDI et extraire les dépendances supplémentaires uniquement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a35d0-140">Use hello jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="a35d0-141">Répertoire de cible GREMLINE Console toohello accédez à `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-141">Go toohello Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="a35d0-142">Déplacer tous les fichiers JAR sous `ext/` trop`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-142">Move all jars under `ext/` too`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="a35d0-143">Supprimer tous les jar bibliothèques sous `lib/` qu’est hello ne figurant pas dans les suivantes : liste :</span><span class="sxs-lookup"><span data-stu-id="a35d0-143">Remove all jar libraries under `lib/` that are not in hello following list:</span></span>

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-hello-azure-cosmos-db-spark-connector"></a><span data-ttu-id="a35d0-144">Obtenir le connecteur de Azure Cosmos DB Spark hello</span><span class="sxs-lookup"><span data-stu-id="a35d0-144">Get hello Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="a35d0-145">Obtenir le connecteur de Azure Cosmos DB Spark hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` et Kit de développement Java Cosmos DB `azure-documentdb-1.10.0.jar` de [Azure Cosmos DB Spark connecteur sur GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="a35d0-145">Get hello Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="a35d0-146">Sinon, vous pouvez le créer localement.</span><span class="sxs-lookup"><span data-stu-id="a35d0-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="a35d0-147">Étant donné que la version la plus récente de Spark-GREMLINE hello a été générée avec Spark 1.6.1 et n’est pas compatible avec Spark 2.0.2, qui est actuellement utilisé dans le connecteur du moteur de base de données Azure Cosmos hello, vous pouvez générer du code de TinkerPop3 dernière hello et installer manuellement les fichiers JAR hello.</span><span class="sxs-lookup"><span data-stu-id="a35d0-147">Because hello latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in hello Azure Cosmos DB Spark connector, you can build hello latest TinkerPop3 code and install hello jars manually.</span></span> <span data-ttu-id="a35d0-148">Hello suivant :</span><span class="sxs-lookup"><span data-stu-id="a35d0-148">Do hello following:</span></span>

    <span data-ttu-id="a35d0-149">a.</span><span class="sxs-lookup"><span data-stu-id="a35d0-149">a.</span></span> <span data-ttu-id="a35d0-150">Cloner le connecteur du moteur de base de données Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="a35d0-150">Clone hello Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="a35d0-151">b.</span><span class="sxs-lookup"><span data-stu-id="a35d0-151">b.</span></span> <span data-ttu-id="a35d0-152">Générer TinkerPop3 (déjà effectué lors des étapes précédentes).</span><span class="sxs-lookup"><span data-stu-id="a35d0-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="a35d0-153">Installez tous les fichiers JAR TinkerPop 3.3.0-SNAPSHOT localement.</span><span class="sxs-lookup"><span data-stu-id="a35d0-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="a35d0-154">c.</span><span class="sxs-lookup"><span data-stu-id="a35d0-154">c.</span></span> <span data-ttu-id="a35d0-155">Mise à jour `tinkerpop.version` `azure-documentdb-spark/pom.xml` trop`3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` too`3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="a35d0-156">d.</span><span class="sxs-lookup"><span data-stu-id="a35d0-156">d.</span></span> <span data-ttu-id="a35d0-157">Générer avec Maven.</span><span class="sxs-lookup"><span data-stu-id="a35d0-157">Build with Maven.</span></span> <span data-ttu-id="a35d0-158">fichiers JAR nécessaires Hello est placés dans `target` et `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-158">hello needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="a35d0-159">Répertoire local de fichiers JAR tooa à mentionnés plus haut hello de copie ~ / azure-documentdb-spark :</span><span class="sxs-lookup"><span data-stu-id="a35d0-159">Copy hello previously mentioned jars tooa local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a><span data-ttu-id="a35d0-160">Distribuer des nœuds de travail Spark hello dépendances toohello</span><span class="sxs-lookup"><span data-stu-id="a35d0-160">Distribute hello dependencies toohello Spark worker nodes</span></span> 

1. <span data-ttu-id="a35d0-161">Transformation hello de données de graphique dépendant de TinkerPop3, vous devez distribuer hello relatives des nœuds de travail dépendances tooall Spark.</span><span class="sxs-lookup"><span data-stu-id="a35d0-161">Because hello transformation of graph data depends on TinkerPop3, you must distribute hello related dependencies tooall Spark worker nodes.</span></span>

2. <span data-ttu-id="a35d0-162">Hello de copie mentionnés précédemment GREMLINE dépendances, hello jar de connecteur CosmosDB Spark et nœuds de travail toohello CosmosDB Java SDK de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="a35d0-162">Copy hello previously mentioned Gremlin dependencies, hello CosmosDB Spark connector jar, and CosmosDB Java SDK toohello worker nodes by doing hello following:</span></span>

    <span data-ttu-id="a35d0-163">a.</span><span class="sxs-lookup"><span data-stu-id="a35d0-163">a.</span></span> <span data-ttu-id="a35d0-164">Copiez tous les fichiers JAR hello dans `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-164">Copy all hello jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="a35d0-165">b.</span><span class="sxs-lookup"><span data-stu-id="a35d0-165">b.</span></span> <span data-ttu-id="a35d0-166">Obtenir la liste de hello de tous les nœuds de travail Spark, que vous pouvez trouver sur le tableau de bord Ambari, Bonjour `Spark2 Clients` liste Bonjour `Spark2` section.</span><span class="sxs-lookup"><span data-stu-id="a35d0-166">Get hello list of all Spark worker nodes, which you can find on Ambari Dashboard, in hello `Spark2 Clients` list in hello `Spark2` section.</span></span>

    <span data-ttu-id="a35d0-167">c.</span><span class="sxs-lookup"><span data-stu-id="a35d0-167">c.</span></span> <span data-ttu-id="a35d0-168">Copiez ce tooeach active des nœuds de hello.</span><span class="sxs-lookup"><span data-stu-id="a35d0-168">Copy that directory tooeach of hello nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a><span data-ttu-id="a35d0-169">Configurer les variables d’environnement hello</span><span class="sxs-lookup"><span data-stu-id="a35d0-169">Set up hello environment variables</span></span>

1. <span data-ttu-id="a35d0-170">Version HDP de hello du cluster de Spark hello introuvable.</span><span class="sxs-lookup"><span data-stu-id="a35d0-170">Find hello HDP version of hello Spark cluster.</span></span> <span data-ttu-id="a35d0-171">Il est le nom du répertoire hello sous `/usr/hdp/` (par exemple, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="a35d0-171">It is hello directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="a35d0-172">Définissez hdp.version pour tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="a35d0-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="a35d0-173">Dans le tableau de bord Ambari, accédez trop**section des fils** > **Configs** > **avancé**et puis hello suivant :</span><span class="sxs-lookup"><span data-stu-id="a35d0-173">In Ambari Dashboard, go too**YARN section** > **Configs** > **Advanced**, and then do hello following:</span></span> 
 
    <span data-ttu-id="a35d0-174">a.</span><span class="sxs-lookup"><span data-stu-id="a35d0-174">a.</span></span> <span data-ttu-id="a35d0-175">Dans `Custom yarn-site`, ajouter une nouvelle propriété `hdp.version` avec la valeur hello de version HDP hello sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="a35d0-175">In `Custom yarn-site`, add a new property `hdp.version` with hello value of hello HDP version on hello master node.</span></span> 
     
    <span data-ttu-id="a35d0-176">b.</span><span class="sxs-lookup"><span data-stu-id="a35d0-176">b.</span></span> <span data-ttu-id="a35d0-177">Enregistrer les configurations de hello.</span><span class="sxs-lookup"><span data-stu-id="a35d0-177">Save hello configurations.</span></span> <span data-ttu-id="a35d0-178">Vous pouvez ignorer les avertissements.</span><span class="sxs-lookup"><span data-stu-id="a35d0-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="a35d0-179">c.</span><span class="sxs-lookup"><span data-stu-id="a35d0-179">c.</span></span> <span data-ttu-id="a35d0-180">Redémarrez les services de fils et Oozie hello comme indiquent les icônes de notification hello.</span><span class="sxs-lookup"><span data-stu-id="a35d0-180">Restart hello YARN and Oozie services as hello notification icons indicate.</span></span>

3. <span data-ttu-id="a35d0-181">Hello ensemble suivant de variables d’environnement sur le nœud principal de hello (remplacer des valeurs hello selon le cas) :</span><span class="sxs-lookup"><span data-stu-id="a35d0-181">Set hello following environment variables on hello master node (replace hello values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a><span data-ttu-id="a35d0-182">Préparer la configuration du graphique hello</span><span class="sxs-lookup"><span data-stu-id="a35d0-182">Prepare hello graph configuration</span></span>

1. <span data-ttu-id="a35d0-183">Créer un fichier de configuration avec hello les paramètres de connexion de base de données Azure Cosmos et au service de paramètres et le placer à `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-183">Create a configuration file with hello Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for hello driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. <span data-ttu-id="a35d0-184">Hello de mise à jour `spark.driver.extraClassPath` et `spark.executor.extraClassPath` répertoire de hello tooinclude des fichiers JAR hello que vous avez distribué à l’étape précédente de hello, dans ce cas `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-184">Update hello `spark.driver.extraClassPath` and `spark.executor.extraClassPath` tooinclude hello directory of hello jars that you distributed in hello previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="a35d0-185">Fournir les détails suivants pour la base de données Azure Cosmos de hello :</span><span class="sxs-lookup"><span data-stu-id="a35d0-185">Provide hello following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a><span data-ttu-id="a35d0-186">Charger hello TinkerPop graphique et l’enregistrer tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a35d0-186">Load hello TinkerPop graph, and save it tooAzure Cosmos DB</span></span>
<span data-ttu-id="a35d0-187">toodemonstrate comment toopersist un graphique dans Azure Cosmos DB, cet exemple utilise hello TinkerPop prédéfinies TinkerPop les graphique moderne.</span><span class="sxs-lookup"><span data-stu-id="a35d0-187">toodemonstrate how toopersist a graph into Azure Cosmos DB, this example uses hello TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="a35d0-188">graphique de Hello est stocké au format de Kryo, et il est fourni dans le référentiel de TinkerPop hello.</span><span class="sxs-lookup"><span data-stu-id="a35d0-188">hello graph is stored in Kryo format, and it's provided in hello TinkerPop repository.</span></span>

1. <span data-ttu-id="a35d0-189">Car GREMLINE sont en cours d’exécution en mode de fils, vous devez rendre les données de graphique hello disponible Bonjour système de fichiers Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a35d0-189">Because you are running Gremlin in YARN mode, you must make hello graph data available in hello Hadoop file system.</span></span> <span data-ttu-id="a35d0-190">Commandes suivantes de hello utilisation toomake un répertoire et copier le fichier graphique local hello dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="a35d0-190">Use hello following commands toomake a directory and copy hello local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="a35d0-191">Mettre à jour temporairement de hello `gremlin-spark.properties` toouse de fichiers `GryoInputFormat` graphique de hello tooread.</span><span class="sxs-lookup"><span data-stu-id="a35d0-191">Temporarily update hello `gremlin-spark.properties` file toouse `GryoInputFormat` tooread hello graph.</span></span> <span data-ttu-id="a35d0-192">Indiquer également `inputLocation` comme répertoire de hello vous créez, comme dans les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="a35d0-192">Also indicate `inputLocation` as hello directory you create, as in hello following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="a35d0-193">Démarrez la Console de GREMLINE et ensuite créer hello suivant de collecte de base de données Azure Cosmos calcul étapes toopersist données toohello configuré :</span><span class="sxs-lookup"><span data-stu-id="a35d0-193">Start Gremlin Console, and then create hello following computation steps toopersist data toohello configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="a35d0-194">a.</span><span class="sxs-lookup"><span data-stu-id="a35d0-194">a.</span></span> <span data-ttu-id="a35d0-195">Créer le graphique de hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-195">Create hello graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="a35d0-196">b.</span><span class="sxs-lookup"><span data-stu-id="a35d0-196">b.</span></span> <span data-ttu-id="a35d0-197">Utilisez SparkGraphComputer pour écrire `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. <span data-ttu-id="a35d0-198">À partir de l’Explorateur de données, vous pouvez vérifier que hello données ont été rendues persistantes tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a35d0-198">From Data Explorer, you can verify that hello data has been persisted tooAzure Cosmos DB.</span></span>

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="a35d0-199">Graphique de hello de charge à partir de la base de données Azure Cosmos et exécuter des requêtes de GREMLINE</span><span class="sxs-lookup"><span data-stu-id="a35d0-199">Load hello graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="a35d0-200">graphique de hello tooload, modifier `gremlin-spark.properties` tooset `graphReader` trop`DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="a35d0-200">tooload hello graph, edit `gremlin-spark.properties` tooset `graphReader` too`DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="a35d0-201">Graphique de charge hello, parcourir des données de hello et exécuter des requêtes de GREMLINE avec lui en procédant comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="a35d0-201">Load hello graph, traverse hello data, and run Gremlin queries with it by doing hello following:</span></span>

    <span data-ttu-id="a35d0-202">a.</span><span class="sxs-lookup"><span data-stu-id="a35d0-202">a.</span></span> <span data-ttu-id="a35d0-203">Démarrer hello GREMLINE Console `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-203">Start hello Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="a35d0-204">b.</span><span class="sxs-lookup"><span data-stu-id="a35d0-204">b.</span></span> <span data-ttu-id="a35d0-205">Créer un graphique de hello avec une configuration hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-205">Create hello graph with hello configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="a35d0-206">c.</span><span class="sxs-lookup"><span data-stu-id="a35d0-206">c.</span></span> <span data-ttu-id="a35d0-207">Créez une traversée de graphique avec SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="a35d0-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="a35d0-208">d.</span><span class="sxs-lookup"><span data-stu-id="a35d0-208">d.</span></span> <span data-ttu-id="a35d0-209">Exécutez hello GREMLINE graphique requêtes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a35d0-209">Run hello following Gremlin graph queries:</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> <span data-ttu-id="a35d0-210">toosee plus détaillée journalisation, définie le niveau de journal hello dans `conf/log4j-console.properties` tooa niveau plus détaillé.</span><span class="sxs-lookup"><span data-stu-id="a35d0-210">toosee more detailed logging, set hello log level in `conf/log4j-console.properties` tooa more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="a35d0-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a35d0-211">Next steps</span></span>

<span data-ttu-id="a35d0-212">Dans cet article de démarrage rapide, vous avez appris comment toowork avec des graphiques en combinant la base de données Azure Cosmos et Spark.</span><span class="sxs-lookup"><span data-stu-id="a35d0-212">In this quick-start article, you've learned how toowork with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
