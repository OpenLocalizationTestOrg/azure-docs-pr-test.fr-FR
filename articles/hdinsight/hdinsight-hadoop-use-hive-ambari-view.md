---
title: toowork de vues de Ambari aaaUse avec Hive dans HDInsight (Hadoop) - Azure | Documents Microsoft
description: "Découvrez comment toouse hello Hive une vue à partir de vos requêtes de ruche de toosubmit de navigateur web. Hello, vue de la ruche fait partie de hello que l’interface utilisateur de Ambari Web fourni avec votre cluster HDInsight de basés sur Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="d4600-104">Utilisez hello Hive une vue avec Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4600-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="d4600-105">Découvrez comment toorun ruche interroge l’affichage de la ruche Ambari.</span><span class="sxs-lookup"><span data-stu-id="d4600-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="d4600-106">Ambari est un utilitaire de gestion et de surveillance fourni avec les clusters HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="d4600-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="d4600-107">Une des fonctionnalités hello fournies via Ambari est une interface utilisateur Web qui peuvent être des requêtes de ruche toorun utilisé.</span><span class="sxs-lookup"><span data-stu-id="d4600-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="d4600-108">Ambari offre de nombreuses fonctionnalités qui ne sont pas traitées dans ce document.</span><span class="sxs-lookup"><span data-stu-id="d4600-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="d4600-109">Pour plus d’informations, consultez [HDInsight de gérer des clusters à l’aide de hello l’interface utilisateur de Ambari Web](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="d4600-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4600-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d4600-110">Prerequisites</span></span>

* <span data-ttu-id="d4600-111">Un cluster HDInsight sous Linux</span><span class="sxs-lookup"><span data-stu-id="d4600-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d4600-112">Pour plus d’informations sur la création d’un cluster, consultez [Prise en main de HDInsight sous Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d4600-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4600-113">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="d4600-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="d4600-114">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="d4600-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d4600-115">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d4600-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="d4600-116">Afficher la ruche hello</span><span class="sxs-lookup"><span data-stu-id="d4600-116">Open hello Hive view</span></span>

<span data-ttu-id="d4600-117">Vous pouvez les vues Ambari de hello portail Azure ; Sélectionnez votre cluster HDInsight, puis **Ambari vues** de hello **liens rapides** section.</span><span class="sxs-lookup"><span data-stu-id="d4600-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![section des liens rapides du portail de hello](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="d4600-119">Dans la liste hello des vues, sélectionnez hello __affichage de la ruche__.</span><span class="sxs-lookup"><span data-stu-id="d4600-119">From hello list of views, select hello __Hive View__.</span></span>

![Hello vue ruche sélectionnée](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="d4600-121">Lors de l’accès Ambari, vous êtes invité à tooauthenticate toohello site.</span><span class="sxs-lookup"><span data-stu-id="d4600-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="d4600-122">Entrez hello admin (valeur par défaut `admin`) compte nom et mot de passe utilisé lors de la création de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="d4600-123">Vous devez voir un toohello similaire de page suivant l’image :</span><span class="sxs-lookup"><span data-stu-id="d4600-123">You should see a page similar toohello following image:</span></span>

![Image de la feuille de calcul hello requête de vue de ruche hello](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="d4600-125"><a name="hivequery"></a>Exécuter une requête</span><span class="sxs-lookup"><span data-stu-id="d4600-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="d4600-126">toorun une requête hive, utilisez hello comme suit à partir de la vue de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="d4600-127">À partir de hello __requête__ onglet, collez hello suivant les instructions HiveQL dans la feuille de calcul hello :</span><span class="sxs-lookup"><span data-stu-id="d4600-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="d4600-128">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="d4600-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="d4600-129">`DROP TABLE`-Supprime la table de hello et fichier de données hello, au cas où la table hello existe déjà.</span><span class="sxs-lookup"><span data-stu-id="d4600-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="d4600-130">`CREATE EXTERNAL TABLE` : crée une nouvelle table « externe » dans Hive.</span><span class="sxs-lookup"><span data-stu-id="d4600-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="d4600-131">Tables externes stockent uniquement la définition de table hello dans la ruche.</span><span class="sxs-lookup"><span data-stu-id="d4600-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="d4600-132">les données de salutation reste dans l’emplacement d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="d4600-133">`ROW FORMAT`-Comment les données de salutation sont mis en forme.</span><span class="sxs-lookup"><span data-stu-id="d4600-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="d4600-134">Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="d4600-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="d4600-135">`STORED AS TEXTFILE LOCATION`-Où sont stockées les données de hello et qu’elle est stockée sous forme de texte.</span><span class="sxs-lookup"><span data-stu-id="d4600-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="d4600-136">`SELECT`-Sélectionne un nombre de toutes les lignes où t4 de colonne contient la valeur de hello [erreur].</span><span class="sxs-lookup"><span data-stu-id="d4600-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="d4600-137">Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe.</span><span class="sxs-lookup"><span data-stu-id="d4600-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="d4600-138">par exemple, par un processus de téléchargement de données automatisé ou une autre opération MapReduce.</span><span class="sxs-lookup"><span data-stu-id="d4600-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="d4600-139">Suppression d’une table externe est *pas* supprimer les données de hello, uniquement la définition de table hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d4600-140">Laissez hello __base de données__ sélection à __par défaut__.</span><span class="sxs-lookup"><span data-stu-id="d4600-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="d4600-141">des exemples de Hello dans ce document utilisent la base de données par défaut hello inclus avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4600-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="d4600-142">requête de hello toostart, utilisez hello **Execute** situé sous la feuille de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="d4600-143">Il désactive les modifications de texte orange et hello trop**arrêter**.</span><span class="sxs-lookup"><span data-stu-id="d4600-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="d4600-144">Une fois la requête hello est terminée, hello **résultats** onglet affiche les résultats de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="d4600-145">Hello suivant le texte est résultat hello de requête de hello :</span><span class="sxs-lookup"><span data-stu-id="d4600-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="d4600-146">Hello **journaux** onglet peut être des informations de journalisation utilisé tooview hello créées par le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="d4600-147">Hello **enregistrer les résultats** liste déroulante de boîte de dialogue de hello supérieur gauche de hello **résultats du processus de requête** section vous permet de toodownload ou enregistrer les résultats.</span><span class="sxs-lookup"><span data-stu-id="d4600-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="d4600-148">Sélectionnez hello quatre premières lignes de cette requête, puis sélectionnez **Execute**.</span><span class="sxs-lookup"><span data-stu-id="d4600-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="d4600-149">Notez qu’il n’y a aucun résultat hello travail une fois.</span><span class="sxs-lookup"><span data-stu-id="d4600-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="d4600-150">À l’aide de hello **Execute** bouton lorsqu’il fait partie de la requête de hello est sélectionné uniquement s’exécute hello instructions sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="d4600-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="d4600-151">Dans ce cas, la sélection hello n’inclure hello dernière instruction qui extrait des lignes de table de hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="d4600-152">Si vous sélectionnez uniquement cette ligne et utilisez **Execute**, vous devez voir les résultats de hello attendu.</span><span class="sxs-lookup"><span data-stu-id="d4600-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="d4600-153">tooadd une feuille de calcul, utilisez hello **nouvelle feuille de calcul** bouton bas hello hello **l’éditeur de requête**.</span><span class="sxs-lookup"><span data-stu-id="d4600-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="d4600-154">Dans hello nouvelle feuille de calcul, entrez hello suivant les instructions HiveQL :</span><span class="sxs-lookup"><span data-stu-id="d4600-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="d4600-155">Ces instructions effectuent hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="d4600-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="d4600-156">**CREATE TABLE IF NOT EXISTS** : crée une table, si elle n'existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="d4600-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="d4600-157">Depuis hello **externe** mot clé n’est pas utilisé, une table interne est créée.</span><span class="sxs-lookup"><span data-stu-id="d4600-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="d4600-158">Une table interne est stockée dans l’entrepôt de données Hive hello et entièrement gérée par ruche.</span><span class="sxs-lookup"><span data-stu-id="d4600-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="d4600-159">Contrairement aux tables externes, la suppression d’une table interne supprime également des données sous-jacentes hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="d4600-160">**ORC de AS stockées** -stocke les données de hello dans format optimisé lignes en colonnes (ORC).</span><span class="sxs-lookup"><span data-stu-id="d4600-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="d4600-161">ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.</span><span class="sxs-lookup"><span data-stu-id="d4600-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="d4600-162">**INSERT OVERWRITE ... Sélectionnez** -sélectionne des lignes à partir de hello **log4jLogs** table qui contiennent des `[ERROR]`, et puis insertions hello des données dans hello **journaux d’erreurs de** table.</span><span class="sxs-lookup"><span data-stu-id="d4600-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="d4600-163">Hello d’utilisation **Execute** bouton toorun cette requête.</span><span class="sxs-lookup"><span data-stu-id="d4600-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="d4600-164">Hello **résultats** onglet ne contient pas d’informations lors de la requête de hello retourne zéro ligne.</span><span class="sxs-lookup"><span data-stu-id="d4600-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="d4600-165">état de Hello doit être **SUCCEEDED** une fois la requête de hello terminée.</span><span class="sxs-lookup"><span data-stu-id="d4600-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="d4600-166">Visual Explain</span><span class="sxs-lookup"><span data-stu-id="d4600-166">Visual explain</span></span>

<span data-ttu-id="d4600-167">toodisplay une visualisation hello du plan de requête, sélectionnez hello **expliquent Visual** onglet au-dessous de feuille de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="d4600-168">Hello **expliquent Visual** vue de requête de hello peut être utile de comprendre le flux hello de requêtes complexes.</span><span class="sxs-lookup"><span data-stu-id="d4600-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="d4600-169">Vous pouvez afficher un équivalent textuel de cette vue à l’aide de hello **expliquer** bouton Bonjour éditeur de requête.</span><span class="sxs-lookup"><span data-stu-id="d4600-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="d4600-170">Interface utilisateur Tez</span><span class="sxs-lookup"><span data-stu-id="d4600-170">Tez UI</span></span>

<span data-ttu-id="d4600-171">toodisplay hello Tez UI pour requête hello, sélectionnez hello **Tez** onglet au-dessous de feuille de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="d4600-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4600-172">Tez est tooresolve non utilisé toutes les requêtes.</span><span class="sxs-lookup"><span data-stu-id="d4600-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="d4600-173">De nombreuses requêtes peuvent être résolues sans utiliser Tez.</span><span class="sxs-lookup"><span data-stu-id="d4600-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="d4600-174">Si Tez était une requête de hello tooresolve utilisé, hello graphique acyclique dirigé (DAG) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d4600-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="d4600-175">Si vous souhaitez tooview hello DAG pour les requêtes, vous avez exécuté Bonjour passées ou déboguez hello Tez processus, utilisez hello [Tez vue](hdinsight-debug-ambari-tez-view.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="d4600-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="d4600-176">Afficher l’historique des tâches</span><span class="sxs-lookup"><span data-stu-id="d4600-176">View job history</span></span>

<span data-ttu-id="d4600-177">Hello __travaux__ onglet affiche un historique des requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="d4600-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Image de l’historique des travaux hello](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="d4600-179">Tables de base de données</span><span class="sxs-lookup"><span data-stu-id="d4600-179">Database tables</span></span>

<span data-ttu-id="d4600-180">Vous pouvez utiliser hello __Tables__ onglet toowork avec des tables dans une base de données de la ruche.</span><span class="sxs-lookup"><span data-stu-id="d4600-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Image de l’onglet de tables hello](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="d4600-182">Requêtes enregistrées</span><span class="sxs-lookup"><span data-stu-id="d4600-182">Saved queries</span></span>

<span data-ttu-id="d4600-183">À partir de l’onglet de requête hello, vous pouvez éventuellement enregistrer des requêtes.</span><span class="sxs-lookup"><span data-stu-id="d4600-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="d4600-184">Une fois enregistré, vous pouvez réutiliser des requêtes hello de hello __requêtes enregistrées__ onglet.</span><span class="sxs-lookup"><span data-stu-id="d4600-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![Image de l’onglet de requêtes enregistrées](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="d4600-186">Fonctions définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d4600-186">User-defined functions</span></span>

<span data-ttu-id="d4600-187">Hive peut également être étendu via des fonctions définies par l'utilisateur (UDF).</span><span class="sxs-lookup"><span data-stu-id="d4600-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="d4600-188">Un fichier UDF vous permet de tooimplement de fonctionnalité ou logique qui n’est pas facilement être modelée dans HiveQL.</span><span class="sxs-lookup"><span data-stu-id="d4600-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="d4600-189">Hello onglet UDF haut hello hello la ruche de vue vous permet de toodeclare et enregistrer des UDF.</span><span class="sxs-lookup"><span data-stu-id="d4600-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="d4600-190">Ces fonctions UDF peuvent être utilisés avec hello **l’éditeur de requête**.</span><span class="sxs-lookup"><span data-stu-id="d4600-190">These UDFs can be used with hello **Query Editor**.</span></span>

![Image de l’onglet UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="d4600-192">Une fois que vous avez ajouté une toohello définie par l’affichage de la ruche, un **insérer UDF** bouton apparaît au bas de hello de hello **l’éditeur de requête**.</span><span class="sxs-lookup"><span data-stu-id="d4600-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="d4600-193">Cette entrée affiche une liste déroulante de hello UDF définis dans hello vue de la ruche.</span><span class="sxs-lookup"><span data-stu-id="d4600-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="d4600-194">Sélection d’un fichier UDF ajoute HiveQL instructions tooyour requête tooenable hello UDF.</span><span class="sxs-lookup"><span data-stu-id="d4600-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="d4600-195">Par exemple, si vous avez défini une UDF avec hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4600-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="d4600-196">Nom de ressource : myudfs</span><span class="sxs-lookup"><span data-stu-id="d4600-196">Resource name: myudfs</span></span>

* <span data-ttu-id="d4600-197">Chemin d’accès à la ressource : /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="d4600-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="d4600-198">Nom de la fonction UDF : myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="d4600-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="d4600-199">Nom de la classe UDF : com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="d4600-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="d4600-200">À l’aide de hello **insérer UDF** bouton affiche une entrée nommée **myudfs**, avec une autre liste déroulante pour chaque UDF défini pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="d4600-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="d4600-201">Dans le cas présent, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="d4600-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="d4600-202">La sélection de cette entrée ajoute hello suivant début toohello de requête de hello :</span><span class="sxs-lookup"><span data-stu-id="d4600-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="d4600-203">Vous pouvez ensuite utiliser hello UDF dans votre requête.</span><span class="sxs-lookup"><span data-stu-id="d4600-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="d4600-204">Par exemple, `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="d4600-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="d4600-205">Pour plus d’informations sur l’utilisation des UDF avec Hive dans HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="d4600-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="d4600-206">Utilisation de Python avec Hive et Pig dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4600-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="d4600-207">Comment tooadd un tooHDInsight UDF de la ruche personnalisé</span><span class="sxs-lookup"><span data-stu-id="d4600-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="d4600-208">Paramètres Hive</span><span class="sxs-lookup"><span data-stu-id="d4600-208">Hive settings</span></span>

<span data-ttu-id="d4600-209">Les paramètres peuvent être utilisé toochange différents paramètres de la ruche.</span><span class="sxs-lookup"><span data-stu-id="d4600-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="d4600-210">Par exemple, remplaçant moteur d’exécution hello pour la ruche Tez (valeur par défaut de hello) tooMapReduce.</span><span class="sxs-lookup"><span data-stu-id="d4600-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="d4600-211"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4600-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="d4600-212">Pour obtenir des informations générales sur Hive dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4600-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="d4600-213">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4600-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="d4600-214">Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="d4600-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="d4600-215">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4600-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d4600-216">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4600-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
