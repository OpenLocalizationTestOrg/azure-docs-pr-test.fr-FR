---
title: "Azure SQL Data Warehouse : didacticiel de prise en main | Microsoft Docs"
description: "Ce didacticiel vous apprend à approvisionner et charger des données dans Azure SQL Data Warehouse. Vous allez également découvrir les principes de base de mise à l’échelle, de mise en attente et de réglage."
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
ms.openlocfilehash: 95e14824ba3b705bb909ec983652dd3305b98805
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="dcf7b-104">Prise en main de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="dcf7b-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="dcf7b-105">Ce didacticiel va vous montrer comment approvisionner et charger des données dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-105">This tutorial shows how to provision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="dcf7b-106">Vous allez également découvrir les principes de base de mise à l’échelle, de mise en attente et de réglage.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-106">You’ll also learn the basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="dcf7b-107">Lorsque vous aurez terminé, vous serez prêt à interroger et à explorer votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-107">When you’re finished, you’ll be ready to query and explore your data warehouse.</span></span>

<span data-ttu-id="dcf7b-108">**Durée de réalisation estimée :** la réalisation de ce didacticiel de bout en bout contenant un exemple de code prend environ 30 minutes une fois que vous avez rempli les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-108">**Estimated time to complete:** This is an end-to-end tutorial with example code that takes about 30 minutes to complete once you have met the prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dcf7b-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dcf7b-109">Prerequisites</span></span>

<span data-ttu-id="dcf7b-110">Ce didacticiel part du principe que vous connaissez bien les concepts de base de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-110">The tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="dcf7b-111">Si vous avez besoin d’une introduction, consultez [En quoi consiste Azure SQL Data Warehouse ?](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="dcf7b-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="dcf7b-112">S'inscrire à Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="dcf7b-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="dcf7b-113">Si vous ne disposez pas d’un compte Microsoft Azure, vous devez vous inscrire pour utiliser ce service.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-113">If you don't already have a Microsoft Azure account, you need to sign up for one to use this service.</span></span> <span data-ttu-id="dcf7b-114">Si vous avez déjà un compte, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="dcf7b-115">Accédez aux pages de compte à l’adresse [https://azure.microsoft.com/fr-fr/account/](https://azure.microsoft.com/account/).</span><span class="sxs-lookup"><span data-stu-id="dcf7b-115">Navigate to the account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="dcf7b-116">Créer un compte Azure gratuit, ou achetez-en un.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="dcf7b-117">Suivez les instructions.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-117">Follow the instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="dcf7b-118">Installer les pilotes du client SQL et les outils appropriés</span><span class="sxs-lookup"><span data-stu-id="dcf7b-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="dcf7b-119">La plupart des outils du client SQL peuvent se connecter à SQL Data Warehouse à l’aide de JDBC, ODBC ou ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-119">Most SQL client tools can connect to SQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="dcf7b-120">En raison du grand nombre de fonctionnalités T-SQL prises en charge par SQL Data Warehouse, certaines applications clientes ne sont pas entièrement compatibles avec SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-120">Due to the large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="dcf7b-121">Si vous exécutez un système d’exploitation Windows, nous vous recommandons de recourir à [Visual Studio] ou à [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="dcf7b-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="dcf7b-122">Créer un entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="dcf7b-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="dcf7b-123">SQL Data Warehouse est un type spécial de base de données conçu pour le traitement massivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="dcf7b-124">La base de données est répartie sur plusieurs nœuds et traite les requêtes en parallèle.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-124">The database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="dcf7b-125">SQL Data Warehouse dispose d’un nœud de contrôle qui orchestre les activités de tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-125">SQL Data Warehouse has a control node that orchestrates the activities of all the nodes.</span></span> <span data-ttu-id="dcf7b-126">Les nœuds eux-mêmes utilisent SQL Database pour gérer vos données.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-126">The nodes themselves use SQL Database to manage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="dcf7b-127">La création d’un entrepôt de données SQL Data Warehouse peut donner lieu à un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="dcf7b-128">Pour en savoir plus, voir [SQL Data Warehouse - Tarification](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="dcf7b-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="dcf7b-129">Créer un entrepôt de données</span><span class="sxs-lookup"><span data-stu-id="dcf7b-129">Create a data warehouse</span></span>

1. <span data-ttu-id="dcf7b-130">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dcf7b-130">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dcf7b-131">Cliquez sur **Nouveau** > **Bases de données** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="dcf7b-132">![Nouveau panneau](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![Choisir DW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="dcf7b-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="dcf7b-133">Renseignez les détails relatifs au déploiement.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-133">Fill out deployment details</span></span>

    <span data-ttu-id="dcf7b-134">**Nom de la base de données** : choisissez le nom de votre choix.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="dcf7b-135">Si vous disposez de plusieurs entrepôts de données, nous vous recommandons d’inclure dans ce nom des détails tels que la région et l’environnement, par exemple *mydw-westus-1-test*.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-135">If you have multiple data warehouses, we recommend your names include details such as the region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="dcf7b-136">**Abonnement** : votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="dcf7b-137">**Groupe de ressources** : créez un groupe de ressources ou utilisez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="dcf7b-138">Les groupes de ressources sont utiles pour administrer les ressources (définition de la portée du contrôle d’accès et déploiement basé sur des modèles, par exemple).</span><span class="sxs-lookup"><span data-stu-id="dcf7b-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="dcf7b-139">Découvrez [ici](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) plus d’informations sur les groupes de ressources et meilleures pratiques Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="dcf7b-140">**Source** : base de données vide.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="dcf7b-141">**Serveur** : sélectionnez le serveur que vous avez créé dans le cadre de la section [Composants requis].</span><span class="sxs-lookup"><span data-stu-id="dcf7b-141">**Server**: Select the server you created in [Prerequisites].</span></span>

    <span data-ttu-id="dcf7b-142">**Classement** : conservez le classement par défaut, à savoir SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-142">**Collation**: Leave the default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="dcf7b-143">**Sélectionner le compteur de performance** : nous vous recommandons de commencer par le modèle 400DWU standard.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-143">**Select performance**: We recommend starting with the standard 400DWU.</span></span>

4. <span data-ttu-id="dcf7b-144">Choisissez **Épingler au tableau de bord** ![Épingler au tableau de bord](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="dcf7b-144">Choose **Pin to dashboard** ![Pin To Dashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="dcf7b-145">Installez-vous confortablement et attendez le déploiement de votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-145">Sit back and wait for your data warehouse to deploy!</span></span> <span data-ttu-id="dcf7b-146">Il est normal que ce processus prenne plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-146">It's normal for this process to take several minutes.</span></span> <span data-ttu-id="dcf7b-147">Le portail vous informe lorsque votre entrepôt de données est opérationnel.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-147">The portal notifies you when your data warehouse is ready to use.</span></span> 

## <a name="connect-to-sql-data-warehouse"></a><span data-ttu-id="dcf7b-148">Se connecter à SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="dcf7b-148">Connect to SQL Data Warehouse</span></span>

<span data-ttu-id="dcf7b-149">Pour les besoins de ce didacticiel, la connexion à l’entrepôt de données est effectuée via SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="dcf7b-149">This tutorial uses SQL Server Management Studio (SSMS) to connect to the data warehouse.</span></span> <span data-ttu-id="dcf7b-150">Vous pouvez vous connecter à SQL Data Warehouse par l’intermédiaire de ces connecteurs pris en charge : ADO.NET, JDBC, ODBC et PHP.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-150">You can connect to SQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="dcf7b-151">N’oubliez pas que les fonctionnalités peuvent être limitées si les outils ne sont pas pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="dcf7b-152">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="dcf7b-152">Get connection information</span></span>

<span data-ttu-id="dcf7b-153">Pour vous connecter à votre entrepôt de données, vous devez recourir au serveur SQL logique que vous avez créé dans [Composants requis].</span><span class="sxs-lookup"><span data-stu-id="dcf7b-153">To connect to your data warehouse, you need to connect through the logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="dcf7b-154">Sélectionnez votre entrepôt de données dans le tableau de bord ou recherchez-le dans vos ressources.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-154">Select your data warehouse from the dashboard or search for it in your resources.</span></span>

    ![Tableau de bord SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="dcf7b-156">Recherchez le nom complet du serveur SQL Server logique.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-156">Find the full name for the logical SQL server.</span></span>

    ![Sélection du nom du serveur](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="dcf7b-158">Ouvrez SSMS et utilisez l’Explorateur d’objets pour vous connecter à ce serveur en utilisant les informations d’identification d’administrateur du serveur que vous avez créées dans [Composants requis]</span><span class="sxs-lookup"><span data-stu-id="dcf7b-158">Open SSMS and use object explorer to connect to this server using the server admin credentials you created in [Prerequisites]</span></span>

    ![Connexion avec SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="dcf7b-160">Si tout se passe correctement, vous devez maintenant être connecté à votre serveur SQL Server logique.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-160">If all goes correctly, you should now be connected to your logical SQL server.</span></span> <span data-ttu-id="dcf7b-161">Étant donné que vous êtes connecté en tant qu’administrateur du serveur, vous pouvez vous connecter à n’importe quelle base de données hébergée par le serveur, y compris à la base de données MASTER.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-161">Since you logged in as the server admin, you can connect to any database hosted by the server, including the master database.</span></span> 

<span data-ttu-id="dcf7b-162">Il n’existe qu’un compte d’administrateur du serveur, qui dispose de la majorité des privilèges des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-162">There is only one server admin account and it has the most privileges of any user.</span></span> <span data-ttu-id="dcf7b-163">Veillez à ne pas autoriser un trop grand nombre de personnes de votre organisation à connaître le mot de passe d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-163">Be careful not to allow too many people in your organization to know the admin password.</span></span> 

<span data-ttu-id="dcf7b-164">Vous pouvez également posséder un compte d’administrateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="dcf7b-165">Nous ne fournissons pas les détails afférents ici.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-165">We don't provide the details here.</span></span> <span data-ttu-id="dcf7b-166">Pour en savoir plus sur l’utilisation de l’authentification Azure Active Directory, voir [Authentification Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="dcf7b-166">If you want to learn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="dcf7b-167">Nous étudions maintenant la création d’utilisateurs et d’information de connexion supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="dcf7b-168">Créer un utilisateur de base de données</span><span class="sxs-lookup"><span data-stu-id="dcf7b-168">Create a database user</span></span>

<span data-ttu-id="dcf7b-169">Dans cette étape, vous créez un compte d’utilisateur pour accéder à votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-169">In this step, you create a user account to access your data warehouse.</span></span> <span data-ttu-id="dcf7b-170">Nous vous montrons également comment autoriser cet utilisateur à exécuter des requêtes avec une grande quantité de mémoire et de ressources processeur.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-170">We also show you how to give that user the ability to run queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-to-queries"></a><span data-ttu-id="dcf7b-171">Remarques sur les classes de ressources pour allouer des ressources aux requêtes</span><span class="sxs-lookup"><span data-stu-id="dcf7b-171">Notes about resource classes for allocating resources to queries</span></span>

- <span data-ttu-id="dcf7b-172">Pour que vos données restent sécurisées, n’utilisez pas le compte d’administrateur du serveur pour exécuter des requêtes sur vos bases de données de production.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-172">To keep your data safe, don't use the server admin to run queries on your production databases.</span></span> <span data-ttu-id="dcf7b-173">Il possède la majorité des privilèges des utilisateurs, et l’utiliser pour effectuer des opérations sur les données utilisateur expose vos données à des risques.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-173">It has the most privileges of any user and using it to perform operations on user data puts your data at risk.</span></span> <span data-ttu-id="dcf7b-174">En outre, comme l’administrateur du serveur est censé effectuer des opérations de gestion, il exécute des opérations avec uniquement une petite allocation de mémoire et de ressources processeur.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-174">Also, since the server admin is meant to perform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="dcf7b-175">SQL Data Warehouse utilise les rôles de base de données prédéfinis, appelés classes de ressources, pour allouer différentes quantités de mémoire, de ressources processeur et d’emplacements de concurrence aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, to allocate different amounts of memory, CPU resources, and concurrency slots to users.</span></span> <span data-ttu-id="dcf7b-176">Chaque utilisateur peut appartenir à une classe de ressources petite, moyenne, grande ou très grande.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-176">Each user can belong to a small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="dcf7b-177">La classe de ressources de l’utilisateur détermine les ressources dont l’utilisateur dispose pour exécuter des requêtes et des opérations de chargement.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-177">The user's resource class determines the resources the user has to run queries and load operations.</span></span>

- <span data-ttu-id="dcf7b-178">Pour optimiser la compression des données, l’utilisateur devra parfois procéder à des chargements avec des allocations de ressources de grande ou de très grande taille.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-178">For optimal data compression, the user may need to load with large or extra large resource allocations.</span></span> <span data-ttu-id="dcf7b-179">Découvrez plus d’informations sur les classes de ressource [ici](./sql-data-warehouse-develop-concurrency.md#resource-classes) :</span><span class="sxs-lookup"><span data-stu-id="dcf7b-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="dcf7b-180">Créer un compte pouvant contrôler une base de données</span><span class="sxs-lookup"><span data-stu-id="dcf7b-180">Create an account that can control a database</span></span>

<span data-ttu-id="dcf7b-181">Comme vous êtes actuellement connecté en tant qu’administrateur du serveur, vous êtes autorisé à créer des connexions et des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-181">Since you are currently logged in as the server admin you have permissions to create logins and users.</span></span>

1. <span data-ttu-id="dcf7b-182">À l’aide de SSMS ou d’un autre client de requête, ouvrez une nouvelle requête pour **master**.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Nouvelle requête sur Master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nouvelle requête sur Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="dcf7b-185">Dans la fenêtre de requête, exécutez cette commande T-SQL pour créer une connexion nommée MedRCLogin et un utilisateur nommé LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-185">In the query window, run this T-SQL command to create a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="dcf7b-186">Cette connexion peut atteindre un serveur SQL Server logique.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-186">This login can connect to the logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="dcf7b-187">En interrogeant la *base de données SQL Data Warehouse*, créez un utilisateur de base de données en fonction de la connexion que vous avez créée pour accéder à la base de données et y effectuer des opérations.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-187">Now querying the *SQL Data Warehouse database*, create a database user based on the login you created to access and perform operations on the database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="dcf7b-188">Octroyez à l’utilisateur de base de données des autorisations de contrôle sur la base de données appelée NYT.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-188">Give the database user control permissions to the database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] to LoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="dcf7b-189">Si le nom de votre base de données comporte des traits d’union, veillez à le placer entre crochets.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-189">If your database name has hyphens in it, be sure to wrap it in brackets!</span></span> 
    >

### <a name="give-the-user-medium-resource-allocations"></a><span data-ttu-id="dcf7b-190">Accorder à l’utilisateur des allocations de ressources de taille moyenne</span><span class="sxs-lookup"><span data-stu-id="dcf7b-190">Give the user medium resource allocations</span></span>

1. <span data-ttu-id="dcf7b-191">Exécutez cette commande T-SQL pour qu’il devienne membre de la classe de ressources de taille moyenne, appelée mediumrc.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-191">Run this T-SQL command to make it a member of the medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="dcf7b-192">Cliquez [ici](sql-data-warehouse-develop-concurrency.md#resource-classes) pour en savoir plus sur les classes d’accès concurrentiel et de ressources.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) to learn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="dcf7b-193">Connectez-vous au serveur logique en utilisant les nouvelles informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-193">Connect to the logical server with the new credentials</span></span>

    ![Connexion avec le nouveau compte de connexion](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="dcf7b-195">Charger des données à partir d’objets Blob Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="dcf7b-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="dcf7b-196">Vous êtes maintenant prêt à charger des données dans votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-196">You are now ready to load data into your data warehouse.</span></span> <span data-ttu-id="dcf7b-197">Cette étape vous montre comment charger les données des taxis de New York à partir d’un stockage d’objets blob Azure public.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-197">This step shows you how to load New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="dcf7b-198">Pour charger des données dans SQL Data Warehouse, il est courant de commencer par les déplacer dans le stockage d’objets blob Azure, puis de les charger dans votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-198">A common way to load data into SQL Data Warehouse is to first move the data to Azure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="dcf7b-199">Pour faciliter la compréhension du chargement, nous avons fait en sorte que les données des taxis de New York soient déjà hébergées dans un stockage d’objets blob Azure public.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-199">To make it easier to understand how to load, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="dcf7b-200">Pour vous y référer ultérieurement, pour savoir comment charger vos données vers le stockage d’objets blob Azure ou pour les charger directement à partir de votre source dans SQL Data Warehouse, consultez la [présentation du chargement](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="dcf7b-200">For future reference, to learn how to get your data to Azure blob storage or to load it directly from your source into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="dcf7b-201">Définir des données externes</span><span class="sxs-lookup"><span data-stu-id="dcf7b-201">Define external data</span></span>

1. <span data-ttu-id="dcf7b-202">Créez une clé principale.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-202">Create a master key.</span></span> <span data-ttu-id="dcf7b-203">Vous ne devez créer qu’une clé principale par base de données.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-203">You only need to create a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="dcf7b-204">Définissez l’emplacement de l’objet blob Azure qui contient les données des taxis.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-204">Define the location of the Azure blob that contains the taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="dcf7b-205">Définissez les formats des fichiers externes.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-205">Define the external file formats</span></span>

    <span data-ttu-id="dcf7b-206">La commande ```CREATE EXTERNAL FILE FORMAT``` permet de spécifier le format des fichiers qui contiennent les données externes.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-206">The ```CREATE EXTERNAL FILE FORMAT``` command is used to specify the format of files that contain the external data.</span></span> <span data-ttu-id="dcf7b-207">Ils contiennent du texte séparé par un ou plusieurs caractères, appelés délimiteurs.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="dcf7b-208">Pour les besoins de démonstration, les données des taxis sont stockées sous forme de données non compressées et de données compressées au format gzip.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-208">For demonstration purposes, the taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="dcf7b-209">Exécutez ces commandes T-SQL pour définir les deux formats : non compressé et compressé.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-209">Run these T-SQL commands to define two different formats: uncompressed and compressed.</span></span>

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

4.  <span data-ttu-id="dcf7b-210">Créez un schéma pour le format de fichier externe.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="dcf7b-211">Créez les tables externes.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-211">Create the external tables.</span></span> <span data-ttu-id="dcf7b-212">Ces tables référencent les données stockées dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="dcf7b-213">Exécutez les commandes T-SQL suivantes pour créer plusieurs tables externes pointant toutes vers l’objet blob Azure que nous avons défini précédemment dans notre source de données externe.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-213">Run the following T-SQL commands to create several external tables that all point to the Azure blob we defined previously in our external data source.</span></span>

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

### <a name="import-the-data-from-azure-blob-storage"></a><span data-ttu-id="dcf7b-214">Importez les données à partir du stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-214">Import the data from Azure blob storage.</span></span>

<span data-ttu-id="dcf7b-215">SQL Data Warehouse prend en charge une instruction clé appelée CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="dcf7b-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="dcf7b-216">Cette instruction crée une table en fonction des résultats d’une instruction select.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-216">This statement creates a new table based on the results of a select statement.</span></span> <span data-ttu-id="dcf7b-217">La nouvelle table propose les mêmes colonnes et les mêmes types de données que les résultats de l’instruction select.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-217">The new table has the same columns and data types as the results of the select statement.</span></span>  <span data-ttu-id="dcf7b-218">Il s’agit d’un excellent moyen pour importer des données du stockage Blob Azure dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-218">This is an elegant way to import data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="dcf7b-219">Exécutez ce script pour importer vos données.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-219">Run this script to import your data.</span></span>

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

2. <span data-ttu-id="dcf7b-220">Affichez vos données à mesure qu’elles sont chargées.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-220">View your data as it loads.</span></span>

   <span data-ttu-id="dcf7b-221">Vous chargez plusieurs gigaoctets de données et les compressez au sein d’index de cluster columnstore hautes performances.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="dcf7b-222">Exécutez la requête suivante qui fait appel à des vues de gestion dynamique pour afficher l’état de la charge.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-222">Run the following query that uses a dynamic management views (DMVs) to show the status of the load.</span></span> <span data-ttu-id="dcf7b-223">Une fois la requête démarrée, prenez un café et quelque chose à grignoter pendant que SQL Data Warehouse fait le gros du travail.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-223">After starting the query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
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

3. <span data-ttu-id="dcf7b-224">Affichez toutes les requêtes du système.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="dcf7b-225">Vous pouvez constater que vos données sont efficacement chargées dans votre entrepôt Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Affichage des données chargées](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="dcf7b-227">Améliorer les performances des requêtes</span><span class="sxs-lookup"><span data-stu-id="dcf7b-227">Improve query performance</span></span>

<span data-ttu-id="dcf7b-228">Il existe plusieurs façons d’améliorer les performances des requêtes et d’obtenir les performances haute vitesse que SQL Data Warehouse est conçu pour fournir.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-228">There are several ways to improve query performance and to achieve the high-speed performance that SQL Data Warehouse is designed to provide.</span></span>  

### <a name="see-the-effect-of-scaling-on-query-performance"></a><span data-ttu-id="dcf7b-229">Observer l’impact de la mise à l’échelle sur les performances des requêtes</span><span class="sxs-lookup"><span data-stu-id="dcf7b-229">See the effect of scaling on query performance</span></span> 

<span data-ttu-id="dcf7b-230">Pour améliorer les performances des requêtes, vous pouvez mettre à l’échelle des ressources en modifiant le niveau de service DWU de votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-230">One way to improve query performance is to scale resources by changing the DWU service level for your data warehouse.</span></span> <span data-ttu-id="dcf7b-231">Chaque niveau de service est plus onéreux, mais vous pouvez réduire la taille des ressources ou les mettre en pause à tout moment.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="dcf7b-232">Lors de cette étape, vous comparez les performances de deux paramètres DWU différents.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="dcf7b-233">Commençons par réduire la taille à 100 DWU, afin de déterminer de manière générale l’efficacité d’un nœud de calcul pris séparément.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-233">First, let's scale the sizing down to 100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="dcf7b-234">Accédez au portail et sélectionnez votre SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-234">Go to the portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="dcf7b-235">Sélectionnez l’échelle dans le panneau SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-235">Select scale in the SQL Data Warehouse blade.</span></span> 

    ![Mise à l’échelle de l’instance SQL Data Warehouse dans le portail](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="dcf7b-237">Effectuez la descente en puissance de la barre de performance jusqu’à atteindre 100 DWU, puis cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-237">Scale down the performance bar to 100 DWU and hit save.</span></span>

    ![Mise à l’échelle et enregistrement](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="dcf7b-239">Attendez que l’opération de mise à l’échelle se termine.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-239">Wait for your scale operation to finish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dcf7b-240">Les requêtes ne peuvent pas être exécutées lors de la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-240">Queries cannot run while changing the scale.</span></span> <span data-ttu-id="dcf7b-241">La mise à l’échelle **supprime** vos requêtes en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="dcf7b-242">Vous pouvez les redémarrer une fois l’opération terminée.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-242">You can restart them when the operation is finished.</span></span>
    >
    
5. <span data-ttu-id="dcf7b-243">Lancez une opération d’analyse sur les données de voyage, en sélectionnant le premier million d’entrées pour toutes les colonnes.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-243">Do a scan operation on the trip data, selecting the top million entries for all the columns.</span></span> <span data-ttu-id="dcf7b-244">Si vous souhaitez avancer rapidement, sélectionnez moins de lignes.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-244">If you're eager to move on quickly, feel free to select fewer rows.</span></span> <span data-ttu-id="dcf7b-245">Prenez note de la durée d’exécution de cette opération.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-245">Take note of the time it takes to run this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="dcf7b-246">Redéfinissez la taille de votre entrepôt de données sur 400 DWU.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-246">Scale your data warehouse back to 400 DWU.</span></span> <span data-ttu-id="dcf7b-247">Rappelez-vous que chaque tranche de 100 DWU entraîne l’ajout d’un autre nœud de calcul dans votre instance Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-247">Remember, each 100 DWU is adding another compute node to your Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="dcf7b-248">Exécutez la requête à nouveau.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-248">Run the query again!</span></span> <span data-ttu-id="dcf7b-249">Vous devriez remarquer une différence importante.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="dcf7b-250">Étant donné que la requête retourne une grande quantité de données, la disponibilité de la bande passante pour l’ordinateur exécutant SSMS peut être un goulot d’étranglement.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-250">Because the query returns a lot of data, the bandwidth availability of the machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="dcf7b-251">Cela peut vous empêcher de noter des améliorations des performances !</span><span class="sxs-lookup"><span data-stu-id="dcf7b-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="dcf7b-252">Étant donné que SQL Data Warehouse utilise le traitement massivement parallèle,</span><span class="sxs-lookup"><span data-stu-id="dcf7b-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="dcf7b-253">les requêtes qui effectuent des opérations d’analyse ou exécutent des fonctions analytiques sur des millions de lignes profitent de la véritable puissance d’Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-253">Queries that scan or perform analytic functions on millions of rows experience the true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-the-effect-of-statistics-on-query-performance"></a><span data-ttu-id="dcf7b-254">Observer l’impact des statistiques sur les performances des requêtes</span><span class="sxs-lookup"><span data-stu-id="dcf7b-254">See the effect of statistics on query performance</span></span>

1. <span data-ttu-id="dcf7b-255">Exécutez une requête joignant la table des dates avec celles des voyages.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-255">Run a query that joins the Date table with the Trip table</span></span>

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

    <span data-ttu-id="dcf7b-256">L’exécution de cette requête prend un certain temps, car SQL Data Warehouse doit réorganiser les données avant de procéder à la jonction.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-256">This query takes a while because SQL Data Warehouse has to shuffle data before it can perform the join.</span></span> <span data-ttu-id="dcf7b-257">Les jonctions n’ont pas besoin de réorganiser les données si elles visent à joindre les données de la même façon que celle dont elles ont été distribuées.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-257">Joins do not have to shuffle data if they are designed to join data in the same way it is distributed.</span></span> <span data-ttu-id="dcf7b-258">Il s’agit d’un thème plus spécifique.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="dcf7b-259">Les statistiques font la différence.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="dcf7b-260">Exécutez cette instruction pour créer des statistiques sur les colonnes de la jonction.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-260">Run this statement to create statistics on the join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="dcf7b-261">Azure SQL Data Warehouse ne gère pas automatiquement les statistiques pour vous.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="dcf7b-262">Or, ces statistiques sont importantes pour déterminer les performances des requêtes. Il est donc fortement recommandé de créer et de mettre à jour les statistiques.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="dcf7b-263">**Vous bénéficiez de performances optimales en lançant des statistiques sur les colonnes impliquées dans les jointures, celles utilisées dans la clause WHERE et celles figurant dans GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="dcf7b-263">**You gain the most benefit by having statistics on columns involved in joins, columns used in the WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="dcf7b-264">Exécutez à nouveau la requête depuis Composants requis et notez les différences en termes de performances.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-264">Run the query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="dcf7b-265">Certes, elles ne sont pas aussi visibles que dans le cas de la montée en puissance, mais vous devriez remarquer une accélération.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-265">While the differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dcf7b-266">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dcf7b-266">Next steps</span></span>

<span data-ttu-id="dcf7b-267">Vous êtes maintenant prêt à lancer des requêtes et explorer les résultats.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-267">You're now ready to query and explore.</span></span> <span data-ttu-id="dcf7b-268">Découvrez nos meilleures pratiques et nos conseils !</span><span class="sxs-lookup"><span data-stu-id="dcf7b-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="dcf7b-269">Si vous avez terminé votre exploration, n’oubliez pas d’interrompre votre instance.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-269">If you're done exploring for the day, make sure to pause your instance!</span></span> <span data-ttu-id="dcf7b-270">Dans un environnement de production, vous pouvez réaliser des économies importantes en interrompant vos requêtes et en les mettant à l’échelle en fonction de vos besoins métier.</span><span class="sxs-lookup"><span data-stu-id="dcf7b-270">In production, you can experience enormous savings by pausing and scaling to meet your business needs.</span></span>

![Suspendre](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="dcf7b-272">Documents utiles</span><span class="sxs-lookup"><span data-stu-id="dcf7b-272">Useful readings</span></span>

<span data-ttu-id="dcf7b-273">[Gestion de la concurrence et des charges de travail][]</span><span class="sxs-lookup"><span data-stu-id="dcf7b-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="dcf7b-274">[Meilleures pratiques pour Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="dcf7b-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="dcf7b-275">[surveillance des requêtes][]</span><span class="sxs-lookup"><span data-stu-id="dcf7b-275">[Query Monitoring][]</span></span>

<span data-ttu-id="dcf7b-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][] (10 meilleures pratiques pour la création d’un entrepôt de données relationnelles à grande échelle)</span><span class="sxs-lookup"><span data-stu-id="dcf7b-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="dcf7b-277">[Migrating Data to Azure SQL Data Warehouse][] (Migration de données vers Microsoft Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="dcf7b-277">[Migrating Data to Azure SQL Data Warehouse][]</span></span>

[Gestion de la concurrence et des charges de travail]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Meilleures pratiques pour Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[surveillance des requêtes]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/ (10 meilleures pratiques pour la création d’un entrepôt de données relationnelles à grande échelle)
[Migrating Data to Azure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/ (Migration de données vers Microsoft Azure SQL Data Warehouse)



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[Composants requis]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
