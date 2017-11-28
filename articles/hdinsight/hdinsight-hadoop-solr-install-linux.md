---
title: "Action de Script d’aaaUse tooinstall Solr sur HDInsight basés sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment tooinstall Solr sur basés sur Linux HDInsight Hadoop clusters à l’aide des Actions de Script."
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
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="85b9a-103">Installation et utilisation de Solr sur des clusters HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="85b9a-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="85b9a-104">Découvrez comment tooinstall Solr sur Azure HDInsight en utilisant l’Action de Script.</span><span class="sxs-lookup"><span data-stu-id="85b9a-104">Learn how tooinstall Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="85b9a-105">Solr est une puissante plateforme de recherche qui fournit des fonctionnalités de recherche au niveau de l'entreprise pour les données gérées par Hadoop.</span><span class="sxs-lookup"><span data-stu-id="85b9a-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="85b9a-106">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="85b9a-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="85b9a-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="85b9a-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="85b9a-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="85b9a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85b9a-109">exemple de script Hello utilisé dans ce document installe Solr 4.9 avec une configuration spécifique.</span><span class="sxs-lookup"><span data-stu-id="85b9a-109">hello sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="85b9a-110">Si vous souhaitez que le cluster de Solr hello tooconfigure avec différents regroupements, partitions, schémas, les réplicas, etc., vous devez modifier le script de hello et les fichiers binaires de Solr.</span><span class="sxs-lookup"><span data-stu-id="85b9a-110">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries.</span></span>

## <span data-ttu-id="85b9a-111"><a name="whatis"></a>Présentation de Solr</span><span class="sxs-lookup"><span data-stu-id="85b9a-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="85b9a-112">[Apache Solr](http://lucene.apache.org/solr/features.html) est une plateforme de recherche d’entreprise qui permet d’effectuer de puissantes opérations de recherche en texte intégral sur des données.</span><span class="sxs-lookup"><span data-stu-id="85b9a-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="85b9a-113">Tandis que Hadoop permet de stocker et gérer des quantités importantes de données, Apache Solr fournit les fonctionnalités de recherche hello tooquickly extraire des données hello.</span><span class="sxs-lookup"><span data-stu-id="85b9a-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

> [!WARNING]
> <span data-ttu-id="85b9a-114">Composants fournis avec le cluster HDInsight de hello sont entièrement pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="85b9a-114">Components provided with hello HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="85b9a-115">Les composants personnalisés, tels que Solr, réception efforcera toohelp vous toofurther hello de dépannage.</span><span class="sxs-lookup"><span data-stu-id="85b9a-115">Custom components, such as Solr, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="85b9a-116">Prise en charge de Microsoft ne peut pas être en mesure de tooresolve des problèmes avec des composants personnalisés.</span><span class="sxs-lookup"><span data-stu-id="85b9a-116">Microsoft support may not be able tooresolve problems with custom components.</span></span> <span data-ttu-id="85b9a-117">Vous devrez peut-être les Communautés de tooengage hello open source pour obtenir une assistance.</span><span class="sxs-lookup"><span data-stu-id="85b9a-117">You may need tooengage hello open source communities for assistance.</span></span> <span data-ttu-id="85b9a-118">Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="85b9a-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-hello-script-does"></a><span data-ttu-id="85b9a-119">Le script hello effectue</span><span class="sxs-lookup"><span data-stu-id="85b9a-119">What hello script does</span></span>

<span data-ttu-id="85b9a-120">Ce script fait hello suivant du cluster HDInsight de toohello modifications :</span><span class="sxs-lookup"><span data-stu-id="85b9a-120">This script makes hello following changes toohello HDInsight cluster:</span></span>

* <span data-ttu-id="85b9a-121">Installe Solr 4.9 dans `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="85b9a-121">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="85b9a-122">Crée un utilisateur, **solrusr**, qui est utilisé toorun hello Solr service</span><span class="sxs-lookup"><span data-stu-id="85b9a-122">Creates a user, **solrusr**, which is used toorun hello Solr service</span></span>
* <span data-ttu-id="85b9a-123">Jeux de **solruser** en tant que propriétaire hello de`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="85b9a-123">Sets **solruser** as hello owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="85b9a-124">Ajoute une configuration [Upstart](http://upstart.ubuntu.com/) qui démarre Solr automatiquement.</span><span class="sxs-lookup"><span data-stu-id="85b9a-124">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="85b9a-125"><a name="install"></a>Installer Solr à l’aide d’actions de script</span><span class="sxs-lookup"><span data-stu-id="85b9a-125"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="85b9a-126">Un tooinstall de script d’exemple Solr sur un cluster HDInsight est disponible à l’adresse hello l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="85b9a-126">A sample script tooinstall Solr on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="85b9a-127">toocreate un cluster avec Solr installé, utilisez hello étapes Bonjour [HDInsight de créer des clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="85b9a-127">toocreate a cluster that has Solr installed, use hello steps in hello [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="85b9a-128">Au cours du processus de création de hello, utilisez hello suivant les étapes tooinstall Solr :</span><span class="sxs-lookup"><span data-stu-id="85b9a-128">During hello creation process, use hello following steps tooinstall Solr:</span></span>

1. <span data-ttu-id="85b9a-129">À partir de hello __résumé du Cluster__ settings__ select__Advanced, puis les lames, __actions de Script__.</span><span class="sxs-lookup"><span data-stu-id="85b9a-129">From hello __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="85b9a-130">Utilisez hello suivant formulaire hello toopopulate :</span><span class="sxs-lookup"><span data-stu-id="85b9a-130">Use hello following information toopopulate hello form:</span></span>

   * <span data-ttu-id="85b9a-131">**NOM**: entrez un nom convivial pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="85b9a-131">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="85b9a-132">**URI du script** : https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="85b9a-132">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="85b9a-133">**HEAD**: cochez cette option.</span><span class="sxs-lookup"><span data-stu-id="85b9a-133">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="85b9a-134">**WORKER** : cochez cette option</span><span class="sxs-lookup"><span data-stu-id="85b9a-134">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="85b9a-135">**SOIGNEUR**: Vérifiez tooinstall de cette option sur le nœud de soigneur hello</span><span class="sxs-lookup"><span data-stu-id="85b9a-135">**ZOOKEEPER**: Check this option tooinstall on hello Zookeeper node</span></span>
   * <span data-ttu-id="85b9a-136">**PARAMETERS**: laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="85b9a-136">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="85b9a-137">En bas de hello Hello **actions de Script** panneau, utilisez hello **sélectionnez** configuration hello toosave du bouton.</span><span class="sxs-lookup"><span data-stu-id="85b9a-137">At hello bottom of hello **Script actions** blade, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="85b9a-138">Enfin, utilisez hello **suivant** bouton tooreturn toohello __résumé du Cluster__</span><span class="sxs-lookup"><span data-stu-id="85b9a-138">Finally, use hello **Next** button tooreturn toohello __Cluster summary__</span></span>

3. <span data-ttu-id="85b9a-139">À partir de hello __résumé du Cluster__ page, sélectionnez __créer__ cluster hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="85b9a-139">From hello __Cluster summary__ page, select __Create__ toocreate hello cluster.</span></span>

## <span data-ttu-id="85b9a-140"><a name="usesolr"></a>Utilisation de Solr dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="85b9a-140"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85b9a-141">étapes Hello de cette section présentent les fonctionnalités de Solr base.</span><span class="sxs-lookup"><span data-stu-id="85b9a-141">hello steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="85b9a-142">Pour plus d’informations sur l’utilisation de Solr, consultez hello [Apache Solr site](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="85b9a-142">For more information on using Solr, see hello [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="85b9a-143">Données d'index</span><span class="sxs-lookup"><span data-stu-id="85b9a-143">Index data</span></span>

<span data-ttu-id="85b9a-144">Utilisez hello suivant les étapes tooadd exemple données tooSolr, puis de la requête :</span><span class="sxs-lookup"><span data-stu-id="85b9a-144">Use hello following steps tooadd example data tooSolr, and then query it:</span></span>

1. <span data-ttu-id="85b9a-145">Connecter le cluster HDInsight de toohello à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="85b9a-145">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="85b9a-146">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="85b9a-146">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="85b9a-147">Plus loin dans ce document utilisent un SSL tunnel tooconnect toohello Solr interface utilisateur web.</span><span class="sxs-lookup"><span data-stu-id="85b9a-147">Steps later in this document use an SSL tunnel tooconnect toohello Solr web UI.</span></span> <span data-ttu-id="85b9a-148">toouse ces étapes, vous devez établir une connexion SSL du tunnel, puis configurez votre navigateur toouse il.</span><span class="sxs-lookup"><span data-stu-id="85b9a-148">toouse these steps, you must establish an SSL tunnel and then configure your browser toouse it.</span></span>
     >
     > <span data-ttu-id="85b9a-149">Pour plus d’informations, consultez hello [utiliser SSH Tunneling hdinsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="85b9a-149">For more information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="85b9a-150">Utilisez hello commandes toohave Solr index exemple données suivantes :</span><span class="sxs-lookup"><span data-stu-id="85b9a-150">Use hello following commands toohave Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="85b9a-151">Hello le résultat suivant toohello console :</span><span class="sxs-lookup"><span data-stu-id="85b9a-151">hello following output is returned toohello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="85b9a-152">Hello `post.jar` utilitaire ajoute hello **solr.xml** et **monitor.xml** index toohello de documents.</span><span class="sxs-lookup"><span data-stu-id="85b9a-152">hello `post.jar` utility adds hello **solr.xml** and **monitor.xml** documents toohello index.</span></span>
  
3. <span data-ttu-id="85b9a-153">Utilisez hello suivant commande tooquery hello Solr REST API :</span><span class="sxs-lookup"><span data-stu-id="85b9a-153">Use hello following command tooquery hello Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="85b9a-154">Cette commande recherche **collection1** les documents correspondant à  **\*:\***  (encodé sous la forme \*% 3 a\* dans la chaîne de requête hello).</span><span class="sxs-lookup"><span data-stu-id="85b9a-154">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in hello query string).</span></span> <span data-ttu-id="85b9a-155">Hello suivant du document JSON est un exemple de réponse de hello :</span><span class="sxs-lookup"><span data-stu-id="85b9a-155">hello following JSON document is an example of hello response:</span></span>

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
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
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
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

### <a name="using-hello-solr-dashboard"></a><span data-ttu-id="85b9a-156">À l’aide du tableau de bord hello Solr</span><span class="sxs-lookup"><span data-stu-id="85b9a-156">Using hello Solr dashboard</span></span>

<span data-ttu-id="85b9a-157">tableau de bord Solr Hello est une interface utilisateur qui vous permet de toowork avec Solr via votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="85b9a-157">hello Solr dashboard is a web UI that allows you toowork with Solr through your web browser.</span></span> <span data-ttu-id="85b9a-158">tableau de bord Solr Hello n’est pas exposée directement sur hello Internet à partir de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85b9a-158">hello Solr dashboard is not exposed directly on hello Internet from your HDInsight cluster.</span></span> <span data-ttu-id="85b9a-159">Vous pouvez utiliser un tooaccess de tunnel SSH il.</span><span class="sxs-lookup"><span data-stu-id="85b9a-159">You can use an SSH tunnel tooaccess it.</span></span> <span data-ttu-id="85b9a-160">Pour plus d’informations sur l’utilisation d’un tunnel SSH, consultez hello [utiliser SSH Tunneling hdinsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="85b9a-160">For more information on using an SSH tunnel, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="85b9a-161">Une fois que vous avez établi un tunnel SSH, utilisez hello suivant du tableau de bord étapes toouse hello Solr :</span><span class="sxs-lookup"><span data-stu-id="85b9a-161">Once you have established an SSH tunnel, use hello following steps toouse hello Solr dashboard:</span></span>

1. <span data-ttu-id="85b9a-162">Déterminer le nom d’hôte hello pour le nœud principal de principal hello :</span><span class="sxs-lookup"><span data-stu-id="85b9a-162">Determine hello host name for hello primary headnode:</span></span>

   1. <span data-ttu-id="85b9a-163">Utilisez le nœud principal du cluster toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="85b9a-163">Use SSH tooconnect toohello cluster head node.</span></span> <span data-ttu-id="85b9a-164">Par exemple, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="85b9a-164">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="85b9a-165">Pour plus d’informations sur l’utilisation de SSH, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="85b9a-165">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="85b9a-166">Utilisez hello tooget hello nom d’hôte complet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="85b9a-166">Use hello following command tooget hello fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="85b9a-167">Cette commande retourne un toohello similaire valeur suivant le nom d’hôte :</span><span class="sxs-lookup"><span data-stu-id="85b9a-167">This command returns a value similar toohello following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="85b9a-168">Enregistrer la valeur hello retourné, qu’il est utilisé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="85b9a-168">Save hello value returned, as it is used later.</span></span>

2. <span data-ttu-id="85b9a-169">Dans votre navigateur, connectez-vous trop**http://HOSTNAME:8983/solr / #/**, où **nom d’hôte** est le nom hello déterminée dans les étapes précédentes hello.</span><span class="sxs-lookup"><span data-stu-id="85b9a-169">In your browser, connect too**http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is hello name you determined in hello previous steps.</span></span>

    <span data-ttu-id="85b9a-170">demande de Hello est routée via hello SSH tunnel toohello Solr interface utilisateur web sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="85b9a-170">hello request is routed through hello SSH tunnel toohello Solr web UI on your cluster.</span></span> <span data-ttu-id="85b9a-171">Hello similaire toohello suivant l’image apparaît :</span><span class="sxs-lookup"><span data-stu-id="85b9a-171">hello page appears similar toohello following image:</span></span>

    ![Image du tableau de bord Solr.](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="85b9a-173">À partir du volet de gauche hello, utilisez hello **Core sélecteur** tooselect de liste déroulante **collection1**.</span><span class="sxs-lookup"><span data-stu-id="85b9a-173">From hello left pane, use hello **Core Selector** drop-down tooselect **collection1**.</span></span> <span data-ttu-id="85b9a-174">Plusieurs entrées doivent apparaître sous **collection1**.</span><span class="sxs-lookup"><span data-stu-id="85b9a-174">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="85b9a-175">À partir des entrées hello ci-dessous **collection1**, sélectionnez **requête**.</span><span class="sxs-lookup"><span data-stu-id="85b9a-175">From hello entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="85b9a-176">Utilisez hello après la page de recherche de valeurs toopopulate hello :</span><span class="sxs-lookup"><span data-stu-id="85b9a-176">Use hello following values toopopulate hello search page:</span></span>

   * <span data-ttu-id="85b9a-177">Bonjour **q** texte, entrez  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="85b9a-177">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="85b9a-178">Cette requête renvoie tous les documents de hello sont indexés dans Solr.</span><span class="sxs-lookup"><span data-stu-id="85b9a-178">This query returns all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="85b9a-179">Si vous souhaitez toosearch une chaîne spécifique au sein de documents de hello, vous pouvez entrer ici cette chaîne.</span><span class="sxs-lookup"><span data-stu-id="85b9a-179">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="85b9a-180">Bonjour **wt** zone de texte, le format de sortie hello select.</span><span class="sxs-lookup"><span data-stu-id="85b9a-180">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="85b9a-181">La valeur par défaut est **json**.</span><span class="sxs-lookup"><span data-stu-id="85b9a-181">Default is **json**.</span></span>

     <span data-ttu-id="85b9a-182">Enfin, sélectionnez hello **exécuter la requête** bouton bas hello pate de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="85b9a-182">Finally, select hello **Execute Query** button at hello bottom of hello search pate.</span></span>

     ![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="85b9a-184">sortie de Hello retourne hello deux documents que vous avez ajouté toohello index précédemment.</span><span class="sxs-lookup"><span data-stu-id="85b9a-184">hello output returns hello two documents that you added toohello index earlier.</span></span> <span data-ttu-id="85b9a-185">Hello est similaire toohello suivant document JSON de sortie :</span><span class="sxs-lookup"><span data-stu-id="85b9a-185">hello output is similar toohello following JSON document:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
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
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="85b9a-186">Démarrage et arrêt de Solr</span><span class="sxs-lookup"><span data-stu-id="85b9a-186">Starting and stopping Solr</span></span>

<span data-ttu-id="85b9a-187">Utilisez hello suivant les commandes toomanually arrêter et démarrer des Solr :</span><span class="sxs-lookup"><span data-stu-id="85b9a-187">Use hello following commands toomanually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="85b9a-188">Sauvegarde de données indexées</span><span class="sxs-lookup"><span data-stu-id="85b9a-188">Backup indexed data</span></span>

<span data-ttu-id="85b9a-189">Hello suivant tooback étapes Solr données toohello par défaut l’espace de stockage pour votre cluster, utilisez :</span><span class="sxs-lookup"><span data-stu-id="85b9a-189">Use hello following steps tooback up Solr data toohello default storage for your cluster:</span></span>

1. <span data-ttu-id="85b9a-190">Se connecter cluster toohello à l’aide de SSH, puis utilisez hello suivant le nom d’hôte de commande tooget hello pour le nœud principal de hello :</span><span class="sxs-lookup"><span data-stu-id="85b9a-190">Connect toohello cluster using SSH, then use hello following command tooget hello host name for hello head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="85b9a-191">Utilisez hello suivant commande toocreate un instantané des données de hello indexé.</span><span class="sxs-lookup"><span data-stu-id="85b9a-191">Use hello following command toocreate a snapshot of hello indexed data.</span></span> <span data-ttu-id="85b9a-192">Remplacez **nom d’hôte** avec nom hello retourné à partir de la commande précédente hello :</span><span class="sxs-lookup"><span data-stu-id="85b9a-192">Replace **HOSTNAME** with hello name returned from hello previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="85b9a-193">réponse de Hello est similaire toohello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="85b9a-193">hello response is similar toohello following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="85b9a-194">Remplacez les répertoires`/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="85b9a-194">Change directories too`/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="85b9a-195">Il y a ici un sous-répertoire pour chaque collection.</span><span class="sxs-lookup"><span data-stu-id="85b9a-195">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="85b9a-196">Chaque répertoire de la collection contient un `data` répertoire qui contient l’instantané hello pour collection de hello.</span><span class="sxs-lookup"><span data-stu-id="85b9a-196">Each collection directory contains a `data` directory that contains hello snapshot for hello collection.</span></span>

4. <span data-ttu-id="85b9a-197">toocreate une archive compressée du dossier de capture instantanée hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="85b9a-197">toocreate a compressed archive of hello snapshot folder, use hello following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="85b9a-198">Remplacez hello `snapshot.20150806185338855` nom hello d’instantané de hello pour votre collection de valeurs.</span><span class="sxs-lookup"><span data-stu-id="85b9a-198">Replace hello `snapshot.20150806185338855` values with hello name of hello snapshot for your collection.</span></span>

    <span data-ttu-id="85b9a-199">Cette commande crée une archive nommée **snapshot.20150806185338855.tgz**, qui contient le contenu de hello Hello **snapshot.20150806185338855** active.</span><span class="sxs-lookup"><span data-stu-id="85b9a-199">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains hello contents of hello **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="85b9a-200">Vous pouvez ensuite stocker le stockage de principal du cluster toohello hello archive à l’aide de hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="85b9a-200">You can then store hello archive toohello cluster's primary storage using hello following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="85b9a-201">Pour plus d’informations sur l’utilisation de sauvegardes et de restaurations Solr, consultez [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="85b9a-201">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="85b9a-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85b9a-202">Next steps</span></span>

* <span data-ttu-id="85b9a-203">[Installation de Giraph sur des clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="85b9a-203">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="85b9a-204">Utilisez tooinstall de personnalisation de cluster que giraph sur HDInsight Hadoop de clusters.</span><span class="sxs-lookup"><span data-stu-id="85b9a-204">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="85b9a-205">Giraph vous permet de graphique tooperform traitement à l’aide de Hadoop et peut être utilisé avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85b9a-205">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="85b9a-206">[Installer Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="85b9a-206">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="85b9a-207">Utilisez cluster personnalisation tooinstall teinte sur des clusters HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="85b9a-207">Use cluster customization tooinstall Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="85b9a-208">La teinte représente qu'un ensemble d’applications Web utilisé toointeract avec un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="85b9a-208">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
