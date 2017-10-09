---
title: "aaaVisualize de données SQL Data Warehouse avec Power BI Microsoft Azure"
description: "Visualiser les données SQL Data Warehouse avec Power BI"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Visualiser des données avec Power BI
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Ce didacticiel vous montre comment toouse Power BI tooconnect tooSQL l’entrepôt de données et créer quelques visualisations de base.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>Composants requis
toostep dans ce didacticiel, vous devez :

* Un entrepôt de données SQL est préchargé avec une base de données AdventureWorksDW hello. tooprovision, consultez [créer un entrepôt de données SQL] [ Create a SQL Data Warehouse] et choisissez les données d’exemple hello tooload. Si vous disposez déjà d’un entrepôt de données, mais sans disposer d’exemples de données, vous pouvez [charger manuellement des exemples de données][load sample data manually].

## <a name="1-connect-tooyour-database"></a>1. Connexion de base de données tooyour
tooopen Power BI et de la connexion de base de données AdventureWorksDW tooyour :

1. L’authentification à hello [portail Azure][Azure portal].
2. Cliquez sur **Bases de données SQL** et choisissez votre base de données SQL Data Warehouse AdventureWorks.
   
    ![Recherche de votre base de données][1]
3. Cliquez sur le bouton « Ouvrir dans Power BI » de hello.
   
    ![Bouton Power BI][2]
4. Vous devez maintenant voir la page de connexion SQL Data Warehouse hello afficher l’adresse web de votre base de données. Cliquez sur Suivant.
   
    ![Connexion Power BI][3]
5. Entrez votre nom d’utilisateur du serveur SQL Azure et votre mot de passe et vous serez la base de données SQL Data Warehouse tooyour totalement connecté.
   
    ![Se connecter à Power BI][4]
6. Une fois que vous avez connecté à Power BI, cliquez sur hello jeu de données AdventureWorksDW sur le panneau gauche de hello. Base de données hello s’ouvre.
   
    ![Ouvrir AdventureWorksDW Power BI][5]

## <a name="2-create-a-report"></a>2. Créer un rapport
Vous est désormais prêt toouse Power BI tooanalyze vos exemples de données AdventureWorksDW. analyse de hello tooperform, AdventureWorksDW a une vue appelée AggregateSales. Cette vue contient quelques exemples de métriques clés de hello pour l’analyse des ventes de la société de hello hello.

1. toocreate un mappage de montant des ventes en fonction de code toopostal, dans le volet de droite de champs de hello, cliquez sur hello AggregateSales vue tooexpand il. Cliquez sur hello PostalCode et SalesAmount tooselect de colonnes les.
   
    ![Sélection d’AggregateSales Power BI][6]
   
    Power BI reconnaît automatiquement ces données comme des données géographiques et les intègre dans une carte.
   
    ![Carte Power BI][7]
2. Cette étape crée un graphique à barres qui affiche le montant des ventes en fonction du revenu client. toocreate cette toohello accédez développé AggregateSales vue. Cliquez sur le champ SalesAmount de hello. Faites glisser hello le revenu champ toohello gauche et déposez-le dans l’axe.
   
    ![Axe de sélection Power BI][8]
   
    Nous avons déplacé le graphique à barres hello sur hello gauche.
   
    ![Barre Power BI][9]
3. Cette étape crée un graphique en courbes qui indique le montant des ventes par date de commande. toocreate cette toohello accédez développé AggregateSales vue. Cliquez sur SalesAmount et OrderDate. Dans la colonne de visualisations hello cliquez sur l’icône de graphique en courbes hello ; Il s’agit d’icône du premier hello hello deuxième ligne sous visualisations.
   
    ![Sélection de graphique en courbes Power BI][10]
   
    Vous avez maintenant un rapport qui affiche les trois différentes visualisations de données de hello.
   
    ![Ligne Power BI][11]

Vous pouvez enregistrer votre progression à tout moment en cliquant sur **Fichier**, puis en sélectionnant **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que nous vous avons donné certains toowarm temps avec les données d’exemple hello, consultez Comment trop[développer][develop], [charger][load], ou [ migrer][migrate]. Ou examiner hello [site Web de Power BI][Power BI website].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
