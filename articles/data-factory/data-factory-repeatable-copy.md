---
title: copie aaaRepeatable dans Azure Data Factory | Documents Microsoft
description: "Découvrez comment tooavoid doublons même si un secteur qui copie des données est exécuté plusieurs fois."
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
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="5106e-103">Copie répétable dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5106e-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="5106e-104">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="5106e-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="5106e-105">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="5106e-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="5106e-106">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="5106e-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="5106e-107">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="5106e-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="5106e-108">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="5106e-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="5106e-109">Hello exemples suivants sont pour SQL Azure, mais banque de données applicable tooany qui prend en charge les jeux de données rectangulaire.</span><span class="sxs-lookup"><span data-stu-id="5106e-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="5106e-110">Vous avez peut-être tooadjust hello **type** de source et hello **requête** propriété (par exemple : requête au lieu de sqlReaderQuery) pour les données de salutation stocker.</span><span class="sxs-lookup"><span data-stu-id="5106e-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="5106e-111">En règle générale, lors de la lecture à partir de magasins relationnelles, vous souhaitez tooread uniquement les données de hello correspondant toothat tranche.</span><span class="sxs-lookup"><span data-stu-id="5106e-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="5106e-112">Un moyen toodo serait donc à l’aide de hello WindowStart et WindowEnd variables système disponibles dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5106e-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="5106e-113">En savoir plus sur les variables de hello et les fonctions dans Azure Data Factory ici Bonjour [Azure Data Factory - fonctions et Variables système](data-factory-functions-variables.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="5106e-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="5106e-114">Exemple :</span><span class="sxs-lookup"><span data-stu-id="5106e-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="5106e-115">Cette requête lit les données qui se situe à partir de la table de hello MyTable hello durée de la tranche (WindowStart -> WindowEnd).</span><span class="sxs-lookup"><span data-stu-id="5106e-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="5106e-116">Réexécutez de cette tranche s’assurent également que ce hello mêmes données sont en lecture.</span><span class="sxs-lookup"><span data-stu-id="5106e-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="5106e-117">Dans d’autres cas, vous souhaiterez peut-être tooread hello totalité de la table et pouvez définir hello sqlReaderQuery comme suit :</span><span class="sxs-lookup"><span data-stu-id="5106e-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="5106e-118">Écriture REPEATABLE tooSqlSink</span><span class="sxs-lookup"><span data-stu-id="5106e-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="5106e-119">Lors de la copie des données trop**Azure SQL/SQL Server** provenant d’autres banques de données, vous devez l’esprit tooavoid tookeep répétabilité des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="5106e-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="5106e-120">Lors de la copie des données tooAzure base de données SQL/SQL Server, l’activité de copie hello ajoute la table de données toohello récepteur par défaut.</span><span class="sxs-lookup"><span data-stu-id="5106e-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="5106e-121">Par exemple, vous copiez des données à partir d’un format CSV (valeurs séparées par des virgules) fichier contenant deux enregistrements toohello suivant de table dans une base de données Azure SQL/SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5106e-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="5106e-122">Lorsqu’une tranche s’exécute, hello deux enregistrements sont copiés toohello SQL table.</span><span class="sxs-lookup"><span data-stu-id="5106e-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="5106e-123">Supposons que vous a détecté des erreurs dans le fichier source et quantité hello du Tube vers le bas à partir de 2 too4 mise à jour.</span><span class="sxs-lookup"><span data-stu-id="5106e-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="5106e-124">Si vous réexécutez la tranche de données hello pour cette période manuellement, vous trouverez deux nouveaux enregistrements ajoutés tooAzure base de données SQL/SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5106e-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="5106e-125">Cet exemple suppose qu’aucune des colonnes hello dans la table de hello de contrainte de clé primaire hello.</span><span class="sxs-lookup"><span data-stu-id="5106e-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="5106e-126">tooavoid ce comportement, vous avez besoin d’une sémantique UPSERT toospecify en utilisant l’une des hello suivant deux mécanismes :</span><span class="sxs-lookup"><span data-stu-id="5106e-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="5106e-127">Mécanisme 1 : utilisation de la propriété sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="5106e-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="5106e-128">Vous pouvez utiliser hello **sqlWriterCleanupScript** tooclean de propriété des données à partir de la table de récepteur de hello avant l’insertion de données de hello lors de l’exécution d’une tranche.</span><span class="sxs-lookup"><span data-stu-id="5106e-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="5106e-129">Lorsqu’une tranche s’exécute, le script de nettoyage hello est exécuté premières données toodelete correspondant tranche toohello à partir de la table SQL de hello.</span><span class="sxs-lookup"><span data-stu-id="5106e-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="5106e-130">activité de copie Hello insère ensuite les données dans hello Table SQL.</span><span class="sxs-lookup"><span data-stu-id="5106e-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="5106e-131">En cas de réexécution de la tranche de hello, la quantité de hello est mise à jour comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="5106e-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="5106e-132">Supposons que hello enregistrement de laver plat est supprimé de volume partagé de cluster hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="5106e-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="5106e-133">Puis réexécuter la tranche de hello produirait hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="5106e-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="5106e-134">activité de copie Hello s’exécutaient hello nettoyage script toodelete hello données correspondantes pour ce secteur.</span><span class="sxs-lookup"><span data-stu-id="5106e-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="5106e-135">Puis il lire l’entrée de hello de csv hello (qui puis ne contenus qu’un seul enregistrement) et inséré dans la Table de hello.</span><span class="sxs-lookup"><span data-stu-id="5106e-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="5106e-136">Mécanisme 2 : utilisation du paramètre sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="5106e-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5106e-137">Pour le moment, le paramètre sliceIdentifierColumnName n’est pas pris en charge par Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5106e-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="5106e-138">répétabilité de tooachieve Hello deuxième mécanisme est en ayant une colonne dédiée (sliceIdentifierColumnName) dans la cible de hello Table.</span><span class="sxs-lookup"><span data-stu-id="5106e-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="5106e-139">Cette colonne peut être utilisée par Azure Data Factory tooensure hello source et destination reste synchronisé.</span><span class="sxs-lookup"><span data-stu-id="5106e-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="5106e-140">Cette approche fonctionne quand il existe une grande souplesse dans la modification ou la définition de schéma de Table SQL de destination hello.</span><span class="sxs-lookup"><span data-stu-id="5106e-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="5106e-141">Cette colonne est utilisée par la fabrique de données Azure à des fins de répétabilité et dans les processus hello Azure Data Factory ne fait pas de n’importe quel schéma change toohello Table.</span><span class="sxs-lookup"><span data-stu-id="5106e-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="5106e-142">Méthode toouse cette approche :</span><span class="sxs-lookup"><span data-stu-id="5106e-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="5106e-143">Définir une colonne de type **binary (32)** dans Table SQL de destination hello.</span><span class="sxs-lookup"><span data-stu-id="5106e-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="5106e-144">Aucune contrainte ne doit exister sur cette colonne.</span><span class="sxs-lookup"><span data-stu-id="5106e-144">There should be no constraints on this column.</span></span> <span data-ttu-id="5106e-145">Pour les besoins de cet exemple, nommons cette colonne « AdfSliceIdentifier ».</span><span class="sxs-lookup"><span data-stu-id="5106e-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="5106e-146">Table source :</span><span class="sxs-lookup"><span data-stu-id="5106e-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="5106e-147">Table de destination :</span><span class="sxs-lookup"><span data-stu-id="5106e-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="5106e-148">Utiliser dans l’activité de copie hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5106e-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="5106e-149">Azure Data Factory remplit cette colonne en fonction de son besoin tooensure hello source et destination restent synchronisés.</span><span class="sxs-lookup"><span data-stu-id="5106e-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="5106e-150">valeurs Hello cette colonne ne doivent pas être utilisées en dehors de ce contexte.</span><span class="sxs-lookup"><span data-stu-id="5106e-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="5106e-151">Toomechanism similaires 1, l’activité de copie nettoie automatiquement les données hello pour hello donné tranche à partir de destination hello Table SQL.</span><span class="sxs-lookup"><span data-stu-id="5106e-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="5106e-152">Il insère ensuite les données à partir de la source de table de destination toohello.</span><span class="sxs-lookup"><span data-stu-id="5106e-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5106e-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5106e-153">Next steps</span></span>
<span data-ttu-id="5106e-154">Passez en revue hello suivant connecteur articles pour exécuter les exemples JSON :</span><span class="sxs-lookup"><span data-stu-id="5106e-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="5106e-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="5106e-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="5106e-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5106e-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="5106e-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="5106e-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)