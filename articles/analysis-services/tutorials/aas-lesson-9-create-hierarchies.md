---
title: "Leçon 9 du didacticiel Azure Analysis Services : Créer des hiérarchies | Microsoft Docs"
description: 
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
ms.openlocfilehash: d628dc621335acf231342a6d9186079de16e85f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="fd435-102">Leçon 9 : Créer des hiérarchies</span><span class="sxs-lookup"><span data-stu-id="fd435-102">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="fd435-103">Dans cette leçon, vous allez créer des hiérarchies.</span><span class="sxs-lookup"><span data-stu-id="fd435-103">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="fd435-104">Les hiérarchies sont des groupes de colonnes organisées en niveaux. Par exemple, la hiérarchie Géographie peut comporter des sous-niveaux correspondant à des pays, des régions, des départements et des villes.</span><span class="sxs-lookup"><span data-stu-id="fd435-104">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="fd435-105">Les hiérarchies peuvent être affichées séparément des autres colonnes, dans une liste de champs d’applications clientes de création de rapports, ce qui permet aux utilisateurs clients de naviguer facilement parmi les hiérarchies et de les inclure dans un rapport.</span><span class="sxs-lookup"><span data-stu-id="fd435-105">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users to navigate and include in a report.</span></span> <span data-ttu-id="fd435-106">Pour plus d’informations, consultez [Hiérarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="fd435-106">To learn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="fd435-107">Pour créer des hiérarchies, utilisez le Générateur de modèles disponible dans la *Vue de diagramme*.</span><span class="sxs-lookup"><span data-stu-id="fd435-107">To create hierarchies, use the model designer in *Diagram View*.</span></span> <span data-ttu-id="fd435-108">La création et la gestion des hiérarchies ne sont pas prises en charge dans la vue de données.</span><span class="sxs-lookup"><span data-stu-id="fd435-108">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="fd435-109">Durée estimée pour suivre cette leçon : **20 minutes**</span><span class="sxs-lookup"><span data-stu-id="fd435-109">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="fd435-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="fd435-110">Prerequisites</span></span>  
<span data-ttu-id="fd435-111">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="fd435-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="fd435-112">Avant d’effectuer les tâches de cette leçon, vous devez avoir terminé la leçon précédente : [Leçon 8 : Créer des perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="fd435-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="fd435-113">Créer des hiérarchies</span><span class="sxs-lookup"><span data-stu-id="fd435-113">Create hierarchies</span></span>  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a><span data-ttu-id="fd435-114">Pour créer une hiérarchie de catégories dans la table DimProduct</span><span class="sxs-lookup"><span data-stu-id="fd435-114">To create a Category hierarchy in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="fd435-115">Dans le Concepteur de modèles (vue de diagramme), cliquez sur la table **DimProduct** > **Créer une hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="fd435-115">In the model designer (diagram view), right-click the **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="fd435-116">Une nouvelle hiérarchie s’affiche au bas de la table.</span><span class="sxs-lookup"><span data-stu-id="fd435-116">A new hierarchy appears at the bottom of the table window.</span></span> <span data-ttu-id="fd435-117">Attribuez à la hiérarchie le nom de **Catégorie**.</span><span class="sxs-lookup"><span data-stu-id="fd435-117">Rename the hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="fd435-118">Cliquez et faites glisser la colonne **ProductCategoryName** vers la nouvelle hiérarchie **Catégorie**.</span><span class="sxs-lookup"><span data-stu-id="fd435-118">Click and drag the **ProductCategoryName** column to the new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="fd435-119">Dans la hiérarchie **Catégorie**, cliquez avec le bouton droit sur **ProductCategoryName** > **Renommer**, puis tapez **Catégorie**.</span><span class="sxs-lookup"><span data-stu-id="fd435-119">In the **Category** hierarchy, right-click the **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="fd435-120">Le fait de renommer une colonne dans une hiérarchie ne renomme pas cette colonne dans la table.</span><span class="sxs-lookup"><span data-stu-id="fd435-120">Renaming a column in a hierarchy does not rename that column in the table.</span></span> <span data-ttu-id="fd435-121">Une colonne de hiérarchie n’est que la représentation de cette colonne dans la table.</span><span class="sxs-lookup"><span data-stu-id="fd435-121">A column in a hierarchy is just a representation of the column in the table.</span></span>  
  
4.  <span data-ttu-id="fd435-122">Cliquez et faites glisser la colonne **ProductSubcategoryName** vers la hiérarchie **Catégorie**.</span><span class="sxs-lookup"><span data-stu-id="fd435-122">Click and drag the **ProductSubcategoryName** column to the **Category** hierarchy.</span></span> <span data-ttu-id="fd435-123">Renommez cette colonne **Sous-catégorie**.</span><span class="sxs-lookup"><span data-stu-id="fd435-123">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="fd435-124">Cliquez avec le bouton droit sur la colonne **ModelName** > **Ajouter à la hiérarchie**, puis sélectionnez **Catégorie**.</span><span class="sxs-lookup"><span data-stu-id="fd435-124">Right-click the **ModelName** column > **Add to hierarchy**, and then select **Category**.</span></span> <span data-ttu-id="fd435-125">Renommez cette colonne **Modèle**.</span><span class="sxs-lookup"><span data-stu-id="fd435-125">Rename it **Model**.</span></span>

6.  <span data-ttu-id="fd435-126">Enfin, ajoutez **EnglishProductName** à la hiérarchie Catégorie.</span><span class="sxs-lookup"><span data-stu-id="fd435-126">Finally, add **EnglishProductName** to the Category hierarchy.</span></span> <span data-ttu-id="fd435-127">Renommez cette colonne **Produit**.</span><span class="sxs-lookup"><span data-stu-id="fd435-127">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a><span data-ttu-id="fd435-129">Pour créer des hiérarchies dans la table DimDate</span><span class="sxs-lookup"><span data-stu-id="fd435-129">To create hierarchies in the DimDate table</span></span>  
  
1.  <span data-ttu-id="fd435-130">Dans la table **DimDate**, créez une hiérarchie nommée **Calendar**.</span><span class="sxs-lookup"><span data-stu-id="fd435-130">In the **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="fd435-131">Ajoutez les colonnes suivantes, dans cet ordre :</span><span class="sxs-lookup"><span data-stu-id="fd435-131">Add the following columns in-order:</span></span>

    *  <span data-ttu-id="fd435-132">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="fd435-132">CalendarYear</span></span>
    *  <span data-ttu-id="fd435-133">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="fd435-133">CalendarSemester</span></span>
    *  <span data-ttu-id="fd435-134">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="fd435-134">CalendarQuarter</span></span>
    *  <span data-ttu-id="fd435-135">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="fd435-135">MonthCalendar</span></span>
    *  <span data-ttu-id="fd435-136">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="fd435-136">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="fd435-137">Dans la table **DimDate**, créez une hiérarchie **Fiscal**.</span><span class="sxs-lookup"><span data-stu-id="fd435-137">In the **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="fd435-138">Ajoutez les colonnes suivantes, dans cet ordre :</span><span class="sxs-lookup"><span data-stu-id="fd435-138">Include the following columns in-order:</span></span>  
  
    *  <span data-ttu-id="fd435-139">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="fd435-139">FiscalYear</span></span>
    *  <span data-ttu-id="fd435-140">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="fd435-140">FiscalSemester</span></span>
    *  <span data-ttu-id="fd435-141">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="fd435-141">FiscalQuarter</span></span>
    *  <span data-ttu-id="fd435-142">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="fd435-142">MonthCalendar</span></span>
    *  <span data-ttu-id="fd435-143">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="fd435-143">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="fd435-144">Enfin, dans la table **DimDate**, créez la hiérarchie **ProductionCalendar**.</span><span class="sxs-lookup"><span data-stu-id="fd435-144">Finally, in the **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="fd435-145">Ajoutez les colonnes suivantes, dans cet ordre :</span><span class="sxs-lookup"><span data-stu-id="fd435-145">Include the following columns in-order:</span></span>  
    *  <span data-ttu-id="fd435-146">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="fd435-146">CalendarYear</span></span>
    *  <span data-ttu-id="fd435-147">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="fd435-147">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="fd435-148">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="fd435-148">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="fd435-149">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="fd435-149">What's next?</span></span>
<span data-ttu-id="fd435-150">[Leçon 10 : Créer des partitions](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="fd435-150">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
