---
title: Apache Storm avec composants Python - Azure HDInsight | Documents Microsoft
description: "Découvrez comment créer une topologie Apache Storm qui utilise des composants Python."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 305c4060ad81458b254e66a4bad6dfd7bf69b28d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="c2631-104">Développer des topologies Storm Apache à l’aide de Python sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2631-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="c2631-105">Découvrez comment créer une topologie Apache Storm qui utilise des composants Python.</span><span class="sxs-lookup"><span data-stu-id="c2631-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="c2631-106">Apache Storm prend en charge plusieurs langages et vous permet de combiner des composants de plusieurs langages dans une même topologie.</span><span class="sxs-lookup"><span data-stu-id="c2631-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="c2631-107">L’infrastructure de Flux (introduite avec Storm 0.10.0) permet de créer facilement des solutions qui utilisent des composants Python.</span><span class="sxs-lookup"><span data-stu-id="c2631-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2631-108">Les informations contenues dans ce document ont été testées avec Storm sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="c2631-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="c2631-109">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="c2631-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c2631-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c2631-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c2631-111">Le code de ce projet est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="c2631-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2631-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c2631-112">Prerequisites</span></span>

* <span data-ttu-id="c2631-113">Python 2.7 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="c2631-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="c2631-114">Java JDK 1.8 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c2631-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="c2631-115">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="c2631-115">Maven 3</span></span>

* <span data-ttu-id="c2631-116">(Facultatif) Un environnement de développement Storm local.</span><span class="sxs-lookup"><span data-stu-id="c2631-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="c2631-117">Un environnement Storm local n’est nécessaire que si vous souhaitez exécuter la topologie localement.</span><span class="sxs-lookup"><span data-stu-id="c2631-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="c2631-118">Pour plus d’informations, consultez la page [Configurer un environnement de développement](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="c2631-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="c2631-119">Prise en charge multi-langage de Storm</span><span class="sxs-lookup"><span data-stu-id="c2631-119">Storm multi-language support</span></span>

<span data-ttu-id="c2631-120">Apache Storm est conçu pour fonctionner avec des composants écrits dans n’importe quel langage de programmation.</span><span class="sxs-lookup"><span data-stu-id="c2631-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="c2631-121">Les composants doivent comprendre comment travailler avec la [définition Thrift pour Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="c2631-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="c2631-122">Pour Python, un module est fourni dans le cadre du projet Apache Storm pour vous permettre de communiquer facilement avec Storm.</span><span class="sxs-lookup"><span data-stu-id="c2631-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="c2631-123">Ce module est disponible à l’adresse [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="c2631-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="c2631-124">Storm est un processus Java qui s’exécute sur une machine virtuelle Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="c2631-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="c2631-125">Les composants écrits dans d’autres langages sont exécutés en tant que sous-processus.</span><span class="sxs-lookup"><span data-stu-id="c2631-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="c2631-126">Storm communique avec ces sous-processus à l’aide de messages JSON envoyées par le biais de stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="c2631-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="c2631-127">Vous trouverez plus de détails sur la communication entre les composants dans la documentation relative au [Protocole multi-langage](https://storm.apache.org/documentation/Multilang-protocol.html).</span><span class="sxs-lookup"><span data-stu-id="c2631-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="c2631-128">Python avec l’infrastructure Flux</span><span class="sxs-lookup"><span data-stu-id="c2631-128">Python with the Flux framework</span></span>

<span data-ttu-id="c2631-129">L’infrastructure Flux permet de définir des topologies Storm séparément des composants.</span><span class="sxs-lookup"><span data-stu-id="c2631-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="c2631-130">L’infrastructure de Flux utilise YAML pour définir la topologie Storm.</span><span class="sxs-lookup"><span data-stu-id="c2631-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="c2631-131">Le texte suivant est un exemple de manière de référencer un composant Python dans le document YAML :</span><span class="sxs-lookup"><span data-stu-id="c2631-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

<span data-ttu-id="c2631-132">La classe `FluxShellSpout` est utilisée pour démarrer le script `sentencespout.py` qui implémente le Spout.</span><span class="sxs-lookup"><span data-stu-id="c2631-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="c2631-133">Flux s’attend à ce que les scripts Python se trouvent dans le répertoire `/resources` du fichier jar contenant la topologie.</span><span class="sxs-lookup"><span data-stu-id="c2631-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="c2631-134">Cet exemple stocke donc les scripts Python dans le répertoire `/multilang/resources`.</span><span class="sxs-lookup"><span data-stu-id="c2631-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="c2631-135">`pom.xml` inclut ce fichier selon le code XML suivant :</span><span class="sxs-lookup"><span data-stu-id="c2631-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="c2631-136">Comme mentionné précédemment, il existe un fichier `storm.py` qui implémente la définition Thrift pour Storm.</span><span class="sxs-lookup"><span data-stu-id="c2631-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="c2631-137">L’infrastructure Flux inclut `storm.py` automatiquement lors de la génération du projet : vous n’avez donc pas besoin de vous en occuper.</span><span class="sxs-lookup"><span data-stu-id="c2631-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="c2631-138">Créer le projet</span><span class="sxs-lookup"><span data-stu-id="c2631-138">Build the project</span></span>

<span data-ttu-id="c2631-139">À la racine du projet, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c2631-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="c2631-140">Cette commande crée un fichier `target/WordCount-1.0-SNAPSHOT.jar` qui contient la topologie compilée.</span><span class="sxs-lookup"><span data-stu-id="c2631-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="c2631-141">Exécuter la topologie localement</span><span class="sxs-lookup"><span data-stu-id="c2631-141">Run the topology locally</span></span>

<span data-ttu-id="c2631-142">Pour exécuter la topologie localement, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c2631-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="c2631-143">Cette commande requiert un environnement de développement Storm local.</span><span class="sxs-lookup"><span data-stu-id="c2631-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="c2631-144">Pour plus d’informations, consultez la page [Configurer un environnement de développement](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="c2631-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="c2631-145">Une fois démarrée, la topologie émet des informations de ce type sur la console locale :</span><span class="sxs-lookup"><span data-stu-id="c2631-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="c2631-146">Pour arrêter la topologie, appuyez sur __Ctrl+C__.</span><span class="sxs-lookup"><span data-stu-id="c2631-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="c2631-147">Exécuter la topologie Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2631-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="c2631-148">Utilisez la commande suivante pour copier le fichier `WordCount-1.0-SNAPSHOT.jar` sur votre Storm dans votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c2631-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="c2631-149">Remplacez `sshuser` par l’utilisateur SSH de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c2631-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="c2631-150">Remplacez `mycluster` par le nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="c2631-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="c2631-151">Vous serez peut-être invité à entrer le mot de passe de l’utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="c2631-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="c2631-152">Pour plus d’informations sur SSH et SCP, consultez la page [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c2631-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c2631-153">Une fois le fichier chargé, connectez-vous au cluster via SSH :</span><span class="sxs-lookup"><span data-stu-id="c2631-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="c2631-154">Dans la session SSH, utilisez la commande suivante pour démarrer la topologie sur le cluster :</span><span class="sxs-lookup"><span data-stu-id="c2631-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="c2631-155">Vous pouvez utiliser l’interface utilisateur Storm pour afficher la topologie sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="c2631-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="c2631-156">L’interface utilisateur Storm se trouve à l’adresse https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="c2631-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="c2631-157">Remplacez `mycluster` par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c2631-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="c2631-158">Une fois démarrée, la topologie Storm s’exécute jusqu’à ce qu’elle soit arrêtée.</span><span class="sxs-lookup"><span data-stu-id="c2631-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="c2631-159">Pour arrêter la topologie, utilisez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c2631-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="c2631-160">la commande `storm kill TOPOLOGYNAME` à partir de la ligne de commande ;</span><span class="sxs-lookup"><span data-stu-id="c2631-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="c2631-161">le bouton **Tuer** dans l’interface utilisateur Storm.</span><span class="sxs-lookup"><span data-stu-id="c2631-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c2631-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c2631-162">Next steps</span></span>

<span data-ttu-id="c2631-163">Consultez les documents suivants pour découvrir d’autres façons de travailler avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="c2631-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="c2631-164">Développement de programmes de diffusion en continu Python pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2631-164">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="c2631-165">Utilisation de Python avec Hive et Pig dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2631-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
