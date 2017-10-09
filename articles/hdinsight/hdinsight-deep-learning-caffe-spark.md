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
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="77844-103">Utiliser Caffe sur Azure HDInsight Spark pour une formation approfondie échelonnée</span><span class="sxs-lookup"><span data-stu-id="77844-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="77844-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="77844-104">Introduction</span></span>

<span data-ttu-id="77844-105">Formation approfondie affecte tous les éléments à partir de soins de santé tootransportation toomanufacturing et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="77844-105">Deep learning is impacting everything from healthcare tootransportation toomanufacturing, and more.</span></span> <span data-ttu-id="77844-106">Sociétés activez toodeep d’apprentissage des problèmes toosolve, tels que [classification d’image](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [la reconnaissance vocale](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), la reconnaissance de l’objet et l’ordinateur de traduction.</span><span class="sxs-lookup"><span data-stu-id="77844-106">Companies are turning toodeep learning toosolve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="77844-107">Il existe de [nombreux frameworks populaires](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), notamment [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe est un des hello des infrastructures non symboliques de réseau neuronal (impératif) plus célèbre qu’et largement utilisé dans de nombreux domaines, y compris la vision de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="77844-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of hello most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="77844-108">En outre, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combine Caffe et Apache Spark. Dès lors, la formation approfondie échelonnée peut être facilement utilisée sur un cluster Hadoop existant avec des pipelines Spark ETL, pour une complexité du système et une latence moindres pour la prise en charge de l’apprentissage de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="77844-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="77844-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) hello est entièrement géré par le cloud Hadoop offre optimisé clusters analytique d’ouvrir la source pour Spark, Hive, MapReduce, HBase, Storm, Kafka et R Server soutenu par un contrat SLA de 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="77844-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is hello only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="77844-110">Chacune de ces technologies Big Data ainsi que les applications d’éditeurs de logiciels indépendants (ISV) sont facilement déployables sous forme de clusters gérés, avec une surveillance et une sécurité à l’échelle de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="77844-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="77844-111">Certains utilisateurs sont nous demande sur la façon toouse approfondie d’apprentissage sur HDInsight, qui est le produit de PaaS Hadoop de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77844-111">Some users are asking us about how toouse deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="77844-112">Nous devrons tooshare plus Bonjour futures, mais aujourd'hui, nous souhaitons toosummarize un blog technique sur la façon de toouse Caffe sur HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="77844-112">We will have more tooshare in hello future, but today we want toosummarize a technical blog on how toouse Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="77844-113">Si vous avez déjà installé Caffe par le passé, vous remarquerez que l’installation de ce framework est quelque peu difficile.</span><span class="sxs-lookup"><span data-stu-id="77844-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="77844-114">Dans ce blog, nous illustrerons tout d’abord comment tooinstall [Caffe sur Spark](https://github.com/yahoo/CaffeOnSpark) pour un cluster HDInsight, puis utilisez hello intégrés MNIST démonstration toodemostrate comment toouse distribués de formation approfondie à l’aide de HDInsight Spark sur des unités centrales.</span><span class="sxs-lookup"><span data-stu-id="77844-114">In this blog, we will first illustrate how tooinstall [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use hello built-in MNIST demo toodemostrate how toouse Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="77844-115">Il existe quatre étapes principales tooget, elle fonctionne sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77844-115">There are four major steps tooget it work on HDInsight.</span></span>

1. <span data-ttu-id="77844-116">Installer des dépendances de hello requis sur tous les nœuds de hello</span><span class="sxs-lookup"><span data-stu-id="77844-116">Install hello required dependencies on all hello nodes</span></span>
2. <span data-ttu-id="77844-117">Build Caffe sur Spark sur HDInsight sur le nœud principal de hello</span><span class="sxs-lookup"><span data-stu-id="77844-117">Build Caffe on Spark for HDInsight on hello head node</span></span>
3. <span data-ttu-id="77844-118">Distribuer des nœuds de travail hello hello requis bibliothèques tooall</span><span class="sxs-lookup"><span data-stu-id="77844-118">Distribute hello required libraries tooall hello worker nodes</span></span>
4. <span data-ttu-id="77844-119">Composer un modèle Caffe et l’exécuter de manière échelonnée</span><span class="sxs-lookup"><span data-stu-id="77844-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="77844-120">Étant donné que HDInsight est une solution PaaS, il offre plate-forme idéale fonctionnalités - il est relativement facile tooperform certaines tâches.</span><span class="sxs-lookup"><span data-stu-id="77844-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy tooperform some tasks.</span></span> <span data-ttu-id="77844-121">Une des fonctionnalités hello que nous utilisons largement dans ce billet de blog est appelée [Action de Script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), avec laquelle vous pouvez exécuter les commandes shell toocustomize des nœuds de cluster (nœud principal, nœud de traitement ou nœud de périmètre).</span><span class="sxs-lookup"><span data-stu-id="77844-121">One of hello features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands toocustomize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a><span data-ttu-id="77844-122">Étape 1 : Installer les dépendances hello requis sur tous les nœuds de hello</span><span class="sxs-lookup"><span data-stu-id="77844-122">Step 1:  Install hello required dependencies on all hello nodes</span></span>

<span data-ttu-id="77844-123">tooget démarré, nous devons les dépendances de hello tooinstall que nous avons besoin.</span><span class="sxs-lookup"><span data-stu-id="77844-123">tooget started, we need tooinstall hello dependencies we need.</span></span> <span data-ttu-id="77844-124">site de Caffe Hello et [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offre certaines wiki très utile pour l’installation des dépendances de hello pour Spark sur fils mode (mode hello pour HDInsight Spark), mais nous devons tooadd un peu plus de dépendances pour la plateforme de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77844-124">hello Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing hello dependencies for Spark on YARN mode (which is hello mode for HDInsight Spark), but we need tooadd a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="77844-125">Nous utilise l’action de script hello comme indiqué ci-dessous et exécutez-le sur tous les nœuds principaux d’hello et les nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="77844-125">We will use hello script action as below and run it on all hello head nodes and worker nodes.</span></span> <span data-ttu-id="77844-126">Cette action prendra environ 20 minutes, car ces dépendances sont également associées à d’autres packages.</span><span class="sxs-lookup"><span data-stu-id="77844-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="77844-127">Vous devez le placer dans un emplacement qui est accessible tooyour cluster HDInsight, tel qu’un emplacement de GitHub ou un compte de stockage BLOB hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="77844-127">You should put it in some location that is accessible tooyour HDInsight cluster, such as a GitHub location or hello default BLOB storage account.</span></span>

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


<span data-ttu-id="77844-128">Il existe deux étapes pour action de script hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="77844-128">There are two steps in hello script action above.</span></span> <span data-ttu-id="77844-129">première étape de Hello est tooinstall tous hello bibliothèques requises.</span><span class="sxs-lookup"><span data-stu-id="77844-129">hello first step is tooinstall all hello required libraries.</span></span> <span data-ttu-id="77844-130">Ces bibliothèques incluent des hello les bibliothèques nécessaires pour la compilation Caffe (par exemple, gflags, glog) et en cours d’exécution Caffe (tels que numpy).</span><span class="sxs-lookup"><span data-stu-id="77844-130">Those libraries include hello necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="77844-131">Nous utilisons libatlas pour optimiser l’UC, mais vous pouvez toujours faire suivre hello CaffeOnSpark wiki sur l’installation d’autres bibliothèques d’optimisation, telles que MKL ou CUDA (pour les GPU).</span><span class="sxs-lookup"><span data-stu-id="77844-131">We are using libatlas for CPU optimization, but you can always follow hello CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="77844-132">deuxième étape de Hello est toodownload, compiler et installer protobuf 2.5.0 pour Caffe pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="77844-132">hello second step is toodownload, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="77844-133">Protobuf 2.5.0 [est requise](https://github.com/yahoo/CaffeOnSpark/issues/87), mais cette version n’est pas disponible en tant que package Ubuntu 16, donc nous devons toocompile à partir de code source de hello.</span><span class="sxs-lookup"><span data-stu-id="77844-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need toocompile it from hello source code.</span></span> <span data-ttu-id="77844-134">Il existe également quelques ressources sur Internet de hello sur la façon de toocompile, tels que [cela](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="77844-134">There are also a few resources on hello Internet on how toocompile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="77844-135">toosimply prise en main, vous pouvez exécuter cette action de script par rapport à votre travail de hello tooall cluster les nœuds de nœuds et head (pour HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="77844-135">toosimply get started, you can just run this script action against your cluster tooall hello worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="77844-136">Vous pouvez exécuter des actions de script hello pour un cluster en cours d’exécution, ou vous pouvez également exécuter des actions de script hello pendant le temps de configurer des clusters hello.</span><span class="sxs-lookup"><span data-stu-id="77844-136">You can either run hello script actions for a running cluster, or you can also run hello script actions during hello cluster provision time.</span></span> <span data-ttu-id="77844-137">Pour plus d’informations sur les actions de script hello, consultez la documentation de hello [ici](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="77844-137">For more details on hello script actions, please see hello documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Actions de script tooInstall dépendances](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a><span data-ttu-id="77844-139">Étape 2 : Générez Caffe sur Spark sur HDInsight sur le nœud principal de hello</span><span class="sxs-lookup"><span data-stu-id="77844-139">Step 2: Build Caffe on Spark for HDInsight on hello head node</span></span>

<span data-ttu-id="77844-140">deuxième étape de Hello est toobuild Caffe sur le nœud principal de hello et distribuez ensuite hello compilé bibliothèques tooall hello de nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="77844-140">hello second step is toobuild Caffe on hello headnode, and then distribute hello compiled libraries tooall hello worker nodes.</span></span> <span data-ttu-id="77844-141">Dans cette étape, vous devez trop[ssh dans votre nœud principal](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), puis suivez simplement hello [CaffeOnSpark les processus de génération](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), et Voici le script hello vous pouvez utiliser toobuild CaffeOnSpark avec quelques étapes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="77844-141">In this step, you will need too[ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow hello [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is hello script you can use toobuild CaffeOnSpark with a few additional steps.</span></span> 

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

<span data-ttu-id="77844-142">Vous devrez peut-être toodo plusieurs indique de quelle documentation hello de CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="77844-142">You may need toodo more than what hello documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="77844-143">modifications de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="77844-143">hello changes are:</span></span>
- <span data-ttu-id="77844-144">TooCPU uniquement de modifier et utiliser libatlas à cet usage particulier.</span><span class="sxs-lookup"><span data-stu-id="77844-144">Change tooCPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="77844-145">Hello datasets toohello stockage d’objets BLOB, qui est un emplacement partagé qui est accessible tooall de nœuds de travail pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="77844-145">Put hello datasets toohello BLOB storage, which is a shared location that is accessible tooall worker nodes for later use.</span></span>
- <span data-ttu-id="77844-146">Put hello compilé stockage de tooBLOB bibliothèques Caffe et ultérieurement, vous allez copier ces nœuds de hello tooall bibliothèques à l’aide de la durée de compilation supplémentaires tooavoid script actions.</span><span class="sxs-lookup"><span data-stu-id="77844-146">Put hello compiled Caffe libraries tooBLOB storage, and later you will copy those libraries tooall hello nodes using script actions tooavoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="77844-147">Résolution des problèmes : An Ant BuildException has occured: exec returned: 2</span><span class="sxs-lookup"><span data-stu-id="77844-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="77844-148">Lors de la première tentative toobuild CaffeOnSpark, parfois, il indiquera</span><span class="sxs-lookup"><span data-stu-id="77844-148">When first trying toobuild CaffeOnSpark, sometimes it will say</span></span>

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="77844-149">Référentiel de code hello simplement nettoyer par « rendre nettoyer », puis exécuter « rendre build » corrige ce problème, tant que vous disposez les dépendances appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="77844-149">Simply clean hello code repository by "make clean" and then run "make build" will solve this issue, as long as you have hello correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="77844-150">Résolution des problèmes : Expiration du délai de connexion du référentiel Maven</span><span class="sxs-lookup"><span data-stu-id="77844-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="77844-151">Parfois maven me donne erreur de délai d’expiration de connexion hello, toobelow similaire :</span><span class="sxs-lookup"><span data-stu-id="77844-151">Sometimes maven gives me hello connection time out error, similar toobelow:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="77844-152">Il sera OK attendez quelques minutes et recommencez simplement code hello de toorebuild, elle peut donc être Maven une certaine manière limites hello le trafic à partir d’une adresse IP donnée.</span><span class="sxs-lookup"><span data-stu-id="77844-152">It will be OK after waiting for a few minutes and then just try toorebuild hello code, so it might be Maven somehow limits hello traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="77844-153">Résolution des problèmes : Défaillance de test Caffe</span><span class="sxs-lookup"><span data-stu-id="77844-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="77844-154">Vous serez probablement voir un échec de test lors de la vérification finale de hello pour CaffeOnSpark, similaire à ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="77844-154">You probably will see a test failure when doing hello final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="77844-155">Cela est prabably lié avec encodage UTF-8, mais il ne devrait pas affecter l’utilisation de hello de Caffe</span><span class="sxs-lookup"><span data-stu-id="77844-155">This is prabably related with UTF-8 encoding, but should not impact hello usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a><span data-ttu-id="77844-156">Étape 3 : Distribuer les nœuds de travail hello hello requis bibliothèques tooall</span><span class="sxs-lookup"><span data-stu-id="77844-156">Step 3: Distribute hello required libraries tooall hello worker nodes</span></span>

<span data-ttu-id="77844-157">étape suivante de Hello est bibliothèques de hello toodistribute (hello essentiellement des bibliothèques dans CaffeOnSpark/caffe-public/distribuer/lib/et CaffeOnSpark/caffe-DIS/distribuer/lib /) les nœuds de hello tooall.</span><span class="sxs-lookup"><span data-stu-id="77844-157">hello next step is toodistribute hello libraries (basically hello libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) tooall hello nodes.</span></span> <span data-ttu-id="77844-158">À l’étape 2, nous plaçons ces bibliothèques sur le stockage d’objets BLOB, et dans cette étape, nous allons utiliser toocopy des actions de script il tooall hello nœuds principal et les nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="77844-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions toocopy it tooall hello head nodes and worker nodes.</span></span>

<span data-ttu-id="77844-159">toodo, simple d’exécuter une action de script comme indiqué ci-dessous (vous devez cluster tooyour spécifique de toopoint toohello bon emplacement) :</span><span class="sxs-lookup"><span data-stu-id="77844-159">toodo this, simple run a script action as below (you need toopoint toohello right location specific tooyour cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="77844-160">Comme à l’étape 2, nous placer sur le stockage d’objets BLOB qui est accessible tooall hello nœuds de hello, dans cette étape nous simplement copier les nœuds de hello tooall.</span><span class="sxs-lookup"><span data-stu-id="77844-160">Because in step 2, we put it on hello BLOB storage which is accessible tooall hello nodes, in this step we just simply copy it tooall hello nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="77844-161">Étape 4 : Composition d’un modèle Caffe et exécution de ce dernier de manière distribuée.</span><span class="sxs-lookup"><span data-stu-id="77844-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="77844-162">Après avoir exécuté hello étapes ci-dessus, Caffe est déjà installé sur le nœud principal de hello, et nous sommes toogo bon.</span><span class="sxs-lookup"><span data-stu-id="77844-162">After running hello above steps, Caffe is alreay installed on hello headnode and we are good toogo.</span></span> <span data-ttu-id="77844-163">étape suivante de Hello est toowrite un modèle Caffe.</span><span class="sxs-lookup"><span data-stu-id="77844-163">hello next step is toowrite a Caffe model.</span></span> 

<span data-ttu-id="77844-164">Caffe est à l’aide de « architecture expressive », pour composer un modèle, vous simplement besoin toodefine un fichier de configuration et sans codage (dans la plupart des cas).</span><span class="sxs-lookup"><span data-stu-id="77844-164">Caffe is using an "expressive architecture", where for composing a model, you just need toodefine a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="77844-165">Jetons un œil sur cette configuration.</span><span class="sxs-lookup"><span data-stu-id="77844-165">So let's take a look there.</span></span> 

<span data-ttu-id="77844-166">modèle Hello que nous apprendre aujourd'hui est un exemple de modèle pour l’apprentissage de MNIST.</span><span class="sxs-lookup"><span data-stu-id="77844-166">hello model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="77844-167">base de données Hello MNIST de chiffres manuscrites a un jeu d’apprentissage des exemples de 60 000 et un jeu de test des exemples de 10 000.</span><span class="sxs-lookup"><span data-stu-id="77844-167">hello MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="77844-168">Il s’agit d’un sous-ensemble d’un jeu plus volumineux de MNIST.</span><span class="sxs-lookup"><span data-stu-id="77844-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="77844-169">les chiffres Hello ont été normalisées de taille et centré dans une image de taille fixe.</span><span class="sxs-lookup"><span data-stu-id="77844-169">hello digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="77844-170">CaffeOnSpark comporte des datasets de hello toodownload scripts et le convertir en un format correct de hello.</span><span class="sxs-lookup"><span data-stu-id="77844-170">CaffeOnSpark has some scripts toodownload hello dataset and convert it into hello right format.</span></span>

<span data-ttu-id="77844-171">CaffeOnSpark fournit quelques exemples de topologies de réseau associés à la formation MNIST.</span><span class="sxs-lookup"><span data-stu-id="77844-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="77844-172">Il possède une conception agréable de fractionnement de l’architecture en réseau hello (topologie hello du réseau de hello) et l’optimisation.</span><span class="sxs-lookup"><span data-stu-id="77844-172">It has a nice design of splitting hello network architecture (hello topology of hello network) and optimization.</span></span> <span data-ttu-id="77844-173">Dans ce cas, deux fichiers sont requis :</span><span class="sxs-lookup"><span data-stu-id="77844-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="77844-174">fichier de « Solveur » Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) est utilisé pour surveiller l’optimisation de hello et générer des mises à jour du paramètre.</span><span class="sxs-lookup"><span data-stu-id="77844-174">hello "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing hello optimization and generating parameter updates.</span></span> <span data-ttu-id="77844-175">Par exemple, il définit si l’UC ou au GPU qui sera utilisé, nouveautés momentum hello, le nombre d’itérations sera, etc.. Il définit également la typologie de réseau de neurones doit hello utilisation du programme (c'est-à-dire hello deuxième fichier que nous devons).</span><span class="sxs-lookup"><span data-stu-id="77844-175">For example, it defines whether CPU or GPU will be used, what's hello momentum, how many iterations will be, etc. It also defines which neuron network topology should hello program use (which is hello second file we need).</span></span> <span data-ttu-id="77844-176">Pour plus d’informations sur le solveur, reportez-vous trop[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="77844-176">For more information about Solver, please refer too[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="77844-177">Pour cet exemple, étant donné que nous utilisons UC plutôt que de GPU, nous devons modifier dernière ligne de hello pour :</span><span class="sxs-lookup"><span data-stu-id="77844-177">For this example, since we are using CPU rather than GPU, we should change hello last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configuration de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="77844-179">Au besoin, vous pouvez modifier d’autres lignes.</span><span class="sxs-lookup"><span data-stu-id="77844-179">You can change other lines as needed.</span></span>

<span data-ttu-id="77844-180">fichier de deuxième Hello (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) définit comment le réseau de neurones hello ressemble à et d’entrée approprié de hello et fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="77844-180">hello second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how hello neuron network looks like, and hello relevant input and output file.</span></span> <span data-ttu-id="77844-181">Nous devons également d’emplacement de données d’apprentissage de tooupdate hello fichier tooreflect hello.</span><span class="sxs-lookup"><span data-stu-id="77844-181">We also need tooupdate hello file tooreflect hello training data location.</span></span> <span data-ttu-id="77844-182">Modifier hello suivant partie dans lenet_memory_train_test.prototxt (vous devez cluster tooyour spécifique de toopoint toohello bon emplacement) :</span><span class="sxs-lookup"><span data-stu-id="77844-182">Change hello following part in lenet_memory_train_test.prototxt (you need toopoint toohello right location specific tooyour cluster):</span></span>

- <span data-ttu-id="77844-183">également modifier hello « file:/Users/mridul/bigml/demodl/mnist_train_lmdb » « wasb : / / / projets/machine_learning/image_dataset/mnist_train_lmdb »</span><span class="sxs-lookup"><span data-stu-id="77844-183">change hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" too"wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="77844-184">modifier trop de « file:/Users/mridul/bigml/demodl/mnist_test_lmdb/ » « wasb : / / / projets/machine_learning/image_dataset/mnist_test_lmdb »</span><span class="sxs-lookup"><span data-stu-id="77844-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" too"wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Configuration de Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="77844-186">Pour plus d’informations sur la façon dont toodefine hello réseau, vérifiez hello [documentation Caffe MNIST le jeu de données](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="77844-186">For more information on how toodefine hello network, please check hello [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="77844-187">Pour les besoins de hello de cette entrée de blog, nous utilisons simplement cet exemple MNIST simple.</span><span class="sxs-lookup"><span data-stu-id="77844-187">For hello purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="77844-188">Vous devez exécuter la commande hello ci-dessous à partir du nœud principal hello :</span><span class="sxs-lookup"><span data-stu-id="77844-188">You should run hello command below from hello head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="77844-189">En fait, il distribue hello requis (lenet_memory_solver.prototxt et lenet_memory_train_test.prototxt) tooeach fils de conteneur, puis définissez les fichiers hello chemin d’accès approprié de chaque tooLD_LIBRARY_PATH pilote/exécuteur Spark, qui est définie dans hello code extrait de code et les points de toohello emplacement précédent qui a les bibliothèques CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="77844-189">Basically it distributes hello required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) tooeach YARN container, and also set hello relevant PATH of each Spark driver/executor tooLD_LIBRARY_PATH, which is defined in hello previous code snippet and points toohello location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="77844-190">Surveillance et dépannage</span><span class="sxs-lookup"><span data-stu-id="77844-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="77844-191">Étant donné que nous utilisons le mode de cluster fils, auquel cas pilote de Spark hello sera conteneur arbitraire de tooan planifiée (et un nœud de travail arbitraire) ne doit s’afficher dans la sortie de console hello quelque chose comme :</span><span class="sxs-lookup"><span data-stu-id="77844-191">Since we are using YARN cluster mode, in which case hello Spark driver will be scheduled tooan arbitrary container (and an arbitrary worker node) you should only see in hello console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="77844-192">Si vous souhaitez tooknow que s’est-il passé, vous devez généralement journal tooget hello Spark conducteur, ce qui a plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="77844-192">If you want tooknow what happened, you usually need tooget hello Spark driver's log, which has more information.</span></span> <span data-ttu-id="77844-193">Dans ce cas, vous devez toogo toohello fils toofind hello pertinentes fils des journaux interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="77844-193">In this case, you need toogo toohello YARN UI toofind hello relevant YARN logs.</span></span> <span data-ttu-id="77844-194">Vous pouvez obtenir hello UI fils par cette URL :</span><span class="sxs-lookup"><span data-stu-id="77844-194">You can get hello YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Interface utilisateur Yarn](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="77844-196">Vous pouvez découvrir le nombre de ressources allouées pour cette application spécifique.</span><span class="sxs-lookup"><span data-stu-id="77844-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="77844-197">Vous pouvez cliquer sur lien de « Planificateur » hello, et vous ne verrez que pour cette application, sont 9 conteneurs en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="77844-197">You can click hello "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="77844-198">Nous demandons fils tooprovide les exécuteurs de 8, et un autre conteneur pour les processus de pilote.</span><span class="sxs-lookup"><span data-stu-id="77844-198">We ask YARN tooprovide 8 executors, and another container is for driver process.</span></span> 

![Planificateur YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="77844-200">Vous souhaiterez toocheck hello pilote ou les journaux de conteneur des cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="77844-200">You may want toocheck hello  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="77844-201">Pour les journaux du pilote, vous pouvez cliquez sur ID de l’application hello dans l’interface utilisateur des fils, puis cliquez sur le bouton « Logs » de hello.</span><span class="sxs-lookup"><span data-stu-id="77844-201">For driver logs, you can click hello application ID in YARN UI, then click hello "Logs" button.</span></span> <span data-ttu-id="77844-202">les journaux du pilote Hello sont écrites dans stderr.</span><span class="sxs-lookup"><span data-stu-id="77844-202">hello driver logs are written into stderr.</span></span>

![Interface utilisateur YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="77844-204">Par exemple, vous pouvez voir certains erreur hello ci-dessous à partir des journaux de pilote hello, indiquant que vous allouez les exécuteurs de trop nombreuses.</span><span class="sxs-lookup"><span data-stu-id="77844-204">For example, you might see some of hello error below from hello driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="77844-205">Parfois, problème de hello peut se produire dans les exécuteurs plutôt que des pilotes.</span><span class="sxs-lookup"><span data-stu-id="77844-205">Sometimes, hello issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="77844-206">Dans ce cas, vous devez toocheck hello conteneur journaux.</span><span class="sxs-lookup"><span data-stu-id="77844-206">In this case, you need toocheck hello container logs.</span></span> <span data-ttu-id="77844-207">Vous pouvez toujours obtenir les journaux du conteneur hello et obtenez conteneur ayant échoué de hello.</span><span class="sxs-lookup"><span data-stu-id="77844-207">You can always get hello container logs, and then get hello failed container.</span></span> <span data-ttu-id="77844-208">Par exemple, vous pouvez rencontrer cette défaillance lors de l’exécution de Caffe.</span><span class="sxs-lookup"><span data-stu-id="77844-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="77844-209">Dans ce cas, vous devez l’ID du conteneur tooget hello a échoué (hello au-dessus de cas, il s’agit container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="77844-209">In this case, you need tooget hello failed container ID (in hello above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="77844-210">Vous devez ensuite toorun</span><span class="sxs-lookup"><span data-stu-id="77844-210">Then you need toorun</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="77844-211">à partir du nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="77844-211">from hello headnode.</span></span> <span data-ttu-id="77844-212">L’examen de la défaillance du conteneur indique qu’elle a été provoquée par le mode GPU (là où vous devriez utiliser le mode UC) dans lenet_memory_solver.prototxt.</span><span class="sxs-lookup"><span data-stu-id="77844-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="77844-213">Obtention des résultats</span><span class="sxs-lookup"><span data-stu-id="77844-213">Getting results</span></span>

<span data-ttu-id="77844-214">Étant donné que nous sommes allouer les exécuteurs de 8, et la topologie de réseau hello est simple, cela ne vous prendra environ 30 minutes toorun hello de résultats.</span><span class="sxs-lookup"><span data-stu-id="77844-214">Since we are allocating 8 executors, and hello network topology is simple, it should only take around 30 minutes toorun hello result.</span></span> <span data-ttu-id="77844-215">À partir de la ligne de commande hello, vous pouvez voir que nous placer hello modèle toowasb:///mnist.model et placer hello résultats tooa dossier nommé wasb : / / / mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="77844-215">From hello command line, you can see that we put hello model toowasb:///mnist.model, and put hello results tooa folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="77844-216">Vous pouvez obtenir des résultats de hello en exécutant</span><span class="sxs-lookup"><span data-stu-id="77844-216">You can get hello results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="77844-217">et le résultat de hello ressemble à :</span><span class="sxs-lookup"><span data-stu-id="77844-217">and hello result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="77844-218">Hello SampleID représente l’ID de hello dans le jeu de données MNIST hello et étiquette de hello est numéro hello hello modèle identifie.</span><span class="sxs-lookup"><span data-stu-id="77844-218">hello SampleID represents hello ID in hello MNIST dataset, and hello label is hello number that hello model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="77844-219">Conclusion</span><span class="sxs-lookup"><span data-stu-id="77844-219">Conclusion</span></span>

<span data-ttu-id="77844-220">Dans cette documentation, vous avez tenté de tooinstall CaffeOnSpark avec l’exécution d’un exemple simple.</span><span class="sxs-lookup"><span data-stu-id="77844-220">In this documentation, you have tried tooinstall CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="77844-221">HDInsight est une plateforme de calcul distribué cloud géré complète et est hello meilleur endroit pour l’exécution d’apprentissage automatique et les charges de travail analytique avancée sur le jeu de données volumineux, et pour en savoir plus approfondie distribuée, vous pouvez utiliser Caffe sur learning approfondie de HDInsight Spark tooperform tâches.</span><span class="sxs-lookup"><span data-stu-id="77844-221">HDInsight is a full managed cloud distributed compute platform, and is hello best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark tooperform deep learning tasks.</span></span>


## <span data-ttu-id="77844-222"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="77844-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="77844-223">Vue d’ensemble : Apache Spark sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="77844-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="77844-224">Scénarios</span><span class="sxs-lookup"><span data-stu-id="77844-224">Scenarios</span></span>
* [<span data-ttu-id="77844-225">Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC</span><span class="sxs-lookup"><span data-stu-id="77844-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="77844-226">Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="77844-226">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="77844-227">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="77844-227">Manage resources</span></span>
* [<span data-ttu-id="77844-228">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="77844-228">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

