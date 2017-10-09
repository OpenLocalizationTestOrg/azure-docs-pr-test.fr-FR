---
<span data-ttu-id="17d8e-101">titre : aaa « leçon du didacticiel Azure Analysis Services 6 : créer des mesures | Description de Microsoft Docs » : décrit comment toocreate mesure dans le projet du didacticiel hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="17d8e-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="17d8e-102">Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="17d8e-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="17d8e-103">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 01/06/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="17d8e-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="17d8e-104">Leçon 6 : Créer des mesures</span><span class="sxs-lookup"><span data-stu-id="17d8e-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="17d8e-105">Dans cette leçon, vous créez toobe de mesures inclus dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="17d8e-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="17d8e-106">Toohello similaire calculée des colonnes que vous avez créé, une mesure est un calcul créé à l’aide d’une formule DAX.</span><span class="sxs-lookup"><span data-stu-id="17d8e-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="17d8e-107">Toutefois, contrairement aux colonnes calculées, les mesures sont évaluées sur la base d’un *filtre* sélectionné par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="17d8e-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="17d8e-108">Par exemple, une colonne particulière ou un segment ajoutée champ des étiquettes de ligne toohello dans un tableau croisé dynamique.</span><span class="sxs-lookup"><span data-stu-id="17d8e-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="17d8e-109">Une valeur pour chaque cellule de filtre de hello est ensuite calculée par mesure de hello appliqué.</span><span class="sxs-lookup"><span data-stu-id="17d8e-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="17d8e-110">Les mesures sont des calculs puissants et flexibles que vous souhaitez tooinclude dans presque tous les calculs dynamiques tooperform de modèles tabulaires sur des données numériques.</span><span class="sxs-lookup"><span data-stu-id="17d8e-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="17d8e-111">toolearn, voir [mesures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="17d8e-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="17d8e-112">les mesures toocreate, vous utilisez hello *grille de mesures*.</span><span class="sxs-lookup"><span data-stu-id="17d8e-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="17d8e-113">Par défaut, chaque table comprend une grille de mesures vide. Toutefois, la plupart du temps, vous n’êtes pas obligé de créer des mesures pour chaque table.</span><span class="sxs-lookup"><span data-stu-id="17d8e-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="17d8e-114">grille de mesures Hello s’affiche sous une table dans le Générateur de modèles hello dans la vue de données.</span><span class="sxs-lookup"><span data-stu-id="17d8e-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="17d8e-115">grille de mesures hello toohide ou afficher une table, cliquez sur hello **Table** menu, puis sur **afficher la grille de mesures**.</span><span class="sxs-lookup"><span data-stu-id="17d8e-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="17d8e-116">Vous pouvez créer une mesure en cliquant sur une cellule vide dans la grille de mesures hello, puis en tapant une formule DAX dans la barre de formule hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="17d8e-117">Lorsque vous cliquez sur entrer une formule hello toocomplete, les mesures hello puis apparaît dans la cellule de hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="17d8e-118">Vous pouvez également créer des mesures à l’aide d’une fonction d’agrégation standard en cliquant sur une colonne, puis en cliquant sur hello bouton Somme automatique (**∑**) sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="17d8e-119">Les mesures créées à l’aide de la fonction de somme automatique hello apparaissent dans la cellule de grille de mesures hello directement sous la colonne de hello, mais peuvent être déplacés.</span><span class="sxs-lookup"><span data-stu-id="17d8e-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="17d8e-120">Dans cette leçon, vous créez les mesures en entrant une formule DAX dans la barre de formule hello et en utilisant la fonction de somme automatique hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="17d8e-121">Estimé temps toocomplete cette leçon : **30 minutes**</span><span class="sxs-lookup"><span data-stu-id="17d8e-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="17d8e-122">Composants requis</span><span class="sxs-lookup"><span data-stu-id="17d8e-122">Prerequisites</span></span>  
<span data-ttu-id="17d8e-123">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="17d8e-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="17d8e-124">Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 5 : créer des colonnes calculées](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="17d8e-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="17d8e-125">Créer des mesures</span><span class="sxs-lookup"><span data-stu-id="17d8e-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="17d8e-126">toocreate une mesure DaysCurrentQuarterToDate dans la table DimDate de hello</span><span class="sxs-lookup"><span data-stu-id="17d8e-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="17d8e-127">Dans le Concepteur de modèle hello, cliquez sur hello **DimDate** table.</span><span class="sxs-lookup"><span data-stu-id="17d8e-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="17d8e-128">Dans la grille de mesures hello, cliquez sur cellule vide en haut à gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="17d8e-129">Dans la barre de formule hello, tapez hello formule suivante :</span><span class="sxs-lookup"><span data-stu-id="17d8e-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="17d8e-130">Avis hello supérieur gauche de la cellule contient désormais un nom de mesure, **DaysCurrentQuarterToDate**, suivi par le résultat de hello, **92**.</span><span class="sxs-lookup"><span data-stu-id="17d8e-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="17d8e-132">Contrairement aux colonnes calculées, des formules de mesure vous pouvez taper un nom de la mesure hello, suivie du signe deux-points, suivi d’une expression de la formule hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="17d8e-133">toocreate une mesure DaysInCurrentQuarter dans la table DimDate de hello</span><span class="sxs-lookup"><span data-stu-id="17d8e-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="17d8e-134">Avec hello **DimDate** toujours active dans le Concepteur de modèle hello, dans la grille de mesures hello, cliquez sur la cellule vide de hello sous mesure hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="17d8e-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="17d8e-135">Dans la barre de formule hello, tapez hello formule suivante :</span><span class="sxs-lookup"><span data-stu-id="17d8e-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="17d8e-136">Lorsque vous créez un rapport de comparaison entre une période incomplète et hello période précédente.</span><span class="sxs-lookup"><span data-stu-id="17d8e-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="17d8e-137">formule de Hello doit calculer la proportion de hello de période hello qui s’est écoulée et comparez-la toohello même proportion Bonjour période précédente.</span><span class="sxs-lookup"><span data-stu-id="17d8e-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="17d8e-138">Dans ce cas, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] donne hello proportion écoulé Bonjour période en cours.</span><span class="sxs-lookup"><span data-stu-id="17d8e-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="17d8e-139">toocreate une mesure de InternetDistinctCountSalesOrder dans la table FactInternetSales de hello</span><span class="sxs-lookup"><span data-stu-id="17d8e-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="17d8e-140">Cliquez sur hello **FactInternetSales** table.</span><span class="sxs-lookup"><span data-stu-id="17d8e-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="17d8e-141">Cliquez sur hello **SalesOrderNumber** en-tête de colonne.</span><span class="sxs-lookup"><span data-stu-id="17d8e-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="17d8e-142">Barre d’outils hello, cliquez sur hello flèche toohello suivant Somme automatique (**∑**), puis **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="17d8e-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="17d8e-143">fonction de somme automatique Hello crée automatiquement une mesure pour la colonne sélectionnée de hello à l’aide de la formule de regroupement standard DistinctCount hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="17d8e-145">Dans la grille de mesures hello, cliquez sur Nouvelle mesure de hello, puis dans hello **propriétés** fenêtre, dans **nom de la mesure**, renommez les mesures hello trop**InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="17d8e-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="17d8e-146">toocreate des mesures supplémentaires dans la table FactInternetSales de hello</span><span class="sxs-lookup"><span data-stu-id="17d8e-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="17d8e-147">En utilisant la fonction de somme automatique hello, créez et nommez les hello suivant de mesures :</span><span class="sxs-lookup"><span data-stu-id="17d8e-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="17d8e-148">Colonne</span><span class="sxs-lookup"><span data-stu-id="17d8e-148">Column</span></span>|<span data-ttu-id="17d8e-149">Nom de la mesure</span><span class="sxs-lookup"><span data-stu-id="17d8e-149">Measure name</span></span>|<span data-ttu-id="17d8e-150">Somme automatique (∑)</span><span class="sxs-lookup"><span data-stu-id="17d8e-150">AutoSum (∑)</span></span>|<span data-ttu-id="17d8e-151">Formule</span><span class="sxs-lookup"><span data-stu-id="17d8e-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="17d8e-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="17d8e-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="17d8e-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="17d8e-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="17d8e-154">Nombre</span><span class="sxs-lookup"><span data-stu-id="17d8e-154">Count</span></span>|<span data-ttu-id="17d8e-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="17d8e-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="17d8e-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="17d8e-156">OrderQuantity</span></span>|<span data-ttu-id="17d8e-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="17d8e-157">InternetTotalUnits</span></span>|<span data-ttu-id="17d8e-158">Somme</span><span class="sxs-lookup"><span data-stu-id="17d8e-158">Sum</span></span>|<span data-ttu-id="17d8e-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="17d8e-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="17d8e-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="17d8e-160">DiscountAmount</span></span>|<span data-ttu-id="17d8e-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="17d8e-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="17d8e-162">Somme</span><span class="sxs-lookup"><span data-stu-id="17d8e-162">Sum</span></span>|<span data-ttu-id="17d8e-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="17d8e-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="17d8e-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="17d8e-164">TotalProductCost</span></span>|<span data-ttu-id="17d8e-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="17d8e-165">InternetTotalProductCost</span></span>|<span data-ttu-id="17d8e-166">Somme</span><span class="sxs-lookup"><span data-stu-id="17d8e-166">Sum</span></span>|<span data-ttu-id="17d8e-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="17d8e-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="17d8e-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="17d8e-168">SalesAmount</span></span>|<span data-ttu-id="17d8e-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="17d8e-169">InternetTotalSales</span></span>|<span data-ttu-id="17d8e-170">Somme</span><span class="sxs-lookup"><span data-stu-id="17d8e-170">Sum</span></span>|<span data-ttu-id="17d8e-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="17d8e-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="17d8e-172">Margin</span><span class="sxs-lookup"><span data-stu-id="17d8e-172">Margin</span></span>|<span data-ttu-id="17d8e-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="17d8e-173">InternetTotalMargin</span></span>|<span data-ttu-id="17d8e-174">Somme</span><span class="sxs-lookup"><span data-stu-id="17d8e-174">Sum</span></span>|<span data-ttu-id="17d8e-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="17d8e-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="17d8e-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="17d8e-176">TaxAmt</span></span>|<span data-ttu-id="17d8e-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="17d8e-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="17d8e-178">Somme</span><span class="sxs-lookup"><span data-stu-id="17d8e-178">Sum</span></span>|<span data-ttu-id="17d8e-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="17d8e-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="17d8e-180">Freight</span><span class="sxs-lookup"><span data-stu-id="17d8e-180">Freight</span></span>|<span data-ttu-id="17d8e-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="17d8e-181">InternetTotalFreight</span></span>|<span data-ttu-id="17d8e-182">Somme</span><span class="sxs-lookup"><span data-stu-id="17d8e-182">Sum</span></span>|<span data-ttu-id="17d8e-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="17d8e-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="17d8e-184">En cliquant sur une cellule vide dans la grille de mesures hello et à l’aide de barre de formule hello, créer et les mesures suivantes hello de nom dans l’ordre :</span><span class="sxs-lookup"><span data-stu-id="17d8e-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="17d8e-185">Les mesures créées pour la table FactInternetSales de hello peuvent être utilisé tooanalyze des données financières critiques telles que les ventes et les coûts, marge bénéficiaire des éléments définis par le filtre de hello utilisateur sélectionné.</span><span class="sxs-lookup"><span data-stu-id="17d8e-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="17d8e-186">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="17d8e-186">What's next?</span></span>
<span data-ttu-id="17d8e-187">[Leçon 7 : Afficher les indicateurs de performance clés](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="17d8e-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
