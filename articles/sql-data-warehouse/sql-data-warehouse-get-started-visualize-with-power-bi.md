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
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="0f227-103">Visualiser des données avec Power BI</span><span class="sxs-lookup"><span data-stu-id="0f227-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f227-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="0f227-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="0f227-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0f227-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="0f227-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f227-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="0f227-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="0f227-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="0f227-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="0f227-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="0f227-109">Ce didacticiel vous montre comment toouse Power BI tooconnect tooSQL l’entrepôt de données et créer quelques visualisations de base.</span><span class="sxs-lookup"><span data-stu-id="0f227-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0f227-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0f227-110">Prerequisites</span></span>
<span data-ttu-id="0f227-111">toostep dans ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="0f227-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="0f227-112">Un entrepôt de données SQL est préchargé avec une base de données AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="0f227-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="0f227-113">tooprovision, consultez [créer un entrepôt de données SQL] [ Create a SQL Data Warehouse] et choisissez les données d’exemple hello tooload.</span><span class="sxs-lookup"><span data-stu-id="0f227-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="0f227-114">Si vous disposez déjà d’un entrepôt de données, mais sans disposer d’exemples de données, vous pouvez [charger manuellement des exemples de données][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="0f227-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="0f227-115">1. Connexion de base de données tooyour</span><span class="sxs-lookup"><span data-stu-id="0f227-115">1. Connect tooyour database</span></span>
<span data-ttu-id="0f227-116">tooopen Power BI et de la connexion de base de données AdventureWorksDW tooyour :</span><span class="sxs-lookup"><span data-stu-id="0f227-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="0f227-117">L’authentification à hello [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0f227-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="0f227-118">Cliquez sur **Bases de données SQL** et choisissez votre base de données SQL Data Warehouse AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="0f227-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Recherche de votre base de données][1]
3. <span data-ttu-id="0f227-120">Cliquez sur le bouton « Ouvrir dans Power BI » de hello.</span><span class="sxs-lookup"><span data-stu-id="0f227-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Bouton Power BI][2]
4. <span data-ttu-id="0f227-122">Vous devez maintenant voir la page de connexion SQL Data Warehouse hello afficher l’adresse web de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="0f227-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="0f227-123">Cliquez sur Suivant.</span><span class="sxs-lookup"><span data-stu-id="0f227-123">Click next.</span></span>
   
    ![Connexion Power BI][3]
5. <span data-ttu-id="0f227-125">Entrez votre nom d’utilisateur du serveur SQL Azure et votre mot de passe et vous serez la base de données SQL Data Warehouse tooyour totalement connecté.</span><span class="sxs-lookup"><span data-stu-id="0f227-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Se connecter à Power BI][4]
6. <span data-ttu-id="0f227-127">Une fois que vous avez connecté à Power BI, cliquez sur hello jeu de données AdventureWorksDW sur le panneau gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="0f227-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="0f227-128">Base de données hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="0f227-128">This will open hello database.</span></span>
   
    ![Ouvrir AdventureWorksDW Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="0f227-130">2. Créer un rapport</span><span class="sxs-lookup"><span data-stu-id="0f227-130">2. Create a report</span></span>
<span data-ttu-id="0f227-131">Vous est désormais prêt toouse Power BI tooanalyze vos exemples de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="0f227-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="0f227-132">analyse de hello tooperform, AdventureWorksDW a une vue appelée AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="0f227-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="0f227-133">Cette vue contient quelques exemples de métriques clés de hello pour l’analyse des ventes de la société de hello hello.</span><span class="sxs-lookup"><span data-stu-id="0f227-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="0f227-134">toocreate un mappage de montant des ventes en fonction de code toopostal, dans le volet de droite de champs de hello, cliquez sur hello AggregateSales vue tooexpand il.</span><span class="sxs-lookup"><span data-stu-id="0f227-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="0f227-135">Cliquez sur hello PostalCode et SalesAmount tooselect de colonnes les.</span><span class="sxs-lookup"><span data-stu-id="0f227-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![Sélection d’AggregateSales Power BI][6]
   
    <span data-ttu-id="0f227-137">Power BI reconnaît automatiquement ces données comme des données géographiques et les intègre dans une carte.</span><span class="sxs-lookup"><span data-stu-id="0f227-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Carte Power BI][7]
2. <span data-ttu-id="0f227-139">Cette étape crée un graphique à barres qui affiche le montant des ventes en fonction du revenu client.</span><span class="sxs-lookup"><span data-stu-id="0f227-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="0f227-140">toocreate cette toohello accédez développé AggregateSales vue.</span><span class="sxs-lookup"><span data-stu-id="0f227-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="0f227-141">Cliquez sur le champ SalesAmount de hello.</span><span class="sxs-lookup"><span data-stu-id="0f227-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="0f227-142">Faites glisser hello le revenu champ toohello gauche et déposez-le dans l’axe.</span><span class="sxs-lookup"><span data-stu-id="0f227-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![Axe de sélection Power BI][8]
   
    <span data-ttu-id="0f227-144">Nous avons déplacé le graphique à barres hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="0f227-144">We moved hello bar chart over hello left.</span></span>
   
    ![Barre Power BI][9]
3. <span data-ttu-id="0f227-146">Cette étape crée un graphique en courbes qui indique le montant des ventes par date de commande.</span><span class="sxs-lookup"><span data-stu-id="0f227-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="0f227-147">toocreate cette toohello accédez développé AggregateSales vue.</span><span class="sxs-lookup"><span data-stu-id="0f227-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="0f227-148">Cliquez sur SalesAmount et OrderDate.</span><span class="sxs-lookup"><span data-stu-id="0f227-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="0f227-149">Dans la colonne de visualisations hello cliquez sur l’icône de graphique en courbes hello ; Il s’agit d’icône du premier hello hello deuxième ligne sous visualisations.</span><span class="sxs-lookup"><span data-stu-id="0f227-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Sélection de graphique en courbes Power BI][10]
   
    <span data-ttu-id="0f227-151">Vous avez maintenant un rapport qui affiche les trois différentes visualisations de données de hello.</span><span class="sxs-lookup"><span data-stu-id="0f227-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![Ligne Power BI][11]

<span data-ttu-id="0f227-153">Vous pouvez enregistrer votre progression à tout moment en cliquant sur **Fichier**, puis en sélectionnant **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0f227-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f227-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f227-154">Next steps</span></span>
<span data-ttu-id="0f227-155">Maintenant que nous vous avons donné certains toowarm temps avec les données d’exemple hello, consultez Comment trop[développer][develop], [charger][load], ou [ migrer][migrate].</span><span class="sxs-lookup"><span data-stu-id="0f227-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="0f227-156">Ou examiner hello [site Web de Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="0f227-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

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
