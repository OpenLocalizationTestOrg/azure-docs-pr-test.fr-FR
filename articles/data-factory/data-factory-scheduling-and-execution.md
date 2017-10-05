---
title: "Planification et exécution avec Data Factory | Microsoft Docs"
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
ms.openlocfilehash: e6fd92cde91ae5f171c855c07fa8974a19703b41
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="12706-103">Planification et exécution avec Data Factory</span><span class="sxs-lookup"><span data-stu-id="12706-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="12706-104">Cet article explique les aspects de la planification et de l’exécution du modèle d’application Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="12706-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> <span data-ttu-id="12706-105">Cet article suppose que vous avez des notions de base sur les concepts de modèle de données Data Factory, dont l’activité, les pipelines, les services connexes et les groupes de données.</span><span class="sxs-lookup"><span data-stu-id="12706-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="12706-106">Pour les concepts de base d’Azure Data Factory, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="12706-106">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="12706-107">Présentation de Data Factory</span><span class="sxs-lookup"><span data-stu-id="12706-107">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="12706-108">Pipelines</span><span class="sxs-lookup"><span data-stu-id="12706-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="12706-109">Groupes de données</span><span class="sxs-lookup"><span data-stu-id="12706-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="12706-110">Heures de début et de fin de pipeline</span><span class="sxs-lookup"><span data-stu-id="12706-110">Start and end times of pipeline</span></span>
<span data-ttu-id="12706-111">Un pipeline est actif uniquement entre son heure de **début** et son heure de **fin**.</span><span class="sxs-lookup"><span data-stu-id="12706-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="12706-112">Il n'est pas exécuté avant l'heure de début, ni après l'heure de fin.</span><span class="sxs-lookup"><span data-stu-id="12706-112">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="12706-113">Lorsque le pipeline est suspendu, il n’est pas exécuté, quelle que soit son heure de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="12706-113">If the pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="12706-114">Pour qu'un pipeline soit exécuté, il ne doit pas être suspendu.</span><span class="sxs-lookup"><span data-stu-id="12706-114">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="12706-115">Vous trouvez ces paramètres (début, fin, suspendu) dans la définition du pipeline :</span><span class="sxs-lookup"><span data-stu-id="12706-115">You find these settings (start, end, paused) in the pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="12706-116">Pour plus d’informations sur ces propriétés, consultez l’article [Créer des pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="12706-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="12706-117">Spécifier la planification d’une activité</span><span class="sxs-lookup"><span data-stu-id="12706-117">Specify schedule for an activity</span></span>
<span data-ttu-id="12706-118">Ce n’est pas le pipeline qui est exécuté.</span><span class="sxs-lookup"><span data-stu-id="12706-118">It is not the pipeline that is executed.</span></span> <span data-ttu-id="12706-119">Ce sont les activités dans le pipeline qui sont exécutées dans le contexte global du pipeline.</span><span class="sxs-lookup"><span data-stu-id="12706-119">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span></span> <span data-ttu-id="12706-120">Vous pouvez planifier l’activité pour qu’elle s’exécute de façon récurrente grâce à la section **scheduler** (planificateur) de l’activité JSON.</span><span class="sxs-lookup"><span data-stu-id="12706-120">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span></span> <span data-ttu-id="12706-121">Par exemple, vous pouvez planifier l’exécution d’une activité toutes les heures comme suit :</span><span class="sxs-lookup"><span data-stu-id="12706-121">For example, you can schedule an activity to run hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="12706-122">Comme illustré dans le diagramme suivant, la définition d’une planification pour une activité crée une série de fenêtres récurrentes dans les heures de début et de fin du pipeline.</span><span class="sxs-lookup"><span data-stu-id="12706-122">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span></span> <span data-ttu-id="12706-123">Les fenêtres récurrentes sont une série d’intervalles de temps fixes contigus, qui ne se chevauchent pas.</span><span class="sxs-lookup"><span data-stu-id="12706-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="12706-124">Ces fenêtres récurrentes logiques pour une activité sont appelées des **fenêtres d’activité**.</span><span class="sxs-lookup"><span data-stu-id="12706-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Exemple de planificateur d’activité](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="12706-126">La propriété **scheduler** (planificateur) d’une activité est facultative.</span><span class="sxs-lookup"><span data-stu-id="12706-126">The **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="12706-127">Si vous définissez cette propriété, elle doit correspondre à la cadence que vous spécifiez dans la définition du jeu de données de sortie pour l’activité.</span><span class="sxs-lookup"><span data-stu-id="12706-127">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span></span> <span data-ttu-id="12706-128">Le jeu de données de sortie pilote actuellement la planification.</span><span class="sxs-lookup"><span data-stu-id="12706-128">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="12706-129">Vous devez donc créer un jeu de données de sortie même si l’activité ne génère aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="12706-129">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="12706-130">Spécifier la planification d’un jeu de données</span><span class="sxs-lookup"><span data-stu-id="12706-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="12706-131">Une activité dans un pipeline Data Factory peut inclure zéro ou plusieurs **jeux de données** d’entrée et produire un ou plusieurs jeux de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="12706-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="12706-132">Pour une activité, vous pouvez spécifier la cadence à laquelle les données d’entrée sont disponibles ou les données de sortie sont produites à l’aide de la section **availability** (disponibilité) dans les définitions de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="12706-132">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span></span> 

<span data-ttu-id="12706-133">La **Fréquence** dans la section **availability** (disponibilité) spécifie l’unité de temps.</span><span class="sxs-lookup"><span data-stu-id="12706-133">**Frequency** in the **availability** section specifies the time unit.</span></span> <span data-ttu-id="12706-134">Les valeurs autorisées pour la fréquence sont : minute, heure, jour, semaine et mois.</span><span class="sxs-lookup"><span data-stu-id="12706-134">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="12706-135">La propriété **interval** (intervalle) dans la section availability (disponibilité) spécifie un multiplicateur de fréquence.</span><span class="sxs-lookup"><span data-stu-id="12706-135">The **interval** property in the availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="12706-136">Par exemple : si la fréquence est définie sur Jour et l’intervalle sur 1 pour un jeu de données de sortie, les données de sortie sont produites chaque jour.</span><span class="sxs-lookup"><span data-stu-id="12706-136">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span></span> <span data-ttu-id="12706-137">Si vous définissez la fréquence en minutes, nous vous recommandons de définir l’intervalle sur une valeur au moins égale à 15.</span><span class="sxs-lookup"><span data-stu-id="12706-137">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span></span> 

<span data-ttu-id="12706-138">Dans l’exemple suivant, les données d’entrée seront disponibles toutes les heures et les données de sortie sont produites toutes les heures (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="12706-138">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="12706-139">**Jeu de données d'entrée :**</span><span class="sxs-lookup"><span data-stu-id="12706-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="12706-140">**Jeu de données de sortie**</span><span class="sxs-lookup"><span data-stu-id="12706-140">**Output dataset**</span></span>

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

<span data-ttu-id="12706-141">Le **jeu de données de sortie pilote actuellement la planification**.</span><span class="sxs-lookup"><span data-stu-id="12706-141">Currently, **output dataset drives the schedule**.</span></span> <span data-ttu-id="12706-142">En d’autres termes, la planification spécifiée pour le jeu de données de sortie est utilisée pour exécuter une activité lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="12706-142">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span></span> <span data-ttu-id="12706-143">Vous devez donc créer un jeu de données de sortie même si l’activité ne génère aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="12706-143">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="12706-144">Si l’activité ne prend aucune entrée, vous pouvez ignorer la création du jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="12706-144">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 

<span data-ttu-id="12706-145">Dans la définition de pipeline suivante, la propriété **scheduler** (planificateur) est utilisée pour spécifier la planification de l’activité.</span><span class="sxs-lookup"><span data-stu-id="12706-145">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span></span> <span data-ttu-id="12706-146">Cette propriété est facultative.</span><span class="sxs-lookup"><span data-stu-id="12706-146">This property is optional.</span></span> <span data-ttu-id="12706-147">La planification de l’activité doit actuellement correspondre à la planification spécifiée pour le jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="12706-147">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span></span>
 
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

<span data-ttu-id="12706-148">Dans cet exemple, l’activité s’exécute toutes les heures entre les heures de début et de fin du pipeline.</span><span class="sxs-lookup"><span data-stu-id="12706-148">In this example, the activity runs hourly between the start and end times of the pipeline.</span></span> <span data-ttu-id="12706-149">Les données de sortie sont produites toutes les heures pour des trois fenêtres de temps (8h-9h, 9h-10h et 10h-11h).</span><span class="sxs-lookup"><span data-stu-id="12706-149">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="12706-150">Chaque unité de données consommée ou produite pendant l’exécution d’une activité est appelée **tranche de données**.</span><span class="sxs-lookup"><span data-stu-id="12706-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="12706-151">Le diagramme suivant illustre un exemple d’une activité avec un jeu de données d’entrée et un jeu de données de sortie :</span><span class="sxs-lookup"><span data-stu-id="12706-151">The following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Planificateur de disponibilité](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="12706-153">Les tranches de données recueillies toutes les heures pour le jeu de données d’entrée et de sortie sont affichées dans le diagramme.</span><span class="sxs-lookup"><span data-stu-id="12706-153">The diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="12706-154">Le diagramme illustre trois tranches d’entrée qui sont prêtes pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="12706-154">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="12706-155">L’activité de 10 à 11 h est en cours, et produit la tranche de sortie de 10 à 11 h.</span><span class="sxs-lookup"><span data-stu-id="12706-155">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span> 

<span data-ttu-id="12706-156">Vous pouvez accéder à l’intervalle de temps associé à la tranche actuelle dans le jeu de données JSON à l’aide des variables [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) et [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="12706-156">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="12706-157">De même, vous pouvez accéder à l’intervalle de temps associé à une fenêtre d’activité à l’aide des variables WindowStart et WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="12706-157">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span></span> <span data-ttu-id="12706-158">La planification d’une activité doit correspondre à la planification du jeu de données de sortie pour l’activité.</span><span class="sxs-lookup"><span data-stu-id="12706-158">The schedule of an activity must match the schedule of the output dataset for the activity.</span></span> <span data-ttu-id="12706-159">Par conséquent, les valeurs SliceStart et SliceEnd sont identiques aux valeurs WindowStart et WindowEnd, respectivement.</span><span class="sxs-lookup"><span data-stu-id="12706-159">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="12706-160">Pour plus d’informations sur ces variables, consultez les articles [Variables système et fonctions Data Factory](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="12706-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="12706-161">Vous pouvez utiliser ces variables à différentes fins dans votre activité JSON.</span><span class="sxs-lookup"><span data-stu-id="12706-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="12706-162">Par exemple, vous pouvez les utiliser pour sélectionner les données à partir des jeux de données d’entrée et de sortie représentant les données de série chronologique (par exemple : 8h à 9h).</span><span class="sxs-lookup"><span data-stu-id="12706-162">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span></span> <span data-ttu-id="12706-163">Cet exemple utilise également **WindowStart** et **WindowEnd** pour sélectionner les données pertinentes pour l’exécution d’une activité et les copier sur un objet Blob avec le bon **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="12706-163">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="12706-164">**folderPath** est paramétré pour avoir un dossier distinct pour chaque heure.</span><span class="sxs-lookup"><span data-stu-id="12706-164">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>  

<span data-ttu-id="12706-165">Dans l’exemple précédent, la planification spécifiée pour les jeux de données d’entrée et de sortie est la même (toutes les heures).</span><span class="sxs-lookup"><span data-stu-id="12706-165">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span></span> <span data-ttu-id="12706-166">Si le jeu de données d’entrée de l’activité est disponible à une fréquence différente, par exemple toutes les 15 minutes, l’activité qui produit ce jeu de données de sortie est toujours exécutée une fois par heure car le jeu de données de sortie pilote la planification de l’activité.</span><span class="sxs-lookup"><span data-stu-id="12706-166">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span></span> <span data-ttu-id="12706-167">Pour plus d’informations, consultez [Modélisation des jeux de données avec des fréquences différentes](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="12706-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="12706-168">Disponibilité et stratégies du jeu de données</span><span class="sxs-lookup"><span data-stu-id="12706-168">Dataset availability and policies</span></span>
<span data-ttu-id="12706-169">Vous avez vu l’utilisation des propriétés de fréquence et d’intervalle de la section availability (disponibilité) de la définition du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="12706-169">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span></span> <span data-ttu-id="12706-170">D’autres propriétés affectent la planification et l’exécution d’une activité.</span><span class="sxs-lookup"><span data-stu-id="12706-170">There are a few other properties that affect the scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="12706-171">Disponibilité du jeu de données</span><span class="sxs-lookup"><span data-stu-id="12706-171">Dataset availability</span></span> 
<span data-ttu-id="12706-172">Le tableau suivant décrit les propriétés que vous pouvez utiliser dans la section **availability** :</span><span class="sxs-lookup"><span data-stu-id="12706-172">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="12706-173">Propriété</span><span class="sxs-lookup"><span data-stu-id="12706-173">Property</span></span> | <span data-ttu-id="12706-174">Description</span><span class="sxs-lookup"><span data-stu-id="12706-174">Description</span></span> | <span data-ttu-id="12706-175">Requis</span><span class="sxs-lookup"><span data-stu-id="12706-175">Required</span></span> | <span data-ttu-id="12706-176">Default</span><span class="sxs-lookup"><span data-stu-id="12706-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12706-177">frequency</span><span class="sxs-lookup"><span data-stu-id="12706-177">frequency</span></span> |<span data-ttu-id="12706-178">Spécifie l’unité de temps pour la production du segment du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="12706-178">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="12706-179"><b>Fréquence prise en charge</b>: minute, heure, jour, semaine, mois</span><span class="sxs-lookup"><span data-stu-id="12706-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="12706-180">Oui</span><span class="sxs-lookup"><span data-stu-id="12706-180">Yes</span></span> |<span data-ttu-id="12706-181">N/D</span><span class="sxs-lookup"><span data-stu-id="12706-181">NA</span></span> |
| <span data-ttu-id="12706-182">interval</span><span class="sxs-lookup"><span data-stu-id="12706-182">interval</span></span> |<span data-ttu-id="12706-183">Spécifie un multiplicateur de fréquence</span><span class="sxs-lookup"><span data-stu-id="12706-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="12706-184">«Frequency» et «interval» déterminent la fréquence à laquelle la tranche est produite.</span><span class="sxs-lookup"><span data-stu-id="12706-184">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="12706-185">Si vous voulez des tranches de jeu de données d’une heure, définissez <b>frequency</b> sur <b>Hour</b> et <b>interval</b> sur <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="12706-185">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="12706-186"><b>Remarque :</b> si vous définissez la fréquence en minutes, nous vous recommandons de définir l’intervalle sur une valeur au moins égale à 15.</span><span class="sxs-lookup"><span data-stu-id="12706-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="12706-187">Oui</span><span class="sxs-lookup"><span data-stu-id="12706-187">Yes</span></span> |<span data-ttu-id="12706-188">N/D</span><span class="sxs-lookup"><span data-stu-id="12706-188">NA</span></span> |
| <span data-ttu-id="12706-189">style</span><span class="sxs-lookup"><span data-stu-id="12706-189">style</span></span> |<span data-ttu-id="12706-190">Spécifie si le segment doit être généré au début / à la fin de l’intervalle.</span><span class="sxs-lookup"><span data-stu-id="12706-190">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="12706-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="12706-191">StartOfInterval</span></span></li><li><span data-ttu-id="12706-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="12706-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="12706-193">Si la fréquence est définie sur Month et le style défini sur EndOfInterval, le segment est généré le dernier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="12706-193">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="12706-194">Si le style est défini sur StartOfInterval, le segment est généré le premier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="12706-194">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="12706-195">Si la fréquence est définie sur Day et le style défini sur EndOfInterval, le segment est généré la dernière heure du jour.</span><span class="sxs-lookup"><span data-stu-id="12706-195">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="12706-196">Si la fréquence est définie sur Hour et le style défini sur EndOfInterval, le segment est généré à la fin de l’heure.</span><span class="sxs-lookup"><span data-stu-id="12706-196">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="12706-197">Par exemple, pour un segment de la période 13 h-14 h, le segment est généré à 14 h.</span><span class="sxs-lookup"><span data-stu-id="12706-197">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="12706-198">Non</span><span class="sxs-lookup"><span data-stu-id="12706-198">No</span></span> |<span data-ttu-id="12706-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="12706-199">EndOfInterval</span></span> |
| <span data-ttu-id="12706-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="12706-200">anchorDateTime</span></span> |<span data-ttu-id="12706-201">Définit la position absolue dans le temps utilisée par le planificateur pour calculer les limites de tranche de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="12706-201">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="12706-202"><b>Remarque :</b> si AnchorDateTime contient des éléments de date plus précis que la fréquence, ces éléments plus précis sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="12706-202"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="12706-203">Par exemple, si <b>interval</b> est défini sur <b>hourly</b> (frequency : hour et interval : 1) et si <b>AnchorDateTime</b> contient <b>minutes et seconds</b>, les parties <b>minutes et seconds</b> de la valeur AnchorDateTime sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="12706-203">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="12706-204">Non</span><span class="sxs-lookup"><span data-stu-id="12706-204">No</span></span> |<span data-ttu-id="12706-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="12706-205">01/01/0001</span></span> |
| <span data-ttu-id="12706-206">Offset</span><span class="sxs-lookup"><span data-stu-id="12706-206">offset</span></span> |<span data-ttu-id="12706-207">Intervalle de temps marquant le déplacement du début et de la fin de toutes les tranches du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="12706-207">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="12706-208"><b>Remarque :</b> si anchorDateTime et offset sont spécifiés, un décalage combiné est obtenu.</span><span class="sxs-lookup"><span data-stu-id="12706-208"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="12706-209">Non</span><span class="sxs-lookup"><span data-stu-id="12706-209">No</span></span> |<span data-ttu-id="12706-210">N/D</span><span class="sxs-lookup"><span data-stu-id="12706-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="12706-211">exemple offset</span><span class="sxs-lookup"><span data-stu-id="12706-211">offset example</span></span>
<span data-ttu-id="12706-212">Par défaut, les tranches quotidiennes (`"frequency": "Day", "interval": 1`) commencent à 0 h UTC (minuit).</span><span class="sxs-lookup"><span data-stu-id="12706-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="12706-213">Si vous souhaitez que l’heure de début soit 6 h UTC, définissez le décalage comme indiqué dans l’extrait suivant :</span><span class="sxs-lookup"><span data-stu-id="12706-213">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="12706-214">Exemple anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="12706-214">anchorDateTime example</span></span>
<span data-ttu-id="12706-215">Dans l’exemple suivant, le jeu de données est généré toutes les 23 heures.</span><span class="sxs-lookup"><span data-stu-id="12706-215">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="12706-216">La première tranche commence à l’heure spécifiée par anchorDateTime, qui est défini sur `2017-04-19T08:00:00` (heure UTC).</span><span class="sxs-lookup"><span data-stu-id="12706-216">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="12706-217">Exemple de décalage/style</span><span class="sxs-lookup"><span data-stu-id="12706-217">offset/style Example</span></span>
<span data-ttu-id="12706-218">Le jeu de données suivant est un jeu de données mensuel et est généré le 3 de chaque mois à 8h00 (`3.08:00:00`) :</span><span class="sxs-lookup"><span data-stu-id="12706-218">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="12706-219">Stratégie du jeu de données</span><span class="sxs-lookup"><span data-stu-id="12706-219">Dataset policy</span></span>
<span data-ttu-id="12706-220">Un jeu de données peut avoir une stratégie de validation définie qui spécifie comment les données générées par l’exécution d’une tranche peuvent être validées avant qu’il soit prêt à la consommation.</span><span class="sxs-lookup"><span data-stu-id="12706-220">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="12706-221">Dans ce cas, une fois que la tranche a terminé l’exécution, l’état de la tranche de sortie devient **En attente** avec un sous-état **Validation**.</span><span class="sxs-lookup"><span data-stu-id="12706-221">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="12706-222">Une fois les tranches validées, l’état de la tranche passe à **prêt**.</span><span class="sxs-lookup"><span data-stu-id="12706-222">After the slices are validated, the slice status changes to **Ready**.</span></span> <span data-ttu-id="12706-223">Si une tranche de données a été générée mais n’a pas réussi la validation, l’activité s’exécute pour les tranches en aval dépendant de cette tranche qui ne sont pas traitées.</span><span class="sxs-lookup"><span data-stu-id="12706-223">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="12706-224">[Surveiller et gérer les pipelines](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="12706-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

<span data-ttu-id="12706-225">La section **policy** de la définition du jeu de données définit les critères ou la condition que les segments du jeu de données doivent remplir.</span><span class="sxs-lookup"><span data-stu-id="12706-225">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span> <span data-ttu-id="12706-226">Le tableau suivant décrit les propriétés que vous pouvez utiliser dans la section **policy** (stratégie) :</span><span class="sxs-lookup"><span data-stu-id="12706-226">The following table describes properties you can use in the **policy** section:</span></span>

| <span data-ttu-id="12706-227">Nom de la stratégie</span><span class="sxs-lookup"><span data-stu-id="12706-227">Policy Name</span></span> | <span data-ttu-id="12706-228">Description</span><span class="sxs-lookup"><span data-stu-id="12706-228">Description</span></span> | <span data-ttu-id="12706-229">Appliqué(e) à</span><span class="sxs-lookup"><span data-stu-id="12706-229">Applied To</span></span> | <span data-ttu-id="12706-230">Requis</span><span class="sxs-lookup"><span data-stu-id="12706-230">Required</span></span> | <span data-ttu-id="12706-231">Default</span><span class="sxs-lookup"><span data-stu-id="12706-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="12706-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="12706-232">minimumSizeMB</span></span> | <span data-ttu-id="12706-233">Valide le fait que les données dans un **objet blob Azure** répondent aux exigences de taille minimale (en mégaoctets).</span><span class="sxs-lookup"><span data-stu-id="12706-233">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="12706-234">objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="12706-234">Azure Blob</span></span> |<span data-ttu-id="12706-235">Non</span><span class="sxs-lookup"><span data-stu-id="12706-235">No</span></span> |<span data-ttu-id="12706-236">N/D</span><span class="sxs-lookup"><span data-stu-id="12706-236">NA</span></span> |
| <span data-ttu-id="12706-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="12706-237">minimumRows</span></span> | <span data-ttu-id="12706-238">Valide le fait que les données dans une **base de données SQL Azure** ou une **table Azure** contiennent le nombre minimal de lignes.</span><span class="sxs-lookup"><span data-stu-id="12706-238">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="12706-239">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="12706-239">Azure SQL Database</span></span></li><li><span data-ttu-id="12706-240">table Azure</span><span class="sxs-lookup"><span data-stu-id="12706-240">Azure Table</span></span></li></ul> |<span data-ttu-id="12706-241">Non</span><span class="sxs-lookup"><span data-stu-id="12706-241">No</span></span> |<span data-ttu-id="12706-242">N/D</span><span class="sxs-lookup"><span data-stu-id="12706-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="12706-243">Exemples</span><span class="sxs-lookup"><span data-stu-id="12706-243">Examples</span></span>
<span data-ttu-id="12706-244">**minimumSizeMB :**</span><span class="sxs-lookup"><span data-stu-id="12706-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="12706-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="12706-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="12706-246">Pour plus d’informations sur ces propriétés et exemples, consultez l’article [Créer des jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="12706-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="12706-247">Stratégies d’activité</span><span class="sxs-lookup"><span data-stu-id="12706-247">Activity policies</span></span>
<span data-ttu-id="12706-248">Les stratégies affectent le comportement d'exécution d'une activité, en particulier lors du traitement du segment d'une table.</span><span class="sxs-lookup"><span data-stu-id="12706-248">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="12706-249">Le tableau suivant fournit les détails.</span><span class="sxs-lookup"><span data-stu-id="12706-249">The following table provides the details.</span></span>

| <span data-ttu-id="12706-250">Propriété</span><span class="sxs-lookup"><span data-stu-id="12706-250">Property</span></span> | <span data-ttu-id="12706-251">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="12706-251">Permitted values</span></span> | <span data-ttu-id="12706-252">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="12706-252">Default Value</span></span> | <span data-ttu-id="12706-253">Description</span><span class="sxs-lookup"><span data-stu-id="12706-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12706-254">accès concurrentiel</span><span class="sxs-lookup"><span data-stu-id="12706-254">concurrency</span></span> |<span data-ttu-id="12706-255">Entier </span><span class="sxs-lookup"><span data-stu-id="12706-255">Integer</span></span> <br/><br/><span data-ttu-id="12706-256">Valeur max : 10</span><span class="sxs-lookup"><span data-stu-id="12706-256">Max value: 10</span></span> |<span data-ttu-id="12706-257">1</span><span class="sxs-lookup"><span data-stu-id="12706-257">1</span></span> |<span data-ttu-id="12706-258">Nombre d’exécutions simultanées de l’activité.</span><span class="sxs-lookup"><span data-stu-id="12706-258">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="12706-259">Il détermine le nombre d’exécutions en parallèle de l’activité qui peuvent se produire sur différents segments.</span><span class="sxs-lookup"><span data-stu-id="12706-259">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="12706-260">Par exemple, si une activité doit passer par un grand ensemble de données disponibles, une valeur de concurrence plus élevée accélère le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="12706-260">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="12706-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="12706-261">executionPriorityOrder</span></span> |<span data-ttu-id="12706-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="12706-262">NewestFirst</span></span><br/><br/><span data-ttu-id="12706-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="12706-263">OldestFirst</span></span> |<span data-ttu-id="12706-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="12706-264">OldestFirst</span></span> |<span data-ttu-id="12706-265">Détermine l’ordre des segments de données qui sont traités.</span><span class="sxs-lookup"><span data-stu-id="12706-265">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="12706-266">Par exemple, si vous avez 2 segments (l’un se produisant à 16 heures et l’autre à 17 heures) et que les deux sont en attente d’exécution.</span><span class="sxs-lookup"><span data-stu-id="12706-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="12706-267">Si vous définissez executionPriorityOrder sur NewestFirst, le segment à 17 h est traité en premier.</span><span class="sxs-lookup"><span data-stu-id="12706-267">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="12706-268">De même, si vous définissez executionPriorityOrder sur OldestFIrst, le segment à 16 h est traité en premier.</span><span class="sxs-lookup"><span data-stu-id="12706-268">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="12706-269">retry</span><span class="sxs-lookup"><span data-stu-id="12706-269">retry</span></span> |<span data-ttu-id="12706-270">Entier </span><span class="sxs-lookup"><span data-stu-id="12706-270">Integer</span></span><br/><br/><span data-ttu-id="12706-271">La valeur max peut être 10</span><span class="sxs-lookup"><span data-stu-id="12706-271">Max value can be 10</span></span> |<span data-ttu-id="12706-272">0</span><span class="sxs-lookup"><span data-stu-id="12706-272">0</span></span> |<span data-ttu-id="12706-273">Nombre de nouvelles tentatives avant que le traitement des données du segment ne soit marqué comme un échec.</span><span class="sxs-lookup"><span data-stu-id="12706-273">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="12706-274">L'exécution de l'activité pour un segment de données est répétée jusqu'au nombre de tentatives spécifié.</span><span class="sxs-lookup"><span data-stu-id="12706-274">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="12706-275">La nouvelle tentative est effectuée dès que possible après l'échec.</span><span class="sxs-lookup"><span data-stu-id="12706-275">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="12706-276">timeout</span><span class="sxs-lookup"><span data-stu-id="12706-276">timeout</span></span> |<span data-ttu-id="12706-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="12706-277">TimeSpan</span></span> |<span data-ttu-id="12706-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="12706-278">00:00:00</span></span> |<span data-ttu-id="12706-279">Délai d'expiration de l'activité.</span><span class="sxs-lookup"><span data-stu-id="12706-279">Timeout for the activity.</span></span> <span data-ttu-id="12706-280">Exemple : 00:10:00 (implique un délai d’expiration de 10 minutes)</span><span class="sxs-lookup"><span data-stu-id="12706-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="12706-281">Si une valeur n’est pas spécifiée ou est égale à 0, le délai d’expiration est infini.</span><span class="sxs-lookup"><span data-stu-id="12706-281">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="12706-282">Si le temps de traitement des données sur un segment dépasse la valeur du délai d’expiration, il est annulé et le système tente de réexécuter le traitement.</span><span class="sxs-lookup"><span data-stu-id="12706-282">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="12706-283">Le nombre de nouvelles tentatives dépend de la propriété « retry ».</span><span class="sxs-lookup"><span data-stu-id="12706-283">The number of retries depends on the retry property.</span></span> <span data-ttu-id="12706-284">Quand le délai d’expiration est atteint, l’état est défini sur TimedOut.</span><span class="sxs-lookup"><span data-stu-id="12706-284">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="12706-285">delay</span><span class="sxs-lookup"><span data-stu-id="12706-285">delay</span></span> |<span data-ttu-id="12706-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="12706-286">TimeSpan</span></span> |<span data-ttu-id="12706-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="12706-287">00:00:00</span></span> |<span data-ttu-id="12706-288">Spécifie le délai avant le début du traitement des données du segment.</span><span class="sxs-lookup"><span data-stu-id="12706-288">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="12706-289">L’exécution d’activité pour une tranche de données est démarrée une fois que le délai a dépassé l’heure d’exécution prévue.</span><span class="sxs-lookup"><span data-stu-id="12706-289">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="12706-290">Exemple : 00:10:00 (implique un délai de 10 minutes)</span><span class="sxs-lookup"><span data-stu-id="12706-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="12706-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="12706-291">longRetry</span></span> |<span data-ttu-id="12706-292">Entier </span><span class="sxs-lookup"><span data-stu-id="12706-292">Integer</span></span><br/><br/><span data-ttu-id="12706-293">Valeur max : 10</span><span class="sxs-lookup"><span data-stu-id="12706-293">Max value: 10</span></span> |<span data-ttu-id="12706-294">1</span><span class="sxs-lookup"><span data-stu-id="12706-294">1</span></span> |<span data-ttu-id="12706-295">Le nombre de nouvelles tentatives longues avant l’échec de l’exécution du segment.</span><span class="sxs-lookup"><span data-stu-id="12706-295">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="12706-296">Les tentatives longRetry sont espacées par longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="12706-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="12706-297">Par conséquent, si vous devez spécifier un délai entre chaque tentative, utilisez longRetry.</span><span class="sxs-lookup"><span data-stu-id="12706-297">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="12706-298">Si les valeurs Retry et longRetry sont spécifiées, chaque tentative longRetry inclut des tentatives Retry et le nombre maximal de tentatives sera égal à Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="12706-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="12706-299">Par exemple, si nous avons les paramètres suivants dans la stratégie de l’activité :</span><span class="sxs-lookup"><span data-stu-id="12706-299">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="12706-300">Retry : 3</span><span class="sxs-lookup"><span data-stu-id="12706-300">Retry: 3</span></span><br/><span data-ttu-id="12706-301">longRetry : 2</span><span class="sxs-lookup"><span data-stu-id="12706-301">longRetry: 2</span></span><br/><span data-ttu-id="12706-302">longRetryInterval : 01:00:00</span><span class="sxs-lookup"><span data-stu-id="12706-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="12706-303">Supposons qu’il existe un seul segment à exécuter (dont l’état est Waiting) et que l’exécution de l’activité échoue à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="12706-303">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="12706-304">Au départ, il y aurait 3 tentatives consécutives d'exécution.</span><span class="sxs-lookup"><span data-stu-id="12706-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="12706-305">Après chaque tentative, l’état du segment serait Retry.</span><span class="sxs-lookup"><span data-stu-id="12706-305">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="12706-306">Une fois les 3 premières tentatives terminées, l’état du segment serait LongRetry.</span><span class="sxs-lookup"><span data-stu-id="12706-306">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="12706-307">Après une heure (c’est-à-dire la valeur de longRetryInterval), il y aurait un autre ensemble de 3 tentatives consécutives d’exécution.</span><span class="sxs-lookup"><span data-stu-id="12706-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="12706-308">Ensuite, l'état du segment serait Failed et aucune autre tentative ne serait exécutée.</span><span class="sxs-lookup"><span data-stu-id="12706-308">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="12706-309">Par conséquent, 6 tentatives ont été exécutées.</span><span class="sxs-lookup"><span data-stu-id="12706-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="12706-310">Si une exécution réussit, l’état de la tranche est Ready et aucune nouvelle tentative n’est tentée.</span><span class="sxs-lookup"><span data-stu-id="12706-310">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="12706-311">La valeur longRetry peut être utilisée dans les situations où les données dépendantes arrivent à des moments non déterministes ou lorsque l’environnement global où le traitement des données se produit est douteux.</span><span class="sxs-lookup"><span data-stu-id="12706-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="12706-312">Dans ces cas, l’exécution de nouvelles tentatives l’une après l’autre peut ne pas être utile et procéder ainsi après un intervalle de temps précis produit la sortie désirée.</span><span class="sxs-lookup"><span data-stu-id="12706-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="12706-313">Mise en garde : ne définissez pas de valeurs élevées pour longRetry ou longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="12706-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="12706-314">En règle générale, des valeurs plus élevées impliquent d’autres problèmes systémiques.</span><span class="sxs-lookup"><span data-stu-id="12706-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="12706-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="12706-315">longRetryInterval</span></span> |<span data-ttu-id="12706-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="12706-316">TimeSpan</span></span> |<span data-ttu-id="12706-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="12706-317">00:00:00</span></span> |<span data-ttu-id="12706-318">Le délai entre les nouvelles tentatives longues</span><span class="sxs-lookup"><span data-stu-id="12706-318">The delay between long retry attempts</span></span> |

<span data-ttu-id="12706-319">Pour plus d’informations, consultez l’article [Pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="12706-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="12706-320">Traitement en parallèle des tranches de données</span><span class="sxs-lookup"><span data-stu-id="12706-320">Parallel processing of data slices</span></span>
<span data-ttu-id="12706-321">Vous pouvez définir la date de début du pipeline dans le passé.</span><span class="sxs-lookup"><span data-stu-id="12706-321">You can set the start date for the pipeline in the past.</span></span> <span data-ttu-id="12706-322">Lorsque vous procédez ainsi, Data Factory calcule (remplit postérieurement) automatiquement toutes les tranches de données dans le passé automatiquement et commence à les traiter.</span><span class="sxs-lookup"><span data-stu-id="12706-322">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span> <span data-ttu-id="12706-323">Par exemple : si vous créez un pipeline avec la date de début 2017-04-01 et que la date actuelle est 2017-04-10.</span><span class="sxs-lookup"><span data-stu-id="12706-323">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span></span> <span data-ttu-id="12706-324">Si la cadence du jeu de données de sortie est tous les jours, Data Factory commence immédiatement le traitement de toutes les tranches entre le 2017-04-01 et le 2017-04-09, car la date de début se situe dans le passé.</span><span class="sxs-lookup"><span data-stu-id="12706-324">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span></span> <span data-ttu-id="12706-325">La tranche du 2017-04-10 n’est pas encore traitée, car la valeur de la propriété style dans la section availability (disponibilité) est EndOfInterval par défaut.</span><span class="sxs-lookup"><span data-stu-id="12706-325">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span></span> <span data-ttu-id="12706-326">La tranche la plus ancienne est traitée en premier, car la valeur par défaut de executionPriorityOrder est OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="12706-326">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="12706-327">Pour obtenir une description de la propriété style, consultez la section [Disponibilité du jeu de données](#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="12706-327">For a description of the style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="12706-328">Pour obtenir une description de la section executionPriorityOrder, consultez la section [Stratégies d’activité](#activity-policies).</span><span class="sxs-lookup"><span data-stu-id="12706-328">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="12706-329">Vous pouvez configurer des tranches de données pour qu’elles soient traitées en parallèle en définissant la propriété **concurrency** (concurrence) dans la section **policy** (stratégie) de l’activité JSON.</span><span class="sxs-lookup"><span data-stu-id="12706-329">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span></span> <span data-ttu-id="12706-330">Cette propriété détermine le nombre d’exécutions en parallèle de l’activité qui peuvent se produire sur différents segments.</span><span class="sxs-lookup"><span data-stu-id="12706-330">This property determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="12706-331">La valeur par défaut de la propriété de concurrence est 1.</span><span class="sxs-lookup"><span data-stu-id="12706-331">The default value for the concurrency property is 1.</span></span> <span data-ttu-id="12706-332">Une tranche est donc traitée à la fois par défaut.</span><span class="sxs-lookup"><span data-stu-id="12706-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="12706-333">La valeur maximale est 10.</span><span class="sxs-lookup"><span data-stu-id="12706-333">The maximum value is 10.</span></span> <span data-ttu-id="12706-334">Lorsqu’un pipeline doit passer par un grand ensemble de données disponibles, une valeur de concurrence plus élevée accélère le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="12706-334">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="12706-335">Réexécuter une tranche de données ayant échoué</span><span class="sxs-lookup"><span data-stu-id="12706-335">Rerun a failed data slice</span></span>
<span data-ttu-id="12706-336">Lorsqu’une erreur se produit pendant le traitement d’une tranche de données, vous pouvez savoir pourquoi le traitement d’une tranche a échoué à l’aide de panneaux du portail Azure ou de l’application Surveiller et gérer.</span><span class="sxs-lookup"><span data-stu-id="12706-336">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="12706-337">Pour plus d’informations, consultez [Surveillance et gestion des pipelines à l’aide des panneaux du portail Azure](data-factory-monitor-manage-pipelines.md) ou de [l’application Surveillance et gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="12706-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="12706-338">Prenons l’exemple suivant, il montre les deux activités.</span><span class="sxs-lookup"><span data-stu-id="12706-338">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="12706-339">Activity1 et Activity2.</span><span class="sxs-lookup"><span data-stu-id="12706-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="12706-340">Activity1 utilise une tranche de Dataset1 et génère une tranche de Dataset2, qui est utilisé en entrée par Activity2 pour produire une tranche du jeu de données final.</span><span class="sxs-lookup"><span data-stu-id="12706-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span></span>

![Tranche de données ayant échoué](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="12706-342">Le diagramme montre que, parmi les trois tranches récentes, il y a eu un échec, ce qui a généré une tranche 9 à 10 h pour Dataset2.</span><span class="sxs-lookup"><span data-stu-id="12706-342">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="12706-343">Data Factory effectue automatiquement le suivi de la dépendance du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="12706-343">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="12706-344">Par conséquent, il ne lance pas l’activité sur la tranche 9 à 10 h en aval.</span><span class="sxs-lookup"><span data-stu-id="12706-344">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="12706-345">Les outils de surveillance et de gestion Data Factory vous permettent d’examiner en détail les journaux de diagnostic pour la tranche ayant échoué, et de trouver facilement la cause du problème pour le régler.</span><span class="sxs-lookup"><span data-stu-id="12706-345">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="12706-346">Une fois le problème résolu, vous pouvez facilement lancer l’exécution de l’activité afin de générer la tranche ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="12706-346">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="12706-347">Pour plus d’informations sur la façon de lancer les réexécutions et comprendre les transitions d’état des tranches de données, consultez [Surveillance et gestion des pipelines à l’aide des panneaux du portail Azure](data-factory-monitor-manage-pipelines.md) ou [Application de surveillance et gestion](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="12706-347">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="12706-348">Une fois que vous avez relancé l’exécution de la tranche de 9-10 h pour **Dataset2**, Data Factory lance l’exécution de la tranche dépendante 9 à 10 h sur un jeu de données final.</span><span class="sxs-lookup"><span data-stu-id="12706-348">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![Réexécuter une tranche de données ayant échoué](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="12706-350">Plusieurs activités à l’intérieur d’un pipeline</span><span class="sxs-lookup"><span data-stu-id="12706-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="12706-351">Un pipeline peut toutefois contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="12706-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="12706-352">Si vous avez plusieurs activités dans un pipeline et que la sortie d’une activité n’est pas une entrée dans une autre activité, les activités peuvent s’exécuter en parallèle si les tranches de données d’entrée pour les activités sont prêtes.</span><span class="sxs-lookup"><span data-stu-id="12706-352">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span>

<span data-ttu-id="12706-353">Vous pouvez chaîner deux activités (une après l’autre) en configurant le jeu de données de sortie d’une activité en tant que jeu de données d’entrée de l’autre activité.</span><span class="sxs-lookup"><span data-stu-id="12706-353">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="12706-354">Les activités peuvent être dans le même pipeline ou dans des pipelines différents.</span><span class="sxs-lookup"><span data-stu-id="12706-354">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="12706-355">La seconde activité s’exécute uniquement quand la première se termine correctement.</span><span class="sxs-lookup"><span data-stu-id="12706-355">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="12706-356">Par exemple, considérez le cas suivant, dans lequel un pipeline a deux activités :</span><span class="sxs-lookup"><span data-stu-id="12706-356">For example, consider the following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="12706-357">L’activité A1 nécessitant le jeu de données d’entrée externe D1 et qui produit le jeu de données de sortie D2.</span><span class="sxs-lookup"><span data-stu-id="12706-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="12706-358">L’activité A2 nécessitant le jeu de données d’entrée D2 et qui produit le jeu de données de sortie D3.</span><span class="sxs-lookup"><span data-stu-id="12706-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="12706-359">Dans ce scénario, les activités A1 et A2 sont dans le même pipeline.</span><span class="sxs-lookup"><span data-stu-id="12706-359">In this scenario, activities A1 and A2 are in the same pipeline.</span></span> <span data-ttu-id="12706-360">L’activité A1 s’exécute lorsque les données externes seront disponibles et que la fréquence de disponibilité planifiée sera atteinte.</span><span class="sxs-lookup"><span data-stu-id="12706-360">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="12706-361">L’activité A2 s’exécute lorsque les tranches planifiées de D2 seront disponibles et que la fréquence de disponibilité planifiée sera atteinte.</span><span class="sxs-lookup"><span data-stu-id="12706-361">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="12706-362">S’il existe une erreur dans l’une des tranches du jeu de données D2, A2 n’est pas exécutée pour cette tranche jusqu’à ce que celle-ci devienne disponible.</span><span class="sxs-lookup"><span data-stu-id="12706-362">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="12706-363">La vue de diagramme avec les deux activités dans le même pipeline se présente comme dans le diagramme suivant :</span><span class="sxs-lookup"><span data-stu-id="12706-363">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![Chaînage des activités dans le même pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="12706-365">Comme mentionné plus tôt, les activités peuvent être dans des pipelines différents.</span><span class="sxs-lookup"><span data-stu-id="12706-365">As mentioned earlier, the activities could be in different pipelines.</span></span> <span data-ttu-id="12706-366">Dans ce scénario, la vue de diagramme se présente comme dans le diagramme suivant :</span><span class="sxs-lookup"><span data-stu-id="12706-366">In such a scenario, the diagram view would look like the following diagram:</span></span>

![Chaînage des activités dans deux pipelines](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="12706-368">Consultez la section [Copier de manière séquentielle](#copy-sequentially) de l’annexe pour obtenir un exemple.</span><span class="sxs-lookup"><span data-stu-id="12706-368">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="12706-369">Modélisation des jeux de données avec des fréquences différentes</span><span class="sxs-lookup"><span data-stu-id="12706-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="12706-370">Dans les exemples, les fréquences de planification des jeux de données d’entrée et de sortie et l’intervalle d’activité sont les mêmes.</span><span class="sxs-lookup"><span data-stu-id="12706-370">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="12706-371">Certains scénarios exigent que la fréquence de génération d’une sortie à soit différente de celles d’une ou de plusieurs entrées.</span><span class="sxs-lookup"><span data-stu-id="12706-371">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="12706-372">Data factory prend en charge la modélisation de ces scénarios.</span><span class="sxs-lookup"><span data-stu-id="12706-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="12706-373">Exemple 1 : production d’un rapport de sortie quotidien pour les données d’entrée est disponible toutes les heures</span><span class="sxs-lookup"><span data-stu-id="12706-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="12706-374">Imaginez un scénario dans lequel nous avons entré des données de mesure à partir de capteurs disponibles toutes les heures dans un stockage Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="12706-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="12706-375">Vous voulez générer un rapport d’agrégation quotidien avec des statistiques, comme les valeurs moyenne, maximum et minimum pour la journée avec une [Activité Hive Data Factory](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="12706-375">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="12706-376">Voici ce que vous pouvez modéliser ce scénario avec data factory :</span><span class="sxs-lookup"><span data-stu-id="12706-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="12706-377">**Jeu de données d'entrée**</span><span class="sxs-lookup"><span data-stu-id="12706-377">**Input dataset**</span></span>

<span data-ttu-id="12706-378">Les fichiers d’entrée des heures sont supprimés dans le dossier pour le jour donné.</span><span class="sxs-lookup"><span data-stu-id="12706-378">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="12706-379">La disponibilité de l’entrée est définie sur **Toutes les heures** (fréquence : Heure, intervalle: 1).</span><span class="sxs-lookup"><span data-stu-id="12706-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="12706-380">**Jeu de données de sortie**</span><span class="sxs-lookup"><span data-stu-id="12706-380">**Output dataset**</span></span>

<span data-ttu-id="12706-381">Un fichier de sortie est créé chaque jour dans le dossier pour la journée.</span><span class="sxs-lookup"><span data-stu-id="12706-381">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="12706-382">Disponibilité de sortie a pour valeur **Quotidien** (fréquence : jour et intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="12706-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="12706-383">**Activité : activité Hive dans un pipeline**</span><span class="sxs-lookup"><span data-stu-id="12706-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="12706-384">Le script Hive reçoit les informations de *DateTime* en tant que paramètres qui utilisent la variable **WindowStart** comme indiqué dans l’extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="12706-384">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="12706-385">Le script Hive utilise cette variable pour charger les données à partir du dossier correspondant à la journée et exécuter l’agrégation pour générer la sortie.</span><span class="sxs-lookup"><span data-stu-id="12706-385">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

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

<span data-ttu-id="12706-386">Le diagramme suivant illustre le scénario du point de vue de la dépendance des données.</span><span class="sxs-lookup"><span data-stu-id="12706-386">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![Dépendance des données](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="12706-388">La tranche de sortie dépend des 24 tranches horaires depuis l’ensemble de données en entrée.</span><span class="sxs-lookup"><span data-stu-id="12706-388">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="12706-389">Data Factory calcule automatiquement ces dépendances en déterminant les tranches de données d’entrée qui tombent dans la même période que la tranche de données à générer.</span><span class="sxs-lookup"><span data-stu-id="12706-389">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="12706-390">Si une des 24 tranches d’entrée n’est pas disponible, Data Factory attend que la tranche d’entrée soit prête avant de lancer l’exécution d’activité quotidienne.</span><span class="sxs-lookup"><span data-stu-id="12706-390">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="12706-391">Exemple 2 : spécifier les dépendances avec des expressions et des fonctions Data Factory</span><span class="sxs-lookup"><span data-stu-id="12706-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="12706-392">Prenons en compte un autre scénario.</span><span class="sxs-lookup"><span data-stu-id="12706-392">Let’s consider another scenario.</span></span> <span data-ttu-id="12706-393">Supposez que vous avez une activité Hive qui traite deux jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="12706-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="12706-394">Un d’eux a de nouvelles données tous les jours, mais l’autre obtient de nouvelles données toutes les semaines.</span><span class="sxs-lookup"><span data-stu-id="12706-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="12706-395">Supposons que vous vouliez faire la jonction entre les deux entrées et générer une sortie quotidiennement.</span><span class="sxs-lookup"><span data-stu-id="12706-395">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="12706-396">L’approche simple consistant pour Data Factory à déterminer des tranches d’entrée appropriées à traiter en alignant la période de temps de la tranche de données en sortie ne fonctionne plus.</span><span class="sxs-lookup"><span data-stu-id="12706-396">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="12706-397">Vous devez spécifier (pour chaque exécution d’activité que Data Factory doit utiliser) les tranches de données de la semaine précédente pour les jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="12706-397">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="12706-398">Vous utilisez les fonctions Azure Data Factory comme indiqué dans l’extrait de code suivant pour implémenter ce comportement.</span><span class="sxs-lookup"><span data-stu-id="12706-398">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="12706-399">**Entrée1 : Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="12706-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="12706-400">La première entrée est l’objet Azure Blob mis à jour quotidiennement.</span><span class="sxs-lookup"><span data-stu-id="12706-400">The first input is the Azure blob being updated daily.</span></span>

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

<span data-ttu-id="12706-401">**Entrée2 : objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="12706-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="12706-402">Entrée2 est l’objet Azure Blob mis à jour chaque semaine.</span><span class="sxs-lookup"><span data-stu-id="12706-402">Input2 is the Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="12706-403">**Sortie : objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="12706-403">**Output: Azure blob**</span></span>

<span data-ttu-id="12706-404">Un fichier de sortie est créé chaque jour dans le dossier pour la journée.</span><span class="sxs-lookup"><span data-stu-id="12706-404">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="12706-405">La disponibilité de sortie est définie sur **Quotidiennement** (fréquence : jour et intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="12706-405">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="12706-406">**Activité : activité Hive dans un pipeline**</span><span class="sxs-lookup"><span data-stu-id="12706-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="12706-407">L’activité Hive accepte les deux entrées et génère une tranche de sortie tous les jours.</span><span class="sxs-lookup"><span data-stu-id="12706-407">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="12706-408">Vous pouvez spécifier la tranche de sortie de tous les jours dépendant de la tranche de semaine précédente pour la sortie hebdomadaire comme suit.</span><span class="sxs-lookup"><span data-stu-id="12706-408">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="12706-409">Pour obtenir la liste des fonctions et variables système prises en charge par Azure Data Factory, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="12706-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="12706-410">Annexe</span><span class="sxs-lookup"><span data-stu-id="12706-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="12706-411">Exemple : Copier de manière séquentielle</span><span class="sxs-lookup"><span data-stu-id="12706-411">Example: copy sequentially</span></span>
<span data-ttu-id="12706-412">Il est possible d’exécuter plusieurs opérations de copie l’une après l’autre, de manière séquentielle/ordonnée.</span><span class="sxs-lookup"><span data-stu-id="12706-412">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="12706-413">Si, par exemple, vous avez deux activités de copie dans un pipeline : (ActivitédeCopie1 et ActivitédeCopie2) avec les jeux de données de sortie de données d’entrée suivants :</span><span class="sxs-lookup"><span data-stu-id="12706-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="12706-414">Activitédecopie1</span><span class="sxs-lookup"><span data-stu-id="12706-414">CopyActivity1</span></span>

<span data-ttu-id="12706-415">Jeu de données d'entrée.</span><span class="sxs-lookup"><span data-stu-id="12706-415">Input: Dataset.</span></span> <span data-ttu-id="12706-416">Sortie : Dataset2.</span><span class="sxs-lookup"><span data-stu-id="12706-416">Output: Dataset2.</span></span>

<span data-ttu-id="12706-417">Activitédecopie2</span><span class="sxs-lookup"><span data-stu-id="12706-417">CopyActivity2</span></span>

<span data-ttu-id="12706-418">Entrée : Jeudedonnées2.</span><span class="sxs-lookup"><span data-stu-id="12706-418">Input: Dataset2.</span></span>  <span data-ttu-id="12706-419">Sortie : Jeudedonnées3.</span><span class="sxs-lookup"><span data-stu-id="12706-419">Output: Dataset3.</span></span>

<span data-ttu-id="12706-420">ActivitédeCopie2 s’exécute uniquement si ActivitédeCopie1 s’est exécutée avec succès et que JeudeDonnées2 est disponible.</span><span class="sxs-lookup"><span data-stu-id="12706-420">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="12706-421">Voici l’exemple de pipeline JSON :</span><span class="sxs-lookup"><span data-stu-id="12706-421">Here is the sample pipeline JSON:</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="12706-422">Notez que dans l’exemple, le jeu de données de sortie de la première activité de copie (Dataset2) est spécifié en tant qu’entrée pour la deuxième activité.</span><span class="sxs-lookup"><span data-stu-id="12706-422">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="12706-423">Par conséquent, la deuxième activité s’exécute uniquement lorsque le jeu de données de sortie de la première activité est prêt.</span><span class="sxs-lookup"><span data-stu-id="12706-423">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="12706-424">Dans l’exemple, ActivitédeCopie2 peut avoir une entrée différente, par exemple JeudeDonnées3, mais vous spécifiez JeudeDonnées2 en tant qu’entrée pour ActivitédeCopie2, afin que l’activité ne s’exécute pas avant la fin d’ActivitédeCopie1.</span><span class="sxs-lookup"><span data-stu-id="12706-424">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="12706-425">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="12706-425">For example:</span></span>

<span data-ttu-id="12706-426">Activitédecopie1</span><span class="sxs-lookup"><span data-stu-id="12706-426">CopyActivity1</span></span>

<span data-ttu-id="12706-427">Entrée : Jeudedonnées1.</span><span class="sxs-lookup"><span data-stu-id="12706-427">Input: Dataset1.</span></span> <span data-ttu-id="12706-428">Sortie : Dataset2.</span><span class="sxs-lookup"><span data-stu-id="12706-428">Output: Dataset2.</span></span>

<span data-ttu-id="12706-429">Activitédecopie2</span><span class="sxs-lookup"><span data-stu-id="12706-429">CopyActivity2</span></span>

<span data-ttu-id="12706-430">Entrées : Jeudedonnées3, Jeudedonnées2.</span><span class="sxs-lookup"><span data-stu-id="12706-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="12706-431">Sortie : Jeudedonnées4.</span><span class="sxs-lookup"><span data-stu-id="12706-431">Output: Dataset4.</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="12706-432">Notez que dans l’exemple, deux jeux de données d’entrée sont spécifiés pour la deuxième activité de copie.</span><span class="sxs-lookup"><span data-stu-id="12706-432">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="12706-433">Quand plusieurs entrées sont spécifiées, seul le premier jeu de données d’entrée est utilisé pour copier des données, mais les autres jeux de données sont utilisés en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="12706-433">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="12706-434">L’exécution d’ActivitédeCopie2 démarre uniquement quand les conditions suivantes sont remplies :</span><span class="sxs-lookup"><span data-stu-id="12706-434">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="12706-435">ActivitédeCopie1 s’est terminée avec succès et JeudeDonnées2 est disponible.</span><span class="sxs-lookup"><span data-stu-id="12706-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="12706-436">Ce jeu de données n’est pas utilisé lors de la copie des données vers JeudeDonnées4.</span><span class="sxs-lookup"><span data-stu-id="12706-436">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="12706-437">Il sert uniquement de dépendance de planification pour ActivitédeCopie2.</span><span class="sxs-lookup"><span data-stu-id="12706-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="12706-438">JeudeDonnées3 est disponible.</span><span class="sxs-lookup"><span data-stu-id="12706-438">Dataset3 is available.</span></span> <span data-ttu-id="12706-439">Ce jeu de données représente les données qui sont copiées vers la destination.</span><span class="sxs-lookup"><span data-stu-id="12706-439">This dataset represents the data that is copied to the destination.</span></span> 