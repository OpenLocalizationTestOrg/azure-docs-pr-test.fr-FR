---
title: "Portail Azure : Créer une base de données SQL | Microsoft Docs"
description: "Découvrez comment toocreate un serveur logique de base de données SQL, les règles de pare-feu de niveau serveur et les bases de données hello portail Azure. Vous découvrirez également tooquery une base de données SQL Azure à l’aide de hello portail Azure."
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
ms.openlocfilehash: d30352d834f2007e0b6b3eabfc3c108c61479b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-database-in-hello-azure-portal"></a><span data-ttu-id="160fb-105">Créer une base de données SQL Azure Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="160fb-105">Create an Azure SQL database in hello Azure portal</span></span>

<span data-ttu-id="160fb-106">Ce didacticiel de démarrage rapide Guide comment toocreate SQL de base de données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="160fb-106">This quick start tutorial walks through how toocreate a SQL database in Azure.</span></span> <span data-ttu-id="160fb-107">Base de données SQL Azure est un « de base de données-as-a-Service » de l’offre qui vous permet de toorun et l’échelle haute disponibilités SQL Server bases de données dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="160fb-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you toorun and scale highly available SQL Server databases in hello cloud.</span></span> <span data-ttu-id="160fb-108">Ce guide de démarrage rapide vous montre comment tooget démarrer en créant une base de données SQL à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="160fb-108">This quick start shows you how tooget started by creating a SQL database using hello Azure portal.</span></span>

<span data-ttu-id="160fb-109">Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="160fb-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="160fb-110">Ouvrez une session dans toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="160fb-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="160fb-111">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="160fb-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="160fb-112">Créer une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="160fb-112">Create a SQL database</span></span>

<span data-ttu-id="160fb-113">Une base de données SQL Azure est créée avec un ensemble défini de [ressources de calcul et de stockage](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="160fb-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="160fb-114">base de données Hello est créé dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) et dans un [serveur logique de base de données SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="160fb-114">hello database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="160fb-115">Suivez ces étapes toocreate une base de données SQL contenant les données d’exemple Adventure Works LT hello.</span><span class="sxs-lookup"><span data-stu-id="160fb-115">Follow these steps toocreate a SQL database containing hello Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="160fb-116">Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="160fb-116">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="160fb-117">Sélectionnez **bases de données** de hello **nouveau** page, puis sélectionnez **base de données SQL** de hello **bases de données** page.</span><span class="sxs-lookup"><span data-stu-id="160fb-117">Select **Databases** from hello **New** page, and select **SQL Database** from hello **Databases** page.</span></span>

   ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="160fb-119">Rempliront hello de base de données SQL avec hello suivant d’informations, comme indiqué dans le hello précédant l’image :</span><span class="sxs-lookup"><span data-stu-id="160fb-119">Fill out hello SQL Database form with hello following information, as shown on hello preceding image:</span></span>   

   | <span data-ttu-id="160fb-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="160fb-120">Setting</span></span>       | <span data-ttu-id="160fb-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="160fb-121">Suggested value</span></span> | <span data-ttu-id="160fb-122">Description</span><span class="sxs-lookup"><span data-stu-id="160fb-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="160fb-123">**Nom de la base de données**</span><span class="sxs-lookup"><span data-stu-id="160fb-123">**Database name**</span></span> | <span data-ttu-id="160fb-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="160fb-124">mySampleDatabase</span></span> | <span data-ttu-id="160fb-125">Pour les noms de base de données valides, consultez [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données).</span><span class="sxs-lookup"><span data-stu-id="160fb-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="160fb-126">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="160fb-126">**Subscription**</span></span> | <span data-ttu-id="160fb-127">Votre abonnement</span><span class="sxs-lookup"><span data-stu-id="160fb-127">Your subscription</span></span>  | <span data-ttu-id="160fb-128">Pour plus d’informations sur vos abonnements, consultez [Abonnements](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="160fb-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="160fb-129">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="160fb-129">**Resource group**</span></span>  | <span data-ttu-id="160fb-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="160fb-130">myResourceGroup</span></span> | <span data-ttu-id="160fb-131">Pour les noms de groupe de ressources valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom).</span><span class="sxs-lookup"><span data-stu-id="160fb-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="160fb-132">**Source**</span><span class="sxs-lookup"><span data-stu-id="160fb-132">**Source source**</span></span> | <span data-ttu-id="160fb-133">Exemple (AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="160fb-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="160fb-134">Charge de hello AdventureWorksLT schéma et les données dans votre nouvelle base de données</span><span class="sxs-lookup"><span data-stu-id="160fb-134">Loads hello AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="160fb-135">Vous devez sélectionner la base de données exemple hello sur ce formulaire, car il est utilisé dans le reste de hello de ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="160fb-135">You must select hello sample database on this form because it is used in hello remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="160fb-136">Sous **Server**, cliquez sur **configurer les paramètres requis** et remplissez hello écran SQL server (serveur logique) avec hello suivant d’informations, comme indiqué dans le hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="160fb-136">Under **Server**, click **Configure required settings** and fill out hello SQL server (logical server) form with hello following information, as shown on hello following image:</span></span>   

   | <span data-ttu-id="160fb-137">Paramètre</span><span class="sxs-lookup"><span data-stu-id="160fb-137">Setting</span></span>       | <span data-ttu-id="160fb-138">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="160fb-138">Suggested value</span></span> | <span data-ttu-id="160fb-139">Description</span><span class="sxs-lookup"><span data-stu-id="160fb-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="160fb-140">**Nom du serveur**</span><span class="sxs-lookup"><span data-stu-id="160fb-140">**Server name**</span></span> | <span data-ttu-id="160fb-141">Nom globalement unique</span><span class="sxs-lookup"><span data-stu-id="160fb-141">Any globally unique name</span></span> | <span data-ttu-id="160fb-142">Pour les noms de serveur valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom).</span><span class="sxs-lookup"><span data-stu-id="160fb-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="160fb-143">**Connexion d’administrateur du serveur**</span><span class="sxs-lookup"><span data-stu-id="160fb-143">**Server admin login**</span></span> | <span data-ttu-id="160fb-144">Nom valide</span><span class="sxs-lookup"><span data-stu-id="160fb-144">Any valid name</span></span> | <span data-ttu-id="160fb-145">Pour les noms de connexion valides, consultez [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données).</span><span class="sxs-lookup"><span data-stu-id="160fb-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="160fb-146">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="160fb-146">**Password**</span></span> | <span data-ttu-id="160fb-147">Mot de passe valide</span><span class="sxs-lookup"><span data-stu-id="160fb-147">Any valid password</span></span> | <span data-ttu-id="160fb-148">Votre mot de passe doit comporter au moins 8 caractères et contenir des caractères appartenant à trois des hello suivant des catégories : caractères majuscules, minuscules, chiffres et caractères non alphanumériques et.</span><span class="sxs-lookup"><span data-stu-id="160fb-148">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="160fb-149">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="160fb-149">**Subscription**</span></span> | <span data-ttu-id="160fb-150">Votre abonnement</span><span class="sxs-lookup"><span data-stu-id="160fb-150">Your subscription</span></span> | <span data-ttu-id="160fb-151">Pour plus d’informations sur vos abonnements, consultez [Abonnements](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="160fb-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="160fb-152">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="160fb-152">**Resource group**</span></span> | <span data-ttu-id="160fb-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="160fb-153">myResourceGroup</span></span> | <span data-ttu-id="160fb-154">Pour les noms de groupe de ressources valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom).</span><span class="sxs-lookup"><span data-stu-id="160fb-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="160fb-155">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="160fb-155">**Location**</span></span> | <span data-ttu-id="160fb-156">Emplacement valide</span><span class="sxs-lookup"><span data-stu-id="160fb-156">Any valid location</span></span> | <span data-ttu-id="160fb-157">Pour plus d’informations sur les régions, consultez [Régions Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="160fb-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="160fb-158">connexion administrateur de serveur Hello et un mot de passe que vous spécifiez ici sont requis toolog dans toohello server et ses bases de données plus loin dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="160fb-158">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="160fb-159">Retenez ou enregistrez ces informations pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="160fb-159">Remember or record this information for later use.</span></span> 
   >  

   ![create database-server](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="160fb-161">Lorsque vous avez terminé d’écran de hello, cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="160fb-161">When you have completed hello form, click **Select**.</span></span>

6. <span data-ttu-id="160fb-162">Cliquez sur **niveau tarifaire** toospecify hello performances et la couche de niveau de service pour votre nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="160fb-162">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="160fb-163">Utilisez hello curseur tooselect **20 dtu** et **250** Go de stockage.</span><span class="sxs-lookup"><span data-stu-id="160fb-163">Use hello slider tooselect **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="160fb-164">Pour plus d’informations sur les DTU, consultez la page [Qu’est-ce qu’un DTU ?](sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="160fb-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![create database-s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="160fb-166">Après avoir quantité hello sélectionné de dtu, cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="160fb-166">After selected hello amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="160fb-167">Maintenant que vous avez terminé le formulaire de base de données SQL hello, cliquez sur **créer** base de données tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="160fb-167">Now that you have completed hello SQL Database form, click **Create** tooprovision hello database.</span></span> <span data-ttu-id="160fb-168">L’approvisionnement prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="160fb-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="160fb-169">Dans la barre d’outils de hello, cliquez sur **Notifications** processus de déploiement toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="160fb-169">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>

   ![notification](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="160fb-171">créer une règle de pare-feu au niveau du serveur ;</span><span class="sxs-lookup"><span data-stu-id="160fb-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="160fb-172">Hello service de base de données SQL crée un pare-feu à hello au niveau du serveur qui empêche des applications externes et des outils de se connecter toohello server ou des bases de données sur le serveur de hello, sauf si une règle de pare-feu est créée le pare-feu tooopen hello pour des adresses IP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="160fb-172">hello SQL Database service creates a firewall at hello server-level that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="160fb-173">Suivez ces étapes toocreate un [règle de pare-feu de niveau serveur de base de données SQL](sql-database-firewall-configure.md) pour l’adressage IP de votre client et activer la connectivité externe via le pare-feu de base de données SQL hello pour votre adresse IP uniquement.</span><span class="sxs-lookup"><span data-stu-id="160fb-173">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through hello SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="160fb-174">SQL Database communique par le biais du port 1433.</span><span class="sxs-lookup"><span data-stu-id="160fb-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="160fb-175">Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="160fb-175">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="160fb-176">Dans ce cas, serveur de base de données SQL Azure tooyour ne peut pas se connecter à moins que votre service informatique s’ouvre le port 1433.</span><span class="sxs-lookup"><span data-stu-id="160fb-176">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="160fb-177">Une fois le déploiement de hello terminé, cliquez sur **bases de données SQL** de menu à gauche hello, puis cliquez sur **mySampleDatabase** sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="160fb-177">After hello deployment completes, click **SQL databases** from hello left-hand menu and then click **mySampleDatabase** on hello **SQL databases** page.</span></span> <span data-ttu-id="160fb-178">nom de serveur complet Hello page Vue d’ensemble de votre base de données ouvre, affichant vous hello entièrement (tel que **mynewserver20170313.database.windows.net**) et fournit des options de configuration supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="160fb-178">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="160fb-179">Copiez ce nom de serveur complet pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="160fb-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="160fb-180">Vous avez besoin de ce serveur complet nom tooconnect tooyour ses bases de données et dans les Démarrages rapides suivants.</span><span class="sxs-lookup"><span data-stu-id="160fb-180">You need this fully qualified server name tooconnect tooyour server and its databases in subsequent quick starts.</span></span>
   > 

   ![nom du serveur](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="160fb-182">Cliquez sur **définir serveur pare-feu** barre d’outils hello comme indiqué dans l’image précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="160fb-182">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="160fb-183">Hello **des paramètres de pare-feu** page serveur de base de données SQL hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="160fb-183">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

   ![règle de pare-feu de serveur](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="160fb-185">Cliquez sur **ajouter l’adresse IP du client** sur tooadd de barre d’outils hello votre adresse IP actuelle d’adresses tooa nouvelle règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="160fb-185">Click **Add client IP** on hello toolbar tooadd your current IP address tooa new firewall rule.</span></span> <span data-ttu-id="160fb-186">Une règle de pare-feu peut ouvrir le port 1433 pour une seule adresse IP ou une plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="160fb-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="160fb-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="160fb-187">Click **Save**.</span></span> <span data-ttu-id="160fb-188">Une règle de pare-feu de niveau serveur est créée pour votre adresse IP actuelle, ouvrir le port 1433 sur le serveur logique de hello.</span><span class="sxs-lookup"><span data-stu-id="160fb-188">A server-level firewall rule is created for your current IP address opening port 1433 on hello logical server.</span></span>

   ![définir la règle de pare-feu de serveur](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="160fb-190">Cliquez sur **OK** , puis fermez hello **des paramètres de pare-feu** page.</span><span class="sxs-lookup"><span data-stu-id="160fb-190">Click **OK** and then close hello **Firewall settings** page.</span></span>

<span data-ttu-id="160fb-191">Vous pouvez désormais connecter le serveur de base de données SQL toohello et ses bases de données à l’aide de SQL Server Management Studio ou un autre outil de votre choix à partir de cette adresse IP à l’aide du compte d’administrateur de serveur hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="160fb-191">You can now connect toohello SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="160fb-192">Par défaut, l’accès via le pare-feu de base de données SQL hello est activé pour tous les services Azure.</span><span class="sxs-lookup"><span data-stu-id="160fb-192">By default, access through hello SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="160fb-193">Cliquez sur **OFF** sur toodisable de cette page pour tous les services Azure.</span><span class="sxs-lookup"><span data-stu-id="160fb-193">Click **OFF** on this page toodisable for all Azure services.</span></span>
>

## <a name="query-hello-sql-database"></a><span data-ttu-id="160fb-194">Base de données de requête hello SQL</span><span class="sxs-lookup"><span data-stu-id="160fb-194">Query hello SQL database</span></span>

<span data-ttu-id="160fb-195">Maintenant que vous avez créé une base de données d’exemple dans Azure, nous allons utiliser outil de requête intégrées hello dans hello Azure tooconfirm portail que vous pouvez vous connecter à toohello de base de données et interroger des données hello.</span><span class="sxs-lookup"><span data-stu-id="160fb-195">Now that you have created a sample database in Azure, let’s use hello built-in query tool within hello Azure portal tooconfirm that you can connect toohello database and query hello data.</span></span> 

1. <span data-ttu-id="160fb-196">Dans la page de base de données SQL hello pour votre base de données, cliquez sur **outils** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="160fb-196">On hello SQL Database page for your database, click **Tools** on hello toolbar.</span></span> <span data-ttu-id="160fb-197">Hello **outils** ouvrir la page.</span><span class="sxs-lookup"><span data-stu-id="160fb-197">hello **Tools** page opens.</span></span>

   ![menu Outils](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="160fb-199">Cliquez sur **l’éditeur de requête (version préliminaire)**, cliquez sur hello **afficher un aperçu des termes du contrat de** case à cocher, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="160fb-199">Click **Query editor (preview)**, click hello **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="160fb-200">page de l’éditeur de requête Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="160fb-200">hello Query editor page opens.</span></span>

3. <span data-ttu-id="160fb-201">Cliquez sur **connexion** , puis, lorsque vous y êtes invité, sélectionnez **l’authentification SQL server** , puis indiquez le compte de connexion administrateur de serveur hello et mot de passe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="160fb-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide hello server admin login and password that you created earlier.</span></span>

   ![se connecter](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="160fb-203">Cliquez sur **OK** toolog dans.</span><span class="sxs-lookup"><span data-stu-id="160fb-203">Click **OK** toolog in.</span></span>

5. <span data-ttu-id="160fb-204">Une fois que vous êtes authentifié, tapez ce qui suit hello de requête dans le volet de l’éditeur de requête hello.</span><span class="sxs-lookup"><span data-stu-id="160fb-204">After you are authenticated, type hello following query in hello query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="160fb-205">Cliquez sur **exécuter** puis passez en revue les résultats de requête hello Bonjour **résultats** volet.</span><span class="sxs-lookup"><span data-stu-id="160fb-205">Click **Run** and then review hello query results in hello **Results** pane.</span></span>

   ![query editor results](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="160fb-207">Fermer hello **l’éditeur de requête** page et hello **outils** page.</span><span class="sxs-lookup"><span data-stu-id="160fb-207">Close hello **Query editor** page and hello **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="160fb-208">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="160fb-208">Clean up resources</span></span>

<span data-ttu-id="160fb-209">Si vous n’avez pas besoin ces ressources pour un autre/didacticiel de démarrage rapide (consultez [étapes](#next-steps)), vous pouvez les supprimer de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="160fb-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing hello following:</span></span>


1. <span data-ttu-id="160fb-210">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="160fb-210">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="160fb-211">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, type **myResourceGroup** dans hello de zone de texte, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="160fb-211">On your resource group page, click **Delete**, type **myResourceGroup** in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="160fb-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="160fb-212">Next steps</span></span>

<span data-ttu-id="160fb-213">Maintenant que vous disposez d’une base de données, vous pouvez vous connecter et interroger à l’aide de vos outils préférés.</span><span class="sxs-lookup"><span data-stu-id="160fb-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="160fb-214">En savoir plus en choisissant votre outil ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="160fb-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="160fb-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="160fb-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="160fb-216">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="160fb-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="160fb-217">.NET</span><span class="sxs-lookup"><span data-stu-id="160fb-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="160fb-218">PHP</span><span class="sxs-lookup"><span data-stu-id="160fb-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="160fb-219">Node.JS</span><span class="sxs-lookup"><span data-stu-id="160fb-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="160fb-220">Java</span><span class="sxs-lookup"><span data-stu-id="160fb-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="160fb-221">Python</span><span class="sxs-lookup"><span data-stu-id="160fb-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="160fb-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="160fb-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
