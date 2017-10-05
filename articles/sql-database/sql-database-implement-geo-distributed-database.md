---
title: "Implémenter une solution de base de données SQL Azure géo-distribuée | Microsoft Docs"
description: "Découvrez comment configurer votre base de données et votre application SQL Azure pour le basculement vers une base de données répliquée et tester le basculement."
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
ms.openlocfilehash: 9f53f318e20dac9248906bdbe898ba4dacb286ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="80a80-103">Implémenter une base de données géo-distribuée</span><span class="sxs-lookup"><span data-stu-id="80a80-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="80a80-104">Dans ce didacticiel, vous configurez une application et une base de données SQL Azure pour le basculement vers une région distante, puis testez votre plan de basculement.</span><span class="sxs-lookup"><span data-stu-id="80a80-104">In this tutorial, you configure an Azure SQL database and application for failover to a remote region, and then test your failover plan.</span></span> <span data-ttu-id="80a80-105">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="80a80-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="80a80-106">Créer des utilisateurs de base de données et leur accorder des autorisations</span><span class="sxs-lookup"><span data-stu-id="80a80-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="80a80-107">Configurer une règle de pare-feu au niveau de la base de données</span><span class="sxs-lookup"><span data-stu-id="80a80-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="80a80-108">Créer un [groupe de basculement de géoréplication](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="80a80-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="80a80-109">Créer et compiler une application Java pour interroger une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="80a80-109">Create and compile a Java application to query an Azure SQL database</span></span>
> * <span data-ttu-id="80a80-110">Effectuer une simulation de récupération d'urgence</span><span class="sxs-lookup"><span data-stu-id="80a80-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="80a80-111">Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="80a80-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="80a80-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="80a80-112">Prerequisites</span></span>

<span data-ttu-id="80a80-113">Pour suivre ce tutoriel, vérifiez que les conditions préalables suivantes sont bien satisfaites :</span><span class="sxs-lookup"><span data-stu-id="80a80-113">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

- <span data-ttu-id="80a80-114">La dernière version d’[Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs) est installée.</span><span class="sxs-lookup"><span data-stu-id="80a80-114">Installed the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="80a80-115">Une base de données SQL Azure est installée.</span><span class="sxs-lookup"><span data-stu-id="80a80-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="80a80-116">Ce didacticiel utilise la base de données exemple AdventureWorksLT nommée **mySampleDatabase** créée à partir de l’un des démarrages rapides suivants :</span><span class="sxs-lookup"><span data-stu-id="80a80-116">This tutorial uses the AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="80a80-117">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="80a80-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="80a80-118">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="80a80-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="80a80-119">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="80a80-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="80a80-120">Vous avez identifié une méthode pour exécuter les scripts SQL sur votre base de données. Vous pouvez utiliser l’un des outils de requête suivants :</span><span class="sxs-lookup"><span data-stu-id="80a80-120">Have identified a method to execute SQL scripts against your database, you can use one of the following query tools:</span></span>
   - <span data-ttu-id="80a80-121">L’éditeur de requêtes dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80a80-121">The query editor in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80a80-122">Pour plus d’informations sur l’utilisation de l’éditeur de requêtes dans le portail Azure, consultez la section [Utilisez l’éditeur de requêtes pour vous connecter et interroger des données](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="80a80-122">For more information on using the query editor in the Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="80a80-123">La dernière version de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), qui est un environnement intégré pour la gestion des infrastructures SQL, allant de SQL Server à SQL Database pour Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="80a80-123">The newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server to SQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="80a80-124">La nouvelle version de [Visual Studio Code](https://code.visualstudio.com/docs), qui est un éditeur de code graphique pour Linux, macOS et Windows et qui prend en charge les extensions, y compris [l’extension mssql](https://aka.ms/mssql-marketplace) pour l’exécution de requêtes dans Microsoft SQL Server, Azure SQL Database et SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="80a80-124">The newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="80a80-125">Pour plus d’informations sur l’utilisation de cet outil avec la base de données SQL Azure, consultez l’article [Utilisez VS Code pour vous connecter et interroger des données](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="80a80-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="80a80-126">Créer des utilisateurs de base de données et accorder des autorisations</span><span class="sxs-lookup"><span data-stu-id="80a80-126">Create database users and grant permissions</span></span>

<span data-ttu-id="80a80-127">Connectez-vous à votre base de données et créez des comptes d’utilisateur à l’aide de l’un des outils de requête suivant :</span><span class="sxs-lookup"><span data-stu-id="80a80-127">Connect to your database and create user accounts using one of the following query tools:</span></span>

- <span data-ttu-id="80a80-128">L’éditeur de requêtes dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="80a80-128">The Query editor in the Azure portal</span></span>
- <span data-ttu-id="80a80-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="80a80-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="80a80-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="80a80-130">Visual Studio Code</span></span>

<span data-ttu-id="80a80-131">Ces comptes d’utilisateur sont répliqués automatiquement vers votre serveur secondaire (et restent synchronisés).</span><span class="sxs-lookup"><span data-stu-id="80a80-131">These user accounts replicate automatically to your secondary server (and be kept in sync).</span></span> <span data-ttu-id="80a80-132">Pour utiliser SQL Server Management Studio ou Visual Studio Code, vous devrez peut-être configurer une règle de pare-feu si vous vous connectez à partir d’un client à une adresse IP pour laquelle vous n’avez pas encore configuré de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="80a80-132">To use SQL Server Management Studio or Visual Studio Code, you may need to configure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="80a80-133">Pour des instructions plus détaillées, consultez la section [Créer une règle de pare-feu au niveau du serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="80a80-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="80a80-134">Dans une fenêtre de requête, exécutez la requête suivante pour créer deux comptes d’utilisateur dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="80a80-134">In a query window, execute the following query to create two user accounts in your database.</span></span> <span data-ttu-id="80a80-135">Ce script accorde des autorisations **db_owner** pour le compte **app_admin** et accorde les autorisations **SÉLECTIONNER** et **METTE À JOUR** pour le compte **app_user**.</span><span class="sxs-lookup"><span data-stu-id="80a80-135">This script grants **db_owner** permissions to the **app_admin** account and grants **SELECT** and **UPDATE** permissions to the **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user to db_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission to SalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product TO app_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="80a80-136">Créer un pare-feu au niveau de la base de données</span><span class="sxs-lookup"><span data-stu-id="80a80-136">Create database-level firewall</span></span>

<span data-ttu-id="80a80-137">Créez une [règle de pare-feu au niveau de la base de données](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) pour votre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="80a80-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="80a80-138">Cette règle de pare-feu au niveau de la base de données effectue automatiquement la réplication vers le serveur secondaire que vous allez créer dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="80a80-138">This database-level firewall rule replicates automatically to the secondary server that you create in this tutorial.</span></span> <span data-ttu-id="80a80-139">Pour vous simplifier la tâche (dans ce didacticiel), utilisez l’adresse IP publique de l’ordinateur sur lequel vous effectuez les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="80a80-139">For simplicity (in this tutorial), use the public IP address of the computer on which you are performing the steps in this tutorial.</span></span> <span data-ttu-id="80a80-140">Pour déterminer l’adresse IP utilisée pour la règle de pare-feu au niveau du serveur pour votre ordinateur actuel, consultez la section [Créer une règle de pare-feu au niveau du serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="80a80-140">To determine the IP address used for the server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="80a80-141">Dans la fenêtre de requête ouverte, remplacez la requête précédente par la requête suivante, en remplaçant les adresses IP par les adresses IP appropriées pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="80a80-141">In your open query window, replace the previous query with the following query, replacing the IP addresses with the appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="80a80-142">Créer un groupe de basculement automatique de géoréplication active</span><span class="sxs-lookup"><span data-stu-id="80a80-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="80a80-143">À l’aide d’Azure PowerShell, créez un [groupe de basculement automatique de géoréplication active](sql-database-geo-replication-overview.md) entre votre serveur SQL Azure existant et le nouveau serveur SQL Azure vide dans une région Azure, puis ajoutez votre base de données exemple au groupe de basculement.</span><span class="sxs-lookup"><span data-stu-id="80a80-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and the new empty Azure SQL server in an Azure region, and then add your sample database to the failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80a80-144">Ces commandes cmdlets nécessitent Azure PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="80a80-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="80a80-145">Remplissez les variables de vos scripts PowerShell en utilisant les valeurs de votre serveur existant et de la base de données exemple et fournissez une valeur globalement unique pour le nom du groupe de basculement.</span><span class="sxs-lookup"><span data-stu-id="80a80-145">Populate variables for your PowerShell scripts using the values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

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

2. <span data-ttu-id="80a80-146">Créez un serveur de sauvegarde vide dans votre région de basculement.</span><span class="sxs-lookup"><span data-stu-id="80a80-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="80a80-147">Créez un groupe de basculement entre les deux serveurs.</span><span class="sxs-lookup"><span data-stu-id="80a80-147">Create a failover group between the two servers.</span></span>

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

4. <span data-ttu-id="80a80-148">Ajoutez votre base de données au groupe de basculement.</span><span class="sxs-lookup"><span data-stu-id="80a80-148">Add your database to the failover group.</span></span>

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

## <a name="install-java-software"></a><span data-ttu-id="80a80-149">Installer le logiciel Java</span><span class="sxs-lookup"><span data-stu-id="80a80-149">Install Java software</span></span>

<span data-ttu-id="80a80-150">Les étapes de cette section supposent que vous connaissez le développement avec Java et que vous ne savez pas utiliser la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="80a80-150">The steps in this section assume that you are familiar with developing using Java and are new to working with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="80a80-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="80a80-151">**Mac OS**</span></span>
<span data-ttu-id="80a80-152">Ouvrez votre terminal et accédez au répertoire dans lequel vous envisagez de créer votre projet Java.</span><span class="sxs-lookup"><span data-stu-id="80a80-152">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="80a80-153">Entrez les commandes suivantes pour installer **brew** et **Maven** :</span><span class="sxs-lookup"><span data-stu-id="80a80-153">Install **brew** and **Maven** by entering the following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="80a80-154">Pour obtenir des instructions détaillées sur l’installation et la configuration des environnements Java et Maven, rendez-vous sur la page [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/) (Création d’une application à l’aide de SQL Server), sélectionnez **Java**, sélectionnez **MacOS**, puis suivez les instructions détaillées pour la configuration de Java et Maven aux étapes 1.2 et 1.3.</span><span class="sxs-lookup"><span data-stu-id="80a80-154">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow the detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="80a80-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="80a80-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="80a80-156">Ouvrez votre terminal et accédez au répertoire dans lequel vous envisagez de créer votre projet Java.</span><span class="sxs-lookup"><span data-stu-id="80a80-156">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="80a80-157">Entrez les commandes suivantes pour installer **Maven** :</span><span class="sxs-lookup"><span data-stu-id="80a80-157">Install **Maven** by entering the following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="80a80-158">Pour obtenir des instructions détaillées sur l’installation et la configuration des environnements Java et Maven, rendez-vous sur la page [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/) (Création d’une application à l’aide de SQL Server), sélectionnez **Java**, sélectionnez **Ubuntu**, puis suivez les instructions détaillées pour la configuration de Java et Maven aux étapes 1.2, 1.3 et 1.4.</span><span class="sxs-lookup"><span data-stu-id="80a80-158">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow the detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="80a80-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="80a80-159">**Windows**</span></span>
<span data-ttu-id="80a80-160">Installez [Maven](https://maven.apache.org/download.cgi) à l’aide du programme d’installation officiel.</span><span class="sxs-lookup"><span data-stu-id="80a80-160">Install [Maven](https://maven.apache.org/download.cgi) using the official installer.</span></span> <span data-ttu-id="80a80-161">Utilisez Maven pour gérer les dépendances ainsi que pour créer, tester et exécuter votre projet Java.</span><span class="sxs-lookup"><span data-stu-id="80a80-161">Use Maven to help manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="80a80-162">Pour obtenir des instructions détaillées sur l’installation et la configuration des environnements Java et Maven, rendez-vous sur la page [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/) (Création d’une application à l’aide de SQL Server), sélectionnez **Java**, sélectionnez Windows, puis suivez les instructions détaillées pour la configuration de Java et Maven aux étapes 1.2 et 1.3.</span><span class="sxs-lookup"><span data-stu-id="80a80-162">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow the detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="80a80-163">Créer le projet SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="80a80-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="80a80-164">Dans la console de commandes (par exemple Bash), créez un projet Maven.</span><span class="sxs-lookup"><span data-stu-id="80a80-164">In the command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="80a80-165">Saisissez **Y** et cliquez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="80a80-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="80a80-166">Remplacez les répertoires dans votre projet nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="80a80-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="80a80-167">À l’aide de votre éditeur habituel, ouvrez le fichier pom.xml dans le dossier de votre projet.</span><span class="sxs-lookup"><span data-stu-id="80a80-167">Using your favorite editor, open the pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="80a80-168">Ajoutez le pilote JDBC Microsoft pour la dépendance de SQL Server à votre projet Maven en ouvrant votre éditeur de texte habituel et en copiant-collant les lignes suivantes dans votre fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="80a80-168">Add the Microsoft JDBC Driver for SQL Server dependency to your Maven project by opening your favorite text editor and copying and pasting the following lines into your pom.xml file.</span></span> <span data-ttu-id="80a80-169">Ne remplacez pas les valeurs existantes préremplies dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="80a80-169">Do not overwrite the existing values prepopulated in the file.</span></span> <span data-ttu-id="80a80-170">La dépendance JDBC doit être collée dans la section « dependencies » plus large ( ).</span><span class="sxs-lookup"><span data-stu-id="80a80-170">The JDBC dependency must be pasted within the larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="80a80-171">Spécifiez la version de Java à utiliser pour compiler le projet en ajoutant la section « properties » suivante dans le fichier pom.xml, après la section « dependencies ».</span><span class="sxs-lookup"><span data-stu-id="80a80-171">Specify the version of Java to compile the project against by adding the following “properties” section into the pom.xml file after the "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="80a80-172">Ajoutez la section « build » suivante dans le fichier pom.xml après la section « properties » pour la prise en charge des fichiers manifeste dans des fichiers JAR.</span><span class="sxs-lookup"><span data-stu-id="80a80-172">Add the following "build" section into the pom.xml file after the "properties" section to support manifest files in jars.</span></span>       

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
8. <span data-ttu-id="80a80-173">Enregistrez et fermez le fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="80a80-173">Save and close the pom.xml file.</span></span>
9. <span data-ttu-id="80a80-174">Ouvrez le fichier App.java (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) et remplacez son contenu avec le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="80a80-174">Open the App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace the contents with the following contents.</span></span> <span data-ttu-id="80a80-175">Remplacez le nom du groupe de basculement par le nom de votre groupe de basculement.</span><span class="sxs-lookup"><span data-stu-id="80a80-175">Replace the failover group name with the name for your failover group.</span></span> <span data-ttu-id="80a80-176">Si vous avez modifié le nom de la base de données, l’utilisateur ou le mot de passe, modifiez aussi ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="80a80-176">If you have changed the values for the database name, user, or password, change those values as well.</span></span>

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
      // Insert data into the product table with a unique product name that we can use to find the product again later
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
      // Query the data that was previously inserted into the primary database from the geo replicated database
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
      // Query the high water mark id that is stored in the table to be able to make unique inserts 
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
6. <span data-ttu-id="80a80-177">Enregistrez et fermez le fichier App.java.</span><span class="sxs-lookup"><span data-stu-id="80a80-177">Save and close the App.java file.</span></span>

## <a name="compile-and-run-the-sqldbsample-project"></a><span data-ttu-id="80a80-178">Compiler et exécuter le projet SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="80a80-178">Compile and run the SqlDbSample project</span></span>

1. <span data-ttu-id="80a80-179">Dans la console de commandes, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="80a80-179">In the command console, execute to following command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="80a80-180">Lorsque vous avez terminé, exécutez la commande suivante pour exécuter l’application (elle s’exécute pendant environ 1 heure, sauf si vous l’arrêtez manuellement) :</span><span class="sxs-lookup"><span data-stu-id="80a80-180">When finished, execute the following command to run the application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="80a80-181">Effectuer une simulation de récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="80a80-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="80a80-182">Appelez le basculement manuel du groupe de basculement.</span><span class="sxs-lookup"><span data-stu-id="80a80-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="80a80-183">Observez les résultats de l’application pendant le basculement.</span><span class="sxs-lookup"><span data-stu-id="80a80-183">Observe the application results during failover.</span></span> <span data-ttu-id="80a80-184">Certaines insertions échouent pendant l’actualisation du cache du DNS.</span><span class="sxs-lookup"><span data-stu-id="80a80-184">Some inserts fail while the DNS cache refreshes.</span></span>     

3. <span data-ttu-id="80a80-185">Découvrez le rôle que votre serveur de récupération d’urgence exécute.</span><span class="sxs-lookup"><span data-stu-id="80a80-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="80a80-186">Effectuez une restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="80a80-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="80a80-187">Observez les résultats de l’application pendant la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="80a80-187">Observe the application results during failback.</span></span> <span data-ttu-id="80a80-188">Certaines insertions échouent pendant l’actualisation du cache du DNS.</span><span class="sxs-lookup"><span data-stu-id="80a80-188">Some inserts fail while the DNS cache refreshes.</span></span>     

6. <span data-ttu-id="80a80-189">Découvrez le rôle que votre serveur de récupération d’urgence exécute.</span><span class="sxs-lookup"><span data-stu-id="80a80-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="80a80-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80a80-190">Next steps</span></span> 

<span data-ttu-id="80a80-191">Pour plus d’informations, voir l’article [Groupes de basculement et géoréplication active](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80a80-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
