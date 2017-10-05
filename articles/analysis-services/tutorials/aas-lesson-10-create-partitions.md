---
title: "Leçon 10 du didacticiel Azure Analysis Services : Créer des partitions | Microsoft Docs"
description: "Explique comment créer des partitions dans le projet du didacticiel Azure Analysis Services."
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
ms.openlocfilehash: df74d9cbdcf4916c24955e491767589e72389155
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="5de19-103">Leçon 10 : Créer des partitions</span><span class="sxs-lookup"><span data-stu-id="5de19-103">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="5de19-104">Dans cette leçon, vous allez créer des partitions pour diviser la table FactInternetSales en sous-parties logiques qui peuvent être traitées (actualisées) indépendamment des autres partitions.</span><span class="sxs-lookup"><span data-stu-id="5de19-104">In this lesson, you create partitions to divide the FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="5de19-105">Par défaut, chaque table que vous incluez dans votre modèle comporte une partition, qui comprend toutes les colonnes et les lignes de la table.</span><span class="sxs-lookup"><span data-stu-id="5de19-105">By default, every table you include in your model has one partition, which includes all the table’s columns and rows.</span></span> <span data-ttu-id="5de19-106">Pour la table FactInternetSales, nous allons diviser les données en fonction des années, en attribuant une partition pour chaque cinq années.</span><span class="sxs-lookup"><span data-stu-id="5de19-106">For the FactInternetSales table, we want to divide the data by year; one partition for each of the table’s five years.</span></span> <span data-ttu-id="5de19-107">Chaque partition peut ensuite être traitée indépendamment.</span><span class="sxs-lookup"><span data-stu-id="5de19-107">Each partition can then be processed independently.</span></span> <span data-ttu-id="5de19-108">Pour plus d’informations, consultez [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="5de19-108">To learn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="5de19-109">Durée estimée pour suivre cette leçon : **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="5de19-109">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="5de19-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="5de19-110">Prerequisites</span></span>  
<span data-ttu-id="5de19-111">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="5de19-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="5de19-112">Avant d’effectuer les tâches de cette leçon, vous devez avoir terminé la leçon précédente : [Leçon 9 : Créer des hiérarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="5de19-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="5de19-113">Créer des partitions</span><span class="sxs-lookup"><span data-stu-id="5de19-113">Create partitions</span></span>  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a><span data-ttu-id="5de19-114">Pour créer des partitions dans la table FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="5de19-114">To create partitions in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="5de19-115">Dans l’Explorateur de modèles tabulaires, développez **Tables**, puis cliquez avec le bouton droit sur **FactInternetSales** > **Partitions**.</span><span class="sxs-lookup"><span data-stu-id="5de19-115">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="5de19-116">Dans le Gestionnaire de partition, cliquez sur **Copier**, puis remplacez le nom par **FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="5de19-116">In Partition Manager, click **Copy**, and then change the name to **FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="5de19-117">Étant donné que la partition doit inclure uniquement les lignes d’une période donnée (pour l’année 2010), vous devez modifier l’expression de requête.</span><span class="sxs-lookup"><span data-stu-id="5de19-117">Because you want the partition to include only those rows within a certain period, for the year 2010, you must modify the query expression.</span></span>
  
4.  <span data-ttu-id="5de19-118">Cliquez sur **Conception** pour ouvrir l’éditeur de requête, puis cliquez sur la requête **FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="5de19-118">Click **Design** to open Query Editor, and then click the **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="5de19-119">Dans l’aperçu, cliquez sur la flèche vers le bas située dans l’en-tête de colonne **OrderDate**, puis cliquez sur **Filtres de date/heure** > **Entre**.</span><span class="sxs-lookup"><span data-stu-id="5de19-119">In preview, click the down arrow in the **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="5de19-121">Dans la boîte de dialogue Filtrer les lignes, dans **Afficher les lignes où : OrderDate**, conservez **postérieur ou égal à**, puis, dans le champ de date, entrez **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="5de19-121">In the Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in the date field, enter **1/1/2010**.</span></span> <span data-ttu-id="5de19-122">Laissez l’opérateur **And** sélectionné, sélectionnez **avant**, puis, dans le champ de date, entrez **1/1/2011** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5de19-122">Leave the **And** operator selected, then select **is before**, then in the date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="5de19-124">Dans l’éditeur de requête, sous ÉTAPES APPLIQUÉES, vous voyez une autre étape nommée Lignes filtrées.</span><span class="sxs-lookup"><span data-stu-id="5de19-124">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="5de19-125">Ce filtre permet de sélectionner uniquement les dates de commande à partir de 2010.</span><span class="sxs-lookup"><span data-stu-id="5de19-125">This filter is to select only order dates from 2010.</span></span>

8.  <span data-ttu-id="5de19-126">Cliquez sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="5de19-126">Click **Import**.</span></span>

    <span data-ttu-id="5de19-127">Dans le Gestionnaire de partition, notez que l’expression de requête comprend maintenant une clause Lignes filtrées supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="5de19-127">In Partition Manager, notice the query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="5de19-129">Cette instruction spécifie que cette partition doit inclure uniquement les données des lignes pour lesquelles OrderDate correspond à l’année 2010, comme spécifié dans la clause de Lignes filtrées.</span><span class="sxs-lookup"><span data-stu-id="5de19-129">This statement specifies this partition should include only the data in those rows where the OrderDate is in the 2010 calendar year as specified in the filtered rows clause.</span></span>  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a><span data-ttu-id="5de19-130">Pour créer une partition pour l’année 2011</span><span class="sxs-lookup"><span data-stu-id="5de19-130">To create a partition for the 2011 year</span></span>  
  
1.  <span data-ttu-id="5de19-131">Dans la liste des partitions, cliquez sur la partition **FactInternetSales2010** que vous avez créée, puis cliquez sur **Copier**.</span><span class="sxs-lookup"><span data-stu-id="5de19-131">In the partitions list, click the **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="5de19-132">Remplacez le nom de la partition par **FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="5de19-132">Change the partition name to **FactInternetSales2011**.</span></span> 

    <span data-ttu-id="5de19-133">Il est inutile d’utiliser l’éditeur de requête pour créer une autre clause de lignes filtrées.</span><span class="sxs-lookup"><span data-stu-id="5de19-133">You do not need to use Query Editor to create a new filtered rows clause.</span></span> <span data-ttu-id="5de19-134">Étant donné que vous avez créé une copie de la requête pour 2010, seule une légère modification de la requête est nécessaire pour 2011.</span><span class="sxs-lookup"><span data-stu-id="5de19-134">Because you created a copy of the query for 2010, all you need to do is make a slight change in the query for 2011.</span></span>
  
2.  <span data-ttu-id="5de19-135">Dans **Expression de requête**, pour que cette partition inclue uniquement les lignes de l’année 2011, remplacez les années de la clause de lignes filtrées par **2011** et **2012**, respectivement, comme ceci :</span><span class="sxs-lookup"><span data-stu-id="5de19-135">In **Query Expression**, in-order for this partition to include only those rows for the 2011 year, replace the years in the Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="5de19-136">Pour créer des partitions pour 2012, 2013 et 2014.</span><span class="sxs-lookup"><span data-stu-id="5de19-136">To create partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="5de19-137">Suivez les étapes précédentes, en créant des partitions pour 2012, 2013 et 2014, puis en modifiant les années de la clause Lignes filtrées de manière à inclure uniquement les lignes de cette année.</span><span class="sxs-lookup"><span data-stu-id="5de19-137">Follow the previous steps, creating partitions for 2012, 2013, and 2014, changing the years in the Filtered Rows clause to include only rows for that year.</span></span> 
  

## <a name="delete-the-factinternetsales-partition"></a><span data-ttu-id="5de19-138">Supprimer la partition FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="5de19-138">Delete the FactInternetSales partition</span></span>
<span data-ttu-id="5de19-139">Maintenant que vous avez des partitions pour chaque année, vous pouvez supprimer la partition FactInternetSales, ce qui va éviter un chevauchement lorsque vous choisirez l’option Traiter tout.</span><span class="sxs-lookup"><span data-stu-id="5de19-139">Now that you have partitions for each year, you can delete the FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="to-delete-the-factinternetsales-partition"></a><span data-ttu-id="5de19-140">Pour supprimer la partition FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="5de19-140">To delete the FactInternetSales partition</span></span>
-  <span data-ttu-id="5de19-141">Cliquez sur la partition FactInternetSales, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="5de19-141">Click the FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="5de19-142">Traiter les partitions</span><span class="sxs-lookup"><span data-stu-id="5de19-142">Process partitions</span></span>  
<span data-ttu-id="5de19-143">Dans le Gestionnaire de partition, notez que la colonne **Dernier traitement** de chacune des partitions créées montre que ces partitions n’ont jamais été traitées.</span><span class="sxs-lookup"><span data-stu-id="5de19-143">In Partition Manager, notice the **Last Processed** column for each of the new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="5de19-144">Lorsque vous créez des partitions, vous devez exécuter l’opération Traiter les partitions ou Traiter la table pour actualiser les données de ces partitions.</span><span class="sxs-lookup"><span data-stu-id="5de19-144">When you create partitions, you should run a Process Partitions or Process Table operation to refresh the data in those partitions.</span></span>  
  
#### <a name="to-process-the-factinternetsales-partitions"></a><span data-ttu-id="5de19-145">Pour traiter les partitions FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="5de19-145">To process the FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="5de19-146">Cliquez sur **OK** pour fermer le Gestionnaire de partition.</span><span class="sxs-lookup"><span data-stu-id="5de19-146">Click **OK** to close Partition Manager.</span></span>  
  
2.  <span data-ttu-id="5de19-147">Cliquez sur la table **FactInternetSales**, puis cliquez sur le menu **Modèle** > **Processus** > **Traiter les partitions**.</span><span class="sxs-lookup"><span data-stu-id="5de19-147">Click the **FactInternetSales** table, then click the **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="5de19-148">Dans la boîte de dialogue Traiter les partitions, vérifiez que **Mode** est défini sur **Traiter par défaut**.</span><span class="sxs-lookup"><span data-stu-id="5de19-148">In the Process Partitions dialog box, verify **Mode** is set to **Process Default**.</span></span>  
  
4.  <span data-ttu-id="5de19-149">Cochez la case située dans la colonne **Processus** pour chacune des cinq partitions que vous avez créées, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5de19-149">Select the checkbox in the **Process** column for each of the five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="5de19-151">Si vous êtes invité à entrer des informations d’identification d’emprunt d’identité, entrez le nom d’utilisateur Windows et le mot de passe spécifiés dans la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="5de19-151">If you're prompted for Impersonation credentials, enter the Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="5de19-152">La boîte de dialogue **Traitement des données** s’affiche et montre les détails du processus pour chaque partition.</span><span class="sxs-lookup"><span data-stu-id="5de19-152">The **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="5de19-153">Notez que le nombre de lignes transférées est différent pour chaque partition.</span><span class="sxs-lookup"><span data-stu-id="5de19-153">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="5de19-154">Chaque partition contient uniquement les lignes de l’année spécifiée dans la clause WHERE de l’instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="5de19-154">Each partition includes only those rows for the year specified in the WHERE clause in the SQL Statement.</span></span> <span data-ttu-id="5de19-155">Lorsque le traitement est terminé, fermez la boîte de dialogue Traitement des données.</span><span class="sxs-lookup"><span data-stu-id="5de19-155">When processing is finished, go ahead and close the Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="5de19-157">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="5de19-157">What's next?</span></span>
<span data-ttu-id="5de19-158">Accédez à la leçon suivante : [Leçon 11 : Créer des rôles](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5de19-158">Go to the next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
