---
title: "aaaUse Java tooquery base de données SQL Azure | Documents Microsoft"
description: "Cette rubrique vous montre comment toouse Java toocreate un programme qui se connecte tooan base de données SQL Azure et requête à l’aide d’instructions Transact-SQL."
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: f014edbe38ca0e7b6e43f4eb4d2e53d3561bf3e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-java-tooquery-an-azure-sql-database"></a>Utiliser Java tooquery une base de données SQL Azure

Ce démarrage rapide montre comment toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan SQL Azure de base de données et ensuite utiliser les données de tooquery d’instructions Transact-SQL.

## <a name="prerequisites"></a>Composants requis

toocomplete rapide de ce didacticiel de démarrage, assurez-vous que vous avez hello suivant des conditions préalables :

- base de données SQL Azure. Ce démarrage rapide utilise des ressources hello créés dans une de ces Démarrages rapides : 

   - [Créer une base de données - Portail](sql-database-get-started-portal.md)
   - [Créer une base de données - CLI](sql-database-get-started-cli.md)
   - [Créer une base de données - PowerShell](sql-database-get-started-powershell.md)

- A [règle de pare-feu de niveau serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de hello d’ordinateur de hello que vous utilisez pour ce didacticiel de démarrage rapide.

- Vous avez installé Java et les logiciels connexes pour votre système d’exploitation.

    - **MacOS** : installez Homebrew et Java, puis Maven. Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).
    - **Ubuntu**: installation hello Kit de développement Java et Maven. Consultez les [étapes 1.2, 1.3 et 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).
    - **Windows**: installation Bonjour Kit de développement Java et Maven. Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).    

## <a name="sql-server-connection-information"></a>Informations de connexion SQL Server

Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database. Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page. 
3. Sur hello **vue d’ensemble** pour votre base de données, vérifiez le nom du serveur complet hello comme indiqué dans hello suivant image : vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si vous oubliez vos informations de connexion du serveur, accédez à nom d’administrateur serveur page tooview hello toohello base de données SQL server.  Si nécessaire, le mot de passe réinitialisé hello.     

## <a name="create-maven-project-and-dependencies"></a>**Création d’un projet Maven et de dépendances**
1. À partir de hello Terminal Server, créez un nouveau projet Maven nommé **sqltest**. 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. Quand vous y êtes invité, entrez **Y**.
3. Remplacez le répertoire trop**sqltest** et ouvrez ***pom.xml*** avec votre éditeur de texte.  Ajouter hello **Microsoft JDBC Driver pour SQL Server** hello des dépendances du projet tooyour à l’aide de code suivant :

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. Également dans ***pom.xml***, ajouter hello suivant projet tooyour de propriétés.  Si vous n’avez pas une section de propriétés, vous pouvez l’ajouter après les dépendances hello.

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. Enregistrez et fermez le fichier ***pom.xml***.

## <a name="insert-code-tooquery-sql-database"></a>Insérer la base de données SQL de code tooquery

1. Vous disposez déjà d’un fichier appelé ***App.java*** dans votre projet Maven situé à cet emplacement : \sqltest\src\main\java\com\sqlsamples\App.Java

2. Ouvrez le fichier de hello et de remplacer son contenu par hello suit le code et ajoutez hello les valeurs appropriées pour votre serveur, une base de données, un utilisateur et un mot de passe.

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect toodatabase
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-hello-code"></a>Exécuter le code de hello

1. À l’invite de commandes hello exécutez hello suivant de commandes :

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. Vérifiez que hello supérieur des 20 lignes sont retournées, puis fermez la fenêtre de l’application hello.


## <a name="next-steps"></a>Étapes suivantes
- [Concevoir votre première base de données SQL Azure](sql-database-design-first-database.md)
- [Pilote JDBC Microsoft pour SQL Server](https://github.com/microsoft/mssql-jdbc)
- [Report issues/ask questions](https://github.com/microsoft/mssql-jdbc/issues) (Signaler des problèmes/poser des questions)

