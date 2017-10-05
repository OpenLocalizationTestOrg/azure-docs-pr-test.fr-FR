---
title: Activer des dumps de tas pour les services Hadoop sur HDInsight - Azure | Microsoft Docs
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
ms.openlocfilehash: 59942e989d622c2486edf181d76e13344c71e6f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="ecbaa-103">Activer les dumps de tas pour les services Hadoop sur HDInsight sur Linux</span><span class="sxs-lookup"><span data-stu-id="ecbaa-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="ecbaa-104">Les dumps de tas contiennent un instantané de la mémoire de l’application, y compris des valeurs des variables au moment de la création du dump.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="ecbaa-105">Ils sont donc utiles pour diagnostiquer les problèmes qui se produisent au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecbaa-106">Les étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight sur Linux.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-106">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="ecbaa-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ecbaa-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ecbaa-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ecbaa-109"><a name="whichServices"></a>Services</span><span class="sxs-lookup"><span data-stu-id="ecbaa-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="ecbaa-110">Vous pouvez activer des dumps de tas pour les services suivants :</span><span class="sxs-lookup"><span data-stu-id="ecbaa-110">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="ecbaa-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="ecbaa-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="ecbaa-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="ecbaa-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="ecbaa-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="ecbaa-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="ecbaa-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="ecbaa-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="ecbaa-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="ecbaa-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="ecbaa-116">Vous pouvez également activer les dumps de tas du mappage et réduire les processus exécutés par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="ecbaa-117"><a name="configuration"></a>Présentation de la configuration du dump du tas</span><span class="sxs-lookup"><span data-stu-id="ecbaa-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="ecbaa-118">Les dumps de tas sont activés par la transmission d’options (parfois appelées options ou paramètres) à la machine virtuelle Java au démarrage d’un service.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span></span> <span data-ttu-id="ecbaa-119">Pour la plupart des services Hadoop, vous pouvez modifier le script shell utilisé pour démarrer le service afin d’activer ces options.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span></span>

<span data-ttu-id="ecbaa-120">Dans chaque script, il existe une exportation pour **\*\_OPTS**, qui contient les options transmises à la machine virtuelle Java.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span></span> <span data-ttu-id="ecbaa-121">Par exemple, dans le script **hadoop-env.sh**, la ligne qui commence par `export HADOOP_NAMENODE_OPTS=` contient les options du service NameNode.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span></span>

<span data-ttu-id="ecbaa-122">Les processus de mappage et de réduction sont légèrement différents, car ces opérations sont des processus enfant du service MapReduce.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span></span> <span data-ttu-id="ecbaa-123">Chaque processus de mappage ou de réduction s’exécute dans un conteneur enfant et deux entrées contiennent les options JVM.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span></span> <span data-ttu-id="ecbaa-124">Ils sont contenus dans **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="ecbaa-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="ecbaa-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="ecbaa-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="ecbaa-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="ecbaa-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="ecbaa-127">Nous recommandons d’utiliser Ambari pour modifier les scripts et les paramètres de mapred-site.xml, car Ambari gère la réplication des modifications sur les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span></span> <span data-ttu-id="ecbaa-128">Consultez la section [Utilisation d’Ambari](#using-ambari) pour connaître les étapes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-128">See the [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="ecbaa-129">Activer les dumps de tas</span><span class="sxs-lookup"><span data-stu-id="ecbaa-129">Enable heap dumps</span></span>

<span data-ttu-id="ecbaa-130">L’option suivante active les dumps de tas quand OutOfMemoryError se produit :</span><span class="sxs-lookup"><span data-stu-id="ecbaa-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="ecbaa-131">Le **+** indique que cette option est activée.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-131">The **+** indicates that this option is enabled.</span></span> <span data-ttu-id="ecbaa-132">La valeur par défaut est désactivée.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-132">The default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="ecbaa-133">Les dumps de tas ne sont pas activés pour les services Hadoop sur HDInsight par défaut, car les fichiers dump peuvent être volumineux.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span></span> <span data-ttu-id="ecbaa-134">Si vous les activez pour la résolution des problèmes, pensez à les désactiver après avoir reproduit le problème et regroupé les fichiers de vidage.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="ecbaa-135">Emplacement du dump</span><span class="sxs-lookup"><span data-stu-id="ecbaa-135">Dump location</span></span>

<span data-ttu-id="ecbaa-136">L’emplacement par défaut pour le fichier dump est le répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-136">The default location for the dump file is the current working directory.</span></span> <span data-ttu-id="ecbaa-137">Vous pouvez contrôler l’endroit de stockage du fichier à l’aide de l’option suivante :</span><span class="sxs-lookup"><span data-stu-id="ecbaa-137">You can control where the file is stored using the following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="ecbaa-138">Par exemple, l’utilisation de `-XX:HeapDumpPath=/tmp` entraîne le stockage des dumps dans le répertoire /tmp.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="ecbaa-139">Scripts</span><span class="sxs-lookup"><span data-stu-id="ecbaa-139">Scripts</span></span>

<span data-ttu-id="ecbaa-140">Vous pouvez également déclencher un script quand **OutOfMemoryError** se produit.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="ecbaa-141">Par exemple, vous pouvez déclencher une notification pour signaler que l’erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-141">For example, triggering a notification so you know that the error has occurred.</span></span> <span data-ttu-id="ecbaa-142">Utilisez l’option suivante pour déclencher un script quand __OutOfMemoryError__ survient :</span><span class="sxs-lookup"><span data-stu-id="ecbaa-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="ecbaa-143">Hadoop étant un système distribué, tout script utilisé doit être placé sur tous les nœuds du cluster sur lequel le service s’exécute.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span></span>
> 
> <span data-ttu-id="ecbaa-144">Le script doit également être dans un emplacement accessible par le compte sur lequel s’exécute le service et doit fournir des autorisations d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="ecbaa-145">Par exemple, vous souhaitez stocker les scripts dans `/usr/local/bin` et utiliser `chmod go+rx /usr/local/bin/filename.sh` pour accorder les autorisations de lecture et d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="ecbaa-146">Utilisation d’Ambari</span><span class="sxs-lookup"><span data-stu-id="ecbaa-146">Using Ambari</span></span>

<span data-ttu-id="ecbaa-147">Pour modifier la configuration d’un service, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ecbaa-147">To modify the configuration for a service, use the following steps:</span></span>

1. <span data-ttu-id="ecbaa-148">Ouvrez l’interface utilisateur web Ambari de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-148">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="ecbaa-149">L’URL est https://NOMDEVOTRECLUSTER.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="ecbaa-150">Quand vous y êtes invité, authentifiez-vous auprès du site en utilisant le nom du compte HTTP (par défaut : admin) et le mot de passe de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ecbaa-151">Vous pouvez être invité une deuxième fois par Ambari à entrer le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-151">You may be prompted a second time by Ambari for the user name and password.</span></span> <span data-ttu-id="ecbaa-152">Dans ce cas, saisissez simplement les mêmes nom de compte et mot de passe</span><span class="sxs-lookup"><span data-stu-id="ecbaa-152">If so, enter the same account name and password</span></span>

2. <span data-ttu-id="ecbaa-153">Dans la liste de gauche, sélectionnez la zone de service que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-153">Using the list of on the left, select the service area you want to modify.</span></span> <span data-ttu-id="ecbaa-154">Par exemple, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-154">For example, **HDFS**.</span></span> <span data-ttu-id="ecbaa-155">Dans la zone centrale, sélectionnez l’onglet **Configurations** .</span><span class="sxs-lookup"><span data-stu-id="ecbaa-155">In the center area, select the **Configs** tab.</span></span>

    ![Image du site web Ambari avec l’onglet des configurations HDFS sélectionné](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="ecbaa-157">À l’aide de l’entrée **Filtre...**, entrez **opts**.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-157">Using the **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="ecbaa-158">Seuls les éléments contenant ce texte s’affichent.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-158">Only items containing this text are displayed.</span></span>

    ![Liste de filtrage](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="ecbaa-160">Recherchez l’entrée **\*\_OPTS** du service pour lequel vous souhaitez activer les dumps de tas et ajoutez les options que vous souhaitez activer.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span></span> <span data-ttu-id="ecbaa-161">Dans l’image suivante, j’ai ajouté `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` à l’entrée **HADOOP\_NAMENODE\_OPTS** :</span><span class="sxs-lookup"><span data-stu-id="ecbaa-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS with -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="ecbaa-163">Quand vous activez les dumps de tas du processus enfant de mappage ou de réduction, cherchez les champs intitulés **mapreduce.admin.map.child.java.opts** et **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="ecbaa-164">Utilisez le bouton **Enregistrer** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-164">Use the **Save** button to save the changes.</span></span> <span data-ttu-id="ecbaa-165">Vous pouvez entrer une courte note décrivant les modifications.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-165">You can enter a short note describing the changes.</span></span>

5. <span data-ttu-id="ecbaa-166">Une fois que ces dernières ont été appliquées, l’icône **Redémarrage requis** s’affiche en regard d’un ou de plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span></span>

    ![icône de redémarrage requis et bouton redémarrer](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="ecbaa-168">Sélectionnez chaque service nécessitant un redémarrage et utilisez le bouton **Actions de service** pour **Activer le mode de maintenance**.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span></span> <span data-ttu-id="ecbaa-169">Le mode de maintenance bloque la génération d’alertes au redémarrage de ce service.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span></span>

    ![menu Activer le mode de maintenance](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="ecbaa-171">Une fois le mode de maintenance activé, utilisez le bouton **Redémarrer** pour que le service puisse **redémarrer tous les éléments affectés**</span><span class="sxs-lookup"><span data-stu-id="ecbaa-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span></span>

    ![entrée Redémarrer tous les éléments affectés](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="ecbaa-173">les entrées du bouton **Redémarrer** peuvent être différentes pour d’autres services.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-173">the entries for the **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="ecbaa-174">Une fois que les services ont été redémarrés, utilisez le bouton **Actions de service** pour **Désactiver le mode de maintenance**.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="ecbaa-175">Ambari reprend la surveillance des alertes du service.</span><span class="sxs-lookup"><span data-stu-id="ecbaa-175">This Ambari to resume monitoring for alerts for the service.</span></span>

