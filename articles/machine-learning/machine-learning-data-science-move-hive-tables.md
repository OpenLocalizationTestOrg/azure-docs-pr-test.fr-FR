---
title: "aaaCreate tables la ruche et charger des données à partir du stockage d’objets Blob Azure | Documents Microsoft"
description: "Créer des tables de la ruche et charger des données dans les tables d’objets blob toohive"
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
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="b35a6-103">Créer des tables Hive et charger des données à partir de Stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="b35a6-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="b35a6-104">Cette rubrique présente des requêtes Hive génériques qui créent des tables Hive et chargent des données à partir d’un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b35a6-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="b35a6-105">Quelques conseils sont également fourni sur le partitionnement des tables de la ruche et sur l’utilisation de hello optimisées en ligne en colonnes (ORC) mise en forme tooimprove les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="b35a6-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="b35a6-106">Cela **menu** lie tootopics qui décrivent comment les données de tooingest dans les environnements cibles où les données de salutation peuvent être stockées et traitées au cours de hello processus de science des données équipe (TDSP).</span><span class="sxs-lookup"><span data-stu-id="b35a6-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="b35a6-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b35a6-107">Prerequisites</span></span>
<span data-ttu-id="b35a6-108">Cet article suppose que vous avez :</span><span class="sxs-lookup"><span data-stu-id="b35a6-108">This article assumes that you have:</span></span>

* <span data-ttu-id="b35a6-109">Créé un compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b35a6-109">Created an Azure storage account.</span></span> <span data-ttu-id="b35a6-110">Pour obtenir des instructions, voir [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b35a6-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="b35a6-111">Configurer un cluster Hadoop personnalisée avec hello service HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b35a6-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="b35a6-112">Si vous avez besoin d'aide, consultez [Personnaliser des clusters Hadoop Azure HDInsight pour l'analyse avancée](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b35a6-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="b35a6-113">Cluster de toohello activé l’accès à distance, connecté et ouvrir la console de ligne de commande Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="b35a6-114">Si vous avez besoin d’instructions, consultez [hello d’accès nœud principal de Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="b35a6-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="b35a6-115">Télécharger le stockage d’objets blob de données tooAzure</span><span class="sxs-lookup"><span data-stu-id="b35a6-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="b35a6-116">Si vous avez créé une machine virtuelle Azure en suivant les instructions hello fournies dans [configurer une machine virtuelle Azure pour analytique avancée](machine-learning-data-science-setup-virtual-machine.md), ce fichier de script doit avoir été téléchargé toohello *C:\\ Les utilisateurs\\\<nom d’utilisateur\>\\Documents\\des Scripts de science des données* répertoire sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="b35a6-117">Ces requêtes Hive nécessitent uniquement que vous connectez votre propre schéma de données et la configuration du stockage blob Azure dans toobe de champs appropriés hello prêt à envoyer.</span><span class="sxs-lookup"><span data-stu-id="b35a6-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="b35a6-118">Nous partons du principe que les données hello pour les tables de la ruche sont dans un **non compressé** sous forme de tableau, et que les données de salutation a été téléchargé par défaut toohello (ou tooan supplémentaire) conteneur hello du compte de stockage utilisé par le cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="b35a6-119">Si vous souhaitez toopractice sur hello **NYC Taxi voyage données**, vous devez :</span><span class="sxs-lookup"><span data-stu-id="b35a6-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="b35a6-120">**télécharger** hello 24 [NYC Taxi voyage données](http://www.andresmh.com/nyctaxitrips) fichiers (fichiers de voyage 12 et les fichiers de tarif 12),</span><span class="sxs-lookup"><span data-stu-id="b35a6-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="b35a6-121">**décompresser** tous les fichiers en fichiers .csv, puis</span><span class="sxs-lookup"><span data-stu-id="b35a6-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="b35a6-122">**télécharger** les toohello par défaut (ou conteneur approprié) du compte de stockage Azure qui a été créé par la procédure hello hello de hello [personnaliser Azure HDInsight Hadoop pour le processus d’Analytique avancée et la technologie des clusters ](machine-learning-data-science-customize-hadoop-cluster.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="b35a6-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="b35a6-123">Hello processus tooupload hello .csv fichiers toohello conteneur par défaut sur le compte de stockage hello se trouvent sur ce [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="b35a6-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="b35a6-124"><a name="submit"></a>Comment les requêtes Hive toosubmit</span><span class="sxs-lookup"><span data-stu-id="b35a6-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="b35a6-125">Pour envoyer des requêtes Hive, utilisez au choix :</span><span class="sxs-lookup"><span data-stu-id="b35a6-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="b35a6-126">Envoyer des requêtes Hive avec la ligne de commande Hadoop dans le nœud principal du cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="b35a6-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="b35a6-127">Envoyer des requêtes Hive avec hello éditeur Hive</span><span class="sxs-lookup"><span data-stu-id="b35a6-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="b35a6-128">Envoyer des requêtes Hive avec les commandes Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b35a6-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="b35a6-129">Des requêtes Hive sont similaires à SQL.</span><span class="sxs-lookup"><span data-stu-id="b35a6-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="b35a6-130">Si vous êtes familiarisé avec SQL, vous souhaiterez peut-être hello [Hive pour SQL utilisateurs Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) utile.</span><span class="sxs-lookup"><span data-stu-id="b35a6-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="b35a6-131">Lorsque vous soumettez une requête Hive, vous pouvez également contrôler la destination hello de sortie de hello de requêtes Hive, qu’il s’agisse de hello écran ou tooa fichier local sur le nœud principal de hello ou tooan d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b35a6-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="b35a6-132"><a name="headnode"></a> 1. Envoyer des requêtes Hive avec la ligne de commande Hadoop dans le nœud principal du cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="b35a6-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="b35a6-133">Si la ruche hello requête est complexe, envoi que directement dans le nœud principal de hello du cluster Hadoop de hello entraîne généralement toofaster de bouclage à envoyer avec un éditeur Hive ou scripts Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b35a6-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="b35a6-134">Connectez-vous à toohello le nœud principal du cluster Hadoop de hello, ouvrez hello de ligne de commande Hadoop sur bureau hello de nœud principal de hello et entrez la commande `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="b35a6-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="b35a6-135">Vous avez des requêtes Hive de trois façons toosubmit Bonjour de ligne de commande Hadoop :</span><span class="sxs-lookup"><span data-stu-id="b35a6-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="b35a6-136">directement ;</span><span class="sxs-lookup"><span data-stu-id="b35a6-136">directly</span></span>
* <span data-ttu-id="b35a6-137">à l’aide de fichiers HQL ;</span><span class="sxs-lookup"><span data-stu-id="b35a6-137">using .hql files</span></span>
* <span data-ttu-id="b35a6-138">avec hello Hive console de commande</span><span class="sxs-lookup"><span data-stu-id="b35a6-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="b35a6-139">Envoyer directement des requêtes Hive dans la ligne de commande Hadoop</span><span class="sxs-lookup"><span data-stu-id="b35a6-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="b35a6-140">Vous pouvez exécuter la commande comme `hive -e "<your hive query>;` toosubmit les requêtes Hive simples directement dans Hadoop ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="b35a6-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="b35a6-141">Voici un exemple, où les contours de zone hello rouge hello commande qui soumet la requête Hive de hello et hello zone verte contours hello sortie à partir de la requête de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="b35a6-143">Envoyer des requêtes Hive dans des fichiers HQL</span><span class="sxs-lookup"><span data-stu-id="b35a6-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="b35a6-144">Lors de la requête de Hive hello est plus complexe et comporte plusieurs lignes, la modification de requêtes dans la ligne de commande ou de la console de commande ruche n’est pas pratique.</span><span class="sxs-lookup"><span data-stu-id="b35a6-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="b35a6-145">Une alternative est toouse un éditeur de texte dans le nœud principal de hello de requêtes Hive hello Hadoop cluster toosave hello dans un fichier .hql dans un répertoire local du nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="b35a6-146">Puis hello ruche requête hello .hql fichier peut être envoyée à l’aide de hello `-f` argument comme suit :</span><span class="sxs-lookup"><span data-stu-id="b35a6-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![Create workspace](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="b35a6-148">**Supprimer l’affichage de l’état d’avancement des requêtes Hive**</span><span class="sxs-lookup"><span data-stu-id="b35a6-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="b35a6-149">Par défaut, une fois la requête Hive est soumise en ligne de commande Hadoop, progression hello de tâche de mappage/réduction hello est imprimée sur écran.</span><span class="sxs-lookup"><span data-stu-id="b35a6-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="b35a6-150">toosuppress hello impression écran de progression de la tâche hello mappage/réduction, vous pouvez utiliser un argument `-S` (« S » en majuscules) Bonjour ligne de commande comme suit :</span><span class="sxs-lookup"><span data-stu-id="b35a6-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="b35a6-151">.</span><span class="sxs-lookup"><span data-stu-id="b35a6-151">.</span></span>    <span data-ttu-id="b35a6-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="b35a6-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="b35a6-153">Envoyer des requêtes Hive dans la console de commande Hive</span><span class="sxs-lookup"><span data-stu-id="b35a6-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="b35a6-154">Vous pouvez également tout d’abord entrer la console de commande hello ruche en exécutant la commande `hive` de ligne de commande Hadoop, puis à soumettre les requêtes Hive dans la console de commande Hive.</span><span class="sxs-lookup"><span data-stu-id="b35a6-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="b35a6-155">Voici un exemple.</span><span class="sxs-lookup"><span data-stu-id="b35a6-155">Here is an example.</span></span> <span data-ttu-id="b35a6-156">Dans cet exemple, hello deux zones rouges surbrillance hello commandes utilisées tooenter hello console de commande Hive et hello requête Hive soumis dans la console de commande Hive, respectivement.</span><span class="sxs-lookup"><span data-stu-id="b35a6-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="b35a6-157">boîte de Hello vert met en surbrillance la sortie hello à partir de la requête de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-157">hello green box highlights hello output from hello Hive query.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="b35a6-159">les exemples précédents Hello directement les résultats de la requête Hive hello sur l’écran de sortie.</span><span class="sxs-lookup"><span data-stu-id="b35a6-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="b35a6-160">Vous pouvez également écrire le fichier local tooa sortie hello sur le nœud principal de hello ou tooan d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b35a6-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="b35a6-161">Ensuite, vous pouvez utiliser d’autres outils toofurther analyser la sortie hello de requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="b35a6-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="b35a6-162">**Sortie ruche requête résultats tooa du fichier local.**</span><span class="sxs-lookup"><span data-stu-id="b35a6-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="b35a6-163">toooutput ruche requête résultats tooa répertoire local sur le nœud principal de hello, vous avez toosubmit hello ruche de requête dans la ligne de commande Hadoop de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b35a6-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="b35a6-164">Dans l’exemple suivant de hello, sortie hello de requête Hive est écrit dans un fichier `hivequeryoutput.txt` dans le répertoire `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="b35a6-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="b35a6-166">**Sortie tooan de résultats de requête Hive blob Azure**</span><span class="sxs-lookup"><span data-stu-id="b35a6-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="b35a6-167">Vous pouvez également produire hello ruche requête résultats tooan des objets blob Azure, dans le conteneur par défaut de hello du cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="b35a6-168">requête Hive de Hello pour cela est la suivante :</span><span class="sxs-lookup"><span data-stu-id="b35a6-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="b35a6-169">Dans l’exemple suivant de hello, sortie hello de requête Hive est écrite répertoire d’objets blob tooa `queryoutputdir` conteneur hello par défaut du cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="b35a6-170">Ici, vous ne devez nom du répertoire hello tooprovide, sans le nom d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="b35a6-171">Une erreur est générée si vous déclarez le nom du répertoire et celui du blob, comme dans `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="b35a6-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="b35a6-173">Si vous ouvrez le conteneur par défaut de hello du cluster Hadoop de hello à l’aide de l’Explorateur de stockage Azure, vous pouvez voir la sortie hello de requête de Hive hello comme indiqué dans la figure suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="b35a6-174">Vous pouvez appliquer hello filtre (mis en surbrillance en rouge) tooonly récupérer hello blob avec des lettres spécifiés dans les noms.</span><span class="sxs-lookup"><span data-stu-id="b35a6-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![Create workspace](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="b35a6-176"><a name="hive-editor"></a> 2. Envoyer des requêtes Hive avec hello éditeur Hive</span><span class="sxs-lookup"><span data-stu-id="b35a6-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="b35a6-177">Vous pouvez également utiliser hello Console de requête (éditeur Hive) en entrant une URL sous forme de hello *https://&#60 ; Nom du cluster Hadoop >.azurehdinsight.net/Home/HiveEditor* dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="b35a6-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="b35a6-178">Vous devez être connecté hello voir cette console et par conséquent, vous avez besoin de vos informations d’identification Hadoop le cluster.</span><span class="sxs-lookup"><span data-stu-id="b35a6-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="b35a6-179"><a name="ps"></a> 3. Envoyer des requêtes Hive avec les commandes Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b35a6-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="b35a6-180">Vous pouvez également utiliser des requêtes Hive de toosubmit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b35a6-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="b35a6-181">Pour obtenir de l'aide, consultez [Envoi de tâches Hive avec PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b35a6-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="b35a6-182"><a name="create-tables"></a>Création de la base de données et des tables Hive</span><span class="sxs-lookup"><span data-stu-id="b35a6-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="b35a6-183">requêtes Hive Hello sont partagés Bonjour [référentiel GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) et peut être téléchargé à partir de là.</span><span class="sxs-lookup"><span data-stu-id="b35a6-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="b35a6-184">Voici la requête Hive hello qui crée une table Hive.</span><span class="sxs-lookup"><span data-stu-id="b35a6-184">Here is hello Hive query that creates a Hive table.</span></span>

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

<span data-ttu-id="b35a6-185">Voici la description de hello de champs hello dont vous avez besoin tooplug dans et d’autres configurations :</span><span class="sxs-lookup"><span data-stu-id="b35a6-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="b35a6-186">**&#60; nom de la base de données >**: nom hello de base de données hello que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="b35a6-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="b35a6-187">Si vous souhaitez simplement la base de données par défaut toouse hello, hello requête *créer la base de données...*  peut être omis.</span><span class="sxs-lookup"><span data-stu-id="b35a6-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="b35a6-188">**&#60; nom de la table >**: nom hello de table hello que vous souhaitez toocreate au sein de la base de données spécifiée hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="b35a6-189">Si vous souhaitez la base de données par défaut toouse hello, table de hello peut être référencé directement par *&#60; nom de la table >* sans &#60; nom de la base de données >.</span><span class="sxs-lookup"><span data-stu-id="b35a6-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="b35a6-190">**&#60; le séparateur de champs >**: séparateur hello qui délimite les champs de toobe de fichier de données hello téléchargé toohello ruche du tableau.</span><span class="sxs-lookup"><span data-stu-id="b35a6-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="b35a6-191">**&#60; le séparateur de ligne >**: séparateur hello qui délimite les lignes dans le fichier de données hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="b35a6-192">**&#60; l’emplacement de stockage >**: hello des données de stockage Azure localisation toosave hello des tables de la ruche.</span><span class="sxs-lookup"><span data-stu-id="b35a6-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="b35a6-193">Si vous ne spécifiez pas *emplacement &#60; emplacement de stockage >*, hello de base de données et tables hello sont stockées dans *hive/entrepôt/* répertoire dans un conteneur par défaut hello de cluster de ruche hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="b35a6-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="b35a6-194">Si vous souhaitez d’emplacement de stockage toospecify hello, emplacement de stockage hello a toobe conteneur hello par défaut pour les tables et de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="b35a6-195">Cet emplacement a toobe appelé conteneur d’emplacement toohello relatif par défaut du cluster hello format hello *' wasb : / / / &#60; répertoire 1 > /'* ou *' wasb : / / / &#60; répertoire 1 > / &#60; répertoire 2 > /'*, etc.. Après l’exécution de requête de hello, répertoire hello est créés dans le conteneur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="b35a6-196">**TBLPROPERTIES("Skip.Header.Line.Count"="1")**: si le fichier de données hello possède une ligne d’en-tête, vous avez tooadd cette propriété **à fin de hello** Hello *create table* requête.</span><span class="sxs-lookup"><span data-stu-id="b35a6-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="b35a6-197">Dans le cas contraire, ligne d’en-tête hello est chargé comme une table d’enregistrement toohello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="b35a6-198">Si le fichier de données hello n’a pas d’une ligne d’en-tête, cette configuration peut être omise dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="b35a6-199"><a name="load-data"></a>Charger les tables de données tooHive</span><span class="sxs-lookup"><span data-stu-id="b35a6-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="b35a6-200">Voici la requête Hive hello qui charge des données dans une table Hive.</span><span class="sxs-lookup"><span data-stu-id="b35a6-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="b35a6-201">**&#60; les données de chemin d’accès tooblob >**: si la table Hive de hello blob fichier toobe téléchargé toohello est dans un conteneur par défaut hello de hello cluster HDInsight Hadoop, hello *&#60; les données de chemin d’accès tooblob >* devrait être au format de hello *' wasb : / / / &#60; répertoire de ce conteneur > / &#60; le nom de fichier blob >'*.</span><span class="sxs-lookup"><span data-stu-id="b35a6-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="b35a6-202">fichier d’objet blob Hello peut également être dans un conteneur supplémentaire de hello cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b35a6-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="b35a6-203">Dans ce cas, *&#60; les données de chemin d’accès tooblob >* devrait être au format de hello *' wasb : / / &#60; nom de conteneur > @&#60; le nom de compte de stockage >.blob.core.windows.net/ &#60; nom du fichier blob >'*.</span><span class="sxs-lookup"><span data-stu-id="b35a6-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b35a6-204">Hello blob données toobe téléchargé tooHive table a toobe dans la valeur par défaut hello ou un conteneur supplémentaire hello du compte de stockage de cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="b35a6-205">Dans le cas contraire, hello *charger des données* signale que qu’il ne peut pas accéder à des données de hello Échec de la requête.</span><span class="sxs-lookup"><span data-stu-id="b35a6-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="b35a6-206"><a name="partition-orc"></a>Rubriques avancées : Table partitionnée et Stocker des données Hive au format ORC</span><span class="sxs-lookup"><span data-stu-id="b35a6-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="b35a6-207">Si les données de salutation sont volumineux, le partitionnement de table de hello est bénéfique pour les requêtes qui doivent uniquement tooscan plusieurs partitions de table de hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="b35a6-208">Il est, par exemple, les données du journal de hello toopartition raisonnable d’un site web par dates.</span><span class="sxs-lookup"><span data-stu-id="b35a6-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="b35a6-209">Dans Ajout toopartitioning ruche tables, il est également utile toostore hello ruche données hello optimisées en ligne en colonnes (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="b35a6-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="b35a6-210">Pour plus d'informations sur le format ORC, consultez l'article <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">L'utilisation de fichiers ORC améliore les performances lorsque Hive lit, écrit et traite des données</a>.</span><span class="sxs-lookup"><span data-stu-id="b35a6-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="b35a6-211">Table partitionnée</span><span class="sxs-lookup"><span data-stu-id="b35a6-211">Partitioned table</span></span>
<span data-ttu-id="b35a6-212">Voici la requête Hive de hello qui crée une table partitionnée et charge les données.</span><span class="sxs-lookup"><span data-stu-id="b35a6-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="b35a6-213">Lors de l’interrogation de tables partitionnées, il est recommandé de condition de partition tooadd hello Bonjour **début** Hello `where` clause comme cela améliore l’efficacité de hello de manière significative la recherche.</span><span class="sxs-lookup"><span data-stu-id="b35a6-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="b35a6-214"><a name="orc"></a>Stocker des données Hive au format ORC</span><span class="sxs-lookup"><span data-stu-id="b35a6-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="b35a6-215">Ne peut pas directement charger des données de stockage d’objets blob dans des tables de ruche qui est stocké dans un format ORC hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="b35a6-216">Voici les étapes hello que hello que vous avez besoin de données de tooload tootake à partir d’Azure BLOB tables tooHive stockées au format ORC.</span><span class="sxs-lookup"><span data-stu-id="b35a6-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="b35a6-217">Créer une table externe **stocké le fichier en tant que texte** et charger des données à partir de la table de toohello de stockage blob.</span><span class="sxs-lookup"><span data-stu-id="b35a6-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

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

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="b35a6-218">Créer une table interne avec hello même schéma que la table externe de hello à l’étape 1, hello le séparateur de champs et stocker hello ruche des données au format ORC hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="b35a6-219">Sélectionnez les données à partir de la table externe de hello à l’étape 1 et l’insérer dans la table ORC hello</span><span class="sxs-lookup"><span data-stu-id="b35a6-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="b35a6-220">Si table de fichier texte hello *&#60; nom de la base de données >. &#60; nom de la table externe fichier texte >* a des partitions, à l’étape 3, hello `SELECT * FROM <database name>.<external textfile table name>` commande sélectionne hello variable de partition comme un champ dans hello retourné de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="b35a6-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="b35a6-221">Il insérant hello *&#60; nom de la base de données >. &#60; nom de la table ORC >* échoue depuis *&#60; nom de la base de données >. &#60; nom de la table ORC >* n’a pas de variable de partition hello comme un champ de schéma de la table hello.</span><span class="sxs-lookup"><span data-stu-id="b35a6-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="b35a6-222">Dans ce cas, vous devez toospecifically hello sélectionnez champs toobe inséré trop*&#60; nom de la base de données >. &#60; nom de la table ORC >* comme suit :</span><span class="sxs-lookup"><span data-stu-id="b35a6-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="b35a6-223">Il est sécurisé toodrop hello *&#60; nom de la table externe fichier texte >* lorsque à l’aide de hello suivant la requête une fois les données a été insérée dans *&#60; nom de la base de données >. &#60; nom de la table ORC >*:</span><span class="sxs-lookup"><span data-stu-id="b35a6-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="b35a6-224">Une fois cette procédure, vous devez disposer d’une table avec des données dans hello ORC format prêt toouse.</span><span class="sxs-lookup"><span data-stu-id="b35a6-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  
