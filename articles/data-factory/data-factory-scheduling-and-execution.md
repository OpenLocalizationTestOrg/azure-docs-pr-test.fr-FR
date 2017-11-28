---
title: "aaaScheduling et l’exécution avec la fabrique de données | Documents Microsoft"
description: "Apprenez à connaître les aspects de planification et d’exécution du modèle d’application Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="13378-103">Planification et exécution avec Data Factory</span><span class="sxs-lookup"><span data-stu-id="13378-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="13378-104">Cet article explique les aspects de planification et l’exécution de hello du modèle d’application hello Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="13378-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="13378-105">Cet article suppose que vous avez des notions de base sur les concepts de modèle de données Data Factory, dont l’activité, les pipelines, les services connexes et les groupes de données.</span><span class="sxs-lookup"><span data-stu-id="13378-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="13378-106">Pour les concepts de base d’Azure Data Factory, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="13378-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="13378-107">Introduction tooData usine</span><span class="sxs-lookup"><span data-stu-id="13378-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="13378-108">Pipelines</span><span class="sxs-lookup"><span data-stu-id="13378-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="13378-109">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="13378-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="13378-110">Heures de début et de fin de pipeline</span><span class="sxs-lookup"><span data-stu-id="13378-110">Start and end times of pipeline</span></span>
<span data-ttu-id="13378-111">Un pipeline est actif uniquement entre son heure de **début** et son heure de **fin**.</span><span class="sxs-lookup"><span data-stu-id="13378-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="13378-112">Il n’est pas exécutée avant l’heure de début hello ou après l’heure de fin hello.</span><span class="sxs-lookup"><span data-stu-id="13378-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="13378-113">Si le pipeline de hello est suspendu, il n’est pas exécutée indépendamment de son heure de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="13378-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="13378-114">Pour un pipeline toorun, il ne doit pas être suspendu.</span><span class="sxs-lookup"><span data-stu-id="13378-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="13378-115">Vous recherchez ces paramètres (début, fin, en pause) dans la définition de pipeline hello :</span><span class="sxs-lookup"><span data-stu-id="13378-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="13378-116">Pour plus d’informations sur ces propriétés, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="13378-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="13378-117">Spécifier la planification d’une activité</span><span class="sxs-lookup"><span data-stu-id="13378-117">Specify schedule for an activity</span></span>
<span data-ttu-id="13378-118">Il n’est pas pipeline hello qui est exécutée.</span><span class="sxs-lookup"><span data-stu-id="13378-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="13378-119">Il s’agit des activités hello dans le pipeline de hello qui sont exécutées dans hello contexte général du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="13378-120">Vous pouvez spécifier une planification périodique pour une activité à l’aide de hello **planificateur** section de l’activité JSON.</span><span class="sxs-lookup"><span data-stu-id="13378-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="13378-121">Par exemple, vous pouvez planifier une activité toorun toutes les heures comme suit :</span><span class="sxs-lookup"><span data-stu-id="13378-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="13378-122">Comme indiqué dans hello suivant schéma, en spécifiant qu'une planification pour une activité crée une série de fenêtres bascules avec Bonjour pipeline début heures et de fin.</span><span class="sxs-lookup"><span data-stu-id="13378-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="13378-123">Les fenêtres récurrentes sont une série d’intervalles de temps fixes contigus, qui ne se chevauchent pas.</span><span class="sxs-lookup"><span data-stu-id="13378-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="13378-124">Ces fenêtres récurrentes logiques pour une activité sont appelées des **fenêtres d’activité**.</span><span class="sxs-lookup"><span data-stu-id="13378-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Exemple de planificateur d’activité](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="13378-126">Hello **planificateur** propriété pour une activité est facultative.</span><span class="sxs-lookup"><span data-stu-id="13378-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="13378-127">Si vous ne spécifiez pas cette propriété, il doit correspondre au rythme hello que vous spécifiez dans la définition de hello du dataset de sortie pour l’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="13378-128">Actuellement, le dataset de sortie est les lecteurs hello planification.</span><span class="sxs-lookup"><span data-stu-id="13378-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="13378-129">Par conséquent, vous devez créer un jeu de données de sortie même si l’activité hello ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="13378-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="13378-130">Spécifier la planification d’un jeu de données</span><span class="sxs-lookup"><span data-stu-id="13378-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="13378-131">Une activité dans un pipeline Data Factory peut inclure zéro ou plusieurs **jeux de données** d’entrée et produire un ou plusieurs jeux de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="13378-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="13378-132">Pour une activité, vous pouvez spécifier la cadence hello à quels hello les données d’entrée sont disponibles ou les données de sortie hello sont générées à l’aide de hello **disponibilité** section dans les définitions de jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="13378-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="13378-133">**Fréquence** Bonjour **disponibilité** section spécifie l’unité de temps hello.</span><span class="sxs-lookup"><span data-stu-id="13378-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="13378-134">Hello valeurs autorisées pour la fréquence sont : Minute, heure, jour, semaine et mois.</span><span class="sxs-lookup"><span data-stu-id="13378-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="13378-135">Hello **intervalle** propriété dans la section disponibilité hello spécifie un multiplicateur de fréquence.</span><span class="sxs-lookup"><span data-stu-id="13378-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="13378-136">Par exemple : si hello frequency tooDay et l’intervalle est défini too1 pour un dataset de sortie, les données de sortie hello produites quotidiennement.</span><span class="sxs-lookup"><span data-stu-id="13378-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="13378-137">Si vous spécifiez la fréquence de hello minute, nous vous recommandons de définir hello intervalle toono inférieur à 15.</span><span class="sxs-lookup"><span data-stu-id="13378-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="13378-138">Bonjour l’exemple suivant, les données d’entrée hello sont disponibles toutes les heures et les données de sortie hello sont produites toutes les heures (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="13378-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="13378-139">**Jeu de données d'entrée :**</span><span class="sxs-lookup"><span data-stu-id="13378-139">**Input dataset:**</span></span> 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


<span data-ttu-id="13378-140">**Jeu de données de sortie**</span><span class="sxs-lookup"><span data-stu-id="13378-140">**Output dataset**</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="13378-141">Actuellement, **sortie dataset lecteurs hello planification**.</span><span class="sxs-lookup"><span data-stu-id="13378-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="13378-142">En d’autres termes, planification hello spécifiée pour le jeu de données de sortie hello est toorun utilisé une activité lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="13378-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="13378-143">Par conséquent, vous devez créer un jeu de données de sortie même si l’activité hello ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="13378-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="13378-144">Si l’activité hello n’accepte aucune entrée, vous pouvez ignorer le jeu de données d’entrée création hello.</span><span class="sxs-lookup"><span data-stu-id="13378-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="13378-145">Suivant de hello pipeline définition, hello **planificateur** propriété est planification toospecify utilisé pour l’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="13378-146">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="13378-146">This property is optional.</span></span> <span data-ttu-id="13378-147">Actuellement, planification hello pour l’activité de hello doit correspondre au calendrier hello spécifié pour le jeu de données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="13378-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

<span data-ttu-id="13378-148">Dans cet exemple, hello activité exécute toutes les heures entre hello début et de fin des heures de pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="13378-149">les données de sortie Hello sont produites toutes les heures pour windows de trois heures (8 h 00 - 9 AM, 9 : 00 - 10 : 00 et 10 AM - 11 AM).</span><span class="sxs-lookup"><span data-stu-id="13378-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="13378-150">Chaque unité de données consommée ou produite pendant l’exécution d’une activité est appelée **tranche de données**.</span><span class="sxs-lookup"><span data-stu-id="13378-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="13378-151">Hello suivant schéma montre un exemple d’une activité avec un jeu de données d’entrée et un jeu de données de sortie :</span><span class="sxs-lookup"><span data-stu-id="13378-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Planificateur de disponibilité](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="13378-153">diagramme de Hello montre toutes les heures hello hello des tranches de données d’entrée et sortie de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="13378-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="13378-154">diagramme de Hello montre trois tranches d’entrée qui sont prêts pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="13378-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="13378-155">activité de 10 et 11 AM Hello est en cours, production de tranche de sortie de 10-11 AM hello.</span><span class="sxs-lookup"><span data-stu-id="13378-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="13378-156">Vous pouvez accéder à intervalle de temps hello associé tranche hello dans le dataset hello JSON à l’aide de variables : [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) et [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="13378-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="13378-157">De même, vous pouvez accéder à intervalle de temps hello associé à une fenêtre d’activité à l’aide de hello WindowStart et WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="13378-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="13378-158">planification Hello d’une activité doit correspondre au calendrier hello du dataset de sortie hello pour l’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="13378-159">Par conséquent, hello SliceStart et SliceEnd valeurs sont hello même en tant que valeurs WindowStart et WindowEnd respectivement.</span><span class="sxs-lookup"><span data-stu-id="13378-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="13378-160">Pour plus d’informations sur ces variables, consultez les articles [Variables système et fonctions Data Factory](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="13378-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="13378-161">Vous pouvez utiliser ces variables à différentes fins dans votre activité JSON.</span><span class="sxs-lookup"><span data-stu-id="13378-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="13378-162">Par exemple, vous pouvez utiliser les données tooselect de jeux de données d’entrée et de sortie qui représente les données de série chronologique (par exemple : 8 AM too9 AM).</span><span class="sxs-lookup"><span data-stu-id="13378-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="13378-163">Cet exemple utilise également **WindowStart** et **WindowEnd** tooselect les données pertinentes pour une activité exécuter et copiez-le blob tooa avec hello approprié **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="13378-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="13378-164">Hello **folderPath** est paramétrable toohave un dossier distinct pour chaque heure.</span><span class="sxs-lookup"><span data-stu-id="13378-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="13378-165">Bonjour précédent exemple, planification hello spécifiée pour les jeux de données d’entrée et de sortie est hello même (horaire).</span><span class="sxs-lookup"><span data-stu-id="13378-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="13378-166">Si hello un jeu de données d’entrée pour l’activité de hello est disponible à une fréquence différente, par exemple toutes les 15 minutes, activité hello qui génère ce jeu de données de sortie s’exécute toujours une fois par heure comme dataset de sortie hello est que les lecteurs hello planification d’activité.</span><span class="sxs-lookup"><span data-stu-id="13378-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="13378-167">Pour plus d’informations, consultez [Modélisation des jeux de données avec des fréquences différentes](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="13378-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="13378-168">Disponibilité et stratégies du jeu de données</span><span class="sxs-lookup"><span data-stu-id="13378-168">Dataset availability and policies</span></span>
<span data-ttu-id="13378-169">Vous avez vu l’utilisation de hello des propriétés de fréquence et l’intervalle dans la section disponibilité hello de définition de dataset.</span><span class="sxs-lookup"><span data-stu-id="13378-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="13378-170">Il existe quelques autres propriétés qui affectent la planification de hello et l’exécution d’une activité.</span><span class="sxs-lookup"><span data-stu-id="13378-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="13378-171">Disponibilité du jeu de données</span><span class="sxs-lookup"><span data-stu-id="13378-171">Dataset availability</span></span> 
<span data-ttu-id="13378-172">Hello tableau suivant décrit les propriétés que vous pouvez utiliser Bonjour **disponibilité** section :</span><span class="sxs-lookup"><span data-stu-id="13378-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="13378-173">Propriété</span><span class="sxs-lookup"><span data-stu-id="13378-173">Property</span></span> | <span data-ttu-id="13378-174">Description</span><span class="sxs-lookup"><span data-stu-id="13378-174">Description</span></span> | <span data-ttu-id="13378-175">Requis</span><span class="sxs-lookup"><span data-stu-id="13378-175">Required</span></span> | <span data-ttu-id="13378-176">Default</span><span class="sxs-lookup"><span data-stu-id="13378-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="13378-177">frequency</span><span class="sxs-lookup"><span data-stu-id="13378-177">frequency</span></span> |<span data-ttu-id="13378-178">Spécifie l’unité de temps hello pour la production de tranche de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="13378-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="13378-179"><b>Fréquence prise en charge</b>: minute, heure, jour, semaine, mois</span><span class="sxs-lookup"><span data-stu-id="13378-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="13378-180">Oui</span><span class="sxs-lookup"><span data-stu-id="13378-180">Yes</span></span> |<span data-ttu-id="13378-181">N/D</span><span class="sxs-lookup"><span data-stu-id="13378-181">NA</span></span> |
| <span data-ttu-id="13378-182">interval</span><span class="sxs-lookup"><span data-stu-id="13378-182">interval</span></span> |<span data-ttu-id="13378-183">Spécifie un multiplicateur de fréquence</span><span class="sxs-lookup"><span data-stu-id="13378-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="13378-184">« Intervalle de fréquence x » détermine la fréquence à laquelle hello tranche est produite.</span><span class="sxs-lookup"><span data-stu-id="13378-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="13378-185">Si vous avez besoin de hello toobe dataset découpée sur toutes les heures, vous définissez <b>fréquence</b> trop<b>heure</b>, et <b>intervalle</b> trop<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="13378-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="13378-186"><b>Remarque</b>: Si vous spécifiez la fréquence de minutes, nous vous recommandons de définir hello intervalle toono inférieur à 15</span><span class="sxs-lookup"><span data-stu-id="13378-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="13378-187">Oui</span><span class="sxs-lookup"><span data-stu-id="13378-187">Yes</span></span> |<span data-ttu-id="13378-188">N/D</span><span class="sxs-lookup"><span data-stu-id="13378-188">NA</span></span> |
| <span data-ttu-id="13378-189">style</span><span class="sxs-lookup"><span data-stu-id="13378-189">style</span></span> |<span data-ttu-id="13378-190">Spécifie si la tranche de hello doit être produite au hello début/fin d’intervalle de salutation.</span><span class="sxs-lookup"><span data-stu-id="13378-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="13378-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="13378-191">StartOfInterval</span></span></li><li><span data-ttu-id="13378-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="13378-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="13378-193">Si tooMonth est définie à la fréquence et le style a la valeur tooEndOfInterval, hello tranche est produite hello dernier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="13378-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="13378-194">Si le style de hello a la valeur tooStartOfInterval, hello tranche est produite hello premier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="13378-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="13378-195">Si tooDay est définie à la fréquence et le style a la valeur tooEndOfInterval, tranche de hello est produite dans hello dernière heure du jour de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="13378-196">Si tooHour est définie à la fréquence et le style a la valeur tooEndOfInterval, tranche de hello est produite à fin hello d’heure de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="13378-197">Par exemple, pour une tranche de période de 13 h 00 à 14 h 00, la tranche de hello est produite à 14 heures.</span><span class="sxs-lookup"><span data-stu-id="13378-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="13378-198">Non</span><span class="sxs-lookup"><span data-stu-id="13378-198">No</span></span> |<span data-ttu-id="13378-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="13378-199">EndOfInterval</span></span> |
| <span data-ttu-id="13378-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="13378-200">anchorDateTime</span></span> |<span data-ttu-id="13378-201">Définit la position absolue de hello dans le temps utilisé par les limites de la section Planificateur toocompute jeu de données.</span><span class="sxs-lookup"><span data-stu-id="13378-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="13378-202"><b>Remarque</b>: si hello AnchorDateTime comporte des parties de date qui sont plus précis que la fréquence de hello, hello plus granulaires parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="13378-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="13378-203">Par exemple, si hello <b>intervalle</b> est <b>toutes les heures</b> (fréquence : heure et intervalle : 1) et hello <b>AnchorDateTime</b> contient <b>minutes et secondes</b>, puis hello <b>minutes et secondes</b> parties Hello AnchorDateTime sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="13378-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="13378-204">Non</span><span class="sxs-lookup"><span data-stu-id="13378-204">No</span></span> |<span data-ttu-id="13378-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="13378-205">01/01/0001</span></span> |
| <span data-ttu-id="13378-206">Offset</span><span class="sxs-lookup"><span data-stu-id="13378-206">offset</span></span> |<span data-ttu-id="13378-207">Intervalle de temps par le hello début et fin de toutes les tranches de jeu de données sont déplacées.</span><span class="sxs-lookup"><span data-stu-id="13378-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="13378-208"><b>Remarque</b>: si anchorDateTime et offset sont spécifiés, hello résulte hello combinée MAJ.</span><span class="sxs-lookup"><span data-stu-id="13378-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="13378-209">Non</span><span class="sxs-lookup"><span data-stu-id="13378-209">No</span></span> |<span data-ttu-id="13378-210">N/D</span><span class="sxs-lookup"><span data-stu-id="13378-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="13378-211">exemple offset</span><span class="sxs-lookup"><span data-stu-id="13378-211">offset example</span></span>
<span data-ttu-id="13378-212">Par défaut, les tranches quotidiennes (`"frequency": "Day", "interval": 1`) commencent à 0 h UTC (minuit).</span><span class="sxs-lookup"><span data-stu-id="13378-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="13378-213">Si vous souhaitez hello début toobe 6 h 00 UTC heure au lieu de cela, définissez hello décalage comme indiqué dans hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="13378-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="13378-214">Exemple anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="13378-214">anchorDateTime example</span></span>
<span data-ttu-id="13378-215">Dans l’exemple suivant de hello, hello dataset se produit une fois toutes les 23 heures.</span><span class="sxs-lookup"><span data-stu-id="13378-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="13378-216">Hello première tranche commence à heure hello spécifié par anchorDateTime hello, qui est défini trop`2017-04-19T08:00:00` (heure UTC).</span><span class="sxs-lookup"><span data-stu-id="13378-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="13378-217">Exemple de décalage/style</span><span class="sxs-lookup"><span data-stu-id="13378-217">offset/style Example</span></span>
<span data-ttu-id="13378-218">Hello dataset suivant est un jeu de données mensuel et 3e de chaque mois à 8 h 00 est produite (`3.08:00:00`) :</span><span class="sxs-lookup"><span data-stu-id="13378-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="13378-219">Stratégie du jeu de données</span><span class="sxs-lookup"><span data-stu-id="13378-219">Dataset policy</span></span>
<span data-ttu-id="13378-220">Un jeu de données peut avoir une stratégie de validation définie qui spécifie comment les données de salutation générées par l’exécution d’une tranche peuvent être validées avant qu’il soit prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="13378-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="13378-221">Dans ce cas, une fois la tranche de hello a terminé l’exécution, état de la tranche hello sortie est modifié trop**attente** avec un sous-état de **Validation**.</span><span class="sxs-lookup"><span data-stu-id="13378-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="13378-222">Une fois validées, les tranches hello hello tranche devient trop**prêt**.</span><span class="sxs-lookup"><span data-stu-id="13378-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="13378-223">Si une tranche de données a été générée mais n’a pas réussi la validation de hello, les séries de l’activité pour tranches en aval qui dépendent de cette tranche ne sont pas traités.</span><span class="sxs-lookup"><span data-stu-id="13378-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="13378-224">[Surveiller et gérer des pipelines](data-factory-monitor-manage-pipelines.md) couvre hello différents États de tranche de données dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="13378-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="13378-225">Hello **stratégie** section dans la définition de dataset définit des critères de hello ou condition hello hello tranches de jeu de données doit répondre.</span><span class="sxs-lookup"><span data-stu-id="13378-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="13378-226">Hello tableau suivant décrit les propriétés que vous pouvez utiliser Bonjour **stratégie** section :</span><span class="sxs-lookup"><span data-stu-id="13378-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="13378-227">Nom de la stratégie</span><span class="sxs-lookup"><span data-stu-id="13378-227">Policy Name</span></span> | <span data-ttu-id="13378-228">Description</span><span class="sxs-lookup"><span data-stu-id="13378-228">Description</span></span> | <span data-ttu-id="13378-229">Appliqué trop</span><span class="sxs-lookup"><span data-stu-id="13378-229">Applied too</span></span>| <span data-ttu-id="13378-230">Requis</span><span class="sxs-lookup"><span data-stu-id="13378-230">Required</span></span> | <span data-ttu-id="13378-231">Default</span><span class="sxs-lookup"><span data-stu-id="13378-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="13378-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="13378-232">minimumSizeMB</span></span> | <span data-ttu-id="13378-233">Valide les données hello dans un **objets blob Azure** répond aux hello exigences de taille minimale (en mégaoctets).</span><span class="sxs-lookup"><span data-stu-id="13378-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="13378-234">Objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="13378-234">Azure Blob</span></span> |<span data-ttu-id="13378-235">Non</span><span class="sxs-lookup"><span data-stu-id="13378-235">No</span></span> |<span data-ttu-id="13378-236">N/D</span><span class="sxs-lookup"><span data-stu-id="13378-236">NA</span></span> |
| <span data-ttu-id="13378-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="13378-237">minimumRows</span></span> | <span data-ttu-id="13378-238">Valide les données hello dans un **base de données SQL Azure** ou un **table Azure** contient hello le nombre minimal de lignes.</span><span class="sxs-lookup"><span data-stu-id="13378-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="13378-239">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="13378-239">Azure SQL Database</span></span></li><li><span data-ttu-id="13378-240">table Azure</span><span class="sxs-lookup"><span data-stu-id="13378-240">Azure Table</span></span></li></ul> |<span data-ttu-id="13378-241">Non</span><span class="sxs-lookup"><span data-stu-id="13378-241">No</span></span> |<span data-ttu-id="13378-242">N/D</span><span class="sxs-lookup"><span data-stu-id="13378-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="13378-243">Exemples</span><span class="sxs-lookup"><span data-stu-id="13378-243">Examples</span></span>
<span data-ttu-id="13378-244">**minimumSizeMB :**</span><span class="sxs-lookup"><span data-stu-id="13378-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="13378-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="13378-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="13378-246">Pour plus d’informations sur ces propriétés et exemples, consultez l’article [Créer des jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="13378-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="13378-247">Stratégies d’activité</span><span class="sxs-lookup"><span data-stu-id="13378-247">Activity policies</span></span>
<span data-ttu-id="13378-248">Stratégies affectent le comportement d’exécution hello d’une activité, en particulier lors du traitement de hello une tranche de table.</span><span class="sxs-lookup"><span data-stu-id="13378-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="13378-249">Hello tableau suivant fournit des détails de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="13378-250">Propriété</span><span class="sxs-lookup"><span data-stu-id="13378-250">Property</span></span> | <span data-ttu-id="13378-251">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="13378-251">Permitted values</span></span> | <span data-ttu-id="13378-252">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="13378-252">Default Value</span></span> | <span data-ttu-id="13378-253">Description</span><span class="sxs-lookup"><span data-stu-id="13378-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="13378-254">accès concurrentiel</span><span class="sxs-lookup"><span data-stu-id="13378-254">concurrency</span></span> |<span data-ttu-id="13378-255">Entier </span><span class="sxs-lookup"><span data-stu-id="13378-255">Integer</span></span> <br/><br/><span data-ttu-id="13378-256">Valeur max : 10</span><span class="sxs-lookup"><span data-stu-id="13378-256">Max value: 10</span></span> |<span data-ttu-id="13378-257">1</span><span class="sxs-lookup"><span data-stu-id="13378-257">1</span></span> |<span data-ttu-id="13378-258">Nombre d’exécutions simultanées de l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="13378-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="13378-259">Il détermine le nombre de hello d’exécutions d’activité parallèles qui peuvent se produire sur différentes tranches.</span><span class="sxs-lookup"><span data-stu-id="13378-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="13378-260">Par exemple, si une activité doit toogo via un grand ensemble de données disponibles, une plus grande valeur d’accès concurrentiel accélère le traitement des données hello.</span><span class="sxs-lookup"><span data-stu-id="13378-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="13378-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="13378-261">executionPriorityOrder</span></span> |<span data-ttu-id="13378-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="13378-262">NewestFirst</span></span><br/><br/><span data-ttu-id="13378-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="13378-263">OldestFirst</span></span> |<span data-ttu-id="13378-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="13378-264">OldestFirst</span></span> |<span data-ttu-id="13378-265">Détermine hello classement de tranches de données qui sont en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="13378-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="13378-266">Par exemple, si vous avez 2 segments (l’un se produisant à 16 heures et l’autre à 17 heures) et que les deux sont en attente d’exécution.</span><span class="sxs-lookup"><span data-stu-id="13378-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="13378-267">Si vous définissez hello executionPriorityOrder toobe NewestFirst, tranche hello à 17 h 00 est traitée en premier.</span><span class="sxs-lookup"><span data-stu-id="13378-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="13378-268">Même si vous définissez executionPriorityORder de hello toobe OldestFIrst, tranche hello à 16 h 00 est traité.</span><span class="sxs-lookup"><span data-stu-id="13378-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="13378-269">retry</span><span class="sxs-lookup"><span data-stu-id="13378-269">retry</span></span> |<span data-ttu-id="13378-270">Entier </span><span class="sxs-lookup"><span data-stu-id="13378-270">Integer</span></span><br/><br/><span data-ttu-id="13378-271">La valeur max peut être 10</span><span class="sxs-lookup"><span data-stu-id="13378-271">Max value can be 10</span></span> |<span data-ttu-id="13378-272">0</span><span class="sxs-lookup"><span data-stu-id="13378-272">0</span></span> |<span data-ttu-id="13378-273">Nombre de tentatives avant le traitement des données de la tranche de hello hello est marqué comme défectueux.</span><span class="sxs-lookup"><span data-stu-id="13378-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="13378-274">Exécution de l’activité pour une tranche de données est retentée des toohello spécifié nombre de tentatives.</span><span class="sxs-lookup"><span data-stu-id="13378-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="13378-275">nouvelle tentative de Hello est faite dès que possible après l’échec de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="13378-276">timeout</span><span class="sxs-lookup"><span data-stu-id="13378-276">timeout</span></span> |<span data-ttu-id="13378-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="13378-277">TimeSpan</span></span> |<span data-ttu-id="13378-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="13378-278">00:00:00</span></span> |<span data-ttu-id="13378-279">Délai d’expiration pour l’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-279">Timeout for hello activity.</span></span> <span data-ttu-id="13378-280">Exemple : 00:10:00 (implique un délai d’expiration de 10 minutes)</span><span class="sxs-lookup"><span data-stu-id="13378-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="13378-281">Si une valeur n’est pas spécifiée ou est égal à 0, hello est infini.</span><span class="sxs-lookup"><span data-stu-id="13378-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="13378-282">Si le temps de traitement de données hello sur une tranche dépasse la valeur de délai d’attente de hello, elle est annulée et le traitement de hello tooretry tente de système de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="13378-283">nombre de Hello de nouvelles tentatives dépend de la propriété de nouvelle tentative hello.</span><span class="sxs-lookup"><span data-stu-id="13378-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="13378-284">En cas de délai d’attente, état de hello a la valeur tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="13378-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="13378-285">delay</span><span class="sxs-lookup"><span data-stu-id="13378-285">delay</span></span> |<span data-ttu-id="13378-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="13378-286">TimeSpan</span></span> |<span data-ttu-id="13378-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="13378-287">00:00:00</span></span> |<span data-ttu-id="13378-288">Spécifier le délai de hello avant le traitement des données de hello tranche commence.</span><span class="sxs-lookup"><span data-stu-id="13378-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="13378-289">exécution de Hello d’activité pour une tranche de données est démarrée une fois hello délai passé hello attendu des temps d’exécution.</span><span class="sxs-lookup"><span data-stu-id="13378-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="13378-290">Exemple : 00:10:00 (implique un délai de 10 minutes)</span><span class="sxs-lookup"><span data-stu-id="13378-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="13378-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="13378-291">longRetry</span></span> |<span data-ttu-id="13378-292">Entier </span><span class="sxs-lookup"><span data-stu-id="13378-292">Integer</span></span><br/><br/><span data-ttu-id="13378-293">Valeur max : 10</span><span class="sxs-lookup"><span data-stu-id="13378-293">Max value: 10</span></span> |<span data-ttu-id="13378-294">1</span><span class="sxs-lookup"><span data-stu-id="13378-294">1</span></span> |<span data-ttu-id="13378-295">nombre de Hello de long tentatives avant l’échec de l’exécution de la tranche hello.</span><span class="sxs-lookup"><span data-stu-id="13378-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="13378-296">Les tentatives longRetry sont espacées par longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="13378-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="13378-297">Par conséquent, si vous devez toospecify une heure entre chaque tentative, utilisez longRetry.</span><span class="sxs-lookup"><span data-stu-id="13378-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="13378-298">Si les valeurs Retry et longRetry sont spécifiées, chaque tentative longRetry inclut de nouvelles tentatives et le nombre maximal de hello de tentatives est de nouvelle tentative * longRetry.</span><span class="sxs-lookup"><span data-stu-id="13378-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="13378-299">Par exemple, si nous avons hello suivant les paramètres de stratégie d’activité hello :</span><span class="sxs-lookup"><span data-stu-id="13378-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="13378-300">Retry : 3</span><span class="sxs-lookup"><span data-stu-id="13378-300">Retry: 3</span></span><br/><span data-ttu-id="13378-301">longRetry : 2</span><span class="sxs-lookup"><span data-stu-id="13378-301">longRetry: 2</span></span><br/><span data-ttu-id="13378-302">longRetryInterval : 01:00:00</span><span class="sxs-lookup"><span data-stu-id="13378-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="13378-303">Supposons qu’une seule tranche tooexecute (l’état est en attente) et de l’exécution de l’activité hello échoue à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="13378-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="13378-304">Au départ, il y aurait 3 tentatives consécutives d'exécution.</span><span class="sxs-lookup"><span data-stu-id="13378-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="13378-305">Après chaque tentative, état hello de la tranche est Retry.</span><span class="sxs-lookup"><span data-stu-id="13378-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="13378-306">Une fois les 3 premiers tentatives sur, état hello de la tranche est LongRetry.</span><span class="sxs-lookup"><span data-stu-id="13378-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="13378-307">Après une heure (c’est-à-dire la valeur de longRetryInterval), il y aurait un autre ensemble de 3 tentatives consécutives d’exécution.</span><span class="sxs-lookup"><span data-stu-id="13378-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="13378-308">Après cela, état de la tranche hello est Failed et aucune nouvelle tentative n’a lieu.</span><span class="sxs-lookup"><span data-stu-id="13378-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="13378-309">Par conséquent, 6 tentatives ont été exécutées.</span><span class="sxs-lookup"><span data-stu-id="13378-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="13378-310">Si toute exécution réussit, état de la tranche hello est prêt et aucune nouvelle tentative n’est tentées.</span><span class="sxs-lookup"><span data-stu-id="13378-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="13378-311">longRetry peut être utilisé dans les situations où les données dépendantes arrivent à des moments non déterministe ou hello environnement global est instable sous laquelle le traitement de données se produit.</span><span class="sxs-lookup"><span data-stu-id="13378-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="13378-312">Dans ce cas, effectuant une après l’autre les nouvelles tentatives ne permettra pas de, et cela après un intervalle de résultats en temps Bonjour souhaitée de sortie.</span><span class="sxs-lookup"><span data-stu-id="13378-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="13378-313">Mise en garde : ne définissez pas de valeurs élevées pour longRetry ou longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="13378-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="13378-314">En règle générale, des valeurs plus élevées impliquent d’autres problèmes systémiques.</span><span class="sxs-lookup"><span data-stu-id="13378-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="13378-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="13378-315">longRetryInterval</span></span> |<span data-ttu-id="13378-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="13378-316">TimeSpan</span></span> |<span data-ttu-id="13378-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="13378-317">00:00:00</span></span> |<span data-ttu-id="13378-318">délai de Hello entre les nouvelles tentatives longues</span><span class="sxs-lookup"><span data-stu-id="13378-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="13378-319">Pour plus d’informations, consultez l’article [Pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="13378-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="13378-320">Traitement en parallèle des tranches de données</span><span class="sxs-lookup"><span data-stu-id="13378-320">Parallel processing of data slices</span></span>
<span data-ttu-id="13378-321">Vous pouvez définir la date de début hello pour le pipeline de hello Bonjour passées.</span><span class="sxs-lookup"><span data-stu-id="13378-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="13378-322">Lorsque vous procédez ainsi, Data Factory calcule (remplissages arrière) toutes les tranches de données Bonjour passées et commence à les traiter automatiquement.</span><span class="sxs-lookup"><span data-stu-id="13378-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="13378-323">Par exemple : Si vous créez un pipeline avec la date de début 2017-04-01 et hello date actuelle est 2017-04-10.</span><span class="sxs-lookup"><span data-stu-id="13378-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="13378-324">Si la sortie cadence hello Hello dataset est tous les jours, puis démarre le Data Factory traitement toutes les tranches hello 2017-04-01 too2017-04-09 immédiatement, car la date de début hello est Bonjour passées.</span><span class="sxs-lookup"><span data-stu-id="13378-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="13378-325">tranche Hello depuis 2017-04-10 n'est pas encore traité, car la valeur hello de propriété de style dans la section disponibilité hello est EndOfInterval par défaut.</span><span class="sxs-lookup"><span data-stu-id="13378-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="13378-326">Hello plus ancienne tranche est traitée tout d’abord comme valeur par défaut hello executionPriorityOrder vaut OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="13378-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="13378-327">Pour obtenir une description de la propriété de style hello, consultez [dataset disponibilité](#dataset-availability) section.</span><span class="sxs-lookup"><span data-stu-id="13378-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="13378-328">Pour obtenir une description de la section d’executionPriorityOrder hello, consultez hello [stratégies d’activité](#activity-policies) section.</span><span class="sxs-lookup"><span data-stu-id="13378-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="13378-329">Vous pouvez configurer toobe de tranches renvoyées les données traitée en parallèle en définissant un hello **concurrency** propriété Bonjour **stratégie** section de l’activité hello JSON.</span><span class="sxs-lookup"><span data-stu-id="13378-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="13378-330">Cette propriété détermine le nombre de hello d’exécutions d’activité parallèles qui peuvent se produire sur différentes tranches.</span><span class="sxs-lookup"><span data-stu-id="13378-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="13378-331">valeur par défaut de Hello pour la propriété d’accès concurrentiel hello est 1.</span><span class="sxs-lookup"><span data-stu-id="13378-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="13378-332">Une tranche est donc traitée à la fois par défaut.</span><span class="sxs-lookup"><span data-stu-id="13378-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="13378-333">valeur maximale de Hello est 10.</span><span class="sxs-lookup"><span data-stu-id="13378-333">hello maximum value is 10.</span></span> <span data-ttu-id="13378-334">Lorsqu’un pipeline doit toogo via un grand ensemble de données disponibles, une valeur concurrency plus importante accélère le traitement des données hello.</span><span class="sxs-lookup"><span data-stu-id="13378-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="13378-335">Réexécuter une tranche de données ayant échoué</span><span class="sxs-lookup"><span data-stu-id="13378-335">Rerun a failed data slice</span></span>
<span data-ttu-id="13378-336">Lorsqu’une erreur se produit lors du traitement d’une tranche de données, vous pouvez trouver des Échec du traitement hello d’une tranche à l’aide de panneaux de portail Azure et un moniteur et gérer une application.</span><span class="sxs-lookup"><span data-stu-id="13378-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="13378-337">Pour plus d’informations, consultez [Surveillance et gestion des pipelines à l’aide des panneaux du portail Azure](data-factory-monitor-manage-pipelines.md) ou de [l’application Surveillance et gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="13378-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="13378-338">Envisagez de hello exemple qui illustre les deux activités suivant.</span><span class="sxs-lookup"><span data-stu-id="13378-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="13378-339">Activity1 et Activity2.</span><span class="sxs-lookup"><span data-stu-id="13378-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="13378-340">Activity1 consomme une tranche de Dataset1 et produit une tranche de Dataset2, qui est utilisée en tant qu’entrée par Activity2 tooproduce une tranche de hello finale du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="13378-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![Tranche de données ayant échoué](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="13378-342">Hello diagramme montre que, hors trois tranches récentes, il a été un secteur 9 et 10 AM échec production hello pour Dataset2.</span><span class="sxs-lookup"><span data-stu-id="13378-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="13378-343">Fabrique de données suit automatiquement dépendance pour le jeu de données hello temps série.</span><span class="sxs-lookup"><span data-stu-id="13378-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="13378-344">Par conséquent, il ne démarre pas activité hello exécutée de la tranche en aval de hello 9 et 10 du matin.</span><span class="sxs-lookup"><span data-stu-id="13378-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="13378-345">Outils de surveillance et de gestion de fabrique de données permettent de toodrill dans les journaux de diagnostic hello pour hello tranche ayant échoué tooeasily rechercher hello cause d’origine pour le problème de hello et corrigez-le.</span><span class="sxs-lookup"><span data-stu-id="13378-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="13378-346">Après avoir résolu le problème de hello, vous pouvez facilement démarrer tranche de tooproduce hello Échec d’exécution de l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="13378-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="13378-347">Pour plus d’informations sur la façon de toorerun et comprendre les transitions d’état pour les tranches de données, consultez [analyse et la gestion des pipelines à l’aide de panneaux de portail Azure](data-factory-monitor-manage-pipelines.md) ou [analyse et gestion de l’application](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="13378-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="13378-348">Une fois que vous exécutez à nouveau hello 9 et 10 AM découper pour **Dataset2**, Data Factory démarre hello s’exécuter pour la tranche dépendant de hello 9 et 10 du matin sur hello de jeu de données final.</span><span class="sxs-lookup"><span data-stu-id="13378-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![Réexécuter une tranche de données ayant échoué](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="13378-350">Plusieurs activités à l’intérieur d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="13378-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="13378-351">Un pipeline peut toutefois contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="13378-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="13378-352">Si vous avez plusieurs activités dans un pipeline et sortie hello d’une activité n’est pas une entrée d’une autre activité, les activités hello peuvent s’exécuter en parallèle si de tranches de données d’entrée pour les activités de hello sont prêtes.</span><span class="sxs-lookup"><span data-stu-id="13378-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="13378-353">Vous pouvez chaîner les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="13378-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="13378-354">activités de Hello peuvent être Bonjour même pipeline ou dans différents pipelines.</span><span class="sxs-lookup"><span data-stu-id="13378-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="13378-355">la deuxième activité Hello s’exécute uniquement lorsque hello tout d’abord un terminé avec succès.</span><span class="sxs-lookup"><span data-stu-id="13378-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="13378-356">Par exemple, considérez hello suivant les cas où un pipeline a deux activités :</span><span class="sxs-lookup"><span data-stu-id="13378-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="13378-357">L’activité A1 nécessitant le jeu de données d’entrée externe D1 et qui produit le jeu de données de sortie D2.</span><span class="sxs-lookup"><span data-stu-id="13378-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="13378-358">L’activité A2 nécessitant le jeu de données d’entrée D2 et qui produit le jeu de données de sortie D3.</span><span class="sxs-lookup"><span data-stu-id="13378-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="13378-359">Dans ce scénario, les activités A1 et A2 sont Bonjour même pipeline.</span><span class="sxs-lookup"><span data-stu-id="13378-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="13378-360">activité Hello qu'a1 s’exécute lorsque les données externes hello sont disponibles et la fréquence de disponibilité hello planifiée est atteinte.</span><span class="sxs-lookup"><span data-stu-id="13378-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="13378-361">Hello activité A2 s’exécute lorsque hello planifiées tranches D2 deviennent disponibles et hello fréquence de disponibilité planifiée est atteinte.</span><span class="sxs-lookup"><span data-stu-id="13378-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="13378-362">S’il existe une erreur dans un des tranches hello dans dataset D2, A2 ne fonctionne pas pour ce secteur jusqu'à ce qu’il devienne disponible.</span><span class="sxs-lookup"><span data-stu-id="13378-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="13378-363">Hello vue de diagramme avec les deux activités Bonjour même pipeline ressemble à hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="13378-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![Chaînage des propriétés des activités Bonjour même pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="13378-365">Comme mentionné précédemment, les activités hello peuvent avoir différents pipelines.</span><span class="sxs-lookup"><span data-stu-id="13378-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="13378-366">Dans ce scénario, vue de diagramme hello ressemblerait hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="13378-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![Chaînage des activités dans deux pipelines](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="13378-368">Consultez hello [copier de manière séquentielle](#copy-sequentially) section annexe hello pour obtenir un exemple.</span><span class="sxs-lookup"><span data-stu-id="13378-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="13378-369">Modélisation des jeux de données avec des fréquences différentes</span><span class="sxs-lookup"><span data-stu-id="13378-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="13378-370">Dans les exemples de hello, les fréquences de hello pour entrée et de sortie des datasets et hello activité fenêtre de planification ont été hello même.</span><span class="sxs-lookup"><span data-stu-id="13378-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="13378-371">Certains scénarios requièrent la sortie de tooproduce hello possibilité à une fréquence autre que les fréquences hello d’une ou plusieurs entrées.</span><span class="sxs-lookup"><span data-stu-id="13378-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="13378-372">Data factory prend en charge la modélisation de ces scénarios.</span><span class="sxs-lookup"><span data-stu-id="13378-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="13378-373">Exemple 1 : production d’un rapport de sortie quotidien pour les données d’entrée est disponible toutes les heures</span><span class="sxs-lookup"><span data-stu-id="13378-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="13378-374">Imaginez un scénario dans lequel nous avons entré des données de mesure à partir de capteurs disponibles toutes les heures dans un stockage Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="13378-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="13378-375">Vous souhaitez tooproduce un rapport quotidien d’agrégation avec des statistiques, telles que la moyenne, maximum et minimum pour jour hello avec [activité hive de Data Factory](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="13378-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="13378-376">Voici ce que vous pouvez modéliser ce scénario avec data factory :</span><span class="sxs-lookup"><span data-stu-id="13378-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="13378-377">**Jeu de données d'entrée**</span><span class="sxs-lookup"><span data-stu-id="13378-377">**Input dataset**</span></span>

<span data-ttu-id="13378-378">Hello toutes les heures d’entrée de fichiers sont supprimés dans le dossier hello pour hello donné de jours.</span><span class="sxs-lookup"><span data-stu-id="13378-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="13378-379">La disponibilité de l’entrée est définie sur **Toutes les heures** (fréquence : Heure, intervalle: 1).</span><span class="sxs-lookup"><span data-stu-id="13378-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="13378-380">**Jeu de données de sortie**</span><span class="sxs-lookup"><span data-stu-id="13378-380">**Output dataset**</span></span>

<span data-ttu-id="13378-381">Un fichier de sortie est créé chaque jour dans le dossier du jour hello.</span><span class="sxs-lookup"><span data-stu-id="13378-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="13378-382">Disponibilité de sortie a pour valeur **Quotidien** (fréquence : jour et intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="13378-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="13378-383">**Activité : activité Hive dans un pipeline**</span><span class="sxs-lookup"><span data-stu-id="13378-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="13378-384">script de hive Hello reçoit hello approprié *DateTime* les informations qui utilisent hello **WindowStart** variable comme indiqué dans hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="13378-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="13378-385">script de hive Hello utilise ces données de hello de variable tooload à partir du dossier hello correct pour le jour de hello et exécutez hello agrégation toogenerate hello sortie.</span><span class="sxs-lookup"><span data-stu-id="13378-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

<span data-ttu-id="13378-386">Hello diagramme suivant illustre scénario hello à partir d’un point de vue de dépendances de données.</span><span class="sxs-lookup"><span data-stu-id="13378-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![Dépendance des données](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="13378-388">Hello tranche de sortie pour chaque jour dépend de 24 tranches horaires à partir d’un jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="13378-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="13378-389">Calcule de fabrique de données ces dépendances automatiquement en déterminant hello tranches de données d’entrée qui se trouvent dans hello même période que hello toobe de tranche de sortie généré.</span><span class="sxs-lookup"><span data-stu-id="13378-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="13378-390">Si une des tranches d’entrée de hello 24 n’est pas disponible, Data Factory attend toobe de tranche d’entrée hello prêt avant de commencer l’exécution d’activité quotidienne hello.</span><span class="sxs-lookup"><span data-stu-id="13378-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="13378-391">Exemple 2 : spécifier les dépendances avec des expressions et des fonctions Data Factory</span><span class="sxs-lookup"><span data-stu-id="13378-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="13378-392">Prenons en compte un autre scénario.</span><span class="sxs-lookup"><span data-stu-id="13378-392">Let’s consider another scenario.</span></span> <span data-ttu-id="13378-393">Supposez que vous avez une activité Hive qui traite deux jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="13378-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="13378-394">Un d’eux a de nouvelles données tous les jours, mais l’autre obtient de nouvelles données toutes les semaines.</span><span class="sxs-lookup"><span data-stu-id="13378-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="13378-395">Supposons que vous souhaitiez toodo une jointure entre les deux entrées de hello et produire une sortie chaque jour.</span><span class="sxs-lookup"><span data-stu-id="13378-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="13378-396">approche simple de Hello dans lequel Data Factory automatiquement cherche l’entrée de droite hello tranches tooprocess en alignant sortie toohello temps de la de tranche de données période ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="13378-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="13378-397">Vous devez spécifier que pour chaque exécution de l’activité, hello Data Factory doit utiliser la tranche de données de la dernière semaine de jeu de données d’entrée hebdomadaires hello.</span><span class="sxs-lookup"><span data-stu-id="13378-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="13378-398">Utilisez les fonctions Azure Data Factory comme Bonjour suivant extrait tooimplement ce comportement.</span><span class="sxs-lookup"><span data-stu-id="13378-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="13378-399">**Entrée1 : Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="13378-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="13378-400">Hello première entrée est hello Azure blob mis à jour quotidiennement.</span><span class="sxs-lookup"><span data-stu-id="13378-400">hello first input is hello Azure blob being updated daily.</span></span>

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="13378-401">**Entrée2 : objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="13378-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="13378-402">Entrée2 est hello Azure blob mis à jour chaque semaine.</span><span class="sxs-lookup"><span data-stu-id="13378-402">Input2 is hello Azure blob being updated weekly.</span></span>

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

<span data-ttu-id="13378-403">**Sortie : objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="13378-403">**Output: Azure blob**</span></span>

<span data-ttu-id="13378-404">Un fichier de sortie est créé chaque jour dans le dossier de hello pour le jour de hello.</span><span class="sxs-lookup"><span data-stu-id="13378-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="13378-405">Disponibilité de la sortie est définie trop**jour** (fréquence : Day, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="13378-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="13378-406">**Activité : activité Hive dans un pipeline**</span><span class="sxs-lookup"><span data-stu-id="13378-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="13378-407">activité de ruche Hello prend hello deux entrées et produit une tranche de sortie chaque jour.</span><span class="sxs-lookup"><span data-stu-id="13378-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="13378-408">Vous pouvez spécifier toodepend de tranche de sortie de tous les jours sur hello tranche d’entrée de la semaine précédente pour l’entrée hebdomadaire comme suit.</span><span class="sxs-lookup"><span data-stu-id="13378-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

<span data-ttu-id="13378-409">Pour obtenir la liste des fonctions et variables système prises en charge par Azure Data Factory, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="13378-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="13378-410">Annexe</span><span class="sxs-lookup"><span data-stu-id="13378-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="13378-411">Exemple : Copier de manière séquentielle</span><span class="sxs-lookup"><span data-stu-id="13378-411">Example: copy sequentially</span></span>
<span data-ttu-id="13378-412">Il est possible de toorun plusieurs opérations de copie une après l’autre de manière séquentielle/classés.</span><span class="sxs-lookup"><span data-stu-id="13378-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="13378-413">Par exemple, vous pouvez avoir deux datasets de sortie de données copie les activités dans un pipeline (CopyActivity1 et CopyActivity2) avec hello suivant d’entrée :</span><span class="sxs-lookup"><span data-stu-id="13378-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="13378-414">Activitédecopie1</span><span class="sxs-lookup"><span data-stu-id="13378-414">CopyActivity1</span></span>

<span data-ttu-id="13378-415">Jeu de données d'entrée.</span><span class="sxs-lookup"><span data-stu-id="13378-415">Input: Dataset.</span></span> <span data-ttu-id="13378-416">Sortie : Dataset2.</span><span class="sxs-lookup"><span data-stu-id="13378-416">Output: Dataset2.</span></span>

<span data-ttu-id="13378-417">Activitédecopie2</span><span class="sxs-lookup"><span data-stu-id="13378-417">CopyActivity2</span></span>

<span data-ttu-id="13378-418">Entrée : Jeudedonnées2.</span><span class="sxs-lookup"><span data-stu-id="13378-418">Input: Dataset2.</span></span>  <span data-ttu-id="13378-419">Sortie : Jeudedonnées3.</span><span class="sxs-lookup"><span data-stu-id="13378-419">Output: Dataset3.</span></span>

<span data-ttu-id="13378-420">CopyActivity2 s’exécute uniquement si hello CopyActivity1 a exécuté avec succès et Dataset2 est disponible.</span><span class="sxs-lookup"><span data-stu-id="13378-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="13378-421">Voici le code JSON de pipeline exemple hello :</span><span class="sxs-lookup"><span data-stu-id="13378-421">Here is hello sample pipeline JSON:</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="13378-422">Notez que dans l’exemple de hello, le dataset de sortie hello Hello première activité de copie (Dataset2) est spécifié en tant qu’entrée pour la deuxième activité hello.</span><span class="sxs-lookup"><span data-stu-id="13378-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="13378-423">Par conséquent, hello deuxième activité s’exécute uniquement lorsque le dataset de sortie hello à partir de la première activité hello est prêt.</span><span class="sxs-lookup"><span data-stu-id="13378-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="13378-424">Dans l’exemple de hello, CopyActivity2 peut avoir une entrée différents, tels que Dataset3, mais vous spécifiez Dataset2 comme une tooCopyActivity2 d’entrée, afin de l’activité hello ne s’exécute pas avant la fin de CopyActivity1.</span><span class="sxs-lookup"><span data-stu-id="13378-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="13378-425">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="13378-425">For example:</span></span>

<span data-ttu-id="13378-426">Activitédecopie1</span><span class="sxs-lookup"><span data-stu-id="13378-426">CopyActivity1</span></span>

<span data-ttu-id="13378-427">Entrée : Jeudedonnées1.</span><span class="sxs-lookup"><span data-stu-id="13378-427">Input: Dataset1.</span></span> <span data-ttu-id="13378-428">Sortie : Dataset2.</span><span class="sxs-lookup"><span data-stu-id="13378-428">Output: Dataset2.</span></span>

<span data-ttu-id="13378-429">Activitédecopie2</span><span class="sxs-lookup"><span data-stu-id="13378-429">CopyActivity2</span></span>

<span data-ttu-id="13378-430">Entrées : Jeudedonnées3, Jeudedonnées2.</span><span class="sxs-lookup"><span data-stu-id="13378-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="13378-431">Sortie : Jeudedonnées4.</span><span class="sxs-lookup"><span data-stu-id="13378-431">Output: Dataset4.</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="13378-432">Notez que dans l’exemple de hello, deux jeux de données d’entrée est spécifiés pour la deuxième activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="13378-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="13378-433">Lorsque plusieurs entrées sont spécifiées, uniquement hello première entrée jeu de données est utilisé pour copier des données, mais les autres jeux de données est utilisés en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="13378-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="13378-434">CopyActivity2 démarre uniquement une fois hello conditions suivantes sont remplies :</span><span class="sxs-lookup"><span data-stu-id="13378-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="13378-435">ActivitédeCopie1 s’est terminée avec succès et JeudeDonnées2 est disponible.</span><span class="sxs-lookup"><span data-stu-id="13378-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="13378-436">Ce jeu de données n’est pas utilisé lors de la copie des données tooDataset4.</span><span class="sxs-lookup"><span data-stu-id="13378-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="13378-437">Il sert uniquement de dépendance de planification pour ActivitédeCopie2.</span><span class="sxs-lookup"><span data-stu-id="13378-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="13378-438">JeudeDonnées3 est disponible.</span><span class="sxs-lookup"><span data-stu-id="13378-438">Dataset3 is available.</span></span> <span data-ttu-id="13378-439">Ce jeu de données représente des données hello sont copié toohello destination.</span><span class="sxs-lookup"><span data-stu-id="13378-439">This dataset represents hello data that is copied toohello destination.</span></span> 
