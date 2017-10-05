---
title: "Copie répétable dans Azure Data Factory | Microsoft Docs"
description: "Découvrez comment éviter les doublons, même si une tranche qui copie des données est exécutée plusieurs fois."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 5b88a235915bf35fec701eee4a5f80beb4a67632
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="b5fb6-103">Copie répétable dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b5fb6-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="b5fb6-104">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="b5fb6-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="b5fb6-105">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="b5fb6-106">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b5fb6-107">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="b5fb6-108">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="b5fb6-109">Les exemples suivants concernent SQL Azure, mais sont applicables à tout autre magasin de données prenant en charge les jeux de données rectangulaires.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="b5fb6-110">Vous pouvez avoir besoin d’ajuster le **type** de source et la propriété de **requête** (par exemple : query au lieu de sqlReaderQuery) pour le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="b5fb6-111">En général, vous souhaitez lire uniquement les données des magasins relationnels qui correspondent à cette tranche.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="b5fb6-112">Pour cela, vous pouvez utiliser les variables système WindowStart et WindowEnd disponibles dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="b5fb6-113">Pour en savoir plus sur les variables et les fonctions dans Azure Data Factory, lisez l’article intitulé [Azure Data Factory - Variables système et fonctions](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="b5fb6-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="b5fb6-114">Exemple :</span><span class="sxs-lookup"><span data-stu-id="b5fb6-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="b5fb6-115">Cette requête lit des données qui figurent dans la plage de durée de tranche (WindowStart -> WindowEnd) à partir de la table MyTable.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="b5fb6-116">Par ailleurs, la réexécution de cette tranche garantit toujours la lecture des mêmes données.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="b5fb6-117">Dans d’autres cas, vous souhaitez lire l’intégralité de la table. Vous pouvez alors définir sqlReaderQuery comme suit :</span><span class="sxs-lookup"><span data-stu-id="b5fb6-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="b5fb6-118">Écriture répétable dans SqlSink</span><span class="sxs-lookup"><span data-stu-id="b5fb6-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="b5fb6-119">Lors de la copie de données vers **SQL Azure/SQL Server** à partir d’autres magasins de données, vous devez garder la répétabilité à l’esprit afin d’éviter des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="b5fb6-120">Lors de la copie de données sur une base de données Azure SQL/SQL Server, l’activité de copie ajoute des données à la table de récepteur par défaut.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="b5fb6-121">Par exemple, vous copiez des données à partir d’un fichier CSV (valeurs séparées par des virgules) contenant deux enregistrements et les collez dans la table suivante d’une base de données Azure SQL/SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="b5fb6-122">Lorsqu’une tranche est exécutée, les deux enregistrements sont copiés dans la table SQL.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="b5fb6-123">Supposons que vous trouviez des erreurs dans le fichier source et mettiez à jour la quantité de Down Tube, la faisant passer de 2 à 4.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="b5fb6-124">Si vous réexécutez manuellement la tranche de données pour cette période, vous trouvez deux nouveaux enregistrements ajoutés à la base de données SQL Azure/SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="b5fb6-125">Cet exemple suppose qu’aucune des colonnes de la table ne présente de contrainte de clé primaire.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="b5fb6-126">Pour éviter ce problème, vous devez spécifier la sémantique UPSERT en utilisant l’une des deux mécanismes suivants :</span><span class="sxs-lookup"><span data-stu-id="b5fb6-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="b5fb6-127">Mécanisme 1 : utilisation de la propriété sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="b5fb6-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="b5fb6-128">Vous pouvez utiliser la propriété **sqlWriterCleanupScript** pour nettoyer les données à partir de la table du récepteur avant d’insérer les données lors de l’exécution d’une tranche.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="b5fb6-129">Lorsqu’une tranche s’exécute, le script de nettoyage est d’abord exécuté pour supprimer les données correspondant à la tranche dans la table SQL.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="b5fb6-130">Ensuite, l’activité de copie insère les données dans la table SQL.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="b5fb6-131">Si la tranche est réexécutée, la quantité est mise à jour comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="b5fb6-132">Supposons que l’enregistrement Flat Washer soit supprimé du fichier csv d’origine.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="b5fb6-133">Une nouvelle exécution de la tranche entraînerait le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="b5fb6-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="b5fb6-134">L’activité de copie a exécuté le script de nettoyage pour supprimer les données correspondant à cette tranche.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="b5fb6-135">Elle a ensuite lu l’entrée du fichier csv (qui ne contenait qu’un enregistrement) avant de l’insérer dans la table.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="b5fb6-136">Mécanisme 2 : utilisation du paramètre sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="b5fb6-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b5fb6-137">Pour le moment, le paramètre sliceIdentifierColumnName n’est pas pris en charge par Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="b5fb6-138">Un deuxième mécanisme pour obtenir la répétabilité consiste à disposer d’une colonne dédiée (sliceIdentifierColumnName) dans la table cible.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="b5fb6-139">Cette colonne peut être utilisée par Azure Data Factory pour s’assurer que la source et la destination restent synchronisées.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="b5fb6-140">Cette approche fonctionne s’il existe une flexibilité dans la modification ou la définition du schéma de table SQL de destination.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="b5fb6-141">Cette colonne est utilisée par Azure Data Factory à des fins de répétabilité. Au cours du processus, Azure Data Factory n’apporte aucune modification de schéma à la table.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="b5fb6-142">Façon d’utiliser cette approche :</span><span class="sxs-lookup"><span data-stu-id="b5fb6-142">Way to use this approach:</span></span>

1. <span data-ttu-id="b5fb6-143">Définissez une colonne de type **binaire (32)** dans la table SQL de destination.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="b5fb6-144">Aucune contrainte ne doit exister sur cette colonne.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-144">There should be no constraints on this column.</span></span> <span data-ttu-id="b5fb6-145">Pour les besoins de cet exemple, nommons cette colonne « AdfSliceIdentifier ».</span><span class="sxs-lookup"><span data-stu-id="b5fb6-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="b5fb6-146">Table source :</span><span class="sxs-lookup"><span data-stu-id="b5fb6-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="b5fb6-147">Table de destination :</span><span class="sxs-lookup"><span data-stu-id="b5fb6-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="b5fb6-148">Utilisez-la dans l’activité de copie comme suit :</span><span class="sxs-lookup"><span data-stu-id="b5fb6-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="b5fb6-149">Azure Data Factory renseigne cette colonne conformément à ses besoins pour s’assurer que la source et la destination restent synchronisées.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="b5fb6-150">Les valeurs de cette colonne ne doivent pas être utilisées en dehors de ce contexte.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="b5fb6-151">Comme pour le mécanisme 1, l’activité de copie nettoie automatiquement les données de la tranche spécifiée dans la table SQL de destination.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="b5fb6-152">Ensuite, elle insère les données de la source dans la table de destination.</span><span class="sxs-lookup"><span data-stu-id="b5fb6-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b5fb6-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b5fb6-153">Next steps</span></span>
<span data-ttu-id="b5fb6-154">Pour accéder à des exemples JSON complets, consultez les articles suivants sur les connecteurs :</span><span class="sxs-lookup"><span data-stu-id="b5fb6-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="b5fb6-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="b5fb6-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="b5fb6-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b5fb6-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="b5fb6-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b5fb6-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)