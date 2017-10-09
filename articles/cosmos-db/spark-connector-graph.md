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
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a>Azure Cosmos DB : Exécuter des analyses graphiques à l’aide de Spark et d’Apache TinkerPop Gremlin

[Base de données Azure Cosmos](introduction.md) est hello service de base de données distribués internationalement, comportant plusieurs modèles à partir de Microsoft. Vous pouvez créer et interroger des bases de données de graphique, de bénéficier de fonctionnalités de distribution globale et à l’échelle horizontale de hello au cœur de hello de base de données Azure Cosmos document et clé/valeur. Azure Cosmos DB prend en charge les charges de travail graphiques OLTP (traitement des transactions en ligne) qui utilisent [Apache TinkerPop Gremlin](graph-introduction.md).

[Spark](http://spark.apache.org/) est un projet Apache Software Foundation consacré au traitement des données OLAP (traitement analytique en ligne) à usage général. Spark fournit un hybride dans-mémoire/basée sur disque modèle informatique distribué qui est similaire toohello Hadoop MapReduce modèle. Vous pouvez déployer Apache Spark dans le cloud de hello en utilisant [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

En associant Azure Cosmos DB et Spark, vous pouvez exécuter des charges de travail OLTP et OLAP lorsque vous utilisez Gremlin. Cet article de démarrage rapide montre comment des requêtes par rapport à la base de données Azure Cosmos toorun GREMLINE sur un cluster Azure HDInsight Spark.

## <a name="prerequisites"></a>Composants requis

Avant de pouvoir exécuter cet exemple, vous devez disposer de hello suivant des conditions préalables :
* Cluster Azure HDInsight Spark 2.0
* JDK 1.8 + (exécutez `apt-get install default-jdk` si vous ne possédez pas JDK)
* Maven (exécutez `apt-get install maven` si vous ne possédez pas Maven)
* Un abonnement Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])

Pour plus d’informations sur la façon tooset configuration d’un cluster Azure HDInsight Spark, consultez [HDInsight de configuration des clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

## <a name="create-an-azure-cosmos-db-database-account"></a>Créer un compte de base de données Azure Cosmos DB

Commencez par créer un compte de base de données avec hello API Graph de manière hello suivante :

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Ajouter une collection

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a>Obtenir Apache TinkerPop

Obtenir Apache TinkerPop de manière hello suivante :

1. Toohello à distance le nœud principal du cluster HDInsight de hello `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.

2. Clone de code source de TinkerPop3 hello, générez-le localement et installez-le tooMaven cache.

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. Installer hello Spark-GREMLINE plug-in 

    a. installation de Hello Hello plug-in est gérée par raisins. Remplir les informations de référentiels hello pour raisins afin de pouvoir télécharger le plug-in de hello et ses dépendances. 

      Créer le fichier de configuration raisins hello si elle n’est pas présent à `~/.groovy/grapeConfig.xml`. Utilisez hello suivant les paramètres :

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

    b. Démarrez la console Gremlin `bin/gremlin.sh`.
        
    c. Installer hello Spark-GREMLINE plug-in avec version 3.3.0-SNAPSHOT, que vous avez construit dans les étapes précédentes hello :

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

4. Vérifiez si les toosee `Hadoop-Gremlin` est activé avec `:plugin list`. Désactiver ce plug-in, car il peut interférer avec hello Spark-GREMLINE plug-in `:plugin unuse tinkerpop.hadoop`.

## <a name="prepare-tinkerpop3-dependencies"></a>Préparer les dépendances TinkerPop3

Lorsque vous avez généré TinkerPop3 à l’étape précédente de hello, processus de hello également extrait toutes les dépendances de fichier jar pour Spark et Hadoop dans le répertoire cible de hello. Utilisez les fichiers JAR hello est pré-installé HDI et extraire les dépendances supplémentaires uniquement si nécessaire.

1. Répertoire de cible GREMLINE Console toohello accédez à `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`. 

2. Déplacer tous les fichiers JAR sous `ext/` trop`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.

3. Supprimer tous les jar bibliothèques sous `lib/` qu’est hello ne figurant pas dans les suivantes : liste :

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a>Obtenir le connecteur de Azure Cosmos DB Spark hello

1. Obtenir le connecteur de Azure Cosmos DB Spark hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` et Kit de développement Java Cosmos DB `azure-documentdb-1.10.0.jar` de [Azure Cosmos DB Spark connecteur sur GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).

2. Sinon, vous pouvez le créer localement. Étant donné que la version la plus récente de Spark-GREMLINE hello a été générée avec Spark 1.6.1 et n’est pas compatible avec Spark 2.0.2, qui est actuellement utilisé dans le connecteur du moteur de base de données Azure Cosmos hello, vous pouvez générer du code de TinkerPop3 dernière hello et installer manuellement les fichiers JAR hello. Hello suivant :

    a. Cloner le connecteur du moteur de base de données Azure Cosmos hello.

    b. Générer TinkerPop3 (déjà effectué lors des étapes précédentes). Installez tous les fichiers JAR TinkerPop 3.3.0-SNAPSHOT localement.

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    c. Mise à jour `tinkerpop.version` `azure-documentdb-spark/pom.xml` trop`3.3.0-SNAPSHOT`.
    
    d. Générer avec Maven. fichiers JAR nécessaires Hello est placés dans `target` et `target/alternateLocation`.

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. Répertoire local de fichiers JAR tooa à mentionnés plus haut hello de copie ~ / azure-documentdb-spark :

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a>Distribuer des nœuds de travail Spark hello dépendances toohello 

1. Transformation hello de données de graphique dépendant de TinkerPop3, vous devez distribuer hello relatives des nœuds de travail dépendances tooall Spark.

2. Hello de copie mentionnés précédemment GREMLINE dépendances, hello jar de connecteur CosmosDB Spark et nœuds de travail toohello CosmosDB Java SDK de manière hello suivante :

    a. Copiez tous les fichiers JAR hello dans `~/azure-documentdb-spark`.

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    b. Obtenir la liste de hello de tous les nœuds de travail Spark, que vous pouvez trouver sur le tableau de bord Ambari, Bonjour `Spark2 Clients` liste Bonjour `Spark2` section.

    c. Copiez ce tooeach active des nœuds de hello.

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a>Configurer les variables d’environnement hello

1. Version HDP de hello du cluster de Spark hello introuvable. Il est le nom du répertoire hello sous `/usr/hdp/` (par exemple, 2.5.4.2-7).

2. Définissez hdp.version pour tous les nœuds. Dans le tableau de bord Ambari, accédez trop**section des fils** > **Configs** > **avancé**et puis hello suivant : 
 
    a. Dans `Custom yarn-site`, ajouter une nouvelle propriété `hdp.version` avec la valeur hello de version HDP hello sur le nœud principal de hello. 
     
    b. Enregistrer les configurations de hello. Vous pouvez ignorer les avertissements. 
     
    c. Redémarrez les services de fils et Oozie hello comme indiquent les icônes de notification hello.

3. Hello ensemble suivant de variables d’environnement sur le nœud principal de hello (remplacer des valeurs hello selon le cas) :

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a>Préparer la configuration du graphique hello

1. Créer un fichier de configuration avec hello les paramètres de connexion de base de données Azure Cosmos et au service de paramètres et le placer à `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.

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

2. Hello de mise à jour `spark.driver.extraClassPath` et `spark.executor.extraClassPath` répertoire de hello tooinclude des fichiers JAR hello que vous avez distribué à l’étape précédente de hello, dans ce cas `/home/sshuser/azure-documentdb-spark/*`.

3. Fournir les détails suivants pour la base de données Azure Cosmos de hello :

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a>Charger hello TinkerPop graphique et l’enregistrer tooAzure Cosmos DB
toodemonstrate comment toopersist un graphique dans Azure Cosmos DB, cet exemple utilise hello TinkerPop prédéfinies TinkerPop les graphique moderne. graphique de Hello est stocké au format de Kryo, et il est fourni dans le référentiel de TinkerPop hello.

1. Car GREMLINE sont en cours d’exécution en mode de fils, vous devez rendre les données de graphique hello disponible Bonjour système de fichiers Hadoop. Commandes suivantes de hello utilisation toomake un répertoire et copier le fichier graphique local hello dans celui-ci. 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. Mettre à jour temporairement de hello `gremlin-spark.properties` toouse de fichiers `GryoInputFormat` graphique de hello tooread. Indiquer également `inputLocation` comme répertoire de hello vous créez, comme dans les éléments suivants de hello :

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. Démarrez la Console de GREMLINE et ensuite créer hello suivant de collecte de base de données Azure Cosmos calcul étapes toopersist données toohello configuré :  

    a. Créer le graphique de hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.

    b. Utilisez SparkGraphComputer pour écrire `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.

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

4. À partir de l’Explorateur de données, vous pouvez vérifier que hello données ont été rendues persistantes tooAzure Cosmos DB.

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a>Graphique de hello de charge à partir de la base de données Azure Cosmos et exécuter des requêtes de GREMLINE

1. graphique de hello tooload, modifier `gremlin-spark.properties` tooset `graphReader` trop`DocumentDBInputRDD`:

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. Graphique de charge hello, parcourir des données de hello et exécuter des requêtes de GREMLINE avec lui en procédant comme suit de hello :

    a. Démarrer hello GREMLINE Console `bin/gremlin.sh`.

    b. Créer un graphique de hello avec une configuration hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.

    c. Créez une traversée de graphique avec SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.

    d. Exécutez hello GREMLINE graphique requêtes suivantes :

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
> toosee plus détaillée journalisation, définie le niveau de journal hello dans `conf/log4j-console.properties` tooa niveau plus détaillé.
>

## <a name="next-steps"></a>Étapes suivantes

Dans cet article de démarrage rapide, vous avez appris comment toowork avec des graphiques en combinant la base de données Azure Cosmos et Spark.

> [!div class="nextstepaction"]
