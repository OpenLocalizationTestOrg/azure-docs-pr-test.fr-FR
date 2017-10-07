---
title: "VS Code : Se connecter et interroger des données dans Azure SQL Database | Microsoft Docs"
description: "Découvrez comment tooconnect tooSQL de base de données sur Azure à l’aide de Visual Studio Code. Ensuite, exécutez les instructions Transact-SQL (T-SQL) tooquery et modifier des données."
metacanonical: 
keywords: "connexion de base de données toosql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a>Base de données SQL Azure : Utilisation de Visual Studio Code tooconnect et interroger des données

[Code Visual Studio](https://code.visualstudio.com/docs) est un éditeur de code graphique pour macOS, Linux et Windows qui prend en charge les extensions, y compris hello [mssql extension](https://aka.ms/mssql-marketplace) pour l’interrogation de Microsoft SQL Server, base de données SQL Azure et SQL Data Warehouse. Ce démarrage rapide montre comment toouse Visual Studio Code tooconnect tooan Azure SQL database et puis tooquery d’instructions Transact-SQL d’utilisation, insérer, mettre à jour et supprimer des données dans la base de données hello.

## <a name="prerequisites"></a>Composants requis

Ce démarrage rapide utilise en tant que ses ressources de hello de point de départ créés dans une de ces Démarrages rapides :

- [Créer une base de données - Portail](sql-database-get-started-portal.md)
- [Créer une base de données - CLI](sql-database-get-started-cli.md)
- [Créer une base de données - PowerShell](sql-database-get-started-powershell.md)

Avant de commencer, assurez-vous que vous avez installé la version la plus récente de hello [Visual Studio Code](https://code.visualstudio.com/Download) et hello chargés [mssql extension](https://aka.ms/mssql-marketplace). Pour obtenir des instructions d’installation pour l’extension de mssql hello, consultez [installer VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) et [mssql pour le Code de Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

## <a name="configure-vs-code"></a>Configurer Visual Studio Code 

### <a name="mac-os"></a>**Mac OS**
Pour macOS, vous devez tooinstall OpenSSL qui est un prérequis pour DotNet Core que l’extension mssql utilise. Ouvrez votre terminal et entrez hello suivant de commandes tooinstall **brew** et **OpenSSL**. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**

Aucune configuration spéciale nécessaire.

### <a name="windows"></a>**Windows**

Aucune configuration spéciale nécessaire.

## <a name="sql-server-connection-information"></a>Informations de connexion SQL Server

Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database. Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page. 
3. Sur hello **vue d’ensemble** page de votre base de données, révision hello serveur nom complet comme dans hello suivant l’image. Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option.

   ![informations de connexion](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si vous avez oublié des informations de connexion hello pour votre serveur de base de données SQL Azure, accédez nom d’administrateur serveur page tooview hello toohello base de données SQL server et, si nécessaire, réinitialiser un mot de passe hello. 

## <a name="set-language-mode-toosql"></a>Set language mode tooSQL

Définir le mode de langage hello est défini trop**SQL** dans T-SQL IntelliSense et les commandes de Visual Studio Code tooenable mssql.

1. Ouvrez une nouvelle fenêtre Visual Studio Code. 

2. Cliquez sur **en texte brut** dans hello coin inférieur droit de la barre d’état hello.
3. Bonjour **mode langage sélectionnez** menu déroulant qui s’ouvre, tapez **SQL**, puis appuyez sur **entrée** tooset hello langage mode tooSQL. 

   ![Mode de langage SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a>Connexion de base de données tooyour

Utilisez Visual Studio Code tooestablish un serveur de base de données SQL Azure de tooyour de connexion.

> [!IMPORTANT]
> Avant de poursuivre, assurez-vous que votre serveur et votre base de données sont prêts, et que vous disposez de vos informations de connexion. Une fois que vous commencez à entrer des informations de profil de connexion hello, si vous modifiez le focus à partir de Code Visual Studio, vous devez toorestart création de profil de connexion hello.
>

1. Dans le Code de Visual Studio, appuyez sur **CTRL + MAJ + P** (ou **F1**) tooopen hello Palette de commandes.

2. Tapez **sqlcon**, puis appuyez sur **ENTRÉE**.

3. Appuyez sur **entrée** tooselect **créer un profil de connexion**. Cela crée un profil de connexion à votre instance SQL Server.

4. Suivre les propriétés de connexion hello invites toospecify hello hello nouveau profil de connexion. Après avoir spécifié de chaque valeur, appuyez sur **entrée** toocontinue. 

   | Paramètre       | Valeur suggérée | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nom du serveur | nom du serveur complet Hello | Hello nom doit être semblable à celui-ci : **mynewserver20170313.database.windows.net**. |
   | **Nom de la base de données** | mySampleDatabase | nom de Hello de hello de base de données toowhich tooconnect. |
   | **Authentification** | Connexion SQL| L’authentification SQL est hello seul type d’authentification que nous avons configuré dans ce didacticiel. |
   | **Nom d'utilisateur** | compte d’administrateur serveur Hello | Il s’agit de compte hello que vous avez spécifié lors de la création du serveur de hello. |
   | **Mot de passe (connexion SQL)** | mot de passe Hello pour votre compte d’administrateur de serveur | Il s’agit d’un mot de passe hello que vous avez spécifié lors de la création du serveur de hello. |
   | **Enregistrer le mot de passe ?** | Oui ou Non | Sélectionnez Oui si vous ne souhaitez pas un mot de passe tooenter hello chaque fois. |
   | **Entrez un nom pour ce profil** | Nom de profil de connexion, par exemple **mySampleDatabase** | Un nom de profil enregistré permet d’accélérer votre connexion lors des connexions suivantes. | 

5. Hello de presse **ÉCHAP** tooclose clé hello info message qui vous informe que le profil de hello est créé et connecté.

6. Vérifiez votre connexion dans la barre d’état hello.

   ![État de la connexion](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a>Données de requête

Tooquery pour les produits de 20 premiers hello de code suivant de hello d’utilisation par catégorie à l’aide de hello [sélectionnez](https://msdn.microsoft.com/library/ms189499.aspx) instruction Transact-SQL.

1. Bonjour **éditeur** fenêtre, entrez hello suivant la requête dans la fenêtre de requête vide hello :

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. Appuyez sur **CTRL + MAJ + E** tooretrieve des données à partir des tables Product et ProductCategory de hello.

    ![Interroger](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a>Insertion des données

Utilisez hello de code suivant tooinsert un nouveau produit dans table de SalesLT.Product hello à l’aide de hello [insérer](https://msdn.microsoft.com/library/ms174335.aspx) instruction Transact-SQL.

1. Bonjour **éditeur** fenêtre, supprimer la requête précédente de hello et entrez hello suivant la requête :

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. Appuyez sur **CTRL + MAJ + E** tooinsert une nouvelle ligne dans la table Product de hello.

## <a name="update-data"></a>Mettre à jour des données

Tooupdate hello produit que vous avez ajouté précédemment à l’aide de hello de code suivant de hello utilisation [mise à jour](https://msdn.microsoft.com/library/ms177523.aspx) instruction Transact-SQL.

1.  Bonjour **éditeur** fenêtre, supprimer la requête précédente de hello et entrez hello suivant la requête :

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Appuyez sur **CTRL + MAJ + E** ligne spécifiée de tooupdate hello dans la table Product de hello.

## <a name="delete-data"></a>Suppression de données

Toodelete hello produit que vous avez ajouté précédemment à l’aide de hello de code suivant de hello utilisation [supprimer](https://msdn.microsoft.com/library/ms189835.aspx) instruction Transact-SQL.

1. Bonjour **éditeur** fenêtre, supprimer la requête précédente de hello et entrez hello suivant la requête :

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Appuyez sur **CTRL + MAJ + E** ligne spécifiée de toodelete hello dans la table Product de hello.

## <a name="next-steps"></a>Étapes suivantes

- tooconnect et la requête à l’aide de SQL Server Management Studio, consultez [se connecter et requête avec SSMS](sql-database-connect-query-ssms.md).
- Pour lire un article du magazine MSDN sur l’utilisation de Visual Studio Code, consultez le [billet de blog Créer un IDE de base de données avec une extension MSSQL](https://msdn.microsoft.com/magazine/mt809115).
