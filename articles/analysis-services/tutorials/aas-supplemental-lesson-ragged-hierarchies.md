---
<span data-ttu-id="8b859-101">titre : aaa « leçon supplémentaire du didacticiel Azure Analysis Services : les hiérarchies irrégulières | Description de Microsoft Docs » : décrit comment toofix les hiérarchies déséquilibrées dans hello Azure Analysis Services tutorial.</span><span class="sxs-lookup"><span data-stu-id="8b859-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="8b859-102">Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="8b859-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="8b859-103">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="8b859-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="8b859-104">Leçon supplémentaire – Hiérarchies déséquilibrées</span><span class="sxs-lookup"><span data-stu-id="8b859-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="8b859-105">Dans cette leçon supplémentaire, vous allez résoudre un problème courant se produisant lors de l’ajout d’un tableau croisé dynamique sur des hiérarchies qui contiennent des valeurs vides (membres) à différents niveaux.</span><span class="sxs-lookup"><span data-stu-id="8b859-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="8b859-106">Par exemple, une organisation où un cadre a à la fois des responsables de département et des non-cadres comme collaborateurs.</span><span class="sxs-lookup"><span data-stu-id="8b859-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="8b859-107">Ou bien des hiérarchies géographiques composées des éléments Pays-Région-Ville, où certaines villes n’ont pas d’état ou de région parent, par exemple Washington D.C. ou la Cité du Vatican.</span><span class="sxs-lookup"><span data-stu-id="8b859-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="8b859-108">Lorsqu’une hiérarchie possède des membres vides, il souvent descend toodifferent ou déséquilibrée, les niveaux.</span><span class="sxs-lookup"><span data-stu-id="8b859-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="8b859-110">Les modèles tabulaires au niveau de compatibilité hello 1400 possèdent un autre **masquer les membres** propriété pour les hiérarchies.</span><span class="sxs-lookup"><span data-stu-id="8b859-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="8b859-111">Hello **par défaut** paramètre qu’il n’y aucun membre vide n’importe quel niveau.</span><span class="sxs-lookup"><span data-stu-id="8b859-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="8b859-112">Hello **masquer les membres vides** paramètre exclut vides à partir de la hiérarchie hello lors de l’ajout tooa tableau croisé dynamique ou un rapport.</span><span class="sxs-lookup"><span data-stu-id="8b859-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="8b859-113">Estimé temps toocomplete cette leçon : **20 minutes**</span><span class="sxs-lookup"><span data-stu-id="8b859-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="8b859-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8b859-114">Prerequisites</span></span>  
<span data-ttu-id="8b859-115">Cette rubrique de leçon supplémentaire fait partie d’un didacticiel de modélisation tabulaire.</span><span class="sxs-lookup"><span data-stu-id="8b859-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="8b859-116">Avant d’effectuer les tâches de hello dans cette leçon supplémentaire, vous devez avoir terminé toutes les leçons précédentes ou avoir un projet de modèle d’exemple Adventure Works Internet Sales terminé.</span><span class="sxs-lookup"><span data-stu-id="8b859-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="8b859-117">Si vous avez créé le projet de AW Internet Sales hello dans le cadre du didacticiel de hello, votre modèle ne contient pas encore toutes les données ou les hiérarchies irrégulières.</span><span class="sxs-lookup"><span data-stu-id="8b859-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="8b859-118">toocomplete cette leçon supplémentaire, vous devez toocreate hello problème en ajoutant des tables supplémentaires, créez des relations, les colonnes calculées, une mesure et une hiérarchie d’organisation.</span><span class="sxs-lookup"><span data-stu-id="8b859-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="8b859-119">Cette partie prend environ 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="8b859-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="8b859-120">Ensuite, vous obtenez toosolve dans quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="8b859-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="8b859-121">Ajouter des tables et des objets</span><span class="sxs-lookup"><span data-stu-id="8b859-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="8b859-122">nouveau modèle de tooyour tables tooadd</span><span class="sxs-lookup"><span data-stu-id="8b859-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="8b859-123">Dans l’Explorateur de modèles tabulaires, développez **Sources de données**, puis cliquez avec le bouton droit sur votre connexion > **Importer de nouvelles tables**.</span><span class="sxs-lookup"><span data-stu-id="8b859-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="8b859-124">Dans le navigateur, sélectionnez **DimEmployee** et **FactResellerSales**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b859-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="8b859-125">Dans l’éditeur de requête, cliquez sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="8b859-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="8b859-126">Créer hello [relations](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="8b859-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="8b859-127">Table 1</span><span class="sxs-lookup"><span data-stu-id="8b859-127">Table 1</span></span>           | <span data-ttu-id="8b859-128">Colonne</span><span class="sxs-lookup"><span data-stu-id="8b859-128">Column</span></span>       | <span data-ttu-id="8b859-129">Direction du filtre</span><span class="sxs-lookup"><span data-stu-id="8b859-129">Filter Direction</span></span>   | <span data-ttu-id="8b859-130">Table 2</span><span class="sxs-lookup"><span data-stu-id="8b859-130">Table 2</span></span>     | <span data-ttu-id="8b859-131">Colonne</span><span class="sxs-lookup"><span data-stu-id="8b859-131">Column</span></span>      | <span data-ttu-id="8b859-132">Actif</span><span class="sxs-lookup"><span data-stu-id="8b859-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="8b859-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8b859-133">FactResellerSales</span></span> | <span data-ttu-id="8b859-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="8b859-134">OrderDateKey</span></span> | <span data-ttu-id="8b859-135">Par défaut</span><span class="sxs-lookup"><span data-stu-id="8b859-135">Default</span></span>            | <span data-ttu-id="8b859-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="8b859-136">DimDate</span></span>     | <span data-ttu-id="8b859-137">Date</span><span class="sxs-lookup"><span data-stu-id="8b859-137">Date</span></span>        | <span data-ttu-id="8b859-138">Oui</span><span class="sxs-lookup"><span data-stu-id="8b859-138">Yes</span></span>    |
    | <span data-ttu-id="8b859-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8b859-139">FactResellerSales</span></span> | <span data-ttu-id="8b859-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="8b859-140">DueDate</span></span>      | <span data-ttu-id="8b859-141">Par défaut</span><span class="sxs-lookup"><span data-stu-id="8b859-141">Default</span></span>            | <span data-ttu-id="8b859-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="8b859-142">DimDate</span></span>     | <span data-ttu-id="8b859-143">Date</span><span class="sxs-lookup"><span data-stu-id="8b859-143">Date</span></span>        | <span data-ttu-id="8b859-144">Non</span><span class="sxs-lookup"><span data-stu-id="8b859-144">No</span></span>     |
    | <span data-ttu-id="8b859-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8b859-145">FactResellerSales</span></span> | <span data-ttu-id="8b859-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="8b859-146">ShipDateKey</span></span>  | <span data-ttu-id="8b859-147">Par défaut</span><span class="sxs-lookup"><span data-stu-id="8b859-147">Default</span></span>            | <span data-ttu-id="8b859-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="8b859-148">DimDate</span></span>     | <span data-ttu-id="8b859-149">Date</span><span class="sxs-lookup"><span data-stu-id="8b859-149">Date</span></span>        | <span data-ttu-id="8b859-150">Non</span><span class="sxs-lookup"><span data-stu-id="8b859-150">No</span></span>     |
    | <span data-ttu-id="8b859-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8b859-151">FactResellerSales</span></span> | <span data-ttu-id="8b859-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="8b859-152">ProductKey</span></span>   | <span data-ttu-id="8b859-153">Par défaut</span><span class="sxs-lookup"><span data-stu-id="8b859-153">Default</span></span>            | <span data-ttu-id="8b859-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="8b859-154">DimProduct</span></span>  | <span data-ttu-id="8b859-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="8b859-155">ProductKey</span></span>  | <span data-ttu-id="8b859-156">Oui</span><span class="sxs-lookup"><span data-stu-id="8b859-156">Yes</span></span>    |
    | <span data-ttu-id="8b859-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8b859-157">FactResellerSales</span></span> | <span data-ttu-id="8b859-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="8b859-158">EmployeeKey</span></span>  | <span data-ttu-id="8b859-159">Tables tooBoth</span><span class="sxs-lookup"><span data-stu-id="8b859-159">tooBoth Tables</span></span> | <span data-ttu-id="8b859-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="8b859-160">DimEmployee</span></span> | <span data-ttu-id="8b859-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="8b859-161">EmployeeKey</span></span> | <span data-ttu-id="8b859-162">Oui</span><span class="sxs-lookup"><span data-stu-id="8b859-162">Yes</span></span>    |

5. <span data-ttu-id="8b859-163">Bonjour **DimEmployee** table, créer hello [des colonnes calculées](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="8b859-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="8b859-164">**Chemin d’accès**</span><span class="sxs-lookup"><span data-stu-id="8b859-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="8b859-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="8b859-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="8b859-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="8b859-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="8b859-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="8b859-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="8b859-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="8b859-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="8b859-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="8b859-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="8b859-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="8b859-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="8b859-171">Bonjour **DimEmployee** table, créez un [hiérarchie](../tutorials/aas-lesson-9-create-hierarchies.md) nommé **organisation**.</span><span class="sxs-lookup"><span data-stu-id="8b859-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="8b859-172">Ajouter hello suivant des colonnes dans l’ordre : **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="8b859-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="8b859-173">Bonjour **FactResellerSales** table, créer hello [mesure](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="8b859-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="8b859-174">Utilisez [analyser dans Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel et de créer automatiquement un tableau croisé dynamique.</span><span class="sxs-lookup"><span data-stu-id="8b859-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="8b859-175">Dans **PivotTable Fields**, ajouter hello **organisation** hiérarchie à partir de hello **DimEmployee** table trop**lignes**et hello **ResellerTotalSales** mesure hello **FactResellerSales** table trop**valeurs**.</span><span class="sxs-lookup"><span data-stu-id="8b859-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="8b859-177">Comme vous pouvez le voir dans le tableau croisé dynamique de hello, hiérarchie de hello affiche les lignes qui sont décalés.</span><span class="sxs-lookup"><span data-stu-id="8b859-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="8b859-178">Il y a de nombreuses lignes où des membres vides sont affichés.</span><span class="sxs-lookup"><span data-stu-id="8b859-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="8b859-179">hiérarchie irrégulière de toofix hello en définissant les membres de masquer hello propriété</span><span class="sxs-lookup"><span data-stu-id="8b859-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="8b859-180">Dans l’**Explorateur de modèles tabulaires**, développez **Tables** > **DimEmployee** > **Hiérarchies** > **Organization**.</span><span class="sxs-lookup"><span data-stu-id="8b859-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="8b859-181">Dans **Propriétés** > **Masquer les membres**, sélectionnez **Masquer les membres vides**.</span><span class="sxs-lookup"><span data-stu-id="8b859-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="8b859-183">Dans Excel, actualiser hello tableau croisé dynamique.</span><span class="sxs-lookup"><span data-stu-id="8b859-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="8b859-185">Voilà qui est beaucoup mieux !</span><span class="sxs-lookup"><span data-stu-id="8b859-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="8b859-186">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8b859-186">See Also</span></span>   
[<span data-ttu-id="8b859-187">Leçon 9 : Créer des hiérarchies</span><span class="sxs-lookup"><span data-stu-id="8b859-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="8b859-188">Leçon supplémentaire – Sécurité dynamique</span><span class="sxs-lookup"><span data-stu-id="8b859-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="8b859-189">Leçon supplémentaire – Lignes de détails</span><span class="sxs-lookup"><span data-stu-id="8b859-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  