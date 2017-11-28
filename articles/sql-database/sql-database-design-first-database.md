---
title: "aaaDesign votre première base de données SQL Azure | Documents Microsoft"
description: "En savoir plus toodesign votre première base de données SQL Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a><span data-ttu-id="8e88a-103">Concevoir votre première base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8e88a-103">Design your first Azure SQL database</span></span>

<span data-ttu-id="8e88a-104">Base de données SQL Azure est un relationnel de base de données comme un service (DBaaS) Bonjour Microsoft Cloud (« Azure »).</span><span class="sxs-lookup"><span data-stu-id="8e88a-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="8e88a-105">Dans ce didacticiel, vous apprendrez comment toouse hello portail Azure et [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) pour :</span><span class="sxs-lookup"><span data-stu-id="8e88a-105">In this tutorial, you learn how toouse hello Azure portal and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="8e88a-106">Créer une base de données Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="8e88a-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="8e88a-107">Définir une règle de pare-feu de niveau serveur Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="8e88a-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="8e88a-108">Connexion de base de données toohello avec SSMS</span><span class="sxs-lookup"><span data-stu-id="8e88a-108">Connect toohello database with SSMS</span></span>
> * <span data-ttu-id="8e88a-109">Créer des tables avec SSMS</span><span class="sxs-lookup"><span data-stu-id="8e88a-109">Create tables with SSMS</span></span>
> * <span data-ttu-id="8e88a-110">Charger en masse des données avec BCP</span><span class="sxs-lookup"><span data-stu-id="8e88a-110">Bulk load data with BCP</span></span>
> * <span data-ttu-id="8e88a-111">Interroger ces données avec SSMS</span><span class="sxs-lookup"><span data-stu-id="8e88a-111">Query that data with SSMS</span></span>
> * <span data-ttu-id="8e88a-112">Restaurer hello tooa de base de données précédente [point de restauration dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore) Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="8e88a-112">Restore hello database tooa previous [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) in hello Azure portal</span></span>

<span data-ttu-id="8e88a-113">Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="8e88a-113">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e88a-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8e88a-114">Prerequisites</span></span>

<span data-ttu-id="8e88a-115">toocomplete ce didacticiel, assurez-vous que vous avez installé :</span><span class="sxs-lookup"><span data-stu-id="8e88a-115">toocomplete this tutorial, make sure you have installed:</span></span>
- <span data-ttu-id="8e88a-116">version la plus récente de Hello [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="8e88a-116">hello newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span></span>
- <span data-ttu-id="8e88a-117">version la plus récente de Hello [BCP et SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span><span class="sxs-lookup"><span data-stu-id="8e88a-117">hello newest version of [BCP and SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="8e88a-118">Ouvrez une session dans toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8e88a-118">Log in toohello Azure portal</span></span>

<span data-ttu-id="8e88a-119">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8e88a-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="8e88a-120">Créer une base de données SQL vide</span><span class="sxs-lookup"><span data-stu-id="8e88a-120">Create a blank SQL database</span></span>

<span data-ttu-id="8e88a-121">Une base de données SQL Azure est créée avec un ensemble défini de [ressources de calcul et de stockage](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="8e88a-121">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="8e88a-122">base de données Hello est créé dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) et dans un [serveur logique de base de données SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="8e88a-122">hello database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="8e88a-123">Suivez ces étapes de toocreate une base de données SQL vide.</span><span class="sxs-lookup"><span data-stu-id="8e88a-123">Follow these steps toocreate a blank SQL database.</span></span> 

1. <span data-ttu-id="8e88a-124">Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8e88a-124">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="8e88a-125">Sélectionnez **bases de données** de hello **nouveau** page, puis sélectionnez **base de données SQL** de hello **bases de données** page.</span><span class="sxs-lookup"><span data-stu-id="8e88a-125">Select **Databases** from hello **New** page, and select **SQL Database** from hello **Databases** page.</span></span> 

   ![créer une base de données vide](./media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="8e88a-127">Rempliront hello de base de données SQL avec hello suivant d’informations, comme indiqué dans le hello précédant l’image :</span><span class="sxs-lookup"><span data-stu-id="8e88a-127">Fill out hello SQL Database form with hello following information, as shown on hello preceding image:</span></span>   

   | <span data-ttu-id="8e88a-128">Paramètre</span><span class="sxs-lookup"><span data-stu-id="8e88a-128">Setting</span></span>       | <span data-ttu-id="8e88a-129">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="8e88a-129">Suggested value</span></span> | <span data-ttu-id="8e88a-130">Description</span><span class="sxs-lookup"><span data-stu-id="8e88a-130">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="8e88a-131">**Nom de la base de données**</span><span class="sxs-lookup"><span data-stu-id="8e88a-131">**Database name**</span></span> | <span data-ttu-id="8e88a-132">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="8e88a-132">mySampleDatabase</span></span> | <span data-ttu-id="8e88a-133">Pour les noms de base de données valides, consultez [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données).</span><span class="sxs-lookup"><span data-stu-id="8e88a-133">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="8e88a-134">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="8e88a-134">**Subscription**</span></span> | <span data-ttu-id="8e88a-135">Votre abonnement</span><span class="sxs-lookup"><span data-stu-id="8e88a-135">Your subscription</span></span>  | <span data-ttu-id="8e88a-136">Pour plus d’informations sur vos abonnements, consultez [Abonnements](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="8e88a-136">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="8e88a-137">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="8e88a-137">**Resource group**</span></span> | <span data-ttu-id="8e88a-138">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8e88a-138">myResourceGroup</span></span> | <span data-ttu-id="8e88a-139">Pour les noms de groupe de ressources valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom).</span><span class="sxs-lookup"><span data-stu-id="8e88a-139">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="8e88a-140">**Sélectionner une source**</span><span class="sxs-lookup"><span data-stu-id="8e88a-140">**Select source**</span></span> | <span data-ttu-id="8e88a-141">Base de données vide</span><span class="sxs-lookup"><span data-stu-id="8e88a-141">Blank database</span></span> | <span data-ttu-id="8e88a-142">Indique qu’une base de données vide doit être créée.</span><span class="sxs-lookup"><span data-stu-id="8e88a-142">Specifies that a blank database should be created.</span></span> |

4. <span data-ttu-id="8e88a-143">Cliquez sur **Server** toocreate et configurer un nouveau serveur pour votre nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="8e88a-143">Click **Server** toocreate and configure a new server for your new database.</span></span> <span data-ttu-id="8e88a-144">Remplir hello **nouveau formulaire serveur** avec hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e88a-144">Fill out hello **New server form** with hello following information:</span></span> 

   | <span data-ttu-id="8e88a-145">Paramètre</span><span class="sxs-lookup"><span data-stu-id="8e88a-145">Setting</span></span>       | <span data-ttu-id="8e88a-146">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="8e88a-146">Suggested value</span></span> | <span data-ttu-id="8e88a-147">Description</span><span class="sxs-lookup"><span data-stu-id="8e88a-147">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="8e88a-148">**Nom du serveur**</span><span class="sxs-lookup"><span data-stu-id="8e88a-148">**Server name**</span></span> | <span data-ttu-id="8e88a-149">Nom globalement unique</span><span class="sxs-lookup"><span data-stu-id="8e88a-149">Any globally unique name</span></span> | <span data-ttu-id="8e88a-150">Pour les noms de serveur valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom).</span><span class="sxs-lookup"><span data-stu-id="8e88a-150">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="8e88a-151">**Connexion d’administrateur du serveur**</span><span class="sxs-lookup"><span data-stu-id="8e88a-151">**Server admin login**</span></span> | <span data-ttu-id="8e88a-152">Nom valide</span><span class="sxs-lookup"><span data-stu-id="8e88a-152">Any valid name</span></span> | <span data-ttu-id="8e88a-153">Pour les noms de connexion valides, consultez [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données).</span><span class="sxs-lookup"><span data-stu-id="8e88a-153">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span>|
   | <span data-ttu-id="8e88a-154">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="8e88a-154">**Password**</span></span> | <span data-ttu-id="8e88a-155">Mot de passe valide</span><span class="sxs-lookup"><span data-stu-id="8e88a-155">Any valid password</span></span> | <span data-ttu-id="8e88a-156">Votre mot de passe doit comporter au moins 8 caractères et contenir des caractères appartenant à trois des hello suivant catégories : les caractères majuscules, caractères en minuscules, des chiffres et des caractères non alphanumériques.</span><span class="sxs-lookup"><span data-stu-id="8e88a-156">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="8e88a-157">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="8e88a-157">**Location**</span></span> | <span data-ttu-id="8e88a-158">Emplacement valide</span><span class="sxs-lookup"><span data-stu-id="8e88a-158">Any valid location</span></span> | <span data-ttu-id="8e88a-159">Pour plus d’informations sur les régions, consultez [Régions Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="8e88a-159">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![create database-server](./media//sql-database-design-first-database/create-database-server.png)

5. <span data-ttu-id="8e88a-161">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="8e88a-161">Click **Select**.</span></span>

6. <span data-ttu-id="8e88a-162">Cliquez sur **niveau tarifaire** toospecify hello performances et la couche de niveau de service pour votre nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="8e88a-162">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="8e88a-163">Pour ce didacticiel, sélectionnez **20 DTU** et **250** Go de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e88a-163">For this tutorial, select **20 DTUs** and **250** GB of storage.</span></span>

   ![create database-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. <span data-ttu-id="8e88a-165">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8e88a-165">Click **Apply**.</span></span>  

8. <span data-ttu-id="8e88a-166">Sélectionnez un **classement** pour la base de données vide hello (pour ce didacticiel, utiliser la valeur par défaut hello).</span><span class="sxs-lookup"><span data-stu-id="8e88a-166">Select a **collation** for hello blank database (for this tutorial, use hello default value).</span></span> <span data-ttu-id="8e88a-167">Pour en savoir plus sur les classements, voir [Classements](https://docs.microsoft.com/sql/t-sql/statements/collations)</span><span class="sxs-lookup"><span data-stu-id="8e88a-167">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span></span>

9. <span data-ttu-id="8e88a-168">Cliquez sur **créer** base de données tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-168">Click **Create** tooprovision hello database.</span></span> <span data-ttu-id="8e88a-169">Approvisionnement prend sur un toocomplete une minute et demie.</span><span class="sxs-lookup"><span data-stu-id="8e88a-169">Provisioning takes about a minute and a half toocomplete.</span></span> 

10. <span data-ttu-id="8e88a-170">Dans la barre d’outils de hello, cliquez sur **Notifications** processus de déploiement toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-170">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>

   ![notification](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="8e88a-172">créer une règle de pare-feu au niveau du serveur ;</span><span class="sxs-lookup"><span data-stu-id="8e88a-172">Create a server-level firewall rule</span></span>

<span data-ttu-id="8e88a-173">Hello service de base de données SQL crée un pare-feu à hello au niveau du serveur qui empêche des applications externes et des outils de se connecter toohello server ou des bases de données sur le serveur de hello, sauf si une règle de pare-feu est créée le pare-feu tooopen hello pour des adresses IP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="8e88a-173">hello SQL Database service creates a firewall at hello server-level that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="8e88a-174">Suivez ces étapes toocreate un [règle de pare-feu de niveau serveur de base de données SQL](sql-database-firewall-configure.md) pour l’adressage IP de votre client et activer la connectivité externe via le pare-feu de base de données SQL hello pour votre adresse IP uniquement.</span><span class="sxs-lookup"><span data-stu-id="8e88a-174">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through hello SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="8e88a-175">SQL Database communique par le biais du port 1433.</span><span class="sxs-lookup"><span data-stu-id="8e88a-175">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="8e88a-176">Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="8e88a-176">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="8e88a-177">Dans ce cas, serveur de base de données SQL Azure tooyour ne peut pas se connecter à moins que votre service informatique s’ouvre le port 1433.</span><span class="sxs-lookup"><span data-stu-id="8e88a-177">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="8e88a-178">Une fois le déploiement de hello terminé, cliquez sur **bases de données SQL** de menu à gauche hello, puis cliquez sur **mySampleDatabase** sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="8e88a-178">After hello deployment completes, click **SQL databases** from hello left-hand menu and then click **mySampleDatabase** on hello **SQL databases** page.</span></span> <span data-ttu-id="8e88a-179">nom de serveur complet Hello page Vue d’ensemble de votre base de données ouvre, affichant vous hello entièrement (tel que **mynewserver20170313.database.windows.net**) et fournit des options de configuration supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="8e88a-179">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="8e88a-180">Copiez ce nom de serveur complet pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8e88a-180">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="8e88a-181">Vous avez besoin de ce serveur complet nom tooconnect tooyour ses bases de données et dans les Démarrages rapides suivants.</span><span class="sxs-lookup"><span data-stu-id="8e88a-181">You need this fully qualified server name tooconnect tooyour server and its databases in subsequent quick starts.</span></span>
   > 

   ![nom du serveur](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="8e88a-183">Cliquez sur **définir serveur pare-feu** barre d’outils hello comme indiqué dans l’image précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-183">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="8e88a-184">Hello **des paramètres de pare-feu** page serveur de base de données SQL hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="8e88a-184">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

   ![règle de pare-feu de serveur](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. <span data-ttu-id="8e88a-186">Cliquez sur **ajouter l’adresse IP du client** sur tooadd de barre d’outils hello votre adresse IP actuelle d’adresses tooa nouvelle règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="8e88a-186">Click **Add client IP** on hello toolbar tooadd your current IP address tooa new firewall rule.</span></span> <span data-ttu-id="8e88a-187">Une règle de pare-feu peut ouvrir le port 1433 pour une seule adresse IP ou une plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="8e88a-187">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="8e88a-188">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8e88a-188">Click **Save**.</span></span> <span data-ttu-id="8e88a-189">Une règle de pare-feu de niveau serveur est créée pour votre adresse IP actuelle, ouvrir le port 1433 sur le serveur logique de hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-189">A server-level firewall rule is created for your current IP address opening port 1433 on hello logical server.</span></span>

   ![définir la règle de pare-feu de serveur](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="8e88a-191">Cliquez sur **OK** , puis fermez hello **des paramètres de pare-feu** page.</span><span class="sxs-lookup"><span data-stu-id="8e88a-191">Click **OK** and then close hello **Firewall settings** page.</span></span>

<span data-ttu-id="8e88a-192">Vous pouvez désormais connecter le serveur de base de données SQL toohello et ses bases de données à l’aide de SQL Server Management Studio ou un autre outil de votre choix à partir de cette adresse IP à l’aide du compte d’administrateur de serveur hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8e88a-192">You can now connect toohello SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e88a-193">Par défaut, l’accès via le pare-feu de base de données SQL hello est activé pour tous les services Azure.</span><span class="sxs-lookup"><span data-stu-id="8e88a-193">By default, access through hello SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="8e88a-194">Cliquez sur **OFF** sur toodisable de cette page pour tous les services Azure.</span><span class="sxs-lookup"><span data-stu-id="8e88a-194">Click **OFF** on this page toodisable for all Azure services.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="8e88a-195">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="8e88a-195">SQL server connection information</span></span>

<span data-ttu-id="8e88a-196">Obtenir le nom du serveur complet hello pour votre serveur de base de données SQL Azure Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8e88a-196">Get hello fully qualified server name for your Azure SQL Database server in hello Azure portal.</span></span> <span data-ttu-id="8e88a-197">Vous utilisez hello complet nom tooconnect tooyour serveur à l’aide de SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="8e88a-197">You use hello fully qualified server name tooconnect tooyour server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="8e88a-198">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8e88a-198">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8e88a-199">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="8e88a-199">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="8e88a-200">Bonjour **Essentials** volet Bonjour page du portail Azure pour votre base de données, recherchez et copiez hello **nom du serveur**.</span><span class="sxs-lookup"><span data-stu-id="8e88a-200">In hello **Essentials** pane in hello Azure portal page for your database, locate and then copy hello **Server name**.</span></span>

   ![informations de connexion](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="8e88a-202">Connexion de base de données toohello avec SSMS</span><span class="sxs-lookup"><span data-stu-id="8e88a-202">Connect toohello database with SSMS</span></span>

<span data-ttu-id="8e88a-203">Utilisez [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish un serveur de base de données SQL Azure de tooyour de connexion.</span><span class="sxs-lookup"><span data-stu-id="8e88a-203">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish a connection tooyour Azure SQL Database server.</span></span>

1. <span data-ttu-id="8e88a-204">Ouvrez SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="8e88a-204">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="8e88a-205">Bonjour **connecter tooServer** boîte de dialogue, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e88a-205">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="8e88a-206">Paramètre</span><span class="sxs-lookup"><span data-stu-id="8e88a-206">Setting</span></span>       | <span data-ttu-id="8e88a-207">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="8e88a-207">Suggested value</span></span> | <span data-ttu-id="8e88a-208">Description</span><span class="sxs-lookup"><span data-stu-id="8e88a-208">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="8e88a-209">Type de serveur</span><span class="sxs-lookup"><span data-stu-id="8e88a-209">Server type</span></span> | <span data-ttu-id="8e88a-210">Moteur de base de données</span><span class="sxs-lookup"><span data-stu-id="8e88a-210">Database engine</span></span> | <span data-ttu-id="8e88a-211">Cette valeur est obligatoire</span><span class="sxs-lookup"><span data-stu-id="8e88a-211">This value is required</span></span> |
   | <span data-ttu-id="8e88a-212">Nom du serveur</span><span class="sxs-lookup"><span data-stu-id="8e88a-212">Server name</span></span> | <span data-ttu-id="8e88a-213">nom du serveur complet Hello</span><span class="sxs-lookup"><span data-stu-id="8e88a-213">hello fully qualified server name</span></span> | <span data-ttu-id="8e88a-214">Hello nom doit être semblable à celui-ci : **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="8e88a-214">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="8e88a-215">Authentification</span><span class="sxs-lookup"><span data-stu-id="8e88a-215">Authentication</span></span> | <span data-ttu-id="8e88a-216">l’authentification SQL Server</span><span class="sxs-lookup"><span data-stu-id="8e88a-216">SQL Server Authentication</span></span> | <span data-ttu-id="8e88a-217">L’authentification SQL est hello seul type d’authentification que nous avons configuré dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8e88a-217">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="8e88a-218">Connexion</span><span class="sxs-lookup"><span data-stu-id="8e88a-218">Login</span></span> | <span data-ttu-id="8e88a-219">compte d’administrateur serveur Hello</span><span class="sxs-lookup"><span data-stu-id="8e88a-219">hello server admin account</span></span> | <span data-ttu-id="8e88a-220">Il s’agit de compte hello que vous avez spécifié lors de la création du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-220">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="8e88a-221">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="8e88a-221">Password</span></span> | <span data-ttu-id="8e88a-222">mot de passe Hello pour votre compte d’administrateur de serveur</span><span class="sxs-lookup"><span data-stu-id="8e88a-222">hello password for your server admin account</span></span> | <span data-ttu-id="8e88a-223">Il s’agit d’un mot de passe hello que vous avez spécifié lors de la création du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-223">This is hello password that you specified when you created hello server.</span></span> |

   ![se connecter tooserver](./media/sql-database-connect-query-ssms/connect.png)

3. <span data-ttu-id="8e88a-225">Cliquez sur **Options** Bonjour **connecter tooserver** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8e88a-225">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="8e88a-226">Bonjour **connecter toodatabase** section, entrez **mySampleDatabase** tooconnect toothis base de données.</span><span class="sxs-lookup"><span data-stu-id="8e88a-226">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![se connecter toodb sur le serveur](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="8e88a-228">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="8e88a-228">Click **Connect**.</span></span> <span data-ttu-id="8e88a-229">Ouvre la fenêtre de l’Explorateur d’objets Hello dans SSMS.</span><span class="sxs-lookup"><span data-stu-id="8e88a-229">hello Object Explorer window opens in SSMS.</span></span> 

5. <span data-ttu-id="8e88a-230">Dans l’Explorateur d’objets, développez **bases de données** , puis **mySampleDatabase** tooview des objets de hello dans la base de données exemple hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-230">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

   ![objets de base de données](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="8e88a-232">Créer des tables dans la base de données hello</span><span class="sxs-lookup"><span data-stu-id="8e88a-232">Create tables in hello database</span></span> 

<span data-ttu-id="8e88a-233">Créez un schéma de base de données avec quatre tables qui modélisent un système de gestion des étudiants pour les universités à l’aide de [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference) :</span><span class="sxs-lookup"><span data-stu-id="8e88a-233">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span></span>

- <span data-ttu-id="8e88a-234">Personne</span><span class="sxs-lookup"><span data-stu-id="8e88a-234">Person</span></span>
- <span data-ttu-id="8e88a-235">Cours</span><span class="sxs-lookup"><span data-stu-id="8e88a-235">Course</span></span>
- <span data-ttu-id="8e88a-236">Étudiant</span><span class="sxs-lookup"><span data-stu-id="8e88a-236">Student</span></span>
- <span data-ttu-id="8e88a-237">Attribuez à ce modèle un système de gestion des étudiants pour les universités</span><span class="sxs-lookup"><span data-stu-id="8e88a-237">Credit that model a student management system for universities</span></span>

<span data-ttu-id="8e88a-238">Hello diagramme suivant montre comment ces tables sont associée tooeach autres.</span><span class="sxs-lookup"><span data-stu-id="8e88a-238">hello following diagram shows how these tables are related tooeach other.</span></span> <span data-ttu-id="8e88a-239">Certaines de ces tables référencent des colonnes d’autres tables.</span><span class="sxs-lookup"><span data-stu-id="8e88a-239">Some of these tables reference columns in other tables.</span></span> <span data-ttu-id="8e88a-240">Par exemple, table de Student hello référence hello **PersonId** colonne Hello **personne** table.</span><span class="sxs-lookup"><span data-stu-id="8e88a-240">For example, hello Student table references hello **PersonId** column of hello **Person** table.</span></span> <span data-ttu-id="8e88a-241">Étude hello diagramme toounderstand comment hello tables dans ce didacticiel sont associée tooone une autre.</span><span class="sxs-lookup"><span data-stu-id="8e88a-241">Study hello diagram toounderstand how hello tables in this tutorial are related tooone another.</span></span> <span data-ttu-id="8e88a-242">Pour des explications approfondies sur la façon de tables de base de données efficace toocreate, consultez [créer des tables de base de données efficace](https://msdn.microsoft.com/library/cc505842.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e88a-242">For an in-depth look at how toocreate effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span></span> <span data-ttu-id="8e88a-243">Pour plus d’informations sur le choix des types de données, consultez [Types de données](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="8e88a-243">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span></span>

> [!NOTE]
> <span data-ttu-id="8e88a-244">Vous pouvez également utiliser hello [Concepteur de tables dans SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate et concevoir vos tables.</span><span class="sxs-lookup"><span data-stu-id="8e88a-244">You can also use hello [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate and design your tables.</span></span> 

![Relations entre les tables](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. <span data-ttu-id="8e88a-246">Dans l’Explorateur d’objets, cliquez avec le bouton droit sur **mySampleDatabase**, puis cliquez sur **Nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="8e88a-246">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="8e88a-247">Une fenêtre de requête vide s’ouvre tooyour connecté de base de données.</span><span class="sxs-lookup"><span data-stu-id="8e88a-247">A blank query window opens that is connected tooyour database.</span></span>

2. <span data-ttu-id="8e88a-248">Dans la fenêtre de requête hello, exécutez hello requête toocreate quatre tables suivantes dans votre base de données :</span><span class="sxs-lookup"><span data-stu-id="8e88a-248">In hello query window, execute hello following query toocreate four tables in your database:</span></span> 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![créez des tables](./media/sql-database-design-first-database/create-tables.png)

3. <span data-ttu-id="8e88a-250">Développez le nœud de « tables » de hello dans les tables hello hello SQL Server Management Studio Object explorer toosee que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="8e88a-250">Expand hello 'tables' node in hello SQL Server Management Studio Object explorer toosee hello tables you created.</span></span>

   ![tables ssms-créées](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="8e88a-252">Charger des données dans les tables de hello</span><span class="sxs-lookup"><span data-stu-id="8e88a-252">Load data into hello tables</span></span>

1. <span data-ttu-id="8e88a-253">Créez un dossier appelé **SampleTableData** dans vos données d’exemple toostore dossier Téléchargements pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="8e88a-253">Create a folder called **SampleTableData** in your Downloads folder toostore sample data for your database.</span></span> 

2. <span data-ttu-id="8e88a-254">Suivant de hello avec le bouton des liens et les enregistrer dans hello **SampleTableData** dossier.</span><span class="sxs-lookup"><span data-stu-id="8e88a-254">Right-click hello following links and save them into hello **SampleTableData** folder.</span></span> 

   - [<span data-ttu-id="8e88a-255">SampleCourseData</span><span class="sxs-lookup"><span data-stu-id="8e88a-255">SampleCourseData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [<span data-ttu-id="8e88a-256">SamplePersonData</span><span class="sxs-lookup"><span data-stu-id="8e88a-256">SamplePersonData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [<span data-ttu-id="8e88a-257">SampleStudentData</span><span class="sxs-lookup"><span data-stu-id="8e88a-257">SampleStudentData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [<span data-ttu-id="8e88a-258">SampleCreditData</span><span class="sxs-lookup"><span data-stu-id="8e88a-258">SampleCreditData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. <span data-ttu-id="8e88a-259">Ouvrez une fenêtre d’invite de commandes et accédez toohello SampleTableData dossier.</span><span class="sxs-lookup"><span data-stu-id="8e88a-259">Open a command prompt window and navigate toohello SampleTableData folder.</span></span>

4. <span data-ttu-id="8e88a-260">Exécutez hello suivant des données d’exemple tooinsert commandes dans des tables hello en remplaçant les valeurs hello pour **nom_serveur**, **DatabaseName**, **nom d’utilisateur**et **Mot de passe** avec les valeurs hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="8e88a-260">Execute hello following commands tooinsert sample data into hello tables replacing hello values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with hello values for your environment.</span></span>
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

<span data-ttu-id="8e88a-261">Vous avez maintenant chargé des exemples de données dans des tables hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8e88a-261">You have now loaded sample data into hello tables you created earlier.</span></span>

## <a name="query-data"></a><span data-ttu-id="8e88a-262">Données de requête</span><span class="sxs-lookup"><span data-stu-id="8e88a-262">Query data</span></span>

<span data-ttu-id="8e88a-263">Exécutez hello suivant informations tooretrieve de requêtes à partir des tables de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-263">Execute hello following queries tooretrieve information from hello database tables.</span></span> <span data-ttu-id="8e88a-264">Consultez [l’écriture des requêtes SQL](https://technet.microsoft.com/library/bb264565.aspx) toolearn plus d’informations sur l’écriture de requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="8e88a-264">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) toolearn more about writing SQL queries.</span></span> <span data-ttu-id="8e88a-265">requête de première Hello joint toutes les quatre tables toofind tous les étudiants hello traités par ' Dominick ce protocole » qui ont un niveau supérieur à 75 % de sa classe.</span><span class="sxs-lookup"><span data-stu-id="8e88a-265">hello first query joins all four tables toofind all hello students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span></span> <span data-ttu-id="8e88a-266">requête de deuxième Hello joint les quatre tables et recherche tous les cours dans lequel 'Noe Coleman' a déjà inscrit.</span><span class="sxs-lookup"><span data-stu-id="8e88a-266">hello second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span></span>

1. <span data-ttu-id="8e88a-267">Dans une fenêtre de requête SQL Server Management Studio, exécutez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="8e88a-267">In a SQL Server Management Studio query window, execute hello following query:</span></span>

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. <span data-ttu-id="8e88a-268">Dans une fenêtre de requête SQL Server Management Studio, exécutez la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="8e88a-268">In a SQL Server Management Studio query window, execute following query:</span></span>

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="8e88a-269">Restaurer un état antérieur de tooa de base de données dans le temps</span><span class="sxs-lookup"><span data-stu-id="8e88a-269">Restore a database tooa previous point in time</span></span>

<span data-ttu-id="8e88a-270">Imaginez que vous avez supprimé une table par inadvertance.</span><span class="sxs-lookup"><span data-stu-id="8e88a-270">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="8e88a-271">Il s’agit de quelque chose que vous ne pouvez pas récupérer facilement.</span><span class="sxs-lookup"><span data-stu-id="8e88a-271">This is something you cannot easily recover from.</span></span> <span data-ttu-id="8e88a-272">Base de données SQL Azure vous permet de toogo tooany précédent point dans le temps dans hello dernière too35 jours et de restauration ce point dans le temps tooa nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="8e88a-272">Azure SQL Database allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new database.</span></span> <span data-ttu-id="8e88a-273">Vous pouvez utiliser cette base de données toorecover les données supprimées.</span><span class="sxs-lookup"><span data-stu-id="8e88a-273">You can you this database toorecover your deleted data.</span></span> <span data-ttu-id="8e88a-274">Hello suit point de restauration hello exemple de base de données tooa avant l’ajout de tables de hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-274">hello following steps restore hello sample database tooa point before hello tables were added.</span></span>

1. <span data-ttu-id="8e88a-275">Dans la page de base de données SQL hello pour votre base de données, cliquez sur **restaurer** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-275">On hello SQL Database page for your database, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="8e88a-276">Hello **restaurer** ouvrir la page.</span><span class="sxs-lookup"><span data-stu-id="8e88a-276">hello **Restore** page opens.</span></span>

   ![restauration](./media/sql-database-design-first-database/restore.png)

2. <span data-ttu-id="8e88a-278">Remplir hello **restaurer** formulaire avec les informations de hello requis :</span><span class="sxs-lookup"><span data-stu-id="8e88a-278">Fill out hello **Restore** form with hello required information:</span></span>
    * <span data-ttu-id="8e88a-279">Nom de la base de données : entrez un nom pour la base de données</span><span class="sxs-lookup"><span data-stu-id="8e88a-279">Database name: Provide a database name</span></span> 
    * <span data-ttu-id="8e88a-280">Point-à-temps : Hello Select **Point-à-temps** onglet sur le formulaire de restauration hello</span><span class="sxs-lookup"><span data-stu-id="8e88a-280">Point-in-time: Select hello **Point-in-time** tab on hello Restore form</span></span> 
    * <span data-ttu-id="8e88a-281">Point de restauration : sélectionnez une heure qui se produit avant la modification de la base de données hello</span><span class="sxs-lookup"><span data-stu-id="8e88a-281">Restore point: Select a time that occurs before hello database was changed</span></span>
    * <span data-ttu-id="8e88a-282">Serveur cible : Vous ne pouvez pas modifier cette valeur lors de la restauration d’une base de données</span><span class="sxs-lookup"><span data-stu-id="8e88a-282">Target server: You cannot change this value when restoring a database</span></span> 
    * <span data-ttu-id="8e88a-283">Pool de base de données élastique : sélectionnez **Aucun**</span><span class="sxs-lookup"><span data-stu-id="8e88a-283">Elastic database pool: Select **None**</span></span>  
    * <span data-ttu-id="8e88a-284">Niveau tarifaire : sélectionnez **20 DTU** et **250 Go** de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e88a-284">Pricing tier: Select **20 DTUs** and **250 GB** of storage.</span></span>

   ![point de restauration](./media/sql-database-design-first-database/restore-point.png)

3. <span data-ttu-id="8e88a-286">Cliquez sur **OK** toorestore hello de base de données trop[restaurer tooa point dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore) avant l’ajout de tables de hello.</span><span class="sxs-lookup"><span data-stu-id="8e88a-286">Click **OK** toorestore hello database too[restore tooa point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before hello tables were added.</span></span> <span data-ttu-id="8e88a-287">Restauration d’un point différent de tooa de base de données dans le temps crée une base de données en double dans hello même serveur que la base de données d’origine hello as of point hello dans le temps que vous spécifiez, tant qu’elle se trouve dans la période de rétention hello pour votre [niveau de service](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="8e88a-287">Restoring a database tooa different point in time creates a duplicate database in hello same server as hello original database as of hello point in time you specify, as long as it is within hello retention period for your [service tier](sql-database-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e88a-288">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e88a-288">Next Steps</span></span> 
<span data-ttu-id="8e88a-289">Dans ce didacticiel, vous avez appris les tâches de base de données telles que la création une base de données et les tables, charger et interroger des données et restaurer le point précédent du tooa hello de base de données dans le temps.</span><span class="sxs-lookup"><span data-stu-id="8e88a-289">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="8e88a-290">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e88a-290">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8e88a-291">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="8e88a-291">Create a database</span></span>
> * <span data-ttu-id="8e88a-292">Configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="8e88a-292">Set up a firewall rule</span></span>
> * <span data-ttu-id="8e88a-293">Se connecter à base de données toohello avec [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span><span class="sxs-lookup"><span data-stu-id="8e88a-293">Connect toohello database with [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span></span>
> * <span data-ttu-id="8e88a-294">créez des tables</span><span class="sxs-lookup"><span data-stu-id="8e88a-294">Create tables</span></span>
> * <span data-ttu-id="8e88a-295">Charger des données en bloc</span><span class="sxs-lookup"><span data-stu-id="8e88a-295">Bulk load data</span></span>
> * <span data-ttu-id="8e88a-296">Interroger ces données</span><span class="sxs-lookup"><span data-stu-id="8e88a-296">Query that data</span></span>
> * <span data-ttu-id="8e88a-297">Restaurer le point précédent du tooa hello de base de données dans le temps à l’aide de la base de données SQL [point de restauration dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore) fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="8e88a-297">Restore hello database tooa previous point in time using SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities</span></span>

<span data-ttu-id="8e88a-298">Avance toohello toolearn de didacticiel suivant sur la conception d’une base de données à l’aide de Visual Studio et c#.</span><span class="sxs-lookup"><span data-stu-id="8e88a-298">Advance toohello next tutorial toolearn about designing a database using Visual Studio and C#.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="8e88a-299">Concevoir une base de données SQL Azure et se connecter avec C# et ADO.NET</span><span class="sxs-lookup"><span data-stu-id="8e88a-299">Design an Azure SQL database and connect with C# and ADO.NET</span></span>](sql-database-design-first-database-csharp.md)
