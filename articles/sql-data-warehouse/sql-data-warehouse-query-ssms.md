---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Documents Microsoft
description: "Utilisez SQL Server Management Studio (SSMS) tooconnect tooand requête Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>Se connecter tooSQL l’entrepôt de données avec SQL Server Management Studio (SSMS)
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Utilisez SQL Server Management Studio (SSMS) tooconnect tooand requête Azure SQL Data Warehouse. 

## <a name="prerequisites"></a>Composants requis
toouse ce didacticiel, vous devez :

* Un entrepôt de données SQL existant. toocreate, consultez [créer un entrepôt de données SQL][Create a SQL Data Warehouse].
* SQL Server Management Studio (SSMS) installé. [Installez SSMS][Install SSMS] gratuitement si vous ne l’avez pas déjà.
* Hello complet nom SQL server. toofind, consultez [connecter tooSQL Data Warehouse][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Se connecter tooyour SQL Data Warehouse
1. Ouvrez SSMS.
2. Ouvrez l’Explorateur d'objets. toodo cette option, sélectionnez **fichier** > **connecter l’Explorateur d’objets**.
   
    ![Explorateur d’objets SQL Server][1]
3. Renseignez les champs hello dans la fenêtre de tooServer hello se connecter.
   
    ![Se connecter tooServer][2]
   
   * **Nom du serveur**. Entrez hello **nom du serveur** précédemment identifiés.
   * **Authentification**. Sélectionnez **Authentification SQL Server** ou **Authentification intégrée Active Directory**.
   * **Nom d’utilisateur** et **Mot de passe**. Entrez un nom d’utilisateur et mot de passe si l’authentification SQL Server a été sélectionnée plus haut.
   * Cliquez sur **Connecter**.
4. tooexplore, développez votre serveur SQL Azure. Vous pouvez afficher les bases de données hello associés avec le serveur de hello. Développez le nœud AdventureWorksDW toosee hello tables dans votre base de données exemple.
   
    ![Explorer AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a>2. Exécuter un exemple de requête
Maintenant qu’une connexion a été établie tooyour de base de données, nous allons écrire une requête.

1. Cliquez avec le bouton droit sur votre base de données dans l’Explorateur d’objets SQL Server.
2. Sélectionnez **Nouvelle requête**. Une nouvelle fenêtre de requête s’ouvre.
   
    ![Nouvelle requête][4]
3. Copiez cette requête TSQL dans une fenêtre de requête de hello :
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Exécutez une requête de hello. toodo, cliquez sur `Execute` ou utilisez hello suit raccourci : `F5`.
   
    ![Exécuter une requête][5]
5. Examinez les résultats de la requête hello. Dans cet exemple, la table FactInternetSales de hello a 60398 lignes.
   
    ![Résultats de la requête][6]

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous pouvez vous connecter et de requête, essayez [visualisation des données hello avec Power BI][visualizing hello data with PowerBI].

tooconfigure votre environnement pour l’authentification Azure Active Directory, voir [authentifier tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
