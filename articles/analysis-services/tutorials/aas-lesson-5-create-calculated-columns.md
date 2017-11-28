---
title: "Leçon 5 du didacticiel Azure Analysis Services : Créer des colonnes calculées | Microsoft Docs"
description: "Explique comment créer des colonnes calculées dans le projet du didacticiel Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 893371145d77e156843271907aeef0c3756d0403
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="59436-103">Leçon 5 : Créer des colonnes calculées</span><span class="sxs-lookup"><span data-stu-id="59436-103">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="59436-104">Dans le cadre de cette leçon, vous créez des données dans votre modèle en ajoutant des colonnes calculées.</span><span class="sxs-lookup"><span data-stu-id="59436-104">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="59436-105">Vous pouvez créer des colonnes calculées (sous la forme de colonnes personnalisées) lorsque vous utilisez Obtenir des données, à l’aide de l’Éditeur de requêtes, ou ultérieurement dans le Concepteur de modèles comme décrit dans cette leçon.</span><span class="sxs-lookup"><span data-stu-id="59436-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span></span> <span data-ttu-id="59436-106">Pour en savoir plus, consultez [Colonnes calculées](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="59436-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="59436-107">Vous créez cinq colonnes calculées dans trois tables différentes.</span><span class="sxs-lookup"><span data-stu-id="59436-107">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="59436-108">La procédure diffère légèrement pour chacune des tâches, de façon à montrer qu’il existe plusieurs façons de créer des colonnes, de les renommer et de les placer à différents emplacements d’une table.</span><span class="sxs-lookup"><span data-stu-id="59436-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="59436-109">Cette leçon vous permet également d’utiliser pour la première fois le langage DAX (Data Analysis Expressions).</span><span class="sxs-lookup"><span data-stu-id="59436-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="59436-110">DAX est un langage spécial permettant de créer des expressions de formule hautement personnalisables pour les modèles tabulaires.</span><span class="sxs-lookup"><span data-stu-id="59436-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="59436-111">Dans le cadre de ce didacticiel, vous utilisez DAX pour créer des colonnes calculées, des mesures et des filtres de rôle.</span><span class="sxs-lookup"><span data-stu-id="59436-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span></span> <span data-ttu-id="59436-112">Pour en savoir plus, consultez [DAX dans les modèles tabulaires](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="59436-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="59436-113">Durée estimée pour suivre cette leçon : **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="59436-113">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="59436-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="59436-114">Prerequisites</span></span>  
<span data-ttu-id="59436-115">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="59436-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="59436-116">Avant d’effectuer les tâches de cette leçon, vous devez avoir suivi la leçon précédente : [Leçon 4 : Créer des relations](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="59436-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="59436-117">Créer des colonnes calculées</span><span class="sxs-lookup"><span data-stu-id="59436-117">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="59436-118">Créer une colonne calculée MonthCalendar dans la table DimDate</span><span class="sxs-lookup"><span data-stu-id="59436-118">Create a MonthCalendar calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="59436-119">Cliquez sur le menu **Modèle**> **Vue du modèle** > **Vue de données**.</span><span class="sxs-lookup"><span data-stu-id="59436-119">Click the **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="59436-120">Les colonnes calculées peuvent uniquement être créées à l’aide du Concepteur de modèles dans la vue de données.</span><span class="sxs-lookup"><span data-stu-id="59436-120">Calculated columns can only be created by using the model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="59436-121">Dans le Concepteur de modèles, cliquez sur la table **DimDate** (onglet).</span><span class="sxs-lookup"><span data-stu-id="59436-121">In the model designer, click the **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="59436-122">Cliquez avec le bouton droit sur l’en-tête de colonne **CalendarQuarter**, puis cliquez sur **Insérer une colonne**.</span><span class="sxs-lookup"><span data-stu-id="59436-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="59436-123">Une nouvelle colonne nommée **Calculated Column 1** est insérée à gauche de la colonne **Calendar Quarter**.</span><span class="sxs-lookup"><span data-stu-id="59436-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="59436-124">Dans la barre de formule située au-dessus de la table, tapez la formule DAX ci-après. La saisie semi-automatique vous aide à taper les noms complets des colonnes et des tables, et répertorie les fonctions disponibles.</span><span class="sxs-lookup"><span data-stu-id="59436-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="59436-125">Les valeurs remplissent alors toutes les lignes de la colonne calculée.</span><span class="sxs-lookup"><span data-stu-id="59436-125">Values are then populated for all the rows in the calculated column.</span></span> <span data-ttu-id="59436-126">Si vous faites défiler la table vers le bas, vous remarquez que les lignes peuvent avoir des valeurs différentes pour cette colonne, en fonction des données figurant dans chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="59436-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span></span>    
  
5.  <span data-ttu-id="59436-127">Renommez cette colonne **MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="59436-127">Rename this column to **MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="59436-129">La colonne calculée MonthCalendar fournit un nom triable pour le mois.</span><span class="sxs-lookup"><span data-stu-id="59436-129">The MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="59436-130">Créer une colonne calculée DayOfWeek dans la table DimDate</span><span class="sxs-lookup"><span data-stu-id="59436-130">Create a DayOfWeek calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="59436-131">La table **DimDate** étant toujours active, cliquez sur le menu **Colonne**, puis sur **Ajouter une colonne**.</span><span class="sxs-lookup"><span data-stu-id="59436-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="59436-132">Dans la barre de formule, tapez la formule suivante :</span><span class="sxs-lookup"><span data-stu-id="59436-132">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="59436-133">Quand vous avez terminé de générer la formule, appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="59436-133">When you've finished building the formula, press ENTER.</span></span> <span data-ttu-id="59436-134">La nouvelle colonne est ajoutée à l’extrême droite de la table.</span><span class="sxs-lookup"><span data-stu-id="59436-134">The new column is added to the far right of the table.</span></span>  
  
3.  <span data-ttu-id="59436-135">Renommez la colonne en **DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="59436-135">Rename the column to **DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="59436-136">Cliquez sur l’en-tête de colonne, puis faites glisser la colonne entre la colonne **EnglishDayNameOfWeek** et la colonne **DayNumberOfMonth**.</span><span class="sxs-lookup"><span data-stu-id="59436-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="59436-137">Déplacer les colonnes dans la table facilite la navigation.</span><span class="sxs-lookup"><span data-stu-id="59436-137">Moving columns in your table makes it easier to navigate.</span></span>  
  
<span data-ttu-id="59436-138">La colonne calculée DayOfWeek fournit un nom triable pour le jour de la semaine.</span><span class="sxs-lookup"><span data-stu-id="59436-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="59436-139">Créer une colonne calculée ProductSubcategoryName dans la table DimProduct</span><span class="sxs-lookup"><span data-stu-id="59436-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="59436-140">Dans la table **DimProduct**, faites défiler l’affichage jusqu’à l’extrême droite de la table.</span><span class="sxs-lookup"><span data-stu-id="59436-140">In the **DimProduct** table, scroll to the far right of the table.</span></span> <span data-ttu-id="59436-141">Notez que la colonne la plus à droite est nommée **Add Column** (en italique). Cliquez sur l’en-tête de colonne.</span><span class="sxs-lookup"><span data-stu-id="59436-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span></span>  
  
2.  <span data-ttu-id="59436-142">Dans la barre de formule, tapez la formule suivante :</span><span class="sxs-lookup"><span data-stu-id="59436-142">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="59436-143">Renommez la colonne en **ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="59436-143">Rename the column to **ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="59436-144">La colonne calculée ProductSubcategoryName est utilisée pour créer une hiérarchie dans la table DimProduct, qui inclut les données de la colonne EnglishProductSubcategoryName de la table DimProductSubcategory.</span><span class="sxs-lookup"><span data-stu-id="59436-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span></span> <span data-ttu-id="59436-145">Les hiérarchies ne peuvent pas couvrir plusieurs tables.</span><span class="sxs-lookup"><span data-stu-id="59436-145">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="59436-146">Vous créerez des hiérarchies ultérieurement, dans le cadre de la Leçon 9.</span><span class="sxs-lookup"><span data-stu-id="59436-146">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="59436-147">Créer une colonne calculée ProductCategoryName dans la table DimProduct</span><span class="sxs-lookup"><span data-stu-id="59436-147">Create a ProductCategoryName calculated column in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="59436-148">La table **DimProduct** étant toujours active, cliquez sur le menu **Colonne**, puis sur **Ajouter une colonne**.</span><span class="sxs-lookup"><span data-stu-id="59436-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="59436-149">Dans la barre de formule, tapez la formule suivante :</span><span class="sxs-lookup"><span data-stu-id="59436-149">In the formula bar, type the following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="59436-150">Renommez la colonne en **ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="59436-150">Rename the column to **ProductCategoryName**.</span></span>  
  
<span data-ttu-id="59436-151">La colonne calculée ProductCategoryName est utilisée pour créer une hiérarchie dans la table DimProduct, qui inclut les données de la colonne EnglishProductCategoryName de la table DimProductCategory.</span><span class="sxs-lookup"><span data-stu-id="59436-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span></span> <span data-ttu-id="59436-152">Les hiérarchies ne peuvent pas couvrir plusieurs tables.</span><span class="sxs-lookup"><span data-stu-id="59436-152">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a><span data-ttu-id="59436-153">Créer une colonne calculée Margin dans la table FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="59436-153">Create a Margin calculated column in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="59436-154">Dans le Concepteur de modèles, sélectionnez la table **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="59436-154">In the model designer, select the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="59436-155">Créez une colonne calculée entre la colonne **SalesAmount** et la colonne **TaxAmt**.</span><span class="sxs-lookup"><span data-stu-id="59436-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="59436-156">Dans la barre de formule, tapez la formule suivante :</span><span class="sxs-lookup"><span data-stu-id="59436-156">In the formula bar, type the following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="59436-157">Renommez la colonne en **Margin**.</span><span class="sxs-lookup"><span data-stu-id="59436-157">Rename the column to **Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="59436-159">La colonne calculée Margin est utilisée pour analyser les marges pour chaque vente.</span><span class="sxs-lookup"><span data-stu-id="59436-159">The Margin calculated column is used to analyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="59436-160">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="59436-160">What's next?</span></span>
<span data-ttu-id="59436-161">[Leçon 6 : Créer des mesures](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="59436-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
