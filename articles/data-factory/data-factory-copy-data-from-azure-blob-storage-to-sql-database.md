---
title: "Copie de données à partir du Stockage Blob vers une base de données SQ - Azure | Microsoft Docs"
description: "Ce didacticiel vous montre comment utiliser l’activité de copie dans un pipeline Azure Data Factory pour copier des données depuis Blob Storage vers une base de données SQL Azure."
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
ms.openlocfilehash: 730140d15f4dec7ddc1280c2e4da1d247902fe4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="e40a9-104">Didacticiel : Copie de données de Stockage Blob vers SQL Database à l’aide de Data Factory</span><span class="sxs-lookup"><span data-stu-id="e40a9-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e40a9-105">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="e40a9-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="e40a9-106">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="e40a9-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="e40a9-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e40a9-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="e40a9-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e40a9-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="e40a9-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e40a9-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="e40a9-110">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e40a9-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="e40a9-111">API REST</span><span class="sxs-lookup"><span data-stu-id="e40a9-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="e40a9-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="e40a9-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="e40a9-113">Dans ce didacticiel, vous allez créer une fabrique de données avec un pipeline afin de copier des données entre Blob Storage et la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="e40a9-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="e40a9-114">L’activité de copie effectue le déplacement des données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e40a9-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="e40a9-115">Elle est mise en œuvre par un service disponible dans le monde entier, capable de copier des données entre différents magasins de données de façon sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="e40a9-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="e40a9-116">Pour plus d’informations sur l’activité de copie, consultez l’article [Activités de déplacement des données](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="e40a9-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="e40a9-117">Pour obtenir une présentation détaillée du service Data Factory, consultez l’article [Présentation d’Azure Data Factory](data-factory-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="e40a9-117">For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="e40a9-118">Configuration requise pour le didacticiel</span><span class="sxs-lookup"><span data-stu-id="e40a9-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="e40a9-119">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e40a9-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="e40a9-120">**Abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-120">**Azure subscription**.</span></span>  <span data-ttu-id="e40a9-121">Si vous n'êtes pas abonné, vous pouvez créer un compte d'essai gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="e40a9-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e40a9-122">Consultez l'article [Essai gratuit](http://azure.microsoft.com/pricing/free-trial/) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="e40a9-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="e40a9-123">**Compte Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-123">**Azure Storage Account**.</span></span> <span data-ttu-id="e40a9-124">Dans le cadre de ce didacticiel, le stockage d’objets blob est utilisé comme magasin de données **source** .</span><span class="sxs-lookup"><span data-stu-id="e40a9-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="e40a9-125">Si vous n’avez pas de compte de stockage Azure, consultez l’article [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) pour découvrir comment en créer un.</span><span class="sxs-lookup"><span data-stu-id="e40a9-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="e40a9-126">**Base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-126">**Azure SQL Database**.</span></span> <span data-ttu-id="e40a9-127">Vous allez utiliser une base de données SQL Azure comme magasin de données **cible** dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e40a9-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="e40a9-128">Si vous n'avez pas de base de données SQL Azure pouvant être utilisée pour le didacticiel, consultez [Comment créer et configurer une base de données SQL Azure](../sql-database/sql-database-get-started.md) pour en créer une.</span><span class="sxs-lookup"><span data-stu-id="e40a9-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="e40a9-129">**SQL Server 2012/2014 ou Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="e40a9-130">Vous allez utiliser SQL Server Management Studio ou Visual Studio pour créer un exemple de base de données et afficher les données de résultat dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="e40a9-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="e40a9-131">Récupération du nom de compte Blob Storage et de la clé d'accès</span><span class="sxs-lookup"><span data-stu-id="e40a9-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="e40a9-132">Pour réaliser ce didacticiel, vous avez besoin du nom et de la clé de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e40a9-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="e40a9-133">Notez le **nom** et la **clé** de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e40a9-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="e40a9-134">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e40a9-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e40a9-135">Cliquez sur **Plus de services** sur le menu de gauche, puis sélectionnez **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    ![Parcourir - Comptes de stockage](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="e40a9-137">Dans le panneau **Comptes de stockage**, sélectionnez le **compte de stockage Azure** que vous souhaitez utiliser dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e40a9-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="e40a9-138">Sélectionnez le lien **Clés d’accès** sous **PARAMÈTRES**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="e40a9-139">Cliquez sur le bouton **copier** (image) situé en regard de la zone de texte **Nom du compte de stockage** et enregistrez/collez-la quelque part (dans un fichier texte, par exemple).</span><span class="sxs-lookup"><span data-stu-id="e40a9-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="e40a9-140">Répétez l'étape précédente pour copier ou noter la **clé1**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![Clé d’accès de stockage](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="e40a9-142">Fermez tous les panneaux en cliquant sur **X**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="e40a9-143">Récupérer les noms de serveur SQL, de base de données et d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e40a9-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="e40a9-144">Pour réaliser ce didacticiel, vous avez besoin des noms du serveur SQL Azure, de la base de données et de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e40a9-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="e40a9-145">Notez les noms du **serveur**, de la **base de données** et de **l’utilisateur** pour votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e40a9-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="e40a9-146">Dans le **portail Azure**, cliquez sur **Plus de services** dans le volet gauche et sélectionnez **Bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="e40a9-147">Dans le panneau **Bases de données SQL**, sélectionnez la **base de données** que vous souhaitez utiliser dans le cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e40a9-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="e40a9-148">Notez le **nom de la base de données**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="e40a9-149">Dans le panneau **Base de données SQL**, cliquez sur la vignette **Propriétés** sous **PARAMÈTRES**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="e40a9-150">Notez les valeurs de **NOM DU SERVEUR** et de **CONNEXION D'ADMINISTRATEUR DU SERVEUR**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="e40a9-151">Fermez tous les panneaux en cliquant sur **X**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="e40a9-152">Autoriser les services Azure à accéder au serveur</span><span class="sxs-lookup"><span data-stu-id="e40a9-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="e40a9-153">Vérifiez que le paramètre **Autoriser l’accès aux services Azure** est **ACTIVÉ** pour votre serveur SQL Azure pour que le service Data Factory puisse accéder à votre serveur SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e40a9-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="e40a9-154">Pour vérifier et activer ce paramètre, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e40a9-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="e40a9-155">Cliquez sur le hub **Plus de services** situé à gauche, puis sur **Serveurs SQL**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="e40a9-156">Sélectionnez votre serveur, puis cliquez sur **Pare-feu** sous **PARAMÈTRES**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="e40a9-157">Dans le panneau **Paramètres de pare-feu**, cliquez sur **ACTIVER** pour **Autoriser l’accès aux services Azure**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="e40a9-158">Fermez tous les panneaux en cliquant sur **X**.</span><span class="sxs-lookup"><span data-stu-id="e40a9-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="e40a9-159">Préparer Blob Storage et la Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="e40a9-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="e40a9-160">À présent, préparez votre stockage d'objets blob Azure et votre base de données SQL Azure pour ce didacticiel, en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="e40a9-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="e40a9-161">Lancez le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="e40a9-161">Launch Notepad.</span></span> <span data-ttu-id="e40a9-162">Copiez le texte suivant puis enregistrez-le sous le nom **emp.txt** dans le dossier **C:\ADFGetStarted** sur votre disque dur.</span><span class="sxs-lookup"><span data-stu-id="e40a9-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="e40a9-163">Utilisez des outils tels que [l’Explorateur de stockage Azure](http://storageexplorer.com/) pour créer le conteneur **adftutorial** et télécharger le fichier **emp.txt** vers ce dernier.</span><span class="sxs-lookup"><span data-stu-id="e40a9-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Azure Storage Explorer.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="e40a9-166">Utilisez le script SQL suivant pour créer la table **emp** dans votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e40a9-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="e40a9-167">**Si vous avez installé SQL Server 2012/2014 sur votre ordinateur :** suivez les instructions de l’article [Gestion d’Azure SQL Database à l’aide de SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) pour vous connecter à votre serveur SQL Azure et exécuter le script SQL.</span><span class="sxs-lookup"><span data-stu-id="e40a9-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="e40a9-168">Cet article utilise le [portail Azure Classic](http://manage.windowsazure.com), et non le [nouveau portail Azure](https://portal.azure.com), pour configurer le pare-feu d’un serveur SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e40a9-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="e40a9-169">Si votre client n’est pas autorisé à accéder au serveur SQL Azure, vous devez configurer le pare-feu pour votre serveur SQL Azure afin d’autoriser l’accès à partir de votre ordinateur (adresse IP).</span><span class="sxs-lookup"><span data-stu-id="e40a9-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="e40a9-170">Consultez [cet article](../sql-database/sql-database-configure-firewall-settings.md) pour savoir comment configurer le pare-feu de votre serveur SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e40a9-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="e40a9-171">Créer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="e40a9-171">Create a data factory</span></span>
<span data-ttu-id="e40a9-172">Vous avez terminé les étapes préalables requises.</span><span class="sxs-lookup"><span data-stu-id="e40a9-172">You have completed the prerequisites.</span></span> <span data-ttu-id="e40a9-173">Créez une fabrique de données à l’aide de l’une des manières suivantes.</span><span class="sxs-lookup"><span data-stu-id="e40a9-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="e40a9-174">Cliquez sur l’une des options de la liste déroulante en haut ou sur les liens suivants pour suivre le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e40a9-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="e40a9-175">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="e40a9-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="e40a9-176">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e40a9-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="e40a9-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e40a9-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="e40a9-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e40a9-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="e40a9-179">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e40a9-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="e40a9-180">API REST</span><span class="sxs-lookup"><span data-stu-id="e40a9-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="e40a9-181">API .NET</span><span class="sxs-lookup"><span data-stu-id="e40a9-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="e40a9-182">Dans ce didacticiel, le pipeline de données copie les données d’un magasin de données source vers un magasin de données de destination.</span><span class="sxs-lookup"><span data-stu-id="e40a9-182">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="e40a9-183">Il ne transforme pas les données d’entrée pour produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="e40a9-183">It does not transform input data to produce output data.</span></span> <span data-ttu-id="e40a9-184">Pour un didacticiel sur la transformation des données à l’aide d’Azure Data Factory, voir [Didacticiel : Générer votre premier pipeline pour traiter les données à l’aide du cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="e40a9-184">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="e40a9-185">Vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité.</span><span class="sxs-lookup"><span data-stu-id="e40a9-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="e40a9-186">Pour des informations détaillées, consultez [Planification et exécution avec Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="e40a9-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
