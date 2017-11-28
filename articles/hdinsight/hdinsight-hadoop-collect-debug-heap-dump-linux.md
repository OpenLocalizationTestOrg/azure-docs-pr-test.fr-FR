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
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="dbefc-103">Activer les dumps de tas pour les services Hadoop sur HDInsight sur Linux</span><span class="sxs-lookup"><span data-stu-id="dbefc-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="dbefc-104">Dumps de tas contiennent un instantané de la mémoire de l’application hello, y compris les valeurs hello des variables au moment de hello création du dump hello.</span><span class="sxs-lookup"><span data-stu-id="dbefc-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="dbefc-105">Ils sont donc utiles pour diagnostiquer les problèmes qui se produisent au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="dbefc-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbefc-106">Hello étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight qui utilisent Linux.</span><span class="sxs-lookup"><span data-stu-id="dbefc-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="dbefc-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="dbefc-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dbefc-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="dbefc-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="dbefc-109"><a name="whichServices"></a>Services</span><span class="sxs-lookup"><span data-stu-id="dbefc-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="dbefc-110">Vous pouvez activer les vidages de segment de mémoire pour hello suivant services :</span><span class="sxs-lookup"><span data-stu-id="dbefc-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="dbefc-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="dbefc-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="dbefc-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="dbefc-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="dbefc-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="dbefc-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="dbefc-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="dbefc-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="dbefc-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="dbefc-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="dbefc-116">Vous pouvez également activer les vidages sur le segment de mémoire pour la carte de hello et réduire les processus qui s’exécutaient par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dbefc-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="dbefc-117"><a name="configuration"></a>Présentation de la configuration du dump du tas</span><span class="sxs-lookup"><span data-stu-id="dbefc-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="dbefc-118">Les vidages de segment de mémoire sont activés en passant des options (parfois appelé opts, ou des paramètres) toohello JVM lorsqu’un service est démarré.</span><span class="sxs-lookup"><span data-stu-id="dbefc-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="dbefc-119">Pour la plupart des services Hadoop, vous pouvez modifier hello shell script utilisé toostart hello service toopass ces options.</span><span class="sxs-lookup"><span data-stu-id="dbefc-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="dbefc-120">Dans chaque script, il existe une exportation pour  **\* \_se**, qui contient les options hello passé toohello JVM.</span><span class="sxs-lookup"><span data-stu-id="dbefc-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="dbefc-121">Par exemple, dans hello **hadoop-env.sh** un script, ligne hello qui commence par `export HADOOP_NAMENODE_OPTS=` contient les options de hello pour hello NameNode service.</span><span class="sxs-lookup"><span data-stu-id="dbefc-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="dbefc-122">Mapper et réduire les processus sont légèrement différents, car ces opérations sont un processus enfant de hello MapReduce service.</span><span class="sxs-lookup"><span data-stu-id="dbefc-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="dbefc-123">Chaque mapper ou de réduire les processus s’exécute dans un conteneur enfant, et il existe deux entrées qui contiennent des options de JVM hello.</span><span class="sxs-lookup"><span data-stu-id="dbefc-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="dbefc-124">Ils sont contenus dans **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="dbefc-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="dbefc-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="dbefc-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="dbefc-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="dbefc-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="dbefc-127">Il est recommandé à l’aide de Ambari toomodify les deux hello scripts mapred-site.XML les paramètres, comme Ambari gérer la réplication des modifications entre les nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dbefc-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="dbefc-128">Consultez hello [à l’aide de Ambari](#using-ambari) section pour connaître la procédure.</span><span class="sxs-lookup"><span data-stu-id="dbefc-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="dbefc-129">Activer les dumps de tas</span><span class="sxs-lookup"><span data-stu-id="dbefc-129">Enable heap dumps</span></span>

<span data-ttu-id="dbefc-130">Hello option suivante permet les vidages de segment de mémoire lorsqu’un OutOfMemoryError se produit :</span><span class="sxs-lookup"><span data-stu-id="dbefc-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="dbefc-131">Hello  **+**  indique que cette option est activée.</span><span class="sxs-lookup"><span data-stu-id="dbefc-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="dbefc-132">valeur par défaut de Hello est désactivé.</span><span class="sxs-lookup"><span data-stu-id="dbefc-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="dbefc-133">Vidages de segment de mémoire ne sont pas activés pour les services de Hadoop dans HDInsight par défaut, comme les fichiers de vidage hello peuvent être volumineux.</span><span class="sxs-lookup"><span data-stu-id="dbefc-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="dbefc-134">Si vous activez les pour la résolution des problèmes, n’oubliez pas toodisable les fois que vous avez reproduit hello problème et les fichiers de vidage hello collectées.</span><span class="sxs-lookup"><span data-stu-id="dbefc-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="dbefc-135">Emplacement du dump</span><span class="sxs-lookup"><span data-stu-id="dbefc-135">Dump location</span></span>

<span data-ttu-id="dbefc-136">emplacement par défaut de Hello pour le fichier de vidage hello est répertoire de travail actuel hello.</span><span class="sxs-lookup"><span data-stu-id="dbefc-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="dbefc-137">Vous pouvez contrôler où hello fichier est stocké à l’aide de hello option suivante :</span><span class="sxs-lookup"><span data-stu-id="dbefc-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="dbefc-138">Par exemple, à l’aide de `-XX:HeapDumpPath=/tmp` provoque hello vidages toobe est stocké dans le répertoire /tmp de hello.</span><span class="sxs-lookup"><span data-stu-id="dbefc-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="dbefc-139">Scripts</span><span class="sxs-lookup"><span data-stu-id="dbefc-139">Scripts</span></span>

<span data-ttu-id="dbefc-140">Vous pouvez également déclencher un script quand **OutOfMemoryError** se produit.</span><span class="sxs-lookup"><span data-stu-id="dbefc-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="dbefc-141">Par exemple, déclencher une notification afin que vous sachiez qu’erreur hello s’est produite.</span><span class="sxs-lookup"><span data-stu-id="dbefc-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="dbefc-142">Suivant de hello utilisez option tootrigger un script sur un __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="dbefc-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="dbefc-143">Hadoop étant un système distribué, n’importe quel script utilisé doit être placé sur tous les nœuds de cluster de hello hello service s’exécute sur.</span><span class="sxs-lookup"><span data-stu-id="dbefc-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="dbefc-144">script de Hello doit également être dans un emplacement qui est accessible par hello compte hello le service s’exécute en tant qu’et doit fournir des autorisations d’exécution.</span><span class="sxs-lookup"><span data-stu-id="dbefc-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="dbefc-145">Par exemple, vous souhaiterez peut-être les scripts toostore dans `/usr/local/bin` et utiliser `chmod go+rx /usr/local/bin/filename.sh` toogrant autorisations read et execute.</span><span class="sxs-lookup"><span data-stu-id="dbefc-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="dbefc-146">Utilisation d’Ambari</span><span class="sxs-lookup"><span data-stu-id="dbefc-146">Using Ambari</span></span>

<span data-ttu-id="dbefc-147">configuration de hello toomodify pour un service, hello utilisation comme suit :</span><span class="sxs-lookup"><span data-stu-id="dbefc-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="dbefc-148">Ouvrez hello Ambari web l’interface utilisateur pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="dbefc-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="dbefc-149">URL de Hello est https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="dbefc-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="dbefc-150">Lorsque vous y êtes invité, authentifier site toohello à l’aide du nom du compte hello HTTP (par défaut : administrateur) et le mot de passe pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="dbefc-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbefc-151">Vous pouvez être invité une deuxième fois par Ambari de mot de passe et le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="dbefc-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="dbefc-152">Dans ce cas, entrez hello du même nom de compte et mot de passe</span><span class="sxs-lookup"><span data-stu-id="dbefc-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="dbefc-153">À l’aide de la liste des hello sur hello gauche, sélectionnez hello service zone toomodify.</span><span class="sxs-lookup"><span data-stu-id="dbefc-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="dbefc-154">Par exemple, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="dbefc-154">For example, **HDFS**.</span></span> <span data-ttu-id="dbefc-155">Dans la zone du centre de hello, sélectionnez hello **configurations** onglet.</span><span class="sxs-lookup"><span data-stu-id="dbefc-155">In hello center area, select hello **Configs** tab.</span></span>

    ![Image du site web Ambari avec l’onglet des configurations HDFS sélectionné](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="dbefc-157">À l’aide de hello **filtre...**  entrée, entrez **opts**.</span><span class="sxs-lookup"><span data-stu-id="dbefc-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="dbefc-158">Seuls les éléments contenant ce texte s’affichent.</span><span class="sxs-lookup"><span data-stu-id="dbefc-158">Only items containing this text are displayed.</span></span>

    ![Liste de filtrage](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="dbefc-160">Recherche hello  **\* \_se** entrée pour service hello souhaité des dumps de tas tooenable pour et l’ajouter hello options que vous souhaitez tooenable.</span><span class="sxs-lookup"><span data-stu-id="dbefc-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="dbefc-161">Bonjour suivant l’image, j’ai ajouté `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_se** entrée :</span><span class="sxs-lookup"><span data-stu-id="dbefc-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS with -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="dbefc-163">Lors de l’activation des dumps de tas pour hello mappent ou réduisent les processus enfant, recherchez les champs de hello nommés **mapreduce.admin.map.child.java.opts** et **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="dbefc-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="dbefc-164">Hello d’utilisation **enregistrer** bouton les modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="dbefc-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="dbefc-165">Vous pouvez entrer une note décrivant les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="dbefc-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="dbefc-166">Une fois que les modifications de hello ont été appliquées, hello **redémarrage requis** icône s’affiche en regard d’un ou plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="dbefc-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![icône de redémarrage requis et bouton redémarrer](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="dbefc-168">Sélectionnez chaque service nécessitant un redémarrage et utilisez hello **Actions Service** bouton trop**activer sur le Mode Maintenance**.</span><span class="sxs-lookup"><span data-stu-id="dbefc-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="dbefc-169">Mode de maintenance empêche la génération à partir du service de hello lors du redémarrage des alertes.</span><span class="sxs-lookup"><span data-stu-id="dbefc-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![menu Activer le mode de maintenance](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="dbefc-171">Une fois que vous avez activé le mode de maintenance, utilisez hello **redémarrer** bouton pour le service de hello trop**redémarrer l’effectuées toutes les**</span><span class="sxs-lookup"><span data-stu-id="dbefc-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![entrée Redémarrer tous les éléments affectés](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="dbefc-173">Hello entrées pour hello **redémarrer** bouton peut être différent pour d’autres services.</span><span class="sxs-lookup"><span data-stu-id="dbefc-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="dbefc-174">Une fois le redémarrage des services de hello, utilisez hello **Actions Service** bouton trop**activer en Mode Maintenance**.</span><span class="sxs-lookup"><span data-stu-id="dbefc-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="dbefc-175">Cette tooresume Ambari d’analyse pour les alertes pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="dbefc-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

