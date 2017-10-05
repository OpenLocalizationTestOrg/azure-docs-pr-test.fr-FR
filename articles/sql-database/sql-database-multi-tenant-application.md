---
title: "Déploiement d’une application SaaS mutualisée avec Azure SQL Database | Microsoft Docs"
description: "Déployez une application SaaS mutualisée avec Azure SQL Database."
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: 0aea69d86a51c38c99a72f46737de1eea27bef83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="1d01a-103">Déployer une application SaaS mutualisée à l’aide d’Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1d01a-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="1d01a-104">Une application mutualisée désigne une application hébergée dans un environnement cloud, qui fournit le même ensemble de services à des centaines ou milliers de locataires qui ne partagent pas ou ne voient pas les données d’autrui.</span><span class="sxs-lookup"><span data-stu-id="1d01a-104">A multi-tenant application is an application hosted in a cloud environment and that provides the same set of services to hundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="1d01a-105">Il peut par exemple s’agir d’une application SaaS qui fournit des services aux locataires dans un environnement hébergé dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="1d01a-105">An example is an SaaS application that provides services to tenants in a cloud-hosted environment.</span></span> <span data-ttu-id="1d01a-106">Ce modèle isole les données pour chaque locataire et optimise la répartition des ressources de coûts.</span><span class="sxs-lookup"><span data-stu-id="1d01a-106">This model isolates the data for each tenant and optimizes the distribution of resources for cost.</span></span> 

<span data-ttu-id="1d01a-107">Ce didacticiel montre comment créer une application SaaS mutualisée à l’aide d’Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1d01a-107">This tutorial demonstrates how to create a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="1d01a-108">Ce didacticiel vous apprendra à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1d01a-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1d01a-109">Configuration d’un environnement de base de données pour la prise en charge d’une application SaaS mutualisée, à l’aide du modèle « base de données par locataire »</span><span class="sxs-lookup"><span data-stu-id="1d01a-109">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="1d01a-110">Création d’un catalogue de locataires</span><span class="sxs-lookup"><span data-stu-id="1d01a-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="1d01a-111">Configuration d’une base de données de locataires et inscription de cette base de données dans le catalogue de locataires</span><span class="sxs-lookup"><span data-stu-id="1d01a-111">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="1d01a-112">Configuration d’un exemple d’application Java</span><span class="sxs-lookup"><span data-stu-id="1d01a-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="1d01a-113">Accès aux bases de données de locataires à l’aide d’une simple application console Java</span><span class="sxs-lookup"><span data-stu-id="1d01a-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="1d01a-114">Suppression d’un locataire</span><span class="sxs-lookup"><span data-stu-id="1d01a-114">Delete a tenant</span></span>

<span data-ttu-id="1d01a-115">Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="1d01a-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d01a-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1d01a-116">Prerequisites</span></span>

<span data-ttu-id="1d01a-117">Pour suivre ce didacticiel, vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1d01a-117">To complete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="1d01a-118">La dernière version de PowerShell et le [dernier Kit de développement logiciel (SDK) Azure PowerShell](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="1d01a-118">Installed the newest version of PowerShell and the [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="1d01a-119">La dernière version de [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="1d01a-119">Installed the latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="1d01a-120">L’installation de SQL Server Management Studio installe également la version la plus récente de SQLPackage, un utilitaire de ligne de commande qui peut être utilisé pour automatiser de nombreuses tâches de développement de bases de données.</span><span class="sxs-lookup"><span data-stu-id="1d01a-120">Installing SQL Server Management Studio also installs the latest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span>

* <span data-ttu-id="1d01a-121">Un ordinateur disposant de [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) et du [dernier kit de développement JAVA (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="1d01a-121">Installed the [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and the [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="1d01a-122">[Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="1d01a-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="1d01a-123">Maven servira à gérer les dépendances et à générer, tester et exécuter l’exemple de projet Java.</span><span class="sxs-lookup"><span data-stu-id="1d01a-123">Maven will be used to help manage dependencies, build, test and run the sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="1d01a-124">Configuration de l’environnement des données</span><span class="sxs-lookup"><span data-stu-id="1d01a-124">Set up data environment</span></span>

<span data-ttu-id="1d01a-125">Vous allez approvisionner une base de données par locataire.</span><span class="sxs-lookup"><span data-stu-id="1d01a-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="1d01a-126">Le modèle « base de données par locataire » constitue la meilleure manière d’isoler les locataires tout en réduisant les coûts DevOps.</span><span class="sxs-lookup"><span data-stu-id="1d01a-126">The database-per-tenant model provides the highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="1d01a-127">Pour optimiser le coût des ressources cloud, vous devrez également configurer les bases de données de locataires dans un pool élastique, de manière à optimiser le rapport prix/performances d’un groupe de bases de données.</span><span class="sxs-lookup"><span data-stu-id="1d01a-127">To optimize the cost of cloud resources, you will also be provisioning the tenant databases into an elastic pool which allows you to optimize the price performance for a group of databases.</span></span> <span data-ttu-id="1d01a-128">Pour en savoir plus sur les autres modèles d’approvisionnement de bases de données, [cliquez ici](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="1d01a-128">To learn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="1d01a-129">Suivez ces étapes pour créer un serveur SQL et un pool élastique qui hébergeront toutes vos bases de données de locataires.</span><span class="sxs-lookup"><span data-stu-id="1d01a-129">Follow these steps to create a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="1d01a-130">Créez des variables pour stocker les valeurs qui seront utilisées dans la suite de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1d01a-130">Create variables to store values that will be used in the rest of the tutorial.</span></span> <span data-ttu-id="1d01a-131">Veillez à modifier la variable d’adresse IP pour inclure votre adresse IP</span><span class="sxs-lookup"><span data-stu-id="1d01a-131">Make sure to modify the IP address variable to include your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify to include your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="1d01a-132">Connectez-vous à Azure et créez un serveur SQL et un pool élastique</span><span class="sxs-lookup"><span data-stu-id="1d01a-132">Login to Azure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login to Azure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="1d01a-133">Création du catalogue de locataires</span><span class="sxs-lookup"><span data-stu-id="1d01a-133">Create tenant catalog</span></span> 

<span data-ttu-id="1d01a-134">Dans une application SaaS mutualisée, il est important de savoir où sont stockées les informations d’un locataire.</span><span class="sxs-lookup"><span data-stu-id="1d01a-134">In a multi-tenant SaaS application, it’s important to know where information for a tenant is stored.</span></span> <span data-ttu-id="1d01a-135">Ces informations sont généralement stockées dans une base de données de catalogue.</span><span class="sxs-lookup"><span data-stu-id="1d01a-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="1d01a-136">Cette base de données contient un mappage entre un locataire et une base de données dans laquelle sont stockées les données du locataire.</span><span class="sxs-lookup"><span data-stu-id="1d01a-136">The catalog database is used to hold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="1d01a-137">Le modèle de base s’applique aussi bien pour les bases de données mutualisées que pour les bases de données à un seul locataire.</span><span class="sxs-lookup"><span data-stu-id="1d01a-137">The basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="1d01a-138">Suivez ces étapes pour créer une base de données de catalogue pour l’exemple d’application SaaS.</span><span class="sxs-lookup"><span data-stu-id="1d01a-138">Follow these steps to create a catalog database for the sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table to track mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="1d01a-139">Approvisionnement de la base de données pour le « locataire 1 » et inscription de cette base dans le catalogue du locataire</span><span class="sxs-lookup"><span data-stu-id="1d01a-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="1d01a-140">Utilisez Powershell pour approvisionner une base de données pour un nouveau locataire appelé « locataire1 » et pour inscrire ce locataire dans le catalogue.</span><span class="sxs-lookup"><span data-stu-id="1d01a-140">Use Powershell to provision a database for a new tenant 'tenant1' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="1d01a-141">Approvisionnement de la base de données pour le « locataire 2 » et inscription de cette base dans le catalogue du locataire</span><span class="sxs-lookup"><span data-stu-id="1d01a-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="1d01a-142">Utilisez Powershell pour approvisionner une base de données pour un nouveau locataire appelé « locataire2 » et pour inscrire ce locataire dans le catalogue.</span><span class="sxs-lookup"><span data-stu-id="1d01a-142">Use Powershell to provision a database for a new tenant 'tenant2' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a><span data-ttu-id="1d01a-143">Configuration d’un exemple d’application Java</span><span class="sxs-lookup"><span data-stu-id="1d01a-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="1d01a-144">Créez un projet Maven.</span><span class="sxs-lookup"><span data-stu-id="1d01a-144">Create a maven project.</span></span> <span data-ttu-id="1d01a-145">Dans une fenêtre d’invite de commandes, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d01a-145">Type the following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="1d01a-146">Ajoutez la dépendance, le niveau de langage et l’option de génération pour prendre en charge les fichiers manifeste JARS dans le fichier pom.xml :</span><span class="sxs-lookup"><span data-stu-id="1d01a-146">Add this dependency, language level, and build option to support manifest files in jars to the pom.xml file:</span></span>
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
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

3. <span data-ttu-id="1d01a-147">Ajoutez le code suivant dans le fichier App.java :</span><span class="sxs-lookup"><span data-stu-id="1d01a-147">Add the following into the App.java file:</span></span>

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit the application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in the system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query the data that was previously inserted into the primary database from the geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. <span data-ttu-id="1d01a-148">Enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="1d01a-148">Save the file.</span></span>

5. <span data-ttu-id="1d01a-149">Accédez à la console de commandes et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d01a-149">Go to command console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="1d01a-150">Lorsque vous avez terminé, exécutez la commande suivante pour exécuter l’application :</span><span class="sxs-lookup"><span data-stu-id="1d01a-150">When finished, execute the following to run the application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="1d01a-151">Si l’exécution réussit, la sortie se présentera ainsi :</span><span class="sxs-lookup"><span data-stu-id="1d01a-151">The output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit the application

* List the tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="1d01a-152">Suppression du premier locataire</span><span class="sxs-lookup"><span data-stu-id="1d01a-152">Delete first tenant</span></span> 
<span data-ttu-id="1d01a-153">Utilisez PowerShell pour supprimer la base de données de locataires et l’entrée du catalogue correspondant au premier locataire.</span><span class="sxs-lookup"><span data-stu-id="1d01a-153">Use PowerShell to delete the tenant database and catalog entry for the first tenant.</span></span>

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

<span data-ttu-id="1d01a-154">Essayez de vous connecter au « locataire1 » à l’aide de l’application Java.</span><span class="sxs-lookup"><span data-stu-id="1d01a-154">Try connecting to 'tenant1' using the Java application.</span></span> <span data-ttu-id="1d01a-155">Vous obtiendrez une erreur indiquant que le client n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="1d01a-155">You will get an error stating that the tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d01a-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d01a-156">Next steps</span></span> 

<span data-ttu-id="1d01a-157">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1d01a-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1d01a-158">Configuration d’un environnement de base de données pour la prise en charge d’une application SaaS mutualisée, à l’aide du modèle « base de données par locataire »</span><span class="sxs-lookup"><span data-stu-id="1d01a-158">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="1d01a-159">Création d’un catalogue de locataires</span><span class="sxs-lookup"><span data-stu-id="1d01a-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="1d01a-160">Configuration d’une base de données de locataires et inscription de cette base de données dans le catalogue de locataires</span><span class="sxs-lookup"><span data-stu-id="1d01a-160">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="1d01a-161">Configuration d’un exemple d’application Java</span><span class="sxs-lookup"><span data-stu-id="1d01a-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="1d01a-162">Accès aux bases de données de locataires à l’aide d’une simple application console Java</span><span class="sxs-lookup"><span data-stu-id="1d01a-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="1d01a-163">Suppression d’un locataire</span><span class="sxs-lookup"><span data-stu-id="1d01a-163">Delete a tenant</span></span>

* <span data-ttu-id="1d01a-164">Pour obtenir des exemples de PowerShell pour les tâches courantes, consultez [Exemples PowerShell pour SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="1d01a-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="1d01a-165">Pour accéder à des modèles de conception pour les applications SaaS mutualisées, consultez les [Modèles de conception](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="1d01a-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="1d01a-166">Pour des exemples Java associés aux tâches courantes dans Azure, consultez le [Centre de développement Java](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="1d01a-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



