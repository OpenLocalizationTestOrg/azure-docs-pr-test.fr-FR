---
title: "Utiliser une action de script pour installer Solr sur HDInsight basé sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment installer Solr sur des clusters Hadoop HDInsight basés sur Linux à l’aide des actions de script."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: ad930ca023a36fa5874483873c82fdba11d117c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="d33c4-103">Installation et utilisation de Solr sur des clusters HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="d33c4-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="d33c4-104">Découvrez comment installer Solr sur Azure HDInsight en utilisant une action de script.</span><span class="sxs-lookup"><span data-stu-id="d33c4-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="d33c4-105">Solr est une puissante plateforme de recherche qui fournit des fonctionnalités de recherche au niveau de l'entreprise pour les données gérées par Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d33c4-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="d33c4-106">Les étapes décrites dans ce document nécessitent un cluster HDInsight utilisant Linux.</span><span class="sxs-lookup"><span data-stu-id="d33c4-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="d33c4-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="d33c4-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d33c4-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d33c4-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d33c4-109">L’exemple de script utilisé dans ce document installe un cluster Solr 4.9 avec une configuration spécifique.</span><span class="sxs-lookup"><span data-stu-id="d33c4-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="d33c4-110">Si vous souhaitez configurer le cluster Solr avec d’autres collections, partitions, schémas, réplicas, etc., vous devez modifier le script et les fichiers binaires Solr.</span><span class="sxs-lookup"><span data-stu-id="d33c4-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span></span>

## <span data-ttu-id="d33c4-111"><a name="whatis"></a>Présentation de Solr</span><span class="sxs-lookup"><span data-stu-id="d33c4-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="d33c4-112">[Apache Solr](http://lucene.apache.org/solr/features.html) est une plateforme de recherche d’entreprises qui permet d’effectuer de puissantes opérations de recherche en texte intégral sur des données.</span><span class="sxs-lookup"><span data-stu-id="d33c4-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="d33c4-113">Alors que Hadoop permet de stocker et de gérer de grandes quantités de données, Apache Solr fournit les fonctionnalités de recherche nécessaires pour les récupérer rapidement.</span><span class="sxs-lookup"><span data-stu-id="d33c4-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

> [!WARNING]
> <span data-ttu-id="d33c4-114">Les composants fournis avec le cluster HDInsight sont entièrement pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d33c4-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="d33c4-115">Les composants personnalisés, tels que Solr, bénéficient d'un support commercialement raisonnable pour vous aider à résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="d33c4-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="d33c4-116">Il se peut que le support Microsoft ne soit pas en mesure de résoudre les problèmes avec des composants personnalisés.</span><span class="sxs-lookup"><span data-stu-id="d33c4-116">Microsoft support may not be able to resolve problems with custom components.</span></span> <span data-ttu-id="d33c4-117">Vous devrez peut-être contacter les communautés open source pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="d33c4-117">You may need to engage the open source communities for assistance.</span></span> <span data-ttu-id="d33c4-118">Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="d33c4-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="d33c4-119">En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="d33c4-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-the-script-does"></a><span data-ttu-id="d33c4-120">Ce que fait le script</span><span class="sxs-lookup"><span data-stu-id="d33c4-120">What the script does</span></span>

<span data-ttu-id="d33c4-121">Ce script effectue les modifications suivantes au cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="d33c4-121">This script makes the following changes to the HDInsight cluster:</span></span>

* <span data-ttu-id="d33c4-122">Installe Solr 4.9 dans `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="d33c4-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="d33c4-123">Crée un nouvel utilisateur, **solrusr**, qui est utilisé pour exécuter le service Solr</span><span class="sxs-lookup"><span data-stu-id="d33c4-123">Creates a user, **solrusr**, which is used to run the Solr service</span></span>
* <span data-ttu-id="d33c4-124">Définit **solruser** comme propriétaire de `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="d33c4-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="d33c4-125">Ajoute une configuration [Upstart](http://upstart.ubuntu.com/) qui démarre Solr automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d33c4-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="d33c4-126"><a name="install"></a>Installer Solr à l’aide d’actions de script</span><span class="sxs-lookup"><span data-stu-id="d33c4-126"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="d33c4-127">Un exemple de script d’installation de Solr sur un cluster HDInsight est disponible à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="d33c4-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="d33c4-128">Pour créer un cluster sur lequel Solr est installé, utilisez les étapes décrites dans le document [Créer des clusters HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d33c4-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="d33c4-129">Pendant le processus de création, procédez comme suit pour installer Solr :</span><span class="sxs-lookup"><span data-stu-id="d33c4-129">During the creation process, use the following steps to install Solr:</span></span>

1. <span data-ttu-id="d33c4-130">Dans le panneau __Résumé du cluster__ sélectionnez__Paramètres avancés__, puis __Actions de script__.</span><span class="sxs-lookup"><span data-stu-id="d33c4-130">From the __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="d33c4-131">Utilisez les informations suivantes pour remplir le formulaire :</span><span class="sxs-lookup"><span data-stu-id="d33c4-131">Use the following information to populate the form:</span></span>

   * <span data-ttu-id="d33c4-132">**NAME**: saisissez un nom convivial pour l’action de script.</span><span class="sxs-lookup"><span data-stu-id="d33c4-132">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="d33c4-133">**URI du script** : https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="d33c4-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="d33c4-134">**HEAD**: cochez cette option.</span><span class="sxs-lookup"><span data-stu-id="d33c4-134">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="d33c4-135">**WORKER** : cochez cette option</span><span class="sxs-lookup"><span data-stu-id="d33c4-135">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="d33c4-136">**ZOOKEEPER** : cochez cette option pour installer le nœud ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="d33c4-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span></span>
   * <span data-ttu-id="d33c4-137">**PARAMETERS**: laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="d33c4-137">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="d33c4-138">En bas du panneau **Actions de script**, utilisez le bouton **Sélectionner** pour enregistrer la configuration.</span><span class="sxs-lookup"><span data-stu-id="d33c4-138">At the bottom of the **Script actions** blade, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="d33c4-139">Enfin, cliquez sur **Suivant** pour revenir au __résumé du cluster__</span><span class="sxs-lookup"><span data-stu-id="d33c4-139">Finally, use the **Next** button to return to the __Cluster summary__</span></span>

3. <span data-ttu-id="d33c4-140">Sur la page __résumé du cluster__, sélectionnez __Créer__ pour créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="d33c4-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span></span>

## <span data-ttu-id="d33c4-141"><a name="usesolr"></a>Utilisation de Solr dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="d33c4-141"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d33c4-142">Les étapes de cette section présentent les fonctionnalités de base de Solr.</span><span class="sxs-lookup"><span data-stu-id="d33c4-142">The steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="d33c4-143">Pour plus d’informations sur l’utilisation de Solr, consultez le [site Apache Solr](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="d33c4-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="d33c4-144">Données d'index</span><span class="sxs-lookup"><span data-stu-id="d33c4-144">Index data</span></span>

<span data-ttu-id="d33c4-145">Procédez comme suit pour ajouter des exemples de données vers Solr, puis procédez à une requête :</span><span class="sxs-lookup"><span data-stu-id="d33c4-145">Use the following steps to add example data to Solr, and then query it:</span></span>

1. <span data-ttu-id="d33c4-146">Connectez-vous au cluster HDInsight à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="d33c4-146">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="d33c4-147">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d33c4-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="d33c4-148">Les étapes suivantes de ce document utilisent un tunnel SSL pour se connecter à l’interface utilisateur Solr.</span><span class="sxs-lookup"><span data-stu-id="d33c4-148">Steps later in this document use an SSL tunnel to connect to the Solr web UI.</span></span> <span data-ttu-id="d33c4-149">Pour utiliser ces étapes, vous devez établir un tunnel SSL, puis configurer votre navigateur pour l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="d33c4-149">To use these steps, you must establish an SSL tunnel and then configure your browser to use it.</span></span>
     >
     > <span data-ttu-id="d33c4-150">Pour plus d’informations, consultez le document [Utilisation du tunnel SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="d33c4-150">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="d33c4-151">Pour obtenir des exemples de données Solr, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d33c4-151">Use the following commands to have Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="d33c4-152">Voici les résultats qui sont retournés à la console :</span><span class="sxs-lookup"><span data-stu-id="d33c4-152">The following output is returned to the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="d33c4-153">L’utilitaire `post.jar` ajoute les documents **solr.xml** et **monitor.xml** à l’index.</span><span class="sxs-lookup"><span data-stu-id="d33c4-153">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span></span>
  
3. <span data-ttu-id="d33c4-154">Pour interroger l’API REST de Solr, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d33c4-154">Use the following command to query the Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="d33c4-155">Cette commande recherche **collection1** pour tous les documents correspondant à  **\*:\***  (encodé sous la forme \*%3A\* dans la chaîne de requête).</span><span class="sxs-lookup"><span data-stu-id="d33c4-155">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span></span> <span data-ttu-id="d33c4-156">Le document JSON suivant est un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="d33c4-156">The following JSON document is an example of the response:</span></span>

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, the Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication to other Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over the e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-the-solr-dashboard"></a><span data-ttu-id="d33c4-157">Utilisation du tableau de bord Solr</span><span class="sxs-lookup"><span data-stu-id="d33c4-157">Using the Solr dashboard</span></span>

<span data-ttu-id="d33c4-158">Le tableau de bord Solr est une interface utilisateur web qui permet de travailler avec le mode série sur Solr via votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="d33c4-158">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span></span> <span data-ttu-id="d33c4-159">Le tableau de bord Solr n’est pas exposé directement sur Internet à partir de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d33c4-159">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span></span> <span data-ttu-id="d33c4-160">Vous pouvez utiliser un tunnel SSH pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="d33c4-160">You can use an SSH tunnel to access it.</span></span> <span data-ttu-id="d33c4-161">Pour plus d’informations sur l’utilisation du tunnel SSH, consultez le document [Utilisation du tunnel SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="d33c4-161">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="d33c4-162">Une fois que vous avez établi un tunnel SSH, procédez comme suit pour utiliser le tableau de bord Solr :</span><span class="sxs-lookup"><span data-stu-id="d33c4-162">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span></span>

1. <span data-ttu-id="d33c4-163">Déterminez le nom d’hôte du nœud principal primaire :</span><span class="sxs-lookup"><span data-stu-id="d33c4-163">Determine the host name for the primary headnode:</span></span>

   1. <span data-ttu-id="d33c4-164">Utilisez SSH pour vous connecter au nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="d33c4-164">Use SSH to connect to the cluster head node.</span></span> <span data-ttu-id="d33c4-165">Par exemple, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="d33c4-165">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="d33c4-166">Pour plus d’informations sur l’utilisation de SSH, consultez le document [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d33c4-166">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="d33c4-167">Utilisez la commande suivante pour obtenir le nom d’hôte complet :</span><span class="sxs-lookup"><span data-stu-id="d33c4-167">Use the following command to get the fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="d33c4-168">Cette commande retourne une valeur semblable au nom d’hôte suivant :</span><span class="sxs-lookup"><span data-stu-id="d33c4-168">This command returns a value similar to the following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="d33c4-169">Enregistrez la valeur retournée, car elle est utilisée ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="d33c4-169">Save the value returned, as it is used later.</span></span>

2. <span data-ttu-id="d33c4-170">Dans votre navigateur, connectez-vous à **http://HOSTNAME:8983/solr/#/**, où **HOSTNAME** correspond au nom que vous avez déterminé aux étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="d33c4-170">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span></span>

    <span data-ttu-id="d33c4-171">La requête est routée via le tunnel SSH jusqu’à l’interface utilisateur web Solr sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d33c4-171">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span></span> <span data-ttu-id="d33c4-172">Le page est similaire à l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="d33c4-172">The page appears similar to the following image:</span></span>

    ![Image du tableau de bord Solr.](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="d33c4-174">Dans le volet de gauche, utilisez la liste déroulante **Sélecteur de base** pour sélectionner **collection1**.</span><span class="sxs-lookup"><span data-stu-id="d33c4-174">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span></span> <span data-ttu-id="d33c4-175">Plusieurs entrées doivent apparaître sous **collection1**.</span><span class="sxs-lookup"><span data-stu-id="d33c4-175">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="d33c4-176">Dans les entrées sous **collection1**, sélectionnez **Requête**.</span><span class="sxs-lookup"><span data-stu-id="d33c4-176">From the entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="d33c4-177">Utilisez les valeurs suivantes pour remplir la page de recherche :</span><span class="sxs-lookup"><span data-stu-id="d33c4-177">Use the following values to populate the search page:</span></span>

   * <span data-ttu-id="d33c4-178">Dans la zone de texte **q**, entrez **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="d33c4-178">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="d33c4-179">La requête renvoie tous les documents indexés dans Solr.</span><span class="sxs-lookup"><span data-stu-id="d33c4-179">This query returns all the documents that are indexed in Solr.</span></span> <span data-ttu-id="d33c4-180">Si vous souhaitez rechercher une chaîne spécifique dans les documents, vous pouvez la saisir à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="d33c4-180">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="d33c4-181">Sélectionnez le format de sortie dans la zone de texte **wt** .</span><span class="sxs-lookup"><span data-stu-id="d33c4-181">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="d33c4-182">La valeur par défaut est **json**.</span><span class="sxs-lookup"><span data-stu-id="d33c4-182">Default is **json**.</span></span>

     <span data-ttu-id="d33c4-183">Enfin, sélectionnez le bouton **Exécuter la requête** au bas de la page de recherche.</span><span class="sxs-lookup"><span data-stu-id="d33c4-183">Finally, select the **Execute Query** button at the bottom of the search pate.</span></span>

     ![Utilisation d’une action de script pour personnaliser un cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="d33c4-185">Le résultat renvoie les deux documents que vous avez précédemment ajoutés à l’index.</span><span class="sxs-lookup"><span data-stu-id="d33c4-185">The output returns the two documents that you added to the index earlier.</span></span> <span data-ttu-id="d33c4-186">Le résultat ressemble au document JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="d33c4-186">The output is similar to the following JSON document:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="d33c4-187">Démarrage et arrêt de Solr</span><span class="sxs-lookup"><span data-stu-id="d33c4-187">Starting and stopping Solr</span></span>

<span data-ttu-id="d33c4-188">Pour arrêter ou démarrer Solr manuellement, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d33c4-188">Use the following commands to manually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="d33c4-189">Sauvegarde de données indexées</span><span class="sxs-lookup"><span data-stu-id="d33c4-189">Backup indexed data</span></span>

<span data-ttu-id="d33c4-190">Pour sauvegarder les données de Solr sur le stockage par défaut pour votre cluster, utilisez la procédure suivante :</span><span class="sxs-lookup"><span data-stu-id="d33c4-190">Use the following steps to back up Solr data to the default storage for your cluster:</span></span>

1. <span data-ttu-id="d33c4-191">Connectez-vous au cluster à l’aide de SSH, puis utilisez la commande suivante pour obtenir le nom d’hôte du nœud principal :</span><span class="sxs-lookup"><span data-stu-id="d33c4-191">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="d33c4-192">Utilisez la commande suivante pour créer une capture instantanée des données indexées.</span><span class="sxs-lookup"><span data-stu-id="d33c4-192">Use the following command to create a snapshot of the indexed data.</span></span> <span data-ttu-id="d33c4-193">Remplacez **HOSTNAME** par le nom retourné par la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="d33c4-193">Replace **HOSTNAME** with the name returned from the previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="d33c4-194">La réponse ressemble au XML suivant :</span><span class="sxs-lookup"><span data-stu-id="d33c4-194">The response is similar to the following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="d33c4-195">Remplacez les répertoires par `/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="d33c4-195">Change directories to `/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="d33c4-196">Il y a ici un sous-répertoire pour chaque collection.</span><span class="sxs-lookup"><span data-stu-id="d33c4-196">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="d33c4-197">Chaque répertoire de la collection contient un répertoire `data` qui contient la capture instantanée de la collection.</span><span class="sxs-lookup"><span data-stu-id="d33c4-197">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span></span>

4. <span data-ttu-id="d33c4-198">Pour créer une archive compressée du dossier de capture d’instantané, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d33c4-198">To create a compressed archive of the snapshot folder, use the following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="d33c4-199">Remplacez les valeurs `snapshot.20150806185338855` portant le nom de la capture d’instantané pour votre collection.</span><span class="sxs-lookup"><span data-stu-id="d33c4-199">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span></span>

    <span data-ttu-id="d33c4-200">Cette commande crée une archive nommée **snapshot.20150806185338855.tgz**, dans laquelle se trouve le contenu du répertoire **snapshot.20150806185338855**.</span><span class="sxs-lookup"><span data-stu-id="d33c4-200">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="d33c4-201">Vous pouvez ensuite stocker l’archive vers le stockage principal du cluster à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d33c4-201">You can then store the archive to the cluster's primary storage using the following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="d33c4-202">Pour plus d’informations sur l’utilisation de sauvegardes et de restaurations Solr, consultez [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="d33c4-202">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d33c4-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d33c4-203">Next steps</span></span>

* <span data-ttu-id="d33c4-204">[Installation de Giraph sur des clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d33c4-204">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="d33c4-205">Utilisez la personnalisation de clusters pour installer Giraph sur des clusters HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d33c4-205">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="d33c4-206">Giraph permet de traiter des graphiques à l’aide de Hadoop et peut être utilisé avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d33c4-206">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="d33c4-207">[Installer Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d33c4-207">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="d33c4-208">Utilisez la personnalisation de clusters pour installer Hue sur des clusters HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d33c4-208">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="d33c4-209">Hue est un ensemble d’applications web permettant d’interagir avec un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d33c4-209">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
