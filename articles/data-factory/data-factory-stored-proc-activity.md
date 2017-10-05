---
title: "Activité de procédure stockée SQL Server"
description: "Découvrez comment utiliser l'activité de procédure stockée SQL Server pour appeler une procédure stockée dans une base de données SQL Azure ou un entrepôt Azure SQL Data Warehouse à partir d'un pipeline Data Factory."
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
ms.openlocfilehash: 6505d9aa2c7ae003bd928e2fa82cd923a9615394
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="4f6d1-103">Activité de procédure stockée SQL Server</span><span class="sxs-lookup"><span data-stu-id="4f6d1-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4f6d1-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="4f6d1-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="4f6d1-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="4f6d1-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4f6d1-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="4f6d1-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4f6d1-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="4f6d1-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4f6d1-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="4f6d1-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4f6d1-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4f6d1-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4f6d1-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4f6d1-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4f6d1-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="4f6d1-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4f6d1-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4f6d1-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4f6d1-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="4f6d1-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="4f6d1-114">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4f6d1-114">Overview</span></span>
<span data-ttu-id="4f6d1-115">Vous utilisez des activités de transformation dans un [pipeline](data-factory-create-pipelines.md) Data Factory pour transformer et traiter des données brutes en prévisions et en analyses.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="4f6d1-116">L’activité de procédure stockée est l’une des activités de transformation prises en charge par Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-116">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="4f6d1-117">Cet article s'appuie sur l'article [Activités de transformation des données](data-factory-data-transformation-activities.md) qui présente une vue d'ensemble de la transformation des données et les activités de transformation prises en charge dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="4f6d1-118">Vous pouvez utiliser l’activité de procédure stockée pour appeler une procédure stockée dans l’une des banques de données suivantes dans votre entreprise ou sur une machine virtuelle Azure :</span><span class="sxs-lookup"><span data-stu-id="4f6d1-118">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="4f6d1-119">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4f6d1-119">Azure SQL Database</span></span>
- <span data-ttu-id="4f6d1-120">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4f6d1-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="4f6d1-121">Base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="4f6d1-121">SQL Server Database.</span></span>  <span data-ttu-id="4f6d1-122">Si vous utilisez SQL Server, installez la passerelle de gestion des données sur l’ordinateur qui héberge la base de données ou sur un autre ordinateur ayant accès à la base de données.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-122">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="4f6d1-123">La passerelle de gestion des données est un composant qui connecte des sources de données locales ou se trouvant sur une machine virtuelle Azure à des services cloud de manière gérée et sécurisée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="4f6d1-124">Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour plus d’informations sur la passerelle.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f6d1-125">Lorsque vous copiez des données dans Azure SQL Database ou SQL Server, vous pouvez configurer l’élément **SqlSink** dans l’activité de copie pour appeler une procédure stockée en utilisant la propriété **sqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-125">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="4f6d1-126">Pour plus de détails, consultez l’article [Appeler une procédure stockée à partir d’une activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="4f6d1-127">Pour plus d’informations sur la propriété, consultez les articles suivants sur les connecteurs : [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-127">For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="4f6d1-128">L’appel d’une procédure stockée lors de la copie de données dans Azure SQL Data Warehouse avec une activité de copie n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="4f6d1-129">Toutefois, vous pouvez utiliser l’activité de procédure stockée pour appeler une procédure stockée dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-129">But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="4f6d1-130">Lors de la copie de données à partir d’Azure SQL Database, SQL Server ou Azure SQL Data Warehouse, vous pouvez configurer **SqlSource** dans l’activité de copie pour appeler une procédure stockée afin de lire les données à partir de la base de données source en utilisant la propriété **sqlReaderStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="4f6d1-131">Pour plus d’informations, consultez les articles suivants sur les connecteurs : [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="4f6d1-131">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="4f6d1-132">La procédure pas à pas suivante utilise l’activité de procédure stockée dans un pipeline pour appeler une procédure stockée dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-132">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="4f6d1-133">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="4f6d1-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="4f6d1-134">Exemple de table et de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="4f6d1-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="4f6d1-135">Créez la **table** suivante dans votre base de données SQL Azure à l’aide de SQL Server Management Studio ou d’un autre outil que vous maîtrisez.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-135">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="4f6d1-136">La colonne datetimestamp affiche la date et l’heure auxquelles l’ID correspondant est généré.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-136">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

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
    <span data-ttu-id="4f6d1-137">La colonne ID affiche l’identifiant unique et la colonne datetimestamp affiche la date et l’heure auxquelles l’ID correspondant est généré.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-137">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![Exemples de données](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="4f6d1-139">Dans cet exemple, la procédure stockée est dans Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-139">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="4f6d1-140">Si elle est dans Azure SQL Data Warehouse et dans SQL Server Database, l’approche est la même.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-140">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="4f6d1-141">Pour une base de données SQL Server, vous devez installer une [passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="4f6d1-142">Créez la **procédure stockée** suivante qui insère des données dans la table **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-142">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="4f6d1-143">Le **nom** et la **casse** du paramètre (DateTime dans cet exemple) doivent correspondre à ceux du paramètre spécifié dans le script JSON de l’activité/du pipeline.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-143">**Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON.</span></span> <span data-ttu-id="4f6d1-144">Dans la définition de procédure stockée, vérifiez que **@** est utilisé en tant que préfixe pour le paramètre.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-144">In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="4f6d1-145">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="4f6d1-145">Create a data factory</span></span>
1. <span data-ttu-id="4f6d1-146">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-146">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4f6d1-147">Cliquez sur **NOUVEAU** dans le menu de gauche, puis sur **Intelligence + analyse** et sur **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-147">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nouvelle fabrique de données](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="4f6d1-149">Dans le panneau **Nouvelle fabrique de données**, entrez **SProcDF** dans le champ Nom.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-149">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="4f6d1-150">Les noms Azure Data Factory sont **globalement uniques**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="4f6d1-151">Vous devez faire précéder le nom de la fabrique de données par votre nom, pour activer la création de la fabrique.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-151">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![Nouvelle fabrique de données](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="4f6d1-153">Sélectionnez votre **abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="4f6d1-154">Pour **Groupe de ressources**, effectuez l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f6d1-154">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="4f6d1-155">Cliquez sur **Créer un nouveau** et entrez un nom pour le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-155">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="4f6d1-156">Cliquez sur **Utiliser l’existant** et sélectionnez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="4f6d1-157">Sélectionnez **l’emplacement** de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-157">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="4f6d1-158">Sélectionnez **Épingler au tableau de bord** pour afficher la fabrique de données dans le tableau de bord la prochaine fois que vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-158">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="4f6d1-159">Cliquez sur **Créer** dans le panneau **Nouvelle fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-159">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="4f6d1-160">La fabrique de données apparaît comme étant en cours de création dans le **tableau de bord** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-160">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="4f6d1-161">Une fois la fabrique de données créée, la page correspondante s’affiche et indique son contenu.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-161">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Page d’accueil Data Factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="4f6d1-163">Créer un service lié Azure SQL</span><span class="sxs-lookup"><span data-stu-id="4f6d1-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="4f6d1-164">Après avoir créé la fabrique de données, vous créez un service lié Azure SQL reliant votre base de données Azure SQL, qui contient la table sampletable et la procédure stockée sp_sample, à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-164">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="4f6d1-165">Dans le panneau **Fabrique de données**, cliquez sur **Créer et déployer** pour que **SProcDF** lance l’éditeur de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-165">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="4f6d1-166">Cliquez sur **Nouvelle banque de données** dans la barre de commandes et choisissez **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-166">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="4f6d1-167">Le script JSON de création d’un service lié Azure SQL doit apparaître dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-167">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![Nouveau magasin de données](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="4f6d1-169">Dans le script JSON, apportez les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f6d1-169">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="4f6d1-170">Remplacez `<servername>` par le nom de votre serveur Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-170">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="4f6d1-171">Remplacez `<databasename>` par la base de données dans laquelle vous avez créé la table et la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-171">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="4f6d1-172">Remplacez `<username@servername>` par le compte d’utilisateur qui a accès à la base de données.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-172">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="4f6d1-173">Remplacez `<password>` par le mot de passe du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-173">Replace `<password>` with the password for the user account.</span></span>

      ![Nouveau magasin de données](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="4f6d1-175">Pour déployer le service lié, cliquez sur **Déployer** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-175">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="4f6d1-176">Vérifiez que AzureSqlLinkedService apparaît dans l’arborescence à gauche.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-176">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![arborescence avec service lié](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="4f6d1-178">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="4f6d1-178">Create an output dataset</span></span>
<span data-ttu-id="4f6d1-179">Vous devez spécifier un jeu de données de sortie pour une activité de procédure stockée même si la procédure stockée ne génère aucune donnée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-179">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="4f6d1-180">C’est parce qu’il s’agit du jeu de données de sortie qui pilote le calendrier de l’activité (fréquence d’exécution de l’activité : horaire, quotidienne, etc.).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-180">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="4f6d1-181">Le jeu de données de sortie doit utiliser un **service lié** qui fait référence à une base de données Azure SQL, à un Azure SQL Data Warehouse ou à une base de données SQL Server dans laquelle vous souhaitez que la procédure stockée soit exécutée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-181">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="4f6d1-182">Le jeu de données de sortie peut être un moyen de passer le résultat de la procédure stockée pour traitement ultérieur par une autre activité ([chaînage des activités](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)) dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-182">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="4f6d1-183">Toutefois, Data Factory n’écrit pas automatiquement la sortie d’une procédure stockée pour ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-183">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="4f6d1-184">C’est la procédure stockée qui écrit dans une table SQL vers laquelle le jeu de données de sortie pointe.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-184">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="4f6d1-185">Dans certains cas, le jeu de données de sortie peut être un **jeu de données factice** (un jeu de données qui pointe vers une table qui ne possède pas vraiment de sortie de la procédure stockée).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-185">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="4f6d1-186">Ce jeu de données factice est utilisé uniquement pour spécifier le calendrier d’exécution de l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-186">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="4f6d1-187">Si ce bouton n'est pas affiché dans la barre d'outils, cliquez sur **... Plus** dans la barre d’outils, sur **Nouveau jeu de données**, puis sur **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-187">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="4f6d1-188">Cliquez sur **Nouveau jeu de données** dans la barre de commandes et sélectionnez **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-188">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![arborescence avec service lié](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="4f6d1-190">Copiez-collez le script JSON suivant dans l’éditeur JSON.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-190">Copy/paste the following JSON script in to the JSON editor.</span></span>

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
3. <span data-ttu-id="4f6d1-191">Pour déployer le jeu de données, cliquez sur **Déployer** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-191">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="4f6d1-192">Vérifiez que le jeu de données apparaît dans l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-192">Confirm that you see the dataset in the tree view.</span></span>

    ![arborescence avec services liés](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="4f6d1-194">Créer un pipeline avec une activité SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="4f6d1-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="4f6d1-195">Nous allons maintenant créer un pipeline avec une activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="4f6d1-196">Notez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f6d1-196">Notice the following properties:</span></span> 

- <span data-ttu-id="4f6d1-197">La propriété **type** doit être définie sur **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-197">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="4f6d1-198">Le paramètre **storedProcedureName** dans les propriétés type est défini sur **sp_sample** (nom de la procédure stockée).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-198">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="4f6d1-199">La section **storedProcedureParameters** contient un paramètre nommé **DataTime**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-199">The **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="4f6d1-200">Le nom et la casse du paramètre dans JSON doivent correspondre à ceux du paramètre dans la définition de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-200">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="4f6d1-201">Si vous avez besoin d’utiliser la valeur null pour un paramètre, utilisez la syntaxe : `"param1": null` (tout en minuscules).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-201">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="4f6d1-202">Si ce bouton n'est pas affiché dans la barre d'outils, cliquez sur **... Plus** dans la barre de commandes et sur **Nouveau pipeline**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-202">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="4f6d1-203">Copiez-collez l’extrait de code JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="4f6d1-203">Copy/paste the following JSON snippet:</span></span>   

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
3. <span data-ttu-id="4f6d1-204">Pour déployer le pipeline, cliquez sur **Déployer** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-204">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="4f6d1-205">Surveiller le pipeline</span><span class="sxs-lookup"><span data-stu-id="4f6d1-205">Monitor the pipeline</span></span>
1. <span data-ttu-id="4f6d1-206">Cliquez sur **X** pour fermer les panneaux de Data Factory Editor et revenir au panneau Data Factory, puis cliquez sur **Diagramme**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-206">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![vignette schématique](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="4f6d1-208">Dans la **Vue de diagramme**, une vue d’ensemble des pipelines et des jeux de données utilisés dans ce didacticiel s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-208">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![vignette schématique](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="4f6d1-210">Dans la vue de diagramme, double-cliquez sur le jeu de données `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-210">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="4f6d1-211">Les tranches s’affichent avec l’état Prêt.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-211">You see the slices in Ready state.</span></span> <span data-ttu-id="4f6d1-212">Il doit y avoir cinq tranches, car une tranche est produite pour chaque heure entre l’heure de début et l’heure de fin dans le JSON.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-212">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![vignette schématique](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="4f6d1-214">Quand une tranche est à l’état **Prêt**, exécutez une requête `select * from sampletable` sur la base de données SQL Azure pour vérifier que les données ont été insérées dans la table par la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-214">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![Données de sortie](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="4f6d1-216">Consultez [Surveiller le pipeline](data-factory-monitor-manage-pipelines.md) pour plus d’informations sur la surveillance des pipelines Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-216">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="4f6d1-217">Spécifier un jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="4f6d1-217">Specify an input dataset</span></span>
<span data-ttu-id="4f6d1-218">Dans la procédure pas à pas, l’activité de procédure stockée n’a pas de jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-218">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="4f6d1-219">Si vous spécifiez un jeu de données d’entrée, l’activité de procédure stockée ne s’exécute pas tant que la tranche du jeu de données d’entrée n’est pas disponible (à l’état Prêt).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-219">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="4f6d1-220">Le jeu de données peut être un jeu de données externe (non généré par une autre activité dans le même pipeline) ou un jeu de données interne généré par une activité en amont (l’activité qui s’exécute avant cette activité).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-220">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="4f6d1-221">Vous pouvez spécifier plusieurs jeux de données d’entrée pour l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-221">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="4f6d1-222">Si vous procédez ainsi, l’activité de procédure stockée ne s’exécute que lorsque toutes les tranches du jeu de données d’entrée sont disponibles (à l’état Prêt).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-222">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="4f6d1-223">Les jeux de données d’entrée ne peuvent pas être utilisés dans la procédure stockée en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-223">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="4f6d1-224">Cela sert uniquement à vérifier la dépendance avant de commencer l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-224">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="4f6d1-225">Chaînage avec d’autres activités</span><span class="sxs-lookup"><span data-stu-id="4f6d1-225">Chaining with other activities</span></span>
<span data-ttu-id="4f6d1-226">Si vous souhaitez chaîner une activité en amont avec cette activité, spécifiez la sortie de l’activité en amont en tant qu’entrée de cette activité.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-226">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="4f6d1-227">Lorsque vous procédez ainsi, l’activité de procédure stockée ne s’exécute pas tant que l’activité en amont n’est pas terminée et que le jeu de données de sortie de l’activité en amont n’est pas disponible (à l’état Prêt).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-227">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="4f6d1-228">Vous pouvez spécifier des jeux de données de sortie de plusieurs activités en amont comme jeux de données d’entrée de l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-228">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="4f6d1-229">Lorsque vous procédez ainsi, l’activité de procédure stockée ne s’exécute que lorsque toutes les tranches du jeu de données d’entrée sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-229">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="4f6d1-230">Dans l’exemple suivant, la sortie de l’activité de copie est : OutputDataset, qui est une entrée de l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-230">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="4f6d1-231">Par conséquent, l’activité de procédure stockée ne s’exécute pas tant que l’activité de copie n’est pas disponible et que la tranche OutputDataset n’est pas disponible (à l’état Prêt).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-231">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="4f6d1-232">Si vous spécifiez plusieurs jeux de données d’entrée, l’activité de procédure stockée ne s’exécute pas tant que toutes les tranches du jeu de données d’entrée ne sont pas disponibles (à l’état Prêt).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-232">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="4f6d1-233">Les jeux de données d’entrée ne peuvent pas servir directement de paramètres pour l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-233">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="4f6d1-234">Pour plus d’informations sur le chaînage des activités, consultez [Plusieurs activités dans un pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="4f6d1-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
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

<span data-ttu-id="4f6d1-235">De même, pour lier l’activité de procédure stockée avec des **activités en aval** (activités qui s’exécutent une fois l’activité de procédure stockée terminée), spécifiez le jeu de données de sortie de l’activité de procédure stockée en tant qu’entrée de l’activité en aval dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-235">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f6d1-236">Lorsque vous copiez des données dans Azure SQL Database ou SQL Server, vous pouvez configurer l’élément **SqlSink** dans l’activité de copie pour appeler une procédure stockée en utilisant la propriété **sqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-236">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="4f6d1-237">Pour plus de détails, consultez l’article [Appeler une procédure stockée à partir d’une activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="4f6d1-238">Pour plus d’informations sur la propriété, consultez les articles suivants sur les connecteurs : [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-238">For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="4f6d1-239">Lors de la copie de données à partir d’Azure SQL Database, SQL Server ou Azure SQL Data Warehouse, vous pouvez configurer **SqlSource** dans l’activité de copie pour appeler une procédure stockée afin de lire les données à partir de la base de données source en utilisant la propriété **sqlReaderStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="4f6d1-240">Pour plus d’informations, consultez les articles suivants sur les connecteurs : [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="4f6d1-240">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="4f6d1-241">Format JSON</span><span class="sxs-lookup"><span data-stu-id="4f6d1-241">JSON format</span></span>
<span data-ttu-id="4f6d1-242">Voici le format JSON pour la définition d’une activité de procédure stockée :</span><span class="sxs-lookup"><span data-stu-id="4f6d1-242">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="4f6d1-243">Le tableau suivant décrit ces paramètres JSON :</span><span class="sxs-lookup"><span data-stu-id="4f6d1-243">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="4f6d1-244">Propriété</span><span class="sxs-lookup"><span data-stu-id="4f6d1-244">Property</span></span> | <span data-ttu-id="4f6d1-245">Description</span><span class="sxs-lookup"><span data-stu-id="4f6d1-245">Description</span></span> | <span data-ttu-id="4f6d1-246">Requis</span><span class="sxs-lookup"><span data-stu-id="4f6d1-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f6d1-247">name</span><span class="sxs-lookup"><span data-stu-id="4f6d1-247">name</span></span> | <span data-ttu-id="4f6d1-248">Nom de l’activité</span><span class="sxs-lookup"><span data-stu-id="4f6d1-248">Name of the activity</span></span> |<span data-ttu-id="4f6d1-249">Oui</span><span class="sxs-lookup"><span data-stu-id="4f6d1-249">Yes</span></span> |
| <span data-ttu-id="4f6d1-250">Description</span><span class="sxs-lookup"><span data-stu-id="4f6d1-250">description</span></span> |<span data-ttu-id="4f6d1-251">Texte décrivant la raison motivant l’activité.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-251">Text describing what the activity is used for</span></span> |<span data-ttu-id="4f6d1-252">Non</span><span class="sxs-lookup"><span data-stu-id="4f6d1-252">No</span></span> |
| <span data-ttu-id="4f6d1-253">type</span><span class="sxs-lookup"><span data-stu-id="4f6d1-253">type</span></span> | <span data-ttu-id="4f6d1-254">Doit être défini sur **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="4f6d1-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="4f6d1-255">Oui</span><span class="sxs-lookup"><span data-stu-id="4f6d1-255">Yes</span></span> |
| <span data-ttu-id="4f6d1-256">inputs</span><span class="sxs-lookup"><span data-stu-id="4f6d1-256">inputs</span></span> | <span data-ttu-id="4f6d1-257">facultatif.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-257">Optional.</span></span> <span data-ttu-id="4f6d1-258">Si vous spécifiez un jeu de données d’entrée, il doit être disponible (à l’état Prêt) pour l’activité de procédure stockée à exécuter.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="4f6d1-259">Les jeux de données d’entrée ne peuvent pas être utilisés dans la procédure stockée en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-259">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="4f6d1-260">Cela sert uniquement à vérifier la dépendance avant de commencer l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-260">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="4f6d1-261">Non</span><span class="sxs-lookup"><span data-stu-id="4f6d1-261">No</span></span> |
| <span data-ttu-id="4f6d1-262">outputs</span><span class="sxs-lookup"><span data-stu-id="4f6d1-262">outputs</span></span> | <span data-ttu-id="4f6d1-263">Vous devez spécifier un jeu de données de sortie pour une activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="4f6d1-264">Le jeu de données de sortie spécifie la **planification** pour l’activité de procédure stockée (horaire, hebdomadaire, mensuelle, etc.).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-264">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="4f6d1-265">Le jeu de données de sortie doit utiliser un **service lié** qui fait référence à une base de données Azure SQL, à un Azure SQL Data Warehouse ou à une base de données SQL Server dans laquelle vous souhaitez que la procédure stockée soit exécutée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-265">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="4f6d1-266">Le jeu de données de sortie peut être un moyen de passer le résultat de la procédure stockée pour traitement ultérieur par une autre activité ([chaînage des activités](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)) dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-266">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="4f6d1-267">Toutefois, Data Factory n’écrit pas automatiquement la sortie d’une procédure stockée pour ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-267">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="4f6d1-268">C’est la procédure stockée qui écrit dans une table SQL vers laquelle le jeu de données de sortie pointe.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-268">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="4f6d1-269">Dans certains cas, le jeu de données de sortie peut être un **jeu de données factice**, qui est utilisé uniquement pour spécifier le calendrier d’exécution de l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-269">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="4f6d1-270">Oui</span><span class="sxs-lookup"><span data-stu-id="4f6d1-270">Yes</span></span> |
| <span data-ttu-id="4f6d1-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="4f6d1-271">storedProcedureName</span></span> |<span data-ttu-id="4f6d1-272">Spécifiez le nom de la procédure stockée dans la base de données Azure SQL Database, Azure SQL Data Warehouse ou SQL Server qui est représenté par le service lié utilisé par la table de sortie.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-272">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="4f6d1-273">Oui</span><span class="sxs-lookup"><span data-stu-id="4f6d1-273">Yes</span></span> |
| <span data-ttu-id="4f6d1-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="4f6d1-274">storedProcedureParameters</span></span> |<span data-ttu-id="4f6d1-275">Spécifiez les valeurs des paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="4f6d1-276">Si vous avez besoin de passer null pour un paramètre, utilisez la syntaxe : "param1": null (le tout en minuscules).</span><span class="sxs-lookup"><span data-stu-id="4f6d1-276">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="4f6d1-277">Consultez l’exemple suivant pour en savoir plus sur l’utilisation de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-277">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="4f6d1-278">Non</span><span class="sxs-lookup"><span data-stu-id="4f6d1-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="4f6d1-279">Transmission d’une valeur statique</span><span class="sxs-lookup"><span data-stu-id="4f6d1-279">Passing a static value</span></span>
<span data-ttu-id="4f6d1-280">À présent, ajoutons une autre colonne nommée « Scénario » dans la table contenant une valeur statique appelée « Exemple de document ».</span><span class="sxs-lookup"><span data-stu-id="4f6d1-280">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![Exemple de données 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="4f6d1-282">**Table :**</span><span class="sxs-lookup"><span data-stu-id="4f6d1-282">**Table:**</span></span>

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

<span data-ttu-id="4f6d1-283">**Procédure stockée**</span><span class="sxs-lookup"><span data-stu-id="4f6d1-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="4f6d1-284">Maintenant, transmettez le paramètre **Scénario** et la valeur de l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="4f6d1-284">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="4f6d1-285">La section **typeProperties** de l’exemple précédent ressemble à l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="4f6d1-285">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

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

<span data-ttu-id="4f6d1-286">**Jeu de données Data Factory :**</span><span class="sxs-lookup"><span data-stu-id="4f6d1-286">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="4f6d1-287">**Pipeline Data Factory**</span><span class="sxs-lookup"><span data-stu-id="4f6d1-287">**Data Factory pipeline**</span></span>

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