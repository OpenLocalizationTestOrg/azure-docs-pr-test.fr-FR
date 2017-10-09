---
title: "aaaUse Caffe sur Azure HDInsight Spark pour l’apprentissage approfondie distribuée | Documents Microsoft"
description: "Utiliser Caffe sur Azure HDInsight Spark pour une formation approfondie échelonnée"
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>Utiliser Caffe sur Azure HDInsight Spark pour une formation approfondie échelonnée


## <a name="introduction"></a>Introduction

Formation approfondie affecte tous les éléments à partir de soins de santé tootransportation toomanufacturing et bien plus encore. Sociétés activez toodeep d’apprentissage des problèmes toosolve, tels que [classification d’image](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [la reconnaissance vocale](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), la reconnaissance de l’objet et l’ordinateur de traduction. 

Il existe de [nombreux frameworks populaires](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), notamment [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe est un des hello des infrastructures non symboliques de réseau neuronal (impératif) plus célèbre qu’et largement utilisé dans de nombreux domaines, y compris la vision de l’ordinateur. En outre, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combine Caffe et Apache Spark. Dès lors, la formation approfondie échelonnée peut être facilement utilisée sur un cluster Hadoop existant avec des pipelines Spark ETL, pour une complexité du système et une latence moindres pour la prise en charge de l’apprentissage de bout en bout.

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) hello est entièrement géré par le cloud Hadoop offre optimisé clusters analytique d’ouvrir la source pour Spark, Hive, MapReduce, HBase, Storm, Kafka et R Server soutenu par un contrat SLA de 99,9 %. Chacune de ces technologies Big Data ainsi que les applications d’éditeurs de logiciels indépendants (ISV) sont facilement déployables sous forme de clusters gérés, avec une surveillance et une sécurité à l’échelle de l’entreprise.

Certains utilisateurs sont nous demande sur la façon toouse approfondie d’apprentissage sur HDInsight, qui est le produit de PaaS Hadoop de Microsoft. Nous devrons tooshare plus Bonjour futures, mais aujourd'hui, nous souhaitons toosummarize un blog technique sur la façon de toouse Caffe sur HDInsight Spark.

Si vous avez déjà installé Caffe par le passé, vous remarquerez que l’installation de ce framework est quelque peu difficile. Dans ce blog, nous illustrerons tout d’abord comment tooinstall [Caffe sur Spark](https://github.com/yahoo/CaffeOnSpark) pour un cluster HDInsight, puis utilisez hello intégrés MNIST démonstration toodemostrate comment toouse distribués de formation approfondie à l’aide de HDInsight Spark sur des unités centrales.

Il existe quatre étapes principales tooget, elle fonctionne sur HDInsight.

1. Installer des dépendances de hello requis sur tous les nœuds de hello
2. Build Caffe sur Spark sur HDInsight sur le nœud principal de hello
3. Distribuer des nœuds de travail hello hello requis bibliothèques tooall
4. Composer un modèle Caffe et l’exécuter de manière échelonnée

Étant donné que HDInsight est une solution PaaS, il offre plate-forme idéale fonctionnalités - il est relativement facile tooperform certaines tâches. Une des fonctionnalités hello que nous utilisons largement dans ce billet de blog est appelée [Action de Script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), avec laquelle vous pouvez exécuter les commandes shell toocustomize des nœuds de cluster (nœud principal, nœud de traitement ou nœud de périmètre).

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>Étape 1 : Installer les dépendances hello requis sur tous les nœuds de hello

tooget démarré, nous devons les dépendances de hello tooinstall que nous avons besoin. site de Caffe Hello et [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offre certaines wiki très utile pour l’installation des dépendances de hello pour Spark sur fils mode (mode hello pour HDInsight Spark), mais nous devons tooadd un peu plus de dépendances pour la plateforme de HDInsight. Nous utilise l’action de script hello comme indiqué ci-dessous et exécutez-le sur tous les nœuds principaux d’hello et les nœuds de travail. Cette action prendra environ 20 minutes, car ces dépendances sont également associées à d’autres packages. Vous devez le placer dans un emplacement qui est accessible tooyour cluster HDInsight, tel qu’un emplacement de GitHub ou un compte de stockage BLOB hello par défaut.

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


Il existe deux étapes pour action de script hello ci-dessus. première étape de Hello est tooinstall tous hello bibliothèques requises. Ces bibliothèques incluent des hello les bibliothèques nécessaires pour la compilation Caffe (par exemple, gflags, glog) et en cours d’exécution Caffe (tels que numpy). Nous utilisons libatlas pour optimiser l’UC, mais vous pouvez toujours faire suivre hello CaffeOnSpark wiki sur l’installation d’autres bibliothèques d’optimisation, telles que MKL ou CUDA (pour les GPU).

deuxième étape de Hello est toodownload, compiler et installer protobuf 2.5.0 pour Caffe pendant l’exécution. Protobuf 2.5.0 [est requise](https://github.com/yahoo/CaffeOnSpark/issues/87), mais cette version n’est pas disponible en tant que package Ubuntu 16, donc nous devons toocompile à partir de code source de hello. Il existe également quelques ressources sur Internet de hello sur la façon de toocompile, tels que [cela](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply prise en main, vous pouvez exécuter cette action de script par rapport à votre travail de hello tooall cluster les nœuds de nœuds et head (pour HDInsight 3.5). Vous pouvez exécuter des actions de script hello pour un cluster en cours d’exécution, ou vous pouvez également exécuter des actions de script hello pendant le temps de configurer des clusters hello. Pour plus d’informations sur les actions de script hello, consultez la documentation de hello [ici](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![Actions de script tooInstall dépendances](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>Étape 2 : Générez Caffe sur Spark sur HDInsight sur le nœud principal de hello

deuxième étape de Hello est toobuild Caffe sur le nœud principal de hello et distribuez ensuite hello compilé bibliothèques tooall hello de nœuds de travail. Dans cette étape, vous devez trop[ssh dans votre nœud principal](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), puis suivez simplement hello [CaffeOnSpark les processus de génération](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), et Voici le script hello vous pouvez utiliser toobuild CaffeOnSpark avec quelques étapes supplémentaires. 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

Vous devrez peut-être toodo plusieurs indique de quelle documentation hello de CaffeOnSpark. modifications de Hello sont :
- TooCPU uniquement de modifier et utiliser libatlas à cet usage particulier.
- Hello datasets toohello stockage d’objets BLOB, qui est un emplacement partagé qui est accessible tooall de nœuds de travail pour une utilisation ultérieure.
- Put hello compilé stockage de tooBLOB bibliothèques Caffe et ultérieurement, vous allez copier ces nœuds de hello tooall bibliothèques à l’aide de la durée de compilation supplémentaires tooavoid script actions.


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>Résolution des problèmes : An Ant BuildException has occured: exec returned: 2

Lors de la première tentative toobuild CaffeOnSpark, parfois, il indiquera

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

Référentiel de code hello simplement nettoyer par « rendre nettoyer », puis exécuter « rendre build » corrige ce problème, tant que vous disposez les dépendances appropriées hello.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>Résolution des problèmes : Expiration du délai de connexion du référentiel Maven

Parfois maven me donne erreur de délai d’expiration de connexion hello, toobelow similaire :

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

Il sera OK attendez quelques minutes et recommencez simplement code hello de toorebuild, elle peut donc être Maven une certaine manière limites hello le trafic à partir d’une adresse IP donnée.


### <a name="troubleshooting-test-failure-for-caffe"></a>Résolution des problèmes : Défaillance de test Caffe

Vous serez probablement voir un échec de test lors de la vérification finale de hello pour CaffeOnSpark, similaire à ci-dessous. Cela est prabably lié avec encodage UTF-8, mais il ne devrait pas affecter l’utilisation de hello de Caffe

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>Étape 3 : Distribuer les nœuds de travail hello hello requis bibliothèques tooall

étape suivante de Hello est bibliothèques de hello toodistribute (hello essentiellement des bibliothèques dans CaffeOnSpark/caffe-public/distribuer/lib/et CaffeOnSpark/caffe-DIS/distribuer/lib /) les nœuds de hello tooall. À l’étape 2, nous plaçons ces bibliothèques sur le stockage d’objets BLOB, et dans cette étape, nous allons utiliser toocopy des actions de script il tooall hello nœuds principal et les nœuds de travail.

toodo, simple d’exécuter une action de script comme indiqué ci-dessous (vous devez cluster tooyour spécifique de toopoint toohello bon emplacement) :

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

Comme à l’étape 2, nous placer sur le stockage d’objets BLOB qui est accessible tooall hello nœuds de hello, dans cette étape nous simplement copier les nœuds de hello tooall.

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>Étape 4 : Composition d’un modèle Caffe et exécution de ce dernier de manière distribuée.

Après avoir exécuté hello étapes ci-dessus, Caffe est déjà installé sur le nœud principal de hello, et nous sommes toogo bon. étape suivante de Hello est toowrite un modèle Caffe. 

Caffe est à l’aide de « architecture expressive », pour composer un modèle, vous simplement besoin toodefine un fichier de configuration et sans codage (dans la plupart des cas). Jetons un œil sur cette configuration. 

modèle Hello que nous apprendre aujourd'hui est un exemple de modèle pour l’apprentissage de MNIST. base de données Hello MNIST de chiffres manuscrites a un jeu d’apprentissage des exemples de 60 000 et un jeu de test des exemples de 10 000. Il s’agit d’un sous-ensemble d’un jeu plus volumineux de MNIST. les chiffres Hello ont été normalisées de taille et centré dans une image de taille fixe. CaffeOnSpark comporte des datasets de hello toodownload scripts et le convertir en un format correct de hello.

CaffeOnSpark fournit quelques exemples de topologies de réseau associés à la formation MNIST. Il possède une conception agréable de fractionnement de l’architecture en réseau hello (topologie hello du réseau de hello) et l’optimisation. Dans ce cas, deux fichiers sont requis : 

fichier de « Solveur » Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) est utilisé pour surveiller l’optimisation de hello et générer des mises à jour du paramètre. Par exemple, il définit si l’UC ou au GPU qui sera utilisé, nouveautés momentum hello, le nombre d’itérations sera, etc.. Il définit également la typologie de réseau de neurones doit hello utilisation du programme (c'est-à-dire hello deuxième fichier que nous devons). Pour plus d’informations sur le solveur, reportez-vous trop[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).

Pour cet exemple, étant donné que nous utilisons UC plutôt que de GPU, nous devons modifier dernière ligne de hello pour :

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configuration de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

Au besoin, vous pouvez modifier d’autres lignes.

fichier de deuxième Hello (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) définit comment le réseau de neurones hello ressemble à et d’entrée approprié de hello et fichier de sortie. Nous devons également d’emplacement de données d’apprentissage de tooupdate hello fichier tooreflect hello. Modifier hello suivant partie dans lenet_memory_train_test.prototxt (vous devez cluster tooyour spécifique de toopoint toohello bon emplacement) :

- également modifier hello « file:/Users/mridul/bigml/demodl/mnist_train_lmdb » « wasb : / / / projets/machine_learning/image_dataset/mnist_train_lmdb »
- modifier trop de « file:/Users/mridul/bigml/demodl/mnist_test_lmdb/ » « wasb : / / / projets/machine_learning/image_dataset/mnist_test_lmdb »

![Configuration de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

Pour plus d’informations sur la façon dont toodefine hello réseau, vérifiez hello [documentation Caffe MNIST le jeu de données](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

Pour les besoins de hello de cette entrée de blog, nous utilisons simplement cet exemple MNIST simple. Vous devez exécuter la commande hello ci-dessous à partir du nœud principal hello :

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

En fait, il distribue hello requis (lenet_memory_solver.prototxt et lenet_memory_train_test.prototxt) tooeach fils de conteneur, puis définissez les fichiers hello chemin d’accès approprié de chaque tooLD_LIBRARY_PATH pilote/exécuteur Spark, qui est définie dans hello code extrait de code et les points de toohello emplacement précédent qui a les bibliothèques CaffeOnSpark. 

## <a name="monitoring-and-troubleshooting"></a>Surveillance et dépannage

Étant donné que nous utilisons le mode de cluster fils, auquel cas pilote de Spark hello sera conteneur arbitraire de tooan planifiée (et un nœud de travail arbitraire) ne doit s’afficher dans la sortie de console hello quelque chose comme :

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

Si vous souhaitez tooknow que s’est-il passé, vous devez généralement journal tooget hello Spark conducteur, ce qui a plus d’informations. Dans ce cas, vous devez toogo toohello fils toofind hello pertinentes fils des journaux interface utilisateur. Vous pouvez obtenir hello UI fils par cette URL : 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Interface utilisateur Yarn](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

Vous pouvez découvrir le nombre de ressources allouées pour cette application spécifique. Vous pouvez cliquer sur lien de « Planificateur » hello, et vous ne verrez que pour cette application, sont 9 conteneurs en cours d’exécution. Nous demandons fils tooprovide les exécuteurs de 8, et un autre conteneur pour les processus de pilote. 

![Planificateur YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

Vous souhaiterez toocheck hello pilote ou les journaux de conteneur des cas de défaillance. Pour les journaux du pilote, vous pouvez cliquez sur ID de l’application hello dans l’interface utilisateur des fils, puis cliquez sur le bouton « Logs » de hello. les journaux du pilote Hello sont écrites dans stderr.

![Interface utilisateur YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

Par exemple, vous pouvez voir certains erreur hello ci-dessous à partir des journaux de pilote hello, indiquant que vous allouez les exécuteurs de trop nombreuses.

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

Parfois, problème de hello peut se produire dans les exécuteurs plutôt que des pilotes. Dans ce cas, vous devez toocheck hello conteneur journaux. Vous pouvez toujours obtenir les journaux du conteneur hello et obtenez conteneur ayant échoué de hello. Par exemple, vous pouvez rencontrer cette défaillance lors de l’exécution de Caffe.

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

Dans ce cas, vous devez l’ID du conteneur tooget hello a échoué (hello au-dessus de cas, il s’agit container_1485916338528_0008_05_000005). Vous devez ensuite toorun 

    yarn logs -containerId container_1485916338528_0008_03_000005

à partir du nœud principal de hello. L’examen de la défaillance du conteneur indique qu’elle a été provoquée par le mode GPU (là où vous devriez utiliser le mode UC) dans lenet_memory_solver.prototxt.

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>Obtention des résultats

Étant donné que nous sommes allouer les exécuteurs de 8, et la topologie de réseau hello est simple, cela ne vous prendra environ 30 minutes toorun hello de résultats. À partir de la ligne de commande hello, vous pouvez voir que nous placer hello modèle toowasb:///mnist.model et placer hello résultats tooa dossier nommé wasb : / / / mnist_features_result.

Vous pouvez obtenir des résultats de hello en exécutant

    hadoop fs -cat hdfs:///mnist_features_result/*

et le résultat de hello ressemble à :

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

Hello SampleID représente l’ID de hello dans le jeu de données MNIST hello et étiquette de hello est numéro hello hello modèle identifie.


## <a name="conclusion"></a>Conclusion

Dans cette documentation, vous avez tenté de tooinstall CaffeOnSpark avec l’exécution d’un exemple simple. HDInsight est une plateforme de calcul distribué cloud géré complète et est hello meilleur endroit pour l’exécution d’apprentissage automatique et les charges de travail analytique avancée sur le jeu de données volumineux, et pour en savoir plus approfondie distribuée, vous pouvez utiliser Caffe sur learning approfondie de HDInsight Spark tooperform tâches.


## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)

