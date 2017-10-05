---
title: "Créer des tables Hive et charger des données à partir de Stockage Blob Azure | Microsoft Docs"
description: "Créer des tables Hive et charger des données d’un blob dans des tables Hive"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: eca4ecd8f639bb9816903f4b1d1f999755da819c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="553ad-103">Créer des tables Hive et charger des données à partir de Stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="553ad-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="553ad-104">Cette rubrique présente des requêtes Hive génériques qui créent des tables Hive et chargent des données à partir d’un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="553ad-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="553ad-105">Il donne également quelques conseils sur le partitionnement des tables Hive et sur l’utilisation du format ORC (Optimized Row Columnar) pour améliorer les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="553ad-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="553ad-106">Ce **menu** pointe vers des rubriques qui expliquent comment recevoir des données dans d’autres environnements cibles où les données peuvent être stockées et traitées pendant le processus TDSP (Team Data Science Process).</span><span class="sxs-lookup"><span data-stu-id="553ad-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="553ad-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="553ad-107">Prerequisites</span></span>
<span data-ttu-id="553ad-108">Cet article suppose que vous avez :</span><span class="sxs-lookup"><span data-stu-id="553ad-108">This article assumes that you have:</span></span>

* <span data-ttu-id="553ad-109">Créé un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="553ad-109">Created an Azure storage account.</span></span> <span data-ttu-id="553ad-110">Pour obtenir des instructions, voir [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="553ad-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="553ad-111">Approvisionné un cluster Hadoop personnalisé avec le service HDInsight.</span><span class="sxs-lookup"><span data-stu-id="553ad-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="553ad-112">Si vous avez besoin d'aide, consultez [Personnaliser des clusters Hadoop Azure HDInsight pour l'analyse avancée](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="553ad-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="553ad-113">Activé l’accès à distance au cluster, saisi les identifiants appropriés et ouvert la console de ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="553ad-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="553ad-114">Si vous avez besoin d'aide, consultez [Accéder au nœud principal du cluster Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="553ad-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="553ad-115">Téléchargement de données vers le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="553ad-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="553ad-116">Si vous avez créé une machine virtuelle Azure en suivant les instructions de l’article [Configurer une machine virtuelle Azure pour l’analyse avancée](machine-learning-data-science-setup-virtual-machine.md), ce fichier de script doit avoir été téléchargé dans le répertoire *C:\\Utilisateurs\\\<nom_utilisateur\>\\Documents\\Data Science Scripts* de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="553ad-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="553ad-117">Pour pouvoir être envoyées, ces requêtes Hive nécessitent simplement que votre schéma de données et la configuration de votre stockage Azure Blob soient déclarés dans les champs appropriés.</span><span class="sxs-lookup"><span data-stu-id="553ad-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="553ad-118">Nous partons du principe que les données des tables Hive ont un format tabulaire **non compressé** et qu’elles ont été chargées dans le conteneur par défaut (ou un conteneur supplémentaire) du compte de stockage utilisé par le cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="553ad-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="553ad-119">Si vous souhaitez vous exercer avec l’exemple **NYC Taxi Trip Data**, vous devez :</span><span class="sxs-lookup"><span data-stu-id="553ad-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="553ad-120">**télécharger** les 24 fichiers [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) (12 fichiers Trip et 12 fichiers Fare),</span><span class="sxs-lookup"><span data-stu-id="553ad-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="553ad-121">**décompresser** tous les fichiers en fichiers .csv, puis</span><span class="sxs-lookup"><span data-stu-id="553ad-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="553ad-122">**télécharger** vers le conteneur par défaut (ou conteneur approprié) du compte de stockage Azure créé par la procédure décrite dans la rubrique [Personnaliser des clusters Azure HDInsight Hadoop pour le processus d’analyse avancé et la technologie](machine-learning-data-science-customize-hadoop-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="553ad-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="553ad-123">Pour découvrir le processus qui vous permet de télécharger les fichiers .csv du conteneur par défaut sur le compte de stockage, consultez cette [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="553ad-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="553ad-124"><a name="submit"></a>Envoi de requêtes Hive</span><span class="sxs-lookup"><span data-stu-id="553ad-124"><a name="submit"></a>How to submit Hive queries</span></span>
<span data-ttu-id="553ad-125">Pour envoyer des requêtes Hive, utilisez au choix :</span><span class="sxs-lookup"><span data-stu-id="553ad-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="553ad-126">Envoyer des requêtes Hive avec la ligne de commande Hadoop dans le nœud principal du cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="553ad-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="553ad-127">Envoyer des requêtes Hive avec l'éditeur Hive</span><span class="sxs-lookup"><span data-stu-id="553ad-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="553ad-128">Envoyer des requêtes Hive avec les commandes Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="553ad-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="553ad-129">Des requêtes Hive sont similaires à SQL.</span><span class="sxs-lookup"><span data-stu-id="553ad-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="553ad-130">Si vous maîtrisez SQL, l’ [aide-mémoire Hive pour utilisateurs SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) peut vous être utile.</span><span class="sxs-lookup"><span data-stu-id="553ad-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="553ad-131">Lors de l’envoi d’une requête Hive, vous pouvez également contrôler la destination de sa sortie : écran, fichier local sur le nœud principal ou blob Azure.</span><span class="sxs-lookup"><span data-stu-id="553ad-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <span data-ttu-id="553ad-132"><a name="headnode"></a> 1. Envoyer des requêtes Hive avec la ligne de commande Hadoop dans le nœud principal du cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="553ad-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="553ad-133">Une requête Hive complexe envoyée directement au nœud principal du cluster Hadoop est traitée plus rapidement qu'avec un éditeur Hive ou des scripts Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="553ad-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="553ad-134">Connectez-vous au nœud principal du cluster Hadoop, ouvrez la ligne de commande Hadoop sur le bureau du nœud principal et saisissez la commande `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="553ad-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="553ad-135">Vous disposez de trois possibilités pour envoyer des requêtes Hive dans la ligne de commande Hadoop :</span><span class="sxs-lookup"><span data-stu-id="553ad-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="553ad-136">directement ;</span><span class="sxs-lookup"><span data-stu-id="553ad-136">directly</span></span>
* <span data-ttu-id="553ad-137">à l’aide de fichiers HQL ;</span><span class="sxs-lookup"><span data-stu-id="553ad-137">using .hql files</span></span>
* <span data-ttu-id="553ad-138">à l’aide de la console de commande Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="553ad-139">Envoyer directement des requêtes Hive dans la ligne de commande Hadoop</span><span class="sxs-lookup"><span data-stu-id="553ad-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="553ad-140">Vous pouvez exécuter une commande du type `hive -e "<your hive query>;` pour envoyer une requête Hive simple directement dans la ligne de commande Hadoop.</span><span class="sxs-lookup"><span data-stu-id="553ad-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="553ad-141">Voici un exemple, où l’encadré rouge indique la commande qui envoie la requête Hive et l’encadré vert, la sortie de la requête Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="553ad-143">Envoyer des requêtes Hive dans des fichiers HQL</span><span class="sxs-lookup"><span data-stu-id="553ad-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="553ad-144">Lorsque la requête Hive est plus complexe et comporte plusieurs lignes, la modifier dans la ligne de commande ou la console de commande Hive n’est pas simple.</span><span class="sxs-lookup"><span data-stu-id="553ad-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="553ad-145">L’alternative consiste à utiliser un éditeur de texte dans le nœud principal du cluster Hadoop pour enregistrer la requête Hive dans un fichier HQL situé dans le répertoire local du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="553ad-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="553ad-146">Ensuite, celle-ci peut être envoyée à l'aide de l'argument `-f` , comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="553ad-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![Create workspace](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="553ad-148">**Supprimer l’affichage de l’état d’avancement des requêtes Hive**</span><span class="sxs-lookup"><span data-stu-id="553ad-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="553ad-149">Par défaut, après l’envoi d’une requête Hive dans la ligne de commande Hadoop, l’état d’avancement de la tâche Map/Reduce s’affiche à l’écran.</span><span class="sxs-lookup"><span data-stu-id="553ad-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="553ad-150">Pour supprimer cet affichage, déclarez l'argument `-S` (« S » en majuscule) dans la ligne de commande, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="553ad-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
<span data-ttu-id="553ad-151">.</span><span class="sxs-lookup"><span data-stu-id="553ad-151">.</span></span>    <span data-ttu-id="553ad-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="553ad-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="553ad-153">Envoyer des requêtes Hive dans la console de commande Hive</span><span class="sxs-lookup"><span data-stu-id="553ad-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="553ad-154">Vous pouvez également ouvrir la console de commande Hive en exécutant la commande `hive` dans la ligne de commande Hadoop, puis envoyer les requêtes Hive dans la console de commande Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-154">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="553ad-155">Voici un exemple.</span><span class="sxs-lookup"><span data-stu-id="553ad-155">Here is an example.</span></span> <span data-ttu-id="553ad-156">Ici, les deux encadrés rouges indiquent les commandes utilisées pour ouvrir la console de commande Hive et envoyer la requête Hive dans cette console.</span><span class="sxs-lookup"><span data-stu-id="553ad-156">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="553ad-157">L’encadré vert montre la sortie de la requête Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-157">The green box highlights the output from the Hive query.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="553ad-159">Les exemples précédents affichent directement les résultats de la requête à l’écran.</span><span class="sxs-lookup"><span data-stu-id="553ad-159">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="553ad-160">Vous pouvez également consigner la sortie dans un fichier local sur le nœud principal ou dans un blob Azure.</span><span class="sxs-lookup"><span data-stu-id="553ad-160">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="553ad-161">Puis, vous pouvez utiliser d’autres outils pour analyser plus finement la sortie de la requête Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-161">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="553ad-162">**Enregistrer les résultats d’une requête Hive dans un fichier local**</span><span class="sxs-lookup"><span data-stu-id="553ad-162">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="553ad-163">Pour enregistrer les résultats d’une requête Hive dans un répertoire local du nœud principal, vous devez envoyer celle-ci dans la ligne de commande Hadoop, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="553ad-163">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="553ad-164">Dans l'exemple suivant, la sortie de la requête Hive est consignée dans un fichier `hivequeryoutput.txt` situé dans le répertoire `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="553ad-164">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="553ad-166">**Enregistrer les résultats d’une requête Hive dans un blob Azure**</span><span class="sxs-lookup"><span data-stu-id="553ad-166">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="553ad-167">Vous pouvez également enregistrer les résultats d’une requête Hive dans un blob Azure situé dans le conteneur par défaut du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="553ad-167">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="553ad-168">La requête Hive se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="553ad-168">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="553ad-169">Dans l'exemple suivant, la sortie de la requête Hive est consignée dans le répertoire de blob `queryoutputdir` situé dans le conteneur par défaut du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="553ad-169">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="553ad-170">Ici, il suffit d’indiquer le nom du répertoire, sans celui du blob.</span><span class="sxs-lookup"><span data-stu-id="553ad-170">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="553ad-171">Une erreur est générée si vous déclarez le nom du répertoire et celui du blob, comme dans `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="553ad-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="553ad-173">Si vous ouvrez le conteneur par défaut du cluster Hadoop à l’aide d’Azure Storage Explorer, la requête Hive renvoie le résultat affiché dans la figure suivante.</span><span class="sxs-lookup"><span data-stu-id="553ad-173">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="553ad-174">Vous pouvez utiliser le filtre (encadré rouge) pour retrouver un blob dont le nom comporte les lettres spécifiées.</span><span class="sxs-lookup"><span data-stu-id="553ad-174">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="553ad-176"><a name="hive-editor"></a> 2. Envoyer des requêtes Hive avec l'éditeur Hive</span><span class="sxs-lookup"><span data-stu-id="553ad-176"><a name="hive-editor"></a> 2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="553ad-177">Vous pouvez également utiliser la console de requête (éditeur Hive) en entrant une URL sous la forme *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="553ad-177">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="553ad-178">Vous devez être connecté pour afficher cette console, et vous devez donc saisir ici vos informations d’identification de cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="553ad-178">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="553ad-179"><a name="ps"></a> 3. Envoyer des requêtes Hive avec les commandes Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="553ad-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="553ad-180">Vous pouvez également utiliser PowerShell pour envoyer des requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-180">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="553ad-181">Pour obtenir de l'aide, consultez [Envoi de tâches Hive avec PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="553ad-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="553ad-182"><a name="create-tables"></a>Création de la base de données et des tables Hive</span><span class="sxs-lookup"><span data-stu-id="553ad-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="553ad-183">Les requêtes Hive sont disponibles en téléchargement dans le [référentiel GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql).</span><span class="sxs-lookup"><span data-stu-id="553ad-183">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="553ad-184">Voici la requête Hive qui crée une table Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-184">Here is the Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="553ad-185">Voici les descriptions des champs que vous devez renseigner et d’autres opérations de configuration :</span><span class="sxs-lookup"><span data-stu-id="553ad-185">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="553ad-186">**&#60;database name>** : nom de la base de données que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="553ad-186">**&#60;database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="553ad-187">Si vous voulez utiliser la base de données par défaut, la requête *create database...* peut être omise.</span><span class="sxs-lookup"><span data-stu-id="553ad-187">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="553ad-188">**&#60;table name>** : nom de la table que vous voulez créer dans la base de données spécifiée.</span><span class="sxs-lookup"><span data-stu-id="553ad-188">**&#60;table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="553ad-189">Si vous voulez utiliser la base de données par défaut, la table peut être désignée directement par *&#60;table name>* sans &#60;database name>.</span><span class="sxs-lookup"><span data-stu-id="553ad-189">If you want to use the default database, the table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="553ad-190">**&#60;field separator>** : séparateur qui délimite les champs dans le fichier de données à charger dans la table Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-190">**&#60;field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="553ad-191">**&#60;line separator>** : séparateur qui délimite les lignes dans le fichier de données.</span><span class="sxs-lookup"><span data-stu-id="553ad-191">**&#60;line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="553ad-192">**&#60;storage location>** : emplacement Azure où enregistrer les données des tables Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-192">**&#60;storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="553ad-193">Si vous ne spécifiez pas *LOCATION &#60;storage location>*, la base de données et les tables sont stockées dans le répertoire *hive/warehouse/* du conteneur par défaut du cluster Hive par défaut.</span><span class="sxs-lookup"><span data-stu-id="553ad-193">If you do not specify *LOCATION &#60;storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="553ad-194">Si vous souhaitez spécifier l’emplacement de stockage, ce dernier doit se trouver dans le conteneur par défaut de la base de données et des tables.</span><span class="sxs-lookup"><span data-stu-id="553ad-194">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="553ad-195">Cet emplacement doit être désigné comme emplacement relatif du conteneur par défaut du cluster au format *’wasb:///&#60;directory 1>/’* ou *’wasb:///&#60;directory 1>/&#60;directory 2>/’*, etc. Une fois la requête exécutée, les répertoires relatifs sont créés dans le conteneur par défaut.</span><span class="sxs-lookup"><span data-stu-id="553ad-195">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="553ad-196">**TBLPROPERTIES("skip.header.line.count"="1")** : si le fichier de données contient une ligne d’en-tête, vous devez ajouter cette propriété **à la fin** de la requête *create table*.</span><span class="sxs-lookup"><span data-stu-id="553ad-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="553ad-197">Sinon, cette ligne d’en-tête est chargée comme un enregistrement dans la table.</span><span class="sxs-lookup"><span data-stu-id="553ad-197">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="553ad-198">Si le fichier de données ne contient aucune ligne d’en-tête, cette configuration peut être omise dans la requête.</span><span class="sxs-lookup"><span data-stu-id="553ad-198">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <span data-ttu-id="553ad-199"><a name="load-data"></a>Chargement des données dans des tables Hive</span><span class="sxs-lookup"><span data-stu-id="553ad-199"><a name="load-data"></a>Load data to Hive tables</span></span>
<span data-ttu-id="553ad-200">Voici la requête Hive qui charge les données dans une table Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-200">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="553ad-201">**&#60;path to blob data>** : si le fichier blob à charger dans la table Hive se trouve dans le conteneur par défaut du cluster Hadoop HDInsight, le chemin *&#60;path to blob data>* doit être au format *’wasb:///&#60;directory in this container>/&#60;blob file name>’*.</span><span class="sxs-lookup"><span data-stu-id="553ad-201">**&#60;path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *&#60;path to blob data>* should be in the format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="553ad-202">Le fichier blob peut également se trouver dans un autre conteneur du cluster Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="553ad-202">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="553ad-203">Dans ce cas, *&#60;path to blob data>* doit présenter le format *’wasb://&#60;nom du conteneur>@&#60;nom du compte de stockage>.blob.core.windows.net/&#60;nom du fichier blob>’*.</span><span class="sxs-lookup"><span data-stu-id="553ad-203">In this case, *&#60;path to blob data>* should be in the format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="553ad-204">Les données blob à charger dans la table Hive doivent se trouver dans le conteneur par défaut ou un autre conteneur du compte de stockage du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="553ad-204">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="553ad-205">Sinon, la requête *LOAD DATA* ne peut pas s'exécuter car elle n'aura pas accès aux données.</span><span class="sxs-lookup"><span data-stu-id="553ad-205">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <span data-ttu-id="553ad-206"><a name="partition-orc"></a>Rubriques avancées : Table partitionnée et Stocker des données Hive au format ORC</span><span class="sxs-lookup"><span data-stu-id="553ad-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="553ad-207">Si les données sont volumineuses, le partitionnement de la table est avantageux pour les requêtes qui doivent n’en balayer que quelques partitions.</span><span class="sxs-lookup"><span data-stu-id="553ad-207">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="553ad-208">Par exemple, il est raisonnable de partitionner les données journalisées d’un site Web par dates.</span><span class="sxs-lookup"><span data-stu-id="553ad-208">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="553ad-209">Outre le partitionnement des tables Hive, il est également judicieux de stocker les données Hive au format ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="553ad-209">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="553ad-210">Pour plus d'informations sur le format ORC, consultez l'article <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">L'utilisation de fichiers ORC améliore les performances lorsque Hive lit, écrit et traite des données</a>.</span><span class="sxs-lookup"><span data-stu-id="553ad-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="553ad-211">Table partitionnée</span><span class="sxs-lookup"><span data-stu-id="553ad-211">Partitioned table</span></span>
<span data-ttu-id="553ad-212">Voici la requête Hive qui crée une table partitionnée et charge les données dans celle-ci.</span><span class="sxs-lookup"><span data-stu-id="553ad-212">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="553ad-213">Lors de l’interrogation de tables partitionnées, il est recommandé d’ajouter la condition de partition au **début** de la clause `where`, car cela améliore considérablement l’efficacité de la recherche.</span><span class="sxs-lookup"><span data-stu-id="553ad-213">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="553ad-214"><a name="orc"></a>Stocker des données Hive au format ORC</span><span class="sxs-lookup"><span data-stu-id="553ad-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="553ad-215">Vous ne pouvez pas charger directement des données au format ORC depuis le stockage blob dans des tables Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-215">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="553ad-216">Voici les étapes que vous devez suivre pour charger des données au format ORC depuis des blobs Azure dans des tables Hive.</span><span class="sxs-lookup"><span data-stu-id="553ad-216">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="553ad-217">Créez une table externe **STORED AS TEXTFILE** et chargez les données du stockage blob dedans.</span><span class="sxs-lookup"><span data-stu-id="553ad-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="553ad-218">Créez une table interne avec le même schéma que la table externe à l’étape 1 et le même délimiteur de champ. Puis, stockez-y les données Hive au format ORC.</span><span class="sxs-lookup"><span data-stu-id="553ad-218">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="553ad-219">Sélectionnez les données de la table externe à l’étape 1 et insérez-les dans la table ORC.</span><span class="sxs-lookup"><span data-stu-id="553ad-219">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="553ad-220">Si la table TEXTFILE *&#60;database name>.&#60;external textfile table name>* a des partitions, à l’Étape 3, la commande `SELECT * FROM <database name>.<external textfile table name>` sélectionne la variable de partition comme champ dans le jeu de données retourné.</span><span class="sxs-lookup"><span data-stu-id="553ad-220">If the TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="553ad-221">Le fait de l’insérer dans *&#60;database name>.&#60;ORC table name>* échoue car *&#60;database name>.&#60;ORC table name>* ne dispose pas de la variable de partition comme champ dans le schéma de la table.</span><span class="sxs-lookup"><span data-stu-id="553ad-221">Inserting it into the *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="553ad-222">Dans ce cas, vous devez sélectionner explicitement les champs à insérer dans *&#60;database name>.&#60;ORC table name>* comme suit :</span><span class="sxs-lookup"><span data-stu-id="553ad-222">In this case, you need to specifically select the fields to be inserted to *&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="553ad-223">Pour plus de sécurité, lorsque vous utilisez la requête suivante, il est recommandé de déplacer la table *&#60;external textfile table name>* une fois toutes les données insérées dans la table *&#60;database name>.&#60;ORC table name>* :</span><span class="sxs-lookup"><span data-stu-id="553ad-223">It is safe to drop the *&#60;external textfile table name>* when using the following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="553ad-224">À l’issue de cette procédure, vous devez obtenir une table immédiatement exploitable et contenant des données au format ORC.</span><span class="sxs-lookup"><span data-stu-id="553ad-224">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  
