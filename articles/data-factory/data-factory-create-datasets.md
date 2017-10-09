---
title: "jeux de données aaaCreate dans Azure Data Factory | Documents Microsoft"
description: "Découvrez comment les jeux de données toocreate dans Azure Data Factory, avec des exemples qui utilisent des propriétés, telles que décalage et anchorDateTime."
keywords: "créer un jeu de données, exemple de jeu de données, exemple offset"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="03f8a-104">Jeux de données dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="03f8a-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="03f8a-105">Cet article décrit les jeux de données, comment ils sont définis au format JSON et comment ils sont utilisés dans les pipelines d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="03f8a-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="03f8a-106">Il fournit des détails sur chaque section (par exemple, structure, disponibilité et stratégie) dans la définition JSON de jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="03f8a-107">Hello article fournit également des exemples d’utilisation de hello **offset**, **anchorDateTime**, et **style** propriétés dans une définition de jeu de données JSON.</span><span class="sxs-lookup"><span data-stu-id="03f8a-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="03f8a-108">Si vous êtes tooData nouvelle fabrique, consultez [Introduction tooAzure Data Factory](data-factory-introduction.md) pour une vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="03f8a-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="03f8a-109">Si vous n’avez pas l’expérience pratique de création de fabriques de données, vous pouvez obtenir une meilleure compréhension par la lecture de hello [didacticiel de transformation de données](data-factory-build-your-first-pipeline.md) et hello [didacticiel sur le déplacement des données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="03f8a-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="03f8a-110">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="03f8a-110">Overview</span></span>
<span data-ttu-id="03f8a-111">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="03f8a-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="03f8a-112">Un **pipeline** constitue un regroupement logique d’**activités** qui exécutent ensemble une tâche.</span><span class="sxs-lookup"><span data-stu-id="03f8a-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="03f8a-113">activités Hello dans un pipeline de définissent les actions tooperform sur vos données.</span><span class="sxs-lookup"><span data-stu-id="03f8a-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="03f8a-114">Par exemple, vous pouvez utiliser un copie activité toocopy des données d’une tooAzure de SQL Server locale stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="03f8a-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="03f8a-115">Ensuite, vous pouvez utiliser une activité Hive qui exécute un script Hive sur des données de tooprocess cluster Azure HDInsight à partir des données de sortie de tooproduce de stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="03f8a-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="03f8a-116">Enfin, vous pouvez utiliser une deuxième copie activité toocopy hello sortie données tooAzure SQL Data Warehouse, par-dessus le décisionnel (BI) reporting les solutions sont créées.</span><span class="sxs-lookup"><span data-stu-id="03f8a-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="03f8a-117">Pour plus d’informations sur les pipelines et les activités, voir [Pipelines et activités dans Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="03f8a-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="03f8a-118">Une activité peut inclure zéro ou plusieurs **jeux de données** d’entrée et produire un ou plusieurs jeux de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="03f8a-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="03f8a-119">Un jeu de données d’entrée représente une entrée hello pour une activité dans le pipeline de hello et un jeu de données de sortie sortie hello pour l’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="03f8a-120">Les jeux de données identifient les données dans différents magasins de données, par exemple des tables, des fichiers, des dossiers et des documents.</span><span class="sxs-lookup"><span data-stu-id="03f8a-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="03f8a-121">Par exemple, un jeu de données d’objets Blob Azure Spécifie le conteneur d’objets blob hello et le dossier de stockage d’objets Blob à partir de quels hello pipeline doit lire les données de hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="03f8a-122">Avant de créer un jeu de données, créer un **service lié** toolink fabrique de données toohello du magasin de vos données.</span><span class="sxs-lookup"><span data-stu-id="03f8a-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="03f8a-123">Services liés ressemblent aux chaînes de connexion, qui définissent les informations de connexion hello requises pour les ressources de tooexternal tooconnect Data Factory.</span><span class="sxs-lookup"><span data-stu-id="03f8a-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="03f8a-124">Jeux de données identifient les données dans les magasins de données hello lié, tels que des tables SQL, des fichiers, des dossiers et des documents.</span><span class="sxs-lookup"><span data-stu-id="03f8a-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="03f8a-125">Par exemple, un stockage Azure lié à des liens de service une fabrique de données de stockage compte toohello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="03f8a-126">Un jeu de données d’objets Blob Azure représente le conteneur d’objets blob hello et dossier hello contenant toobe d’objets BLOB d’entrée hello traité.</span><span class="sxs-lookup"><span data-stu-id="03f8a-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="03f8a-127">Voici un exemple de scénario.</span><span class="sxs-lookup"><span data-stu-id="03f8a-127">Here is a sample scenario.</span></span> <span data-ttu-id="03f8a-128">toocopy des données à partir de la base de données Blob stockage tooa SQL, vous créez deux services liés : le stockage Azure et base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="03f8a-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="03f8a-129">Ensuite, créez deux jeux de données : dataset d’objets Blob Azure (c'est-à-dire toohello lié Azure Storage service) et le jeu de données de Table de SQL Azure (qui fait référence le service de base de données SQL Azure lié toohello).</span><span class="sxs-lookup"><span data-stu-id="03f8a-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="03f8a-130">Bonjour Azure Storage et la base de données SQL Azure Data Factory utilise respectivement au runtime tooconnect tooyour le stockage Azure et à la base de données SQL Azure, les chaînes de connexion contiennent des services liés.</span><span class="sxs-lookup"><span data-stu-id="03f8a-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="03f8a-131">dataset d’objets Blob Azure Hello Spécifie le conteneur d’objets blob hello et le dossier d’objets blob qui contient des objets BLOB d’entrée de hello dans votre stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="03f8a-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="03f8a-132">jeu de données de Table de SQL Azure Hello spécifie hello SQL table dans les données de salutation toowhich votre base de données SQL est toobe copié.</span><span class="sxs-lookup"><span data-stu-id="03f8a-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="03f8a-133">Hello diagramme suivant présente hello relations entre pipeline, activité, jeu de données et le service lié dans la fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="03f8a-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relation entre le pipeline, l’activité, le jeu de données et les services liés](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="03f8a-135">Jeu de données JSON</span><span class="sxs-lookup"><span data-stu-id="03f8a-135">Dataset JSON</span></span>
<span data-ttu-id="03f8a-136">Un jeu de données dans la fabrique de données est défini au format JSON comme suit :</span><span class="sxs-lookup"><span data-stu-id="03f8a-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="03f8a-137">Hello tableau suivant décrit les propriétés dans hello ci-dessus JSON :</span><span class="sxs-lookup"><span data-stu-id="03f8a-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="03f8a-138">Propriété</span><span class="sxs-lookup"><span data-stu-id="03f8a-138">Property</span></span> | <span data-ttu-id="03f8a-139">Description</span><span class="sxs-lookup"><span data-stu-id="03f8a-139">Description</span></span> | <span data-ttu-id="03f8a-140">Requis</span><span class="sxs-lookup"><span data-stu-id="03f8a-140">Required</span></span> | <span data-ttu-id="03f8a-141">Default</span><span class="sxs-lookup"><span data-stu-id="03f8a-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="03f8a-142">name</span><span class="sxs-lookup"><span data-stu-id="03f8a-142">name</span></span> |<span data-ttu-id="03f8a-143">Nom du jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-143">Name of hello dataset.</span></span> <span data-ttu-id="03f8a-144">Pour connaître les règles d’affectation des noms, voir [Azure Data Factory - Règles d’affectation des noms](data-factory-naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="03f8a-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="03f8a-145">Oui</span><span class="sxs-lookup"><span data-stu-id="03f8a-145">Yes</span></span> |<span data-ttu-id="03f8a-146">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-146">NA</span></span> |
| <span data-ttu-id="03f8a-147">type</span><span class="sxs-lookup"><span data-stu-id="03f8a-147">type</span></span> |<span data-ttu-id="03f8a-148">Type de jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-148">Type of hello dataset.</span></span> <span data-ttu-id="03f8a-149">Spécifiez un des types hello pris en charge par la fabrique de données (par exemple : AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="03f8a-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="03f8a-150">Pour plus d’informations, consultez [Type du jeu de données](#Type).</span><span class="sxs-lookup"><span data-stu-id="03f8a-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="03f8a-151">Oui</span><span class="sxs-lookup"><span data-stu-id="03f8a-151">Yes</span></span> |<span data-ttu-id="03f8a-152">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-152">NA</span></span> |
| <span data-ttu-id="03f8a-153">structure</span><span class="sxs-lookup"><span data-stu-id="03f8a-153">structure</span></span> |<span data-ttu-id="03f8a-154">Schéma du jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="03f8a-155">Pour plus d’informations, consultez [Structure d’un jeu de données](#Structure).</span><span class="sxs-lookup"><span data-stu-id="03f8a-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="03f8a-156">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-156">No</span></span> |<span data-ttu-id="03f8a-157">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-157">NA</span></span> |
| <span data-ttu-id="03f8a-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="03f8a-158">typeProperties</span></span> | <span data-ttu-id="03f8a-159">propriétés de type Hello sont différentes pour chaque type (par exemple : objet Blob Azure, table SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="03f8a-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="03f8a-160">Pour plus d’informations sur les types hello pris en charge et leurs propriétés, consultez [type Dataset](#Type).</span><span class="sxs-lookup"><span data-stu-id="03f8a-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="03f8a-161">Oui</span><span class="sxs-lookup"><span data-stu-id="03f8a-161">Yes</span></span> |<span data-ttu-id="03f8a-162">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-162">NA</span></span> |
| <span data-ttu-id="03f8a-163">external</span><span class="sxs-lookup"><span data-stu-id="03f8a-163">external</span></span> | <span data-ttu-id="03f8a-164">Indicateur booléen toospecify si un jeu de données est explicitement généré par un pipeline de fabrique de données ou non.</span><span class="sxs-lookup"><span data-stu-id="03f8a-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="03f8a-165">Si hello un jeu de données d’entrée pour une activité n’est pas produit par le pipeline actuel de hello, définissez cette tootrue indicateur.</span><span class="sxs-lookup"><span data-stu-id="03f8a-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="03f8a-166">Définissez cette tootrue indicateur pour hello un jeu de données d’entrée de la première activité hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="03f8a-167">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-167">No</span></span> |<span data-ttu-id="03f8a-168">false</span><span class="sxs-lookup"><span data-stu-id="03f8a-168">false</span></span> |
| <span data-ttu-id="03f8a-169">availability</span><span class="sxs-lookup"><span data-stu-id="03f8a-169">availability</span></span> | <span data-ttu-id="03f8a-170">Définit hello fenêtre de traitement (par exemple, toutes les heures ou tous les jours) ou hello le découpage du modèle pour la production de dataset hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="03f8a-171">Chaque unité de données consommée et produite pendant l’exécution d’une activité est appelée tranche de données.</span><span class="sxs-lookup"><span data-stu-id="03f8a-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="03f8a-172">Si la disponibilité de hello d’un dataset de sortie est toodaily de jeu (fréquence - Day, intervalle de-1), une tranche est produite quotidiennement.</span><span class="sxs-lookup"><span data-stu-id="03f8a-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="03f8a-173">Pour plus d’informations, consultez [Disponibilité du jeu de données](#Availability).</span><span class="sxs-lookup"><span data-stu-id="03f8a-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="03f8a-174">Pour plus d’informations sur le jeu de données hello le découpage du modèle, consultez hello [de planification et de l’exécution](data-factory-scheduling-and-execution.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="03f8a-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="03f8a-175">Oui</span><span class="sxs-lookup"><span data-stu-id="03f8a-175">Yes</span></span> |<span data-ttu-id="03f8a-176">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-176">NA</span></span> |
| <span data-ttu-id="03f8a-177">policy</span><span class="sxs-lookup"><span data-stu-id="03f8a-177">policy</span></span> |<span data-ttu-id="03f8a-178">Définit les critères de hello ou une condition hello tranches de dataset hello doivent répondre.</span><span class="sxs-lookup"><span data-stu-id="03f8a-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="03f8a-179">Pour plus d’informations, consultez hello [stratégie de groupe de données](#Policy) section.</span><span class="sxs-lookup"><span data-stu-id="03f8a-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="03f8a-180">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-180">No</span></span> |<span data-ttu-id="03f8a-181">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="03f8a-182">Exemple de jeu de données</span><span class="sxs-lookup"><span data-stu-id="03f8a-182">Dataset example</span></span>
<span data-ttu-id="03f8a-183">Dans l’exemple suivant de hello, hello dataset représente une table nommée **MyTable** dans une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="03f8a-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="03f8a-184">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="03f8a-184">Note hello following points:</span></span>

* <span data-ttu-id="03f8a-185">**type** a la valeur tooAzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="03f8a-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="03f8a-186">**tableName** la propriété de type (type tooAzureSqlTable spécifique) a la valeur tooMyTable.</span><span class="sxs-lookup"><span data-stu-id="03f8a-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="03f8a-187">**linkedServiceName** fait référence de service tooa lié de type AzureSqlDatabase, qui est définie dans l’extrait de code JSON suivant hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="03f8a-188">**fréquence de disponibilité** a la valeur tooDay, et **intervalle** a la valeur too1.</span><span class="sxs-lookup"><span data-stu-id="03f8a-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="03f8a-189">Cela signifie que cette tranche de dataset hello est produite quotidiennement.</span><span class="sxs-lookup"><span data-stu-id="03f8a-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="03f8a-190">**AzureSqlLinkedService** est défini comme suit :</span><span class="sxs-lookup"><span data-stu-id="03f8a-190">**AzureSqlLinkedService** is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="03f8a-191">Bonjour précédant l’extrait de code JSON :</span><span class="sxs-lookup"><span data-stu-id="03f8a-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="03f8a-192">**type** a la valeur tooAzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="03f8a-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="03f8a-193">**connectionString** propriété type spécifie des informations de base de données tooconnect tooa SQL.</span><span class="sxs-lookup"><span data-stu-id="03f8a-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="03f8a-194">Comme vous pouvez le voir, hello service lié définit comment tooconnect tooa base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="03f8a-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="03f8a-195">jeu de données Hello définit quelle table est utilisée comme entrée et de sortie pour l’activité hello dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="03f8a-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="03f8a-196">Sauf si un jeu de données n’est produit par le pipeline de hello, il doit être marqué comme étant **externe**.</span><span class="sxs-lookup"><span data-stu-id="03f8a-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="03f8a-197">Ce paramètre s’applique généralement à tooinputs de la première activité dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="03f8a-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="03f8a-198"><a name="Type"></a> Type du jeu de données</span><span class="sxs-lookup"><span data-stu-id="03f8a-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="03f8a-199">type Hello du jeu de données hello dépend du magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="03f8a-200">Consultez hello tableau pour obtenir la liste des magasins de données pris en charge par la fabrique de données suivant.</span><span class="sxs-lookup"><span data-stu-id="03f8a-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="03f8a-201">Cliquez sur un toolearn de magasin de données comment toocreate un service lié et un jeu de données pour que les données de stockage.</span><span class="sxs-lookup"><span data-stu-id="03f8a-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="03f8a-202">Les magasins de données avec * peuvent être locaux ou sur l’infrastructure Azure en tant que service (IaaS).</span><span class="sxs-lookup"><span data-stu-id="03f8a-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="03f8a-203">Ces magasins de données nécessitent tooinstall [passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="03f8a-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="03f8a-204">Dans l’exemple hello dans la section précédente de hello, type hello du jeu de données hello est défini trop**AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="03f8a-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="03f8a-205">De même, pour un jeu de données d’objets Blob Azure, hello type du jeu de données hello est défini trop**AzureBlob**, comme indiqué dans hello suivant JSON :</span><span class="sxs-lookup"><span data-stu-id="03f8a-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <span data-ttu-id="03f8a-206"><a name="Structure"></a>Structure d’un jeu de données</span><span class="sxs-lookup"><span data-stu-id="03f8a-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="03f8a-207">Hello **structure** section est facultative.</span><span class="sxs-lookup"><span data-stu-id="03f8a-207">hello **structure** section is optional.</span></span> <span data-ttu-id="03f8a-208">Il définit le schéma hello du jeu de données hello par contenant une collection de noms et types de données des colonnes.</span><span class="sxs-lookup"><span data-stu-id="03f8a-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="03f8a-209">Vous utilisez hello section tooprovide type information de structure qui est utilisé tooconvert types et mapper les colonnes de destination de toohello hello source.</span><span class="sxs-lookup"><span data-stu-id="03f8a-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="03f8a-210">Dans l’exemple suivant de hello, jeu de données hello possède trois colonnes : `slicetimestamp`, `projectname`, et `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="03f8a-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="03f8a-211">Elles sont respectivement de type String, String et Decimal.</span><span class="sxs-lookup"><span data-stu-id="03f8a-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="03f8a-212">Chaque colonne de structure de hello contient hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="03f8a-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="03f8a-213">Propriété</span><span class="sxs-lookup"><span data-stu-id="03f8a-213">Property</span></span> | <span data-ttu-id="03f8a-214">Description</span><span class="sxs-lookup"><span data-stu-id="03f8a-214">Description</span></span> | <span data-ttu-id="03f8a-215">Requis</span><span class="sxs-lookup"><span data-stu-id="03f8a-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="03f8a-216">name</span><span class="sxs-lookup"><span data-stu-id="03f8a-216">name</span></span> |<span data-ttu-id="03f8a-217">Nom de colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-217">Name of hello column.</span></span> |<span data-ttu-id="03f8a-218">Oui</span><span class="sxs-lookup"><span data-stu-id="03f8a-218">Yes</span></span> |
| <span data-ttu-id="03f8a-219">type</span><span class="sxs-lookup"><span data-stu-id="03f8a-219">type</span></span> |<span data-ttu-id="03f8a-220">Type de données de colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-220">Data type of hello column.</span></span>  |<span data-ttu-id="03f8a-221">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-221">No</span></span> |
| <span data-ttu-id="03f8a-222">culture</span><span class="sxs-lookup"><span data-stu-id="03f8a-222">culture</span></span> |<span data-ttu-id="03f8a-223">. Toobe culture basée sur le réseau utilisé lorsque le type de hello est un type .NET : `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="03f8a-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="03f8a-224">valeur par défaut Hello est `en-us`.</span><span class="sxs-lookup"><span data-stu-id="03f8a-224">hello default is `en-us`.</span></span> |<span data-ttu-id="03f8a-225">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-225">No</span></span> |
| <span data-ttu-id="03f8a-226">format</span><span class="sxs-lookup"><span data-stu-id="03f8a-226">format</span></span> |<span data-ttu-id="03f8a-227">Mettre en forme toobe de chaîne utilisé lorsque le type de hello est un type .NET : `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="03f8a-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="03f8a-228">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-228">No</span></span> |

<span data-ttu-id="03f8a-229">Hello indications suivantes vous aider à déterminer quand tooinclude structurer les informations et le tooinclude Bonjour **structure** section.</span><span class="sxs-lookup"><span data-stu-id="03f8a-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="03f8a-230">**Pour les sources de données structurées**, spécifiez la section de structure hello uniquement si vous souhaitez mapper les colonnes de toosink de colonnes sources et leurs noms ne sont pas hello identiques.</span><span class="sxs-lookup"><span data-stu-id="03f8a-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="03f8a-231">Ce type de source de données structurées stocke les informations de schéma et de type de données, ainsi que les données de salutation lui-même.</span><span class="sxs-lookup"><span data-stu-id="03f8a-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="03f8a-232">SQL Server, Oracle et la table Azure sont des exemples de sources de données structurées.</span><span class="sxs-lookup"><span data-stu-id="03f8a-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="03f8a-233">Comme les informations de type sont déjà disponibles pour les sources de données structurées, vous ne devez pas inclure les informations de type lorsque vous incluez la section de structure hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="03f8a-234">**Pour le schéma sur les sources de données de lecture (stockage d’objets Blob spécifiquement)**, vous pouvez choisir les données toostore sans stocker toutes les informations de type ou de schéma avec des données hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="03f8a-235">Pour ces types de sources de données, incluez structure lorsque vous souhaitez que les colonnes toosink colonnes toomap source.</span><span class="sxs-lookup"><span data-stu-id="03f8a-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="03f8a-236">Inclure également structure lorsque hello dataset est une entrée pour une activité de copie et de types de données de jeu de données source doivent être de types toonative converti pour le récepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="03f8a-237">Fabrique de données prend en charge hello valeurs pour fournir des informations de type de structure suivantes : **Int16, Int32, Int64, unique, Double, Decimal, Byte [], booléen, chaîne, Guid, Datetime, Datetimeoffset et Timespan**.</span><span class="sxs-lookup"><span data-stu-id="03f8a-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="03f8a-238">Ces valeurs sont des valeurs de type basées sur .NET compatibles avec la norme CLS (Common Language Specification).</span><span class="sxs-lookup"><span data-stu-id="03f8a-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="03f8a-239">Fabrique de données effectue automatiquement les conversions de type lors du déplacement du magasin de données récepteur tooa du magasin de données à partir des données sources.</span><span class="sxs-lookup"><span data-stu-id="03f8a-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="03f8a-240">Disponibilité du jeu de données</span><span class="sxs-lookup"><span data-stu-id="03f8a-240">Dataset availability</span></span>
<span data-ttu-id="03f8a-241">Hello **disponibilité** section dans un jeu de données définit la fenêtre de traitement hello (par exemple, toutes les heures, tous les jours, ou toutes les semaines) pour le jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="03f8a-242">Pour plus d’informations sur les fenêtres d’activité, voir [Planification et exécution](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="03f8a-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="03f8a-243">Hello suivant la section disponibilité Spécifie que hello dataset de sortie soit produit toutes les heures ou jeu de données d’entrée hello est disponible, toutes les heures :</span><span class="sxs-lookup"><span data-stu-id="03f8a-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="03f8a-244">Si le pipeline de hello a hello après les heures de début et de fin :</span><span class="sxs-lookup"><span data-stu-id="03f8a-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="03f8a-245">Hello dataset de sortie est généré dans le pipeline de hello Démarrer toutes les heures et d’heure de fin.</span><span class="sxs-lookup"><span data-stu-id="03f8a-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="03f8a-246">Par conséquent, cinq tranches de jeu de données sont générées par ce pipeline, une pour chaque fenêtre d’activité (0 h - 1 h, 1 h - 2 h, 2 h - 3 h, 3 h - 4 h, 4 h - 5 h).</span><span class="sxs-lookup"><span data-stu-id="03f8a-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="03f8a-247">Hello tableau suivant décrit les propriétés que vous pouvez utiliser la section disponibilité hello :</span><span class="sxs-lookup"><span data-stu-id="03f8a-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="03f8a-248">Propriété</span><span class="sxs-lookup"><span data-stu-id="03f8a-248">Property</span></span> | <span data-ttu-id="03f8a-249">Description</span><span class="sxs-lookup"><span data-stu-id="03f8a-249">Description</span></span> | <span data-ttu-id="03f8a-250">Requis</span><span class="sxs-lookup"><span data-stu-id="03f8a-250">Required</span></span> | <span data-ttu-id="03f8a-251">Default</span><span class="sxs-lookup"><span data-stu-id="03f8a-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="03f8a-252">frequency</span><span class="sxs-lookup"><span data-stu-id="03f8a-252">frequency</span></span> |<span data-ttu-id="03f8a-253">Spécifie l’unité de temps hello pour la production de tranche de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="03f8a-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="03f8a-254"><b>Fréquence prise en charge</b>: minute, heure, jour, semaine, mois</span><span class="sxs-lookup"><span data-stu-id="03f8a-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="03f8a-255">Oui</span><span class="sxs-lookup"><span data-stu-id="03f8a-255">Yes</span></span> |<span data-ttu-id="03f8a-256">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-256">NA</span></span> |
| <span data-ttu-id="03f8a-257">interval</span><span class="sxs-lookup"><span data-stu-id="03f8a-257">interval</span></span> |<span data-ttu-id="03f8a-258">Spécifie un multiplicateur de fréquence.</span><span class="sxs-lookup"><span data-stu-id="03f8a-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="03f8a-259">« Intervalle de fréquence x » détermine la fréquence à laquelle hello tranche est produite.</span><span class="sxs-lookup"><span data-stu-id="03f8a-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="03f8a-260">Par exemple, si vous avez besoin de hello toobe dataset découpée sur toutes les heures, vous définissez <b>fréquence</b> trop<b>heure</b>, et <b>intervalle</b> trop<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="03f8a-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="03f8a-261">Notez que si vous spécifiez **fréquence** en tant que **Minute**, vous devez définir hello intervalle toono inférieur à 15.</span><span class="sxs-lookup"><span data-stu-id="03f8a-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="03f8a-262">Oui</span><span class="sxs-lookup"><span data-stu-id="03f8a-262">Yes</span></span> |<span data-ttu-id="03f8a-263">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-263">NA</span></span> |
| <span data-ttu-id="03f8a-264">style</span><span class="sxs-lookup"><span data-stu-id="03f8a-264">style</span></span> |<span data-ttu-id="03f8a-265">Spécifie si la tranche de hello doit être produite au démarrage de hello ou à la fin de l’intervalle de salutation.</span><span class="sxs-lookup"><span data-stu-id="03f8a-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="03f8a-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="03f8a-266">StartOfInterval</span></span></li><li><span data-ttu-id="03f8a-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="03f8a-267">EndOfInterval</span></span></li></ul><span data-ttu-id="03f8a-268">Si **fréquence** est défini trop**mois**, et **style** est défini trop**EndOfInterval**, tranche de hello est produite sur hello dernier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="03f8a-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="03f8a-269">Si **style** est défini trop**StartOfInterval**, hello tranche est produite hello premier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="03f8a-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="03f8a-270">Si **fréquence** est défini trop**jour**, et **style** est défini trop**EndOfInterval**, tranche de hello est produite dans hello dernière heure du jour de hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="03f8a-271">Si **fréquence** est défini trop**heure**, et **style** est défini trop**EndOfInterval**, tranche de hello est produite à fin hello d’heure de hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="03f8a-272">Par exemple, pour une tranche de hello période de 13 h 00 - 14 h 00, la tranche de hello est produite à 14 heures.</span><span class="sxs-lookup"><span data-stu-id="03f8a-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="03f8a-273">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-273">No</span></span> |<span data-ttu-id="03f8a-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="03f8a-274">EndOfInterval</span></span> |
| <span data-ttu-id="03f8a-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="03f8a-275">anchorDateTime</span></span> |<span data-ttu-id="03f8a-276">Définit la position absolue de hello dans le temps utilisé par les limites de la section hello planificateur toocompute jeu de données.</span><span class="sxs-lookup"><span data-stu-id="03f8a-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="03f8a-277">Notez que si cette propoerty comporte les parties de date qui sont plus précis hello spécifié fréquence, hello plus granulaires parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="03f8a-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="03f8a-278">Par exemple, si hello **intervalle** est **toutes les heures** (fréquence : heure et intervalle : 1) et hello **anchorDateTime** contient **minutes et secondes**, puis hello minutes et secondes des parties de **anchorDateTime** sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="03f8a-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="03f8a-279">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-279">No</span></span> |<span data-ttu-id="03f8a-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="03f8a-280">01/01/0001</span></span> |
| <span data-ttu-id="03f8a-281">Offset</span><span class="sxs-lookup"><span data-stu-id="03f8a-281">offset</span></span> |<span data-ttu-id="03f8a-282">Intervalle de temps par le hello début et fin de toutes les tranches de jeu de données sont déplacées.</span><span class="sxs-lookup"><span data-stu-id="03f8a-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="03f8a-283">Notez que si les deux **anchorDateTime** et **offset** est spécifié, les résultats hello sont hello combinée MAJ.</span><span class="sxs-lookup"><span data-stu-id="03f8a-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="03f8a-284">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-284">No</span></span> |<span data-ttu-id="03f8a-285">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="03f8a-286">exemple offset</span><span class="sxs-lookup"><span data-stu-id="03f8a-286">offset example</span></span>
<span data-ttu-id="03f8a-287">Par défaut, les tranches quotidiennes (`"frequency": "Day", "interval": 1`) commencent à 12:00 (minuit), temps universel coordonné (UTC).</span><span class="sxs-lookup"><span data-stu-id="03f8a-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="03f8a-288">Si vous souhaitez hello début toobe 6 h 00 UTC heure au lieu de cela, définissez hello décalage comme indiqué dans hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="03f8a-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="03f8a-289">Exemple anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="03f8a-289">anchorDateTime example</span></span>
<span data-ttu-id="03f8a-290">Dans l’exemple suivant de hello, hello dataset se produit une fois toutes les 23 heures.</span><span class="sxs-lookup"><span data-stu-id="03f8a-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="03f8a-291">Hello première tranche commence à heure hello spécifiée par **anchorDateTime**, qui est défini trop`2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="03f8a-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="03f8a-292">Exemple de décalage/style</span><span class="sxs-lookup"><span data-stu-id="03f8a-292">offset/style example</span></span>
<span data-ttu-id="03f8a-293">Bonjour dataset suivant est tous les mois et est généré sur hello 3e de chaque mois à 8 h 00 (`3.08:00:00`) :</span><span class="sxs-lookup"><span data-stu-id="03f8a-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="03f8a-294"><a name="Policy"></a>Stratégie du jeu de données</span><span class="sxs-lookup"><span data-stu-id="03f8a-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="03f8a-295">Hello **stratégie** section dans la définition de dataset hello définit les critères de hello ou condition hello hello tranches de jeu de données doit répondre.</span><span class="sxs-lookup"><span data-stu-id="03f8a-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="03f8a-296">Stratégies de validation</span><span class="sxs-lookup"><span data-stu-id="03f8a-296">Validation policies</span></span>
| <span data-ttu-id="03f8a-297">Nom de la stratégie</span><span class="sxs-lookup"><span data-stu-id="03f8a-297">Policy name</span></span> | <span data-ttu-id="03f8a-298">Description</span><span class="sxs-lookup"><span data-stu-id="03f8a-298">Description</span></span> | <span data-ttu-id="03f8a-299">Appliqué trop</span><span class="sxs-lookup"><span data-stu-id="03f8a-299">Applied too</span></span>| <span data-ttu-id="03f8a-300">Requis</span><span class="sxs-lookup"><span data-stu-id="03f8a-300">Required</span></span> | <span data-ttu-id="03f8a-301">Default</span><span class="sxs-lookup"><span data-stu-id="03f8a-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="03f8a-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="03f8a-302">minimumSizeMB</span></span> |<span data-ttu-id="03f8a-303">Valide les données hello **le stockage Blob Azure** répond aux hello exigences de taille minimale (en mégaoctets).</span><span class="sxs-lookup"><span data-stu-id="03f8a-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="03f8a-304">Stockage d'objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="03f8a-304">Azure Blob storage</span></span> |<span data-ttu-id="03f8a-305">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-305">No</span></span> |<span data-ttu-id="03f8a-306">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-306">NA</span></span> |
| <span data-ttu-id="03f8a-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="03f8a-307">minimumRows</span></span> |<span data-ttu-id="03f8a-308">Valide les données hello dans un **base de données SQL Azure** ou un **table Azure** contient hello le nombre minimal de lignes.</span><span class="sxs-lookup"><span data-stu-id="03f8a-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="03f8a-309">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="03f8a-309">Azure SQL database</span></span></li><li><span data-ttu-id="03f8a-310">Table Azure</span><span class="sxs-lookup"><span data-stu-id="03f8a-310">Azure table</span></span></li></ul> |<span data-ttu-id="03f8a-311">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-311">No</span></span> |<span data-ttu-id="03f8a-312">N/D</span><span class="sxs-lookup"><span data-stu-id="03f8a-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="03f8a-313">Exemples</span><span class="sxs-lookup"><span data-stu-id="03f8a-313">Examples</span></span>
<span data-ttu-id="03f8a-314">**minimumSizeMB :**</span><span class="sxs-lookup"><span data-stu-id="03f8a-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="03f8a-315">**minimumRows :**</span><span class="sxs-lookup"><span data-stu-id="03f8a-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="03f8a-316">Jeux de données externes</span><span class="sxs-lookup"><span data-stu-id="03f8a-316">External datasets</span></span>
<span data-ttu-id="03f8a-317">Jeux de données externes est hello ceux qui ne sont pas produits par un pipeline en cours d’exécution dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="03f8a-318">Si hello le jeu de données est marquée comme **externe**, hello **ExternalData** stratégie peut être le comportement de hello tooinfluence défini de la disponibilité de coupe de dataset hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="03f8a-319">À moins qu’un jeu de données ne soit généré par la fabrique de données, il doit être marqué comme **external**(externe).</span><span class="sxs-lookup"><span data-stu-id="03f8a-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="03f8a-320">Ce paramètre s’applique généralement toohello les entrées de la première activité dans un pipeline, à moins que l’activité ou le chaînage des propriétés de pipeline sont utilisé.</span><span class="sxs-lookup"><span data-stu-id="03f8a-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="03f8a-321">Nom</span><span class="sxs-lookup"><span data-stu-id="03f8a-321">Name</span></span> | <span data-ttu-id="03f8a-322">Description</span><span class="sxs-lookup"><span data-stu-id="03f8a-322">Description</span></span> | <span data-ttu-id="03f8a-323">Requis</span><span class="sxs-lookup"><span data-stu-id="03f8a-323">Required</span></span> | <span data-ttu-id="03f8a-324">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="03f8a-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="03f8a-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="03f8a-325">dataDelay</span></span> |<span data-ttu-id="03f8a-326">temps de Hello toodelay hello Vérifier disponibilité hello de données externes de hello pour hello donné tranche.</span><span class="sxs-lookup"><span data-stu-id="03f8a-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="03f8a-327">Par exemple, vous pouvez retarder une vérification de toutes les heures à l’aide de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="03f8a-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="03f8a-328">Hello paramètre s’applique uniquement toohello moment présent.</span><span class="sxs-lookup"><span data-stu-id="03f8a-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="03f8a-329">Par exemple, si elle est de 1:00 PM maintenant et cette valeur est de 10 minutes, la validation hello démarre à 1 h 10.</span><span class="sxs-lookup"><span data-stu-id="03f8a-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="03f8a-330">Notez que ce paramètre n’affecte pas les tranches Bonjour passées.</span><span class="sxs-lookup"><span data-stu-id="03f8a-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="03f8a-331">Les tranches avec **Slice End Time** + **dataDelay** < **Now** sont traitées sans aucun délai.</span><span class="sxs-lookup"><span data-stu-id="03f8a-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="03f8a-332">Fois supérieure à 23:59 heures doivent être spécifiés à l’aide de hello `day.hours:minutes:seconds` format.</span><span class="sxs-lookup"><span data-stu-id="03f8a-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="03f8a-333">Par exemple, toospecify 24 heures, n’utilisez pas 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="03f8a-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="03f8a-334">Utilisez plutôt 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="03f8a-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="03f8a-335">Si vous utilisez 24:00:00, cette valeur est traitée comme 24 jours (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="03f8a-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="03f8a-336">Pour 1 jour et 4 heures, spécifiez 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="03f8a-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="03f8a-337">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-337">No</span></span> |<span data-ttu-id="03f8a-338">0</span><span class="sxs-lookup"><span data-stu-id="03f8a-338">0</span></span> |
| <span data-ttu-id="03f8a-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="03f8a-339">retryInterval</span></span> |<span data-ttu-id="03f8a-340">temps d’attente Hello entre un échec et hello prochaine tentative.</span><span class="sxs-lookup"><span data-stu-id="03f8a-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="03f8a-341">Ce paramètre s’applique toopresent heure.</span><span class="sxs-lookup"><span data-stu-id="03f8a-341">This setting applies toopresent time.</span></span> <span data-ttu-id="03f8a-342">Si vous essayez de hello précédente a échoué, la prochaine tentative de hello est après hello **retryInterval** période.</span><span class="sxs-lookup"><span data-stu-id="03f8a-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="03f8a-343">S’il s’agit de 1:00 PM dès maintenant, nous commençons hello première tentative.</span><span class="sxs-lookup"><span data-stu-id="03f8a-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="03f8a-344">Si hello durée toocomplete hello premier contrôle de validation est 1 minute et échoué de l’opération hello, nouvelle tentative suivante d’hello est à 1:00 + 1 min (durée) + 1 minute (intervalle avant nouvelle tentative) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="03f8a-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="03f8a-345">Aux tranches passées de hello, il n’existe aucun délai.</span><span class="sxs-lookup"><span data-stu-id="03f8a-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="03f8a-346">nouvelle tentative de Hello se produit immédiatement.</span><span class="sxs-lookup"><span data-stu-id="03f8a-346">hello retry happens immediately.</span></span> |<span data-ttu-id="03f8a-347">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-347">No</span></span> |<span data-ttu-id="03f8a-348">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="03f8a-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="03f8a-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="03f8a-349">retryTimeout</span></span> |<span data-ttu-id="03f8a-350">délai d’expiration de Hello pour chaque nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="03f8a-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="03f8a-351">Si cette propriété a la valeur too10 minutes, la validation hello doit être effectuée dans les 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="03f8a-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="03f8a-352">Si elle dure plus longtemps que la validation de 10 minutes tooperform hello, hello recommencez arrive à expiration.</span><span class="sxs-lookup"><span data-stu-id="03f8a-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="03f8a-353">Si toutes les tentatives pour hello validation expirent, hello tranche est marquée comme **TimedOut**.</span><span class="sxs-lookup"><span data-stu-id="03f8a-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="03f8a-354">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-354">No</span></span> |<span data-ttu-id="03f8a-355">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="03f8a-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="03f8a-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="03f8a-356">maximumRetry</span></span> |<span data-ttu-id="03f8a-357">Hello fréquence toocheck pour la disponibilité de données externes de hello hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="03f8a-358">Hello valeur maximale autorisée est de 10.</span><span class="sxs-lookup"><span data-stu-id="03f8a-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="03f8a-359">Non</span><span class="sxs-lookup"><span data-stu-id="03f8a-359">No</span></span> |<span data-ttu-id="03f8a-360">3</span><span class="sxs-lookup"><span data-stu-id="03f8a-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="03f8a-361">Créer des jeux de données</span><span class="sxs-lookup"><span data-stu-id="03f8a-361">Create datasets</span></span>
<span data-ttu-id="03f8a-362">Vous pouvez créer des jeux de données à l’aide de l’un de ces outils ou kits de développement logiciel (SDK) :</span><span class="sxs-lookup"><span data-stu-id="03f8a-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="03f8a-363">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="03f8a-363">Copy Wizard</span></span> 
- <span data-ttu-id="03f8a-364">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="03f8a-364">Azure portal</span></span>
- <span data-ttu-id="03f8a-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03f8a-365">Visual Studio</span></span>
- <span data-ttu-id="03f8a-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="03f8a-366">PowerShell</span></span>
- <span data-ttu-id="03f8a-367">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="03f8a-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="03f8a-368">API REST</span><span class="sxs-lookup"><span data-stu-id="03f8a-368">REST API</span></span>
- <span data-ttu-id="03f8a-369">API .NET</span><span class="sxs-lookup"><span data-stu-id="03f8a-369">.NET API</span></span>

<span data-ttu-id="03f8a-370">Consultez hello suivant des didacticiels pour obtenir des instructions pour la création de pipelines et les jeux de données en utilisant l’une de ces outils ou les kits de développement logiciel :</span><span class="sxs-lookup"><span data-stu-id="03f8a-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="03f8a-371">Créer un pipeline avec une activité de transformation des données</span><span class="sxs-lookup"><span data-stu-id="03f8a-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="03f8a-372">Créer un pipeline avec une activité de déplacement des données</span><span class="sxs-lookup"><span data-stu-id="03f8a-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="03f8a-373">Après un pipeline est créé et déployé, vous pouvez gérer et surveiller vos pipelines à l’aide de hello panneaux portail Azure ou une application de gestion et de surveillance hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="03f8a-374">Consultez hello rubriques pour obtenir des instructions pas à pas suivantes :</span><span class="sxs-lookup"><span data-stu-id="03f8a-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="03f8a-375">Surveiller et gérer les pipelines à l’aide des panneaux du portail Azure</span><span class="sxs-lookup"><span data-stu-id="03f8a-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="03f8a-376">Surveiller et gérer des pipelines à l’aide d’application de gestion et de surveillance hello</span><span class="sxs-lookup"><span data-stu-id="03f8a-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="03f8a-377">Étendue des jeux de données</span><span class="sxs-lookup"><span data-stu-id="03f8a-377">Scoped datasets</span></span>
<span data-ttu-id="03f8a-378">Vous pouvez créer des jeux de données qui est incluses dans l’étendue tooa pipeline à l’aide de hello **datasets** propriété.</span><span class="sxs-lookup"><span data-stu-id="03f8a-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="03f8a-379">Ces jeux de données peuvent uniquement être utilisés par les activités dans ce pipeline, et non pas par les activités d’autres pipelines.</span><span class="sxs-lookup"><span data-stu-id="03f8a-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="03f8a-380">Bonjour à l’exemple suivant définit un pipeline avec toobe (InputDataset-rdc et OutputDataset-rdc) deux jeux de données utilisé dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="03f8a-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="03f8a-381">Jeux de données incluses dans l’étendue est pris en charge uniquement avec des pipelines à usage unique (où **pipelineMode** est défini trop**OneTime**).</span><span class="sxs-lookup"><span data-stu-id="03f8a-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="03f8a-382">Pour plus d’informations, consultez [Pipeline onetime](data-factory-create-pipelines.md#onetime-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="03f8a-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="03f8a-383">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="03f8a-383">Next steps</span></span>
- <span data-ttu-id="03f8a-384">Pour plus d’informations sur les pipelines, voir [Créer des pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="03f8a-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="03f8a-385">Pour plus d’informations sur la façon dont les pipelines sont planifiés et exécutés, voir [Planification et exécution dans Azure Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="03f8a-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
