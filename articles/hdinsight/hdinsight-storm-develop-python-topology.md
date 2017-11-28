---
title: aaaApache Storm avec les composants sinon Python - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toocreate une topologie d’Apache Storm qui utilise les composants de Python."
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
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="6d7a5-104">Développer des topologies Storm Apache à l’aide de Python sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d7a5-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="6d7a5-105">Découvrez comment toocreate une topologie d’Apache Storm qui utilise les composants de Python.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="6d7a5-106">Apache Storm prend en charge plusieurs langues, de même que toocombine des composants à partir de plusieurs langues dans une topologie.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="6d7a5-107">Hello Flux framework (introduit avec Storm 0.10.0) vous permet de créer des solutions qui utilisent des composants de Python tooeasily.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d7a5-108">informations Hello dans ce document a été testées à l’aide de Storm sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="6d7a5-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6d7a5-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6d7a5-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="6d7a5-111">code Hello pour ce projet est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="6d7a5-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d7a5-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6d7a5-112">Prerequisites</span></span>

* <span data-ttu-id="6d7a5-113">Python 2.7 ou ultérieure</span><span class="sxs-lookup"><span data-stu-id="6d7a5-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="6d7a5-114">Java JDK 1.8 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="6d7a5-115">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-115">Maven 3</span></span>

* <span data-ttu-id="6d7a5-116">(Facultatif) Un environnement de développement Storm local.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="6d7a5-117">Un environnement Storm local est uniquement nécessaire si vous souhaitez que la topologie de hello toorun localement.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="6d7a5-118">Pour plus d’informations, consultez la page [Configurer un environnement de développement](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="6d7a5-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="6d7a5-119">Prise en charge multi-langage de Storm</span><span class="sxs-lookup"><span data-stu-id="6d7a5-119">Storm multi-language support</span></span>

<span data-ttu-id="6d7a5-120">Apache Storm a été conçue toowork des composants écrits à l’aide de n’importe quel langage de programmation.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="6d7a5-121">composants de Hello doivent comprendre comment toowork avec hello [définition Thrift Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="6d7a5-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="6d7a5-122">Pour Python, un module est fourni en tant que partie du projet Apache Storm hello qui vous permet d’interface tooeasily avec Storm.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="6d7a5-123">Ce module est disponible à l’adresse [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="6d7a5-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="6d7a5-124">Storm est un processus Java qui s’exécute sur hello Machine virtuelle Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="6d7a5-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="6d7a5-125">Les composants écrits dans d’autres langages sont exécutés en tant que sous-processus.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="6d7a5-126">Hello Storm communique avec ces sous-processus à l’aide de messages JSON envoyés via stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="6d7a5-127">Vous trouverez plus d’informations sur la communication entre les composants Bonjour [Multi-lang protocole](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="6d7a5-128">Python avec l’infrastructure de Flux hello</span><span class="sxs-lookup"><span data-stu-id="6d7a5-128">Python with hello Flux framework</span></span>

<span data-ttu-id="6d7a5-129">infrastructure de Flux Hello permet les topologies Storm toodefine séparément à partir des composants de hello.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="6d7a5-130">infrastructure de Flux Hello utilise la topologie de Storm YAML toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="6d7a5-131">Bonjour texte suivant est un exemple de tooreference un composant de Python dans le document YAML hello :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

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

<span data-ttu-id="6d7a5-132">Hello classe `FluxShellSpout` est utilisé toostart hello `sentencespout.py` script qui implémente les bec hello.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="6d7a5-133">Flux attend toobe de scripts Python hello Bonjour `/resources` répertoire à l’intérieur du fichier jar hello qui contient la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="6d7a5-134">Pour cet exemple stocke les scripts de Python hello Bonjour `/multilang/resources` active.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="6d7a5-135">Hello `pom.xml` inclut ce fichier à l’aide de hello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="6d7a5-136">Comme mentionné précédemment, il existe un `storm.py` fichier qui implémente la définition Thrift hello Storm.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="6d7a5-137">Hello Flux framework inclut `storm.py` automatiquement lorsque hello projet est généré, vous n’avez donc tooworry sur l’insertion.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="6d7a5-138">Générez le projet de hello</span><span class="sxs-lookup"><span data-stu-id="6d7a5-138">Build hello project</span></span>

<span data-ttu-id="6d7a5-139">À partir de la racine de hello du projet de hello, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="6d7a5-140">Cette commande crée un `target/WordCount-1.0-SNAPSHOT.jar` fichier qui contient les hello compilé de topologie.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="6d7a5-141">Exécuter la topologie de hello localement</span><span class="sxs-lookup"><span data-stu-id="6d7a5-141">Run hello topology locally</span></span>

<span data-ttu-id="6d7a5-142">topologie de hello toorun localement, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="6d7a5-143">Cette commande requiert un environnement de développement Storm local.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="6d7a5-144">Pour plus d’informations, consultez la page [Configurer un environnement de développement](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="6d7a5-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="6d7a5-145">Une fois hello topologie démarre, il émet similaire toohello informations toohello console locale après le texte :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="6d7a5-146">topologie de hello toostop, utilisez __Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="6d7a5-147">Exécuter la topologie de Storm hello sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d7a5-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="6d7a5-148">Suivant de hello utilisez commande toocopy hello `WordCount-1.0-SNAPSHOT.jar` tooyour Storm sur le cluster HDInsight de fichiers :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6d7a5-149">Remplacez `sshuser` avec l’utilisateur SSH hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="6d7a5-150">Remplacez `mycluster` avec le nom du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="6d7a5-151">Vous pouvez être invité à tooenter hello mot de passe utilisateur SSH hello.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="6d7a5-152">Pour plus d’informations sur SSH et SCP, consultez la page [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6d7a5-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="6d7a5-153">Une fois que le fichier de hello a été téléchargé, connexion cluster toohello à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="6d7a5-154">À partir de la session SSH hello, utilisez hello suivant de topologie de hello toostart de commande de cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="6d7a5-155">Vous pouvez utiliser la topologie de hello hello Storm UI tooview sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="6d7a5-156">Hello Storm UI se trouve dans https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="6d7a5-157">Remplacez `mycluster` par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="6d7a5-158">Une fois démarrée, la topologie Storm s’exécute jusqu’à ce qu’elle soit arrêtée.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="6d7a5-159">topologie de hello toostop, utilisez une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="6d7a5-160">Hello `storm kill TOPOLOGYNAME` commande à partir de la ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="6d7a5-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="6d7a5-161">Hello **Kill** bouton Bonjour Storm UI.</span><span class="sxs-lookup"><span data-stu-id="6d7a5-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6d7a5-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d7a5-162">Next steps</span></span>

<span data-ttu-id="6d7a5-163">Consultez hello suivant des documents pour les autres façons de toouse Python avec HDInsight :</span><span class="sxs-lookup"><span data-stu-id="6d7a5-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="6d7a5-164">Comment toouse Python pour les tâches MapReduce de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="6d7a5-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="6d7a5-165">Comment toouse Python utilisateur définie par les fonctions (UDF) dans Pig et Hive</span><span class="sxs-lookup"><span data-stu-id="6d7a5-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
