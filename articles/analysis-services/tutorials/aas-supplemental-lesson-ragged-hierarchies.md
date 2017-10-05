---
title: "Leçon supplémentaire du didacticiel Azure Analysis Services : Hiérarchies déséquilibrées | Microsoft Docs"
description: "Décrit comment corriger les hiérarchies déséquilibrées dans le didacticiel Azure Analysis Services."
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
ms.openlocfilehash: 0f02ff73eb126cc397312e87bde50b3ee2d6ce53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="2802d-103">Leçon supplémentaire – Hiérarchies déséquilibrées</span><span class="sxs-lookup"><span data-stu-id="2802d-103">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="2802d-104">Dans cette leçon supplémentaire, vous allez résoudre un problème courant se produisant lors de l’ajout d’un tableau croisé dynamique sur des hiérarchies qui contiennent des valeurs vides (membres) à différents niveaux.</span><span class="sxs-lookup"><span data-stu-id="2802d-104">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="2802d-105">Par exemple, une organisation où un cadre a à la fois des responsables de département et des non-cadres comme collaborateurs.</span><span class="sxs-lookup"><span data-stu-id="2802d-105">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="2802d-106">Ou bien des hiérarchies géographiques composées des éléments Pays-Région-Ville, où certaines villes n’ont pas d’état ou de région parent, par exemple Washington D.C. ou la Cité du Vatican.</span><span class="sxs-lookup"><span data-stu-id="2802d-106">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="2802d-107">Quand une hiérarchie a des membres vides, elle descend souvent à des niveaux différents ou déséquilibrés.</span><span class="sxs-lookup"><span data-stu-id="2802d-107">When a hierarchy has blank members, it often descends to different, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="2802d-109">Les modèles tabulaires de niveau de compatibilité 1400 disposent d’une propriété **Masquer les membres** supplémentaire pour les hiérarchies.</span><span class="sxs-lookup"><span data-stu-id="2802d-109">Tabular models at the 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="2802d-110">Le paramètre **Par défaut** suppose qu’il n’y a aucun membre vide à aucun niveau.</span><span class="sxs-lookup"><span data-stu-id="2802d-110">The **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="2802d-111">Le paramètre **Masquer les membres vides** exclut les membres vides de la hiérarchie quand ils sont ajoutés à un tableau croisé dynamique ou à un rapport.</span><span class="sxs-lookup"><span data-stu-id="2802d-111">The **Hide blank members** setting excludes blank members from the hierarchy when added to a PivotTable or report.</span></span>  
  
<span data-ttu-id="2802d-112">Durée estimée pour suivre cette leçon : **20 minutes**</span><span class="sxs-lookup"><span data-stu-id="2802d-112">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="2802d-113">Prérequis</span><span class="sxs-lookup"><span data-stu-id="2802d-113">Prerequisites</span></span>  
<span data-ttu-id="2802d-114">Cette rubrique de leçon supplémentaire fait partie d’un didacticiel de modélisation tabulaire.</span><span class="sxs-lookup"><span data-stu-id="2802d-114">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="2802d-115">Avant d’effectuer les tâches de cette leçon supplémentaire, vous devez avoir effectué toutes les leçons précédentes ou disposer d’un exemple de projet de modèle de ventes sur Internet Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="2802d-115">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="2802d-116">Si vous avez créé le projet de ventes sur Internet AW dans le cadre du didacticiel, votre modèle ne contient encore aucune donnée ou hiérarchie déséquilibrée.</span><span class="sxs-lookup"><span data-stu-id="2802d-116">If you've created the AW Internet Sales project as part of the tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="2802d-117">Pour suivre cette leçon supplémentaire, vous devez d’abord créer le problème en ajoutant des tables supplémentaires, puis créer des relations, des colonnes calculées, une mesure et une hiérarchie d’organisation.</span><span class="sxs-lookup"><span data-stu-id="2802d-117">To complete this supplemental lesson, you first have to create the problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="2802d-118">Cette partie prend environ 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="2802d-118">That part takes about 15 minutes.</span></span> <span data-ttu-id="2802d-119">Ensuite, vous allez résoudre le problème en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="2802d-119">Then, you get to solve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="2802d-120">Ajouter des tables et des objets</span><span class="sxs-lookup"><span data-stu-id="2802d-120">Add tables and objects</span></span>
  
### <a name="to-add-new-tables-to-your-model"></a><span data-ttu-id="2802d-121">Pour ajouter de nouvelles tables à votre modèle</span><span class="sxs-lookup"><span data-stu-id="2802d-121">To add new tables to your model</span></span>
  
1.  <span data-ttu-id="2802d-122">Dans l’Explorateur de modèles tabulaires, développez **Sources de données**, puis cliquez avec le bouton droit sur votre connexion > **Importer de nouvelles tables**.</span><span class="sxs-lookup"><span data-stu-id="2802d-122">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="2802d-123">Dans le navigateur, sélectionnez **DimEmployee** et **FactResellerSales**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2802d-123">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="2802d-124">Dans l’éditeur de requête, cliquez sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="2802d-124">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="2802d-125">Créez les [relations](../tutorials/aas-lesson-4-create-relationships.md) suivantes :</span><span class="sxs-lookup"><span data-stu-id="2802d-125">Create the following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="2802d-126">Table 1</span><span class="sxs-lookup"><span data-stu-id="2802d-126">Table 1</span></span>           | <span data-ttu-id="2802d-127">Colonne</span><span class="sxs-lookup"><span data-stu-id="2802d-127">Column</span></span>       | <span data-ttu-id="2802d-128">Direction du filtre</span><span class="sxs-lookup"><span data-stu-id="2802d-128">Filter Direction</span></span>   | <span data-ttu-id="2802d-129">Table 2</span><span class="sxs-lookup"><span data-stu-id="2802d-129">Table 2</span></span>     | <span data-ttu-id="2802d-130">Colonne</span><span class="sxs-lookup"><span data-stu-id="2802d-130">Column</span></span>      | <span data-ttu-id="2802d-131">Actif</span><span class="sxs-lookup"><span data-stu-id="2802d-131">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="2802d-132">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2802d-132">FactResellerSales</span></span> | <span data-ttu-id="2802d-133">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="2802d-133">OrderDateKey</span></span> | <span data-ttu-id="2802d-134">Par défaut</span><span class="sxs-lookup"><span data-stu-id="2802d-134">Default</span></span>            | <span data-ttu-id="2802d-135">DimDate</span><span class="sxs-lookup"><span data-stu-id="2802d-135">DimDate</span></span>     | <span data-ttu-id="2802d-136">Date</span><span class="sxs-lookup"><span data-stu-id="2802d-136">Date</span></span>        | <span data-ttu-id="2802d-137">Oui</span><span class="sxs-lookup"><span data-stu-id="2802d-137">Yes</span></span>    |
    | <span data-ttu-id="2802d-138">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2802d-138">FactResellerSales</span></span> | <span data-ttu-id="2802d-139">DueDate</span><span class="sxs-lookup"><span data-stu-id="2802d-139">DueDate</span></span>      | <span data-ttu-id="2802d-140">Par défaut</span><span class="sxs-lookup"><span data-stu-id="2802d-140">Default</span></span>            | <span data-ttu-id="2802d-141">DimDate</span><span class="sxs-lookup"><span data-stu-id="2802d-141">DimDate</span></span>     | <span data-ttu-id="2802d-142">Date</span><span class="sxs-lookup"><span data-stu-id="2802d-142">Date</span></span>        | <span data-ttu-id="2802d-143">Non</span><span class="sxs-lookup"><span data-stu-id="2802d-143">No</span></span>     |
    | <span data-ttu-id="2802d-144">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2802d-144">FactResellerSales</span></span> | <span data-ttu-id="2802d-145">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="2802d-145">ShipDateKey</span></span>  | <span data-ttu-id="2802d-146">Par défaut</span><span class="sxs-lookup"><span data-stu-id="2802d-146">Default</span></span>            | <span data-ttu-id="2802d-147">DimDate</span><span class="sxs-lookup"><span data-stu-id="2802d-147">DimDate</span></span>     | <span data-ttu-id="2802d-148">Date</span><span class="sxs-lookup"><span data-stu-id="2802d-148">Date</span></span>        | <span data-ttu-id="2802d-149">Non</span><span class="sxs-lookup"><span data-stu-id="2802d-149">No</span></span>     |
    | <span data-ttu-id="2802d-150">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2802d-150">FactResellerSales</span></span> | <span data-ttu-id="2802d-151">ProductKey</span><span class="sxs-lookup"><span data-stu-id="2802d-151">ProductKey</span></span>   | <span data-ttu-id="2802d-152">Par défaut</span><span class="sxs-lookup"><span data-stu-id="2802d-152">Default</span></span>            | <span data-ttu-id="2802d-153">DimProduct</span><span class="sxs-lookup"><span data-stu-id="2802d-153">DimProduct</span></span>  | <span data-ttu-id="2802d-154">ProductKey</span><span class="sxs-lookup"><span data-stu-id="2802d-154">ProductKey</span></span>  | <span data-ttu-id="2802d-155">Oui</span><span class="sxs-lookup"><span data-stu-id="2802d-155">Yes</span></span>    |
    | <span data-ttu-id="2802d-156">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2802d-156">FactResellerSales</span></span> | <span data-ttu-id="2802d-157">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="2802d-157">EmployeeKey</span></span>  | <span data-ttu-id="2802d-158">Vers les deux tables</span><span class="sxs-lookup"><span data-stu-id="2802d-158">To Both Tables</span></span> | <span data-ttu-id="2802d-159">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="2802d-159">DimEmployee</span></span> | <span data-ttu-id="2802d-160">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="2802d-160">EmployeeKey</span></span> | <span data-ttu-id="2802d-161">Oui</span><span class="sxs-lookup"><span data-stu-id="2802d-161">Yes</span></span>    |

5. <span data-ttu-id="2802d-162">Dans la table **DimEmployee**, créez les [colonnes calculées](../tutorials/aas-lesson-5-create-calculated-columns.md) suivantes :</span><span class="sxs-lookup"><span data-stu-id="2802d-162">In the **DimEmployee** table, create the following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="2802d-163">**Path**</span><span class="sxs-lookup"><span data-stu-id="2802d-163">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="2802d-164">**FullName**</span><span class="sxs-lookup"><span data-stu-id="2802d-164">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="2802d-165">**Level1**</span><span class="sxs-lookup"><span data-stu-id="2802d-165">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="2802d-166">**Level2**</span><span class="sxs-lookup"><span data-stu-id="2802d-166">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="2802d-167">**Level3**</span><span class="sxs-lookup"><span data-stu-id="2802d-167">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="2802d-168">**Level4**</span><span class="sxs-lookup"><span data-stu-id="2802d-168">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="2802d-169">**Level5**</span><span class="sxs-lookup"><span data-stu-id="2802d-169">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="2802d-170">Dans la table **DimEmployee**, créez une [hiérarchie](../tutorials/aas-lesson-9-create-hierarchies.md) nommée **Organization**.</span><span class="sxs-lookup"><span data-stu-id="2802d-170">In the **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="2802d-171">Ajoutez les colonnes suivantes, dans l’ordre : **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="2802d-171">Add the following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="2802d-172">Dans la table **FactResellerSales**, créez la [mesure](../tutorials/aas-lesson-6-create-measures.md) suivante :</span><span class="sxs-lookup"><span data-stu-id="2802d-172">In the **FactResellerSales** table, create the following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="2802d-173">Utilisez [Analyser dans Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) pour ouvrir Excel et créer automatiquement un tableau croisé dynamique.</span><span class="sxs-lookup"><span data-stu-id="2802d-173">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) to open Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="2802d-174">Dans **Champs de tableau croisé dynamique**, ajoutez la hiérarchie **Organization** de la table **DimEmployee** à **Lignes** et la mesure **ResellerTotalSales** de la table **FactResellerSales** à **Valeurs**.</span><span class="sxs-lookup"><span data-stu-id="2802d-174">In **PivotTable Fields**, add the **Organization** hierarchy from the **DimEmployee** table to **Rows**, and the **ResellerTotalSales** measure from the **FactResellerSales**  table to **Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="2802d-176">Comme vous pouvez le voir dans le tableau croisé dynamique, la hiérarchie affiche les lignes qui sont déséquilibrées.</span><span class="sxs-lookup"><span data-stu-id="2802d-176">As you can see in the PivotTable, the hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="2802d-177">Il y a de nombreuses lignes où des membres vides sont affichés.</span><span class="sxs-lookup"><span data-stu-id="2802d-177">There are many rows where blank members are shown.</span></span>

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a><span data-ttu-id="2802d-178">Pour corriger la hiérarchie déséquilibrée en définissant la propriété Masquer les membres</span><span class="sxs-lookup"><span data-stu-id="2802d-178">To fix the ragged hierarchy by setting the Hide members property</span></span>

1.  <span data-ttu-id="2802d-179">Dans l’**Explorateur de modèles tabulaires**, développez **Tables** > **DimEmployee** > **Hiérarchies** > **Organization**.</span><span class="sxs-lookup"><span data-stu-id="2802d-179">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="2802d-180">Dans **Propriétés** > **Masquer les membres**, sélectionnez **Masquer les membres vides**.</span><span class="sxs-lookup"><span data-stu-id="2802d-180">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="2802d-182">De retour dans Excel, actualisez le tableau croisé dynamique.</span><span class="sxs-lookup"><span data-stu-id="2802d-182">Back in Excel, refresh the PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="2802d-184">Voilà qui est beaucoup mieux !</span><span class="sxs-lookup"><span data-stu-id="2802d-184">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="2802d-185">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2802d-185">See Also</span></span>   
[<span data-ttu-id="2802d-186">Leçon 9 : Créer des hiérarchies</span><span class="sxs-lookup"><span data-stu-id="2802d-186">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="2802d-187">Leçon supplémentaire – Sécurité dynamique</span><span class="sxs-lookup"><span data-stu-id="2802d-187">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="2802d-188">Leçon supplémentaire – Lignes de détails</span><span class="sxs-lookup"><span data-stu-id="2802d-188">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  