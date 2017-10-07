---
title: "aaaSecure votre base de données SQL Azure | Documents Microsoft"
description: "En savoir plus sur les techniques et fonctionnalités toosecure votre base de données SQL Azure."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="c61ce-103">Sécuriser votre base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c61ce-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="c61ce-104">Base de données SQL protège vos données en limitant la base de données access tooyour à l’aide de règles de pare-feu, nécessitant des utilisateurs tooprove leur identité et autorisation toodata via les autorisations et les appartenances de rôle, ainsi que par le biais des mécanismes d’authentification sécurité de niveau ligne et masquage dynamique des données.</span><span class="sxs-lookup"><span data-stu-id="c61ce-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="c61ce-105">Vous pouvez améliorer la protection de hello de votre base de données contre les utilisateurs malveillants ou de tout accès non autorisé seulement quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="c61ce-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="c61ce-106">Ce didacticiel vous apprend à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c61ce-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c61ce-107">Configurer des règles de pare-feu de niveau serveur pour votre serveur Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="c61ce-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="c61ce-108">Créer des règles de pare-feu pour votre base de données à l’aide de SSMS</span><span class="sxs-lookup"><span data-stu-id="c61ce-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="c61ce-109">Se connecter à l’aide d’une chaîne de connexion sécurisée de la base de données tooyour</span><span class="sxs-lookup"><span data-stu-id="c61ce-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="c61ce-110">Gérer l’accès des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="c61ce-110">Manage user access</span></span>
> * <span data-ttu-id="c61ce-111">Protéger vos données à l’aide du chiffrement</span><span class="sxs-lookup"><span data-stu-id="c61ce-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="c61ce-112">Activer l’audit Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c61ce-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="c61ce-113">Activer la détection de menaces pour les bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="c61ce-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="c61ce-114">Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="c61ce-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c61ce-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c61ce-115">Prerequisites</span></span>

<span data-ttu-id="c61ce-116">toocomplete ce didacticiel, assurez-vous que vous avez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c61ce-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="c61ce-117">Version la plus récente installée hello de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="c61ce-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="c61ce-118">Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="c61ce-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="c61ce-119">Création d’un serveur SQL Azure et la base de données - voir [créer une base de données SQL Azure Bonjour Azure portal](sql-database-get-started-portal.md), [créer une seule base de données SQL Azure à l’aide de hello CLI d’Azure](sql-database-get-started-cli.md), et [Create a SQL Azure unique base de données à l’aide de PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c61ce-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="c61ce-120">Ouvrez une session dans toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c61ce-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="c61ce-121">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c61ce-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="c61ce-122">Créer une règle de pare-feu de niveau serveur dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c61ce-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="c61ce-123">Les bases de données SQL sont protégées par un pare-feu dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ce-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="c61ce-124">Par défaut, toutes les connexions toohello serveur hello bases de données et à l’intérieur du serveur de hello sont rejetées à l’exception des connexions à partir d’autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ce-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="c61ce-125">Pour plus d’informations, consultez [Règles de pare-feu au niveau du serveur et de la base de données d’Azure SQL Database](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c61ce-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="c61ce-126">une configuration plus sécurisée Hello est tooOFF de tooset « Autoriser l’accès tooAzure services ».</span><span class="sxs-lookup"><span data-stu-id="c61ce-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="c61ce-127">Si vous devez tooconnect toohello base de données à partir d’un service cloud ou machine virtuelle Azure, vous devez créer un [adresse IP réservée](../virtual-network/virtual-networks-reserved-public-ip.md) et autoriser uniquement hello réservé accès par adresse IP via le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="c61ce-128">Suivez ces étapes toocreate un [règle de pare-feu de niveau serveur de base de données SQL](sql-database-firewall-configure.md) pour vos connexions au serveur tooallow à partir d’une adresse IP spécifique.</span><span class="sxs-lookup"><span data-stu-id="c61ce-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="c61ce-129">Si vous avez créé une base de données d’exemple dans Azure à l’aide d’un des didacticiels précédents de hello ou Démarrages rapides et sont effectuer ce didacticiel sur un ordinateur avec hello même adresse IP qu’il avait lorsque vous passé en revue ces didacticiels, vous pouvez ignorer cette étape car vous devrez déjà créé une règle de pare-feu de niveau serveur.</span><span class="sxs-lookup"><span data-stu-id="c61ce-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="c61ce-130">Cliquez sur **bases de données SQL** de hello gauche menu et cliquez sur hello base de données vous souhaitez que la règle de pare-feu hello tooconfigure pour sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="c61ce-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="c61ce-131">nom de serveur complet Hello page Vue d’ensemble de votre base de données ouvre, affichant vous hello entièrement (tel que **mynewserver-20170313.database.windows.net**) et fournit des options de configuration supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="c61ce-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![règle de pare-feu de serveur](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="c61ce-133">Cliquez sur **définir serveur pare-feu** barre d’outils hello comme indiqué dans l’image précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="c61ce-134">Hello **des paramètres de pare-feu** page serveur de base de données SQL hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c61ce-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="c61ce-135">Cliquez sur **ajouter l’adresse IP du client** hello barre d’outils tooadd hello adresse IP publique du portail de toohello connecté hello ordinateur avec ou entrer manuellement les règles de pare-feu hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c61ce-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![définir la règle de pare-feu de serveur](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="c61ce-137">Cliquez sur **OK** puis cliquez sur hello **X** tooclose hello **des paramètres de pare-feu** page.</span><span class="sxs-lookup"><span data-stu-id="c61ce-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="c61ce-138">Vous pouvez maintenant vous connecter tooany de base de données de serveur de hello avec hello spécifié plage d’adresses IP ou adresse IP.</span><span class="sxs-lookup"><span data-stu-id="c61ce-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="c61ce-139">SQL Database communique par le biais du port 1433.</span><span class="sxs-lookup"><span data-stu-id="c61ce-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="c61ce-140">Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="c61ce-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="c61ce-141">Dans ce cas, vous ne serez pas de serveur de base de données SQL Azure en mesure de tooconnect tooyour, sauf si votre service informatique s’ouvre le port 1433.</span><span class="sxs-lookup"><span data-stu-id="c61ce-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="c61ce-142">Créer une règle de pare-feu au niveau de la base de données à l’aide de SSMS</span><span class="sxs-lookup"><span data-stu-id="c61ce-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="c61ce-143">Règles de pare-feu de niveau base de données vous activer les paramètres de pare-feu différent de toocreate pour différentes bases de données hello même pare-feu de serveur et toocreate logique les règles qui sont portables - c'est-à-dire qu’elles respectent les base de données hello pendant un [basculement ](sql-database-geo-replication-overview.md) plutôt que stockés sur le serveur SQL de hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="c61ce-144">Règles de pare-feu de niveau base de données ne peuvent être configuré à l’aide d’instructions Transact-SQL et uniquement après avoir configuré la première règle de pare-feu de niveau serveur hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="c61ce-145">Pour plus d’informations, consultez [Règles de pare-feu au niveau du serveur et de la base de données d’Azure SQL Database](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c61ce-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="c61ce-146">Suit ces toocreate suit une règle de pare-feu de base de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="c61ce-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="c61ce-147">Se connecter à une base de données tooyour, par exemple à l’aide de [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="c61ce-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="c61ce-148">Dans l’Explorateur d’objets, cliquez sur hello base de données tooadd un pare-feu pour la règle, puis cliquez sur **nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="c61ce-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="c61ce-149">Une fenêtre de requête vide s’ouvre tooyour connecté de base de données.</span><span class="sxs-lookup"><span data-stu-id="c61ce-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="c61ce-150">Dans la fenêtre de requête hello, modifiez des hello tooyour publique adresse IP, puis exécutez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="c61ce-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="c61ce-151">Dans la barre d’outils de hello, cliquez sur **Execute** règle de pare-feu toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="c61ce-152">Afficher comment tooconnect un tooyour de l’application de base de données à l’aide d’une chaîne de connexion sécurisée</span><span class="sxs-lookup"><span data-stu-id="c61ce-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="c61ce-153">tooensure une connexion sécurisée, chiffrée entre une application cliente et la base de données SQL, la chaîne de connexion hello a toobe configuré pour :</span><span class="sxs-lookup"><span data-stu-id="c61ce-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="c61ce-154">demander une connexion chiffrée ;</span><span class="sxs-lookup"><span data-stu-id="c61ce-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="c61ce-155">certificat de serveur hello toonot approbation.</span><span class="sxs-lookup"><span data-stu-id="c61ce-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="c61ce-156">Cela établit une connexion à l’aide de la sécurité TLS (Transport Layer) et réduit les risques d’attaques de man-in-the-middle hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="c61ce-157">Vous pouvez obtenir les chaînes de connexion correctement configuré pour votre base de données SQL pour les clients pris en charge à pilotes à partir de hello portail Azure comme pour ADO.net dans cette capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="c61ce-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="c61ce-158">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="c61ce-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="c61ce-159">Sur hello **vue d’ensemble** pour votre base de données, cliquez sur **afficher les chaînes de connexion de base de données**.</span><span class="sxs-lookup"><span data-stu-id="c61ce-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="c61ce-160">Hello révision complète **ADO.NET** chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="c61ce-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![Chaîne de connexion ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="c61ce-162">Création d’utilisateurs de base de données</span><span class="sxs-lookup"><span data-stu-id="c61ce-162">Creating database users</span></span>

<span data-ttu-id="c61ce-163">Avant de créer des utilisateurs, vous devez d’abord choisir l’un des deux types d’authentification pris en charge par Azure SQL Database :</span><span class="sxs-lookup"><span data-stu-id="c61ce-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="c61ce-164">**L’authentification SQL**qui utilise le nom d’utilisateur et mot de passe pour les connexions et les utilisateurs qui ne sont valides uniquement dans hello le contexte d’une base de données spécifique au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="c61ce-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="c61ce-165">**L’authentification Azure Active Directory**, qui utilise des identités gérées par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c61ce-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="c61ce-166">Si vous souhaitez toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate par rapport à la base de données SQL, un annuaire Azure Active Directory rempli doit exister avant de pouvoir continuer.</span><span class="sxs-lookup"><span data-stu-id="c61ce-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="c61ce-167">Suivez ces étapes toocreate un utilisateur à l’aide de l’authentification SQL :</span><span class="sxs-lookup"><span data-stu-id="c61ce-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="c61ce-168">Se connecter à une base de données tooyour, par exemple à l’aide de [SQL Server Management Studio](./sql-database-connect-query-ssms.md) à l’aide de vos informations d’identification administrateur de serveur.</span><span class="sxs-lookup"><span data-stu-id="c61ce-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="c61ce-169">Dans l’Explorateur d’objets, cliquez sur la base de données hello tooadd un nouvel utilisateur sur et cliquez sur **nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="c61ce-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="c61ce-170">Une fenêtre de requête vide s’ouvre toohello connecté de base de données sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="c61ce-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="c61ce-171">Dans la fenêtre de requête hello, entrez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="c61ce-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="c61ce-172">Dans la barre d’outils de hello, cliquez sur **Execute** utilisateur de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c61ce-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="c61ce-173">Par défaut, utilisateur de hello peut se connecter toohello de base de données, mais ne comporte aucune donnée de tooread ou d’écriture des autorisations.</span><span class="sxs-lookup"><span data-stu-id="c61ce-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="c61ce-174">toogrant toohello de ces autorisations utilisateur récemment créé, exécutez hello suivant les deux commandes dans une nouvelle fenêtre de requête</span><span class="sxs-lookup"><span data-stu-id="c61ce-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="c61ce-175">Il s’agit des meilleures pratiques toocreate ces comptes non administrateurs à tooyour de niveau tooconnect hello de base de données de base de données, sauf si vous avez besoin de tooexecute les tâches d’administration telles que la création de nouveaux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c61ce-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="c61ce-176">Passez en revue hello [didacticiel d’Azure Active Directory](./sql-database-aad-authentication-configure.md) sur la façon de tooauthenticate à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c61ce-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="c61ce-177">Protéger vos données à l’aide du chiffrement</span><span class="sxs-lookup"><span data-stu-id="c61ce-177">Protect your data with encryption</span></span>

<span data-ttu-id="c61ce-178">Chiffrement de données transparent de base de données SQL Azure (TDE) chiffre automatiquement vos données au repos, sans nécessiter des modifications toohello application l’accès aux hello base de données chiffrée.</span><span class="sxs-lookup"><span data-stu-id="c61ce-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="c61ce-179">Pour les bases de données créées, TDE est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="c61ce-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="c61ce-180">tooenable chiffrement transparent des données pour votre base de données ou un tooverify TDE est activé, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c61ce-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="c61ce-181">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="c61ce-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="c61ce-182">Cliquez sur **chiffrement Transparent des données** tooopen page de configuration hello pour le chiffrement transparent des données.</span><span class="sxs-lookup"><span data-stu-id="c61ce-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![Chiffrement transparent des données](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="c61ce-184">Si nécessaire, définissez **le chiffrement des données** tooON et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c61ce-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="c61ce-185">processus de chiffrement Hello démarre en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="c61ce-186">Vous pouvez surveiller la progression hello à l’aide de base de données tooSQL connexion [SQL Server Management Studio](./sql-database-connect-query-ssms.md) en interrogeant la colonne encryption_state hello hello `sys.dm_database_encryption_keys` vue.</span><span class="sxs-lookup"><span data-stu-id="c61ce-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="c61ce-187">Activer l’audit Azure SQL Database, si nécessaire</span><span class="sxs-lookup"><span data-stu-id="c61ce-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="c61ce-188">Audit de base de données SQL Azure effectue le suivi des événements de base de données et les écrit le journal d’audit de tooan dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ce-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="c61ce-189">L’audit peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données et à découvrir des discordances et anomalies susceptibles d’indiquer des violations potentielles de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="c61ce-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="c61ce-190">Suivez ces étapes de toocreate une stratégie d’audit par défaut pour votre base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="c61ce-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="c61ce-191">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="c61ce-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="c61ce-192">Dans le panneau des paramètres de hello, sélectionnez **audit et la détection des menaces**.</span><span class="sxs-lookup"><span data-stu-id="c61ce-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="c61ce-193">Notez que l’audit au niveau serveur est désactivée et qu’il existe un **afficher les paramètres du serveur** lien qui vous permet de tooview ou modifier les paramètres d’audit de serveur hello à partir de ce contexte.</span><span class="sxs-lookup"><span data-stu-id="c61ce-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![Panneau Audit](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="c61ce-195">Si vous préférez tooenable un type d’Audit (ou un emplacement ?) différent de hello celle spécifiée au niveau du serveur hello, activer **ON** l’audit, puis choisissez hello **Blob** du Type d’audit.</span><span class="sxs-lookup"><span data-stu-id="c61ce-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="c61ce-196">Si l’audit des objets Blob de serveur est activé, audit de base de données configurée hello existe côte à côte avec l’audit du Blob serveur hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![Activer l’audit](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="c61ce-198">Sélectionnez **détails de stockage** tooopen hello Panneau de stockage des journaux d’Audit.</span><span class="sxs-lookup"><span data-stu-id="c61ce-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="c61ce-199">Compte de stockage Azure hello sélectionnez où seront enregistrés les journaux et la période de rétention hello, après le hello anciens journaux seront supprimés, puis cliquez sur **OK** bas hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="c61ce-200">Utilisez hello même compte de stockage pour tous les hello tooget de bases de données audités meilleur parti de l’audit de hello des modèles de rapports.</span><span class="sxs-lookup"><span data-stu-id="c61ce-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="c61ce-201">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c61ce-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c61ce-202">Si vous souhaitez que les événements audité de hello toocustomize, cela via PowerShell ou l’API REST - consultez hello [Automation (PowerShell / de l’API REST)](sql-database-auditing.md#subheading-7) section pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="c61ce-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="c61ce-203">Activer la détection de menaces pour les bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="c61ce-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="c61ce-204">La détection des menaces fournit une nouvelle couche de sécurité, ce qui permet aux clients toodetect et de répond toopotential menaces qu’ils se produisent en fournissant des alertes de sécurité sur les activités anormales.</span><span class="sxs-lookup"><span data-stu-id="c61ce-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="c61ce-205">Les utilisateurs peuvent Explorer à l’aide de l’audit de base de données SQL de toodetermine s’ils résultent d’une tooaccess de la tentative de violation ou exploitent les données dans la base de données hello d’événements suspects hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="c61ce-206">La détection des menaces rend tooaddress simple potentiels menaces toohello base de données sans nécessité de hello toobe un expert en sécurité ou gérer des systèmes de surveillance de la sécurité avancée.</span><span class="sxs-lookup"><span data-stu-id="c61ce-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="c61ce-207">Par exemple, il détecte certaines activités de base de données anormales indiquant des tentatives d’injection SQL potentielles.</span><span class="sxs-lookup"><span data-stu-id="c61ce-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="c61ce-208">Injection SQL est un des hello Web application problèmes de sécurité courants sur hello Internet, les applications utilisées tooattack piloté par les données.</span><span class="sxs-lookup"><span data-stu-id="c61ce-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="c61ce-209">Les attaquants profiter d’application vulnérabilités tooinject des instructions SQL malveillantes dans les champs de saisie d’application, de violation ou de modification des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="c61ce-210">Accédez à panneau de configuration de toohello de base de données SQL toomonitor de hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="c61ce-211">Dans le panneau des paramètres de hello, sélectionnez **audit et la détection des menaces**.</span><span class="sxs-lookup"><span data-stu-id="c61ce-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Volet de navigation](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="c61ce-213">Bonjour **audit et la détection des menaces** activer Panneau de configuration **ON** l’audit, qui affiche les paramètres de détection de menace hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="c61ce-214">**Activez** la détection des menaces.</span><span class="sxs-lookup"><span data-stu-id="c61ce-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="c61ce-215">Configurez la liste hello d’adresses de messagerie qui recevront les alertes de sécurité lors de la détection des activités anormales base de données.</span><span class="sxs-lookup"><span data-stu-id="c61ce-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="c61ce-216">Cliquez sur **enregistrer** Bonjour **détection d’audit et de menaces** panneau toosave hello nouvelle ou mis à jour stratégie de détection des menaces et de l’audit.</span><span class="sxs-lookup"><span data-stu-id="c61ce-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![Volet de navigation](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="c61ce-218">Si des activités de base de données anormales sont détectées, vous recevrez une notification par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="c61ce-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="c61ce-219">messagerie de Hello fournit des informations sur les événements de sécurité anormaux hello, y compris la nature hello d’activités anormales de hello, nom de la base de données, heure de serveur hello et de nom de l’événement.</span><span class="sxs-lookup"><span data-stu-id="c61ce-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="c61ce-220">En outre, il fournit des informations sur les causes possibles et recommandé actions tooinvestigate et atténuer la base de données du toohello de menaces potentielles hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="c61ce-221">parcours étapes suivant de Hello vous guident dans le toodo devez vous recevez ce courrier électronique :</span><span class="sxs-lookup"><span data-stu-id="c61ce-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![Courrier électronique de détection de menaces](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="c61ce-223">Dans le message électronique de hello, cliquez sur hello **le journal d’audit Azure SQL** lien lance hello portail Azure et afficher les enregistrements d’audit pertinentes hello en temps hello d’événement de suspectes hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![Enregistrements d’audit](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="c61ce-225">Cliquez sur hello audit enregistrements tooview plus de détails sur les activités de base de données suspecte hello comme instruction SQL, IP raison et le client d’échec.</span><span class="sxs-lookup"><span data-stu-id="c61ce-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Détails des enregistrements](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="c61ce-227">Dans le panneau des enregistrements d’audit hello, cliquez sur **ouvrir dans Excel** tooopen un préconfiguré excel tooimport de modèle et d’exécuter une analyse plus approfondie du journal d’audit de hello en temps hello d’événement de suspectes hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c61ce-228">Dans Excel 2010 ou version ultérieure, Power Query et hello **combinaison rapide** paramètre n’est requis.</span><span class="sxs-lookup"><span data-stu-id="c61ce-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![Ouvrir les enregistrements dans Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="c61ce-230">tooconfigure hello **combinaison rapide** le paramètre - Bonjour **POWER QUERY** onglet de ruban, sélectionnez **Options** boîte de dialogue Options toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="c61ce-231">Sélectionnez la section de confidentialité hello et choisissez hello deuxième option - « Ignorer les niveaux de confidentialité hello et potentiellement améliorer les performances » :</span><span class="sxs-lookup"><span data-stu-id="c61ce-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Combinaison rapide dans Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="c61ce-233">les journaux d’audit tooload SQL, assurez-vous que hello les paramètres dans l’onglet Paramètres de hello sont correctement définies et puis sélectionnez hello 'Data' ruban et cliquez sur le bouton Actualiser tout de hello.</span><span class="sxs-lookup"><span data-stu-id="c61ce-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Paramètres Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="c61ce-235">résultats de Hello s’affichent dans hello **les journaux d’Audit SQL** feuille qui vous permet d’effectuer une analyse toorun des activités anormales de hello qui ont été détectés et d’atténuer l’impact hello d’événement de sécurité hello dans votre application.</span><span class="sxs-lookup"><span data-stu-id="c61ce-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c61ce-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c61ce-236">Next steps</span></span>
<span data-ttu-id="c61ce-237">Vous pouvez améliorer la protection de hello de votre base de données contre les utilisateurs malveillants ou de tout accès non autorisé seulement quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="c61ce-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="c61ce-238">Ce didacticiel vous apprend à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c61ce-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c61ce-239">Définir des règles de pare-feu pour votre serveur et ou base de données</span><span class="sxs-lookup"><span data-stu-id="c61ce-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="c61ce-240">Se connecter à l’aide d’une chaîne de connexion sécurisée de la base de données tooyour</span><span class="sxs-lookup"><span data-stu-id="c61ce-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="c61ce-241">Gérer l’accès des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="c61ce-241">Manage user access</span></span>
> * <span data-ttu-id="c61ce-242">Protéger vos données à l’aide du chiffrement</span><span class="sxs-lookup"><span data-stu-id="c61ce-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="c61ce-243">Activer l’audit Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c61ce-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="c61ce-244">Activer la détection de menaces pour les bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="c61ce-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="c61ce-245">Améliorer les performances des bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="c61ce-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

