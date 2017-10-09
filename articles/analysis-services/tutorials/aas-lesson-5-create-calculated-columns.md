---
<span data-ttu-id="96f3b-101">titre : aaa « leçon du didacticiel Azure Analysis Services 5 : créer des colonnes calculées | Description de Microsoft Docs » : décrit comment toocreate calculées des colonnes dans le projet du didacticiel hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="96f3b-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="96f3b-102">Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="96f3b-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="96f3b-103">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 01/06/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="96f3b-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="96f3b-104">Leçon 5 : Créer des colonnes calculées</span><span class="sxs-lookup"><span data-stu-id="96f3b-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="96f3b-105">Dans le cadre de cette leçon, vous créez des données dans votre modèle en ajoutant des colonnes calculées.</span><span class="sxs-lookup"><span data-stu-id="96f3b-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="96f3b-106">Vous pouvez créer des colonnes calculées (en tant que colonnes personnalisées) lorsque vous utilisez obtenir des données, à l’aide de l’éditeur de requête hello ou plus loin dans le type de Concepteur de modèle hello suivre ici.</span><span class="sxs-lookup"><span data-stu-id="96f3b-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="96f3b-107">toolearn, voir [des colonnes calculées](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="96f3b-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="96f3b-108">Vous créez cinq colonnes calculées dans trois tables différentes.</span><span class="sxs-lookup"><span data-stu-id="96f3b-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="96f3b-109">Hello étapes sont légèrement différentes pour chaque tâche indiquant de plusieurs manières toocreate colonnes, les renommer et les placer à différents emplacements dans une table.</span><span class="sxs-lookup"><span data-stu-id="96f3b-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="96f3b-110">Cette leçon vous permet également d’utiliser pour la première fois le langage DAX (Data Analysis Expressions).</span><span class="sxs-lookup"><span data-stu-id="96f3b-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="96f3b-111">DAX est un langage spécial permettant de créer des expressions de formule hautement personnalisables pour les modèles tabulaires.</span><span class="sxs-lookup"><span data-stu-id="96f3b-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="96f3b-112">Dans ce didacticiel, vous utilisez les colonnes calculée de toocreate DAX, les mesures et les filtres de rôle.</span><span class="sxs-lookup"><span data-stu-id="96f3b-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="96f3b-113">toolearn, voir [DAX dans les modèles tabulaires](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="96f3b-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="96f3b-114">Estimé temps toocomplete cette leçon : **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="96f3b-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="96f3b-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="96f3b-115">Prerequisites</span></span>  
<span data-ttu-id="96f3b-116">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="96f3b-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="96f3b-117">Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 4 : créer des relations](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="96f3b-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="96f3b-118">Créer des colonnes calculées</span><span class="sxs-lookup"><span data-stu-id="96f3b-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="96f3b-119">Créer une colonne calculée MonthCalendar dans la table DimDate de hello</span><span class="sxs-lookup"><span data-stu-id="96f3b-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="96f3b-120">Cliquez sur hello **modèle** menu > **vue de modèle** > **vue données**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="96f3b-121">Les colonnes calculées peuvent uniquement être créées à l’aide du Générateur de modèles hello dans la vue de données.</span><span class="sxs-lookup"><span data-stu-id="96f3b-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="96f3b-122">Dans le Concepteur de modèle hello, cliquez sur hello **DimDate** table (onglet).</span><span class="sxs-lookup"><span data-stu-id="96f3b-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="96f3b-123">Avec le bouton hello **CalendarQuarter** en-tête de colonne, puis cliquez sur **insérer une colonne**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="96f3b-124">Une nouvelle colonne nommée **1 de colonne calculée** est inséré toohello gauche hello **trimestre** colonne.</span><span class="sxs-lookup"><span data-stu-id="96f3b-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="96f3b-125">Dans la barre de formule hello au-dessus de table de hello, tapez Bonjour DAX formule suivante : vous aide à la saisie semi-automatique vous tapez hello des noms complets des colonnes et tables et listes hello des fonctions qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="96f3b-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="96f3b-126">Des valeurs remplissent ensuite toutes les lignes hello dans la colonne calculée de hello.</span><span class="sxs-lookup"><span data-stu-id="96f3b-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="96f3b-127">Si vous faites défiler la table de hello, vous consultez lignes peuvent avoir des valeurs différentes pour cette colonne, en fonction des données hello dans chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="96f3b-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="96f3b-128">Renommer cette colonne trop**MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="96f3b-130">colonne calculée de MonthCalendar Hello fournit un nom triable pour le mois.</span><span class="sxs-lookup"><span data-stu-id="96f3b-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="96f3b-131">Créer une colonne calculée DayOfWeek dans la table DimDate de hello</span><span class="sxs-lookup"><span data-stu-id="96f3b-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="96f3b-132">Avec hello **DimDate** toujours active, cliquez sur hello **colonne** menu, puis sur **ajouter une colonne**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="96f3b-133">Dans la barre de formule hello, tapez hello formule suivante :</span><span class="sxs-lookup"><span data-stu-id="96f3b-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="96f3b-134">Lorsque vous avez terminé de créer la formule de hello, appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="96f3b-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="96f3b-135">Hello nouvelle colonne est ajoutée toohello plus à droite de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="96f3b-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="96f3b-136">Renommer les colonnes hello trop**DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="96f3b-137">Cliquez sur l’en-tête de colonne hello, puis faites glisser les colonnes hello entre hello **EnglishDayNameOfWeek** colonne et hello **DayNumberOfMonth** colonne.</span><span class="sxs-lookup"><span data-stu-id="96f3b-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="96f3b-138">Déplacer les colonnes dans votre table rend toonavigate plus facile.</span><span class="sxs-lookup"><span data-stu-id="96f3b-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="96f3b-139">colonne calculée de Hello DayOfWeek fournit un nom triable pour le jour hello de la semaine.</span><span class="sxs-lookup"><span data-stu-id="96f3b-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="96f3b-140">Créer une colonne calculée ProductSubcategoryName dans la table DimProduct de hello</span><span class="sxs-lookup"><span data-stu-id="96f3b-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="96f3b-141">Bonjour **DimProduct** table, faites défiler toohello plus à droite de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="96f3b-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="96f3b-142">Colonne de notification hello plus à droite est nommée **ajouter une colonne** (en italique), cliquez sur l’en-tête de colonne hello.</span><span class="sxs-lookup"><span data-stu-id="96f3b-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="96f3b-143">Dans la barre de formule hello, tapez hello formule suivante :</span><span class="sxs-lookup"><span data-stu-id="96f3b-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="96f3b-144">Renommer les colonnes hello trop**ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="96f3b-145">colonne calculée de Hello ProductSubcategoryName est toocreate utilisé une hiérarchie dans la table DimProduct hello, qui inclut des données à partir de la colonne de EnglishProductSubcategoryName hello dans la table DimProductSubcategory de hello.</span><span class="sxs-lookup"><span data-stu-id="96f3b-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="96f3b-146">Les hiérarchies ne peuvent pas couvrir plusieurs tables.</span><span class="sxs-lookup"><span data-stu-id="96f3b-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="96f3b-147">Vous créerez des hiérarchies ultérieurement, dans le cadre de la Leçon 9.</span><span class="sxs-lookup"><span data-stu-id="96f3b-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="96f3b-148">Créer une colonne calculée ProductCategoryName dans la table DimProduct de hello</span><span class="sxs-lookup"><span data-stu-id="96f3b-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="96f3b-149">Avec hello **DimProduct** toujours active, cliquez sur hello **colonne** menu, puis sur **ajouter une colonne**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="96f3b-150">Dans la barre de formule hello, tapez hello formule suivante :</span><span class="sxs-lookup"><span data-stu-id="96f3b-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="96f3b-151">Renommer les colonnes hello trop**ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="96f3b-152">colonne calculée de ProductCategoryName Hello est toocreate utilisé une hiérarchie dans la table DimProduct hello, qui inclut des données à partir de la colonne de EnglishProductCategoryName hello dans la table de DimProductCategory hello.</span><span class="sxs-lookup"><span data-stu-id="96f3b-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="96f3b-153">Les hiérarchies ne peuvent pas couvrir plusieurs tables.</span><span class="sxs-lookup"><span data-stu-id="96f3b-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="96f3b-154">Créer une colonne calculée de marge dans la table FactInternetSales de hello</span><span class="sxs-lookup"><span data-stu-id="96f3b-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="96f3b-155">Dans le Concepteur de modèle hello, sélectionnez hello **FactInternetSales** table.</span><span class="sxs-lookup"><span data-stu-id="96f3b-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="96f3b-156">Créer une nouvelle colonne calculée entre hello **SalesAmount** colonne et hello **TaxAmt** colonne.</span><span class="sxs-lookup"><span data-stu-id="96f3b-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="96f3b-157">Dans la barre de formule hello, tapez hello formule suivante :</span><span class="sxs-lookup"><span data-stu-id="96f3b-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="96f3b-158">Renommer les colonnes hello trop**marge**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="96f3b-160">colonne calculée de marge Hello est marges tooanalyze utilisés pour chaque vente.</span><span class="sxs-lookup"><span data-stu-id="96f3b-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="96f3b-161">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="96f3b-161">What's next?</span></span>
<span data-ttu-id="96f3b-162">[Leçon 6 : Créer des mesures](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="96f3b-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
