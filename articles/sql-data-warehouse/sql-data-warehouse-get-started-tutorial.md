---
title: aaaAzure SQL Data Warehouse - commencer didacticiel | Documents Microsoft
description: "Ce didacticiel vous apprend comment tooprovision et charger les données dans l’entrepôt de données SQL Azure. Vous allez également principes hello sur la mise à l’échelle ou d’interruption et de paramétrage."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="edbbe-104">Prise en main de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="edbbe-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="edbbe-105">Ce didacticiel montre comment tooprovision et charger les données dans l’entrepôt de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="edbbe-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="edbbe-106">Vous allez également principes hello sur la mise à l’échelle ou d’interruption et de paramétrage.</span><span class="sxs-lookup"><span data-stu-id="edbbe-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="edbbe-107">Lorsque vous avez terminé, prêt tooquery et vous explorez votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="edbbe-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="edbbe-108">**Estimation du temps toocomplete :** il s’agit d’un didacticiel de bout en bout avec le code d’exemple qui prend environ 30 minutes toocomplete une fois que vous avez rempli les conditions préalables de hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="edbbe-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="edbbe-109">Prerequisites</span></span>

<span data-ttu-id="edbbe-110">didacticiel de Hello suppose que vous êtes familiarisé avec les concepts de base de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="edbbe-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="edbbe-111">Si vous avez besoin d’une introduction, consultez [En quoi consiste Azure SQL Data Warehouse ?](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="edbbe-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="edbbe-112">S'inscrire à Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="edbbe-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="edbbe-113">Si vous n’avez pas déjà un compte Microsoft Azure, vous devez toosign pour un toouse ce service.</span><span class="sxs-lookup"><span data-stu-id="edbbe-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="edbbe-114">Si vous avez déjà un compte, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="edbbe-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="edbbe-115">Naviguer entre les pages de compte toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="edbbe-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="edbbe-116">Créer un compte Azure gratuit, ou achetez-en un.</span><span class="sxs-lookup"><span data-stu-id="edbbe-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="edbbe-117">Suivez les instructions de hello</span><span class="sxs-lookup"><span data-stu-id="edbbe-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="edbbe-118">Installer les pilotes du client SQL et les outils appropriés</span><span class="sxs-lookup"><span data-stu-id="edbbe-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="edbbe-119">La plupart des outils clients SQL peuvent se connecter tooSQL l’entrepôt de données à l’aide de JDBC, ODBC ou ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="edbbe-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="edbbe-120">En raison de toohello grand nombre de fonctionnalités de T-SQL qui prend en charge de l’entrepôt de données SQL, certaines applications clientes ne sont pas entièrement compatibles avec l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="edbbe-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="edbbe-121">Si vous exécutez un système d’exploitation Windows, nous vous recommandons de recourir à [Visual Studio] ou à [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="edbbe-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="edbbe-122">Créer un entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="edbbe-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="edbbe-123">SQL Data Warehouse est un type spécial de base de données conçu pour le traitement massivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="edbbe-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="edbbe-124">base de données Hello est distribuée sur plusieurs nœuds et traite les requêtes en parallèle.</span><span class="sxs-lookup"><span data-stu-id="edbbe-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="edbbe-125">Entrepôt de données SQL a un nœud de contrôle qui orchestre les activités de tous les nœuds hello hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="edbbe-126">nœuds Hello eux-mêmes utilisent toomanage de la base de données SQL à vos données.</span><span class="sxs-lookup"><span data-stu-id="edbbe-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="edbbe-127">La création d’un entrepôt de données SQL Data Warehouse peut donner lieu à un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="edbbe-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="edbbe-128">Pour en savoir plus, voir [SQL Data Warehouse - Tarification](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="edbbe-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="edbbe-129">Créer un entrepôt de données</span><span class="sxs-lookup"><span data-stu-id="edbbe-129">Create a data warehouse</span></span>

1. <span data-ttu-id="edbbe-130">L’authentification à hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="edbbe-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="edbbe-131">Cliquez sur **Nouveau** > **Bases de données** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="edbbe-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="edbbe-132">![Nouveau panneau](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png)![Choisir DW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="edbbe-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="edbbe-133">Renseignez les détails relatifs au déploiement.</span><span class="sxs-lookup"><span data-stu-id="edbbe-133">Fill out deployment details</span></span>

    <span data-ttu-id="edbbe-134">**Nom de la base de données** : choisissez le nom de votre choix.</span><span class="sxs-lookup"><span data-stu-id="edbbe-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="edbbe-135">Si vous avez plusieurs entrepôts de données, nous vous recommandons de vos noms d’incluent des détails tels que la région de hello, environnement, par exemple *mydw-westus-1-test*.</span><span class="sxs-lookup"><span data-stu-id="edbbe-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="edbbe-136">**Abonnement** : votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="edbbe-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="edbbe-137">**Groupe de ressources** : créez un groupe de ressources ou utilisez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="edbbe-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="edbbe-138">Les groupes de ressources sont utiles pour administrer les ressources (définition de la portée du contrôle d’accès et déploiement basé sur des modèles, par exemple).</span><span class="sxs-lookup"><span data-stu-id="edbbe-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="edbbe-139">Découvrez [ici](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) plus d’informations sur les groupes de ressources et meilleures pratiques Azure.</span><span class="sxs-lookup"><span data-stu-id="edbbe-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="edbbe-140">**Source** : base de données vide.</span><span class="sxs-lookup"><span data-stu-id="edbbe-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="edbbe-141">**Serveur**: serveur hello sélectionnez créé dans [conditions préalables].</span><span class="sxs-lookup"><span data-stu-id="edbbe-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="edbbe-142">**Classement**: laissez le classement par défaut de hello SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="edbbe-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="edbbe-143">**Sélectionnez performance**: nous vous recommandons de commencer avec 400DWU standard de hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="edbbe-144">Choisissez **code confidentiel toodashboard** ![tooDashboard du code confidentiel](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="edbbe-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="edbbe-145">Confortablement et attendez que votre toodeploy de l’entrepôt de données !</span><span class="sxs-lookup"><span data-stu-id="edbbe-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="edbbe-146">Il est normal pour cette tootake processus plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="edbbe-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="edbbe-147">portail de Hello vous avertit lorsque votre entrepôt de données est prêt toouse.</span><span class="sxs-lookup"><span data-stu-id="edbbe-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="edbbe-148">Se connecter tooSQL l’entrepôt de données</span><span class="sxs-lookup"><span data-stu-id="edbbe-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="edbbe-149">Ce didacticiel utilise l’entrepôt de données SQL Server Management Studio (SSMS) tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="edbbe-150">Vous pouvez vous connecter tooSQL l’entrepôt de données via ces connecteurs pris en charge : ADO.NET, JDBC, ODBC et PHP.</span><span class="sxs-lookup"><span data-stu-id="edbbe-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="edbbe-151">N’oubliez pas que les fonctionnalités peuvent être limitées si les outils ne sont pas pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="edbbe-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="edbbe-152">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="edbbe-152">Get connection information</span></span>

<span data-ttu-id="edbbe-153">tooconnect tooyour l’entrepôt de données, vous devez tooconnect via hello logique SQL server vous avez créé dans [conditions préalables].</span><span class="sxs-lookup"><span data-stu-id="edbbe-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="edbbe-154">Sélectionnez votre entrepôt de données à partir du tableau de bord hello ou la recherche de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="edbbe-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![Tableau de bord SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="edbbe-156">Rechercher le nom complet de hello pour hello logique SQL server.</span><span class="sxs-lookup"><span data-stu-id="edbbe-156">Find hello full name for hello logical SQL server.</span></span>

    ![Sélection du nom du serveur](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="edbbe-158">Ouvrez SSMS et utiliser objet explorer tooconnect toothis serveur utilisant hello informations d’identification administrateur serveur vous avez créé dans [conditions préalables]</span><span class="sxs-lookup"><span data-stu-id="edbbe-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![Connexion avec SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="edbbe-160">Si tout se passe correctement, vous devez maintenant être connecté tooyour logique SQL server.</span><span class="sxs-lookup"><span data-stu-id="edbbe-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="edbbe-161">Étant donné que vous connecté comme administrateur du serveur de hello, vous pouvez vous connecter tooany de base de données hébergée par serveur hello, y compris la base de données master hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="edbbe-162">Compte d’administrateur qu’un seul serveur est et il a hello la plupart des privilèges d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="edbbe-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="edbbe-163">Veillez à ne pas tooallow trop d’utilisateurs dans votre mot de passe d’administrateur organisation tooknow hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="edbbe-164">Vous pouvez également posséder un compte d’administrateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="edbbe-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="edbbe-165">Nous ne fournissent pas ici les détails hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-165">We don't provide hello details here.</span></span> <span data-ttu-id="edbbe-166">Si vous souhaitez toolearn plus en détail à l’aide de l’authentification Azure Active Directory, voir [d’authentification Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="edbbe-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="edbbe-167">Nous étudions maintenant la création d’utilisateurs et d’information de connexion supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="edbbe-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="edbbe-168">Créer un utilisateur de base de données</span><span class="sxs-lookup"><span data-stu-id="edbbe-168">Create a database user</span></span>

<span data-ttu-id="edbbe-169">Dans cette étape, vous créez un tooaccess de compte d’utilisateur votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="edbbe-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="edbbe-170">Nous vous montrons également comment toogive ce toorun de capacité hello utilisateur interroge avec une grande quantité de mémoire et des ressources processeur.</span><span class="sxs-lookup"><span data-stu-id="edbbe-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="edbbe-171">Remarques sur les classes de ressources pour allouer les ressources tooqueries</span><span class="sxs-lookup"><span data-stu-id="edbbe-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="edbbe-172">tookeep vos données en sécurité, n’utilisez pas des requêtes hello server administration toorun sur vos bases de données de production.</span><span class="sxs-lookup"><span data-stu-id="edbbe-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="edbbe-173">Il a hello de la plupart des privilèges d’un utilisateur et l’utiliser tooperform opérations sur les données utilisateur expose vos données à un risque.</span><span class="sxs-lookup"><span data-stu-id="edbbe-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="edbbe-174">En outre, étant donné que l’administrateur du serveur hello vise tooperform les opérations de gestion, il exécute des opérations avec qu’une petite allocation de mémoire et des ressources processeur.</span><span class="sxs-lookup"><span data-stu-id="edbbe-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="edbbe-175">SQL Data Warehouse utilise des rôles de base de données prédéfinis, appelées classes de ressources, tooallocate différentes quantités de mémoire, les ressources du processeur et toousers des emplacements d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="edbbe-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="edbbe-176">Chaque utilisateur peut appartenir la classe de ressource de petite, moyenne, grande ou très grand tooa.</span><span class="sxs-lookup"><span data-stu-id="edbbe-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="edbbe-177">Hello classe de ressource de l’utilisateur détermine hello ressources hello utilisateur toorun requêtes et opérations de chargement.</span><span class="sxs-lookup"><span data-stu-id="edbbe-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="edbbe-178">Pour la compression des données optimale, hello est nécessaire tooload de grande taille ou des allocations de ressources très volumineux.</span><span class="sxs-lookup"><span data-stu-id="edbbe-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="edbbe-179">Découvrez plus d’informations sur les classes de ressource [ici](./sql-data-warehouse-develop-concurrency.md#resource-classes) :</span><span class="sxs-lookup"><span data-stu-id="edbbe-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="edbbe-180">Créer un compte pouvant contrôler une base de données</span><span class="sxs-lookup"><span data-stu-id="edbbe-180">Create an account that can control a database</span></span>

<span data-ttu-id="edbbe-181">Étant donné que vous êtes actuellement connecté comme administrateur du serveur de hello vous disposez des autorisations toocreate connexions et les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="edbbe-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="edbbe-182">À l’aide de SSMS ou d’un autre client de requête, ouvrez une nouvelle requête pour **master**.</span><span class="sxs-lookup"><span data-stu-id="edbbe-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Nouvelle requête sur Master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nouvelle requête sur Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="edbbe-185">Dans la fenêtre de requête hello, exécutez cette toocreate de commande T-SQL, une connexion nommée MedRCLogin et un utilisateur nommé LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="edbbe-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="edbbe-186">Cette connexion peut se connecter toohello logique SQL server.</span><span class="sxs-lookup"><span data-stu-id="edbbe-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="edbbe-187">Maintenant interrogation hello *base de données SQL Data Warehouse*, créez un utilisateur de base de données en fonction hello de connexion que vous avez créé tooaccess et effectuer des opérations sur la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="edbbe-188">Donnez à hello de base de données utilisateur contrôle autorisations toohello base de données appelée NYT.</span><span class="sxs-lookup"><span data-stu-id="edbbe-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="edbbe-189">Si le nom de votre base de données comporte des traits d’union, être toowrap que dans les crochets !</span><span class="sxs-lookup"><span data-stu-id="edbbe-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="edbbe-190">Donner des allocations de hello utilisateur moyenne des ressources</span><span class="sxs-lookup"><span data-stu-id="edbbe-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="edbbe-191">Exécutez cette toomake de commande T-SQL informatique, un membre de classe de ressource moyennes hello, qui est appelé mediumrc.</span><span class="sxs-lookup"><span data-stu-id="edbbe-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="edbbe-192">Cliquez sur [ici](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn plus d’informations sur les classes d’accès concurrentiel et de ressources !</span><span class="sxs-lookup"><span data-stu-id="edbbe-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="edbbe-193">Connecter le serveur logique de toohello avec nouvelles informations d’identification de hello</span><span class="sxs-lookup"><span data-stu-id="edbbe-193">Connect toohello logical server with hello new credentials</span></span>

    ![Connexion avec le nouveau compte de connexion](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="edbbe-195">Charger des données à partir d’objets Blob Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="edbbe-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="edbbe-196">Vous êtes maintenant les données tooload prêt dans votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="edbbe-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="edbbe-197">Cette étape vous montre comment les données de fichier cab tooload New York City taxi à partir d’un stockage Azure public blob.</span><span class="sxs-lookup"><span data-stu-id="edbbe-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="edbbe-198">Une méthode courante données tooload dans SQL Data Warehouse sont toofirst déplacer le stockage d’objets blob hello données tooAzure et puis son chargement dans votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="edbbe-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="edbbe-199">toomake il toounderstand plus facilement comment tooload, nous disposons de New York taxi cab données déjà hébergées dans un objet blob de stockage Azure publique.</span><span class="sxs-lookup"><span data-stu-id="edbbe-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="edbbe-200">Pour référence ultérieure, toolearn comment tooget votre tooAzure de données d’objets blob de stockage ou tooload il directement à partir de votre source dans l’entrepôt de données SQL, consultez hello [vue d’ensemble de chargement](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="edbbe-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="edbbe-201">Définir des données externes</span><span class="sxs-lookup"><span data-stu-id="edbbe-201">Define external data</span></span>

1. <span data-ttu-id="edbbe-202">Créez une clé principale.</span><span class="sxs-lookup"><span data-stu-id="edbbe-202">Create a master key.</span></span> <span data-ttu-id="edbbe-203">Vous ne devez toocreate une clé principale une fois par base de données.</span><span class="sxs-lookup"><span data-stu-id="edbbe-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="edbbe-204">Définir emplacement hello hello Azure blob qui contient les données de fichier cab taxi hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="edbbe-205">Définir des formats de fichier externe hello</span><span class="sxs-lookup"><span data-stu-id="edbbe-205">Define hello external file formats</span></span>

    <span data-ttu-id="edbbe-206">Hello ```CREATE EXTERNAL FILE FORMAT``` commande est utilisée toospecify le format des fichiers qui contiennent des données externes hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="edbbe-207">Ils contiennent du texte séparé par un ou plusieurs caractères, appelés délimiteurs.</span><span class="sxs-lookup"><span data-stu-id="edbbe-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="edbbe-208">À des fins de démonstration, les données de fichier cab taxi hello sont stockées à la fois des données et les données gzip compressées.</span><span class="sxs-lookup"><span data-stu-id="edbbe-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="edbbe-209">Exécuter ces commandes T-SQL de toodefine deux formats : non compressés et compressé.</span><span class="sxs-lookup"><span data-stu-id="edbbe-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="edbbe-210">Créez un schéma pour le format de fichier externe.</span><span class="sxs-lookup"><span data-stu-id="edbbe-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="edbbe-211">Créer des tables externes hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-211">Create hello external tables.</span></span> <span data-ttu-id="edbbe-212">Ces tables référencent les données stockées dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="edbbe-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="edbbe-213">Exécutez hello suivant toocreate de commandes T-SQL de plusieurs tables externes que toohello point tous les objets blob Azure nous défini précédemment dans notre source de données externe.</span><span class="sxs-lookup"><span data-stu-id="edbbe-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="edbbe-214">Importer les données de salutation depuis le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="edbbe-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="edbbe-215">SQL Data Warehouse prend en charge une instruction clé appelée CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="edbbe-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="edbbe-216">Cette instruction crée une nouvelle table basée sur les résultats d’une instruction select hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="edbbe-217">Hello nouvelle table a hello les mêmes colonnes et types de données comme résultats hello Hello select (instruction).</span><span class="sxs-lookup"><span data-stu-id="edbbe-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="edbbe-218">Il s’agit d’une données tooimport de manière élégante à partir du stockage d’objets blob Azure dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="edbbe-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="edbbe-219">Exécutez ce script tooimport vos données.</span><span class="sxs-lookup"><span data-stu-id="edbbe-219">Run this script tooimport your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="edbbe-220">Affichez vos données à mesure qu’elles sont chargées.</span><span class="sxs-lookup"><span data-stu-id="edbbe-220">View your data as it loads.</span></span>

   <span data-ttu-id="edbbe-221">Vous chargez plusieurs gigaoctets de données et les compressez au sein d’index de cluster columnstore hautes performances.</span><span class="sxs-lookup"><span data-stu-id="edbbe-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="edbbe-222">Exécutez hello suivant la requête qui utilise un état de hello gestion dynamique (DMV) de vues tooshow de charge de hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="edbbe-223">Après le démarrage de la requête de hello, saisissez un café et une tasse SQL Data Warehouse Contrairement à certaines tâches.</span><span class="sxs-lookup"><span data-stu-id="edbbe-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="edbbe-224">Affichez toutes les requêtes du système.</span><span class="sxs-lookup"><span data-stu-id="edbbe-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="edbbe-225">Vous pouvez constater que vos données sont efficacement chargées dans votre entrepôt Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="edbbe-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Affichage des données chargées](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="edbbe-227">Améliorer les performances des requêtes</span><span class="sxs-lookup"><span data-stu-id="edbbe-227">Improve query performance</span></span>

<span data-ttu-id="edbbe-228">Performances des requêtes de plusieurs façons tooimprove et performances haut débit tooachieve hello qui est de l’entrepôt de données SQL conçue tooprovide.</span><span class="sxs-lookup"><span data-stu-id="edbbe-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="edbbe-229">Voir effet hello de mise à l’échelle sur les performances des requêtes</span><span class="sxs-lookup"><span data-stu-id="edbbe-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="edbbe-230">Performances des requêtes tooimprove unidirectionnel sont tooscale ressources en modifiant le niveau de service hello DWU de votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="edbbe-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="edbbe-231">Chaque niveau de service est plus onéreux, mais vous pouvez réduire la taille des ressources ou les mettre en pause à tout moment.</span><span class="sxs-lookup"><span data-stu-id="edbbe-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="edbbe-232">Lors de cette étape, vous comparez les performances de deux paramètres DWU différents.</span><span class="sxs-lookup"><span data-stu-id="edbbe-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="edbbe-233">Tout d’abord, nous allons mettre à l’échelle de dimensionnement hello too100 DWU afin de nous pouvons obtenir une idée de la manière dont un nœud de calcul peut s’exécuter sur son propre vers le bas.</span><span class="sxs-lookup"><span data-stu-id="edbbe-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="edbbe-234">Toohello portail, sélectionnez votre entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="edbbe-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="edbbe-235">Sélectionnez l’échelle dans le panneau de l’entrepôt de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![Mise à l’échelle de l’instance SQL Data Warehouse dans le portail](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="edbbe-237">Performances hello barre too100 DWU à l’échelle et cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="edbbe-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![Mise à l’échelle et enregistrement](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="edbbe-239">Attendez que votre toofinish d’opération de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="edbbe-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="edbbe-240">Impossible d’exécuter des requêtes lors du changement d’échelle de hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="edbbe-241">La mise à l’échelle **supprime** vos requêtes en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="edbbe-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="edbbe-242">Vous pourrez les redémarrer lorsque hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="edbbe-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="edbbe-243">Effectuer une opération d’analyse sur les données de voyage hello, en sélectionnant millions entrées de hello supérieur pour toutes les colonnes hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="edbbe-244">Si vous êtes toomove hâtif sur rapidement, vous pouvez tooselect libre moins de lignes.</span><span class="sxs-lookup"><span data-stu-id="edbbe-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="edbbe-245">Prenez note de hello temps toorun cette opération.</span><span class="sxs-lookup"><span data-stu-id="edbbe-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="edbbe-246">Mettre à l’échelle de votre entrepôt de données de sauvegarde too400 DWU.</span><span class="sxs-lookup"><span data-stu-id="edbbe-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="edbbe-247">N’oubliez pas de chaque DWU 100 consiste à ajouter un autre tooyour de nœud de calcul Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="edbbe-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="edbbe-248">Réexécutez la requête de hello !</span><span class="sxs-lookup"><span data-stu-id="edbbe-248">Run hello query again!</span></span> <span data-ttu-id="edbbe-249">Vous devriez remarquer une différence importante.</span><span class="sxs-lookup"><span data-stu-id="edbbe-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="edbbe-250">Requête de hello retourne une grande quantité de données, disponibilité de la bande passante hello d’ordinateur hello SSMS en cours d’exécution peut-être ne pas être un goulot d’étranglement.</span><span class="sxs-lookup"><span data-stu-id="edbbe-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="edbbe-251">Cela peut vous empêcher de noter des améliorations des performances !</span><span class="sxs-lookup"><span data-stu-id="edbbe-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="edbbe-252">Étant donné que SQL Data Warehouse utilise le traitement massivement parallèle,</span><span class="sxs-lookup"><span data-stu-id="edbbe-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="edbbe-253">Les requêtes qui analyse ou d’effectuer des fonctions analytiques sur des millions de lignes tirer hello véritable puissance de Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="edbbe-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="edbbe-254">Voir l’effet hello des statistiques sur les performances des requêtes</span><span class="sxs-lookup"><span data-stu-id="edbbe-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="edbbe-255">Exécuter une requête que les jointures hello table Date avec la table de voyage hello</span><span class="sxs-lookup"><span data-stu-id="edbbe-255">Run a query that joins hello Date table with hello Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="edbbe-256">Cette requête prend un certain temps car SQL Data Warehouse contient des données de tooshuffle avant de pouvoir effectuer la jointure de hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="edbbe-257">Jointures de données ne sont pas tooshuffle s’ils sont conçus toojoin données hello même façon, il est distribué.</span><span class="sxs-lookup"><span data-stu-id="edbbe-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="edbbe-258">Il s’agit d’un thème plus spécifique.</span><span class="sxs-lookup"><span data-stu-id="edbbe-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="edbbe-259">Les statistiques font la différence.</span><span class="sxs-lookup"><span data-stu-id="edbbe-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="edbbe-260">Exécutez cette toocreate les statistiques instruction sur les colonnes de jointure hello.</span><span class="sxs-lookup"><span data-stu-id="edbbe-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="edbbe-261">Azure SQL Data Warehouse ne gère pas automatiquement les statistiques pour vous.</span><span class="sxs-lookup"><span data-stu-id="edbbe-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="edbbe-262">Or, ces statistiques sont importantes pour déterminer les performances des requêtes. Il est donc fortement recommandé de créer et de mettre à jour les statistiques.</span><span class="sxs-lookup"><span data-stu-id="edbbe-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="edbbe-263">**Vous pouvez bénéficier hello plus en ayant des statistiques sur des colonnes impliquées dans les jointures, les colonnes utilisées dans hello où clause et colonnes trouvent dans GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="edbbe-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="edbbe-264">Réexécutez hello requête à la configuration requise et observez les différences de performances.</span><span class="sxs-lookup"><span data-stu-id="edbbe-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="edbbe-265">Pendant les différences de hello dans les performances des requêtes ne sera pas aussi radicales que l’évolution verticale, vous devez remarquer une accélération.</span><span class="sxs-lookup"><span data-stu-id="edbbe-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="edbbe-266">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="edbbe-266">Next steps</span></span>

<span data-ttu-id="edbbe-267">Vous êtes maintenant prêt tooquery et Explorer.</span><span class="sxs-lookup"><span data-stu-id="edbbe-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="edbbe-268">Découvrez nos meilleures pratiques et nos conseils !</span><span class="sxs-lookup"><span data-stu-id="edbbe-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="edbbe-269">Si vous avez terminé exploration jours hello, de rendre toopause que votre instance !</span><span class="sxs-lookup"><span data-stu-id="edbbe-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="edbbe-270">En production, vous pouvez être confronté économies considérables en suspendant et mise à l’échelle toomeet besoins de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="edbbe-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![Suspendre](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="edbbe-272">Documents utiles</span><span class="sxs-lookup"><span data-stu-id="edbbe-272">Useful readings</span></span>

<span data-ttu-id="edbbe-273">[Gestion de la concurrence et des charges de travail][]</span><span class="sxs-lookup"><span data-stu-id="edbbe-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="edbbe-274">[Meilleures pratiques pour Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="edbbe-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="edbbe-275">[surveillance des requêtes][]</span><span class="sxs-lookup"><span data-stu-id="edbbe-275">[Query Monitoring][]</span></span>

<span data-ttu-id="edbbe-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][] (10 meilleures pratiques pour la création d’un entrepôt de données relationnelles à grande échelle)</span><span class="sxs-lookup"><span data-stu-id="edbbe-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="edbbe-277">[Migration tooAzure de données SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="edbbe-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[Gestion de la concurrence et des charges de travail]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Meilleures pratiques pour Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[surveillance des requêtes]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/ (10 meilleures pratiques pour la création d’un entrepôt de données relationnelles à grande échelle)
[Migration tooAzure de données SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[conditions préalables]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
