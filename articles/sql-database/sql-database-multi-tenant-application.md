---
title: "application de SaaS mutualisée aaaImplement avec la base de données SQL Azure | Documents Microsoft"
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
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="6f229-103">Déployer une application SaaS mutualisée à l’aide d’Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6f229-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="6f229-104">Une application mutualisée est une application hébergée dans un environnement cloud et hello même ensemble de services toohundreds plusieurs milliers de clients qui ne pas partager ou afficher les données de l’autre.</span><span class="sxs-lookup"><span data-stu-id="6f229-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="6f229-105">Un exemple est une application SaaS qui fournit des tootenants de services dans un environnement hébergé dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="6f229-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="6f229-106">Ce modèle isole les données de salutation pour chaque client et optimise distribution hello de ressources pour un coût.</span><span class="sxs-lookup"><span data-stu-id="6f229-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="6f229-107">Ce didacticiel montre comment toocreate une application de SaaS mutualisée à l’aide de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6f229-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="6f229-108">Ce didacticiel vous apprendra à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6f229-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="6f229-109">Configurer un toosupport d’environnement de base de données d’une application SaaS mutualisée, à l’aide du modèle de base de données pour chaque locataire hello</span><span class="sxs-lookup"><span data-stu-id="6f229-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="6f229-110">Création d’un catalogue de locataires</span><span class="sxs-lookup"><span data-stu-id="6f229-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="6f229-111">Configurer une base de données client et l’inscrire dans le catalogue du locataire hello</span><span class="sxs-lookup"><span data-stu-id="6f229-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="6f229-112">Configuration d’un exemple d’application Java</span><span class="sxs-lookup"><span data-stu-id="6f229-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="6f229-113">Accès aux bases de données de locataires à l’aide d’une simple application console Java</span><span class="sxs-lookup"><span data-stu-id="6f229-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="6f229-114">Suppression d’un locataire</span><span class="sxs-lookup"><span data-stu-id="6f229-114">Delete a tenant</span></span>

<span data-ttu-id="6f229-115">Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="6f229-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f229-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6f229-116">Prerequisites</span></span>

<span data-ttu-id="6f229-117">toocomplete ce didacticiel, assurez-vous que vous avez :</span><span class="sxs-lookup"><span data-stu-id="6f229-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="6f229-118">Version la plus récente installée hello de PowerShell et hello [dernier Kit de développement Azure PowerShell](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="6f229-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="6f229-119">Version la plus récente installée hello de [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="6f229-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="6f229-120">L’installation de SQL Server Management Studio installe également la version la plus récente hello de SQLPackage, un utilitaire de ligne de commande qui peut être utilisé tooautomate un éventail de tâches de développement de base de données.</span><span class="sxs-lookup"><span data-stu-id="6f229-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="6f229-121">Hello installé [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) et hello [dernier Kit de développement JAVA (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6f229-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="6f229-122">[Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="6f229-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="6f229-123">Maven servira toohelp gérer les dépendances, créer, tester et exécuter l’exemple de projet Java de hello</span><span class="sxs-lookup"><span data-stu-id="6f229-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="6f229-124">Configuration de l’environnement des données</span><span class="sxs-lookup"><span data-stu-id="6f229-124">Set up data environment</span></span>

<span data-ttu-id="6f229-125">Vous allez approvisionner une base de données par locataire.</span><span class="sxs-lookup"><span data-stu-id="6f229-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="6f229-126">modèle de base de données pour chaque locataire Hello fournit hello plus haut degré d’isolation entre les clients, avec un faible coût de DevOps.</span><span class="sxs-lookup"><span data-stu-id="6f229-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="6f229-127">coût de hello toooptimize des ressources de cloud computing, sera également approvisionner les bases de données clientes hello dans un pool élastique, qui vous permet de toooptimize hello prix/performances pour un groupe de bases de données.</span><span class="sxs-lookup"><span data-stu-id="6f229-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="6f229-128">toolearn sur une autre base de données de configuration de modèles [ici](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="6f229-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="6f229-129">Suivez ces étapes toocreate un serveur SQL server et un pool élastique qui va héberger toutes vos bases de données client.</span><span class="sxs-lookup"><span data-stu-id="6f229-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="6f229-130">Créer des variables les valeurs toostore qui seront utilisés dans le reste de hello du didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="6f229-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="6f229-131">Assurez-vous que toomodify hello IP adresse variable tooinclude votre adresse IP</span><span class="sxs-lookup"><span data-stu-id="6f229-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="6f229-132">Connexion tooAzure et créer un pool élastique et le serveur SQL</span><span class="sxs-lookup"><span data-stu-id="6f229-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login tooAzure 
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="6f229-133">Création du catalogue de locataires</span><span class="sxs-lookup"><span data-stu-id="6f229-133">Create tenant catalog</span></span> 

<span data-ttu-id="6f229-134">Dans une application SaaS mutualisée, il est important tooknow où sont stockées les informations pour un client.</span><span class="sxs-lookup"><span data-stu-id="6f229-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="6f229-135">Ces informations sont généralement stockées dans une base de données de catalogue.</span><span class="sxs-lookup"><span data-stu-id="6f229-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="6f229-136">base de données de catalogue Hello est toohold utilisé un mappage entre un client et une base de données dans lequel sont stockées les données du locataire.</span><span class="sxs-lookup"><span data-stu-id="6f229-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="6f229-137">modèle de base Hello s’applique si une architecture mutualisée ou une base de données locataire unique est utilisé.</span><span class="sxs-lookup"><span data-stu-id="6f229-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="6f229-138">Suivez ces étapes de toocreate une base de données de catalogue pour une application SaaS d’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="6f229-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="6f229-139">Approvisionnement de la base de données pour le « locataire 1 » et inscription de cette base dans le catalogue du locataire</span><span class="sxs-lookup"><span data-stu-id="6f229-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="6f229-140">Utilisez Powershell tooprovision une base de données pour un nouveau client 'un locataire 1' et enregistrer ce client dans le catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="6f229-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register 'tenant1' in hello tenant catalog 
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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="6f229-141">Approvisionnement de la base de données pour le « locataire 2 » et inscription de cette base dans le catalogue du locataire</span><span class="sxs-lookup"><span data-stu-id="6f229-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="6f229-142">Utilisez Powershell tooprovision une base de données pour un nouveau client 'tenant2' et enregistrer ce client dans le catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="6f229-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register tenant 'tenant2' in hello tenant catalog 
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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="6f229-143">Configuration d’un exemple d’application Java</span><span class="sxs-lookup"><span data-stu-id="6f229-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="6f229-144">Créez un projet Maven.</span><span class="sxs-lookup"><span data-stu-id="6f229-144">Create a maven project.</span></span> <span data-ttu-id="6f229-145">Tapez hello qui suit dans une fenêtre d’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="6f229-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="6f229-146">Ajouter cette dépendance, le niveau de langage et générer des fichiers manifeste dans le fichier de fichiers JAR toohello pom.xml option toosupport :</span><span class="sxs-lookup"><span data-stu-id="6f229-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
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

3. <span data-ttu-id="6f229-147">Ajoutez dans le fichier de App.java hello hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="6f229-147">Add hello following into hello App.java file:</span></span>

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
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
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
   
   // List all tenants that currently exist in hello system
   
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
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
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

4. <span data-ttu-id="6f229-148">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="6f229-148">Save hello file.</span></span>

5. <span data-ttu-id="6f229-149">Toocommand console et exécutez</span><span class="sxs-lookup"><span data-stu-id="6f229-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="6f229-150">Lorsque vous avez terminé, exécutez hello après application de hello toorun</span><span class="sxs-lookup"><span data-stu-id="6f229-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="6f229-151">Si elle s’exécute avec succès, sortie de Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="6f229-151">hello output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="6f229-152">Suppression du premier locataire</span><span class="sxs-lookup"><span data-stu-id="6f229-152">Delete first tenant</span></span> 
<span data-ttu-id="6f229-153">Utilisez PowerShell toodelete hello client de base de données et le catalogue d’entrée pour le client de première hello.</span><span class="sxs-lookup"><span data-stu-id="6f229-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

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

<span data-ttu-id="6f229-154">Essayez de vous connecter à l’aide de 'un locataire 1' trop hello des application Java.</span><span class="sxs-lookup"><span data-stu-id="6f229-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="6f229-155">Vous obtiendrez une erreur indiquant que ce client hello n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="6f229-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f229-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6f229-156">Next steps</span></span> 

<span data-ttu-id="6f229-157">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6f229-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="6f229-158">Configurer un toosupport d’environnement de base de données d’une application SaaS mutualisée, à l’aide du modèle de base de données pour chaque locataire hello</span><span class="sxs-lookup"><span data-stu-id="6f229-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="6f229-159">Création d’un catalogue de locataires</span><span class="sxs-lookup"><span data-stu-id="6f229-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="6f229-160">Configurer une base de données client et l’inscrire dans le catalogue du locataire hello</span><span class="sxs-lookup"><span data-stu-id="6f229-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="6f229-161">Configuration d’un exemple d’application Java</span><span class="sxs-lookup"><span data-stu-id="6f229-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="6f229-162">Accès aux bases de données de locataires à l’aide d’une simple application console Java</span><span class="sxs-lookup"><span data-stu-id="6f229-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="6f229-163">Suppression d’un locataire</span><span class="sxs-lookup"><span data-stu-id="6f229-163">Delete a tenant</span></span>

* <span data-ttu-id="6f229-164">Pour obtenir des exemples de PowerShell pour les tâches courantes, consultez [Exemples PowerShell pour SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="6f229-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="6f229-165">Pour accéder à des modèles de conception pour les applications SaaS mutualisées, consultez les [Modèles de conception](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="6f229-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="6f229-166">Pour des exemples Java associés aux tâches courantes dans Azure, consultez le [Centre de développement Java](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="6f229-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



