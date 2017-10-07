---
title: "cluster d’aaaCreate un Apache Spark dans Azure HDInsight | Documents Microsoft"
description: "Démarrage rapide de HDInsight Spark sur comment toocreate un Apache Spark dans HDInsight de cluster."
keywords: "démarrage rapide spark,spark interactif,requête interactive,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="6b28b-104">Créer un cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b28b-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="6b28b-105">Dans cet article, vous découvrez comment toocreate un Apache Spark cluster dans Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b28b-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="6b28b-106">Pour en savoir plus sur le service Spark sur HDInsight, consultez [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b28b-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="6b28b-107">![Diagramme de démarrage rapide qui décrit les étapes toocreate un cluster Apache Spark sur Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "quickstart Spark à l’aide d’Apache Spark dans HDInsight. Étapes illustrées : création d’un cluster ; exécution d’une requête interactive Spark")</span><span class="sxs-lookup"><span data-stu-id="6b28b-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b28b-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6b28b-108">Prerequisites</span></span>

* <span data-ttu-id="6b28b-109">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="6b28b-109">**An Azure subscription**.</span></span> <span data-ttu-id="6b28b-110">Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6b28b-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="6b28b-111">Voir [Créez votre compte Azure gratuit](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="6b28b-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="6b28b-112">Créer un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="6b28b-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="6b28b-113">Dans cette section, vous créez un cluster HDInsight Spark à l’aide d’un [modèle Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="6b28b-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="6b28b-114">Pour obtenir d’autres méthodes de création de cluster, consultez [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="6b28b-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="6b28b-115">Cliquez sur hello suit image tooopen hello template Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6b28b-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="6b28b-116">Entrez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="6b28b-116">Enter hello following values:</span></span>

    <span data-ttu-id="6b28b-117">![Créer un cluster HDInsight Spark à l’aide d’un modèle Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Créer un cluster Spark dans HDInsight à l’aide d’un modèle Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="6b28b-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="6b28b-118">**Abonnement** : sélectionnez votre abonnement Azure pour ce cluster.</span><span class="sxs-lookup"><span data-stu-id="6b28b-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="6b28b-119">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez un groupe existant.</span><span class="sxs-lookup"><span data-stu-id="6b28b-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="6b28b-120">Groupe de ressources est utilisé toomanage ressources Azure pour vos projets.</span><span class="sxs-lookup"><span data-stu-id="6b28b-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="6b28b-121">**Emplacement**: sélectionnez un emplacement pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="6b28b-122">modèle de Hello utilise cet emplacement pour la création de cluster de hello ainsi que pour stockage de cluster par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="6b28b-123">**ClusterName**: entrez un nom pour le cluster HDInsight de hello que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="6b28b-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="6b28b-124">**Version de Spark**: sélectionnez **2.0** en tant que version hello que vous souhaitez tooinstall sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="6b28b-125">**Nom de connexion et mot de passe de cluster**: nom de connexion hello par défaut est Admin.</span><span class="sxs-lookup"><span data-stu-id="6b28b-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="6b28b-126">**Nom d’utilisateur et mot de passe SSH**.</span><span class="sxs-lookup"><span data-stu-id="6b28b-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="6b28b-127">Notez ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="6b28b-127">Write down these values.</span></span>  <span data-ttu-id="6b28b-128">Vous avez besoin plus tard dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="6b28b-129">Sélectionnez **J’accepte les conditions susmentionnées générales toohello**, sélectionnez **code confidentiel toodashboard**, puis cliquez sur **bon**.</span><span class="sxs-lookup"><span data-stu-id="6b28b-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="6b28b-130">Vous pouvez voir une nouvelle vignette intitulée Envoi du déploiement pour Déploiement de modèle.</span><span class="sxs-lookup"><span data-stu-id="6b28b-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="6b28b-131">Il prend le cluster de hello toocreate environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="6b28b-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="6b28b-132">Si vous rencontrez un problème avec la création de clusters HDInsight, il peut être que vous n’avez pas toodo des autorisations appropriées hello ainsi.</span><span class="sxs-lookup"><span data-stu-id="6b28b-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="6b28b-133">Consultez la page [À propos des noms d’espaces de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6b28b-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="6b28b-134">Cet article crée un cluster Spark utilise [stockage en cluster objets BLOB de stockage Azure en tant que hello](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="6b28b-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="6b28b-135">Vous pouvez également créer un cluster Spark qui utilise [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) comme stockage par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="6b28b-136">Pour plus d’informations, voir [Créer un cluster HDInsight avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6b28b-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="6b28b-137">Exécuter une requête Hive à l’aide de Spark SQL</span><span class="sxs-lookup"><span data-stu-id="6b28b-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="6b28b-138">Lorsque vous utilisez un bloc-notes jupyter configuré pour votre cluster HDInsight Spark, vous obtenez une présélection `sqlContext` que vous pouvez utiliser les requêtes Hive toorun à l’aide de Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="6b28b-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="6b28b-139">Dans cette section, vous apprendrez comment toostart un bloc-notes jupyter, puis exécutez une requête Hive base.</span><span class="sxs-lookup"><span data-stu-id="6b28b-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="6b28b-140">Ouvrez hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6b28b-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="6b28b-141">Si vous avez choisi de tableau de bord toohello toopin hello cluster, cliquez sur hello en mosaïque de cluster à partir du Panneau de cluster hello du tableau de bord toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="6b28b-142">Si vous ne pas épinglez hello cluster toohello du tableau de bord, à partir du volet de gauche hello, cliquez sur **clusters HDInsight**, puis cliquez sur cluster hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="6b28b-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="6b28b-143">À partir de **Liens rapides**, cliquez sur **Tableaux de bord de Cluster**, puis sur **Bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="6b28b-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="6b28b-144">Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="6b28b-145">![Ouvrez Notebook bloc-notes toorun interactive Spark requête SQL](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "la requête interactive Spark SQL Notebook ouvrir Bloc-notes toorun")</span><span class="sxs-lookup"><span data-stu-id="6b28b-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="6b28b-146">Vous pouvez également accéder bloc-notes jupyter de hello pour votre cluster en hello ouverture suivante d’URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="6b28b-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="6b28b-147">Remplacez **CLUSTERNAME** avec nom hello de votre cluster :</span><span class="sxs-lookup"><span data-stu-id="6b28b-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="6b28b-148">Créez un bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="6b28b-148">Create a notebook.</span></span> <span data-ttu-id="6b28b-149">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="6b28b-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="6b28b-150">![Créer une requête de Spark SQL interactive Notebook bloc-notes toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "créer une requête de Spark SQL Notebook bloc-notes toorun interactive")</span><span class="sxs-lookup"><span data-stu-id="6b28b-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="6b28b-151">Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="6b28b-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="6b28b-152">Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial, si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="6b28b-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="6b28b-153">![Fournissez un nom pour hello Jupter bloc-notes toorun Spark requêtes interactif de](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "fournir un nom pour hello Jupter bloc-notes toorun interactive Spark requête à partir de")</span><span class="sxs-lookup"><span data-stu-id="6b28b-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="6b28b-154">Suit hello de coller le code dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE** code hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="6b28b-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="6b28b-155">Dans le code hello ci-dessous `%%sql` (magique de sql appelée hello) indique hello de toouse bloc-notes Notebook présélection `sqlContext` requête Hive de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="6b28b-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="6b28b-156">requête de Hello récupère hello 10 premières lignes d’une table Hive (**hivesampletable**) qui est disponible par défaut sur tous les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b28b-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="6b28b-157">![Requête Hive dans HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Requête Hive dans HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="6b28b-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="6b28b-158">Pour plus d’informations sur hello `%%sql` magique et hello présélection des contextes, consultez [noyaux Notebook disponibles pour un cluster HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="6b28b-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b28b-159">Chaque fois que vous exécutez une requête dans le bloc-notes, le titre de la fenêtre de navigateur web affiche un **(occupé)** état, ainsi que le titre du bloc-notes hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="6b28b-160">Vous voyez également un toohello suivant cercle plein **PySpark** texte dans l’angle supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="6b28b-161">Une fois le travail de hello est terminé, il modifie tooa les cercle vide.</span><span class="sxs-lookup"><span data-stu-id="6b28b-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="6b28b-162">écran Hello doit actualiser le résultat de la requête tooshow hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="6b28b-163">![Sortie de requête Hive dans HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Sortie de requête Hive dans HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="6b28b-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="6b28b-164">Arrêt des ressources de cluster hello hello bloc-notes toorelease une fois que vous avez terminé d’exécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6b28b-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="6b28b-165">toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**.</span><span class="sxs-lookup"><span data-stu-id="6b28b-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="6b28b-166">Si vous envisagez d’étapes de hello toocomplete à une date ultérieure, assurez-vous que vous supprimez le cluster HDInsight de hello que vous avez créé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6b28b-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="6b28b-167">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="6b28b-167">Next step</span></span> 

<span data-ttu-id="6b28b-168">Dans cet article, vous avez appris comment toocreate un HDInsight Spark cluster et exécutez une base Spark SQL de requête.</span><span class="sxs-lookup"><span data-stu-id="6b28b-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="6b28b-169">Avance toohello toolearn de l’article suivant comment toouse un HDInsight Spark cluster toorun des requêtes interactives sur les exemples de données.</span><span class="sxs-lookup"><span data-stu-id="6b28b-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="6b28b-170">Exécuter des requêtes interactives sur un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="6b28b-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



