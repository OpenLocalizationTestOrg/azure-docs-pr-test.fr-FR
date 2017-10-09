---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Documents Microsoft
description: Interrogez SQL Data Warehouse avec Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Se connecter tooSQL Data Warehouse avec Visual Studio et SSDT
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Utilisez Visual Studio tooquery Azure SQL Data Warehouse dans quelques minutes. Cette méthode utilise l’extension de SQL Server Data Tools (SSDT) hello dans Visual Studio. 

## <a name="prerequisites"></a>Composants requis
toouse ce didacticiel, vous devez :

* Un entrepôt de données SQL existant. toocreate, consultez [créer un entrepôt de données SQL][Create a SQL Data Warehouse].
* SSDT pour Visual Studio. Si vous avez Visual Studio, vous en disposez probablement déjà. Pour obtenir des instructions et des options d’installation, consultez [Installation de Visual Studio et/ou SSDT][Installing Visual Studio and SSDT].
* Hello complet nom SQL server. toofind, consultez [connecter tooSQL Data Warehouse][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Se connecter tooyour SQL Data Warehouse
1. Ouvrir Visual Studio 2013 ou 2015
2. Ouvrez l’Explorateur d’objets SQL Server. toodo cette option, sélectionnez **vue** > **l’Explorateur d’objets SQL Server**.
   
    ![Explorateur d’objets SQL Server][1]
3. Cliquez sur hello **ajouter SQL Server** icône.
   
    ![Ajouter SQL Server][2]
4. Renseignez les champs hello dans la fenêtre de tooServer hello se connecter.
   
    ![Se connecter tooServer][3]
   
   * **Nom du serveur**. Entrez hello **nom du serveur** précédemment identifiés.
   * **Authentification**. Sélectionnez **Authentification SQL Server** ou **Authentification intégrée Active Directory**.
   * **Nom d’utilisateur** et **Mot de passe**. Entrez un nom d’utilisateur et mot de passe si l’authentification SQL Server a été sélectionnée plus haut.
   * Cliquez sur **Connecter**.
5. tooexplore, développez votre serveur SQL Azure. Vous pouvez afficher les bases de données hello associés avec le serveur de hello. Développez le nœud AdventureWorksDW toosee hello tables dans votre base de données exemple.
   
    ![Explorer AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a>2. Exécuter un exemple de requête
Maintenant qu’une connexion a été établie tooyour de base de données, nous allons écrire une requête.

1. Cliquez avec le bouton droit sur votre base de données dans l’Explorateur d’objets SQL Server.
2. Sélectionnez **Nouvelle requête**. Une nouvelle fenêtre de requête s’ouvre.
   
    ![Nouvelle requête][5]
3. Copiez cette requête TSQL dans une fenêtre de requête de hello :
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Exécutez une requête de hello. toodo, cliquez sur la flèche de hello vert ou utiliser hello suivant raccourci : `CTRL` + `SHIFT` + `E`.
   
    ![Exécuter une requête][6]
5. Examinez les résultats de la requête hello. Dans cet exemple, la table FactInternetSales de hello a 60398 lignes.
   
    ![Résultats de la requête][7]

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous pouvez vous connecter et de requête, essayez [visualisation des données hello avec Power BI][visualizing hello data with PowerBI].

tooconfigure votre environnement pour l’authentification Azure Active Directory, voir [authentifier tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
