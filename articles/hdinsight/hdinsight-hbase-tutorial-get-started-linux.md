---
title: "aaaGet a démarré avec un exemple de HBase sur HDInsight - Azure | Documents Microsoft"
description: "Suivez cette toostart d’exemple Apache HBase à l’aide de hadoop dans HDInsight. Créer des tables à partir du shell HBase de hello et les interroger à l’aide de la ruche."
keywords: commande hbase, exemple hbase
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="1b3b3-105">Prise en main d’un exemple Apache HBase dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="1b3b3-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="1b3b3-106">Découvrez comment créer des tables de HBase toocreate un cluster HBase dans HDInsight, et interroger des tables à l’aide de ruche.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-106">Learn how toocreate an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="1b3b3-107">Pour obtenir des informations générales sur HBase, voir [Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="1b3b3-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="1b3b3-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1b3b3-108">Prerequisites</span></span>
<span data-ttu-id="1b3b3-109">Avant de commencer la tentative de cet exemple HBase, vous devez disposer de hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-109">Before you begin trying this HBase example, you must have hello following items:</span></span>

* <span data-ttu-id="1b3b3-110">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-110">**An Azure subscription**.</span></span> <span data-ttu-id="1b3b3-111">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1b3b3-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="1b3b3-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="1b3b3-114">Créer un cluster HBase</span><span class="sxs-lookup"><span data-stu-id="1b3b3-114">Create HBase cluster</span></span>
<span data-ttu-id="1b3b3-115">Hello procédure suivante utilise une toocreate de modèle Azure Resource Manager un version 3.4 HBase de basés sur Linux cluster et hello dépendants compte par défaut le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-115">hello following procedure uses an Azure Resource Manager template toocreate a version 3.4 Linux-based HBase cluster and hello dependent default Azure Storage account.</span></span> <span data-ttu-id="1b3b3-116">paramètres de hello toounderstand utilisés dans la procédure de hello et d’autres méthodes de création de cluster, consultez [Hadoop basé sur Linux de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-116">toounderstand hello parameters used in hello procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="1b3b3-117">Cliquez sur hello suit image tooopen hello template Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-117">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="1b3b3-118">modèle de Hello se trouve dans un conteneur d’objets blob publics.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-118">hello template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="1b3b3-119">À partir de hello **les déploiement personnalisé** panneau, entrez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-119">From hello **Custom deployment** blade, enter hello following values:</span></span>
   
   * <span data-ttu-id="1b3b3-120">**Abonnement**: sélectionnez votre abonnement Azure est utilisé toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-120">**Subscription**: Select your Azure subscription that is used toocreate hello cluster.</span></span>
   * <span data-ttu-id="1b3b3-121">**Groupe de ressources** : créez un groupe Azure Resource Manager ou utilisez un groupe existant.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="1b3b3-122">**Emplacement**: spécifiez l’emplacement hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-122">**Location**: Specify hello location of hello resource group.</span></span> 
   * <span data-ttu-id="1b3b3-123">**ClusterName**: entrez un nom pour le cluster de HBase hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-123">**ClusterName**: Enter a name for hello HBase cluster.</span></span>
   * <span data-ttu-id="1b3b3-124">**Nom de connexion et mot de passe de cluster**: nom de connexion par défaut hello est **admin**.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-124">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="1b3b3-125">**Mot de passe et le nom d’utilisateur SSH**: nom d’utilisateur par défaut de hello est **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-125">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="1b3b3-126">Vous pouvez le renommer.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-126">You can rename it.</span></span>
     
     <span data-ttu-id="1b3b3-127">Tous les autres paramètres sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="1b3b3-128">Chaque cluster possède une dépendance de compte Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="1b3b3-129">Après avoir supprimé un cluster, les données de salutation conservent dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-129">After you delete a cluster, hello data retains in hello storage account.</span></span> <span data-ttu-id="1b3b3-130">nom du compte de stockage Hello cluster par défaut est le nom de cluster hello avec « store » ajouté.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-130">hello cluster default storage account name is hello cluster name with "store" appended.</span></span> <span data-ttu-id="1b3b3-131">Il est codé en dur dans la section de variables de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-131">It is hardcoded in hello template variables section.</span></span>
3. <span data-ttu-id="1b3b3-132">Sélectionnez **J’accepte les conditions susmentionnées générales toohello**, puis cliquez sur **bon**.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-132">Select **I agree toohello terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="1b3b3-133">Il prend environ 20 minutes toocreate un cluster.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-133">It takes about 20 minutes toocreate a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="1b3b3-134">Après la suppression d’un cluster HBase, vous pouvez créer un autre cluster HBase à l’aide de hello même conteneur d’objets blob par défaut.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-134">After an HBase cluster is deleted, you can create another HBase cluster by using hello same default blob container.</span></span> <span data-ttu-id="1b3b3-135">nouveau cluster de Hello récupère les tables de HBase hello créées hello cluster d’origine.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-135">hello new cluster picks up hello HBase tables you created in hello original cluster.</span></span> <span data-ttu-id="1b3b3-136">des incohérences tooavoid, nous vous conseillons de désactiver les tables HBase hello avant de supprimer le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-136">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="1b3b3-137">Créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="1b3b3-137">Create tables and insert data</span></span>
<span data-ttu-id="1b3b3-138">Vous pouvez utiliser SSH tooconnect tooHBase clusters et utilisent des tables de HBase Shell toocreate HBase, insérer des données et interroger des données.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-138">You can use SSH tooconnect tooHBase clusters and then use HBase Shell toocreate HBase tables, insert data, and query data.</span></span> <span data-ttu-id="1b3b3-139">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="1b3b3-140">Pour la plupart des personnes, les données apparaissent sous forme de hello :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-140">For most people, data appears in hello tabular format:</span></span>

![Données tabulaires HBase HDInsight][img-hbase-sample-data-tabular]

<span data-ttu-id="1b3b3-142">Dans HBase (il s’agit d’une implémentation de BigTable), hello même données ressemble à :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-142">In HBase (an implementation of BigTable), hello same data looks like:</span></span>

![Données bigtable HBase HDInsight][img-hbase-sample-data-bigtable]


<span data-ttu-id="1b3b3-144">**toouse hello shell HBase**</span><span class="sxs-lookup"><span data-stu-id="1b3b3-144">**toouse hello HBase shell**</span></span>

1. <span data-ttu-id="1b3b3-145">À partir de SSH, exécutez hello HBase commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-145">From SSH, run hello following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="1b3b3-146">Créez une HBase contenant deux familles de colonne :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="1b3b3-147">Insérez des données :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Interpréteur de commandes HBase Hadoop HDInsight][img-hbase-shell]
4. <span data-ttu-id="1b3b3-149">Récupérez une seule ligne :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="1b3b3-150">Vous devez voir hello mêmes résultats comme à l’aide de la commande d’analyse hello, car il y a qu’une seule ligne.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-150">You shall see hello same results as using hello scan command because there is only one row.</span></span>
   
    <span data-ttu-id="1b3b3-151">Pour plus d’informations sur le schéma de la table HBase hello, consultez [Introduction tooHBase conception de schéma][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="1b3b3-151">For more information about hello HBase table schema, see [Introduction tooHBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="1b3b3-152">Pour obtenir plus de commandes HBase, consultez le [Guide de référence Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="1b3b3-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="1b3b3-153">Sortie hello shell</span><span class="sxs-lookup"><span data-stu-id="1b3b3-153">Exit hello shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="1b3b3-154">**toobulk charger des données dans la table HBase de contacts hello**</span><span class="sxs-lookup"><span data-stu-id="1b3b3-154">**toobulk load data into hello contacts HBase table**</span></span>

<span data-ttu-id="1b3b3-155">HBase propose plusieurs méthodes pour charger des données dans des tables.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="1b3b3-156">Pour en savoir plus, consultez la rubrique [Chargement en bloc](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="1b3b3-157">Vous trouverez un exemple de fichier de données dans un conteneur de blobs public, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="1b3b3-158">contenu Hello hello du fichier de données est :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-158">hello content of hello data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="1b3b3-159">Vous pouvez éventuellement créer un fichier texte et télécharger le compte de stockage propre fichier tooyour de hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-159">You can optionally create a text file and upload hello file tooyour own storage account.</span></span> <span data-ttu-id="1b3b3-160">Pour obtenir des instructions de hello, consultez [télécharger des données pour les travaux Hadoop dans HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="1b3b3-160">For hello instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="1b3b3-161">Cette procédure utilise la table de Contacts HBase hello que vous avez créé dans la dernière procédure de hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-161">This procedure uses hello Contacts HBase table you have created in hello last procedure.</span></span>
> 

1. <span data-ttu-id="1b3b3-162">À partir de SSH, exécutez hello suivant commande tootransform hello tooStoreFiles du fichier de données et stocker à un chemin d’accès relatif spécifié par Dimporttsv.bulk.output.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-162">From SSH, run hello following command tootransform hello data file tooStoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="1b3b3-163">Si vous êtes dans le HBase Shell, utilisez tooexit de commande exit hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-163">If you are in HBase Shell, use hello exit command tooexit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="1b3b3-164">Exécutez hello suivant des données de commande tooupload hello à partir de la table HBase à toohello /example/data/storeDataFileOutput :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-164">Run hello following command tooupload hello data from  /example/data/storeDataFileOutput toohello HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="1b3b3-165">Vous pouvez ouvrir hello shell HBase et utiliser le contenu de la table hello analyse commande toolist hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-165">You can open hello HBase shell, and use hello scan command toolist hello table content.</span></span>

## <a name="use-hive-tooquery-hbase"></a><span data-ttu-id="1b3b3-166">Utiliser la ruche tooquery HBase</span><span class="sxs-lookup"><span data-stu-id="1b3b3-166">Use Hive tooquery HBase</span></span>

<span data-ttu-id="1b3b3-167">Vous pouvez interroger les données des tables HBase à l’aide de Hive.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="1b3b3-168">Dans cette section, vous créez une table Hive qui mappe la table HBase à toohello et utilise les données de salutation tooquery dans votre table HBase.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-168">In this section, you create a Hive table that maps toohello HBase table and uses it tooquery hello data in your HBase table.</span></span>

1. <span data-ttu-id="1b3b3-169">Ouvrez **PuTTY**et vous connecter toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-169">Open **PuTTY**, and connect toohello cluster.</span></span>  <span data-ttu-id="1b3b3-170">Consultez les instructions hello dans la procédure précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-170">See hello instructions in hello previous procedure.</span></span>
2. <span data-ttu-id="1b3b3-171">À partir de la session SSH hello, utilisez hello suivant commande toostart Beeline :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-171">From hello SSH session, use hello following command toostart Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="1b3b3-172">Pour plus d’informations sur Beeline, consultez [Utilisation de Hive avec Hadoop dans HDInsight via Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="1b3b3-173">Exécutez hello suivant HiveQL script toocreate une table Hive qui mappe la table HBase à toohello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-173">Run hello following HiveQL script  toocreate a Hive table that maps toohello HBase table.</span></span> <span data-ttu-id="1b3b3-174">Assurez-vous que vous avez créé la table d’exemple hello mentionné plus haut dans ce didacticiel à l’aide de shell HBase de hello avant d’exécuter cette instruction.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-174">Make sure that you have created hello sample table referenced earlier in this tutorial by using hello HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="1b3b3-175">Exécutez hello HiveQL script tooquery hello données dans la table HBase à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-175">Run hello following HiveQL script tooquery hello data in hello HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="1b3b3-176">Utilisation des API REST HBase à l’aide de Curl</span><span class="sxs-lookup"><span data-stu-id="1b3b3-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="1b3b3-177">API REST Hello est sécurisé via [l’authentification de base](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-177">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="1b3b3-178">Vous sont toujours effectuer des demandes à l’aide de HTTP sécurisée (HTTPS) toohelp vous assurer que vos informations d’identification sont envoyées en toute sécurité toohello server.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-178">You shall always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>

2. <span data-ttu-id="1b3b3-179">Utilisez hello commande toolist hello existant HBase tables suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-179">Use hello following command toolist hello existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="1b3b3-180">Utilisez hello suivant commande toocreate une nouvelle table HBase avec les familles de deux colonnes :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-180">Use hello following command toocreate a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="1b3b3-181">schéma de Hello est fournie au format JSon de hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-181">hello schema is provided in hello JSon format.</span></span>
4. <span data-ttu-id="1b3b3-182">Utilisez hello suivant de commande tooinsert des données :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-182">Use hello following command tooinsert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="1b3b3-183">Vous devez en base64 encoder les valeurs hello spécifiés dans le commutateur -d de hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-183">You must base64 encode hello values specified in hello -d switch.</span></span> <span data-ttu-id="1b3b3-184">Dans l’exemple de hello :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-184">In hello example:</span></span>
   
   * <span data-ttu-id="1b3b3-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="1b3b3-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="1b3b3-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="1b3b3-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="1b3b3-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="1b3b3-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="1b3b3-188">[clé de ligne false](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) vous permet de tooinsert plusieurs valeurs (par lot).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you tooinsert multiple (batched) values.</span></span>
5. <span data-ttu-id="1b3b3-189">Utilisez hello suivant commande tooget une ligne :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-189">Use hello following command tooget a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="1b3b3-190">Pour plus d’informations sur HBase Rest, voir le [Guide de référence Apache HBase](https://hbase.apache.org/book.html#_rest).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="1b3b3-191">Thrift n’est pas pris en charge par HBase dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="1b3b3-192">Lorsque vous utilisez Curl ou toute autre communication reste avec WebHCat, vous devez vous authentifier les demandes hello en fournissant le nom d’utilisateur hello et mot de passe administrateur de cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-192">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="1b3b3-193">Vous devez également utiliser le nom du cluster hello comme partie d’identificateur de ressource uniforme (URI) de hello utilisé serveur toohello de toosend hello demandes :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-193">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="1b3b3-194">Vous devez recevoir un toohello similaire de réponse suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-194">You should receive a response similar toohello following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="1b3b3-195">Vérification du statut du cluster</span><span class="sxs-lookup"><span data-stu-id="1b3b3-195">Check cluster status</span></span>
<span data-ttu-id="1b3b3-196">HBase dans HDInsight est livré avec une interface utilisateur web pour la surveillance des clusters.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="1b3b3-197">À l’aide de l’interface utilisateur Web de hello, vous pouvez demander des statistiques ou des informations sur les régions.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-197">Using hello Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="1b3b3-198">**tooaccess hello HBase Master UI**</span><span class="sxs-lookup"><span data-stu-id="1b3b3-198">**tooaccess hello HBase Master UI**</span></span>

1. <span data-ttu-id="1b3b3-199">L’authentification à hello hello Ambari Web UI à https://&lt;nomcluster >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-199">Sign into hello hello Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="1b3b3-200">Cliquez sur **HBase** à partir du menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-200">Click **HBase** from hello left menu.</span></span>
3. <span data-ttu-id="1b3b3-201">Cliquez sur **liens rapides** hello haut de page hello, point toohello active soigneur nœud lien et puis cliquez sur **HBase Master UI**.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-201">Click **Quick links** on hello top of hello page, point toohello active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="1b3b3-202">l’interface utilisateur de Hello est ouvert dans un autre onglet de navigateur :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-202">hello UI is opened in another browser tab:</span></span>

  ![Interface utilisateur principale HDInsight HBase](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="1b3b3-204">Hello HBase Master UI contient hello les sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-204">hello HBase Master UI contains hello following sections:</span></span>

  - <span data-ttu-id="1b3b3-205">serveurs de région</span><span class="sxs-lookup"><span data-stu-id="1b3b3-205">region servers</span></span>
  - <span data-ttu-id="1b3b3-206">serveurs de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1b3b3-206">backup masters</span></span>
  - <span data-ttu-id="1b3b3-207">tables</span><span class="sxs-lookup"><span data-stu-id="1b3b3-207">tables</span></span>
  - <span data-ttu-id="1b3b3-208">tâches</span><span class="sxs-lookup"><span data-stu-id="1b3b3-208">tasks</span></span>
  - <span data-ttu-id="1b3b3-209">attributs logiciels</span><span class="sxs-lookup"><span data-stu-id="1b3b3-209">software attributes</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="1b3b3-210">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="1b3b3-210">Delete hello cluster</span></span>
<span data-ttu-id="1b3b3-211">des incohérences tooavoid, nous vous conseillons de désactiver les tables HBase hello avant de supprimer le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-211">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="1b3b3-212">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="1b3b3-212">Troubleshoot</span></span>

<span data-ttu-id="1b3b3-213">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="1b3b3-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b3b3-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b3b3-214">Next steps</span></span>
<span data-ttu-id="1b3b3-215">Dans cet article, vous avez appris comment toocreate un cluster HBase et comment afficher et les tables toocreate hello données dans ces tables à partir de hello shell HBase.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-215">In this article, you learned how toocreate an HBase cluster and how toocreate tables and view hello data in those tables from hello HBase shell.</span></span> <span data-ttu-id="1b3b3-216">Vous avez également appris comment toouse une ruche des requêtes sur les données dans les tables HBase et comment toouse hello HBase c# API REST toocreate une table HBase et récupérer des données à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-216">You also learned how toouse a Hive query on data in HBase tables and how toouse hello HBase C# REST APIs toocreate an HBase table and retrieve data from hello table.</span></span>

<span data-ttu-id="1b3b3-217">toolearn, voir :</span><span class="sxs-lookup"><span data-stu-id="1b3b3-217">toolearn more, see:</span></span>

* <span data-ttu-id="1b3b3-218">[Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview] : HBase est une base de données NoSQL open source Apache basée sur Hadoop qui fournit un accès aléatoire et une forte cohérence pour de grandes quantités de données non structurées et semi-structurées.</span><span class="sxs-lookup"><span data-stu-id="1b3b3-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
