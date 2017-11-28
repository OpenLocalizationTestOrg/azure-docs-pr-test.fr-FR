---
title: "Leçon supplémentaire du didacticiel Azure Analysis Services : Lignes de détails | Microsoft Docs"
description: "Explique comment créer une expression de lignes de détails dans le didacticiel Azure Analysis Services."
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
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: fde5cd9a9efc3a13e731a91962ced5c086a72355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="46c80-103">Leçon supplémentaire – Lignes de détails</span><span class="sxs-lookup"><span data-stu-id="46c80-103">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="46c80-104">Dans cette leçon supplémentaire, vous allez utiliser l’éditeur DAX pour définir une expression de lignes de détail personnalisée.</span><span class="sxs-lookup"><span data-stu-id="46c80-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span></span> <span data-ttu-id="46c80-105">Une expression de lignes de détail est une propriété sur une mesure qui fournit aux utilisateurs finaux des informations supplémentaires sur les résultats agrégées d’une mesure.</span><span class="sxs-lookup"><span data-stu-id="46c80-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span></span> 
  
<span data-ttu-id="46c80-106">Durée estimée pour suivre cette leçon : **10 minutes**</span><span class="sxs-lookup"><span data-stu-id="46c80-106">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="46c80-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="46c80-107">Prerequisites</span></span>  
<span data-ttu-id="46c80-108">Cette rubrique de leçon supplémentaire fait partie d’un didacticiel de modélisation tabulaire.</span><span class="sxs-lookup"><span data-stu-id="46c80-108">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="46c80-109">Avant d’effectuer les tâches de cette leçon supplémentaire, vous devez avoir effectué toutes les leçons précédentes ou disposer d’un exemple de projet de modèle de ventes sur Internet Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="46c80-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-to-solve"></a><span data-ttu-id="46c80-110">Quels problèmes devons-nous résoudre ?</span><span class="sxs-lookup"><span data-stu-id="46c80-110">What do we need to solve?</span></span>
<span data-ttu-id="46c80-111">Examinons les détails de notre mesure InternetTotalSales avant l’ajout d’expression de lignes de détail.</span><span class="sxs-lookup"><span data-stu-id="46c80-111">Let's look at the details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="46c80-112">Dans SSDT, cliquez sur le menu **Modèle** > **Analyser dans Excel** pour ouvrir Excel et créer un tableau croisé dynamique vide.</span><span class="sxs-lookup"><span data-stu-id="46c80-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="46c80-113">Dans **Champs de tableau croisé dynamique**, ajoutez la mesure **InternetTotalSales** de la table FactInternetSales à **Valeurs**, **CalendarYear** de la table DimDate à **Colonnes** et **EnglishCountryRegionName** à **Lignes**.</span><span class="sxs-lookup"><span data-stu-id="46c80-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span></span> <span data-ttu-id="46c80-114">Notre tableau croisé dynamique nous indique maintenant les résultats agrégés de la mesure InternetTotalSales par région et par année.</span><span class="sxs-lookup"><span data-stu-id="46c80-114">Our PivotTable now gives us aggregated results from the InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="46c80-116">Dans le tableau croisé dynamique, double-cliquez sur une valeur agrégée pour une année et un nom de région.</span><span class="sxs-lookup"><span data-stu-id="46c80-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="46c80-117">Ici, nous avons double-cliqué sur la valeur correspondant à l’Australie et à l’année 2014.</span><span class="sxs-lookup"><span data-stu-id="46c80-117">Here we double-clicked the value for Australia and the year 2014.</span></span> <span data-ttu-id="46c80-118">Cette opération affiche une nouvelle feuille contenant des données dont nous n’avons pas l’utilité.</span><span class="sxs-lookup"><span data-stu-id="46c80-118">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="46c80-120">Nous aimerions voir ici une table contenant des colonnes et des lignes de données qui contribuent au résultat agrégé de notre mesure InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="46c80-120">What we would like to see here is a table containing columns and rows of data that contribute to the aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="46c80-121">Pour ce faire, nous pouvons ajouter une expression de lignes de détail comme propriété de la mesure.</span><span class="sxs-lookup"><span data-stu-id="46c80-121">To do that, we can add a Detail Rows Expression as a property of the measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="46c80-122">Ajouter une expression de lignes de détail</span><span class="sxs-lookup"><span data-stu-id="46c80-122">Add a Detail Rows Expression</span></span>

#### <a name="to-create-a-detail-rows-expression"></a><span data-ttu-id="46c80-123">Pour créer une expression de lignes de détail</span><span class="sxs-lookup"><span data-stu-id="46c80-123">To create a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="46c80-124">Dans SSDT, dans la grille de mesure de la table FactInternetSales, cliquez sur la mesure **InternetTotalSales**.</span><span class="sxs-lookup"><span data-stu-id="46c80-124">In SSDT, in the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="46c80-125">Dans **Propriétés** > **Expression de lignes de détail**, cliquez sur le bouton de l’éditeur pour ouvrir l’éditeur DAX.</span><span class="sxs-lookup"><span data-stu-id="46c80-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="46c80-127">Dans l’éditeur DAX, entrez l’expression suivante :</span><span class="sxs-lookup"><span data-stu-id="46c80-127">In DAX Editor, enter the following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="46c80-128">Cette expression indique que des noms, des colonnes et des résultats de mesure provenant de la table FactInternetSales et de tables associées sont retournés quand un utilisateur double-clique sur un résultat agrégé dans un tableau croisé dynamique ou un rapport.</span><span class="sxs-lookup"><span data-stu-id="46c80-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="46c80-129">De retour dans Excel, supprimez la feuille créée à l’étape 3, puis double-cliquez sur une valeur agrégée.</span><span class="sxs-lookup"><span data-stu-id="46c80-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="46c80-130">Cette fois, avec une propriété d’expression de lignes de détail définie pour la mesure, une nouvelle feuille contenant des données beaucoup plus utiles s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="46c80-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="46c80-132">Redéployez votre modèle.</span><span class="sxs-lookup"><span data-stu-id="46c80-132">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="46c80-133">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="46c80-133">See Also</span></span>  
<span data-ttu-id="46c80-134">[SELECTCOLUMNS, fonction (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="46c80-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="46c80-135">Leçon supplémentaire – Sécurité dynamique</span><span class="sxs-lookup"><span data-stu-id="46c80-135">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="46c80-136">Leçon supplémentaire – Hiérarchies déséquilibrées</span><span class="sxs-lookup"><span data-stu-id="46c80-136">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
