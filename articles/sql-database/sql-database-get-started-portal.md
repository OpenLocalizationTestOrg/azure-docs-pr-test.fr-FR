---
title: "Portail Azure : Créer une base de données SQL | Microsoft Docs"
description: "Découvrez comment créer un serveur logique SQL Database, une règle de pare-feu au niveau du serveur et des bases de données dans le Portail Azure. Vous apprendrez également à interroger une base de données SQL Azure à l’aide du portail Azure."
keywords: "didacticiel sur la base de données sql, créer une base de données sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: a863cf3ad08040906850f64db6505f30bcfa72eb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-sql-database-in-the-azure-portal"></a><span data-ttu-id="fcc42-105">Création d’une base de données SQL Azure à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="fcc42-105">Create an Azure SQL database in the Azure portal</span></span>

<span data-ttu-id="fcc42-106">Ce didacticiel de démarrage rapide vous guide dans la procédure de création d’une base de données SQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-106">This quick start tutorial walks through how to create a SQL database in Azure.</span></span> <span data-ttu-id="fcc42-107">Azure SQL Database est une offre de type « base de données en tant que service » qui vous permet d’exécuter et de mettre à l’échelle des bases de données SQL Server hautement disponibles dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="fcc42-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you to run and scale highly available SQL Server databases in the cloud.</span></span> <span data-ttu-id="fcc42-108">Ce guide de démarrage rapide vous indique comment commencer par créer une base de données SQL à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-108">This quick start shows you how to get started by creating a SQL database using the Azure portal.</span></span>

<span data-ttu-id="fcc42-109">Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="fcc42-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="fcc42-110">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-110">Log in to the Azure portal</span></span>

<span data-ttu-id="fcc42-111">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fcc42-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="fcc42-112">Créer une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="fcc42-112">Create a SQL database</span></span>

<span data-ttu-id="fcc42-113">Une base de données SQL Azure est créée avec un ensemble défini de [ressources de calcul et de stockage](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="fcc42-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="fcc42-114">La base de données est créée dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) et dans un [serveur logique Azure SQL Database](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="fcc42-114">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="fcc42-115">Suivez ces étapes pour créer une base de données SQL contenant les exemples de données Adventure Works LT.</span><span class="sxs-lookup"><span data-stu-id="fcc42-115">Follow these steps to create a SQL database containing the Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="fcc42-116">Cliquez sur le bouton **Nouveau** dans le coin supérieur gauche du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-116">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="fcc42-117">Sélectionnez **Bases de données** dans la page **Nouveau**, puis **Base de données SQL** dans la page **Bases de données**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-117">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span>

   ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="fcc42-119">Remplissez le formulaire de base de données SQL avec les informations suivantes, comme indiqué dans l’illustration précédente :</span><span class="sxs-lookup"><span data-stu-id="fcc42-119">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="fcc42-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="fcc42-120">Setting</span></span>       | <span data-ttu-id="fcc42-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="fcc42-121">Suggested value</span></span> | <span data-ttu-id="fcc42-122">Description</span><span class="sxs-lookup"><span data-stu-id="fcc42-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="fcc42-123">**Nom de la base de données**</span><span class="sxs-lookup"><span data-stu-id="fcc42-123">**Database name**</span></span> | <span data-ttu-id="fcc42-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="fcc42-124">mySampleDatabase</span></span> | <span data-ttu-id="fcc42-125">Pour les noms de base de données valides, consultez [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données).</span><span class="sxs-lookup"><span data-stu-id="fcc42-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="fcc42-126">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="fcc42-126">**Subscription**</span></span> | <span data-ttu-id="fcc42-127">Votre abonnement</span><span class="sxs-lookup"><span data-stu-id="fcc42-127">Your subscription</span></span>  | <span data-ttu-id="fcc42-128">Pour plus d’informations sur vos abonnements, consultez [Abonnements](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="fcc42-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="fcc42-129">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="fcc42-129">**Resource group**</span></span>  | <span data-ttu-id="fcc42-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fcc42-130">myResourceGroup</span></span> | <span data-ttu-id="fcc42-131">Pour les noms de groupe de ressources valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom).</span><span class="sxs-lookup"><span data-stu-id="fcc42-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="fcc42-132">**Source**</span><span class="sxs-lookup"><span data-stu-id="fcc42-132">**Source source**</span></span> | <span data-ttu-id="fcc42-133">Exemple (AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="fcc42-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="fcc42-134">Charge le schéma et les données AdventureWorksLT schéma dans votre nouvelle base de données</span><span class="sxs-lookup"><span data-stu-id="fcc42-134">Loads the AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="fcc42-135">Vous devez sélectionner l’exemple de base de données sur ce formulaire, car il est utilisé dans le reste de ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="fcc42-135">You must select the sample database on this form because it is used in the remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="fcc42-136">Sous **Serveur**, cliquez sur **Configurer les paramètres requis** et remplissez le formulaire de serveur SQL (serveur logique) avec les informations suivantes, comme indiqué dans l’illustration précédente :</span><span class="sxs-lookup"><span data-stu-id="fcc42-136">Under **Server**, click **Configure required settings** and fill out the SQL server (logical server) form with the following information, as shown on the following image:</span></span>   

   | <span data-ttu-id="fcc42-137">Paramètre</span><span class="sxs-lookup"><span data-stu-id="fcc42-137">Setting</span></span>       | <span data-ttu-id="fcc42-138">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="fcc42-138">Suggested value</span></span> | <span data-ttu-id="fcc42-139">Description</span><span class="sxs-lookup"><span data-stu-id="fcc42-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="fcc42-140">**Nom du serveur**</span><span class="sxs-lookup"><span data-stu-id="fcc42-140">**Server name**</span></span> | <span data-ttu-id="fcc42-141">Nom globalement unique</span><span class="sxs-lookup"><span data-stu-id="fcc42-141">Any globally unique name</span></span> | <span data-ttu-id="fcc42-142">Pour les noms de serveur valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom).</span><span class="sxs-lookup"><span data-stu-id="fcc42-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="fcc42-143">**Connexion d’administrateur du serveur**</span><span class="sxs-lookup"><span data-stu-id="fcc42-143">**Server admin login**</span></span> | <span data-ttu-id="fcc42-144">Nom valide</span><span class="sxs-lookup"><span data-stu-id="fcc42-144">Any valid name</span></span> | <span data-ttu-id="fcc42-145">Pour les noms de connexion valides, consultez [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données).</span><span class="sxs-lookup"><span data-stu-id="fcc42-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="fcc42-146">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="fcc42-146">**Password**</span></span> | <span data-ttu-id="fcc42-147">Mot de passe valide</span><span class="sxs-lookup"><span data-stu-id="fcc42-147">Any valid password</span></span> | <span data-ttu-id="fcc42-148">Votre mot de passe doit comporter au moins 8 caractères et contenir des caractères appartenant à trois des catégories suivantes : caractères en majuscules, caractères en minuscules, chiffres et caractères non alphanumériques.</span><span class="sxs-lookup"><span data-stu-id="fcc42-148">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="fcc42-149">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="fcc42-149">**Subscription**</span></span> | <span data-ttu-id="fcc42-150">Votre abonnement</span><span class="sxs-lookup"><span data-stu-id="fcc42-150">Your subscription</span></span> | <span data-ttu-id="fcc42-151">Pour plus d’informations sur vos abonnements, consultez [Abonnements](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="fcc42-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="fcc42-152">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="fcc42-152">**Resource group**</span></span> | <span data-ttu-id="fcc42-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fcc42-153">myResourceGroup</span></span> | <span data-ttu-id="fcc42-154">Pour les noms de groupe de ressources valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom).</span><span class="sxs-lookup"><span data-stu-id="fcc42-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="fcc42-155">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="fcc42-155">**Location**</span></span> | <span data-ttu-id="fcc42-156">Emplacement valide</span><span class="sxs-lookup"><span data-stu-id="fcc42-156">Any valid location</span></span> | <span data-ttu-id="fcc42-157">Pour plus d’informations sur les régions, consultez [Régions Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="fcc42-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="fcc42-158">La connexion d’administrateur serveur et le mot de passe que vous spécifiez ici seront requis plus loin dans ce guide de démarrage rapide pour la connexion au serveur et à ses bases de données.</span><span class="sxs-lookup"><span data-stu-id="fcc42-158">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="fcc42-159">Retenez ou enregistrez ces informations pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-159">Remember or record this information for later use.</span></span> 
   >  

   ![create database-server](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="fcc42-161">Une fois le formulaire rempli, cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-161">When you have completed the form, click **Select**.</span></span>

6. <span data-ttu-id="fcc42-162">Cliquez sur **Niveau tarifaire** pour spécifier le niveau de service et le niveau de performances pour votre nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="fcc42-162">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="fcc42-163">Utilisez le curseur pour sélectionner **20 DTU** et **250** Go de stockage.</span><span class="sxs-lookup"><span data-stu-id="fcc42-163">Use the slider to select **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="fcc42-164">Pour plus d’informations sur les DTU, consultez la page [Qu’est-ce qu’un DTU ?](sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="fcc42-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![create database-s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="fcc42-166">Après avoir sélectionné le nombre de DTU, cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-166">After selected the amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="fcc42-167">Maintenant que vous avez rempli le formulaire SQL Database, cliquez sur **Créer** pour approvisionner la base de données.</span><span class="sxs-lookup"><span data-stu-id="fcc42-167">Now that you have completed the SQL Database form, click **Create** to provision the database.</span></span> <span data-ttu-id="fcc42-168">L’approvisionnement prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="fcc42-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="fcc42-169">Dans la barre d’outils, cliquez sur **Notifications** pour surveiller le processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="fcc42-169">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

   ![notification](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="fcc42-171">créer une règle de pare-feu au niveau du serveur ;</span><span class="sxs-lookup"><span data-stu-id="fcc42-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="fcc42-172">Le service SQL Database crée un pare-feu au niveau du serveur qui empêche les applications et les outils externes de se connecter au serveur ou à toute base de données sur le serveur, sauf si une règle de pare-feu est créée pour ouvrir le pare-feu à des adresses IP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="fcc42-172">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="fcc42-173">Suivez ces étapes pour créer une [règle de pare-feu au niveau du serveur de base de données SQL](sql-database-firewall-configure.md) pour l’adresse IP de votre client afin de permettre la connectivité externe via le pare-feu de base de données SQL pour votre adresse IP uniquement.</span><span class="sxs-lookup"><span data-stu-id="fcc42-173">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="fcc42-174">SQL Database communique par le biais du port 1433.</span><span class="sxs-lookup"><span data-stu-id="fcc42-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="fcc42-175">Si vous essayez de vous connecter à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 peut ne pas être autorisé par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="fcc42-175">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="fcc42-176">Dans ce cas, vous ne pouvez pas vous connecter à votre serveur Azure SQL Database, sauf si votre service informatique ouvre le port 1433.</span><span class="sxs-lookup"><span data-stu-id="fcc42-176">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="fcc42-177">Une fois le déploiement terminé, cliquez sur **Bases de données SQL** dans le menu de gauche, puis cliquez sur **mySampleDatabase** sur la page **Bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-177">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="fcc42-178">La page de présentation de votre base de données s’ouvre, affiche le nom de serveur complet (tel que **mynewserver20170313.database.windows.net**) et fournit des options pour poursuivre la configuration.</span><span class="sxs-lookup"><span data-stu-id="fcc42-178">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="fcc42-179">Copiez ce nom de serveur complet pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="fcc42-180">Vous avez besoin du nom complet du serveur pour vous connecter à votre serveur et à ses bases de données dans les guides de démarrage rapide suivants.</span><span class="sxs-lookup"><span data-stu-id="fcc42-180">You need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

   ![nom du serveur](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="fcc42-182">Cliquez sur **Définir le pare-feu du serveur** dans la barre d’outils, comme illustré sur l’image précédente.</span><span class="sxs-lookup"><span data-stu-id="fcc42-182">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="fcc42-183">La page **Paramètres de pare-feu** du serveur de base de données SQL s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="fcc42-183">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![règle de pare-feu de serveur](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="fcc42-185">Dans la barre d’outils, cliquez sur **Ajouter une adresse IP cliente** afin d’ajouter votre adresse IP actuelle à une nouvelle règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="fcc42-185">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="fcc42-186">Une règle de pare-feu peut ouvrir le port 1433 pour une seule adresse IP ou une plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="fcc42-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="fcc42-187">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-187">Click **Save**.</span></span> <span data-ttu-id="fcc42-188">Une règle de pare-feu au niveau du serveur est créée pour votre adresse IP actuelle et ouvre le port 1433 sur le serveur logique.</span><span class="sxs-lookup"><span data-stu-id="fcc42-188">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

   ![définir la règle de pare-feu de serveur](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="fcc42-190">Cliquez sur **OK**, puis fermez la page **Paramètres de pare-feu**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-190">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="fcc42-191">Vous pouvez maintenant vous connecter au serveur SQL Database et à ses bases de données à l’aide de SQL Server Management Studio ou de tout autre outil de votre choix à partir de cette adresse IP à l’aide du compte Administrateur de serveur créé au préalable.</span><span class="sxs-lookup"><span data-stu-id="fcc42-191">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcc42-192">Par défaut, l’accès via le pare-feu SQL Database est activé pour tous les services Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-192">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="fcc42-193">Cliquez sur **ÉTEINT** sur cette page pour le désactiver pour tous les services Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-193">Click **OFF** on this page to disable for all Azure services.</span></span>
>

## <a name="query-the-sql-database"></a><span data-ttu-id="fcc42-194">Interroger la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="fcc42-194">Query the SQL database</span></span>

<span data-ttu-id="fcc42-195">Maintenant que vous avez créé un exemple de base de données dans Azure, nous allons utiliser l’outil de requête intégré au portail Azure pour vérifier que vous pouvez vous connecter à la base de données et demander des données.</span><span class="sxs-lookup"><span data-stu-id="fcc42-195">Now that you have created a sample database in Azure, let’s use the built-in query tool within the Azure portal to confirm that you can connect to the database and query the data.</span></span> 

1. <span data-ttu-id="fcc42-196">Sur la page SQL Database de votre base de données, cliquez sur **Outils** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="fcc42-196">On the SQL Database page for your database, click **Tools** on the toolbar.</span></span> <span data-ttu-id="fcc42-197">La page **Outils** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="fcc42-197">The **Tools** page opens.</span></span>

   ![menu Outils](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="fcc42-199">Cliquez sur **Éditeur de requêtes (version préliminaire)**, cochez la case **Conditions d’utilisation de la version préliminaire**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-199">Click **Query editor (preview)**, click the **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="fcc42-200">La page de l’éditeur de requêtes s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="fcc42-200">The Query editor page opens.</span></span>

3. <span data-ttu-id="fcc42-201">Cliquez sur **Connexion**, puis, lorsque vous y êtes invité, sélectionnez **Authentification du serveur SQL Server** et indiquez l’identifiant et le mot de passe de connexion administrateur créés précédemment.</span><span class="sxs-lookup"><span data-stu-id="fcc42-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide the server admin login and password that you created earlier.</span></span>

   ![se connecter](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="fcc42-203">Cliquez sur **OK** pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="fcc42-203">Click **OK** to log in.</span></span>

5. <span data-ttu-id="fcc42-204">Après vous être authentifié, saisissez la requête suivante dans le volet de l’éditeur de requête.</span><span class="sxs-lookup"><span data-stu-id="fcc42-204">After you are authenticated, type the following query in the query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="fcc42-205">Cliquez sur **Exécuter**, puis passez en revue les résultats de la requête dans le volet **Résultats**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-205">Click **Run** and then review the query results in the **Results** pane.</span></span>

   ![query editor results](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="fcc42-207">Fermez la page **Éditeur de requêtes** et la page **Outils**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-207">Close the **Query editor** page and the **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="fcc42-208">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="fcc42-208">Clean up resources</span></span>

<span data-ttu-id="fcc42-209">Si vous n’avez pas besoin de ces ressources pour un autre didacticiel de démarrage rapide (voir [Étapes suivantes](#next-steps)), vous pouvez les supprimer en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="fcc42-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing the following:</span></span>


1. <span data-ttu-id="fcc42-210">Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis sur **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-210">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="fcc42-211">Sur la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez **myResourceGroup** dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fcc42-211">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcc42-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fcc42-212">Next steps</span></span>

<span data-ttu-id="fcc42-213">Maintenant que vous disposez d’une base de données, vous pouvez vous connecter et interroger à l’aide de vos outils préférés.</span><span class="sxs-lookup"><span data-stu-id="fcc42-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="fcc42-214">En savoir plus en choisissant votre outil ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fcc42-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="fcc42-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="fcc42-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="fcc42-216">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fcc42-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="fcc42-217">.NET</span><span class="sxs-lookup"><span data-stu-id="fcc42-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="fcc42-218">PHP</span><span class="sxs-lookup"><span data-stu-id="fcc42-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="fcc42-219">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fcc42-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="fcc42-220">Java</span><span class="sxs-lookup"><span data-stu-id="fcc42-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="fcc42-221">Python</span><span class="sxs-lookup"><span data-stu-id="fcc42-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="fcc42-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="fcc42-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
