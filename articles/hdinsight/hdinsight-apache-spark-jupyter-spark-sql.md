---
title: "Créer un cluster Apache Spark dans Azure HDInsight | Microsoft Docs"
description: "Démarrage rapide Spark HDInsight pour créer un cluster Apache Spark dans HDInsight."
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
ms.openlocfilehash: ad4330a1fc7f8de154d9aaa8df3acc2ab59b9dc1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="5dc4d-104">Créer un cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5dc4d-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="5dc4d-105">Dans cet article, vous allez découvrir comment créer un cluster Apache Spark dans Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-105">In this article, you learn how to create an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="5dc4d-106">Pour en savoir plus sur le service Spark sur HDInsight, consultez [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5dc4d-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="5dc4d-107">![Schéma de démarrage rapide décrivant la procédure de création d’un cluster Apache Spark dans Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Démarrage rapide Spark à l’aide d’Apache Spark dans HDInsight. Étapes illustrées : création d’un cluster ; exécution d’une requête interactive Spark")</span><span class="sxs-lookup"><span data-stu-id="5dc4d-107">![Quickstart diagram describing steps to create an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dc4d-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5dc4d-108">Prerequisites</span></span>

* <span data-ttu-id="5dc4d-109">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-109">**An Azure subscription**.</span></span> <span data-ttu-id="5dc4d-110">Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="5dc4d-111">Voir [Créez votre compte Azure gratuit](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="5dc4d-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="5dc4d-112">Créer un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="5dc4d-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="5dc4d-113">Dans cette section, vous créez un cluster HDInsight Spark à l’aide d’un [modèle Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="5dc4d-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="5dc4d-114">Pour obtenir d’autres méthodes de création de cluster, consultez [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5dc4d-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="5dc4d-115">Cliquez sur l’image suivante pour ouvrir le modèle dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-115">Click the following image to open the template in the Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="5dc4d-116">Saisissez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="5dc4d-116">Enter the following values:</span></span>

    <span data-ttu-id="5dc4d-117">![Créer un cluster HDInsight Spark à l’aide d’un modèle Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Créer un cluster Spark dans HDInsight à l’aide d’un modèle Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="5dc4d-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="5dc4d-118">**Abonnement** : sélectionnez votre abonnement Azure pour ce cluster.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="5dc4d-119">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez un groupe existant.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="5dc4d-120">Le groupe de ressources est utilisé pour gérer des ressources Azure pour vos projets.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-120">Resource group is used to manage Azure resources for your projects.</span></span>
    * <span data-ttu-id="5dc4d-121">**Emplacement** : sélectionnez un emplacement pour le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-121">**Location**: Select a location for the resource group.</span></span> <span data-ttu-id="5dc4d-122">Le modèle utilise cet emplacement pour créer le cluster, ainsi que pour stocker le cluster par défaut.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-122">The template uses this location for creating the cluster as well as for the default cluster storage.</span></span>
    * <span data-ttu-id="5dc4d-123">**ClusterName** : entrez un nom pour le cluster HDInsight que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-123">**ClusterName**: Enter a name for the HDInsight cluster that you want to create.</span></span>
    * <span data-ttu-id="5dc4d-124">**Version de Spark** : sélectionnez **2.0** comme version que vous souhaitez installer sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-124">**Spark version**: Select **2.0** as the version that you want to install on the cluster.</span></span>
    * <span data-ttu-id="5dc4d-125">**Nom d’utilisateur et mot de passe de cluster**: le nom de connexion par défaut est admin.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-125">**Cluster login name and password**: The default login name is admin.</span></span>
    * <span data-ttu-id="5dc4d-126">**Nom d’utilisateur et mot de passe SSH**.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="5dc4d-127">Notez ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-127">Write down these values.</span></span>  <span data-ttu-id="5dc4d-128">Vous en aurez besoin plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-128">You need them later in the tutorial.</span></span>

3. <span data-ttu-id="5dc4d-129">Sélectionnez **J’accepte les termes et conditions mentionnés ci-dessus** et **Épingler au tableau de bord**, puis cliquez sur **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-129">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="5dc4d-130">Vous pouvez voir une nouvelle vignette intitulée Envoi du déploiement pour Déploiement de modèle.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="5dc4d-131">La création du cluster prend environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-131">It takes about 20 minutes to create the cluster.</span></span>

<span data-ttu-id="5dc4d-132">Si vous rencontrez un problème avec la création de clusters HDInsight, c’est que vous n’avez peut-être pas les autorisations requises pour le faire.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have the right permissions to do so.</span></span> <span data-ttu-id="5dc4d-133">Consultez la page [À propos des noms d’espaces de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="5dc4d-134">Cet article crée un cluster Spark qui utilise des [objets Blob Azure Storage en tant que cluster de stockage](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5dc4d-134">This article creates a Spark cluster that uses [Azure Storage Blobs as the cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="5dc4d-135">Vous pouvez également créer un cluster Spark qui utilise [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) comme stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as the default storage.</span></span> <span data-ttu-id="5dc4d-136">Pour plus d’informations, voir [Créer un cluster HDInsight avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5dc4d-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="5dc4d-137">Exécuter une requête Hive à l’aide de Spark SQL</span><span class="sxs-lookup"><span data-stu-id="5dc4d-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="5dc4d-138">Lorsque vous utilisez un bloc-notes Jupyter configuré pour votre cluster HDInsight Spark, vous obtenez une présélection `sqlContext` que vous pouvez utiliser pour exécuter des requêtes Hive à l’aide de Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use to run Hive queries using Spark SQL.</span></span> <span data-ttu-id="5dc4d-139">Dans cette section, vous allez découvrir comment démarrer un bloc-notes Jupyter, puis vous allez exécuter une requête de base Hive.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-139">In this section, you learn how to start a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="5dc4d-140">Ouvrez le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5dc4d-140">Open the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="5dc4d-141">Si vous avez choisi d’épingler le cluster au tableau de bord, cliquez sur la mosaïque du cluster dans le tableau de bord pour lancer le panneau du cluster.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-141">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="5dc4d-142">Si vous n’avez pas épinglé le cluster au tableau de bord, dans le volet gauche, cliquez sur **Clusters HDInsight**, puis cliquez sur le cluster que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-142">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="5dc4d-143">À partir de **Liens rapides**, cliquez sur **Tableaux de bord de Cluster**, puis sur **Bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="5dc4d-144">Si vous y êtes invité, entrez les informations d’identification d’administrateur pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-144">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="5dc4d-145">![Ouvrir le bloc-notes Jupyter pour exécuter une requête interactive Spark SQL](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Ouvrir un bloc-notes Jupyter pour exécuter une requête interactive Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="5dc4d-145">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="5dc4d-146">Vous pouvez également accéder au bloc-notes Jupyter pour votre cluster en ouvrant l'URL suivante dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-146">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="5dc4d-147">Remplacez **CLUSTERNAME** par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-147">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="5dc4d-148">Créez un bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-148">Create a notebook.</span></span> <span data-ttu-id="5dc4d-149">Cliquez sur **Nouveau**, puis sur **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="5dc4d-150">![Créer un bloc-notes Jupyter pour exécuter une requête interactive Spark SQL](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Créer un bloc-notes Jupyter pour exécuter une requête interactive Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="5dc4d-150">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="5dc4d-151">Un nouveau bloc-notes est créé et ouvert sous le nom Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="5dc4d-151">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="5dc4d-152">Cliquez sur le nom du bloc-notes en haut, puis entrez un nom convivial si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-152">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="5dc4d-153">![Fournir un nom pour le bloc-notes Jupyter à partir duquel exécuter une requête interactive Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Fournir un nom pour le bloc-notes Jupyter à partir duquel exécuter une requête interactive Spark")</span><span class="sxs-lookup"><span data-stu-id="5dc4d-153">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5.  <span data-ttu-id="5dc4d-154">Collez l’exemple de code suivant dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE** pour exécuter le code.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-154">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="5dc4d-155">Dans le code ci-dessous, `%%sql` (appelé la commande magique sql) demande au bloc-notes Jupyter d’utiliser la présélection `sqlContext` pour exécuter la requête Hive.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-155">In the code below `%%sql` (called the sql magic) tells Jupyter notebook to use the preset `sqlContext` to run the Hive query.</span></span> <span data-ttu-id="5dc4d-156">La requête extrait les 10 premières lignes d’une table Hive (**hivesampletable**) qui est disponible par défaut sur tous les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-156">The query retrieves the top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="5dc4d-157">![Requête Hive dans HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Requête Hive dans HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="5dc4d-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="5dc4d-158">Pour plus d’informations sur la commande magique `%%sql` et les contextes de présélection, consultez [Noyaux Jupyter disponibles pour un cluster HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="5dc4d-158">For more information on the `%%sql` magic and the preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5dc4d-159">À chaque exécution d’une requête dans Jupyter, le titre de la fenêtre du navigateur web affiche l’état **(Occupé)** ainsi que le titre du bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="5dc4d-160">Un cercle plein s’affiche également en regard du texte **PySpark** dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-160">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="5dc4d-161">Une fois le travail terminé, ce cercle est remplacé par un cercle vide.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-161">After the job is completed, it changes to a hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="5dc4d-162">L’écran devrait s’actualiser pour afficher la sortie de requête.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-162">The screen should refresh to show the query output.</span></span>

    <span data-ttu-id="5dc4d-163">![Sortie de requête Hive dans HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Sortie de requête Hive dans HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="5dc4d-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="5dc4d-164">Arrêtez le bloc-notes pour libérer les ressources du cluster une fois l’exécution de l’application terminée.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-164">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="5dc4d-165">Pour ce faire, dans le menu **Fichier** du bloc-notes, cliquez sur **Fermer et arrêter**.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-165">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="5dc4d-166">Si vous envisagez d’effectuer les étapes suivantes à une date ultérieure, assurez-vous de supprimer le cluster HDInsight que vous avez créé avec cet article.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-166">If you plan to complete the next steps at a later time, make sure you delete the HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="5dc4d-167">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="5dc4d-167">Next step</span></span> 

<span data-ttu-id="5dc4d-168">Dans cet article vous avez appris à créer un cluster HDInsight Spark et à exécuter une requête de base Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-168">In this article you learned how to create an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="5dc4d-169">Passer à l’article suivant pour apprendre à utiliser un cluster HDInsight Spark pour exécuter des requêtes interactives sur des données test.</span><span class="sxs-lookup"><span data-stu-id="5dc4d-169">Advance to the next article to learn how to use an HDInsight Spark cluster to run interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="5dc4d-170">Exécuter des requêtes interactives sur un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="5dc4d-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



