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
# <a name="implement-a-geo-distributed-database"></a>Implémenter une base de données géo-distribuée

Dans ce didacticiel, vous configurez une base de données SQL Azure et d’une application de la région de basculement tooa à distance, ensuite Testez votre plan de basculement. Vous allez apprendre à effectuer les actions suivantes : 

> [!div class="checklist"]
> * Créer des utilisateurs de base de données et leur accorder des autorisations
> * Configurer une règle de pare-feu au niveau de la base de données
> * Créer un [groupe de basculement de géoréplication](sql-database-geo-replication-overview.md)
> * Créer et compiler un tooquery d’application Java une base de données SQL Azure
> * Effectuer une simulation de récupération d'urgence

Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.


## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, assurez-vous que hello est suivant des conditions préalables requises sont effectuées :

- Hello installé dernières [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs). 
- Une base de données SQL Azure est installée. Ce didacticiel utilise la base de données AdventureWorksLT hello avec un nom de **mySampleDatabase** à partir d’un de ces Démarrages rapides :

   - [Créer une base de données - Portail](sql-database-get-started-portal.md)
   - [Créer une base de données - CLI](sql-database-get-started-cli.md)
   - [Créer une base de données - PowerShell](sql-database-get-started-powershell.md)

- A identifié un tooexecute méthode SQL scripts contre votre base de données, vous pouvez utiliser une des hello suivant des outils de requête :
   - éditeur de requête Hello Bonjour [portail Azure](https://portal.azure.com). Pour plus d’informations sur l’utilisation de l’éditeur de requête hello Bonjour portail Azure, consultez [se connecter et requête à l’aide de l’éditeur de requête](sql-database-get-started-portal.md#query-the-sql-database).
   - version la plus récente de Hello [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), qui est un environnement intégré pour la gestion d’une infrastructure SQL, à partir de SQL Server tooSQL de base de données pour Microsoft Windows.
   - version la plus récente de Hello [Visual Studio Code](https://code.visualstudio.com/docs), qui est un éditeur de code graphique pour Linux, Mac OS, et que Windows qui prend en charge les extensions, y compris hello [mssql extension](https://aka.ms/mssql-marketplace) pour l’interrogation de Microsoft SQL Server , Base de données SQL azure et SQL Data Warehouse. Pour plus d’informations sur l’utilisation de cet outil avec la base de données SQL Azure, consultez l’article [Utilisez VS Code pour vous connecter et interroger des données](sql-database-connect-query-vscode.md). 

## <a name="create-database-users-and-grant-permissions"></a>Créer des utilisateurs de base de données et accorder des autorisations

Se connecter tooyour de base de données et créer des comptes d’utilisateur à l’aide de hello suivant des outils de requête :

- éditeur de requête Hello Bonjour portail Azure
- SQL Server Management Studio
- Visual Studio Code

Ces comptes d’utilisateur répliquent automatiquement le serveur secondaire de tooyour (et être synchronisés). toouse SQL Server Management Studio ou Visual Studio Code, vous devrez peut-être tooconfigure une règle de pare-feu si vous vous connectez à partir d’un client à une adresse IP pour laquelle vous n'avez pas encore configuré un pare-feu. Pour des instructions plus détaillées, consultez la section [Créer une règle de pare-feu au niveau du serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).

- Dans une fenêtre de requête, exécutez hello suivant requête toocreate deux comptes d’utilisateur dans votre base de données. Ce script accorde **db_owner** autorisations toohello **app_admin** compte et accorde **sélectionnez** et **mise à jour** toohello d’autorisations **app_user** compte. 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a>Créer un pare-feu au niveau de la base de données

Créez une [règle de pare-feu au niveau de la base de données](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) pour votre base de données SQL. Cette règle de pare-feu de niveau base de données réplique automatiquement toohello serveur secondaire que vous créez dans ce didacticiel. Pour plus de simplicité (dans ce didacticiel), utilisez hello une adresse IP publique de l’ordinateur hello sur lequel vous effectuez les étapes hello dans ce didacticiel. adresse IP de toodetermine hello utilisé pour la règle de pare-feu de niveau serveur hello pour votre ordinateur actuel, consultez [création d’un pare-feu au niveau du serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).  

- Dans la fenêtre de requête ouverte, remplacez les requêtes précédentes hello hello suivant la requête, en remplaçant les adresses IP hello avec hello adresses IP appropriées pour votre environnement.  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a>Créer un groupe de basculement automatique de géoréplication active 

À l’aide d’Azure PowerShell, créer un [groupe de basculement automatique de géo-réplication active](sql-database-geo-replication-overview.md) entre votre serveur SQL Azure et hello nouvelle existants vides serveur SQL Azure dans une région Azure, et puis ajoutez votre groupe de basculement toohello exemple de base de données.

> [!IMPORTANT]
> Ces commandes cmdlets nécessitent Azure PowerShell 4.0. [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. Remplir les variables pour vos scripts PowerShell à l’aide des valeurs de hello pour votre serveur existant et de la base de données exemple et fournir une valeur unique pour le nom de groupe de basculement.

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

2. Créez un serveur de sauvegarde vide dans votre région de basculement.

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. Créer un groupe de basculement entre deux serveurs de hello.

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

4. Ajouter à votre groupe de basculement de toohello de base de données.

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

## <a name="install-java-software"></a>Installer le logiciel Java

étapes de Hello dans cette section supposent que vous êtes familiarisé avec le développement à l’aide de Java et tooworking nouvelle base de données SQL Azure. 

### <a name="mac-os"></a>**Mac OS**
Ouvrez votre terminal et accédez répertoire tooa où vous prévoyez de créer un projet Java. Installer **brew** et **Maven** en entrant hello suivant de commandes : 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

Pour obtenir des instructions détaillées sur l’installation et configuration d’environnement Java et Maven, accédez hello [générer une application à l’aide de SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), sélectionnez **Java**, sélectionnez **MacOS**, puis suivez Hello instructions détaillées pour la configuration de Java et Maven à l’étape 1.2 et 1.3.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
Ouvrez votre terminal et accédez répertoire tooa où vous prévoyez de créer un projet Java. Installer **Maven** en entrant hello suivant de commandes :

```bash
sudo apt-get install maven
```

Pour obtenir des instructions détaillées sur l’installation et configuration d’environnement Java et Maven, accédez hello [générer une application à l’aide de SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), sélectionnez **Java**, sélectionnez **Ubuntu**, puis suivez Hello instructions détaillées pour la configuration de Java et Maven à l’étape 1.2, 1.3 et 1.4.

### <a name="windows"></a>**Windows**
Installer [Maven](https://maven.apache.org/download.cgi) à l’aide du programme d’installation officielle de hello. Utilisez Maven toohelp gérer les dépendances, créer, tester et exécuter votre projet Java. Pour obtenir des instructions détaillées sur l’installation et configuration d’environnement Java et Maven, accédez hello [générer une application à l’aide de SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), sélectionnez **Java**, sélectionnez Windows, puis suivez hello des instructions détaillées de configuration de Java et Maven à l’étape 1.2 et 1.3.

## <a name="create-sqldbsample-project"></a>Créer le projet SqlDbSample

1. Dans la console de commande hello (par exemple, un interpréteur de commandes), créez un projet de Maven. 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. Saisissez **Y** et cliquez sur **Entrée**.
3. Remplacez les répertoires dans votre projet nouvellement créé.

   ```bash
   cd SqlDbSamples
   ```

4. À l’aide de votre éditeur favori, ouvrir le fichier de pom.xml hello dans votre dossier de projet. 

5. Ajouter hello pilote JDBC Microsoft pour le projet de SQL Server dépendance tooyour Maven en ouvrant l’éditeur de texte et copier- coller hello lignes suivantes dans votre fichier pom.xml. Ne pas remplacer les valeurs existantes hello préremplies dans le fichier de hello. Hello dépendance JDBC doit être collé dans hello section « dépendances » supérieure ().   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. Spécifiez hello version de Java toocompile hello projet contre en ajoutant des hello suivant la section « Propriétés » dans le fichier de pom.xml hello après la section « dépendances » de hello. 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. Ajouter suivant de hello « build » section dans le fichier de pom.xml hello après hello « propriétés » section toosupport fichiers manifeste dans des fichiers JAR.       

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
8. Enregistrez et fermez le fichier de pom.xml hello.
9. Ouvrir le fichier de App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) et remplacez contenu de hello par hello suivant le contenu. Remplacez le nom de groupe de basculement hello par nom hello pour votre groupe de basculement. Si vous avez modifié les valeurs hello pour le nom de base de données hello, un utilisateur ou mot de passe, modifiez ces valeurs.

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
6. Enregistrez et fermez le fichier de App.java hello.

## <a name="compile-and-run-hello-sqldbsample-project"></a>Compilez et exécutez hello SqlDbSample projet

1. Dans la console de commande hello, exécutez toofollowing commande.

   ```bash
   mvn package
   ```
2. Lorsque vous avez terminé, exécutez hello suivant commande toorun hello application (il s’exécute pendant environ 1 heure, sauf si vous l’arrêtez manuellement) :

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a>Effectuer une simulation de récupération d’urgence

1. Appelez le basculement manuel du groupe de basculement. 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. Observer les résultats de l’application hello pendant le basculement. Certaines insertions échouent pendant que hello cache DNS actualise.     

3. Découvrez le rôle que votre serveur de récupération d’urgence exécute.

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. Effectuez une restauration automatique.

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. Observer les résultats de l’application hello lors de la restauration automatique. Certaines insertions échouent pendant que hello cache DNS actualise.     

6. Découvrez le rôle que votre serveur de récupération d’urgence exécute.

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a>Étapes suivantes 

Pour plus d’informations, voir l’article [Groupes de basculement et géoréplication active](sql-database-geo-replication-overview.md).
