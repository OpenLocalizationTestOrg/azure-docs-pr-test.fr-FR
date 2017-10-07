---
title: "données aaaLoad dans Azure SQL Data Warehouse – Data Factory | Documents Microsoft"
description: "Ce didacticiel charge les données dans Azure SQL Data Warehouse à l’aide d’Azure Data Factory et utilise une base de données SQL Server en tant que source de données hello."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="afd80-103">Chargement de données dans SQL Data Warehouse avec Data Factory</span><span class="sxs-lookup"><span data-stu-id="afd80-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="afd80-104">Vous pouvez utiliser les données de tooload d’Azure Data Factory dans Azure SQL Data Warehouse de n’importe quelle hello [prise en charge des magasins de données source](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="afd80-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="afd80-105">Par exemple, vous pouvez charger des données dans un entrepôt de données SQL à partir d’une base de données SQL Azure ou d’une base de données Oracle à l’aide de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="afd80-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="afd80-106">Didacticiel dans cet article vous montre comment les données tooload à partir d’un ordinateur local SQL Server de base de données dans un entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="afd80-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="afd80-107">**Durée estimée**: ce didacticiel prend environ 10 à 15 minutes toocomplete une fois que les conditions préalables de hello sont remplies.</span><span class="sxs-lookup"><span data-stu-id="afd80-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afd80-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="afd80-108">Prerequisites</span></span>

- <span data-ttu-id="afd80-109">Vous avez besoin une **base de données SQL Server** avec les tables qui contiennent des données hello toobe copiée toohello entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="afd80-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="afd80-110">Vous avez besoin d’un **SQL Data Warehouse** en ligne.</span><span class="sxs-lookup"><span data-stu-id="afd80-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="afd80-111">Si vous n’avez pas déjà d’un entrepôt de données, découvrez comment trop[créer un entrepôt de données SQL Azure](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="afd80-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="afd80-112">Vous avez besoin d’un **compte de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="afd80-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="afd80-113">Si vous n’avez pas déjà un compte de stockage, découvrez comment trop[créer un compte de stockage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="afd80-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="afd80-114">Pour de meilleures performances, recherchez le compte de stockage hello et hello l’entrepôt de données Bonjour même région Azure.</span><span class="sxs-lookup"><span data-stu-id="afd80-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="afd80-115">Configurer une fabrique de données</span><span class="sxs-lookup"><span data-stu-id="afd80-115">Configure a data factory</span></span>
1. <span data-ttu-id="afd80-116">Connectez-vous à toohello [portail Azure][].</span><span class="sxs-lookup"><span data-stu-id="afd80-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="afd80-117">Recherchez votre entrepôt de données et cliquez sur tooopen il.</span><span class="sxs-lookup"><span data-stu-id="afd80-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="afd80-118">Dans le panneau principal de hello, cliquez sur **charger des données** > **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="afd80-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Lancer l’Assistant Charger des données](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="afd80-120">Si vous n’avez pas une fabrique de données dans votre abonnement Azure, vous voyez un **nouvelle fabrique de données** boîte de dialogue dans un onglet distinct du navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="afd80-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="afd80-121">Hello, renseignez les informations demandées, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="afd80-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="afd80-122">Après la création de la fabrique de données hello, hello **nouvelle fabrique de données** boîte de dialogue se ferme et vous voyez hello **sélectionnez Data Factory** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="afd80-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="afd80-123">Si vous avez une ou plusieurs fabriques de données déjà dans hello abonnement Azure, vous voyez hello **sélectionnez Data Factory** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="afd80-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="afd80-124">Dans cette boîte de dialogue, vous pouvez sélectionner une fabrique de données existante ou cliquez sur **créer une nouvelle fabrique de données** toocreate un nouveau.</span><span class="sxs-lookup"><span data-stu-id="afd80-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![Configurer une fabrique de données](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="afd80-126">Bonjour **sélectionnez Data Factory** boîte de dialogue, hello **charger des données** option est sélectionnée par défaut.</span><span class="sxs-lookup"><span data-stu-id="afd80-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="afd80-127">Cliquez sur **suivant** toostart création d’une tâche de chargement de données.</span><span class="sxs-lookup"><span data-stu-id="afd80-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="afd80-128">Configurer les propriétés de fabrique de données hello</span><span class="sxs-lookup"><span data-stu-id="afd80-128">Configure hello data factory properties</span></span>
<span data-ttu-id="afd80-129">Maintenant que vous avez créé une fabrique de données, étape suivante de hello donnée tooconfigure hello du chargement de planification.</span><span class="sxs-lookup"><span data-stu-id="afd80-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="afd80-130">Pour le **nom de la tâche**, entrez **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="afd80-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="afd80-131">Utiliser la valeur par défaut hello **exécuter qu’une seule fois maintenant** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="afd80-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![Configurer la planification](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="afd80-133">Configurer le magasin de données source hello et la passerelle</span><span class="sxs-lookup"><span data-stu-id="afd80-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="afd80-134">Vous indiquez maintenant Data Factory hello local SQL Server de base de données à partir de laquelle vous souhaitez que les données de tooload.</span><span class="sxs-lookup"><span data-stu-id="afd80-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="afd80-135">Choisissez **SQL Server** de source de données pris en charge de hello stocker le catalogue, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="afd80-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![Choisir la source du serveur SQL](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="afd80-137">A **base de données SQL Server de spécifier hello locale** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="afd80-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="afd80-138">Hello tout d’abord **nom de la connexion** champ est automatiquement renseigné.</span><span class="sxs-lookup"><span data-stu-id="afd80-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="afd80-139">deuxième champ de Hello demande nom hello Hello **passerelle**.</span><span class="sxs-lookup"><span data-stu-id="afd80-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="afd80-140">Si vous utilisez une fabrique de données existant qui possède déjà une passerelle, vous pouvez réutiliser la passerelle de hello en le sélectionnant dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="afd80-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="afd80-141">Cliquez sur hello **créer une passerelle** lien toocreate une passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="afd80-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="afd80-142">Si le magasin de données de source de hello est local ou dans une machine virtuelle Azure IaaS, une passerelle de gestion des données est requise.</span><span class="sxs-lookup"><span data-stu-id="afd80-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="afd80-143">Une passerelle a une relation 1-1 avec une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="afd80-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="afd80-144">Elle ne peut pas être utilisée à partir de la fabrique de données dans un autre, mais il peut être utilisé par plusieurs données chargement des tâches avec Bonjour même fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="afd80-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="afd80-145">Une passerelle peut être banques de données toomultiple tooconnect utilisé lors de l’exécution des tâches de chargement des données.</span><span class="sxs-lookup"><span data-stu-id="afd80-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="afd80-146">Pour plus d’informations sur la passerelle de hello, consultez [passerelle de gestion des données](../data-factory/data-factory-data-management-gateway.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="afd80-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="afd80-147">Une boîte de dialogue **Créer une passerelle** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="afd80-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="afd80-148">Dans le champ Nom, entrez **GatewayForDWLoading**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="afd80-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="afd80-149">Une boîte de dialogue **Configurer la passerelle** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="afd80-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="afd80-150">Cliquez sur **lancer le programme d’installation express sur cet ordinateur** tooautomatically télécharger, installer et inscrire la passerelle de gestion des données sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="afd80-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="afd80-151">progression de Hello est indiquée dans une fenêtre indépendante.</span><span class="sxs-lookup"><span data-stu-id="afd80-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="afd80-152">Si la machine de hello ne peut pas connecter le magasin de données toohello, vous pouvez manuellement [télécharger et installer la passerelle de hello](https://www.microsoft.com/download/details.aspx?id=39717) sur un ordinateur qui peut se connecter à des données de toohello stocker et ensuite utiliser tooregister de clé hello.</span><span class="sxs-lookup"><span data-stu-id="afd80-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="afd80-153">le programme d’installation express de Hello fonctionne en mode natif avec Microsoft Edge et Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="afd80-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="afd80-154">Si vous utilisez Google Chrome, d’abord installer extension de ClickOnce hello web Store de Chrome.</span><span class="sxs-lookup"><span data-stu-id="afd80-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![Lancer le programme d’installation express](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="afd80-156">Attendez que hello passerelle le programme d’installation toocomplete.</span><span class="sxs-lookup"><span data-stu-id="afd80-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="afd80-157">Une fois que la passerelle de hello est enregistré correctement et est en ligne, fermeture de fenêtre contextuelle hello et passerelle hello s’affiche dans le champ de la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="afd80-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="afd80-158">Puis rest de hello, renseignez les champs obligatoires comme suit, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="afd80-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="afd80-159">**Nom du serveur**: nom de hello local SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afd80-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="afd80-160">**Nom de la base de données** : base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afd80-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="afd80-161">**Chiffrement des informations d’identification**: utiliser par défaut de hello « par le navigateur web ».</span><span class="sxs-lookup"><span data-stu-id="afd80-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="afd80-162">**Type d’authentification**: choisissez de type hello d’authentification que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="afd80-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="afd80-163">**Nom d’utilisateur** et **mot de passe**: entrez le nom d’utilisateur hello et le mot de passe pour un utilisateur qui a des données d’autorisation toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="afd80-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![Lancer le programme d’installation express](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="afd80-165">étape suivante de Hello est toochoose les tables de hello depuis lequel les données hello toocopy.</span><span class="sxs-lookup"><span data-stu-id="afd80-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="afd80-166">Vous pouvez filtrer les tables hello à l’aide de mots clés.</span><span class="sxs-lookup"><span data-stu-id="afd80-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="afd80-167">Et vous pouvez afficher un aperçu de schéma de données et la table hello dans le panneau inférieur hello.</span><span class="sxs-lookup"><span data-stu-id="afd80-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="afd80-168">Une fois la sélection terminée, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="afd80-168">After you finish your selection, click **Next**.</span></span>

    ![Sélectionner des tables](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="afd80-170">Configurer la destination hello, votre entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="afd80-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="afd80-171">Maintenant, vous indiquez Data Factory les informations de destination hello.</span><span class="sxs-lookup"><span data-stu-id="afd80-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="afd80-172">Vos informations de connexion SQL Data Warehouse sont renseignées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="afd80-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="afd80-173">Entrez un mot de passe hello hello nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afd80-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="afd80-174">, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="afd80-174">and click **Next**.</span></span>

    ![Configurer la destination](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="afd80-176">Un mappage de table intelligent s’affiche qui mappe les tables sources toodestination basées sur des noms de table.</span><span class="sxs-lookup"><span data-stu-id="afd80-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="afd80-177">Si la table de hello n’existe pas dans la destination de hello, par défaut ADF créera un par hello même nom (cela s’applique tooSQL serveur ou base de données SQL Azure en tant que source).</span><span class="sxs-lookup"><span data-stu-id="afd80-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="afd80-178">Vous pouvez également choisir la table de toomap tooan existante.</span><span class="sxs-lookup"><span data-stu-id="afd80-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="afd80-179">Vérifiez, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="afd80-179">Review and click **Next**.</span></span>

    ![Mapper les tables](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="afd80-181">Passez en revue le mappage de schéma hello et recherchez les messages d’erreur ou avertissement.</span><span class="sxs-lookup"><span data-stu-id="afd80-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="afd80-182">Le mappage intelligent repose sur le nom de colonne.</span><span class="sxs-lookup"><span data-stu-id="afd80-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="afd80-183">S’il existe une conversion de type de données non pris en charge entre les colonnes source et de destination hello, vous consultez un message d’erreur en même temps que la table correspondante de hello.</span><span class="sxs-lookup"><span data-stu-id="afd80-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="afd80-184">Si vous choisissez automatique de Data Factory toolet créer des tables de hello, conversion de type de données peut se produire si nécessaire l’incompatibilité de hello toofix entre des magasins de source et de destination.</span><span class="sxs-lookup"><span data-stu-id="afd80-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![Mapper le schéma](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="afd80-186">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="afd80-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="afd80-187">Configurer les paramètres de performances hello</span><span class="sxs-lookup"><span data-stu-id="afd80-187">Configure hello performance settings</span></span>
<span data-ttu-id="afd80-188">Dans les configurations de performances hello, vous configurez un compte de stockage Azure utilisé pour le transit des données de hello avant de charger dans l’entrepôt de données SQL à l’aide d’énumérer efficacement [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="afd80-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="afd80-189">Une fois hello copie terminée, les données intermédiaires dans le stockage de salutation seront nettoyées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="afd80-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="afd80-190">Sélectionnez un compte de stockage Azure existant, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="afd80-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Configurer le blob intermédiaire](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="afd80-192">Passez en revue les informations de résumé et de déploiement du pipeline de hello</span><span class="sxs-lookup"><span data-stu-id="afd80-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="afd80-193">Passez en revue la configuration de hello et cliquez sur **Terminer** pipeline de bouton toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="afd80-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![Déployer la fabrique de données](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="afd80-195">Surveiller la progression du chargement des données</span><span class="sxs-lookup"><span data-stu-id="afd80-195">Monitor data loading progress</span></span>

<span data-ttu-id="afd80-196">Vous pouvez voir la progression du déploiement hello et résultats Bonjour **déploiement** page.</span><span class="sxs-lookup"><span data-stu-id="afd80-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="afd80-197">Une fois le déploiement de hello est terminé, cliquez sur lien hello indiquant **cliquez ici pipeline de copie toomonitor** données toomonitor progression du chargement.</span><span class="sxs-lookup"><span data-stu-id="afd80-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![Surveillance d’un pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="afd80-199">Hello nouvellement créé **DWLoadData-fromSQLServer** pipeline de chargement de données est automatiquement sélectionné à partir de hello gauche **l’Explorateur de ressources**.</span><span class="sxs-lookup"><span data-stu-id="afd80-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![Afficher le pipeline](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="afd80-201">Cliquez sur dans le pipeline hello au milieu de hello hello toosee de panneau état détaillé de chaque table qui mappe tooan activité.</span><span class="sxs-lookup"><span data-stu-id="afd80-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![Afficher l’activité de la table](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="afd80-203">Plus cliquez dans une activité et vous voyez le chargement des détails dans le volet droit de hello, y compris la taille des données, les lignes, débit, etc. les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="afd80-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![Afficher les informations relatives à l’activité des tables](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="afd80-205">Cliquez sur cette analyse vue ultérieur, accédez tooyour SQL Data Warehouse, de toolaunch **charger des données > Azure Data Factory**, sélectionnez votre fabrique et choisissez **surveiller existant du chargement des tâches**.</span><span class="sxs-lookup"><span data-stu-id="afd80-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afd80-206">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="afd80-206">Next steps</span></span>

<span data-ttu-id="afd80-207">reportez-vous à votre tooSQL de base de données Data Warehouse, toomigrate [présentation de la Migration](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="afd80-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="afd80-208">toolearn en savoir plus sur Azure Data Factory et de ses fonctionnalités de déplacement des données, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="afd80-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="afd80-209">Introduction tooAzure Data Factory</span><span class="sxs-lookup"><span data-stu-id="afd80-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="afd80-210">Déplacer des données à l’aide de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="afd80-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="afd80-211">Déplacer les données tooand à partir de l’entrepôt de données SQL Azure à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="afd80-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="afd80-212">tooexplore vos données dans l’entrepôt de données SQL, consultez hello suivants articles :</span><span class="sxs-lookup"><span data-stu-id="afd80-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="afd80-213">Se connecter tooSQL Data Warehouse avec Visual Studio et SSDT</span><span class="sxs-lookup"><span data-stu-id="afd80-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="afd80-214">[Données visuelles avec Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="afd80-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[portail Azure]: https://portal.azure.com
