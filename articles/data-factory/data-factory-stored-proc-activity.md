---
title: "aaaSQL serveur activité de procédure stockée"
description: "Découvrez comment vous pouvez utiliser l’activité de la procédure stockée SQL Server de hello tooinvoke une procédure stockée dans une base de données SQL Azure ou d’un entrepôt de données SQL Azure à partir d’un pipeline de fabrique de données."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="c8497-103">Activité de procédure stockée SQL Server</span><span class="sxs-lookup"><span data-stu-id="c8497-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="c8497-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="c8497-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="c8497-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="c8497-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="c8497-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="c8497-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="c8497-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="c8497-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="c8497-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="c8497-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="c8497-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c8497-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="c8497-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c8497-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="c8497-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="c8497-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="c8497-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c8497-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="c8497-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="c8497-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="c8497-114">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c8497-114">Overview</span></span>
<span data-ttu-id="c8497-115">Vous utilisez des activités de transformation des données dans une fabrique de données [pipeline](data-factory-create-pipelines.md) tootransform et traitent les données brutes dans des prédictions et des analyses.</span><span class="sxs-lookup"><span data-stu-id="c8497-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="c8497-116">Hello activité de procédure stockée est une des activités de transformation hello qui prend en charge de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="c8497-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="c8497-117">Cet article s’appuie sur hello [activités de transformation des données](data-factory-data-transformation-activities.md) article, qui présente une vue d’ensemble de la transformation des données et des activités de transformation hello pris en charge dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="c8497-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="c8497-118">Vous pouvez utiliser tooinvoke d’activité de procédure stockée hello une procédure stockée dans un des données suivantes de hello stocke dans votre entreprise ou sur une machine virtuelle Azure (VM) :</span><span class="sxs-lookup"><span data-stu-id="c8497-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="c8497-119">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c8497-119">Azure SQL Database</span></span>
- <span data-ttu-id="c8497-120">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c8497-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="c8497-121">Base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="c8497-121">SQL Server Database.</span></span>  <span data-ttu-id="c8497-122">Si vous utilisez SQL Server, installez la passerelle de gestion des données sur le même ordinateur que les ordinateurs hôtes hello de base de données ou sur un ordinateur distinct qui possède la base de données access toohello de hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="c8497-123">La passerelle de gestion des données est un composant qui connecte des sources de données locales ou se trouvant sur une machine virtuelle Azure à des services cloud de manière gérée et sécurisée.</span><span class="sxs-lookup"><span data-stu-id="c8497-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="c8497-124">Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour plus d’informations sur la passerelle.</span><span class="sxs-lookup"><span data-stu-id="c8497-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8497-125">Lors de la copie des données dans la base de données SQL Azure ou SQL Server, vous pouvez configurer hello **SqlSink** dans l’activité de copie tooinvoke une procédure stockée à l’aide de hello **sqlWriterStoredProcedureName** propriété.</span><span class="sxs-lookup"><span data-stu-id="c8497-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="c8497-126">Pour plus de détails, consultez l’article [Appeler une procédure stockée à partir d’une activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="c8497-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="c8497-127">Pour plus d’informations sur la propriété de hello, consultez suivant des articles de connecteur : [base de données SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c8497-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="c8497-128">L’appel d’une procédure stockée lors de la copie de données dans Azure SQL Data Warehouse avec une activité de copie n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c8497-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="c8497-129">Toutefois, vous pouvez utiliser tooinvoke activité de procédure stockée hello une procédure stockée dans un entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="c8497-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="c8497-130">Lors de la copie des données à partir de la base de données SQL Azure ou SQL Server ou entrepôt de données SQL Azure, vous pouvez configurer **SqlSource** dans l’activité de copie tooinvoke un tooread de données de la procédure stockée à partir de la base de données source hello à l’aide de hello  **sqlReaderStoredProcedureName** propriété.</span><span class="sxs-lookup"><span data-stu-id="c8497-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="c8497-131">Pour plus d’informations, consultez hello suivant des articles de connecteur : [base de données SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="c8497-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="c8497-132">Hello, suivant la procédure pas à pas utilise hello activité de procédure stockée dans un pipeline de tooinvoke une procédure stockée dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c8497-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="c8497-133">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="c8497-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="c8497-134">Exemple de table et de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="c8497-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="c8497-135">Créer hello **table** dans votre base de données SQL Azure à l’aide de SQL Server Management Studio ou tout autre outil que vous êtes familiarisé avec.</span><span class="sxs-lookup"><span data-stu-id="c8497-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="c8497-136">colonne de datetimestamp Hello est la date de hello et l’heure à laquelle le code hello correspondante est généré.</span><span class="sxs-lookup"><span data-stu-id="c8497-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="c8497-137">ID est hello unique identifié et hello datetimestamp est date de hello et l’heure à laquelle le code hello correspondante est généré.</span><span class="sxs-lookup"><span data-stu-id="c8497-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![Exemples de données](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="c8497-139">Dans cet exemple, la procédure stockée hello est dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c8497-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="c8497-140">Si hello procédure stockée est dans un entrepôt de données SQL Azure et de la base de données SQL Server, l’approche de hello est similaire.</span><span class="sxs-lookup"><span data-stu-id="c8497-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="c8497-141">Pour une base de données SQL Server, vous devez installer une [passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c8497-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="c8497-142">Créer hello **procédure stockée** qui insère des données dans toohello **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="c8497-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="c8497-143">**Nom** et **casse** Hello paramètre (DateTime dans cet exemple) doit correspondre à celui du paramètre spécifié dans le pipeline/activité hello JSON.</span><span class="sxs-lookup"><span data-stu-id="c8497-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="c8497-144">Dans hello la définition de procédure stockée, vérifiez que  **@**  est utilisé en tant que préfixe pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="c8497-145">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="c8497-145">Create a data factory</span></span>
1. <span data-ttu-id="c8497-146">Connectez-vous trop[portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c8497-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c8497-147">Cliquez sur **nouveau** sur menu gauche hello **Intelligence + Analytique**, puis cliquez sur **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="c8497-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nouvelle fabrique de données](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="c8497-149">Bonjour **nouvelle fabrique de données** panneau, entrez **SProcDF** pour hello nom.</span><span class="sxs-lookup"><span data-stu-id="c8497-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="c8497-150">Les noms Azure Data Factory sont **globalement uniques**.</span><span class="sxs-lookup"><span data-stu-id="c8497-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="c8497-151">Vous avez besoin de nom de hello tooprefix hello fabrique de données avec votre nom, tooenable hello réussi la création de la fabrique de hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![Nouvelle fabrique de données](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="c8497-153">Sélectionnez votre **abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="c8497-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="c8497-154">Pour **groupe de ressources**, effectuez l’une des hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8497-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="c8497-155">Cliquez sur **nouvel** et entrez un nom pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="c8497-156">Cliquez sur **Utiliser l’existant** et sélectionnez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="c8497-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="c8497-157">Sélectionnez hello **emplacement** de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="c8497-158">Sélectionnez **toodashboard du code confidentiel** afin que vous puissiez voir fabrique de données hello sur le tableau de bord hello prochaine ouverture de session dans.</span><span class="sxs-lookup"><span data-stu-id="c8497-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="c8497-159">Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.</span><span class="sxs-lookup"><span data-stu-id="c8497-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="c8497-160">Vous voyez la fabrique de données hello en cours de création dans hello **tableau de bord** de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c8497-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="c8497-161">Une fois que la fabrique de données hello a été créé avec succès, vous voyez page de fabrique de données hello, qui vous indique hello contenu hello fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="c8497-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Page d’accueil Data Factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="c8497-163">Créer un service lié Azure SQL</span><span class="sxs-lookup"><span data-stu-id="c8497-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="c8497-164">Après avoir créé la fabrique de données hello, vous créez un service lié SQL Azure qui lie votre base de données SQL Azure, qui contient la table de sampletable hello et sp_sample stockées procédure, fabrique de données tooyour.</span><span class="sxs-lookup"><span data-stu-id="c8497-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="c8497-165">Cliquez sur **auteur et déployer** sur hello **Data Factory** panneau pour **SProcDF** toolaunch hello éditeur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c8497-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="c8497-166">Cliquez sur **nouveau magasin de données** hello de barre de commandes et choisissez **base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="c8497-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="c8497-167">Vous devez voir le service dans l’éditeur de hello de lié hello script JSON pour la création d’une SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c8497-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![Nouveau magasin de données](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="c8497-169">Bonjour script JSON, apportez hello modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8497-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="c8497-170">Remplacez `<servername>` par nom hello de votre serveur de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c8497-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="c8497-171">Remplacez `<databasename>` avec la base de données hello dans lequel vous avez créé la table de hello et hello la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="c8497-172">Remplacez `<username@servername>` avec un compte d’utilisateur hello qui possède la base de données access toohello.</span><span class="sxs-lookup"><span data-stu-id="c8497-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="c8497-173">Remplacez `<password>` avec mot de passe hello hello compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8497-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![Nouveau magasin de données](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="c8497-175">toodeploy hello service lié, cliquez sur **déployer** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="c8497-176">Vérifiez que vous voyez hello AzureSqlLinkedService dans l’arborescence de hello afficher à gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![arborescence avec service lié](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="c8497-178">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="c8497-178">Create an output dataset</span></span>
<span data-ttu-id="c8497-179">Vous devez spécifier qu'un jeu de données de sortie pour une activité de procédure stockée même si la procédure stockée de hello ne produit pas de données.</span><span class="sxs-lookup"><span data-stu-id="c8497-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="c8497-180">C'est-à-dire, car son hello la sortie de dataset qui gère la planification hello d’activité hello (la fréquence à laquelle hello exécution activité - toutes les heures, tous les jours, etc.).</span><span class="sxs-lookup"><span data-stu-id="c8497-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="c8497-181">Hello dataset de sortie doit utiliser un **service lié** qui fait référence tooan de base de données SQL Azure ou d’un entrepôt de données SQL Azure ou d’une base de données SQL Server dans lequel vous souhaitez hello toorun de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="c8497-182">Hello dataset de sortie puisse agir comme un moyen toopass hello de résultats de la procédure stockée hello pour un traitement ultérieur par une autre activité ([chaînage des propriétés des activités](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="c8497-183">Toutefois, la fabrique de données n’écrit pas automatiquement sortie hello d’un dataset toothis de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="c8497-184">Il est hello table SQL tooa écritures hello points de jeu de données de sortie à procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="c8497-185">Dans certains cas, le jeu de données de sortie hello peut être un **dataset factice** (un dataset qui pointe tooa table qui ne possède pas vraiment le résultat de hello ou procédure stockée).</span><span class="sxs-lookup"><span data-stu-id="c8497-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="c8497-186">Ce jeu de données factice est utilisée uniquement de l’activité de procédure stockée de toospecify hello planification de l’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="c8497-187">Si ce bouton n'est pas affiché dans la barre d'outils, cliquez sur **... Plus** dans la barre d’outils de hello, cliquez sur **nouveau dataset**, puis cliquez sur **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="c8497-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="c8497-188">**Nouveau jeu de données** sur commande hello barre et sélectionnez **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="c8497-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![arborescence avec service lié](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="c8497-190">Copiez-collez hello script JSON dans l’éditeur JSON toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="c8497-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="c8497-191">toodeploy hello du jeu de données, cliquez sur **déployer** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="c8497-192">Vérifiez que vous voyez hello le jeu de données dans l’arborescence hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![arborescence avec services liés](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="c8497-194">Créer un pipeline avec une activité SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="c8497-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="c8497-195">Nous allons maintenant créer un pipeline avec une activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="c8497-196">Notez hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8497-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="c8497-197">Hello **type** propriété a la valeur trop**SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="c8497-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="c8497-198">Hello **storedProcedureName** dans le type de propriétés est défini trop**sp_sample** (nom de hello ou procédure stockée).</span><span class="sxs-lookup"><span data-stu-id="c8497-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="c8497-199">Hello **storedProcedureParameters** section contient un paramètre nommé **DataTime**.</span><span class="sxs-lookup"><span data-stu-id="c8497-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="c8497-200">Nom et la casse du paramètre hello dans JSON doivent correspondre au nom de hello et de la casse du paramètre hello dans la définition de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="c8497-201">Si vous avez besoin de passer null pour un paramètre, utilisez la syntaxe de hello : `"param1": null` (tout en minuscules).</span><span class="sxs-lookup"><span data-stu-id="c8497-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="c8497-202">Si ce bouton n'est pas affiché dans la barre d'outils, cliquez sur **... Plus** hello de barre de commandes et cliquez sur **nouveau pipeline**.</span><span class="sxs-lookup"><span data-stu-id="c8497-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="c8497-203">Copier/coller hello suivant extrait de code JSON :</span><span class="sxs-lookup"><span data-stu-id="c8497-203">Copy/paste hello following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="c8497-204">pipeline de hello toodeploy, cliquez sur **déployer** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="c8497-205">Pipeline d’analyse hello</span><span class="sxs-lookup"><span data-stu-id="c8497-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="c8497-206">Cliquez sur **X** tooclose éditeur Data Factory panneaux et toonavigate Panneau de fabrique de données toohello de sauvegarde, puis cliquez sur **diagramme**.</span><span class="sxs-lookup"><span data-stu-id="c8497-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![vignette schématique](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="c8497-208">Bonjour **vue de diagramme**, vous voyez une vue d’ensemble des pipelines de hello et les datasets utilisés dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c8497-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![vignette schématique](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="c8497-210">Dans la vue de diagramme de hello, double-cliquez sur hello dataset `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="c8497-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="c8497-211">Vous voyez les tranches hello dans l’état Ready.</span><span class="sxs-lookup"><span data-stu-id="c8497-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="c8497-212">Il doit être cinq tranches, car une tranche est produite pour chaque heure entre l’heure de début hello et l’heure de fin de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="c8497-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![vignette schématique](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="c8497-214">Lorsqu’une tranche est dans **prêt** état, exécutez un `select * from sampletable` requête sur tooverify de base de données SQL Azure hello qui hello de données a été inséré dans la table de toohello par la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![Données de sortie](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="c8497-216">Consultez [pipeline d’analyse hello](data-factory-monitor-manage-pipelines.md) pour plus d’informations sur la surveillance des pipelines d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c8497-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="c8497-217">Spécifier un jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="c8497-217">Specify an input dataset</span></span>
<span data-ttu-id="c8497-218">Procédure pas à pas de hello, activité de procédure stockée n’a pas les jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="c8497-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="c8497-219">Si vous spécifiez un jeu de données d’entrée, hello activité de procédure stockée ne s’exécute pas jusqu'à ce que la tranche hello du jeu de données d’entrée est disponible (prêt).</span><span class="sxs-lookup"><span data-stu-id="c8497-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="c8497-220">Hello dataset peut être un jeu de données externe (qui n’est pas produit par une autre activité Bonjour même pipeline) ou un jeu de données interne qui est généré par une activité en amont (activité hello qui s’exécute avant cette activité).</span><span class="sxs-lookup"><span data-stu-id="c8497-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="c8497-221">Vous pouvez spécifier plusieurs jeux de données d’entrée pour l’activité de procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="c8497-222">Si vous le faites, hello activité de procédure stockée s’exécute uniquement quand toutes les tranches de jeu de données d’entrée hello sont disponibles (dans l’état prêt).</span><span class="sxs-lookup"><span data-stu-id="c8497-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="c8497-223">Hello de jeu de données d’entrée ne peut pas être utilisé dans la procédure stockée hello en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="c8497-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="c8497-224">Il est uniquement des dépendances hello toocheck utilisé avant l’activité de procédure stockée de départ hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="c8497-225">Chaînage avec d’autres activités</span><span class="sxs-lookup"><span data-stu-id="c8497-225">Chaining with other activities</span></span>
<span data-ttu-id="c8497-226">Si vous souhaitez toochain une activité en amont avec cette activité, spécifiez la sortie hello d’activité en amont hello en tant qu’entrée de cette activité.</span><span class="sxs-lookup"><span data-stu-id="c8497-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="c8497-227">Lorsque vous procédez ainsi, hello activité de procédure stockée ne s’exécute pas avant l’achèvement d’activité en amont hello et hello dataset de sortie de l’activité en amont hello est disponible (en état « prêt »).</span><span class="sxs-lookup"><span data-stu-id="c8497-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="c8497-228">Vous pouvez spécifier des jeux de données de sortie de plusieurs activités en amont en tant que jeux de données d’entrée de l’activité de procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="c8497-229">Lorsque vous procédez ainsi, à l’activité de procédure stockée de hello s’exécute uniquement quand toutes les tranches de jeu de données d’entrée hello sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="c8497-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="c8497-230">Dans l’exemple suivant de hello, sortie hello de l’activité de copie hello est : activité de procédure stockée de OutputDataset, qui est une entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="c8497-231">Par conséquent, hello activité de procédure stockée ne s’exécute pas avant l’achèvement de l’activité de copie hello et la tranche de OutputDataset hello est disponible (prêt).</span><span class="sxs-lookup"><span data-stu-id="c8497-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="c8497-232">Si vous spécifiez plusieurs jeux de données d’entrée, hello activité de procédure stockée ne s’exécute pas jusqu'à ce que toutes les tranches de jeu de données d’entrée hello sont disponibles (dans l’état prêt).</span><span class="sxs-lookup"><span data-stu-id="c8497-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="c8497-233">Hello de jeux de données d’entrée ne peut pas être utilisé directement en tant qu’activité de procédure stockée de toohello de paramètres.</span><span class="sxs-lookup"><span data-stu-id="c8497-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="c8497-234">Pour plus d’informations sur le chaînage des activités, consultez [Plusieurs activités dans un pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="c8497-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="c8497-235">De même, toolink hello magasin activité de procédure avec **activités en aval** (activités hello exécutent une fois terminée hello activité de procédure stockée), spécifiez le dataset de sortie hello d’activité de procédure stockée hello comme un entrée de l’activité en aval hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8497-236">Lors de la copie des données dans la base de données SQL Azure ou SQL Server, vous pouvez configurer hello **SqlSink** dans l’activité de copie tooinvoke une procédure stockée à l’aide de hello **sqlWriterStoredProcedureName** propriété.</span><span class="sxs-lookup"><span data-stu-id="c8497-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="c8497-237">Pour plus de détails, consultez l’article [Appeler une procédure stockée à partir d’une activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="c8497-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="c8497-238">Pour plus d’informations sur la propriété de hello, consultez hello suivant des articles de connecteur : [base de données SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c8497-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="c8497-239">Lors de la copie des données à partir de la base de données SQL Azure ou SQL Server ou entrepôt de données SQL Azure, vous pouvez configurer **SqlSource** dans l’activité de copie tooinvoke un tooread de données de la procédure stockée à partir de la base de données source hello à l’aide de hello  **sqlReaderStoredProcedureName** propriété.</span><span class="sxs-lookup"><span data-stu-id="c8497-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="c8497-240">Pour plus d’informations, consultez hello suivant des articles de connecteur : [base de données SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="c8497-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="c8497-241">Format JSON</span><span class="sxs-lookup"><span data-stu-id="c8497-241">JSON format</span></span>
<span data-ttu-id="c8497-242">Voici le format JSON de hello pour définir une activité de procédure stockée :</span><span class="sxs-lookup"><span data-stu-id="c8497-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="c8497-243">Hello tableau suivant décrit ces propriétés JSON :</span><span class="sxs-lookup"><span data-stu-id="c8497-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="c8497-244">Propriété</span><span class="sxs-lookup"><span data-stu-id="c8497-244">Property</span></span> | <span data-ttu-id="c8497-245">Description</span><span class="sxs-lookup"><span data-stu-id="c8497-245">Description</span></span> | <span data-ttu-id="c8497-246">Requis</span><span class="sxs-lookup"><span data-stu-id="c8497-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8497-247">name</span><span class="sxs-lookup"><span data-stu-id="c8497-247">name</span></span> | <span data-ttu-id="c8497-248">Nom de l’activité hello</span><span class="sxs-lookup"><span data-stu-id="c8497-248">Name of hello activity</span></span> |<span data-ttu-id="c8497-249">Oui</span><span class="sxs-lookup"><span data-stu-id="c8497-249">Yes</span></span> |
| <span data-ttu-id="c8497-250">description</span><span class="sxs-lookup"><span data-stu-id="c8497-250">description</span></span> |<span data-ttu-id="c8497-251">Texte qui décrit quelle activité hello est utilisé pour</span><span class="sxs-lookup"><span data-stu-id="c8497-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="c8497-252">Non</span><span class="sxs-lookup"><span data-stu-id="c8497-252">No</span></span> |
| <span data-ttu-id="c8497-253">type</span><span class="sxs-lookup"><span data-stu-id="c8497-253">type</span></span> | <span data-ttu-id="c8497-254">Doit être défini sur **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="c8497-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="c8497-255">Oui</span><span class="sxs-lookup"><span data-stu-id="c8497-255">Yes</span></span> |
| <span data-ttu-id="c8497-256">inputs</span><span class="sxs-lookup"><span data-stu-id="c8497-256">inputs</span></span> | <span data-ttu-id="c8497-257">facultatif.</span><span class="sxs-lookup"><span data-stu-id="c8497-257">Optional.</span></span> <span data-ttu-id="c8497-258">Si vous ne spécifiez pas un jeu de données d’entrée, il doit être disponible (en état « Prêt ») pour hello stockées toorun d’activité de procédure.</span><span class="sxs-lookup"><span data-stu-id="c8497-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="c8497-259">Hello de jeu de données d’entrée ne peut pas être utilisé dans la procédure stockée hello en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="c8497-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="c8497-260">Il est uniquement des dépendances hello toocheck utilisé avant l’activité de procédure stockée de départ hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="c8497-261">Non</span><span class="sxs-lookup"><span data-stu-id="c8497-261">No</span></span> |
| <span data-ttu-id="c8497-262">outputs</span><span class="sxs-lookup"><span data-stu-id="c8497-262">outputs</span></span> | <span data-ttu-id="c8497-263">Vous devez spécifier un jeu de données de sortie pour une activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="c8497-264">Dataset de sortie spécifie hello **planification** pour hello stockées activité de procédure (horaire, hebdomadaire, mensuelle, etc.).</span><span class="sxs-lookup"><span data-stu-id="c8497-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="c8497-265">Hello dataset de sortie doit utiliser un **service lié** qui fait référence tooan de base de données SQL Azure ou d’un entrepôt de données SQL Azure ou d’une base de données SQL Server dans lequel vous souhaitez hello toorun de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="c8497-266">Hello dataset de sortie puisse agir comme un moyen toopass hello de résultats de la procédure stockée hello pour un traitement ultérieur par une autre activité ([chaînage des propriétés des activités](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="c8497-267">Toutefois, la fabrique de données n’écrit pas automatiquement sortie hello d’un dataset toothis de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="c8497-268">Il est hello table SQL tooa écritures hello points de jeu de données de sortie à procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="c8497-269">Dans certains cas, le jeu de données de sortie hello peut être un **dataset factice**, qui est utilisé uniquement de l’activité de procédure stockée de toospecify hello planification de l’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="c8497-270">Oui</span><span class="sxs-lookup"><span data-stu-id="c8497-270">Yes</span></span> |
| <span data-ttu-id="c8497-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="c8497-271">storedProcedureName</span></span> |<span data-ttu-id="c8497-272">Spécifiez le nom hello de procédure stockée hello dans la base de données SQL Azure hello ou base de données Azure SQL Data Warehouse ou SQL Server qui est représenté par le service hello lié hello utilisations de table de sortie.</span><span class="sxs-lookup"><span data-stu-id="c8497-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="c8497-273">Oui</span><span class="sxs-lookup"><span data-stu-id="c8497-273">Yes</span></span> |
| <span data-ttu-id="c8497-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="c8497-274">storedProcedureParameters</span></span> |<span data-ttu-id="c8497-275">Spécifiez les valeurs des paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="c8497-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="c8497-276">Si vous avez besoin de toopass null pour un paramètre, utilisez la syntaxe de hello : « param1 » : null (toutes les minuscules).</span><span class="sxs-lookup"><span data-stu-id="c8497-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="c8497-277">Consultez hello suivant toolearn exemple sur l’utilisation de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="c8497-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="c8497-278">Non</span><span class="sxs-lookup"><span data-stu-id="c8497-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="c8497-279">Transmission d’une valeur statique</span><span class="sxs-lookup"><span data-stu-id="c8497-279">Passing a static value</span></span>
<span data-ttu-id="c8497-280">Maintenant, prenons l’exemple d’ajout d’une autre colonne nommée « Scénario » dans la table hello contenant une valeur statique est appelée « Exemple de Document ».</span><span class="sxs-lookup"><span data-stu-id="c8497-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![Exemple de données 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="c8497-282">**Table :**</span><span class="sxs-lookup"><span data-stu-id="c8497-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="c8497-283">**Procédure stockée**</span><span class="sxs-lookup"><span data-stu-id="c8497-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="c8497-284">À présent, passez hello **scénario** activité de procédure stockée de valeur de paramètre et hello de hello.</span><span class="sxs-lookup"><span data-stu-id="c8497-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="c8497-285">Hello **typeProperties** section Bonjour précédent exemple ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="c8497-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="c8497-286">**Jeu de données Data Factory :**</span><span class="sxs-lookup"><span data-stu-id="c8497-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="c8497-287">**Pipeline Data Factory**</span><span class="sxs-lookup"><span data-stu-id="c8497-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```