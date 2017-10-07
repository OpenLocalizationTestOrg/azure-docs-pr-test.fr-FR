---
title: "aaaImplement une solution de base de données SQL Azure répartis géographiquement | Documents Microsoft"
description: "En savoir plus tooconfigure votre base de données SQL Azure et l’application tooa basculement répliquée de base de données et testez le basculement."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="0e693-103">Implémenter une base de données géo-distribuée</span><span class="sxs-lookup"><span data-stu-id="0e693-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="0e693-104">Dans ce didacticiel, vous configurez une base de données SQL Azure et d’une application de la région de basculement tooa à distance, ensuite Testez votre plan de basculement.</span><span class="sxs-lookup"><span data-stu-id="0e693-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="0e693-105">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="0e693-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="0e693-106">Créer des utilisateurs de base de données et leur accorder des autorisations</span><span class="sxs-lookup"><span data-stu-id="0e693-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="0e693-107">Configurer une règle de pare-feu au niveau de la base de données</span><span class="sxs-lookup"><span data-stu-id="0e693-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="0e693-108">Créer un [groupe de basculement de géoréplication](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0e693-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="0e693-109">Créer et compiler un tooquery d’application Java une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0e693-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="0e693-110">Effectuer une simulation de récupération d'urgence</span><span class="sxs-lookup"><span data-stu-id="0e693-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="0e693-111">Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="0e693-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0e693-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0e693-112">Prerequisites</span></span>

<span data-ttu-id="0e693-113">toocomplete ce didacticiel, assurez-vous que hello est suivant des conditions préalables requises sont effectuées :</span><span class="sxs-lookup"><span data-stu-id="0e693-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="0e693-114">Hello installé dernières [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="0e693-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="0e693-115">Une base de données SQL Azure est installée.</span><span class="sxs-lookup"><span data-stu-id="0e693-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="0e693-116">Ce didacticiel utilise la base de données AdventureWorksLT hello avec un nom de **mySampleDatabase** à partir d’un de ces Démarrages rapides :</span><span class="sxs-lookup"><span data-stu-id="0e693-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="0e693-117">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="0e693-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="0e693-118">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="0e693-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="0e693-119">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e693-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="0e693-120">A identifié un tooexecute méthode SQL scripts contre votre base de données, vous pouvez utiliser une des hello suivant des outils de requête :</span><span class="sxs-lookup"><span data-stu-id="0e693-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="0e693-121">éditeur de requête Hello Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e693-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0e693-122">Pour plus d’informations sur l’utilisation de l’éditeur de requête hello Bonjour portail Azure, consultez [se connecter et requête à l’aide de l’éditeur de requête](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="0e693-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="0e693-123">version la plus récente de Hello [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), qui est un environnement intégré pour la gestion d’une infrastructure SQL, à partir de SQL Server tooSQL de base de données pour Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="0e693-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="0e693-124">version la plus récente de Hello [Visual Studio Code](https://code.visualstudio.com/docs), qui est un éditeur de code graphique pour Linux, Mac OS, et que Windows qui prend en charge les extensions, y compris hello [mssql extension](https://aka.ms/mssql-marketplace) pour l’interrogation de Microsoft SQL Server , Base de données SQL azure et SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0e693-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="0e693-125">Pour plus d’informations sur l’utilisation de cet outil avec la base de données SQL Azure, consultez l’article [Utilisez VS Code pour vous connecter et interroger des données](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="0e693-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="0e693-126">Créer des utilisateurs de base de données et accorder des autorisations</span><span class="sxs-lookup"><span data-stu-id="0e693-126">Create database users and grant permissions</span></span>

<span data-ttu-id="0e693-127">Se connecter tooyour de base de données et créer des comptes d’utilisateur à l’aide de hello suivant des outils de requête :</span><span class="sxs-lookup"><span data-stu-id="0e693-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="0e693-128">éditeur de requête Hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="0e693-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="0e693-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="0e693-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="0e693-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0e693-130">Visual Studio Code</span></span>

<span data-ttu-id="0e693-131">Ces comptes d’utilisateur répliquent automatiquement le serveur secondaire de tooyour (et être synchronisés).</span><span class="sxs-lookup"><span data-stu-id="0e693-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="0e693-132">toouse SQL Server Management Studio ou Visual Studio Code, vous devrez peut-être tooconfigure une règle de pare-feu si vous vous connectez à partir d’un client à une adresse IP pour laquelle vous n'avez pas encore configuré un pare-feu.</span><span class="sxs-lookup"><span data-stu-id="0e693-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="0e693-133">Pour des instructions plus détaillées, consultez la section [Créer une règle de pare-feu au niveau du serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="0e693-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="0e693-134">Dans une fenêtre de requête, exécutez hello suivant requête toocreate deux comptes d’utilisateur dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="0e693-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="0e693-135">Ce script accorde **db_owner** autorisations toohello **app_admin** compte et accorde **sélectionnez** et **mise à jour** toohello d’autorisations **app_user** compte.</span><span class="sxs-lookup"><span data-stu-id="0e693-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="0e693-136">Créer un pare-feu au niveau de la base de données</span><span class="sxs-lookup"><span data-stu-id="0e693-136">Create database-level firewall</span></span>

<span data-ttu-id="0e693-137">Créez une [règle de pare-feu au niveau de la base de données](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) pour votre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0e693-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="0e693-138">Cette règle de pare-feu de niveau base de données réplique automatiquement toohello serveur secondaire que vous créez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0e693-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="0e693-139">Pour plus de simplicité (dans ce didacticiel), utilisez hello une adresse IP publique de l’ordinateur hello sur lequel vous effectuez les étapes hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0e693-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="0e693-140">adresse IP de toodetermine hello utilisé pour la règle de pare-feu de niveau serveur hello pour votre ordinateur actuel, consultez [création d’un pare-feu au niveau du serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="0e693-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="0e693-141">Dans la fenêtre de requête ouverte, remplacez les requêtes précédentes hello hello suivant la requête, en remplaçant les adresses IP hello avec hello adresses IP appropriées pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="0e693-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="0e693-142">Créer un groupe de basculement automatique de géoréplication active</span><span class="sxs-lookup"><span data-stu-id="0e693-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="0e693-143">À l’aide d’Azure PowerShell, créer un [groupe de basculement automatique de géo-réplication active](sql-database-geo-replication-overview.md) entre votre serveur SQL Azure et hello nouvelle existants vides serveur SQL Azure dans une région Azure, et puis ajoutez votre groupe de basculement toohello exemple de base de données.</span><span class="sxs-lookup"><span data-stu-id="0e693-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e693-144">Ces commandes cmdlets nécessitent Azure PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="0e693-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="0e693-145">Remplir les variables pour vos scripts PowerShell à l’aide des valeurs de hello pour votre serveur existant et de la base de données exemple et fournir une valeur unique pour le nom de groupe de basculement.</span><span class="sxs-lookup"><span data-stu-id="0e693-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. <span data-ttu-id="0e693-146">Créez un serveur de sauvegarde vide dans votre région de basculement.</span><span class="sxs-lookup"><span data-stu-id="0e693-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="0e693-147">Créer un groupe de basculement entre deux serveurs de hello.</span><span class="sxs-lookup"><span data-stu-id="0e693-147">Create a failover group between hello two servers.</span></span>

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. <span data-ttu-id="0e693-148">Ajouter à votre groupe de basculement de toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="0e693-148">Add your database toohello failover group.</span></span>

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a><span data-ttu-id="0e693-149">Installer le logiciel Java</span><span class="sxs-lookup"><span data-stu-id="0e693-149">Install Java software</span></span>

<span data-ttu-id="0e693-150">étapes de Hello dans cette section supposent que vous êtes familiarisé avec le développement à l’aide de Java et tooworking nouvelle base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0e693-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="0e693-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="0e693-151">**Mac OS**</span></span>
<span data-ttu-id="0e693-152">Ouvrez votre terminal et accédez répertoire tooa où vous prévoyez de créer un projet Java.</span><span class="sxs-lookup"><span data-stu-id="0e693-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="0e693-153">Installer **brew** et **Maven** en entrant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="0e693-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="0e693-154">Pour obtenir des instructions détaillées sur l’installation et configuration d’environnement Java et Maven, accédez hello [générer une application à l’aide de SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), sélectionnez **Java**, sélectionnez **MacOS**, puis suivez Hello instructions détaillées pour la configuration de Java et Maven à l’étape 1.2 et 1.3.</span><span class="sxs-lookup"><span data-stu-id="0e693-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="0e693-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="0e693-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="0e693-156">Ouvrez votre terminal et accédez répertoire tooa où vous prévoyez de créer un projet Java.</span><span class="sxs-lookup"><span data-stu-id="0e693-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="0e693-157">Installer **Maven** en entrant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="0e693-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="0e693-158">Pour obtenir des instructions détaillées sur l’installation et configuration d’environnement Java et Maven, accédez hello [générer une application à l’aide de SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), sélectionnez **Java**, sélectionnez **Ubuntu**, puis suivez Hello instructions détaillées pour la configuration de Java et Maven à l’étape 1.2, 1.3 et 1.4.</span><span class="sxs-lookup"><span data-stu-id="0e693-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="0e693-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="0e693-159">**Windows**</span></span>
<span data-ttu-id="0e693-160">Installer [Maven](https://maven.apache.org/download.cgi) à l’aide du programme d’installation officielle de hello.</span><span class="sxs-lookup"><span data-stu-id="0e693-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="0e693-161">Utilisez Maven toohelp gérer les dépendances, créer, tester et exécuter votre projet Java.</span><span class="sxs-lookup"><span data-stu-id="0e693-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="0e693-162">Pour obtenir des instructions détaillées sur l’installation et configuration d’environnement Java et Maven, accédez hello [générer une application à l’aide de SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), sélectionnez **Java**, sélectionnez Windows, puis suivez hello des instructions détaillées de configuration de Java et Maven à l’étape 1.2 et 1.3.</span><span class="sxs-lookup"><span data-stu-id="0e693-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="0e693-163">Créer le projet SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="0e693-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="0e693-164">Dans la console de commande hello (par exemple, un interpréteur de commandes), créez un projet de Maven.</span><span class="sxs-lookup"><span data-stu-id="0e693-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="0e693-165">Saisissez **Y** et cliquez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="0e693-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="0e693-166">Remplacez les répertoires dans votre projet nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="0e693-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="0e693-167">À l’aide de votre éditeur favori, ouvrir le fichier de pom.xml hello dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="0e693-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="0e693-168">Ajouter hello pilote JDBC Microsoft pour le projet de SQL Server dépendance tooyour Maven en ouvrant l’éditeur de texte et copier- coller hello lignes suivantes dans votre fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="0e693-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="0e693-169">Ne pas remplacer les valeurs existantes hello préremplies dans le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="0e693-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="0e693-170">Hello dépendance JDBC doit être collé dans hello section « dépendances » supérieure ().</span><span class="sxs-lookup"><span data-stu-id="0e693-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="0e693-171">Spécifiez hello version de Java toocompile hello projet contre en ajoutant des hello suivant la section « Propriétés » dans le fichier de pom.xml hello après la section « dépendances » de hello.</span><span class="sxs-lookup"><span data-stu-id="0e693-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="0e693-172">Ajouter suivant de hello « build » section dans le fichier de pom.xml hello après hello « propriétés » section toosupport fichiers manifeste dans des fichiers JAR.</span><span class="sxs-lookup"><span data-stu-id="0e693-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. <span data-ttu-id="0e693-173">Enregistrez et fermez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="0e693-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="0e693-174">Ouvrir le fichier de App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) et remplacez contenu de hello par hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="0e693-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="0e693-175">Remplacez le nom de groupe de basculement hello par nom hello pour votre groupe de basculement.</span><span class="sxs-lookup"><span data-stu-id="0e693-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="0e693-176">Si vous avez modifié les valeurs hello pour le nom de base de données hello, un utilisateur ou mot de passe, modifiez ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0e693-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. <span data-ttu-id="0e693-177">Enregistrez et fermez le fichier de App.java hello.</span><span class="sxs-lookup"><span data-stu-id="0e693-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="0e693-178">Compilez et exécutez hello SqlDbSample projet</span><span class="sxs-lookup"><span data-stu-id="0e693-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="0e693-179">Dans la console de commande hello, exécutez toofollowing commande.</span><span class="sxs-lookup"><span data-stu-id="0e693-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="0e693-180">Lorsque vous avez terminé, exécutez hello suivant commande toorun hello application (il s’exécute pendant environ 1 heure, sauf si vous l’arrêtez manuellement) :</span><span class="sxs-lookup"><span data-stu-id="0e693-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="0e693-181">Effectuer une simulation de récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="0e693-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="0e693-182">Appelez le basculement manuel du groupe de basculement.</span><span class="sxs-lookup"><span data-stu-id="0e693-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="0e693-183">Observer les résultats de l’application hello pendant le basculement.</span><span class="sxs-lookup"><span data-stu-id="0e693-183">Observe hello application results during failover.</span></span> <span data-ttu-id="0e693-184">Certaines insertions échouent pendant que hello cache DNS actualise.</span><span class="sxs-lookup"><span data-stu-id="0e693-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="0e693-185">Découvrez le rôle que votre serveur de récupération d’urgence exécute.</span><span class="sxs-lookup"><span data-stu-id="0e693-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="0e693-186">Effectuez une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="0e693-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="0e693-187">Observer les résultats de l’application hello lors de la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="0e693-187">Observe hello application results during failback.</span></span> <span data-ttu-id="0e693-188">Certaines insertions échouent pendant que hello cache DNS actualise.</span><span class="sxs-lookup"><span data-stu-id="0e693-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="0e693-189">Découvrez le rôle que votre serveur de récupération d’urgence exécute.</span><span class="sxs-lookup"><span data-stu-id="0e693-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="0e693-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e693-190">Next steps</span></span> 

<span data-ttu-id="0e693-191">Pour plus d’informations, voir l’article [Groupes de basculement et géoréplication active](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e693-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
