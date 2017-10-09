---
title: "aaaCopy des données à partir du stockage d’objets Blob tooSQL de base de données - Azure | Documents Microsoft"
description: "Ce didacticiel vous montre comment toouse l’activité de copie dans une fabrique de données Azure pipeline toocopy des données à partir de la base de données tooSQL de stockage Blob."
keywords: "blob sql, blob storage, copie de données"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a><span data-ttu-id="2e529-104">Didacticiel : Copier des données à partir du stockage d’objets Blob tooSQL de base de données à l’aide de la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="2e529-104">Tutorial: Copy data from Blob Storage tooSQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e529-105">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="2e529-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="2e529-106">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="2e529-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="2e529-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="2e529-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="2e529-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e529-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="2e529-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e529-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="2e529-110">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e529-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="2e529-111">API REST</span><span class="sxs-lookup"><span data-stu-id="2e529-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="2e529-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="2e529-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="2e529-113">Dans ce didacticiel, vous créez une fabrique de données comportant des données à partir de la base de données tooSQL de stockage Blob toocopy pipeline.</span><span class="sxs-lookup"><span data-stu-id="2e529-113">In this tutorial, you create a data factory with a pipeline toocopy data from Blob storage tooSQL database.</span></span>

<span data-ttu-id="2e529-114">Activité de copie de Hello effectue le déplacement des données de hello dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2e529-114">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="2e529-115">Elle est mise en œuvre par un service disponible dans le monde entier, capable de copier des données entre différents magasins de données de façon sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="2e529-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="2e529-116">Consultez [les activités de déplacement des données](data-factory-data-movement-activities.md) article pour plus d’informations sur l’activité de copie de hello.</span><span class="sxs-lookup"><span data-stu-id="2e529-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="2e529-117">Pour obtenir une présentation détaillée de hello service Data Factory, consultez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="2e529-117">For a detailed overview of hello Data Factory service, see hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="2e529-118">Configuration requise pour le didacticiel de hello</span><span class="sxs-lookup"><span data-stu-id="2e529-118">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="2e529-119">Avant de commencer ce didacticiel, vous devez disposer de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="2e529-119">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="2e529-120">**Abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="2e529-120">**Azure subscription**.</span></span>  <span data-ttu-id="2e529-121">Si vous n'êtes pas abonné, vous pouvez créer un compte d'essai gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="2e529-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2e529-122">Consultez hello [version d’évaluation gratuite](http://azure.microsoft.com/pricing/free-trial/) article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="2e529-122">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="2e529-123">**Compte Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="2e529-123">**Azure Storage Account**.</span></span> <span data-ttu-id="2e529-124">Vous utilisez le stockage d’objets blob hello comme un **source** stocker des données dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2e529-124">You use hello blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="2e529-125">Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) toocreate suit un article.</span><span class="sxs-lookup"><span data-stu-id="2e529-125">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="2e529-126">**Base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="2e529-126">**Azure SQL Database**.</span></span> <span data-ttu-id="2e529-127">Vous allez utiliser une base de données SQL Azure comme magasin de données **cible** dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2e529-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="2e529-128">Si vous n’avez pas une base de données SQL Azure que vous pouvez utiliser dans le didacticiel hello, voir [comment toocreate et configurer une base de données SQL Azure](../sql-database/sql-database-get-started.md) toocreate une.</span><span class="sxs-lookup"><span data-stu-id="2e529-128">If you don't have an Azure SQL database that you can use in hello tutorial, See [How toocreate and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate one.</span></span>
* <span data-ttu-id="2e529-129">**SQL Server 2012/2014 ou Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="2e529-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="2e529-130">Vous utilisez SQL Server Management Studio ou Visual Studio toocreate une base de données exemple et les données de résultat de salutation tooview dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="2e529-130">You use SQL Server Management Studio or Visual Studio toocreate a sample database and tooview hello result data in hello database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="2e529-131">Récupération du nom de compte Blob Storage et de la clé d'accès</span><span class="sxs-lookup"><span data-stu-id="2e529-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="2e529-132">Vous devez compte hello clé et le nom de votre stockage Azure compte toodo ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2e529-132">You need hello account name and account key of your Azure storage account toodo this tutorial.</span></span> <span data-ttu-id="2e529-133">Notez le **nom** et la **clé** de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2e529-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="2e529-134">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2e529-134">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2e529-135">Cliquez sur **davantage de services** sur hello gauche menu et sélectionnez **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="2e529-135">Click **More services** on hello left menu and select **Storage Accounts**.</span></span>

    ![Parcourir - Comptes de stockage](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="2e529-137">Bonjour **comptes de stockage** panneau, sélectionnez hello **compte de stockage Azure** que vous souhaitez toouse dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2e529-137">In hello **Storage Accounts** blade, select hello **Azure storage account** that you want toouse in this tutorial.</span></span>
4. <span data-ttu-id="2e529-138">Sélectionnez le lien **Clés d’accès** sous **PARAMÈTRES**.</span><span class="sxs-lookup"><span data-stu-id="2e529-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="2e529-139">Cliquez sur **copie** (image) bouton ensuite trop**nom de compte de stockage** texte zone et d’enregistrer/coller il quelque part (par exemple : dans un fichier texte).</span><span class="sxs-lookup"><span data-stu-id="2e529-139">Click **copy** (image) button next too**Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="2e529-140">Répétez hello précédente étape toocopy ou notez hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="2e529-140">Repeat hello previous step toocopy or note down hello **key1**.</span></span>

    ![Clé d’accès de stockage](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="2e529-142">Fermer tous les panneaux de hello en cliquant sur **X**.</span><span class="sxs-lookup"><span data-stu-id="2e529-142">Close all hello blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="2e529-143">Récupérer les noms de serveur SQL, de base de données et d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2e529-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="2e529-144">Vous devez les noms hello du serveur SQL Azure, de base de données et de toodo de l’utilisateur de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2e529-144">You need hello names of Azure SQL server, database, and user toodo this tutorial.</span></span> <span data-ttu-id="2e529-145">Notez les noms du **serveur**, de la **base de données** et de **l’utilisateur** pour votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2e529-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="2e529-146">Bonjour **portail Azure**, cliquez sur **davantage de services** sur hello gauche et sélectionnez **bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="2e529-146">In hello **Azure portal**, click **More services** on hello left and select **SQL databases**.</span></span>
2. <span data-ttu-id="2e529-147">Bonjour **Panneau de bases de données SQL**, sélectionnez hello **base de données** que vous souhaitez toouse dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2e529-147">In hello **SQL databases blade**, select hello **database** that you want toouse in this tutorial.</span></span> <span data-ttu-id="2e529-148">Notez les hello **nom de la base de données**.</span><span class="sxs-lookup"><span data-stu-id="2e529-148">Note down hello **database name**.</span></span>  
3. <span data-ttu-id="2e529-149">Bonjour **base de données SQL** panneau, cliquez sur **propriétés** sous **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2e529-149">In hello **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="2e529-150">Notez les valeurs hello pour **nom du serveur** et **ouverture de session de serveur ADMIN**.</span><span class="sxs-lookup"><span data-stu-id="2e529-150">Note down hello values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="2e529-151">Fermer tous les panneaux de hello en cliquant sur **X**.</span><span class="sxs-lookup"><span data-stu-id="2e529-151">Close all hello blades by clicking **X**.</span></span>

## <a name="allow-azure-services-tooaccess-sql-server"></a><span data-ttu-id="2e529-152">Autoriser les services Azure tooaccess SQL server</span><span class="sxs-lookup"><span data-stu-id="2e529-152">Allow Azure services tooaccess SQL server</span></span>
<span data-ttu-id="2e529-153">Vérifiez que **autoriser l’accès des services de tooAzure** paramètre désactivé **ON** pour votre serveur SQL Azure pour que ce service Data Factory hello peut accéder à votre serveur SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2e529-153">Ensure that **Allow access tooAzure services** setting turned **ON** for your Azure SQL server so that hello Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="2e529-154">tooverify et activer ce paramètre, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2e529-154">tooverify and turn on this setting, do hello following steps:</span></span>

1. <span data-ttu-id="2e529-155">Cliquez sur **davantage de services** hub dans hello gauche, cliquez sur **serveurs SQL**.</span><span class="sxs-lookup"><span data-stu-id="2e529-155">Click **More services** hub on hello left and click **SQL servers**.</span></span>
2. <span data-ttu-id="2e529-156">Sélectionnez votre serveur, puis cliquez sur **Pare-feu** sous **PARAMÈTRES**.</span><span class="sxs-lookup"><span data-stu-id="2e529-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="2e529-157">Bonjour **des paramètres de pare-feu** panneau, cliquez sur **ON** pour **autoriser l’accès des services de tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="2e529-157">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
4. <span data-ttu-id="2e529-158">Fermer tous les panneaux de hello en cliquant sur **X**.</span><span class="sxs-lookup"><span data-stu-id="2e529-158">Close all hello blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="2e529-159">Préparer Blob Storage et la Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2e529-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="2e529-160">À présent, préparer votre stockage d’objets blob Azure et de la base de données SQL Azure hello en effectuant hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2e529-160">Now, prepare your Azure blob storage and Azure SQL database for hello tutorial by performing hello following steps:</span></span>  

1. <span data-ttu-id="2e529-161">Lancez le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="2e529-161">Launch Notepad.</span></span> <span data-ttu-id="2e529-162">Copier hello après le texte et l’enregistrer en tant que **emp.txt** trop**C:\ADFGetStarted** dossier sur votre disque dur.</span><span class="sxs-lookup"><span data-stu-id="2e529-162">Copy hello following text and save it as **emp.txt** too**C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="2e529-163">Utiliser des outils tels que [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** hello conteneur et tooupload **emp.txt** conteneur toohello de fichier.</span><span class="sxs-lookup"><span data-stu-id="2e529-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** container and tooupload hello **emp.txt** file toohello container.</span></span>

    ![Azure Storage Explorer.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="2e529-166">Hello utilisation suivant hello SQL script toocreate **emp** table dans votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2e529-166">Use hello following SQL script toocreate hello **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="2e529-167">**Si vous disposez de SQL Server 2012/2014 installé sur votre ordinateur :** suivez les instructions à partir de [la gestion de Azure SQL Database à l’aide de SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server et exécutez hello SQL script.</span><span class="sxs-lookup"><span data-stu-id="2e529-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server and run hello SQL script.</span></span> <span data-ttu-id="2e529-168">Cet article utilise hello [portail Azure classic](http://manage.windowsazure.com), pas hello [nouveau portail Azure](https://portal.azure.com), pare-feu tooconfigure pour un serveur SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2e529-168">This article uses hello [classic Azure portal](http://manage.windowsazure.com), not hello [new Azure portal](https://portal.azure.com), tooconfigure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="2e529-169">Si votre client n’est pas autorisé serveur SQL Azure de hello tooaccess, vous devez tooconfigure pare-feu pour votre accès tooallow du serveur SQL Azure à partir de votre ordinateur (adresse IP).</span><span class="sxs-lookup"><span data-stu-id="2e529-169">If your client is not allowed tooaccess hello Azure SQL server, you need tooconfigure firewall for your Azure SQL server tooallow access from your machine (IP Address).</span></span> <span data-ttu-id="2e529-170">Consultez [cet article](../sql-database/sql-database-configure-firewall-settings.md) pour le pare-feu étapes tooconfigure hello pour votre serveur SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2e529-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps tooconfigure hello firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="2e529-171">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="2e529-171">Create a data factory</span></span>
<span data-ttu-id="2e529-172">Vous avez terminé la configuration requise de hello.</span><span class="sxs-lookup"><span data-stu-id="2e529-172">You have completed hello prerequisites.</span></span> <span data-ttu-id="2e529-173">Vous pouvez créer une fabrique de données à l’aide de hello suivant façons.</span><span class="sxs-lookup"><span data-stu-id="2e529-173">You can create a data factory using one of hello following ways.</span></span> <span data-ttu-id="2e529-174">Cliquez sur une des options de hello dans la liste déroulante de hello au haut de hello ou hello suivant liens tooperform hello didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2e529-174">Click one of hello options in hello drop-down list at hello top or hello following links tooperform hello tutorial.</span></span>     

* [<span data-ttu-id="2e529-175">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="2e529-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="2e529-176">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="2e529-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="2e529-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e529-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="2e529-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e529-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="2e529-179">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e529-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="2e529-180">API REST</span><span class="sxs-lookup"><span data-stu-id="2e529-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="2e529-181">API .NET</span><span class="sxs-lookup"><span data-stu-id="2e529-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="2e529-182">le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa.</span><span class="sxs-lookup"><span data-stu-id="2e529-182">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="2e529-183">Il ne transforme pas les données de sortie de données d’entrée tooproduce.</span><span class="sxs-lookup"><span data-stu-id="2e529-183">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="2e529-184">Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer vos premières données tootransform de pipeline à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="2e529-184">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="2e529-185">Vous pouvez chaîner les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="2e529-185">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="2e529-186">Pour plus d’informations, voir [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="2e529-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
