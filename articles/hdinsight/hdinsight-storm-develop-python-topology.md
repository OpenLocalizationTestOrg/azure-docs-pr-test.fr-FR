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
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>Développer des topologies Storm Apache à l’aide de Python sur HDInsight

Découvrez comment toocreate une topologie d’Apache Storm qui utilise les composants de Python. Apache Storm prend en charge plusieurs langues, de même que toocombine des composants à partir de plusieurs langues dans une topologie. Hello Flux framework (introduit avec Storm 0.10.0) vous permet de créer des solutions qui utilisent des composants de Python tooeasily.

> [!IMPORTANT]
> informations Hello dans ce document a été testées à l’aide de Storm sur HDInsight 3.6. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

code Hello pour ce projet est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).

## <a name="prerequisites"></a>Composants requis

* Python 2.7 ou ultérieure

* Java JDK 1.8 ou version ultérieure.

* Maven 3.

* (Facultatif) Un environnement de développement Storm local. Un environnement Storm local est uniquement nécessaire si vous souhaitez que la topologie de hello toorun localement. Pour plus d’informations, consultez la page [Configurer un environnement de développement](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).

## <a name="storm-multi-language-support"></a>Prise en charge multi-langage de Storm

Apache Storm a été conçue toowork des composants écrits à l’aide de n’importe quel langage de programmation. composants de Hello doivent comprendre comment toowork avec hello [définition Thrift Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift). Pour Python, un module est fourni en tant que partie du projet Apache Storm hello qui vous permet d’interface tooeasily avec Storm. Ce module est disponible à l’adresse [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).

Storm est un processus Java qui s’exécute sur hello Machine virtuelle Java (JVM). Les composants écrits dans d’autres langages sont exécutés en tant que sous-processus. Hello Storm communique avec ces sous-processus à l’aide de messages JSON envoyés via stdin/stdout. Vous trouverez plus d’informations sur la communication entre les composants Bonjour [Multi-lang protocole](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.

## <a name="python-with-hello-flux-framework"></a>Python avec l’infrastructure de Flux hello

infrastructure de Flux Hello permet les topologies Storm toodefine séparément à partir des composants de hello. infrastructure de Flux Hello utilise la topologie de Storm YAML toodefine hello. Bonjour texte suivant est un exemple de tooreference un composant de Python dans le document YAML hello :

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

Hello classe `FluxShellSpout` est utilisé toostart hello `sentencespout.py` script qui implémente les bec hello.

Flux attend toobe de scripts Python hello Bonjour `/resources` répertoire à l’intérieur du fichier jar hello qui contient la topologie de hello. Pour cet exemple stocke les scripts de Python hello Bonjour `/multilang/resources` active. Hello `pom.xml` inclut ce fichier à l’aide de hello XML suivant :

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

Comme mentionné précédemment, il existe un `storm.py` fichier qui implémente la définition Thrift hello Storm. Hello Flux framework inclut `storm.py` automatiquement lorsque hello projet est généré, vous n’avez donc tooworry sur l’insertion.

## <a name="build-hello-project"></a>Générez le projet de hello

À partir de la racine de hello du projet de hello, utilisez hello de commande suivante :

```bash
mvn clean compile package
```

Cette commande crée un `target/WordCount-1.0-SNAPSHOT.jar` fichier qui contient les hello compilé de topologie.

## <a name="run-hello-topology-locally"></a>Exécuter la topologie de hello localement

topologie de hello toorun localement, utilisez hello de commande suivante :

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> Cette commande requiert un environnement de développement Storm local. Pour plus d’informations, consultez la page [Configurer un environnement de développement](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).

Une fois hello topologie démarre, il émet similaire toohello informations toohello console locale après le texte :


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


topologie de hello toostop, utilisez __Ctrl + C__.

## <a name="run-hello-storm-topology-on-hdinsight"></a>Exécuter la topologie de Storm hello sur HDInsight

1. Suivant de hello utilisez commande toocopy hello `WordCount-1.0-SNAPSHOT.jar` tooyour Storm sur le cluster HDInsight de fichiers :

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    Remplacez `sshuser` avec l’utilisateur SSH hello pour votre cluster. Remplacez `mycluster` avec le nom du cluster hello. Vous pouvez être invité à tooenter hello mot de passe utilisateur SSH hello.

    Pour plus d’informations sur SSH et SCP, consultez la page [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Une fois que le fichier de hello a été téléchargé, connexion cluster toohello à l’aide de SSH :

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. À partir de la session SSH hello, utilisez hello suivant de topologie de hello toostart de commande de cluster de hello :

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. Vous pouvez utiliser la topologie de hello hello Storm UI tooview sur le cluster de hello. Hello Storm UI se trouve dans https://mycluster.azurehdinsight.net/stormui. Remplacez `mycluster` par le nom de votre cluster.

> [!NOTE]
> Une fois démarrée, la topologie Storm s’exécute jusqu’à ce qu’elle soit arrêtée. topologie de hello toostop, utilisez une des méthodes suivantes de hello :
>
> * Hello `storm kill TOPOLOGYNAME` commande à partir de la ligne de commande hello
> * Hello **Kill** bouton Bonjour Storm UI.


## <a name="next-steps"></a>Étapes suivantes

Consultez hello suivant des documents pour les autres façons de toouse Python avec HDInsight :

* [Comment toouse Python pour les tâches MapReduce de diffusion en continu](hdinsight-hadoop-streaming-python.md)
* [Comment toouse Python utilisateur définie par les fonctions (UDF) dans Pig et Hive](hdinsight-python.md)
