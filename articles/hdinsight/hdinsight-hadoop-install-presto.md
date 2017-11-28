---
title: les clusters Presto sur Azure HDInsight Linux aaaInstall | Documents Microsoft
description: "Découvrez comment tooinstall Presto et Airpal sur basés sur Linux HDInsight Hadoop les clusters à l’aide des Actions de Script."
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
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="aeb7e-103">Installer et utiliser Presto sur des clusters Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="aeb7e-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="aeb7e-104">Dans cette rubrique, vous découvrez comment tooinstall Presto sur HDInsight Hadoop clusters en utilisant l’Action de Script.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="aeb7e-105">Vous apprendrez également comment tooinstall Airpal sur un cluster HDInsight appliqués aux existant.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aeb7e-106">Hello étapes décrites dans ce document nécessitent une **cluster HDInsight 3.5 Hadoop** qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="aeb7e-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aeb7e-108">Pour plus d’informations, consultez la page [Versions de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="aeb7e-109">Qu’est-ce que Presto ?</span><span class="sxs-lookup"><span data-stu-id="aeb7e-109">What is Presto?</span></span>
<span data-ttu-id="aeb7e-110">[Presto](https://prestodb.io/overview.html) est un moteur de requête SQL rapide distribué pour les Big Data.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="aeb7e-111">Presto convient à l’exécution interactive de requêtes de pétaoctets de données.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="aeb7e-112">Pour plus d’informations sur les composants de hello Presto et comment ils fonctionnent ensemble, consultez [concepts Presto](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="aeb7e-113">Les composants fournis avec le cluster HDInsight de hello sont entièrement gérés et permet de tooisolate et résoudre les problèmes connexes toothese composants de Support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="aeb7e-114">Les composants personnalisés, tels que Presto, réception efforcera toohelp vous toofurther hello de dépannage.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="aeb7e-115">Cela peut entraîner hello de résoudre ou demandant que vous tooengage les canaux disponibles pour hello ouvrir technologies source où se trouve une grande expérience pour cette technologie.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="aeb7e-116">Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="aeb7e-117">Installer Presto à l’aide d’une action de script</span><span class="sxs-lookup"><span data-stu-id="aeb7e-117">Install Presto using script action</span></span>

<span data-ttu-id="aeb7e-118">Cette section explique comment toouse hello exemple de script lors de la création d’un nouveau cluster à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="aeb7e-119">Démarrer l’approvisionnement d’un cluster à l’aide des étapes hello dans [clusters basés sur Linux de fourniture de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="aeb7e-120">Vérifiez que vous créez le cluster hello à l’aide de hello **personnalisé** flux de création de cluster.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="aeb7e-121">Vous devez vous assurer que vous créez le cluster hello répond aux hello suivant les exigences.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="aeb7e-122">a.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-122">a.</span></span> <span data-ttu-id="aeb7e-123">Ce doit être un cluster Hadoop créé avec la version 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="aeb7e-124">b.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-124">b.</span></span> <span data-ttu-id="aeb7e-125">Elle doit utiliser le stockage Azure en tant que banque de données hello.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="aeb7e-126">À l’aide de tour sur un cluster qui utilise Azure Data Lake Store comme option de stockage hello n’est pas encore pris en charge.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![Créer un cluster HDInsight à l’aide d’options personnalisées](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="aeb7e-128">Sur hello **paramètres avancés** panneau, sélectionnez **Actions de Script**et fournissent des informations de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="aeb7e-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="aeb7e-129">**NOM**: entrez un nom convivial pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="aeb7e-130">**URI de script bash** : `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="aeb7e-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="aeb7e-131">**HEAD**: cochez cette option.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="aeb7e-132">**WORKER** : cochez cette option</span><span class="sxs-lookup"><span data-stu-id="aeb7e-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="aeb7e-133">**ZOOKEEPER** : décochez cette case</span><span class="sxs-lookup"><span data-stu-id="aeb7e-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="aeb7e-134">**PARAMETERS**: laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="aeb7e-135">En bas de hello Hello **Actions de Script** panneau, cliquez sur hello **sélectionnez** configuration hello toosave du bouton.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="aeb7e-136">Enfin, cliquez sur hello **sélectionnez** bouton bas hello hello **paramètres avancés** informations de configuration de panneau toosave hello.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="aeb7e-137">Continuer la mise en service de cluster de hello comme décrit dans [clusters basés sur Linux de fourniture de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="aeb7e-138">Azure PowerShell, hello CLI d’Azure, hello HDInsight .NET SDK ou modèles Azure Resource Manager peuvent également être utilisés tooapply les actions de script.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="aeb7e-139">Vous pouvez également appliquer tooalready d’actions de script clusters en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="aeb7e-140">Pour plus d’informations, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="aeb7e-141">Utiliser Presto avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="aeb7e-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="aeb7e-142">Effectuer hello suivant les étapes toouse Presto dans un cluster HDInsight après avoir installé à l’aide des étapes hello décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="aeb7e-143">Connecter le cluster HDInsight de toohello à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="aeb7e-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="aeb7e-144">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="aeb7e-145">Démarrer l’interpréteur de commandes Presto hello à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="aeb7e-146">Exécutez une requête sur un exemple de table, comme **hivesampletable**, disponible sur tous les clusters HDInsight par défaut.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="aeb7e-147">Par défaut, les connecteurs [Hive](https://prestodb.io/docs/current/connector/hive.html) et [TPCH](https://prestodb.io/docs/current/connector/tpch.html) pour Presto sont déjà configurés.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="aeb7e-148">Connecteur de la ruche étant toouse configuré hello-installation ruche par défaut, toutes les tables hello à partir de la ruche seront automatiquement visibles dans Presto.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="aeb7e-149">Pour obtenir une description détaillée de la manière d’utiliser Presto, consultez la [documentation Presto](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="aeb7e-150">Utiliser Airpal avec Presto</span><span class="sxs-lookup"><span data-stu-id="aeb7e-150">Use Airpal with Presto</span></span>

<span data-ttu-id="aeb7e-151">[Airpal](https://github.com/airbnb/airpal#airpal) est une interface de requête web open source pour Presto.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="aeb7e-152">Pour plus d’informations sur Airpal, consultez la [documentation Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="aeb7e-153">Dans cette section, nous abordons les étapes hello trop**installer Airpal sur hello edgenode** d’un cluster HDInsight Hadoop, qui possède déjà Presto installé.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="aeb7e-154">Cela garantit que l’interface de requête web qui Airpal hello est disponible via hello Internet.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="aeb7e-155">À l’aide de SSH, se connecter à nœud de toohello principal du cluster HDInsight hello qui a installé appliqués aux :</span><span class="sxs-lookup"><span data-stu-id="aeb7e-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="aeb7e-156">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="aeb7e-157">Une fois que vous êtes connecté, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="aeb7e-158">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="aeb7e-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="aeb7e-159">À partir de la sortie de hello, notez la valeur hello hello **valeur** propriété.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="aeb7e-160">Vous en aurez besoin lors de l’installation Airpal sur hello cluster edgenode.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="aeb7e-161">À partir de la sortie de hello ci-dessus, la valeur hello dont vous avez besoin est **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="aeb7e-162">Utiliser un modèle hello  **[ici](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate un HDInsight edgenode de cluster et fournir des valeurs de hello comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![HDInsight installe Airpal sur un cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="aeb7e-164">Cliquez sur **Achat**.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="aeb7e-165">Une fois les modifications de hello appliqué toohello configuration du cluster, vous pouvez accéder à l’interface web hello Airpal à l’aide de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="aeb7e-166">a.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-166">a.</span></span> <span data-ttu-id="aeb7e-167">Dans le panneau de cluster hello, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-167">From hello cluster blade, click **Applications**.</span></span>

    ![HDInsight lance Airpal sur un cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="aeb7e-169">b.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-169">b.</span></span> <span data-ttu-id="aeb7e-170">À partir de hello **installé des applications** panneau, cliquez sur **Portal** contre airpal.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![HDInsight lance Airpal sur un cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="aeb7e-172">c.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-172">c.</span></span> <span data-ttu-id="aeb7e-173">Lorsque vous y êtes invité, entrez des informations d’identification d’admin hello que vous avez spécifié lors de la création du cluster HDInsight Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="aeb7e-174">Personnaliser une installation Presto sur un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="aeb7e-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="aeb7e-175">Une fois que vous avez installé Presto sur un cluster HDInsight Hadoop, vous pouvez personnaliser hello installation toomake modifications telles que les paramètres de mémoire mise à jour, modifier les connecteurs, etc.. Hello suivant les étapes toodo donc d’effectuer.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="aeb7e-176">À l’aide de SSH, se connecter à nœud de toohello principal du cluster HDInsight hello qui a installé appliqués aux :</span><span class="sxs-lookup"><span data-stu-id="aeb7e-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="aeb7e-177">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="aeb7e-178">Apportez les modifications de configuration dans le fichier de hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="aeb7e-179">Pour en savoir plus sur la configuration de Presto, consultez la page [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html) (Configuration de Presto pour des clusters sous Yarn).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="aeb7e-180">Arrêter et supprimer l’instance en cours d’exécution en cours de hello de Presto.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="aeb7e-181">Démarrer une nouvelle instance de Presto avec une personnalisation hello.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="aeb7e-182">Attendez que toobe instance hello nouveau prêt et notez l’adresse du coordinateur presto.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="aeb7e-183">Générer des données de point de référence pour les clusters HDInsight qui exécutent Presto</span><span class="sxs-lookup"><span data-stu-id="aeb7e-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="aeb7e-184">TPC-DS est hello standard pour mesurer les performances de hello de nombreux systèmes de prise en charge de décision, y compris les systèmes de données volumineuses.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="aeb7e-185">Vous pouvez utiliser appliqués aux données de toogenerate clusters HDInsight et évaluer le compare avec vos propres données de test d’évaluation de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="aeb7e-186">Vous pourrez trouver plus d’informations [ici](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="aeb7e-187">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="aeb7e-187">See also</span></span>
* <span data-ttu-id="aeb7e-188">[Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="aeb7e-189">La teinte représente une interface utilisateur web qui permet de facilement toocreate, exécuter et enregistrer des travaux Pig et Hive, également en tant que parcourir du stockage par défaut pour votre cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="aeb7e-190">[Installation de Giraph sur des clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="aeb7e-191">Utilisez tooinstall de personnalisation de cluster que giraph sur HDInsight Hadoop de clusters.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="aeb7e-192">Giraph vous permet de graphique tooperform traitement à l’aide de Hadoop et peut être utilisé avec Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="aeb7e-193">[Installation de Solr sur des clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aeb7e-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="aeb7e-194">Utilisez tooinstall de personnalisation de cluster que solr sur HDInsight Hadoop de clusters.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="aeb7e-195">Solr vous permet de tooperform les opérations de recherche puissante sur les données stockées.</span><span class="sxs-lookup"><span data-stu-id="aeb7e-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
