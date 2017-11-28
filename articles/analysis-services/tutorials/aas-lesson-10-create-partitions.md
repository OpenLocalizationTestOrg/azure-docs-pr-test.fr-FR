---
<span data-ttu-id="c9ff4-101">titre : aaa « leçon du didacticiel Azure Analysis Services 10 : créer des partitions | Description de Microsoft Docs » : décrit comment toocreate partitions dans le projet du didacticiel hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="c9ff4-102">Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="c9ff4-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="c9ff4-103">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="c9ff4-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="c9ff4-104">Leçon 10 : Créer des partitions</span><span class="sxs-lookup"><span data-stu-id="c9ff4-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="c9ff4-105">Dans cette leçon, vous créer la table FactInternetSales de partitions toodivide hello en parties logiques plus petites qui peuvent être traitée (actualisées) indépendamment d’autres partitions.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="c9ff4-106">Par défaut, chaque table que vous incluez dans votre modèle a une partition, qui inclut les colonnes et lignes de la table du hello.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="c9ff4-107">Pour la table FactInternetSales de hello, nous souhaitons les données de salutation toodivide par année ; une seule partition pour chacune des cinq années de la table hello.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="c9ff4-108">Chaque partition peut ensuite être traitée indépendamment.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="c9ff4-109">toolearn, voir [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="c9ff4-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="c9ff4-110">Estimé temps toocomplete cette leçon : **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="c9ff4-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="c9ff4-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c9ff4-111">Prerequisites</span></span>  
<span data-ttu-id="c9ff4-112">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="c9ff4-113">Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 9 : créer des hiérarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="c9ff4-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="c9ff4-114">Créer des partitions</span><span class="sxs-lookup"><span data-stu-id="c9ff4-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="c9ff4-115">partitions toocreate dans la table FactInternetSales de hello</span><span class="sxs-lookup"><span data-stu-id="c9ff4-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="c9ff4-116">Dans l’Explorateur de modèles tabulaires, développez **Tables**, puis cliquez avec le bouton droit sur **FactInternetSales** > **Partitions**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="c9ff4-117">Dans le Gestionnaire de Partition, cliquez sur **copie**, puis modifiez le nom de hello trop**FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="c9ff4-118">Pour que vous puissiez hello partition tooinclude uniquement les lignes dans une période donnée, pour l’année hello 2010, vous devez modifier l’expression de requête hello.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="c9ff4-119">Cliquez sur **conception** tooopen éditeur de requête, puis cliquez sur hello **FactInternetSales2010** requête.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="c9ff4-120">Dans l’aperçu, cliquez sur hello bas Bonjour **OrderDate** en-tête de colonne, puis cliquez sur **filtres de Date/heure** > **entre**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="c9ff4-122">Dans la boîte de dialogue Filtrer les lignes hello dans **afficher les lignes où : OrderDate**, laissez **est postérieur ou égal à**, puis dans le champ de date hello, entrez **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="c9ff4-123">Laissez hello **et** opérateur sélectionné, puis sélectionnez **avant**, puis, dans le champ de date hello, entrez **1/1/2011**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="c9ff4-125">Dans l’éditeur de requête, sous ÉTAPES APPLIQUÉES, vous voyez une autre étape nommée Lignes filtrées.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="c9ff4-126">Ce filtre est tooselect les dates de commande uniquement à partir de 2010.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="c9ff4-127">Cliquez sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-127">Click **Import**.</span></span>

    <span data-ttu-id="c9ff4-128">Dans le Gestionnaire de Partition, notez que la requête hello expression maintenant comporte une clause de filtrer les lignes supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="c9ff4-130">Cette instruction spécifie que cette partition doit inclure uniquement les données hello dans les lignes où OrderDate de hello est Bonjour année 2010 comme spécifié dans la clause de lignes filtrées hello.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="c9ff4-131">toocreate une partition pour hello année 2011</span><span class="sxs-lookup"><span data-stu-id="c9ff4-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="c9ff4-132">Dans la liste des partitions hello, cliquez sur hello **FactInternetSales2010** de partition que vous avez créé, puis cliquez sur **copie**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="c9ff4-133">Modifier le nom de la partition hello trop**FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="c9ff4-134">Vous n’avez pas besoin de toouse toocreate de l’éditeur de requête une nouvelle clause de lignes filtrées.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="c9ff4-135">Étant donné que vous avez créé une copie de la requête de hello pour 2010, vous devez toodo est apporter une légère modification dans la requête de hello pour 2011.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="c9ff4-136">Dans **Expression de requête**, dans l’ordre pour ce tooinclude partition uniquement les lignes pour hello année 2011, la remplacer les années hello dans la clause de filtrer les lignes hello avec **2011** et **2012**, respectivement, telles que :</span><span class="sxs-lookup"><span data-stu-id="c9ff4-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="c9ff4-137">partitions toocreate pour 2012, 2013 et 2014.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="c9ff4-138">Suivez les étapes précédentes hello, création de partitions pour 2014, la modification des années hello dans hello filtré lignes clause tooinclude uniquement les lignes pour l’année 2012 et 2013.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="c9ff4-139">Supprimer la partition de FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="c9ff4-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="c9ff4-140">Maintenant que vous avez des partitions pour chaque année, vous pouvez supprimer la partition de FactInternetSales hello ; empêche le chevauchement lors du choix de traiter toutes les lors du traitement de partitions.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="c9ff4-141">toodelete hello FactInternetSales partition</span><span class="sxs-lookup"><span data-stu-id="c9ff4-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="c9ff4-142">Cliquez sur la partition FactInternetSales hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="c9ff4-143">Traiter les partitions</span><span class="sxs-lookup"><span data-stu-id="c9ff4-143">Process partitions</span></span>  
<span data-ttu-id="c9ff4-144">Dans le Gestionnaire de Partition, notez hello **traités dernière** colonne pour chacune des partitions hello vous créées montre ces partitions n’ont jamais été traitées.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="c9ff4-145">Lorsque vous créez des partitions, vous devez exécuter un traiter les Partitions ou les données de traiter la Table opération toorefresh hello dans ces partitions.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="c9ff4-146">partitions de FactInternetSales tooprocess hello</span><span class="sxs-lookup"><span data-stu-id="c9ff4-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="c9ff4-147">Cliquez sur **OK** tooclose le Gestionnaire de Partition.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="c9ff4-148">Cliquez sur hello **FactInternetSales** , puis cliquez sur hello **modèle** menu > **processus** > **traiter les Partitions**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="c9ff4-149">Dans la boîte de dialogue traiter les Partitions hello, vérifiez **Mode** est défini trop**traiter par défaut**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="c9ff4-150">Sélectionnez la case à cocher hello Bonjour **processus** colonne pour chacune des hello cinq partitions que vous avez créé, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="c9ff4-152">Si vous êtes invité à entrer des informations d’identification d’emprunt d’identité, entrez le nom d’utilisateur Windows hello et le mot de passe spécifié dans la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="c9ff4-153">Hello **le traitement des données** boîte de dialogue apparaît et affiche les détails du processus pour chaque partition.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="c9ff4-154">Notez que le nombre de lignes transférées est différent pour chaque partition.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="c9ff4-155">Chaque partition contient uniquement les lignes pour l’année hello spécifiée dans la clause WHERE dans l’instruction SQL de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="c9ff4-156">Lorsque le traitement est terminé, continuez et fermer la boîte de dialogue hello le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="c9ff4-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="c9ff4-158">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="c9ff4-158">What's next?</span></span>
<span data-ttu-id="c9ff4-159">Accédez toohello prochaine leçon : [leçon 11 : créer des rôles](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c9ff4-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
