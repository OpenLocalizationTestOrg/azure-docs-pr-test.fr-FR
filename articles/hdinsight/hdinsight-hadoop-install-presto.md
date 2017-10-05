---
title: "Installer Presto sur des clusters Azure HDInsight Linux | Documents Microsoft"
description: "Apprenez à installer Presto et Airpal sur des clusters Hadoop HDInsight sous Linux, à l’aide des actions de script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 406ef84e72d253fec51a0b37c48f326dafd511b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="803eb-103">Installer et utiliser Presto sur des clusters Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="803eb-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="803eb-104">Dans cette rubrique, vous allez apprendre à installer Presto sur des clusters Hadoop HDInsight à l’aide des actions de script.</span><span class="sxs-lookup"><span data-stu-id="803eb-104">In this topic, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="803eb-105">Vous allez également apprendre à installer Airpal sur un cluster HDInsight Presto existant.</span><span class="sxs-lookup"><span data-stu-id="803eb-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="803eb-106">Les étapes décrites dans ce document nécessitent un **cluster Hadoop HDInsight version 3.5** qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="803eb-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="803eb-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="803eb-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="803eb-108">Pour plus d’informations, consultez la page [Versions de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="803eb-109">Qu’est-ce que Presto ?</span><span class="sxs-lookup"><span data-stu-id="803eb-109">What is Presto?</span></span>
<span data-ttu-id="803eb-110">[Presto](https://prestodb.io/overview.html) est un moteur de requête SQL rapide distribué pour les Big Data.</span><span class="sxs-lookup"><span data-stu-id="803eb-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="803eb-111">Presto convient à l’exécution interactive de requêtes de pétaoctets de données.</span><span class="sxs-lookup"><span data-stu-id="803eb-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="803eb-112">Pour plus d’informations sur les composants de Presto et leur manière de fonctionner ensemble, consultez la page [Concepts Presto](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="803eb-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="803eb-113">Les composants fournis avec le cluster HDInsight bénéficient d’une prise en charge totale, et le support Microsoft vous aidera à identifier et à résoudre les problèmes liés à ces composants.</span><span class="sxs-lookup"><span data-stu-id="803eb-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
> 
> <span data-ttu-id="803eb-114">Les composants personnalisés, tels que Presto, bénéficient d'un support commercialement raisonnable pour vous aider à résoudre le problème de manière plus approfondie.</span><span class="sxs-lookup"><span data-stu-id="803eb-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="803eb-115">Cela signifie SOIT que le problème pourra être résolu, SOIT que vous serez invité à affecter les ressources disponibles pour les technologies Open Source.</span><span class="sxs-lookup"><span data-stu-id="803eb-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="803eb-116">Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="803eb-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="803eb-117">En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="803eb-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="803eb-118">Installer Presto à l’aide d’une action de script</span><span class="sxs-lookup"><span data-stu-id="803eb-118">Install Presto using script action</span></span>

<span data-ttu-id="803eb-119">Cette section explique comment utiliser l’exemple de script dans le cadre de la création d’un cluster à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="803eb-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span></span> 

1. <span data-ttu-id="803eb-120">Commencez à approvisionner un cluster en suivant la procédure décrite sur la page [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) (Approvisionner des clusters HDInsight sous Linux).</span><span class="sxs-lookup"><span data-stu-id="803eb-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="803eb-121">Veillez à créer le cluster à l’aide du flux de création de cluster **personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="803eb-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span></span> <span data-ttu-id="803eb-122">Vous devez vous assurer que le cluster que vous créez remplit les conditions suivantes.</span><span class="sxs-lookup"><span data-stu-id="803eb-122">You must ensure that the cluster you create meets the following requirements.</span></span>

    <span data-ttu-id="803eb-123">a.</span><span class="sxs-lookup"><span data-stu-id="803eb-123">a.</span></span> <span data-ttu-id="803eb-124">Ce doit être un cluster Hadoop créé avec la version 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="803eb-124">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="803eb-125">b.</span><span class="sxs-lookup"><span data-stu-id="803eb-125">b.</span></span> <span data-ttu-id="803eb-126">Il doit utiliser Stockage Azure comme banque de données.</span><span class="sxs-lookup"><span data-stu-id="803eb-126">It must use Azure Storage as the data store.</span></span> <span data-ttu-id="803eb-127">Il n’est pas encore possible d’utiliser Presto sur un cluster qui utilise Azure Data Lake Store comme option de stockage.</span><span class="sxs-lookup"><span data-stu-id="803eb-127">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span></span> 

    ![Créer un cluster HDInsight à l’aide d’options personnalisées](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="803eb-129">Dans le panneau **Paramètres avancés**, sélectionnez **Actions de script**, puis indiquez les informations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="803eb-129">On the **Advanced settings** blade, select **Script Actions**, and provide the information below:</span></span>
   
   * <span data-ttu-id="803eb-130">**NAME**: saisissez un nom convivial pour l’action de script.</span><span class="sxs-lookup"><span data-stu-id="803eb-130">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="803eb-131">**URI de script bash** : `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="803eb-131">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="803eb-132">**HEAD**: cochez cette option.</span><span class="sxs-lookup"><span data-stu-id="803eb-132">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="803eb-133">**WORKER** : cochez cette option</span><span class="sxs-lookup"><span data-stu-id="803eb-133">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="803eb-134">**ZOOKEEPER** : décochez cette case</span><span class="sxs-lookup"><span data-stu-id="803eb-134">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="803eb-135">**PARAMETERS**: laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="803eb-135">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="803eb-136">En bas du panneau **Actions de script**, cliquez sur le bouton **Sélectionner** pour enregistrer la configuration.</span><span class="sxs-lookup"><span data-stu-id="803eb-136">At the bottom of the **Script Actions** blade, click the **Select** button to save the configuration.</span></span> <span data-ttu-id="803eb-137">Pour terminer, cliquez sur le bouton **Sélectionner** au bas du panneau **Paramètres personnalisés** afin d’enregistrer les informations de configuration.</span><span class="sxs-lookup"><span data-stu-id="803eb-137">Finally, click  the **Select** button at the bottom of the **Advanced Settings** blade to save the configuration information.</span></span>

4. <span data-ttu-id="803eb-138">Continuez l’approvisionnement du cluster, comme décrit dans la section [Approvisionner des clusters HDInsight sous Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-138">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="803eb-139">Azure PowerShell, l'interface de ligne de commande Azure (CLI), le Kit de développement logiciel (SDK) .NET HDInsight ou les modèles Azure Resource Manager peuvent également être utilisés pour appliquer des actions de script.</span><span class="sxs-lookup"><span data-stu-id="803eb-139">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="803eb-140">Vous pouvez également appliquer les actions de script aux clusters qui sont déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="803eb-140">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="803eb-141">Pour plus d’informations, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-141">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="803eb-142">Utiliser Presto avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="803eb-142">Use Presto with HDInsight</span></span>

<span data-ttu-id="803eb-143">Réalisez les étapes suivantes afin d’utiliser Presto dans un cluster HDInsight, après l’avoir installé grâce aux étapes décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="803eb-143">Perform the following steps to use Presto in an HDInsight cluster after you have installed it using the steps described above.</span></span>

1. <span data-ttu-id="803eb-144">Connectez-vous au cluster HDInsight à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="803eb-144">Connect to the HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="803eb-145">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="803eb-146">Démarrez l’interface Presto à l’aide de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="803eb-146">Start the Presto shell using the following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="803eb-147">Exécutez une requête sur un exemple de table, comme **hivesampletable**, disponible sur tous les clusters HDInsight par défaut.</span><span class="sxs-lookup"><span data-stu-id="803eb-147">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="803eb-148">Par défaut, les connecteurs [Hive](https://prestodb.io/docs/current/connector/hive.html) et [TPCH](https://prestodb.io/docs/current/connector/tpch.html) pour Presto sont déjà configurés.</span><span class="sxs-lookup"><span data-stu-id="803eb-148">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="803eb-149">Le connecteur Hive est configuré pour utiliser l’installation Hive qui est installée par défaut. De ce fait, toutes les tables venant de Hive seront automatiquement visibles dans Presto.</span><span class="sxs-lookup"><span data-stu-id="803eb-149">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="803eb-150">Pour obtenir une description détaillée de la manière d’utiliser Presto, consultez la [documentation Presto](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="803eb-150">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="803eb-151">Utiliser Airpal avec Presto</span><span class="sxs-lookup"><span data-stu-id="803eb-151">Use Airpal with Presto</span></span>

<span data-ttu-id="803eb-152">[Airpal](https://github.com/airbnb/airpal#airpal) est une interface de requête web open source pour Presto.</span><span class="sxs-lookup"><span data-stu-id="803eb-152">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="803eb-153">Pour plus d’informations sur Airpal, consultez la [documentation Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="803eb-153">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="803eb-154">Dans cette section, nous allons examiner la procédure **d’installation de Airpal sur le nœud de périmètre** d’un cluster Hadoop HDInsight, sur lequel Presto est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="803eb-154">In this section, we look at the steps to **install Airpal on the edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="803eb-155">Cela garantit que l’interface de requête web Airpal est disponible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="803eb-155">This ensures that the Airpal web query interface is available over the Internet.</span></span>

1. <span data-ttu-id="803eb-156">À l’aide de SSH, connectez-vous au nœud principal du cluster HDInsight, sur lequel Presto est déjà installé :</span><span class="sxs-lookup"><span data-stu-id="803eb-156">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="803eb-157">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-157">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="803eb-158">Une fois que vous êtes connecté, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="803eb-158">Once you are connected, run the following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="803eb-159">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="803eb-159">You should see an output like the following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="803eb-160">À partir de la sortie, notez la valeur pour la propriété de **valeur**.</span><span class="sxs-lookup"><span data-stu-id="803eb-160">From the output, note the value for the **value** property.</span></span> <span data-ttu-id="803eb-161">Elle vous sera nécessaire lors de l’installation de Airpal sur le nœud de périmètre du cluster.</span><span class="sxs-lookup"><span data-stu-id="803eb-161">You will need this while installing Airpal on the cluster edgenode.</span></span> <span data-ttu-id="803eb-162">À partir de la sortie ci-dessus, vous aurez besoin de la valeur **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="803eb-162">From the output above, the value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="803eb-163">Utilisez le modèle  **[ici](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  pour créer un nœud de périmètre du cluster HDInsight et fournir les valeurs telles qu’elles sont indiquées dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="803eb-163">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span></span>

    ![HDInsight installe Airpal sur un cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="803eb-165">Cliquez sur **Achat**.</span><span class="sxs-lookup"><span data-stu-id="803eb-165">Click **Purchase**.</span></span>

6. <span data-ttu-id="803eb-166">Une fois que les modifications sont appliquées à la configuration du cluster, vous pouvez accéder à l’interface web de Airpal en réalisant les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="803eb-166">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span></span>

    <span data-ttu-id="803eb-167">a.</span><span class="sxs-lookup"><span data-stu-id="803eb-167">a.</span></span> <span data-ttu-id="803eb-168">À partir du panneau du cluster, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="803eb-168">From the cluster blade, click **Applications**.</span></span>

    ![HDInsight lance Airpal sur un cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="803eb-170">b.</span><span class="sxs-lookup"><span data-stu-id="803eb-170">b.</span></span> <span data-ttu-id="803eb-171">À partir du panneau **Applications installées**, cliquez sur **Portail**, situé à l’opposé de airpal.</span><span class="sxs-lookup"><span data-stu-id="803eb-171">From the **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![HDInsight lance Airpal sur un cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="803eb-173">c.</span><span class="sxs-lookup"><span data-stu-id="803eb-173">c.</span></span> <span data-ttu-id="803eb-174">Lorsque vous y êtes invité, entrez les informations d’identification d’administrateur que vous avez spécifié lors de la création du cluster Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="803eb-174">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="803eb-175">Personnaliser une installation Presto sur un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="803eb-175">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="803eb-176">Lorsque Presto est installé sur un cluster Hadoop HDInsight, vous avez la possibilité de personnaliser l’installation pour effectuer des changements, comme mettre à jour les paramètres de mémoire, modifier les connecteurs, etc. Pour ce faire, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="803eb-176">After you have installed Presto on an HDInsight Hadoop cluster, you can customize the installation to make changes such as update memory settings, change connectors, etc. Perform the following steps to do so.</span></span>

1. <span data-ttu-id="803eb-177">À l’aide de SSH, connectez-vous au nœud principal du cluster HDInsight, sur lequel Presto est déjà installé :</span><span class="sxs-lookup"><span data-stu-id="803eb-177">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="803eb-178">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-178">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="803eb-179">Apportez vos modifications de configuration dans le fichier `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="803eb-179">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="803eb-180">Pour en savoir plus sur la configuration de Presto, consultez la page [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html) (Configuration de Presto pour des clusters sous Yarn).</span><span class="sxs-lookup"><span data-stu-id="803eb-180">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="803eb-181">Arrêter et supprimer l’instance de Presto en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="803eb-181">Stop and kill the current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="803eb-182">Démarrer une nouvelle instance de Presto grâce à la personnalisation.</span><span class="sxs-lookup"><span data-stu-id="803eb-182">Start a new instance of Presto with the customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="803eb-183">Attendez que la nouvelle instance soit prête et notez l’adresse du coordinateur Presto.</span><span class="sxs-lookup"><span data-stu-id="803eb-183">Wait for the new instance to be ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="803eb-184">Générer des données de point de référence pour les clusters HDInsight qui exécutent Presto</span><span class="sxs-lookup"><span data-stu-id="803eb-184">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="803eb-185">Les normes industrielles TPC-DS mesure la performance de nombreux systèmes de support de décision, incluant les systèmes de Big Data.</span><span class="sxs-lookup"><span data-stu-id="803eb-185">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="803eb-186">Vous pouvez utiliser Presto sur des clusters HDInsight afin de générer des données et d’évaluer la manière dont elles se comparent avec vos propres données de point de référence HDInsight.</span><span class="sxs-lookup"><span data-stu-id="803eb-186">You can use Presto on HDInsight clusters to generate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="803eb-187">Vous pourrez trouver plus d’informations [ici](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-187">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="803eb-188">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="803eb-188">See also</span></span>
* <span data-ttu-id="803eb-189">[Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-189">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="803eb-190">Hue est une interface utilisateur web qui permet de facilement créer, exécuter et enregistrer des tâches Pig et Hive, ainsi que de parcourir le stockage par défaut pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="803eb-190">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="803eb-191">[Installation de Giraph sur des clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-191">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="803eb-192">Utilisez la personnalisation de clusters pour installer Giraph sur des clusters HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="803eb-192">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="803eb-193">Giraph permet de traiter des graphiques à l’aide de Hadoop et peut être utilisé avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="803eb-193">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="803eb-194">[Installation de Solr sur des clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="803eb-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="803eb-195">Utilisez la personnalisation de clusters pour installer Solr sur des clusters HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="803eb-195">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="803eb-196">Solr vous permet d’effectuer de puissantes opérations de recherche sur des données stockées.</span><span class="sxs-lookup"><span data-stu-id="803eb-196">Solr allows you to perform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
