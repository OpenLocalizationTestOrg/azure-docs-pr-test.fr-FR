---
title: "segment de mémoire aaaEnable vide des services Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Activez les services Hadoop à partir des clusters HDInsight sur Linux pour le débogage et l’analyse."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a>Activer les dumps de tas pour les services Hadoop sur HDInsight sur Linux

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Dumps de tas contiennent un instantané de la mémoire de l’application hello, y compris les valeurs hello des variables au moment de hello création du dump hello. Ils sont donc utiles pour diagnostiquer les problèmes qui se produisent au moment de l’exécution.

> [!IMPORTANT]
> Hello étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight qui utilisent Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whichServices"></a>Services

Vous pouvez activer les vidages de segment de mémoire pour hello suivant services :

* **hcatalog** - tempelton
* **hive** - hiveserver2, metastore, derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager, nodemanager, timelineserver
* **hdfs** - datanode, secondarynamenode, namenode

Vous pouvez également activer les vidages sur le segment de mémoire pour la carte de hello et réduire les processus qui s’exécutaient par HDInsight.

## <a name="configuration"></a>Présentation de la configuration du dump du tas

Les vidages de segment de mémoire sont activés en passant des options (parfois appelé opts, ou des paramètres) toohello JVM lorsqu’un service est démarré. Pour la plupart des services Hadoop, vous pouvez modifier hello shell script utilisé toostart hello service toopass ces options.

Dans chaque script, il existe une exportation pour  **\* \_se**, qui contient les options hello passé toohello JVM. Par exemple, dans hello **hadoop-env.sh** un script, ligne hello qui commence par `export HADOOP_NAMENODE_OPTS=` contient les options de hello pour hello NameNode service.

Mapper et réduire les processus sont légèrement différents, car ces opérations sont un processus enfant de hello MapReduce service. Chaque mapper ou de réduire les processus s’exécute dans un conteneur enfant, et il existe deux entrées qui contiennent des options de JVM hello. Ils sont contenus dans **mapred-site.xml**:

* **mapreduce.admin.map.child.java.opts**
* **mapreduce.admin.reduce.child.java.opts**

> [!NOTE]
> Il est recommandé à l’aide de Ambari toomodify les deux hello scripts mapred-site.XML les paramètres, comme Ambari gérer la réplication des modifications entre les nœuds de cluster de hello. Consultez hello [à l’aide de Ambari](#using-ambari) section pour connaître la procédure.

### <a name="enable-heap-dumps"></a>Activer les dumps de tas

Hello option suivante permet les vidages de segment de mémoire lorsqu’un OutOfMemoryError se produit :

    -XX:+HeapDumpOnOutOfMemoryError

Hello  **+**  indique que cette option est activée. valeur par défaut de Hello est désactivé.

> [!WARNING]
> Vidages de segment de mémoire ne sont pas activés pour les services de Hadoop dans HDInsight par défaut, comme les fichiers de vidage hello peuvent être volumineux. Si vous activez les pour la résolution des problèmes, n’oubliez pas toodisable les fois que vous avez reproduit hello problème et les fichiers de vidage hello collectées.

### <a name="dump-location"></a>Emplacement du dump

emplacement par défaut de Hello pour le fichier de vidage hello est répertoire de travail actuel hello. Vous pouvez contrôler où hello fichier est stocké à l’aide de hello option suivante :

    -XX:HeapDumpPath=/path

Par exemple, à l’aide de `-XX:HeapDumpPath=/tmp` provoque hello vidages toobe est stocké dans le répertoire /tmp de hello.

### <a name="scripts"></a>Scripts

Vous pouvez également déclencher un script quand **OutOfMemoryError** se produit. Par exemple, déclencher une notification afin que vous sachiez qu’erreur hello s’est produite. Suivant de hello utilisez option tootrigger un script sur un __OutOfMemoryError__:

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> Hadoop étant un système distribué, n’importe quel script utilisé doit être placé sur tous les nœuds de cluster de hello hello service s’exécute sur.
> 
> script de Hello doit également être dans un emplacement qui est accessible par hello compte hello le service s’exécute en tant qu’et doit fournir des autorisations d’exécution. Par exemple, vous souhaiterez peut-être les scripts toostore dans `/usr/local/bin` et utiliser `chmod go+rx /usr/local/bin/filename.sh` toogrant autorisations read et execute.

## <a name="using-ambari"></a>Utilisation d’Ambari

configuration de hello toomodify pour un service, hello utilisation comme suit :

1. Ouvrez hello Ambari web l’interface utilisateur pour votre cluster. URL de Hello est https://YOURCLUSTERNAME.azurehdinsight.net.

    Lorsque vous y êtes invité, authentifier site toohello à l’aide du nom du compte hello HTTP (par défaut : administrateur) et le mot de passe pour votre cluster.

   > [!NOTE]
   > Vous pouvez être invité une deuxième fois par Ambari de mot de passe et le nom d’utilisateur hello. Dans ce cas, entrez hello du même nom de compte et mot de passe

2. À l’aide de la liste des hello sur hello gauche, sélectionnez hello service zone toomodify. Par exemple, **HDFS**. Dans la zone du centre de hello, sélectionnez hello **configurations** onglet.

    ![Image du site web Ambari avec l’onglet des configurations HDFS sélectionné](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. À l’aide de hello **filtre...**  entrée, entrez **opts**. Seuls les éléments contenant ce texte s’affichent.

    ![Liste de filtrage](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. Recherche hello  **\* \_se** entrée pour service hello souhaité des dumps de tas tooenable pour et l’ajouter hello options que vous souhaitez tooenable. Bonjour suivant l’image, j’ai ajouté `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_se** entrée :

    ![HADOOP_NAMENODE_OPTS with -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > Lors de l’activation des dumps de tas pour hello mappent ou réduisent les processus enfant, recherchez les champs de hello nommés **mapreduce.admin.map.child.java.opts** et **mapreduce.admin.reduce.child.java.opts**.

    Hello d’utilisation **enregistrer** bouton les modifications de hello toosave. Vous pouvez entrer une note décrivant les modifications de hello.

5. Une fois que les modifications de hello ont été appliquées, hello **redémarrage requis** icône s’affiche en regard d’un ou plusieurs services.

    ![icône de redémarrage requis et bouton redémarrer](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. Sélectionnez chaque service nécessitant un redémarrage et utilisez hello **Actions Service** bouton trop**activer sur le Mode Maintenance**. Mode de maintenance empêche la génération à partir du service de hello lors du redémarrage des alertes.

    ![menu Activer le mode de maintenance](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. Une fois que vous avez activé le mode de maintenance, utilisez hello **redémarrer** bouton pour le service de hello trop**redémarrer l’effectuées toutes les**

    ![entrée Redémarrer tous les éléments affectés](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > Hello entrées pour hello **redémarrer** bouton peut être différent pour d’autres services.

8. Une fois le redémarrage des services de hello, utilisez hello **Actions Service** bouton trop**activer en Mode Maintenance**. Cette tooresume Ambari d’analyse pour les alertes pour le service de hello.

