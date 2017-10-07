---
title: aaaInstall et utiliser Giraph sur HDInsight (Hadoop) - Azure | Documents Microsoft
description: "Découvrez comment les clusters tooinstall Giraph sur HDInsight de basés sur Linux à l’aide des Actions de Script. Actions de script permettent de toocustomize hello cluster lors de la création, par la modification de la configuration de cluster ou l’installation des services et les utilitaires."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="aafec-104">Installer Giraph sur les clusters HDInsight Hadoop et utiliser des graphiques de Giraph tooprocess à grande échelle</span><span class="sxs-lookup"><span data-stu-id="aafec-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="aafec-105">Découvrez comment tooinstall Apache Giraph sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aafec-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="aafec-106">fonctionnalité d’action de script Hello de HDInsight vous permet de toocustomize votre cluster en exécutant un script de l’interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="aafec-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="aafec-107">Scripts peuvent être utilisés toocustomize clusters pendant et après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="aafec-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aafec-108">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="aafec-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="aafec-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="aafec-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aafec-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aafec-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="aafec-111"><a name="whatis"></a>Présentation de Giraph</span><span class="sxs-lookup"><span data-stu-id="aafec-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="aafec-112">[Apache Giraph](http://giraph.apache.org/) vous permet de graphique tooperform traitement à l’aide de Hadoop et peut être utilisé avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aafec-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="aafec-113">Les graphiques modélisent les relations entre les objets.</span><span class="sxs-lookup"><span data-stu-id="aafec-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="aafec-114">Par exemple, les connexions entre des routeurs d’un réseau étendu hello comme hello Internet ou les relations entre les utilisateurs pouvant accéder à des réseaux sociaux.</span><span class="sxs-lookup"><span data-stu-id="aafec-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="aafec-115">Le traitement du graphique vous permet de tooreason sur les relations hello entre les objets dans un graphique, telles que :</span><span class="sxs-lookup"><span data-stu-id="aafec-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="aafec-116">identifier les amis potentiels en fonction de vos relations actuelles ;</span><span class="sxs-lookup"><span data-stu-id="aafec-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="aafec-117">Identification hello la plus courte entre deux ordinateurs dans un réseau.</span><span class="sxs-lookup"><span data-stu-id="aafec-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="aafec-118">Calcul de rang dans la page hello des pages Web.</span><span class="sxs-lookup"><span data-stu-id="aafec-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="aafec-119">Les composants fournis avec le cluster HDInsight de hello sont entièrement gérés - Support technique de Microsoft vous aide à tooisolate et résoudre les problèmes connexes toothese composants.</span><span class="sxs-lookup"><span data-stu-id="aafec-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="aafec-120">Les composants personnalisés, tels que Giraph, réception efforcera toohelp vous toofurther hello de dépannage.</span><span class="sxs-lookup"><span data-stu-id="aafec-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="aafec-121">Support technique de Microsoft soit en mesure de tooresolving hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="aafec-122">Si ce n’est pas le cas, vous devez consulter les communautés open source. Elles regorgent de connaissances approfondies sur cette technologie.</span><span class="sxs-lookup"><span data-stu-id="aafec-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="aafec-123">Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="aafec-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="aafec-124">Le script hello effectue</span><span class="sxs-lookup"><span data-stu-id="aafec-124">What hello script does</span></span>

<span data-ttu-id="aafec-125">Ce script effectue hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="aafec-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="aafec-126">Installe Giraph trop`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="aafec-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="aafec-127">Hello de copies `giraph-examples.jar` stockage de fichier toodefault (WASB) pour votre cluster :`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="aafec-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="aafec-128"><a name="install"></a>Installez Giraph à l’aide des actions de script</span><span class="sxs-lookup"><span data-stu-id="aafec-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="aafec-129">Un tooinstall de script d’exemple Giraph sur un cluster HDInsight est disponible à l’adresse hello l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="aafec-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="aafec-130">Cette section fournit des instructions sur la façon dont toouse hello exemple de script lors de la création du cluster de hello à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aafec-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="aafec-131">Une action de script peut être appliquée à l’aide d’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="aafec-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="aafec-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aafec-132">Azure PowerShell</span></span>
> * <span data-ttu-id="aafec-133">Hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="aafec-133">hello Azure CLI</span></span>
> * <span data-ttu-id="aafec-134">Hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="aafec-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="aafec-135">Modèles Microsoft Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="aafec-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="aafec-136">Vous pouvez également appliquer tooalready d’actions de script clusters en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="aafec-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="aafec-137">Pour plus d’informations, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aafec-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="aafec-138">Démarrer la création d’un cluster à l’aide des étapes hello dans [clusters basés sur Linux de créer de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md), mais n’effectuez pas la création.</span><span class="sxs-lookup"><span data-stu-id="aafec-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="aafec-139">Sur hello **Configuration facultative** panneau, sélectionnez **Actions de Script**et fournir hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="aafec-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="aafec-140">**NOM**: entrez un nom convivial pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="aafec-141">**URI du SCRIPT** : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="aafec-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="aafec-142">**HEAD** : cochez cette entrée.</span><span class="sxs-lookup"><span data-stu-id="aafec-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="aafec-143">**WORKER** : laissez cette entrée désactivée.</span><span class="sxs-lookup"><span data-stu-id="aafec-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="aafec-144">**ZOOKEEPER** : laissez cette entrée désactivée.</span><span class="sxs-lookup"><span data-stu-id="aafec-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="aafec-145">**PARAMETERS**: laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="aafec-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="aafec-146">En bas de hello Hello **Actions de Script**, utilisez hello **sélectionnez** configuration hello toosave du bouton.</span><span class="sxs-lookup"><span data-stu-id="aafec-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="aafec-147">Enfin, utilisez hello **sélectionnez** bouton bas hello hello **Configuration facultative** informations de configuration facultatives panneau toosave hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="aafec-148">Poursuivre la création de cluster de hello comme décrit dans [clusters basés sur Linux de créer de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aafec-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="aafec-149"><a name="usegiraph"></a>Utilisation de Giraph dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="aafec-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="aafec-150">Une fois que le cluster de hello a été créé, utilisez hello étapes toorun hello SimpleShortestPathsComputation exemple inclus avec Giraph suivant.</span><span class="sxs-lookup"><span data-stu-id="aafec-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="aafec-151">Cet exemple utilise basic de hello [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implémentation utilisée pour rechercher le chemin d’accès plus court de hello entre les objets dans un graphique.</span><span class="sxs-lookup"><span data-stu-id="aafec-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="aafec-152">Connecter le cluster HDInsight de toohello à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="aafec-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="aafec-153">Pour en savoir plus, voir [Utilisation de SSH avec HDInsight (Hadoop) depuis Bash (l’interpréteur de commande) sur Windows 10, Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aafec-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="aafec-154">Toocreate de commande suivant de hello d’utiliser un fichier nommé **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="aafec-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="aafec-155">Utilisez hello après le texte en tant que contenu hello de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="aafec-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="aafec-156">Ces données décrivant une relation entre les objets dans un graphique orienté, à l’aide du format de hello `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="aafec-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="aafec-157">Chaque ligne représente une relation entre un objet `source_id` et un ou plusieurs objets `dest_id`.</span><span class="sxs-lookup"><span data-stu-id="aafec-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="aafec-158">Hello `edge_value` peut être considéré comme puissance de hello ou de distance de connexion hello entre `source_id` et `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="aafec-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="aafec-159">Dessiner, à l’aide de valeur hello (ou les poids) en tant que distance hello entre des objets, les données de salutation peut se présenter comme hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="aafec-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="aafec-161">fichier de hello toosave, utilisez **Ctrl + X**, puis **Y**et enfin **entrée** nom de fichier tooaccept hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="aafec-162">Utilisez hello suivant des données de salutation toostore dans le stockage principal pour votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="aafec-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="aafec-163">Exécutez hello SimpleShortestPathsComputation exemple à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="aafec-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="aafec-164">paramètres de Hello utilisés avec cette commande sont décrits dans hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="aafec-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="aafec-165">Paramètre</span><span class="sxs-lookup"><span data-stu-id="aafec-165">Parameter</span></span> | <span data-ttu-id="aafec-166">Résultat</span><span class="sxs-lookup"><span data-stu-id="aafec-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="aafec-167">fichier jar du Hello qui contient des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="aafec-168">classe Hello utilisé les exemples de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="aafec-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="aafec-169">exemple Hello qui est utilisé.</span><span class="sxs-lookup"><span data-stu-id="aafec-169">hello example that is used.</span></span> <span data-ttu-id="aafec-170">Dans cet exemple, il calcule hello plus court chemin entre ID 1 et tous les autres ID dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="aafec-171">nœud principal de Hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="aafec-172">Hello toouse de format d’entrée pour les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="aafec-173">fichier de données d’entrée Hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="aafec-174">format de sortie Hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-174">hello output format.</span></span> <span data-ttu-id="aafec-175">Dans cet exemple, l’ID et la valeur sous forme de texte brut.</span><span class="sxs-lookup"><span data-stu-id="aafec-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="aafec-176">emplacement de sortie Hello.</span><span class="sxs-lookup"><span data-stu-id="aafec-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="aafec-177">nombre de Hello de travailleurs toouse.</span><span class="sxs-lookup"><span data-stu-id="aafec-177">hello number of workers toouse.</span></span> <span data-ttu-id="aafec-178">Dans cet exemple, 2.</span><span class="sxs-lookup"><span data-stu-id="aafec-178">In this example, 2.</span></span> |

    <span data-ttu-id="aafec-179">Pour plus d’informations sur ces et autres paramètres utilisés avec les exemples de Giraph, consultez hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="aafec-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="aafec-180">Une fois le travail de hello terminée, les résultats de hello sont stockés dans hello **/example/out/shotestpaths** active.</span><span class="sxs-lookup"><span data-stu-id="aafec-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="aafec-181">Hello les noms de fichiers de sortie commencent par **partie-m -** et se terminer par un nombre indiquant hello tout d’abord, en second lieu, les fichiers etc..</span><span class="sxs-lookup"><span data-stu-id="aafec-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="aafec-182">Utilisez hello après la sortie de commande tooview hello :</span><span class="sxs-lookup"><span data-stu-id="aafec-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="aafec-183">une sortie Hello doit apparaître toohello similaire après le texte :</span><span class="sxs-lookup"><span data-stu-id="aafec-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="aafec-184">Hello SimpleShortestPathComputation exemple est codé en dur toostart avec l’objet ID 1 et rechercher des objets de tooother hello plus courts chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="aafec-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="aafec-185">sortie de Hello est au format hello de `destination_id` et `distance`.</span><span class="sxs-lookup"><span data-stu-id="aafec-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="aafec-186">Hello `distance` est hello valeur (poids) des bords hello traversées entre l’objet ID 1 et ID hello cible.</span><span class="sxs-lookup"><span data-stu-id="aafec-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="aafec-187">Visualiser ces données, vous pouvez vérifier les résultats hello par déplacement des chemins d’accès plus courts de hello entre l’ID 1 et tous les autres objets.</span><span class="sxs-lookup"><span data-stu-id="aafec-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="aafec-188">Hello plus court chemin entre ID 1 et 4 de l’ID est 5.</span><span class="sxs-lookup"><span data-stu-id="aafec-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="aafec-189">Cette valeur est la distance totale de hello entre <span style="color:orange">ID 1 et 3</span>, puis <span style="color:red">ID 3 et 4</span>.</span><span class="sxs-lookup"><span data-stu-id="aafec-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="aafec-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aafec-191">Next steps</span></span>

* <span data-ttu-id="aafec-192">[Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aafec-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="aafec-193">[Installation de Solr sur des clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aafec-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
