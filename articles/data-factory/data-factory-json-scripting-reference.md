---
title: "Azure Data Factory - Référence de script JSON | Microsoft Docs"
description: "Fournit des schémas JSON pour les entités Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 805106c0a5cdbff1f143f22a2ae59f6d2a0bf126
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="40a79-103">Azure Data Factory - Référence de script JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="40a79-104">Cet article fournit des schémas JSON et des exemples pour la définition des entités Azure Data Factory (pipeline, activité, jeu de données et service lié).</span><span class="sxs-lookup"><span data-stu-id="40a79-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="40a79-105">Pipeline</span><span class="sxs-lookup"><span data-stu-id="40a79-105">Pipeline</span></span> 
<span data-ttu-id="40a79-106">La structure de haut niveau d’une définition de pipeline est la suivante :</span><span class="sxs-lookup"><span data-stu-id="40a79-106">The high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="40a79-107">Le tableau suivant décrit les propriétés dans la définition JSON du pipeline :</span><span class="sxs-lookup"><span data-stu-id="40a79-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="40a79-108">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-108">Property</span></span> | <span data-ttu-id="40a79-109">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-109">Description</span></span> | <span data-ttu-id="40a79-110">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="40a79-111">name</span><span class="sxs-lookup"><span data-stu-id="40a79-111">name</span></span> | <span data-ttu-id="40a79-112">Nom du pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-112">Name of the pipeline.</span></span> <span data-ttu-id="40a79-113">Spécifiez un nom qui représente l’action que l’activité ou le pipeline est configuré(e) à exécuter</span><span class="sxs-lookup"><span data-stu-id="40a79-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="40a79-114">Nombre maximal de caractères : 260</span><span class="sxs-lookup"><span data-stu-id="40a79-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="40a79-115">Doit commencer par une lettre, un chiffre ou un trait de soulignement (_)</span><span class="sxs-lookup"><span data-stu-id="40a79-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="40a79-116">Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</span><span class="sxs-lookup"><span data-stu-id="40a79-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="40a79-117">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-117">Yes</span></span> |
| <span data-ttu-id="40a79-118">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-118">description</span></span> |<span data-ttu-id="40a79-119">Texte décrivant la raison motivant l’activité ou le pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="40a79-120">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-120">No</span></span> |
| <span data-ttu-id="40a79-121">activités</span><span class="sxs-lookup"><span data-stu-id="40a79-121">activities</span></span> | <span data-ttu-id="40a79-122">Contient une liste d’activités.</span><span class="sxs-lookup"><span data-stu-id="40a79-122">Contains a list of activities.</span></span> | <span data-ttu-id="40a79-123">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-123">Yes</span></span> |
| <span data-ttu-id="40a79-124">start</span><span class="sxs-lookup"><span data-stu-id="40a79-124">start</span></span> |<span data-ttu-id="40a79-125">Date et heure de début du pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="40a79-126">Doit se trouver au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="40a79-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="40a79-127">Par exemple : 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="40a79-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="40a79-128">Il est possible de spécifier une heure locale, par exemple une heure EST.</span><span class="sxs-lookup"><span data-stu-id="40a79-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="40a79-129">Voici un exemple : `2016-02-27T06:00:00**-05:00`, qui correspond à 6h EST.</span><span class="sxs-lookup"><span data-stu-id="40a79-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="40a79-130">Ensemble, les propriétés de début et de fin spécifient la période active du pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="40a79-131">Les tranches de sortie sont uniquement générées pendant cette période active.</span><span class="sxs-lookup"><span data-stu-id="40a79-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="40a79-132">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-132">No</span></span><br/><br/><span data-ttu-id="40a79-133">Si vous spécifiez une valeur pour la propriété end, vous devez en spécifier une pour la propriété start.</span><span class="sxs-lookup"><span data-stu-id="40a79-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="40a79-134">Les heures de début et de fin peuvent être toutes les deux non renseignées pour créer un pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="40a79-135">Vous devez spécifier les deux valeurs pour définir une période active d’exécution du pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="40a79-136">Si vous ne spécifiez pas d’heures de début et de fin lors de la création d’un pipeline, vous pouvez les définir à l’aide de l’applet de commande Set-AzureRmDataFactoryPipelineActivePeriod ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="40a79-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="40a79-137">end</span><span class="sxs-lookup"><span data-stu-id="40a79-137">end</span></span> |<span data-ttu-id="40a79-138">Date et heure de fin du pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-138">End date-time for the pipeline.</span></span> <span data-ttu-id="40a79-139">Si spécifiée, doit être au format ISO.</span><span class="sxs-lookup"><span data-stu-id="40a79-139">If specified must be in ISO format.</span></span> <span data-ttu-id="40a79-140">Par exemple : 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="40a79-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="40a79-141">Il est possible de spécifier une heure locale, par exemple une heure EST.</span><span class="sxs-lookup"><span data-stu-id="40a79-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="40a79-142">Voici un exemple : `2016-02-27T06:00:00**-05:00`, qui correspond à 6h EST.</span><span class="sxs-lookup"><span data-stu-id="40a79-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="40a79-143">Pour exécuter le pipeline indéfiniment, spécifiez 9999-09-09 comme valeur pour la propriété end.</span><span class="sxs-lookup"><span data-stu-id="40a79-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="40a79-144">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-144">No</span></span> <br/><br/><span data-ttu-id="40a79-145">Si vous spécifiez une valeur pour la propriété start, vous devez en spécifier une pour la propriété end.</span><span class="sxs-lookup"><span data-stu-id="40a79-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="40a79-146">Consultez les remarques relatives à la propriété **start** .</span><span class="sxs-lookup"><span data-stu-id="40a79-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="40a79-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="40a79-147">isPaused</span></span> |<span data-ttu-id="40a79-148">Si la valeur est true, le pipeline ne s’exécute pas.</span><span class="sxs-lookup"><span data-stu-id="40a79-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="40a79-149">Valeur par défaut = false.</span><span class="sxs-lookup"><span data-stu-id="40a79-149">Default value = false.</span></span> <span data-ttu-id="40a79-150">Vous pouvez utiliser cette propriété pour activer ou désactiver.</span><span class="sxs-lookup"><span data-stu-id="40a79-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="40a79-151">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-151">No</span></span> |
| <span data-ttu-id="40a79-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="40a79-152">pipelineMode</span></span> |<span data-ttu-id="40a79-153">La méthode de planification des exécutions pour le pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="40a79-154">Les valeurs autorisées sont : scheduled (par défaut) et onetime.</span><span class="sxs-lookup"><span data-stu-id="40a79-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="40a79-155">« scheduled » indique que le pipeline s’exécute selon un intervalle de temps spécifié en fonction de sa période active (heure de début et de fin).</span><span class="sxs-lookup"><span data-stu-id="40a79-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="40a79-156">« Onetime » indique que le pipeline ne s’exécute qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="40a79-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="40a79-157">Une fois créés, les pipelines de type onetime ne peuvent pas être modifiés ni mis à jour pour le moment.</span><span class="sxs-lookup"><span data-stu-id="40a79-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="40a79-158">Consultez la page [Pipeline onetime](data-factory-create-pipelines.md#onetime-pipeline) pour plus d’informations sur le paramètre onetime.</span><span class="sxs-lookup"><span data-stu-id="40a79-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="40a79-159">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-159">No</span></span> |
| <span data-ttu-id="40a79-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="40a79-160">expirationTime</span></span> |<span data-ttu-id="40a79-161">Durée pendant laquelle le pipeline est valide et doit rester configuré.</span><span class="sxs-lookup"><span data-stu-id="40a79-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="40a79-162">Le pipeline est automatiquement supprimé une fois le délai d’expiration atteint s’il ne contient aucune exécution active, en échec ou en attente.</span><span class="sxs-lookup"><span data-stu-id="40a79-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="40a79-163">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="40a79-164">Activité</span><span class="sxs-lookup"><span data-stu-id="40a79-164">Activity</span></span> 
<span data-ttu-id="40a79-165">La structure de haut niveau pour une activité dans une définition de pipeline (élément d’activités) est la suivante :</span><span class="sxs-lookup"><span data-stu-id="40a79-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="40a79-166">Le tableau suivant décrit les propriétés dans la définition JSON du pipeline :</span><span class="sxs-lookup"><span data-stu-id="40a79-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="40a79-167">Tag</span><span class="sxs-lookup"><span data-stu-id="40a79-167">Tag</span></span> | <span data-ttu-id="40a79-168">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-168">Description</span></span> | <span data-ttu-id="40a79-169">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-170">name</span><span class="sxs-lookup"><span data-stu-id="40a79-170">name</span></span> |<span data-ttu-id="40a79-171">Nom de l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-171">Name of the activity.</span></span> <span data-ttu-id="40a79-172">Spécifiez un nom qui représente l’action pour laquelle l’activité est configurée</span><span class="sxs-lookup"><span data-stu-id="40a79-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="40a79-173">Nombre maximal de caractères : 260</span><span class="sxs-lookup"><span data-stu-id="40a79-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="40a79-174">Doit commencer par une lettre, un chiffre ou un trait de soulignement (_)</span><span class="sxs-lookup"><span data-stu-id="40a79-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="40a79-175">Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</span><span class="sxs-lookup"><span data-stu-id="40a79-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="40a79-176">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-176">Yes</span></span> |
| <span data-ttu-id="40a79-177">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-177">description</span></span> |<span data-ttu-id="40a79-178">Texte décrivant la raison motivant l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="40a79-179">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-179">Yes</span></span> |
| <span data-ttu-id="40a79-180">type</span><span class="sxs-lookup"><span data-stu-id="40a79-180">type</span></span> |<span data-ttu-id="40a79-181">Spécifie le type de l'activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-181">Specifies the type of the activity.</span></span> <span data-ttu-id="40a79-182">Consultez les sections [MAGASINS DE DONNÉS](#data-stores) et [ACTIVITÉS DE TRANSFORMATION DES DONNÉES](#data-transformation-activities) pour en savoir plus sur les différents types d’activités.</span><span class="sxs-lookup"><span data-stu-id="40a79-182">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="40a79-183">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-183">Yes</span></span> |
| <span data-ttu-id="40a79-184">inputs</span><span class="sxs-lookup"><span data-stu-id="40a79-184">inputs</span></span> |<span data-ttu-id="40a79-185">Les tables d’entrée utilisées par l’activité</span><span class="sxs-lookup"><span data-stu-id="40a79-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="40a79-186">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-186">Yes</span></span> |
| <span data-ttu-id="40a79-187">outputs</span><span class="sxs-lookup"><span data-stu-id="40a79-187">outputs</span></span> |<span data-ttu-id="40a79-188">Les tables de sortie utilisées par l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="40a79-189">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-189">Yes</span></span> |
| <span data-ttu-id="40a79-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="40a79-190">linkedServiceName</span></span> |<span data-ttu-id="40a79-191">Nom du service lié utilisé par l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="40a79-192">Une activité peut nécessiter que vous spécifiiez le service lié à l’environnement de calcul requis.</span><span class="sxs-lookup"><span data-stu-id="40a79-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="40a79-193">Oui pour les activités HDInsight, les activités de Azure Machine Learning et les activités de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="40a79-194">Non pour toutes les autres</span><span class="sxs-lookup"><span data-stu-id="40a79-194">No for all others</span></span> |
| <span data-ttu-id="40a79-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="40a79-195">typeProperties</span></span> |<span data-ttu-id="40a79-196">Les propriétés de la section typeProperties dépendent du type de l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="40a79-197">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-197">No</span></span> |
| <span data-ttu-id="40a79-198">policy</span><span class="sxs-lookup"><span data-stu-id="40a79-198">policy</span></span> |<span data-ttu-id="40a79-199">Stratégies affectant le comportement d’exécution de l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="40a79-200">Si aucune valeur n’est spécifiée, les stratégies par défaut sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="40a79-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="40a79-201">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-201">No</span></span> |
| <span data-ttu-id="40a79-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="40a79-202">scheduler</span></span> |<span data-ttu-id="40a79-203">La propriété « scheduler » est utilisée pour définir la planification souhaitée pour l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="40a79-204">Ses sous-propriétés sont les mêmes que celles de la [propriété de disponibilité dans un jeu de données](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="40a79-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="40a79-205">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="40a79-206">Stratégies</span><span class="sxs-lookup"><span data-stu-id="40a79-206">Policies</span></span>
<span data-ttu-id="40a79-207">Les stratégies affectent le comportement d'exécution d'une activité, en particulier lors du traitement du segment d'une table.</span><span class="sxs-lookup"><span data-stu-id="40a79-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="40a79-208">Le tableau suivant fournit les détails.</span><span class="sxs-lookup"><span data-stu-id="40a79-208">The following table provides the details.</span></span>

| <span data-ttu-id="40a79-209">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-209">Property</span></span> | <span data-ttu-id="40a79-210">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-210">Permitted values</span></span> | <span data-ttu-id="40a79-211">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="40a79-211">Default Value</span></span> | <span data-ttu-id="40a79-212">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-213">accès concurrentiel</span><span class="sxs-lookup"><span data-stu-id="40a79-213">concurrency</span></span> |<span data-ttu-id="40a79-214">Entier </span><span class="sxs-lookup"><span data-stu-id="40a79-214">Integer</span></span> <br/><br/><span data-ttu-id="40a79-215">Valeur max : 10</span><span class="sxs-lookup"><span data-stu-id="40a79-215">Max value: 10</span></span> |<span data-ttu-id="40a79-216">1</span><span class="sxs-lookup"><span data-stu-id="40a79-216">1</span></span> |<span data-ttu-id="40a79-217">Nombre d’exécutions simultanées de l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="40a79-218">Il détermine le nombre d’exécutions en parallèle de l’activité qui peuvent se produire sur différents segments.</span><span class="sxs-lookup"><span data-stu-id="40a79-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="40a79-219">Par exemple, si une activité doit passer par un grand ensemble de données disponibles, une valeur de concurrence plus élevée accélère le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="40a79-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="40a79-220">executionPriorityOrder</span></span> |<span data-ttu-id="40a79-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="40a79-221">NewestFirst</span></span><br/><br/><span data-ttu-id="40a79-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="40a79-222">OldestFirst</span></span> |<span data-ttu-id="40a79-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="40a79-223">OldestFirst</span></span> |<span data-ttu-id="40a79-224">Détermine l’ordre des segments de données qui sont traités.</span><span class="sxs-lookup"><span data-stu-id="40a79-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="40a79-225">Par exemple, si vous avez 2 segments (l’un se produisant à 16 heures et l’autre à 17 heures) et que les deux sont en attente d’exécution.</span><span class="sxs-lookup"><span data-stu-id="40a79-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="40a79-226">Si vous définissez executionPriorityOrder sur NewestFirst, le segment à 17 h est traité en premier.</span><span class="sxs-lookup"><span data-stu-id="40a79-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="40a79-227">De même, si vous définissez executionPriorityOrder sur OldestFIrst, le segment à 16 h est traité en premier.</span><span class="sxs-lookup"><span data-stu-id="40a79-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="40a79-228">retry</span><span class="sxs-lookup"><span data-stu-id="40a79-228">retry</span></span> |<span data-ttu-id="40a79-229">Entier </span><span class="sxs-lookup"><span data-stu-id="40a79-229">Integer</span></span><br/><br/><span data-ttu-id="40a79-230">La valeur max peut être 10</span><span class="sxs-lookup"><span data-stu-id="40a79-230">Max value can be 10</span></span> |<span data-ttu-id="40a79-231">0</span><span class="sxs-lookup"><span data-stu-id="40a79-231">0</span></span> |<span data-ttu-id="40a79-232">Nombre de nouvelles tentatives avant que le traitement des données du segment ne soit marqué comme un échec.</span><span class="sxs-lookup"><span data-stu-id="40a79-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="40a79-233">L'exécution de l'activité pour un segment de données est répétée jusqu'au nombre de tentatives spécifié.</span><span class="sxs-lookup"><span data-stu-id="40a79-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="40a79-234">La nouvelle tentative est effectuée dès que possible après l'échec.</span><span class="sxs-lookup"><span data-stu-id="40a79-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="40a79-235">timeout</span><span class="sxs-lookup"><span data-stu-id="40a79-235">timeout</span></span> |<span data-ttu-id="40a79-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="40a79-236">TimeSpan</span></span> |<span data-ttu-id="40a79-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="40a79-237">00:00:00</span></span> |<span data-ttu-id="40a79-238">Délai d'expiration de l'activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-238">Timeout for the activity.</span></span> <span data-ttu-id="40a79-239">Exemple : 00:10:00 (implique un délai d’expiration de 10 minutes)</span><span class="sxs-lookup"><span data-stu-id="40a79-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="40a79-240">Si une valeur n’est pas spécifiée ou est égale à 0, le délai d’expiration est infini.</span><span class="sxs-lookup"><span data-stu-id="40a79-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="40a79-241">Si le temps de traitement des données sur un segment dépasse la valeur du délai d’expiration, il est annulé et le système tente de réexécuter le traitement.</span><span class="sxs-lookup"><span data-stu-id="40a79-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="40a79-242">Le nombre de nouvelles tentatives dépend de la propriété « retry ».</span><span class="sxs-lookup"><span data-stu-id="40a79-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="40a79-243">Quand le délai d’expiration est atteint, l’état est défini sur TimedOut.</span><span class="sxs-lookup"><span data-stu-id="40a79-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="40a79-244">delay</span><span class="sxs-lookup"><span data-stu-id="40a79-244">delay</span></span> |<span data-ttu-id="40a79-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="40a79-245">TimeSpan</span></span> |<span data-ttu-id="40a79-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="40a79-246">00:00:00</span></span> |<span data-ttu-id="40a79-247">Spécifie le délai avant le début du traitement des données du segment.</span><span class="sxs-lookup"><span data-stu-id="40a79-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="40a79-248">L’exécution d’activité pour une tranche de données est démarrée une fois que le délai a dépassé l’heure d’exécution prévue.</span><span class="sxs-lookup"><span data-stu-id="40a79-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="40a79-249">Exemple : 00:10:00 (implique un délai de 10 minutes)</span><span class="sxs-lookup"><span data-stu-id="40a79-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="40a79-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="40a79-250">longRetry</span></span> |<span data-ttu-id="40a79-251">Entier </span><span class="sxs-lookup"><span data-stu-id="40a79-251">Integer</span></span><br/><br/><span data-ttu-id="40a79-252">Valeur max : 10</span><span class="sxs-lookup"><span data-stu-id="40a79-252">Max value: 10</span></span> |<span data-ttu-id="40a79-253">1</span><span class="sxs-lookup"><span data-stu-id="40a79-253">1</span></span> |<span data-ttu-id="40a79-254">Le nombre de nouvelles tentatives longues avant l’échec de l’exécution du segment.</span><span class="sxs-lookup"><span data-stu-id="40a79-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="40a79-255">Les tentatives longRetry sont espacées par longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="40a79-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="40a79-256">Par conséquent, si vous devez spécifier un délai entre chaque tentative, utilisez longRetry.</span><span class="sxs-lookup"><span data-stu-id="40a79-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="40a79-257">Si les valeurs Retry et longRetry sont spécifiées, chaque tentative longRetry inclut des tentatives Retry et le nombre maximal de tentatives sera égal à Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="40a79-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="40a79-258">Par exemple, si nous avons les paramètres suivants dans la stratégie de l’activité :</span><span class="sxs-lookup"><span data-stu-id="40a79-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="40a79-259">Retry : 3</span><span class="sxs-lookup"><span data-stu-id="40a79-259">Retry: 3</span></span><br/><span data-ttu-id="40a79-260">longRetry : 2</span><span class="sxs-lookup"><span data-stu-id="40a79-260">longRetry: 2</span></span><br/><span data-ttu-id="40a79-261">longRetryInterval : 01:00:00</span><span class="sxs-lookup"><span data-stu-id="40a79-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="40a79-262">Supposons qu’il existe un seul segment à exécuter (dont l’état est Waiting) et que l’exécution de l’activité échoue à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="40a79-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="40a79-263">Au départ, il y aurait 3 tentatives consécutives d'exécution.</span><span class="sxs-lookup"><span data-stu-id="40a79-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="40a79-264">Après chaque tentative, l’état du segment serait Retry.</span><span class="sxs-lookup"><span data-stu-id="40a79-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="40a79-265">Une fois les 3 premières tentatives terminées, l’état du segment serait LongRetry.</span><span class="sxs-lookup"><span data-stu-id="40a79-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="40a79-266">Après une heure (c’est-à-dire la valeur de longRetryInterval), il y aurait un autre ensemble de 3 tentatives consécutives d’exécution.</span><span class="sxs-lookup"><span data-stu-id="40a79-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="40a79-267">Ensuite, l'état du segment serait Failed et aucune autre tentative ne serait exécutée.</span><span class="sxs-lookup"><span data-stu-id="40a79-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="40a79-268">Par conséquent, 6 tentatives ont été exécutées.</span><span class="sxs-lookup"><span data-stu-id="40a79-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="40a79-269">Si une exécution réussit, l’état de la tranche est Ready et aucune nouvelle tentative n’est tentée.</span><span class="sxs-lookup"><span data-stu-id="40a79-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="40a79-270">La valeur longRetry peut être utilisée dans les situations où les données dépendantes arrivent à des moments non déterministes ou lorsque l’environnement global où le traitement des données se produit est douteux.</span><span class="sxs-lookup"><span data-stu-id="40a79-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="40a79-271">Dans ces cas, l’exécution de nouvelles tentatives l’une après l’autre peut ne pas être utile et procéder ainsi après un intervalle de temps précis produit la sortie désirée.</span><span class="sxs-lookup"><span data-stu-id="40a79-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="40a79-272">Mise en garde : ne définissez pas de valeurs élevées pour longRetry ou longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="40a79-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="40a79-273">En règle générale, des valeurs plus élevées impliquent d’autres problèmes systémiques.</span><span class="sxs-lookup"><span data-stu-id="40a79-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="40a79-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="40a79-274">longRetryInterval</span></span> |<span data-ttu-id="40a79-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="40a79-275">TimeSpan</span></span> |<span data-ttu-id="40a79-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="40a79-276">00:00:00</span></span> |<span data-ttu-id="40a79-277">Le délai entre les nouvelles tentatives longues</span><span class="sxs-lookup"><span data-stu-id="40a79-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="40a79-278">Section typeProperties</span><span class="sxs-lookup"><span data-stu-id="40a79-278">typeProperties section</span></span>
<span data-ttu-id="40a79-279">La section typeProperties est différente pour chaque activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="40a79-280">Les activités de transformation n’ont que les propriétés du type.</span><span class="sxs-lookup"><span data-stu-id="40a79-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="40a79-281">Consultez la section [Activités de transformation des données](#data-transformation-activities) dans cet article pour obtenir des exemples JSON qui définissent les activités de transformation dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="40a79-282">L’**Activité de copie** a deux sous-sections dans la section typeProperties : **source** et **sink**.</span><span class="sxs-lookup"><span data-stu-id="40a79-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="40a79-283">Consultez la section [Magasins de données](#data-stores) de cet article pour obtenir des exemples JSON montrant comment utiliser un magasin de données comme source et/ou récepteur.</span><span class="sxs-lookup"><span data-stu-id="40a79-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="40a79-284">Exemple de pipeline de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-284">Sample copy pipeline</span></span>
<span data-ttu-id="40a79-285">Dans l’exemple de pipeline suivant, il existe une activité de type **Copy** in the **d’activités** .</span><span class="sxs-lookup"><span data-stu-id="40a79-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="40a79-286">Dans cet exemple, [l’activité de copie](data-factory-data-movement-activities.md) copie des données d’un stockage blob Azure vers une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="40a79-287">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="40a79-287">Note the following points:</span></span>

* <span data-ttu-id="40a79-288">Dans la section des activités, il existe une seule activité dont le **type** a la valeur **Copy**.</span><span class="sxs-lookup"><span data-stu-id="40a79-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="40a79-289">L’entrée de l’activité est définie sur **InputDataset** et sa sortie, sur **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="40a79-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="40a79-290">Dans la section **typeProperties**, **BlobSource** est spécifié en tant que type de source et **SqlSink**, en tant que type de récepteur.</span><span class="sxs-lookup"><span data-stu-id="40a79-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="40a79-291">Consultez la section [Magasins de données](#data-stores) de cet article pour obtenir des exemples JSON montrant comment utiliser un magasin de données comme source et/ou récepteur.</span><span class="sxs-lookup"><span data-stu-id="40a79-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="40a79-292">Pour une procédure pas à pas complète de création de ce pipeline, consultez [Didacticiel : Copie de données de stockage blob vers une SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="40a79-293">Exemple de pipeline de transformation</span><span class="sxs-lookup"><span data-stu-id="40a79-293">Sample transformation pipeline</span></span>
<span data-ttu-id="40a79-294">Dans l’exemple de pipeline suivant, il existe une activité de type **HDInsightHive** in the **d’activités** .</span><span class="sxs-lookup"><span data-stu-id="40a79-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="40a79-295">Dans cet exemple, [l’activité Hive HDInsight](data-factory-hive-activity.md) transforme les données d’un stockage blob Azure en exécutant un fichier de script Hive sur un cluster Hadoop Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a79-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
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
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="40a79-296">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="40a79-296">Note the following points:</span></span> 

* <span data-ttu-id="40a79-297">Dans la section des activités, il existe une seule activité dont le **type** a la valeur **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="40a79-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="40a79-298">Le fichier de script Hive, **partitionweblogs.hql**, est stocké dans le compte de stockage Azure (spécifié par le service scriptLinkedService, appelé **AzureStorageLinkedService**) et dans le dossier **script** du conteneur **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="40a79-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="40a79-299">La section **defines** est utilisée pour spécifier les paramètres d’exécution transmis au script Hive comme valeurs de configuration Hive (par ex. `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="40a79-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="40a79-300">Consultez la section [Activités de transformation des données](#data-transformation-activities) dans cet article pour obtenir des exemples JSON qui définissent les activités de transformation dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="40a79-301">Pour une procédure pas à pas complète de création de ce pipeline, consultez [Didacticiel : Générer votre premier pipeline pour traiter les données à l’aide du cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="40a79-302">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-302">Linked service</span></span>
<span data-ttu-id="40a79-303">La structure de haut niveau d’une définition de service lié est la suivante :</span><span class="sxs-lookup"><span data-stu-id="40a79-303">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="40a79-304">Le tableau suivant décrit les propriétés dans la définition JSON du pipeline :</span><span class="sxs-lookup"><span data-stu-id="40a79-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="40a79-305">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-305">Property</span></span> | <span data-ttu-id="40a79-306">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-306">Description</span></span> | <span data-ttu-id="40a79-307">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="40a79-308">name</span><span class="sxs-lookup"><span data-stu-id="40a79-308">name</span></span> | <span data-ttu-id="40a79-309">Nom du service lié.</span><span class="sxs-lookup"><span data-stu-id="40a79-309">Name of the linked service.</span></span> | <span data-ttu-id="40a79-310">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-310">Yes</span></span> | 
| <span data-ttu-id="40a79-311">propriétés - type</span><span class="sxs-lookup"><span data-stu-id="40a79-311">properties - type</span></span> | <span data-ttu-id="40a79-312">Type du service lié.</span><span class="sxs-lookup"><span data-stu-id="40a79-312">Type of the linked service.</span></span> <span data-ttu-id="40a79-313">Par exemple : Stockage Azure, Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="40a79-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="40a79-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="40a79-314">typeProperties</span></span> | <span data-ttu-id="40a79-315">La section typeProperties comporte des éléments qui sont différents pour chaque magasin de données ou environnement de calcul.</span><span class="sxs-lookup"><span data-stu-id="40a79-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="40a79-316">Consultez la section [Magasins de données](#datastores) pour obtenir des informations sur les services liés de magasin de données et [Environnements de calcul](#compute-environments) pour tous les service liés de calcul</span><span class="sxs-lookup"><span data-stu-id="40a79-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="40a79-317">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-317">Dataset</span></span> 
<span data-ttu-id="40a79-318">Un jeu de données dans Azure Data Factory est défini comme suit :</span><span class="sxs-lookup"><span data-stu-id="40a79-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="40a79-319">La table suivante décrit les propriétés dans le JSON ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="40a79-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="40a79-320">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-320">Property</span></span> | <span data-ttu-id="40a79-321">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-321">Description</span></span> | <span data-ttu-id="40a79-322">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-322">Required</span></span> | <span data-ttu-id="40a79-323">Default</span><span class="sxs-lookup"><span data-stu-id="40a79-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-324">name</span><span class="sxs-lookup"><span data-stu-id="40a79-324">name</span></span> | <span data-ttu-id="40a79-325">Nom du jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-325">Name of the dataset.</span></span> <span data-ttu-id="40a79-326">Pour connaître les règles d’affectation des noms, voir [Azure Data Factory - Règles d’affectation des noms](data-factory-naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="40a79-327">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-327">Yes</span></span> |<span data-ttu-id="40a79-328">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-328">NA</span></span> |
| <span data-ttu-id="40a79-329">type</span><span class="sxs-lookup"><span data-stu-id="40a79-329">type</span></span> | <span data-ttu-id="40a79-330">Type du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-330">Type of the dataset.</span></span> <span data-ttu-id="40a79-331">Spécifiez un des types pris en charge par Azure Data Factory (par exemple : AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="40a79-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="40a79-332">Consultez la section [Magasins de données](#data-stores) pour obtenir des informations sur les types de magasins de données et jeu de données pris en charge par Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="40a79-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="40a79-333">structure</span><span class="sxs-lookup"><span data-stu-id="40a79-333">structure</span></span> | <span data-ttu-id="40a79-334">Schéma du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-334">Schema of the dataset.</span></span> <span data-ttu-id="40a79-335">Il contient des colonnes, leurs types, etc.</span><span class="sxs-lookup"><span data-stu-id="40a79-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="40a79-336">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-336">No</span></span> |<span data-ttu-id="40a79-337">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-337">NA</span></span> |
| <span data-ttu-id="40a79-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="40a79-338">typeProperties</span></span> | <span data-ttu-id="40a79-339">Propriétés correspondant au type sélectionné.</span><span class="sxs-lookup"><span data-stu-id="40a79-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="40a79-340">Consultez la section [Magasins de données](#data-stores) pour en savoir plus sur les types pris en charge et leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="40a79-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="40a79-341">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-341">Yes</span></span> |<span data-ttu-id="40a79-342">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-342">NA</span></span> |
| <span data-ttu-id="40a79-343">external</span><span class="sxs-lookup"><span data-stu-id="40a79-343">external</span></span> | <span data-ttu-id="40a79-344">Indicateur booléen pour indiquer si un jeu de données est explicitement généré par un pipeline de fabrique de données ou non.</span><span class="sxs-lookup"><span data-stu-id="40a79-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="40a79-345">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-345">No</span></span> |<span data-ttu-id="40a79-346">false</span><span class="sxs-lookup"><span data-stu-id="40a79-346">false</span></span> |
| <span data-ttu-id="40a79-347">availability</span><span class="sxs-lookup"><span data-stu-id="40a79-347">availability</span></span> | <span data-ttu-id="40a79-348">Définit la fenêtre de traitement ou le modèle de découpage pour la production du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="40a79-349">Pour plus d’informations sur le modèle de découpage du jeu de données, consultez l’article [Planification et exécution](data-factory-scheduling-and-execution.md) .</span><span class="sxs-lookup"><span data-stu-id="40a79-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="40a79-350">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-350">Yes</span></span> |<span data-ttu-id="40a79-351">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-351">NA</span></span> |
| <span data-ttu-id="40a79-352">policy</span><span class="sxs-lookup"><span data-stu-id="40a79-352">policy</span></span> |<span data-ttu-id="40a79-353">Définit les critères ou la condition que les segments du jeu de données doivent remplir.</span><span class="sxs-lookup"><span data-stu-id="40a79-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="40a79-354">Pour plus d’informations, consultez la section [Disponibilité du jeu de données](#Policy) .</span><span class="sxs-lookup"><span data-stu-id="40a79-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="40a79-355">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-355">No</span></span> |<span data-ttu-id="40a79-356">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-356">NA</span></span> |

<span data-ttu-id="40a79-357">Chaque colonne de la section **structure** contient les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="40a79-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="40a79-358">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-358">Property</span></span> | <span data-ttu-id="40a79-359">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-359">Description</span></span> | <span data-ttu-id="40a79-360">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-361">name</span><span class="sxs-lookup"><span data-stu-id="40a79-361">name</span></span> |<span data-ttu-id="40a79-362">Nom de la colonne.</span><span class="sxs-lookup"><span data-stu-id="40a79-362">Name of the column.</span></span> |<span data-ttu-id="40a79-363">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-363">Yes</span></span> |
| <span data-ttu-id="40a79-364">type</span><span class="sxs-lookup"><span data-stu-id="40a79-364">type</span></span> |<span data-ttu-id="40a79-365">Type de données de la colonne.</span><span class="sxs-lookup"><span data-stu-id="40a79-365">Data type of the column.</span></span>  |<span data-ttu-id="40a79-366">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-366">No</span></span> |
| <span data-ttu-id="40a79-367">culture</span><span class="sxs-lookup"><span data-stu-id="40a79-367">culture</span></span> |<span data-ttu-id="40a79-368">Culture .NET à utiliser lorsque le type est spécifié et qu’il est de type .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="40a79-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="40a79-369">La valeur par défaut est `en-us`.</span><span class="sxs-lookup"><span data-stu-id="40a79-369">Default is `en-us`.</span></span> |<span data-ttu-id="40a79-370">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-370">No</span></span> |
| <span data-ttu-id="40a79-371">format</span><span class="sxs-lookup"><span data-stu-id="40a79-371">format</span></span> |<span data-ttu-id="40a79-372">Chaîne de format à utiliser lorsque le type est spécifié et qu’il est de type .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="40a79-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="40a79-373">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-373">No</span></span> |

<span data-ttu-id="40a79-374">Dans l’exemple suivant, le jeu de données contient les trois colonnes `slicetimestamp`, `projectname` et `pageviews`. Leurs types respectifs sont les suivants : String, String et Decimal.</span><span class="sxs-lookup"><span data-stu-id="40a79-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="40a79-375">Le tableau suivant décrit les propriétés que vous pouvez utiliser dans la section **availability** :</span><span class="sxs-lookup"><span data-stu-id="40a79-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="40a79-376">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-376">Property</span></span> | <span data-ttu-id="40a79-377">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-377">Description</span></span> | <span data-ttu-id="40a79-378">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-378">Required</span></span> | <span data-ttu-id="40a79-379">Default</span><span class="sxs-lookup"><span data-stu-id="40a79-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-380">frequency</span><span class="sxs-lookup"><span data-stu-id="40a79-380">frequency</span></span> |<span data-ttu-id="40a79-381">Spécifie l’unité de temps pour la production du segment du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="40a79-382"><b>Fréquence prise en charge</b>: minute, heure, jour, semaine, mois</span><span class="sxs-lookup"><span data-stu-id="40a79-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="40a79-383">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-383">Yes</span></span> |<span data-ttu-id="40a79-384">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-384">NA</span></span> |
| <span data-ttu-id="40a79-385">interval</span><span class="sxs-lookup"><span data-stu-id="40a79-385">interval</span></span> |<span data-ttu-id="40a79-386">Spécifie un multiplicateur de fréquence</span><span class="sxs-lookup"><span data-stu-id="40a79-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="40a79-387">«Frequency» et «interval» déterminent la fréquence à laquelle la tranche est produite.</span><span class="sxs-lookup"><span data-stu-id="40a79-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="40a79-388">Si vous voulez des tranches de jeu de données d’une heure, définissez <b>frequency</b> sur <b>Hour</b> et <b>interval</b> sur <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="40a79-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="40a79-389"><b>Remarque :</b> si vous définissez la fréquence en minutes, nous vous recommandons de définir l’intervalle sur une valeur au moins égale à 15.</span><span class="sxs-lookup"><span data-stu-id="40a79-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="40a79-390">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-390">Yes</span></span> |<span data-ttu-id="40a79-391">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-391">NA</span></span> |
| <span data-ttu-id="40a79-392">style</span><span class="sxs-lookup"><span data-stu-id="40a79-392">style</span></span> |<span data-ttu-id="40a79-393">Spécifie si le segment doit être généré au début / à la fin de l’intervalle.</span><span class="sxs-lookup"><span data-stu-id="40a79-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="40a79-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="40a79-394">StartOfInterval</span></span></li><li><span data-ttu-id="40a79-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="40a79-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="40a79-396">Si la fréquence est définie sur Month et le style défini sur EndOfInterval, le segment est généré le dernier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="40a79-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="40a79-397">Si le style est défini sur StartOfInterval, le segment est généré le premier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="40a79-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="40a79-398">Si la fréquence est définie sur Day et le style défini sur EndOfInterval, le segment est généré la dernière heure du jour.</span><span class="sxs-lookup"><span data-stu-id="40a79-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="40a79-399">Si la fréquence est définie sur Hour et le style défini sur EndOfInterval, le segment est généré à la fin de l’heure.</span><span class="sxs-lookup"><span data-stu-id="40a79-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="40a79-400">Par exemple, pour un segment de la période 13 h-14 h, le segment est généré à 14 h.</span><span class="sxs-lookup"><span data-stu-id="40a79-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="40a79-401">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-401">No</span></span> |<span data-ttu-id="40a79-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="40a79-402">EndOfInterval</span></span> |
| <span data-ttu-id="40a79-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="40a79-403">anchorDateTime</span></span> |<span data-ttu-id="40a79-404">Définit la position absolue dans le temps utilisée par le planificateur pour calculer les limites de tranche de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="40a79-405"><b>Remarque :</b> si AnchorDateTime contient des éléments de date plus précis que la fréquence, ces éléments plus précis sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="40a79-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="40a79-406">Par exemple, si <b>interval</b> est défini sur <b>hourly</b> (frequency : hour et interval : 1) et si <b>AnchorDateTime</b> contient <b>minutes et seconds</b>, les parties <b>minutes et seconds</b> de la valeur AnchorDateTime sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="40a79-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="40a79-407">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-407">No</span></span> |<span data-ttu-id="40a79-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="40a79-408">01/01/0001</span></span> |
| <span data-ttu-id="40a79-409">Offset</span><span class="sxs-lookup"><span data-stu-id="40a79-409">offset</span></span> |<span data-ttu-id="40a79-410">Intervalle de temps marquant le déplacement du début et de la fin de toutes les tranches du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="40a79-411"><b>Remarque :</b> si anchorDateTime et offset sont spécifiés, un décalage combiné est obtenu.</span><span class="sxs-lookup"><span data-stu-id="40a79-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="40a79-412">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-412">No</span></span> |<span data-ttu-id="40a79-413">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-413">NA</span></span> |

<span data-ttu-id="40a79-414">La section availability suivante spécifie que le jeu de données de sortie est exécuté toutes les heures (ou) que le jeu de données d’entrée est disponible toutes les heures :</span><span class="sxs-lookup"><span data-stu-id="40a79-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="40a79-415">La section **policy** de la définition du jeu de données définit les critères ou la condition que les segments du jeu de données doivent remplir.</span><span class="sxs-lookup"><span data-stu-id="40a79-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="40a79-416">Nom de la stratégie</span><span class="sxs-lookup"><span data-stu-id="40a79-416">Policy Name</span></span> | <span data-ttu-id="40a79-417">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-417">Description</span></span> | <span data-ttu-id="40a79-418">Appliqué(e) à</span><span class="sxs-lookup"><span data-stu-id="40a79-418">Applied To</span></span> | <span data-ttu-id="40a79-419">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-419">Required</span></span> | <span data-ttu-id="40a79-420">Default</span><span class="sxs-lookup"><span data-stu-id="40a79-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="40a79-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="40a79-421">minimumSizeMB</span></span> |<span data-ttu-id="40a79-422">Valide le fait que les données dans un **objet blob Azure** répondent aux exigences de taille minimale (en mégaoctets).</span><span class="sxs-lookup"><span data-stu-id="40a79-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="40a79-423">objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-423">Azure Blob</span></span> |<span data-ttu-id="40a79-424">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-424">No</span></span> |<span data-ttu-id="40a79-425">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-425">NA</span></span> |
| <span data-ttu-id="40a79-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="40a79-426">minimumRows</span></span> |<span data-ttu-id="40a79-427">Valide le fait que les données dans une **base de données SQL Azure** ou une **table Azure** contiennent le nombre minimal de lignes.</span><span class="sxs-lookup"><span data-stu-id="40a79-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="40a79-428">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-428">Azure SQL Database</span></span></li><li><span data-ttu-id="40a79-429">table Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-429">Azure Table</span></span></li></ul> |<span data-ttu-id="40a79-430">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-430">No</span></span> |<span data-ttu-id="40a79-431">N/D</span><span class="sxs-lookup"><span data-stu-id="40a79-431">NA</span></span> |

<span data-ttu-id="40a79-432">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="40a79-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="40a79-433">À moins qu’un jeu de données ne soit généré par Azure Data Factory, il doit être marqué comme **external**(externe).</span><span class="sxs-lookup"><span data-stu-id="40a79-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="40a79-434">Ce paramètre s’applique généralement aux entrées de la première activité d’un pipeline, à moins que le chaînage des activités ou pipelines ne soit utilisé.</span><span class="sxs-lookup"><span data-stu-id="40a79-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="40a79-435">name</span><span class="sxs-lookup"><span data-stu-id="40a79-435">Name</span></span> | <span data-ttu-id="40a79-436">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-436">Description</span></span> | <span data-ttu-id="40a79-437">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-437">Required</span></span> | <span data-ttu-id="40a79-438">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="40a79-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="40a79-439">dataDelay</span></span> |<span data-ttu-id="40a79-440">Durée du délai de la vérification de la disponibilité des données externes pour le segment donné.</span><span class="sxs-lookup"><span data-stu-id="40a79-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="40a79-441">Par exemple, si les données sont disponibles toutes les heures, il est possible de retarder le test vérifiant si les données externes sont disponibles et si le segment correspondant est prêt à l’aide de dataDelay.</span><span class="sxs-lookup"><span data-stu-id="40a79-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="40a79-442">S’applique uniquement à l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="40a79-442">Only applies to the present time.</span></span>  <span data-ttu-id="40a79-443">Par exemple, s’il est 13 h et si cette valeur est de 10 minutes, la validation commence à 13 h 10.</span><span class="sxs-lookup"><span data-stu-id="40a79-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="40a79-444">Ce paramètre n’affecte pas les tranches passées (tranches dont la valeur Heure de fin de la tranche + dataDelay < maintenant) qui sont traitées sans délai.</span><span class="sxs-lookup"><span data-stu-id="40a79-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="40a79-445">Les heures supérieures à 23:59 doivent être spécifiées en suivant le format `day.hours:minutes:seconds`.</span><span class="sxs-lookup"><span data-stu-id="40a79-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="40a79-446">Par exemple, pour spécifier 24 heures, n'utilisez pas 24:00:00 ; utilisez plutôt 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="40a79-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="40a79-447">Si vous utilisez 24:00:00, cette valeur est traitée comme 24 jours (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="40a79-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="40a79-448">Pour 1 jour et 4 heures, spécifiez 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="40a79-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="40a79-449">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-449">No</span></span> |<span data-ttu-id="40a79-450">0</span><span class="sxs-lookup"><span data-stu-id="40a79-450">0</span></span> |
| <span data-ttu-id="40a79-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="40a79-451">retryInterval</span></span> |<span data-ttu-id="40a79-452">Délai d'attente entre un échec et la nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="40a79-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="40a79-453">Si une tentative échoue, la prochaine tentative est après retryInterval.</span><span class="sxs-lookup"><span data-stu-id="40a79-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="40a79-454">S’il est 13 h actuellement, la première tentative commence.</span><span class="sxs-lookup"><span data-stu-id="40a79-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="40a79-455">Si la durée de la première vérification de validation est de 1 minute et si l’opération a échoué, la tentative suivante aura lieu à 13 h + 1 minute (durée) + 1 minute (intervalle avant nouvelle tentative) = 13 h 02.</span><span class="sxs-lookup"><span data-stu-id="40a79-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="40a79-456">Pour les segments dans le passé, il n’y a aucun délai.</span><span class="sxs-lookup"><span data-stu-id="40a79-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="40a79-457">La nouvelle tentative se fait immédiatement.</span><span class="sxs-lookup"><span data-stu-id="40a79-457">The retry happens immediately.</span></span> |<span data-ttu-id="40a79-458">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-458">No</span></span> |<span data-ttu-id="40a79-459">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="40a79-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="40a79-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="40a79-460">retryTimeout</span></span> |<span data-ttu-id="40a79-461">Délai d’attente pour chaque nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="40a79-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="40a79-462">Si la propriété est définie sur 10 minutes, la validation doit être effectuée en 10 minutes maximum.</span><span class="sxs-lookup"><span data-stu-id="40a79-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="40a79-463">S’il faut plus de 10 minutes pour effectuer la validation, la nouvelle tentative expire.</span><span class="sxs-lookup"><span data-stu-id="40a79-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="40a79-464">Si toutes les tentatives de validation expirent, le segment est marqué comme TimedOut.</span><span class="sxs-lookup"><span data-stu-id="40a79-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="40a79-465">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-465">No</span></span> |<span data-ttu-id="40a79-466">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="40a79-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="40a79-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="40a79-467">maximumRetry</span></span> |<span data-ttu-id="40a79-468">Nombre de fois où la disponibilité des données externes est vérifiée.</span><span class="sxs-lookup"><span data-stu-id="40a79-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="40a79-469">La valeur maximale autorisée est de 10.</span><span class="sxs-lookup"><span data-stu-id="40a79-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="40a79-470">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-470">No</span></span> |<span data-ttu-id="40a79-471">3</span><span class="sxs-lookup"><span data-stu-id="40a79-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="40a79-472">MAGASINS DE DONNÉES</span><span class="sxs-lookup"><span data-stu-id="40a79-472">DATA STORES</span></span>
<span data-ttu-id="40a79-473">La section [Service lié](#linked-service) fournit des descriptions pour les éléments JSON qui sont communes à tous les types de services liés.</span><span class="sxs-lookup"><span data-stu-id="40a79-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="40a79-474">Cette section fournit des informations sur les éléments JSON qui sont spécifiques à chaque magasin de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="40a79-475">La section [Jeu de données](#dataset) fournit des descriptions pour les éléments JSON qui sont communes à tous les types de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="40a79-476">Cette section fournit des informations sur les éléments JSON qui sont spécifiques à chaque magasin de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="40a79-477">La section [Activité](#activity) fournit des descriptions pour les éléments JSON qui sont communes à tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="40a79-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="40a79-478">Cette section fournit des informations sur les éléments JSON qui sont spécifiques à chaque magasin de données lorsqu’ils sont utilisés en tant que source/récepteur dans une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="40a79-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="40a79-479">Cliquez sur le lien du magasin qui vous intéresse pour afficher les schémas JSON pour les services liés, les jeux de données et la source/récepteur pour l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="40a79-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="40a79-480">Catégorie</span><span class="sxs-lookup"><span data-stu-id="40a79-480">Category</span></span> | <span data-ttu-id="40a79-481">Banque de données</span><span class="sxs-lookup"><span data-stu-id="40a79-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="40a79-482">**Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="40a79-482">**Azure**</span></span> |[<span data-ttu-id="40a79-483">stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="40a79-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="40a79-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="40a79-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="40a79-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="40a79-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="40a79-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="40a79-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="40a79-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="40a79-488">Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="40a79-489">Stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="40a79-490">**Bases de données**</span><span class="sxs-lookup"><span data-stu-id="40a79-490">**Databases**</span></span> |[<span data-ttu-id="40a79-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="40a79-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="40a79-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="40a79-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="40a79-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="40a79-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="40a79-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="40a79-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="40a79-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="40a79-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="40a79-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="40a79-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="40a79-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="40a79-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="40a79-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="40a79-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="40a79-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="40a79-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="40a79-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="40a79-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="40a79-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="40a79-501">**NoSQL**</span></span> |[<span data-ttu-id="40a79-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="40a79-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="40a79-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="40a79-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="40a79-504">**File**</span><span class="sxs-lookup"><span data-stu-id="40a79-504">**File**</span></span> |[<span data-ttu-id="40a79-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="40a79-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="40a79-506">Système de fichiers</span><span class="sxs-lookup"><span data-stu-id="40a79-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="40a79-507">FTP</span><span class="sxs-lookup"><span data-stu-id="40a79-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="40a79-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="40a79-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="40a79-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="40a79-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="40a79-510">**Autres**</span><span class="sxs-lookup"><span data-stu-id="40a79-510">**Others**</span></span> |[<span data-ttu-id="40a79-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="40a79-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="40a79-512">OData</span><span class="sxs-lookup"><span data-stu-id="40a79-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="40a79-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="40a79-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="40a79-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="40a79-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="40a79-515">Table web</span><span class="sxs-lookup"><span data-stu-id="40a79-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="40a79-516">un stockage Azure Blob</span><span class="sxs-lookup"><span data-stu-id="40a79-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-517">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-517">Linked service</span></span>
<span data-ttu-id="40a79-518">Il existe deux types de services liés : les services liés de stockage Azure et les services liés SAP de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="40a79-519">Service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="40a79-520">Pour lier votre compte de stockage Azure à une fabrique de données à l’aide de la **clé de compte**, créez un service lié de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="40a79-521">Pour définir un stockage Azure lié au service, définissez le **type** du service lié sur **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="40a79-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="40a79-522">Vous pouvez ensuite spécifier les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-523">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-523">Property</span></span> | <span data-ttu-id="40a79-524">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-524">Description</span></span> | <span data-ttu-id="40a79-525">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-526">connectionString</span></span> |<span data-ttu-id="40a79-527">Spécifier les informations requises pour la connexion au stockage Azure pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="40a79-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="40a79-528">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="40a79-529">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="40a79-530">Service lié SAP de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="40a79-531">Le service lié Stockage Azure SAS vous permet de lier un compte de stockage Azure à une fabrique de données Azure à l’aide d’une signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="40a79-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="40a79-532">Ainsi, la fabrique de données dispose d’un accès restreint ou limité dans le temps à tout ou partie des ressources (objet blob/conteneur) dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="40a79-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="40a79-533">Pour lier votre compte de stockage Azure à une fabrique de données à l’aide de la signature d’accès partagé, créez un service lié SAP de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="40a79-534">Pour définir un service lié SAP de stockage Azure, définissez le **type** du service lié sur **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="40a79-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="40a79-535">Vous pouvez ensuite spécifier les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="40a79-536">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-536">Property</span></span> | <span data-ttu-id="40a79-537">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-537">Description</span></span> | <span data-ttu-id="40a79-538">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="40a79-539">sasUri</span></span> |<span data-ttu-id="40a79-540">Spécifiez l’URI de signature d’accès partagé des ressources Stockage Azure, telles qu’un objet blob, un conteneur ou une table.</span><span class="sxs-lookup"><span data-stu-id="40a79-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="40a79-541">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="40a79-542">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="40a79-543">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-544">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-544">Dataset</span></span>
<span data-ttu-id="40a79-545">Pour définir un jeu de données d’objet blob Azure, définissez le **type** du jeu de données sur **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="40a79-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="40a79-546">Ensuite, spécifiez les propriétés spécifiques d’objet blob Azure suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-547">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-547">Property</span></span> | <span data-ttu-id="40a79-548">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-548">Description</span></span> | <span data-ttu-id="40a79-549">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="40a79-550">folderPath</span></span> |<span data-ttu-id="40a79-551">Chemin d'accès au conteneur et au dossier dans le stockage des objets Blobs.</span><span class="sxs-lookup"><span data-stu-id="40a79-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="40a79-552">Exemple : monconteneurblob\mondossierblob\\</span><span class="sxs-lookup"><span data-stu-id="40a79-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="40a79-553">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-553">Yes</span></span> |
| <span data-ttu-id="40a79-554">fileName</span><span class="sxs-lookup"><span data-stu-id="40a79-554">fileName</span></span> |<span data-ttu-id="40a79-555">Le nom de l’objet Blob.</span><span class="sxs-lookup"><span data-stu-id="40a79-555">Name of the blob.</span></span> <span data-ttu-id="40a79-556">fileName est facultatif et sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="40a79-557">Si vous spécifiez un nom de fichier, l’activité (y compris la copie) fonctionne sur l’objet Blob spécifique.</span><span class="sxs-lookup"><span data-stu-id="40a79-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="40a79-558">Lorsque fileName n’est pas spécifié, la copie inclut tous les objets Blob dans le paramètre folderPath du jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="40a79-559">Lorsque fileName n'est pas spécifié pour un jeu de données de sortie, le nom du fichier généré aura ce format dans l'exemple suivant : Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="40a79-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40a79-560">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-560">No</span></span> |
| <span data-ttu-id="40a79-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40a79-561">partitionedBy</span></span> |<span data-ttu-id="40a79-562">partitionedBy est une propriété facultative.</span><span class="sxs-lookup"><span data-stu-id="40a79-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="40a79-563">Vous pouvez l'utiliser pour spécifier un folderPath dynamique et le nom de fichier pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="40a79-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="40a79-564">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="40a79-565">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-565">No</span></span> |
| <span data-ttu-id="40a79-566">format</span><span class="sxs-lookup"><span data-stu-id="40a79-566">format</span></span> | <span data-ttu-id="40a79-567">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40a79-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40a79-568">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="40a79-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40a79-569">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40a79-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40a79-570">Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40a79-571">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-571">No</span></span> |
| <span data-ttu-id="40a79-572">compression</span><span class="sxs-lookup"><span data-stu-id="40a79-572">compression</span></span> | <span data-ttu-id="40a79-573">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40a79-574">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40a79-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40a79-575">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40a79-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40a79-576">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40a79-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40a79-577">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-578">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-578">Example</span></span>

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


<span data-ttu-id="40a79-579">Pour plus d’informations, consultez l’article [Azure Blob connector (connecteur d’objet blob Azure)](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="40a79-580">BlobSource dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="40a79-581">Si vous copiez des données à partir d’un stockage d’objets blob Azure, définissez le **type de source** de l’activité de copie sur **BlobSource** et spécifiez les propriétés suivantes dans la section ** source ** :</span><span class="sxs-lookup"><span data-stu-id="40a79-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source **section:</span></span>

| <span data-ttu-id="40a79-582">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-582">Property</span></span> | <span data-ttu-id="40a79-583">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-583">Description</span></span> | <span data-ttu-id="40a79-584">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-584">Allowed values</span></span> | <span data-ttu-id="40a79-585">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-586">recursive</span><span class="sxs-lookup"><span data-stu-id="40a79-586">recursive</span></span> |<span data-ttu-id="40a79-587">Indique si les données sont lues de manière récursive à partir des sous-dossiers ou uniquement du dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="40a79-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40a79-588">True (valeur par défaut), False</span><span class="sxs-lookup"><span data-stu-id="40a79-588">True (default value), False</span></span> |<span data-ttu-id="40a79-589">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="40a79-590">Exemple : BlobSource**</span><span class="sxs-lookup"><span data-stu-id="40a79-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="40a79-591">BlobSink dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="40a79-592">Si vous copiez des données dans un stockage d’objets blob Azure, définissez le **type de récepteur** de l’activité de copie sur **BlobSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-593">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-593">Property</span></span> | <span data-ttu-id="40a79-594">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-594">Description</span></span> | <span data-ttu-id="40a79-595">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-595">Allowed values</span></span> | <span data-ttu-id="40a79-596">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="40a79-597">copyBehavior</span></span> |<span data-ttu-id="40a79-598">Cette propriété définit le comportement de copie lorsque la source est BlobSource ou FileSystem.</span><span class="sxs-lookup"><span data-stu-id="40a79-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="40a79-599"><b>PreserveHierarchy</b> : conserve la hiérarchie des fichiers dans le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="40a79-600">Le chemin d’accès relatif du fichier source vers le dossier source est identique au chemin d’accès relatif du fichier cible vers le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="40a79-601"><b>FlattenHierarchy</b> : tous les fichiers du dossier source figurent dans le premier niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="40a79-602">Le nom des fichiers cibles est généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="40a79-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="40a79-603"><b>MergeFiles (par défaut)</b> : fusionne tous les fichiers du dossier source dans un même fichier.</span><span class="sxs-lookup"><span data-stu-id="40a79-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="40a79-604">Si le nom de fichier/d’objet blob est spécifié, le nom de fichier fusionné est le nom spécifié. Dans le cas contraire, le nom de fichier est généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="40a79-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="40a79-605">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="40a79-606">Exemple : BlobSink</span><span class="sxs-lookup"><span data-stu-id="40a79-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-607">Pour plus d’informations, consultez l’article [Azure Blob connector (connecteur d’objet blob Azure)](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="40a79-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="40a79-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-609">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-609">Linked service</span></span>
<span data-ttu-id="40a79-610">Pour définir un service lié Azure Data Lake Store, définissez le type du service lié sur **AzureDataLakeStore**et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-611">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-611">Property</span></span> | <span data-ttu-id="40a79-612">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-612">Description</span></span> | <span data-ttu-id="40a79-613">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-614">type</span><span class="sxs-lookup"><span data-stu-id="40a79-614">type</span></span> | <span data-ttu-id="40a79-615">La propriété type doit être définie sur : **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="40a79-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="40a79-616">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-616">Yes</span></span> |
| <span data-ttu-id="40a79-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="40a79-617">dataLakeStoreUri</span></span> | <span data-ttu-id="40a79-618">Spécifiez des informations à propos du compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40a79-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="40a79-619">Il se présente au format suivant : `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="40a79-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="40a79-620">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-620">Yes</span></span> |
| <span data-ttu-id="40a79-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="40a79-621">subscriptionId</span></span> | <span data-ttu-id="40a79-622">ID d’abonnement Azure auquel appartient le magasin Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40a79-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="40a79-623">Requis pour le récepteur</span><span class="sxs-lookup"><span data-stu-id="40a79-623">Required for sink</span></span> |
| <span data-ttu-id="40a79-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="40a79-624">resourceGroupName</span></span> | <span data-ttu-id="40a79-625">Nom du groupe de ressources Azure auquel appartient le magasin Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40a79-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="40a79-626">Requis pour le récepteur</span><span class="sxs-lookup"><span data-stu-id="40a79-626">Required for sink</span></span> |
| <span data-ttu-id="40a79-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="40a79-627">servicePrincipalId</span></span> | <span data-ttu-id="40a79-628">Spécifiez l’ID client de l’application.</span><span class="sxs-lookup"><span data-stu-id="40a79-628">Specify the application's client ID.</span></span> | <span data-ttu-id="40a79-629">Oui (pour l’authentification du principal du service)</span><span class="sxs-lookup"><span data-stu-id="40a79-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="40a79-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="40a79-630">servicePrincipalKey</span></span> | <span data-ttu-id="40a79-631">Spécifiez la clé de l’application.</span><span class="sxs-lookup"><span data-stu-id="40a79-631">Specify the application's key.</span></span> | <span data-ttu-id="40a79-632">Oui (pour l’authentification du principal du service)</span><span class="sxs-lookup"><span data-stu-id="40a79-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="40a79-633">locataire</span><span class="sxs-lookup"><span data-stu-id="40a79-633">tenant</span></span> | <span data-ttu-id="40a79-634">Spécifiez les informations de locataire (nom de domaine ou ID de locataire) dans lesquels se trouve votre application.</span><span class="sxs-lookup"><span data-stu-id="40a79-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="40a79-635">Vous pouvez le récupérer en pointant la souris dans le coin supérieur droit du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="40a79-636">Oui (pour l’authentification du principal du service)</span><span class="sxs-lookup"><span data-stu-id="40a79-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="40a79-637">autorisation</span><span class="sxs-lookup"><span data-stu-id="40a79-637">authorization</span></span> | <span data-ttu-id="40a79-638">Cliquez sur le bouton **Autoriser** dans **Data Factory Editor** et saisissez vos informations d’identification, ce qui affecte l’URL d’autorisation générée automatiquement à cette propriété.</span><span class="sxs-lookup"><span data-stu-id="40a79-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="40a79-639">Oui (pour l’authentification des informations d’identification utilisateur)</span><span class="sxs-lookup"><span data-stu-id="40a79-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="40a79-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="40a79-640">sessionId</span></span> | <span data-ttu-id="40a79-641">ID de session OAuth issu de la session d’autorisation OAuth.</span><span class="sxs-lookup"><span data-stu-id="40a79-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="40a79-642">Chaque ID de session est unique et ne peut être utilisé qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="40a79-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="40a79-643">Ce paramètre est généré automatiquement lorsque vous utilisez Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="40a79-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="40a79-644">Oui (pour l’authentification des informations d’identification utilisateur)</span><span class="sxs-lookup"><span data-stu-id="40a79-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="40a79-645">Exemple : utilisation de l’authentification d’un principal du service</span><span class="sxs-lookup"><span data-stu-id="40a79-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="40a79-646">Exemple : utilisation de l’authentification des informations d’identification utilisateur</span><span class="sxs-lookup"><span data-stu-id="40a79-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="40a79-647">Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-648">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-648">Dataset</span></span>
<span data-ttu-id="40a79-649">Pour définir un jeu de données Azure Data Lake Store, définissez le **type** du jeu de données sur **AzureDataLakeStore** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-650">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-650">Property</span></span> | <span data-ttu-id="40a79-651">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-651">Description</span></span> | <span data-ttu-id="40a79-652">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="40a79-653">folderPath</span></span> |<span data-ttu-id="40a79-654">Chemin d’accès au conteneur et au dossier dans le magasin Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="40a79-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="40a79-655">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-655">Yes</span></span> |
| <span data-ttu-id="40a79-656">fileName</span><span class="sxs-lookup"><span data-stu-id="40a79-656">fileName</span></span> |<span data-ttu-id="40a79-657">Le nom du fichier dans le magasin Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="40a79-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="40a79-658">fileName est facultatif et sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="40a79-659">Si vous spécifiez un nom de fichier, l’activité (y compris la copie) fonctionne sur le fichier spécifique.</span><span class="sxs-lookup"><span data-stu-id="40a79-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="40a79-660">Lorsque fileName n’est pas spécifié, la copie inclut tous les fichiers dans le paramètre folderPath du jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="40a79-661">Lorsque fileName n'est pas spécifié pour un jeu de données de sortie, le nom du fichier généré aura ce format dans l'exemple suivant : Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="40a79-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40a79-662">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-662">No</span></span> |
| <span data-ttu-id="40a79-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40a79-663">partitionedBy</span></span> |<span data-ttu-id="40a79-664">partitionedBy est une propriété facultative.</span><span class="sxs-lookup"><span data-stu-id="40a79-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="40a79-665">Vous pouvez l'utiliser pour spécifier un folderPath dynamique et le nom de fichier pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="40a79-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="40a79-666">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="40a79-667">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-667">No</span></span> |
| <span data-ttu-id="40a79-668">format</span><span class="sxs-lookup"><span data-stu-id="40a79-668">format</span></span> | <span data-ttu-id="40a79-669">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40a79-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40a79-670">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="40a79-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40a79-671">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40a79-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40a79-672">Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40a79-673">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-673">No</span></span> |
| <span data-ttu-id="40a79-674">compression</span><span class="sxs-lookup"><span data-stu-id="40a79-674">compression</span></span> | <span data-ttu-id="40a79-675">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40a79-676">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40a79-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40a79-677">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40a79-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40a79-678">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40a79-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40a79-679">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-680">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-681">Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="40a79-682">Source Azure Data Lake Store dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="40a79-683">Si vous copiez des données à partir d’Azure Data Lake Store, définissez le **type de source** de l’activité de copie sur **AzureDataLakeStoreSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="40a79-684">**AzureDataLakeStoreSource** prend en charge les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="40a79-685">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-685">Property</span></span> | <span data-ttu-id="40a79-686">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-686">Description</span></span> | <span data-ttu-id="40a79-687">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-687">Allowed values</span></span> | <span data-ttu-id="40a79-688">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-689">recursive</span><span class="sxs-lookup"><span data-stu-id="40a79-689">recursive</span></span> |<span data-ttu-id="40a79-690">Indique si les données sont lues de manière récursive à partir des sous-dossiers ou uniquement du dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="40a79-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40a79-691">True (valeur par défaut), False</span><span class="sxs-lookup"><span data-stu-id="40a79-691">True (default value), False</span></span> |<span data-ttu-id="40a79-692">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="40a79-693">Exemple : AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="40a79-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-694">Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="40a79-695">Récepteur Azure Data Lake Store dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="40a79-696">Si vous copiez des données dans un Azure Data Lake Store, définissez le **type de récepteur** de l’activité de copie sur **AzureDataLakeStoreSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-697">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-697">Property</span></span> | <span data-ttu-id="40a79-698">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-698">Description</span></span> | <span data-ttu-id="40a79-699">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-699">Allowed values</span></span> | <span data-ttu-id="40a79-700">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="40a79-701">copyBehavior</span></span> |<span data-ttu-id="40a79-702">Spécifie le comportement de copie.</span><span class="sxs-lookup"><span data-stu-id="40a79-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="40a79-703"><b>PreserveHierarchy</b> : conserve la hiérarchie des fichiers dans le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="40a79-704">Le chemin d’accès relatif du fichier source vers le dossier source est identique au chemin d’accès relatif du fichier cible vers le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="40a79-705"><b>FlattenHierarchy</b> : tous les fichiers du dossier source sont créés dans le premier niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="40a79-706">Les fichiers cibles sont créés avec le nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="40a79-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="40a79-707"><b>MergeFiles</b> : fusionne tous les fichiers du dossier source dans un même fichier.</span><span class="sxs-lookup"><span data-stu-id="40a79-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="40a79-708">Si le nom de fichier/d’objet blob est spécifié, le nom de fichier fusionné est le nom spécifié. Dans le cas contraire, le nom de fichier est généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="40a79-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="40a79-709">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="40a79-710">Exemple : AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="40a79-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-711">Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="40a79-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="40a79-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="40a79-713">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-713">Linked service</span></span>
<span data-ttu-id="40a79-714">Pour définir un service lié Azure Cosmos DB, réglez le **type** du service lié sur **DocumentDb** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-714">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-715">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="40a79-715">**Property**</span></span> | <span data-ttu-id="40a79-716">**Description**</span><span class="sxs-lookup"><span data-stu-id="40a79-716">**Description**</span></span> | <span data-ttu-id="40a79-717">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="40a79-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-718">connectionString</span></span> |<span data-ttu-id="40a79-719">Spécifiez les informations requises pour se connecter à la base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40a79-719">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="40a79-720">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-721">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="40a79-722">Pour plus d’informations, consultez l’article sur le [connecteur d’objet blob Azure](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-723">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-723">Dataset</span></span>
<span data-ttu-id="40a79-724">Pour définir un jeu de données Azure Cosmos DB, réglez le **type** du jeu de données sur **DocumentDbCollection** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-724">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-725">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="40a79-725">**Property**</span></span> | <span data-ttu-id="40a79-726">**Description**</span><span class="sxs-lookup"><span data-stu-id="40a79-726">**Description**</span></span> | <span data-ttu-id="40a79-727">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="40a79-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="40a79-728">collectionName</span></span> |<span data-ttu-id="40a79-729">Nom de la collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40a79-729">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="40a79-730">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-731">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="40a79-732">Pour plus d’informations, consultez l’article sur le [connecteur Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="40a79-733">Source de la collection Azure Cosmos DB dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="40a79-734">Si vous copiez des données à partir d’Azure Cosmos DB, réglez le **type de source** de l’activité de copie sur **DocumentDbCollectionSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-734">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-735">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="40a79-735">**Property**</span></span> | <span data-ttu-id="40a79-736">**Description**</span><span class="sxs-lookup"><span data-stu-id="40a79-736">**Description**</span></span> | <span data-ttu-id="40a79-737">**Valeurs autorisées**</span><span class="sxs-lookup"><span data-stu-id="40a79-737">**Allowed values**</span></span> | <span data-ttu-id="40a79-738">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="40a79-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-739">query</span><span class="sxs-lookup"><span data-stu-id="40a79-739">query</span></span> |<span data-ttu-id="40a79-740">Spécifier la requête pour lire les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-740">Specify the query to read data.</span></span> |<span data-ttu-id="40a79-741">Chaîne de requête prise en charge par Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40a79-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="40a79-742">Exemple : `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="40a79-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="40a79-743">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-743">No</span></span> <br/><br/><span data-ttu-id="40a79-744">Si non spécifié, l’instruction SQL exécutée : `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="40a79-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="40a79-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="40a79-745">nestingSeparator</span></span> |<span data-ttu-id="40a79-746">Caractère spécial pour indiquer que le document est imbriqué.</span><span class="sxs-lookup"><span data-stu-id="40a79-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="40a79-747">Tout caractère.</span><span class="sxs-lookup"><span data-stu-id="40a79-747">Any character.</span></span> <br/><br/><span data-ttu-id="40a79-748">Azure Cosmos DB est une banque NoSQL de documents JSON, où les structures imbriquées sont autorisées.</span><span class="sxs-lookup"><span data-stu-id="40a79-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="40a79-749">Azure Data Factory permet à l'utilisateur de désigner la hiérarchie via nestingSeparator, qui est « .</span><span class="sxs-lookup"><span data-stu-id="40a79-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="40a79-750">» dans les exemples ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="40a79-750">in the above examples.</span></span> <span data-ttu-id="40a79-751">Avec le séparateur, l'activité de copie générera l'objet « Name » avec trois éléments enfants First, Middle et Last, en fonction de « Name.First », « Name.Middle » et « Name.Last » dans la définition de la table.</span><span class="sxs-lookup"><span data-stu-id="40a79-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="40a79-752">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-753">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="40a79-754">Récepteur de collection Azure Cosmos DB dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="40a79-755">Si vous copiez des données dans Azure Cosmos DB, réglez le **type de récepteur** de l’activité de copie sur **DocumentDbCollectionSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-755">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-756">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="40a79-756">**Property**</span></span> | <span data-ttu-id="40a79-757">**Description**</span><span class="sxs-lookup"><span data-stu-id="40a79-757">**Description**</span></span> | <span data-ttu-id="40a79-758">**Valeurs autorisées**</span><span class="sxs-lookup"><span data-stu-id="40a79-758">**Allowed values**</span></span> | <span data-ttu-id="40a79-759">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="40a79-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="40a79-760">nestingSeparator</span></span> |<span data-ttu-id="40a79-761">Caractère spécial dans le nom de colonne source pour indiquer que le document imbriqué est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="40a79-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="40a79-762">Par exemple, ci-dessus : `Name.First` dans la table de sortie produit la structure JSON suivante dans le document Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="40a79-762">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="40a79-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="40a79-763">"Name": {</span></span><br/>    <span data-ttu-id="40a79-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="40a79-764">"First": "John"</span></span><br/><span data-ttu-id="40a79-765">},</span><span class="sxs-lookup"><span data-stu-id="40a79-765">},</span></span> |<span data-ttu-id="40a79-766">Caractère utilisé pour séparer les niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="40a79-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="40a79-767">La valeur par défaut est `.` (point).</span><span class="sxs-lookup"><span data-stu-id="40a79-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="40a79-768">Caractère utilisé pour séparer les niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="40a79-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="40a79-769">La valeur par défaut est `.` (point).</span><span class="sxs-lookup"><span data-stu-id="40a79-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="40a79-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-770">writeBatchSize</span></span> |<span data-ttu-id="40a79-771">Nombre de requêtes parallèles auprès du service Azure Cosmos DB pour créer des documents.</span><span class="sxs-lookup"><span data-stu-id="40a79-771">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="40a79-772">Vous pouvez optimiser les performances lors de la copie des données dans/à partir d’Azure Cosmos DB à l’aide de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="40a79-772">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="40a79-773">Vous pouvez obtenir de meilleures performances en augmentant writeBatchSize car davantage de requêtes sont envoyées à Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40a79-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="40a79-774">Toutefois, vous devez éviter les limitations qui peuvent déclencher le message d’erreur : « Le taux de demandes est élevé ».</span><span class="sxs-lookup"><span data-stu-id="40a79-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="40a79-775">Une limitation dépend de divers facteurs, dont la taille des documents, le nombre de termes qu’ils contiennent, la stratégie d’indexation de la collection cible, etc. Pour les opérations de copie, vous pouvez utiliser une meilleure collection (par exemple, S3) pour que le débit disponible soit maximal (2 500 unités de demande par seconde).</span><span class="sxs-lookup"><span data-stu-id="40a79-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="40a79-776">Entier </span><span class="sxs-lookup"><span data-stu-id="40a79-776">Integer</span></span> |<span data-ttu-id="40a79-777">Non (valeur par défaut : 5)</span><span class="sxs-lookup"><span data-stu-id="40a79-777">No (default: 5)</span></span> |
| <span data-ttu-id="40a79-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40a79-778">writeBatchTimeout</span></span> |<span data-ttu-id="40a79-779">Temps d'attente pour que l'opération soit terminée avant d'expirer.</span><span class="sxs-lookup"><span data-stu-id="40a79-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="40a79-780">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="40a79-780">timespan</span></span><br/><br/> <span data-ttu-id="40a79-781">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="40a79-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="40a79-782">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-783">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="40a79-784">Pour plus d’informations, consultez l’article sur le [connecteur Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="40a79-785">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-786">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-786">Linked service</span></span>
<span data-ttu-id="40a79-787">Pour définir un service lié Azure SQL Database, définissez le **type** du service lié sur **AzureSqlDatabase** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-788">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-788">Property</span></span> | <span data-ttu-id="40a79-789">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-789">Description</span></span> | <span data-ttu-id="40a79-790">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-791">connectionString</span></span> |<span data-ttu-id="40a79-792">Spécifier les informations requises pour la connexion à l’instance de base de données SQL Azure pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="40a79-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="40a79-793">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-794">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="40a79-795">Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-796">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-796">Dataset</span></span>
<span data-ttu-id="40a79-797">Pour définir un jeu de données Azure SQL Database, définissez le **type** du jeu de données sur **AzureSqlTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-798">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-798">Property</span></span> | <span data-ttu-id="40a79-799">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-799">Description</span></span> | <span data-ttu-id="40a79-800">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-801">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-801">tableName</span></span> |<span data-ttu-id="40a79-802">Nom de la table ou de la vue dans l’instance Azure SQL Database à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="40a79-803">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-804">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="40a79-805">Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="40a79-806">Source SQL dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="40a79-807">Si vous copiez des données à partir d’Azure SQL Database, définissez le **type de source** de l’activité de copie sur **SqlSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-808">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-808">Property</span></span> | <span data-ttu-id="40a79-809">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-809">Description</span></span> | <span data-ttu-id="40a79-810">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-810">Allowed values</span></span> | <span data-ttu-id="40a79-811">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="40a79-812">sqlReaderQuery</span></span> |<span data-ttu-id="40a79-813">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-813">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-814">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-814">SQL query string.</span></span> <span data-ttu-id="40a79-815">Exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40a79-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="40a79-816">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-816">No</span></span> |
| <span data-ttu-id="40a79-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40a79-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="40a79-818">Nom de la procédure stockée qui lit les données de la table source.</span><span class="sxs-lookup"><span data-stu-id="40a79-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="40a79-819">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-819">Name of the stored procedure.</span></span> |<span data-ttu-id="40a79-820">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-820">No</span></span> |
| <span data-ttu-id="40a79-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40a79-821">storedProcedureParameters</span></span> |<span data-ttu-id="40a79-822">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40a79-823">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="40a79-823">Name/value pairs.</span></span> <span data-ttu-id="40a79-824">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40a79-825">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-826">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="40a79-827">Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="40a79-828">Récepteur SQL dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="40a79-829">Si vous copiez des données dans Azure SQL Database, définissez le **type de récepteur** de l’activité de copie sur **SqlSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-830">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-830">Property</span></span> | <span data-ttu-id="40a79-831">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-831">Description</span></span> | <span data-ttu-id="40a79-832">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-832">Allowed values</span></span> | <span data-ttu-id="40a79-833">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40a79-834">writeBatchTimeout</span></span> |<span data-ttu-id="40a79-835">Temps d’attente pour que l’opération d’insertion de lot soit terminée avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="40a79-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="40a79-836">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="40a79-836">timespan</span></span><br/><br/> <span data-ttu-id="40a79-837">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="40a79-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="40a79-838">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-838">No</span></span> |
| <span data-ttu-id="40a79-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-839">writeBatchSize</span></span> |<span data-ttu-id="40a79-840">Insère des données dans la table SQL lorsque la taille du tampon atteint writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="40a79-841">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="40a79-841">Integer (number of rows)</span></span> |<span data-ttu-id="40a79-842">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="40a79-842">No (default: 10000)</span></span> |
| <span data-ttu-id="40a79-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="40a79-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="40a79-844">Spécifiez une requête pour exécuter l’activité de copie afin que les données d’un segment spécifique soient nettoyées.</span><span class="sxs-lookup"><span data-stu-id="40a79-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="40a79-845">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="40a79-845">A query statement.</span></span> |<span data-ttu-id="40a79-846">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-846">No</span></span> |
| <span data-ttu-id="40a79-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="40a79-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="40a79-848">Spécifiez le nom de la colonne que l’activité de copie doit remplir avec l’identificateur de segment généré automatiquement, qui est utilisé pour nettoyer les données d’un segment spécifique lors de la ré-exécution.</span><span class="sxs-lookup"><span data-stu-id="40a79-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="40a79-849">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="40a79-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="40a79-850">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-850">No</span></span> |
| <span data-ttu-id="40a79-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40a79-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="40a79-852">Nom de la procédure stockée qui met à jour/insère les données dans la table cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="40a79-853">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-853">Name of the stored procedure.</span></span> |<span data-ttu-id="40a79-854">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-854">No</span></span> |
| <span data-ttu-id="40a79-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40a79-855">storedProcedureParameters</span></span> |<span data-ttu-id="40a79-856">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40a79-857">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="40a79-857">Name/value pairs.</span></span> <span data-ttu-id="40a79-858">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40a79-859">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-859">No</span></span> |
| <span data-ttu-id="40a79-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="40a79-860">sqlWriterTableType</span></span> |<span data-ttu-id="40a79-861">Spécifiez le nom du type de table à utiliser dans la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="40a79-862">L’activité de copie place les données déplacées disponibles dans une table temporaire avec ce type de table.</span><span class="sxs-lookup"><span data-stu-id="40a79-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="40a79-863">Le code de procédure stockée peut ensuite fusionner les données copiées avec les données existantes.</span><span class="sxs-lookup"><span data-stu-id="40a79-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="40a79-864">Nom de type de table.</span><span class="sxs-lookup"><span data-stu-id="40a79-864">A table type name.</span></span> |<span data-ttu-id="40a79-865">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-866">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-867">Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="40a79-868">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="40a79-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-869">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-869">Linked service</span></span>
<span data-ttu-id="40a79-870">Pour définir un service lié Azure SQL Data Warehouse, définissez le **type** du service lié sur **AzureSqlDW** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-871">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-871">Property</span></span> | <span data-ttu-id="40a79-872">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-872">Description</span></span> | <span data-ttu-id="40a79-873">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-874">connectionString</span></span> |<span data-ttu-id="40a79-875">Spécifier les informations requises pour la connexion à l’instance Azure SQL Data Warehouse pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="40a79-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="40a79-876">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="40a79-877">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="40a79-878">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-879">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-879">Dataset</span></span>
<span data-ttu-id="40a79-880">Pour définir un jeu de données Azure SQL Data Warehouse, définissez le **type** du jeu de données sur **AzureSqlDWTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-881">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-881">Property</span></span> | <span data-ttu-id="40a79-882">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-882">Description</span></span> | <span data-ttu-id="40a79-883">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-884">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-884">tableName</span></span> |<span data-ttu-id="40a79-885">Nom de la table ou de la vue dans la base de données Azure SQL Data Warehouse à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="40a79-886">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-887">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-888">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="40a79-889">Source SQL DW dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="40a79-890">Si vous copiez des données à partir d’Azure SQL Data Warehouse, définissez le **type de source** de l’activité de copie sur **SqlDWSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-891">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-891">Property</span></span> | <span data-ttu-id="40a79-892">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-892">Description</span></span> | <span data-ttu-id="40a79-893">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-893">Allowed values</span></span> | <span data-ttu-id="40a79-894">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="40a79-895">sqlReaderQuery</span></span> |<span data-ttu-id="40a79-896">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-896">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-897">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-897">SQL query string.</span></span> <span data-ttu-id="40a79-898">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40a79-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40a79-899">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-899">No</span></span> |
| <span data-ttu-id="40a79-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40a79-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="40a79-901">Nom de la procédure stockée qui lit les données de la table source.</span><span class="sxs-lookup"><span data-stu-id="40a79-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="40a79-902">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-902">Name of the stored procedure.</span></span> |<span data-ttu-id="40a79-903">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-903">No</span></span> |
| <span data-ttu-id="40a79-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40a79-904">storedProcedureParameters</span></span> |<span data-ttu-id="40a79-905">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40a79-906">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="40a79-906">Name/value pairs.</span></span> <span data-ttu-id="40a79-907">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40a79-908">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-909">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-910">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="40a79-911">Récepteur SQL DW dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="40a79-912">Si vous copiez des données dans Azure SQL Data Warehouse, définissez le **type de récepteur** de l’activité de copie sur **SqlDWSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-913">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-913">Property</span></span> | <span data-ttu-id="40a79-914">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-914">Description</span></span> | <span data-ttu-id="40a79-915">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-915">Allowed values</span></span> | <span data-ttu-id="40a79-916">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="40a79-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="40a79-918">Spécifiez une requête pour exécuter l’activité de copie afin que les données d’un segment spécifique soient nettoyées.</span><span class="sxs-lookup"><span data-stu-id="40a79-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="40a79-919">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="40a79-919">A query statement.</span></span> |<span data-ttu-id="40a79-920">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-920">No</span></span> |
| <span data-ttu-id="40a79-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="40a79-921">allowPolyBase</span></span> |<span data-ttu-id="40a79-922">Indique s’il faut utiliser PolyBase (le cas échéant) au lieu du mécanisme BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="40a79-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="40a79-923">**Utiliser PolyBase est la méthode recommandée pour charger des données dans SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="40a79-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="40a79-924">true</span><span class="sxs-lookup"><span data-stu-id="40a79-924">True</span></span> <br/><span data-ttu-id="40a79-925">False (valeur par défaut)</span><span class="sxs-lookup"><span data-stu-id="40a79-925">False (default)</span></span> |<span data-ttu-id="40a79-926">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-926">No</span></span> |
| <span data-ttu-id="40a79-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="40a79-927">polyBaseSettings</span></span> |<span data-ttu-id="40a79-928">Groupe de propriétés pouvant être spécifié lorsque la propriété **allowPolybase** est définie sur **true**.</span><span class="sxs-lookup"><span data-stu-id="40a79-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="40a79-929">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-929">No</span></span> |
| <span data-ttu-id="40a79-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="40a79-930">rejectValue</span></span> |<span data-ttu-id="40a79-931">Spécifie le nombre ou le pourcentage de lignes pouvant être rejetées avant l’échec de la requête.</span><span class="sxs-lookup"><span data-stu-id="40a79-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="40a79-932">Pour en savoir plus sur les options de rejet de PolyBase dans la section **Arguments** de la rubrique [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) (Créer une table externe (Transact-SQL)).</span><span class="sxs-lookup"><span data-stu-id="40a79-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="40a79-933">0 (par défaut), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="40a79-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="40a79-934">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-934">No</span></span> |
| <span data-ttu-id="40a79-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="40a79-935">rejectType</span></span> |<span data-ttu-id="40a79-936">Spécifie si l’option rejectValue est spécifiée comme une valeur littérale ou un pourcentage.</span><span class="sxs-lookup"><span data-stu-id="40a79-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="40a79-937">Value (par défaut), Percentage</span><span class="sxs-lookup"><span data-stu-id="40a79-937">Value (default), Percentage</span></span> |<span data-ttu-id="40a79-938">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-938">No</span></span> |
| <span data-ttu-id="40a79-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="40a79-939">rejectSampleValue</span></span> |<span data-ttu-id="40a79-940">Détermine le nombre de lignes à extraire avant que PolyBase recalcule le pourcentage de lignes rejetées.</span><span class="sxs-lookup"><span data-stu-id="40a79-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="40a79-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="40a79-941">1, 2, …</span></span> |<span data-ttu-id="40a79-942">Oui, si le **rejectType** est **percentage**</span><span class="sxs-lookup"><span data-stu-id="40a79-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="40a79-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="40a79-943">useTypeDefault</span></span> |<span data-ttu-id="40a79-944">Spécifie comment gérer les valeurs manquantes dans les fichiers texte délimités lorsque PolyBase extrait des données à partir du fichier texte.</span><span class="sxs-lookup"><span data-stu-id="40a79-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="40a79-945">Pour plus d’informations sur cette propriété, consultez la section Arguments dans [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="40a79-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="40a79-946">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="40a79-946">True, False (default)</span></span> |<span data-ttu-id="40a79-947">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-947">No</span></span> |
| <span data-ttu-id="40a79-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-948">writeBatchSize</span></span> |<span data-ttu-id="40a79-949">Insère des données dans la table SQL lorsque la taille du tampon atteint writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="40a79-950">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="40a79-950">Integer (number of rows)</span></span> |<span data-ttu-id="40a79-951">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="40a79-951">No (default: 10000)</span></span> |
| <span data-ttu-id="40a79-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40a79-952">writeBatchTimeout</span></span> |<span data-ttu-id="40a79-953">Temps d’attente pour que l’opération d’insertion de lot soit terminée avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="40a79-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="40a79-954">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="40a79-954">timespan</span></span><br/><br/> <span data-ttu-id="40a79-955">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="40a79-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="40a79-956">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-957">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-958">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="40a79-959">Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-960">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-960">Linked service</span></span>
<span data-ttu-id="40a79-961">Pour définir un service lié Recherche Azure, définissez le **type** du service lié sur **Recherche Azure** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-962">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-962">Property</span></span> | <span data-ttu-id="40a79-963">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-963">Description</span></span> | <span data-ttu-id="40a79-964">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="40a79-965">url</span><span class="sxs-lookup"><span data-stu-id="40a79-965">url</span></span> | <span data-ttu-id="40a79-966">URL du service Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="40a79-967">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-967">Yes</span></span> |
| <span data-ttu-id="40a79-968">key</span><span class="sxs-lookup"><span data-stu-id="40a79-968">key</span></span> | <span data-ttu-id="40a79-969">Clé d’administration du service Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="40a79-970">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-971">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="40a79-972">Pour plus d’informations, consultez l’article [Connecteur Recherche Azure](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-973">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-973">Dataset</span></span>
<span data-ttu-id="40a79-974">Pour définir un jeu de données Recherche Azure, définissez le **type** du jeu de données sur **AzureSearchIndex** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-975">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-975">Property</span></span> | <span data-ttu-id="40a79-976">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-976">Description</span></span> | <span data-ttu-id="40a79-977">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="40a79-978">type</span><span class="sxs-lookup"><span data-stu-id="40a79-978">type</span></span> | <span data-ttu-id="40a79-979">La propriété de type doit être définie sur **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="40a79-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="40a79-980">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-980">Yes</span></span> |
| <span data-ttu-id="40a79-981">indexName</span><span class="sxs-lookup"><span data-stu-id="40a79-981">indexName</span></span> | <span data-ttu-id="40a79-982">Nom de l’index Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-982">Name of the Azure Search index.</span></span> <span data-ttu-id="40a79-983">Data Factory ne crée pas l’index.</span><span class="sxs-lookup"><span data-stu-id="40a79-983">Data Factory does not create the index.</span></span> <span data-ttu-id="40a79-984">L’index doit exister dans Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="40a79-985">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-986">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="40a79-987">Pour plus d’informations, consultez l’article [Connecteur Recherche Azure](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="40a79-988">Récepteur Index Recherche Azure dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="40a79-989">Si vous copiez des données dans un Index Recherche Azure, définissez le **type de récepteur** de l’activité de copie sur **AzureSearchIndexSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-990">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-990">Property</span></span> | <span data-ttu-id="40a79-991">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-991">Description</span></span> | <span data-ttu-id="40a79-992">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-992">Allowed values</span></span> | <span data-ttu-id="40a79-993">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="40a79-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="40a79-994">WriteBehavior</span></span> | <span data-ttu-id="40a79-995">Indique s’il convient de procéder à une fusion ou à un remplacement lorsqu’un document existe déjà dans l’index.</span><span class="sxs-lookup"><span data-stu-id="40a79-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="40a79-996">Merge (par défaut)</span><span class="sxs-lookup"><span data-stu-id="40a79-996">Merge (default)</span></span><br/><span data-ttu-id="40a79-997">Télécharger</span><span class="sxs-lookup"><span data-stu-id="40a79-997">Upload</span></span>| <span data-ttu-id="40a79-998">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-998">No</span></span> |
| <span data-ttu-id="40a79-999">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-999">WriteBatchSize</span></span> | <span data-ttu-id="40a79-1000">Charge des données dans l’index Recherche Azure lorsque la taille du tampon atteint writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="40a79-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="40a79-1001">1 à 1 000.</span><span class="sxs-lookup"><span data-stu-id="40a79-1001">1 to 1,000.</span></span> <span data-ttu-id="40a79-1002">Valeur par défaut : 1 000.</span><span class="sxs-lookup"><span data-stu-id="40a79-1002">Default value is 1000.</span></span> | <span data-ttu-id="40a79-1003">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1004">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-1005">Pour plus d’informations, consultez l’article [Connecteur Recherche Azure](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="40a79-1006">Stockage de table Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1007">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1007">Linked service</span></span>
<span data-ttu-id="40a79-1008">Il existe deux types de services liés : les services liés de stockage Azure et les services liés SAP de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="40a79-1009">Service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="40a79-1010">Pour lier votre compte de stockage Azure à une fabrique de données à l’aide de la **clé de compte**, créez un service lié de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="40a79-1011">Pour définir un stockage Azure lié au service, définissez le **type** du service lié sur **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="40a79-1012">Vous pouvez ensuite spécifier les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1013">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1013">Property</span></span> | <span data-ttu-id="40a79-1014">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1014">Description</span></span> | <span data-ttu-id="40a79-1015">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-1016">type</span><span class="sxs-lookup"><span data-stu-id="40a79-1016">type</span></span> |<span data-ttu-id="40a79-1017">La propriété de type doit être définie sur : **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="40a79-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="40a79-1018">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1018">Yes</span></span> |
| <span data-ttu-id="40a79-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-1019">connectionString</span></span> |<span data-ttu-id="40a79-1020">Spécifier les informations requises pour la connexion au stockage Azure pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="40a79-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="40a79-1021">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1021">Yes</span></span> |

<span data-ttu-id="40a79-1022">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="40a79-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="40a79-1023">Service lié SAP de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="40a79-1024">Le service lié Stockage Azure SAS vous permet de lier un compte de stockage Azure à une fabrique de données Azure à l’aide d’une signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="40a79-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="40a79-1025">Ainsi, la fabrique de données dispose d’un accès restreint ou limité dans le temps à tout ou partie des ressources (objet blob/conteneur) dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="40a79-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="40a79-1026">Pour lier votre compte de stockage Azure à une fabrique de données à l’aide de la signature d’accès partagé, créez un service lié SAP de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="40a79-1027">Pour définir un service lié SAP de stockage Azure, définissez le **type** du service lié sur **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="40a79-1028">Vous pouvez ensuite spécifier les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="40a79-1029">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1029">Property</span></span> | <span data-ttu-id="40a79-1030">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1030">Description</span></span> | <span data-ttu-id="40a79-1031">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-1032">type</span><span class="sxs-lookup"><span data-stu-id="40a79-1032">type</span></span> |<span data-ttu-id="40a79-1033">La propriété de type doit être définie sur : **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="40a79-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="40a79-1034">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1034">Yes</span></span> |
| <span data-ttu-id="40a79-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="40a79-1035">sasUri</span></span> |<span data-ttu-id="40a79-1036">Spécifiez l’URI de signature d’accès partagé des ressources Stockage Azure, telles qu’un objet blob, un conteneur ou une table.</span><span class="sxs-lookup"><span data-stu-id="40a79-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="40a79-1037">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1037">Yes</span></span> |

<span data-ttu-id="40a79-1038">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="40a79-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="40a79-1039">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-1040">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1040">Dataset</span></span>
<span data-ttu-id="40a79-1041">Pour définir un jeu de données Table Azure, définissez le **type** du jeu de données sur **AzureTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1042">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1042">Property</span></span> | <span data-ttu-id="40a79-1043">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1043">Description</span></span> | <span data-ttu-id="40a79-1044">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1045">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-1045">tableName</span></span> |<span data-ttu-id="40a79-1046">Nom de la table dans l'instance de base de données Table Azure à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="40a79-1047">Oui.</span><span class="sxs-lookup"><span data-stu-id="40a79-1047">Yes.</span></span> <span data-ttu-id="40a79-1048">Lorsqu’un tableName est spécifié sans azureTableSourceQuery, tous les enregistrements de la table sont copiés vers la destination.</span><span class="sxs-lookup"><span data-stu-id="40a79-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="40a79-1049">Si un azureTableSourceQuery est également spécifié, les enregistrements de la table qui satisfont à la requête sont copiés vers la destination.</span><span class="sxs-lookup"><span data-stu-id="40a79-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1050">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-1051">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure)](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="40a79-1052">Source Table Azure dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1053">Si vous copiez des données à partir d’un stockage de table Azure, définissez le **type de source** de l’activité de copie sur **AzureTableSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-1054">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1054">Property</span></span> | <span data-ttu-id="40a79-1055">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1055">Description</span></span> | <span data-ttu-id="40a79-1056">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1056">Allowed values</span></span> | <span data-ttu-id="40a79-1057">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="40a79-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="40a79-1059">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1060">Chaîne de requête de table Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-1060">Azure table query string.</span></span> <span data-ttu-id="40a79-1061">Consultez les exemples dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="40a79-1061">See examples in the next section.</span></span> |<span data-ttu-id="40a79-1062">Non.</span><span class="sxs-lookup"><span data-stu-id="40a79-1062">No.</span></span> <span data-ttu-id="40a79-1063">Lorsqu’un tableName est spécifié sans azureTableSourceQuery, tous les enregistrements de la table sont copiés vers la destination.</span><span class="sxs-lookup"><span data-stu-id="40a79-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="40a79-1064">Si un azureTableSourceQuery est également spécifié, les enregistrements de la table qui satisfont à la requête sont copiés vers la destination.</span><span class="sxs-lookup"><span data-stu-id="40a79-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="40a79-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="40a79-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="40a79-1066">Indiquer si l'exception de la table n'existe pas.</span><span class="sxs-lookup"><span data-stu-id="40a79-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="40a79-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="40a79-1067">TRUE</span></span><br/><span data-ttu-id="40a79-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="40a79-1068">FALSE</span></span> |<span data-ttu-id="40a79-1069">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1070">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-1071">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure)](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="40a79-1072">Récepteur Table Azure dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="40a79-1073">Si vous copiez des données dans un stockage de table Azure, définissez le **type de récepteur** de l’activité de copie sur **AzureTableSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-1074">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1074">Property</span></span> | <span data-ttu-id="40a79-1075">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1075">Description</span></span> | <span data-ttu-id="40a79-1076">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1076">Allowed values</span></span> | <span data-ttu-id="40a79-1077">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="40a79-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="40a79-1079">Valeur de clé de partition par défaut qui peut être utilisée par le récepteur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="40a79-1080">Valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1080">A string value.</span></span> |<span data-ttu-id="40a79-1081">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1081">No</span></span> |
| <span data-ttu-id="40a79-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="40a79-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="40a79-1083">Spécifiez le nom de la colonne dont les valeurs sont utilisées comme clés de partition.</span><span class="sxs-lookup"><span data-stu-id="40a79-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="40a79-1084">Si aucune valeur n'est spécifiée, AzureTableDefaultPartitionKeyValue est utilisée comme clé de partition.</span><span class="sxs-lookup"><span data-stu-id="40a79-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="40a79-1085">Nom de colonne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1085">A column name.</span></span> |<span data-ttu-id="40a79-1086">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1086">No</span></span> |
| <span data-ttu-id="40a79-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="40a79-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="40a79-1088">Spécifiez le nom de la colonne dont les valeurs sont utilisées comme clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="40a79-1089">Si aucune valeur n'est spécifiée, un GUID est utilisé pour chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="40a79-1090">Nom de colonne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1090">A column name.</span></span> |<span data-ttu-id="40a79-1091">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1091">No</span></span> |
| <span data-ttu-id="40a79-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="40a79-1092">azureTableInsertType</span></span> |<span data-ttu-id="40a79-1093">Le mode d’insertion des données dans une table Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="40a79-1094">Cette propriété détermine le remplacement ou la fusion des valeurs des lignes existantes dans la table de sortie avec des clés de partition et de ligne correspondantes.</span><span class="sxs-lookup"><span data-stu-id="40a79-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="40a79-1095">Consultez [Insertion ou fusion d’entité](https://msdn.microsoft.com/library/azure/hh452241.aspx) et [Insertion ou remplacement d’entité](https://msdn.microsoft.com/library/azure/hh452242.aspx) pour en savoir plus sur le fonctionnement de ces paramètres (fusion et remplacement).</span><span class="sxs-lookup"><span data-stu-id="40a79-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="40a79-1096">Ce paramètre s’applique au niveau de la ligne, non au niveau de la table, et aucune option ne supprime des lignes de la table de sortie qui n’existent pas dans l’entrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="40a79-1097">fusionner (par défaut)</span><span class="sxs-lookup"><span data-stu-id="40a79-1097">merge (default)</span></span><br/><span data-ttu-id="40a79-1098">remplacer</span><span class="sxs-lookup"><span data-stu-id="40a79-1098">replace</span></span> |<span data-ttu-id="40a79-1099">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1099">No</span></span> |
| <span data-ttu-id="40a79-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-1100">writeBatchSize</span></span> |<span data-ttu-id="40a79-1101">Insère des données dans la table Azure lorsque la valeur de writeBatchSize ou writeBatchTimeout est atteinte.</span><span class="sxs-lookup"><span data-stu-id="40a79-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="40a79-1102">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="40a79-1102">Integer (number of rows)</span></span> |<span data-ttu-id="40a79-1103">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="40a79-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="40a79-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40a79-1104">writeBatchTimeout</span></span> |<span data-ttu-id="40a79-1105">Insère des données dans la table Azure lorsque la valeur de writeBatchSize ou writeBatchTimeout est atteinte</span><span class="sxs-lookup"><span data-stu-id="40a79-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="40a79-1106">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="40a79-1106">timespan</span></span><br/><br/><span data-ttu-id="40a79-1107">Exemple : « 00: 20:00 » (20 minutes)</span><span class="sxs-lookup"><span data-stu-id="40a79-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="40a79-1108">Non (Valeur par défaut du délai d'attente du stockage client par défaut : 90 secondes)</span><span class="sxs-lookup"><span data-stu-id="40a79-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1109">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="40a79-1110">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure)](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="40a79-1111">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="40a79-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1112">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1112">Linked service</span></span>
<span data-ttu-id="40a79-1113">Pour définir un service lié Amazon Redshift, définissez le **type** du service lié sur **AmazonRedshift** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1114">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1114">Property</span></span> | <span data-ttu-id="40a79-1115">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1115">Description</span></span> | <span data-ttu-id="40a79-1116">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1117">server</span><span class="sxs-lookup"><span data-stu-id="40a79-1117">server</span></span> |<span data-ttu-id="40a79-1118">Nom d’hôte ou adresse IP du serveur Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="40a79-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="40a79-1119">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1119">Yes</span></span> |
| <span data-ttu-id="40a79-1120">port</span><span class="sxs-lookup"><span data-stu-id="40a79-1120">port</span></span> |<span data-ttu-id="40a79-1121">Le numéro du port TCP utilisé par le serveur Amazon Redshift pour écouter les connexions clientes.</span><span class="sxs-lookup"><span data-stu-id="40a79-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="40a79-1122">Non, valeur par défaut : 5439</span><span class="sxs-lookup"><span data-stu-id="40a79-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="40a79-1123">database</span><span class="sxs-lookup"><span data-stu-id="40a79-1123">database</span></span> |<span data-ttu-id="40a79-1124">Nom de la base de données Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="40a79-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="40a79-1125">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1125">Yes</span></span> |
| <span data-ttu-id="40a79-1126">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1126">username</span></span> |<span data-ttu-id="40a79-1127">Nom d’utilisateur ayant accès à la base de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="40a79-1128">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1128">Yes</span></span> |
| <span data-ttu-id="40a79-1129">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1129">password</span></span> |<span data-ttu-id="40a79-1130">Mot de passe du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1130">Password for the user account.</span></span> |<span data-ttu-id="40a79-1131">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1132">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="40a79-1133">Pour plus d’informations, consultez l’article [Amazon Redshift connector (connecteur Amazon Redshift)](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-1134">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1134">Dataset</span></span>
<span data-ttu-id="40a79-1135">Pour définir un jeu de données Amazon Redshift, définissez le **type** du jeu de données sur **RelationalTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1136">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1136">Property</span></span> | <span data-ttu-id="40a79-1137">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1137">Description</span></span> | <span data-ttu-id="40a79-1138">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1139">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-1139">tableName</span></span> |<span data-ttu-id="40a79-1140">Nom de la table dans l’instance de base de données Amazon Redshift à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="40a79-1141">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="40a79-1142">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="40a79-1143">Pour plus d’informations, consultez l’article [Amazon Redshift connector (connecteur Amazon Redshift)](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-1144">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="40a79-1145">Si vous copiez des données à partir d’Amazon Redshift, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-1146">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1146">Property</span></span> | <span data-ttu-id="40a79-1147">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1147">Description</span></span> | <span data-ttu-id="40a79-1148">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1148">Allowed values</span></span> | <span data-ttu-id="40a79-1149">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1150">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1150">query</span></span> |<span data-ttu-id="40a79-1151">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1152">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1152">SQL query string.</span></span> <span data-ttu-id="40a79-1153">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40a79-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40a79-1154">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1155">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="40a79-1156">Pour plus d’informations, consultez l’article [Amazon Redshift connector (connecteur Amazon Redshift)](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="40a79-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="40a79-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1158">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1158">Linked service</span></span>
<span data-ttu-id="40a79-1159">Pour définir un service lié IBM DB2, définissez le **type** du service lié sur **OnPremisesDB2** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1160">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1160">Property</span></span> | <span data-ttu-id="40a79-1161">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1161">Description</span></span> | <span data-ttu-id="40a79-1162">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1163">server</span><span class="sxs-lookup"><span data-stu-id="40a79-1163">server</span></span> |<span data-ttu-id="40a79-1164">Nom du serveur DB2.</span><span class="sxs-lookup"><span data-stu-id="40a79-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="40a79-1165">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1165">Yes</span></span> |
| <span data-ttu-id="40a79-1166">database</span><span class="sxs-lookup"><span data-stu-id="40a79-1166">database</span></span> |<span data-ttu-id="40a79-1167">Nom de la base de données DB2.</span><span class="sxs-lookup"><span data-stu-id="40a79-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="40a79-1168">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1168">Yes</span></span> |
| <span data-ttu-id="40a79-1169">schema</span><span class="sxs-lookup"><span data-stu-id="40a79-1169">schema</span></span> |<span data-ttu-id="40a79-1170">Nom du schéma dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1170">Name of the schema in the database.</span></span> <span data-ttu-id="40a79-1171">Le nom du schéma respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="40a79-1172">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1172">No</span></span> |
| <span data-ttu-id="40a79-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-1173">authenticationType</span></span> |<span data-ttu-id="40a79-1174">Type d'authentification utilisé pour se connecter à la base de données DB2.</span><span class="sxs-lookup"><span data-stu-id="40a79-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="40a79-1175">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40a79-1176">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1176">Yes</span></span> |
| <span data-ttu-id="40a79-1177">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1177">username</span></span> |<span data-ttu-id="40a79-1178">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="40a79-1179">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1179">No</span></span> |
| <span data-ttu-id="40a79-1180">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1180">password</span></span> |<span data-ttu-id="40a79-1181">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40a79-1182">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1182">No</span></span> |
| <span data-ttu-id="40a79-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1183">gatewayName</span></span> |<span data-ttu-id="40a79-1184">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données DB2 locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="40a79-1185">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1186">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="40a79-1187">Pour plus d’informations, consultez l’article [IBM DB2 connector (connecteur IBM DB2)](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-1188">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1188">Dataset</span></span>
<span data-ttu-id="40a79-1189">Pour définir un jeu de données DB2, définissez le **type** du jeu de données sur **RelationalTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="40a79-1190">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1190">Property</span></span> | <span data-ttu-id="40a79-1191">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1191">Description</span></span> | <span data-ttu-id="40a79-1192">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1193">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-1193">tableName</span></span> |<span data-ttu-id="40a79-1194">Nom de la table dans l'instance de base de données DB2 à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="40a79-1195">Le nom de la table respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="40a79-1196">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="40a79-1197">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-1198">Pour plus d’informations, consultez l’article [IBM DB2 connector (connecteur IBM DB2)](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-1199">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1200">Si vous copiez des données à partir d’IBM DB2, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-1201">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1201">Property</span></span> | <span data-ttu-id="40a79-1202">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1202">Description</span></span> | <span data-ttu-id="40a79-1203">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1203">Allowed values</span></span> | <span data-ttu-id="40a79-1204">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1205">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1205">query</span></span> |<span data-ttu-id="40a79-1206">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1207">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1207">SQL query string.</span></span> <span data-ttu-id="40a79-1208">Par exemple : `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="40a79-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="40a79-1209">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1210">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="40a79-1211">Pour plus d’informations, consultez l’article [IBM DB2 connector (connecteur IBM DB2)](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="40a79-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="40a79-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1213">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1213">Linked service</span></span>
<span data-ttu-id="40a79-1214">Pour définir un service lié MySQL, définissez le **type** du service lié sur **OnPremisesMySql** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1215">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1215">Property</span></span> | <span data-ttu-id="40a79-1216">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1216">Description</span></span> | <span data-ttu-id="40a79-1217">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1218">server</span><span class="sxs-lookup"><span data-stu-id="40a79-1218">server</span></span> |<span data-ttu-id="40a79-1219">Nom du serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="40a79-1220">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1220">Yes</span></span> |
| <span data-ttu-id="40a79-1221">database</span><span class="sxs-lookup"><span data-stu-id="40a79-1221">database</span></span> |<span data-ttu-id="40a79-1222">Nom de la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="40a79-1223">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1223">Yes</span></span> |
| <span data-ttu-id="40a79-1224">schema</span><span class="sxs-lookup"><span data-stu-id="40a79-1224">schema</span></span> |<span data-ttu-id="40a79-1225">Nom du schéma dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="40a79-1226">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1226">No</span></span> |
| <span data-ttu-id="40a79-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-1227">authenticationType</span></span> |<span data-ttu-id="40a79-1228">Type d'authentification utilisé pour se connecter à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="40a79-1229">Les valeurs possibles sont les suivantes : `Basic`.</span><span class="sxs-lookup"><span data-stu-id="40a79-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="40a79-1230">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1230">Yes</span></span> |
| <span data-ttu-id="40a79-1231">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1231">username</span></span> |<span data-ttu-id="40a79-1232">Spécifiez le nom d’utilisateur associé à la connexion à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="40a79-1233">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1233">Yes</span></span> |
| <span data-ttu-id="40a79-1234">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1234">password</span></span> |<span data-ttu-id="40a79-1235">Spécifiez le mot de passe du compte d’utilisateur que vous avez indiqué.</span><span class="sxs-lookup"><span data-stu-id="40a79-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="40a79-1236">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1236">Yes</span></span> |
| <span data-ttu-id="40a79-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1237">gatewayName</span></span> |<span data-ttu-id="40a79-1238">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="40a79-1239">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1240">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="40a79-1241">Pour plus d’informations, consultez l’article [MySQL connector (connecteur MySQL)](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-1242">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1242">Dataset</span></span>
<span data-ttu-id="40a79-1243">Pour définir un jeu de données MySQL, définissez le **type** du jeu de données sur **RelationalTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1244">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1244">Property</span></span> | <span data-ttu-id="40a79-1245">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1245">Description</span></span> | <span data-ttu-id="40a79-1246">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1247">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-1247">tableName</span></span> |<span data-ttu-id="40a79-1248">Nom de la table dans l'instance de base de données MySQL à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="40a79-1249">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1250">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="40a79-1251">Pour plus d’informations, consultez l’article [MySQL connector (connecteur MySQL)](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-1252">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1253">Si vous copiez des données à partir d’une base de données MySQL, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-1254">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1254">Property</span></span> | <span data-ttu-id="40a79-1255">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1255">Description</span></span> | <span data-ttu-id="40a79-1256">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1256">Allowed values</span></span> | <span data-ttu-id="40a79-1257">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1258">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1258">query</span></span> |<span data-ttu-id="40a79-1259">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1260">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1260">SQL query string.</span></span> <span data-ttu-id="40a79-1261">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40a79-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40a79-1262">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="40a79-1263">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="40a79-1264">Pour plus d’informations, consultez l’article [MySQL connector (connecteur MySQL)](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="40a79-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="40a79-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40a79-1266">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1266">Linked service</span></span>
<span data-ttu-id="40a79-1267">Pour définir un service lié Oracle, définissez le **type** du service lié sur **OnPremisesOracle** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1268">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1268">Property</span></span> | <span data-ttu-id="40a79-1269">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1269">Description</span></span> | <span data-ttu-id="40a79-1270">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="40a79-1271">driverType</span></span> | <span data-ttu-id="40a79-1272">Spécifiez le pilote à utiliser pour copier les données à partir de ou vers la base de données Oracle.</span><span class="sxs-lookup"><span data-stu-id="40a79-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="40a79-1273">Valeurs autorisées : **Microsoft** ou **ODP** (par défaut).</span><span class="sxs-lookup"><span data-stu-id="40a79-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="40a79-1274">Consultez la section [Version prise en charge et installation](#supported-versions-and-installation) sur les détails du pilote.</span><span class="sxs-lookup"><span data-stu-id="40a79-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="40a79-1275">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1275">No</span></span> |
| <span data-ttu-id="40a79-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-1276">connectionString</span></span> | <span data-ttu-id="40a79-1277">Spécifier les informations requises pour la connexion à l’instance de base de données Oracle pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="40a79-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="40a79-1278">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1278">Yes</span></span> |
| <span data-ttu-id="40a79-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1279">gatewayName</span></span> | <span data-ttu-id="40a79-1280">Nom de la passerelle utilisée pour se connecter au serveur Oracle local</span><span class="sxs-lookup"><span data-stu-id="40a79-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="40a79-1281">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1282">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="40a79-1283">Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-1284">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1284">Dataset</span></span>
<span data-ttu-id="40a79-1285">Pour définir un jeu de données Oracle, définissez le **type** du jeu de données sur **OracleTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1286">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1286">Property</span></span> | <span data-ttu-id="40a79-1287">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1287">Description</span></span> | <span data-ttu-id="40a79-1288">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1289">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-1289">tableName</span></span> |<span data-ttu-id="40a79-1290">Nom de la table dans la base de données Oracle à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="40a79-1291">Non (si **oracleReaderQuery** de **OracleSource** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="40a79-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1292">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="40a79-1293">Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="40a79-1294">Source Oracle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1295">Si vous copiez des données à partir d’une base de données Oracle, définissez le **type de source** de l’activité de copie sur **OracleSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-1296">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1296">Property</span></span> | <span data-ttu-id="40a79-1297">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1297">Description</span></span> | <span data-ttu-id="40a79-1298">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1298">Allowed values</span></span> | <span data-ttu-id="40a79-1299">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="40a79-1300">oracleReaderQuery</span></span> |<span data-ttu-id="40a79-1301">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1302">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1302">SQL query string.</span></span> <span data-ttu-id="40a79-1303">Par exemple : `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="40a79-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="40a79-1304">Si non spécifié, l’instruction SQL exécutée : `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="40a79-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="40a79-1305">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1306">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-1307">Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="40a79-1308">Récepteur Oracle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="40a79-1309">Si vous copiez des données dans une base de données Oracle, définissez le **type de récepteur** de l’activité de copie sur **OracleSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-1310">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1310">Property</span></span> | <span data-ttu-id="40a79-1311">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1311">Description</span></span> | <span data-ttu-id="40a79-1312">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1312">Allowed values</span></span> | <span data-ttu-id="40a79-1313">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40a79-1314">writeBatchTimeout</span></span> |<span data-ttu-id="40a79-1315">Temps d’attente pour que l’opération d’insertion de lot soit terminée avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="40a79-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="40a79-1316">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="40a79-1316">timespan</span></span><br/><br/> <span data-ttu-id="40a79-1317">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="40a79-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="40a79-1318">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1318">No</span></span> |
| <span data-ttu-id="40a79-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-1319">writeBatchSize</span></span> |<span data-ttu-id="40a79-1320">Insère des données dans la table SQL lorsque la taille du tampon atteint writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="40a79-1321">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="40a79-1321">Integer (number of rows)</span></span> |<span data-ttu-id="40a79-1322">Non (valeur par défaut : 100)</span><span class="sxs-lookup"><span data-stu-id="40a79-1322">No (default: 100)</span></span> |
| <span data-ttu-id="40a79-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="40a79-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="40a79-1324">Spécifiez une requête pour exécuter l’activité de copie afin que les données d’un segment spécifique soient nettoyées.</span><span class="sxs-lookup"><span data-stu-id="40a79-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="40a79-1325">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="40a79-1325">A query statement.</span></span> |<span data-ttu-id="40a79-1326">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1326">No</span></span> |
| <span data-ttu-id="40a79-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="40a79-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="40a79-1328">Spécifiez le nom de la colonne que l’activité de copie doit remplir avec l’identificateur de segment généré automatiquement, et qui est utilisée pour nettoyer les données d’un segment spécifique lors de la réexécution.</span><span class="sxs-lookup"><span data-stu-id="40a79-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="40a79-1329">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="40a79-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="40a79-1330">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1331">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="40a79-1332">Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="40a79-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="40a79-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1334">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1334">Linked service</span></span>
<span data-ttu-id="40a79-1335">Pour définir un service lié PostgreSQL, définissez le **type** du service lié sur **OnPremisesPostgreSql** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1336">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1336">Property</span></span> | <span data-ttu-id="40a79-1337">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1337">Description</span></span> | <span data-ttu-id="40a79-1338">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1339">server</span><span class="sxs-lookup"><span data-stu-id="40a79-1339">server</span></span> |<span data-ttu-id="40a79-1340">Nom du serveur PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="40a79-1341">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1341">Yes</span></span> |
| <span data-ttu-id="40a79-1342">database</span><span class="sxs-lookup"><span data-stu-id="40a79-1342">database</span></span> |<span data-ttu-id="40a79-1343">Nom de la base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="40a79-1344">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1344">Yes</span></span> |
| <span data-ttu-id="40a79-1345">schema</span><span class="sxs-lookup"><span data-stu-id="40a79-1345">schema</span></span> |<span data-ttu-id="40a79-1346">Nom du schéma dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1346">Name of the schema in the database.</span></span> <span data-ttu-id="40a79-1347">Le nom du schéma respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="40a79-1348">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1348">No</span></span> |
| <span data-ttu-id="40a79-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-1349">authenticationType</span></span> |<span data-ttu-id="40a79-1350">Type d'authentification utilisé pour se connecter à la base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="40a79-1351">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40a79-1352">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1352">Yes</span></span> |
| <span data-ttu-id="40a79-1353">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1353">username</span></span> |<span data-ttu-id="40a79-1354">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="40a79-1355">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1355">No</span></span> |
| <span data-ttu-id="40a79-1356">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1356">password</span></span> |<span data-ttu-id="40a79-1357">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40a79-1358">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1358">No</span></span> |
| <span data-ttu-id="40a79-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1359">gatewayName</span></span> |<span data-ttu-id="40a79-1360">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données PostgreSQL locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="40a79-1361">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1362">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="40a79-1363">Pour plus d’informations, consultez l’article [PostgreSQL connector (connecteur PostgreSQL)](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-1364">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1364">Dataset</span></span>
<span data-ttu-id="40a79-1365">Pour définir un jeu de données PostgreSQL, définissez le **type** du jeu de données sur **RelationalTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1366">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1366">Property</span></span> | <span data-ttu-id="40a79-1367">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1367">Description</span></span> | <span data-ttu-id="40a79-1368">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1369">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-1369">tableName</span></span> |<span data-ttu-id="40a79-1370">Nom de la table dans l'instance de base de données PostgreSQL à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="40a79-1371">Le nom de la table respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="40a79-1372">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1373">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="40a79-1374">Pour plus d’informations, consultez l’article [PostgreSQL connector (connecteur PostgreSQL)](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-1375">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1376">Si vous copiez des données à partir d’une base de données PostgreSQL, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-1377">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1377">Property</span></span> | <span data-ttu-id="40a79-1378">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1378">Description</span></span> | <span data-ttu-id="40a79-1379">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1379">Allowed values</span></span> | <span data-ttu-id="40a79-1380">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1381">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1381">query</span></span> |<span data-ttu-id="40a79-1382">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1383">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1383">SQL query string.</span></span> <span data-ttu-id="40a79-1384">Par exemple : "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="40a79-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="40a79-1385">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1386">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="40a79-1387">Pour plus d’informations, consultez l’article [PostgreSQL connector (connecteur PostgreSQL)](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="40a79-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="40a79-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="40a79-1389">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1389">Linked service</span></span>
<span data-ttu-id="40a79-1390">Pour définir un service lié SAP Business Warehouse (BW), définissez le **type** du service lié sur **SapBw** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="40a79-1391">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1391">Property</span></span> | <span data-ttu-id="40a79-1392">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1392">Description</span></span> | <span data-ttu-id="40a79-1393">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1393">Allowed values</span></span> | <span data-ttu-id="40a79-1394">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="40a79-1395">server</span><span class="sxs-lookup"><span data-stu-id="40a79-1395">server</span></span> | <span data-ttu-id="40a79-1396">Nom du serveur sur lequel réside l’instance SAP BW.</span><span class="sxs-lookup"><span data-stu-id="40a79-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="40a79-1397">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1397">string</span></span> | <span data-ttu-id="40a79-1398">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1398">Yes</span></span>
<span data-ttu-id="40a79-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="40a79-1399">systemNumber</span></span> | <span data-ttu-id="40a79-1400">Numéro de système du système SAP BW.</span><span class="sxs-lookup"><span data-stu-id="40a79-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="40a79-1401">Nombre décimal à deux chiffres représenté sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="40a79-1402">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1402">Yes</span></span>
<span data-ttu-id="40a79-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="40a79-1403">clientId</span></span> | <span data-ttu-id="40a79-1404">ID client du client dans le système SAP W.</span><span class="sxs-lookup"><span data-stu-id="40a79-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="40a79-1405">Nombre décimal à trois chiffres représenté sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="40a79-1406">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1406">Yes</span></span>
<span data-ttu-id="40a79-1407">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1407">username</span></span> | <span data-ttu-id="40a79-1408">Nom de l’utilisateur qui a accès au serveur SAP</span><span class="sxs-lookup"><span data-stu-id="40a79-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="40a79-1409">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1409">string</span></span> | <span data-ttu-id="40a79-1410">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1410">Yes</span></span>
<span data-ttu-id="40a79-1411">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1411">password</span></span> | <span data-ttu-id="40a79-1412">Mot de passe pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1412">Password for the user.</span></span> | <span data-ttu-id="40a79-1413">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1413">string</span></span> | <span data-ttu-id="40a79-1414">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1414">Yes</span></span>
<span data-ttu-id="40a79-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1415">gatewayName</span></span> | <span data-ttu-id="40a79-1416">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à l’instance SAP BW locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="40a79-1417">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1417">string</span></span> | <span data-ttu-id="40a79-1418">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1418">Yes</span></span>
<span data-ttu-id="40a79-1419">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-1419">encryptedCredential</span></span> | <span data-ttu-id="40a79-1420">La chaîne d’informations d’identification chiffrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1420">The encrypted credential string.</span></span> | <span data-ttu-id="40a79-1421">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1421">string</span></span> | <span data-ttu-id="40a79-1422">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="40a79-1423">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="40a79-1424">Pour plus d’informations, consultez l’article [SAP Business Warehouse connector (connecteur SAP Business Warehouse)](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-1425">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1425">Dataset</span></span>
<span data-ttu-id="40a79-1426">Pour définir un jeu de données SAP BW, définissez le **type** du jeu de données sur **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="40a79-1427">Aucune propriété propre à un type n’est prise en charge pour le type de jeu de données SAP BW **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="40a79-1428">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="40a79-1429">Pour plus d’informations, consultez l’article [SAP Business Warehouse connector (connecteur SAP Business Warehouse)](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-1430">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1431">Si vous copiez des données à partir de SAP Business Warehouse, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-1432">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1432">Property</span></span> | <span data-ttu-id="40a79-1433">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1433">Description</span></span> | <span data-ttu-id="40a79-1434">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1434">Allowed values</span></span> | <span data-ttu-id="40a79-1435">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1436">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1436">query</span></span> | <span data-ttu-id="40a79-1437">Spécifie la requête MDX pour lire les données de l’instance SAP BW.</span><span class="sxs-lookup"><span data-stu-id="40a79-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="40a79-1438">Requête MDX.</span><span class="sxs-lookup"><span data-stu-id="40a79-1438">MDX query.</span></span> | <span data-ttu-id="40a79-1439">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1440">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="40a79-1441">Pour plus d’informations, consultez l’article [SAP Business Warehouse connector (connecteur SAP Business Warehouse)](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="40a79-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="40a79-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1443">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1443">Linked service</span></span>
<span data-ttu-id="40a79-1444">Pour définir un service lié SAP HANA, définissez le **type** du service lié sur **SapHana** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="40a79-1445">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1445">Property</span></span> | <span data-ttu-id="40a79-1446">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1446">Description</span></span> | <span data-ttu-id="40a79-1447">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1447">Allowed values</span></span> | <span data-ttu-id="40a79-1448">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="40a79-1449">server</span><span class="sxs-lookup"><span data-stu-id="40a79-1449">server</span></span> | <span data-ttu-id="40a79-1450">Le nom du serveur sur lequel réside l’instance SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="40a79-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="40a79-1451">Si votre serveur utilise un port personnalisé, spécifiez `server:port`.</span><span class="sxs-lookup"><span data-stu-id="40a79-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="40a79-1452">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1452">string</span></span> | <span data-ttu-id="40a79-1453">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1453">Yes</span></span>
<span data-ttu-id="40a79-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-1454">authenticationType</span></span> | <span data-ttu-id="40a79-1455">Type d'authentification.</span><span class="sxs-lookup"><span data-stu-id="40a79-1455">Type of authentication.</span></span> | <span data-ttu-id="40a79-1456">chaîne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1456">string.</span></span> <span data-ttu-id="40a79-1457">« Basic » ou « Windows »</span><span class="sxs-lookup"><span data-stu-id="40a79-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="40a79-1458">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1458">Yes</span></span> 
<span data-ttu-id="40a79-1459">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1459">username</span></span> | <span data-ttu-id="40a79-1460">Nom de l’utilisateur qui a accès au serveur SAP</span><span class="sxs-lookup"><span data-stu-id="40a79-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="40a79-1461">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1461">string</span></span> | <span data-ttu-id="40a79-1462">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1462">Yes</span></span>
<span data-ttu-id="40a79-1463">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1463">password</span></span> | <span data-ttu-id="40a79-1464">Mot de passe pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1464">Password for the user.</span></span> | <span data-ttu-id="40a79-1465">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1465">string</span></span> | <span data-ttu-id="40a79-1466">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1466">Yes</span></span>
<span data-ttu-id="40a79-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1467">gatewayName</span></span> | <span data-ttu-id="40a79-1468">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à l’instance SAP HANA locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="40a79-1469">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1469">string</span></span> | <span data-ttu-id="40a79-1470">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1470">Yes</span></span>
<span data-ttu-id="40a79-1471">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-1471">encryptedCredential</span></span> | <span data-ttu-id="40a79-1472">La chaîne d’informations d’identification chiffrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1472">The encrypted credential string.</span></span> | <span data-ttu-id="40a79-1473">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1473">string</span></span> | <span data-ttu-id="40a79-1474">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="40a79-1475">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="40a79-1476">Pour plus d’informations, consultez l’article [SAP HANA connector (connecteur SAP HANA)](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="40a79-1477">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1477">Dataset</span></span>
<span data-ttu-id="40a79-1478">Pour définir un jeu de données SAP HANA, définissez le **type** du jeu de données sur **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="40a79-1479">Aucune propriété propre à un type n’est prise en charge pour le type de jeu de données SAP HANA **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="40a79-1480">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="40a79-1481">Pour plus d’informations, consultez l’article [SAP HANA connector (connecteur SAP HANA)](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-1482">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1483">Si vous copiez des données à partir d’un magasin de données SAP HANA, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-1484">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1484">Property</span></span> | <span data-ttu-id="40a79-1485">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1485">Description</span></span> | <span data-ttu-id="40a79-1486">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1486">Allowed values</span></span> | <span data-ttu-id="40a79-1487">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1488">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1488">query</span></span> | <span data-ttu-id="40a79-1489">Spécifie la requête SQL pour lire les données de l’instance SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="40a79-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="40a79-1490">Requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1490">SQL query.</span></span> | <span data-ttu-id="40a79-1491">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="40a79-1492">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="40a79-1493">Pour plus d’informations, consultez l’article [SAP HANA connector (connecteur SAP HANA)](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="40a79-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="40a79-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1495">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1495">Linked service</span></span>
<span data-ttu-id="40a79-1496">Vous créez un service lié de type **OnPremisesSqlServer** pour lier une base de données SQL Server locale à une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="40a79-1497">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="40a79-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="40a79-1498">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40a79-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="40a79-1499">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1499">Property</span></span> | <span data-ttu-id="40a79-1500">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1500">Description</span></span> | <span data-ttu-id="40a79-1501">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1502">type</span><span class="sxs-lookup"><span data-stu-id="40a79-1502">type</span></span> |<span data-ttu-id="40a79-1503">Le type de propriété doit être défini sur **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="40a79-1504">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1504">Yes</span></span> |
| <span data-ttu-id="40a79-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-1505">connectionString</span></span> |<span data-ttu-id="40a79-1506">Spécifiez les informations connectionString nécessaires pour connecter la base de données SQL Server locale à l’aide de l’authentification SQL ou de l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="40a79-1507">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1507">Yes</span></span> |
| <span data-ttu-id="40a79-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1508">gatewayName</span></span> |<span data-ttu-id="40a79-1509">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="40a79-1510">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1510">Yes</span></span> |
| <span data-ttu-id="40a79-1511">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1511">username</span></span> |<span data-ttu-id="40a79-1512">Spécifiez le nom d’utilisateur si vous utilisez l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="40a79-1513">Exemple : **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="40a79-1514">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1514">No</span></span> |
| <span data-ttu-id="40a79-1515">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1515">password</span></span> |<span data-ttu-id="40a79-1516">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40a79-1517">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1517">No</span></span> |

<span data-ttu-id="40a79-1518">Vous pouvez chiffrer les informations d’identification à l’aide de l’applet de commande **New-AzureRmDataFactoryEncryptValue** et les utiliser dans la chaîne de connexion comme indiqué dans l’exemple suivant (propriété **EncryptedCredential**) :</span><span class="sxs-lookup"><span data-stu-id="40a79-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="40a79-1519">Exemple : JSON pour utilisation de l’authentification SQL</span><span class="sxs-lookup"><span data-stu-id="40a79-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="40a79-1520">Exemple : JSON pour utilisation de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="40a79-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="40a79-1521">Si le nom d’utilisateur et le mot de passe sont spécifiés, la passerelle les utilise pour identifier le compte utilisateur spécifié pour connecter la base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="40a79-1522">Dans le cas contraire, la passerelle se connecte directement à SQL Server avec le contexte de sécurité de la passerelle (son compte de démarrage).</span><span class="sxs-lookup"><span data-stu-id="40a79-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="40a79-1523">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-1524">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1524">Dataset</span></span>
<span data-ttu-id="40a79-1525">Pour définir un jeu de données SQL Server, définissez le **type** du jeu de données sur **SqlServerTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1526">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1526">Property</span></span> | <span data-ttu-id="40a79-1527">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1527">Description</span></span> | <span data-ttu-id="40a79-1528">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1529">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-1529">tableName</span></span> |<span data-ttu-id="40a79-1530">Nom de la table ou de la vue dans l’instance de base de données SQL Server à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="40a79-1531">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1532">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-1533">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="40a79-1534">Source SQL dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1535">Si vous copiez des données à partir d’une base de données SQL Server, définissez le **type de source** de l’activité de copie sur **SqlSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-1536">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1536">Property</span></span> | <span data-ttu-id="40a79-1537">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1537">Description</span></span> | <span data-ttu-id="40a79-1538">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1538">Allowed values</span></span> | <span data-ttu-id="40a79-1539">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="40a79-1540">sqlReaderQuery</span></span> |<span data-ttu-id="40a79-1541">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1542">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1542">SQL query string.</span></span> <span data-ttu-id="40a79-1543">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40a79-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="40a79-1544">Peut faire référence à plusieurs tables de la base de données référencée par le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="40a79-1545">S’il n’est pas spécifié, l’instruction SQL est exécutée : select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="40a79-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="40a79-1546">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1546">No</span></span> |
| <span data-ttu-id="40a79-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40a79-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="40a79-1548">Nom de la procédure stockée qui lit les données de la table source.</span><span class="sxs-lookup"><span data-stu-id="40a79-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="40a79-1549">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="40a79-1550">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1550">No</span></span> |
| <span data-ttu-id="40a79-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40a79-1551">storedProcedureParameters</span></span> |<span data-ttu-id="40a79-1552">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40a79-1553">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1553">Name/value pairs.</span></span> <span data-ttu-id="40a79-1554">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40a79-1555">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1555">No</span></span> |

<span data-ttu-id="40a79-1556">Si **sqlReaderQuery** est spécifié pour la SqlSource, l'activité de copie exécute cette requête dans la source Azure SQL Database pour obtenir les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="40a79-1557">Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="40a79-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="40a79-1558">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section structure du code JSON du jeu de données sont utilisées pour créer une requête à exécuter sur Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="40a79-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="40a79-1559">Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="40a79-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="40a79-1560">Quand vous utilisez **sqlReaderStoredProcedureName**, vous devez toujours spécifier une valeur pour la propriété **tableName** du code JSON du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="40a79-1561">Cependant, il n’existe aucune validation effectuée pour cette table.</span><span class="sxs-lookup"><span data-stu-id="40a79-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="40a79-1562">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-1563">Dans cet exemple, **sqlReaderQuery** est spécifié pour SqlSource.</span><span class="sxs-lookup"><span data-stu-id="40a79-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="40a79-1564">L'activité de copie exécute cette requête dans la source de base de données SQL server pour obtenir les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="40a79-1565">Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="40a79-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="40a79-1566">sqlReaderQuery peut faire référence à plusieurs tables de la base de données référencée par le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="40a79-1567">Cela n’est pas limité à la seule table définie en tant que typeProperty tableName du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="40a79-1568">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section Structure sont utilisées pour sélectionner une requête à exécuter dans l'Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="40a79-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="40a79-1569">Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="40a79-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="40a79-1570">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="40a79-1571">Récepteur SQL dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="40a79-1572">Si vous copiez des données dans une base de données SQL Server, définissez le **type de récepteur** de l’activité de copie sur **SqlSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-1573">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1573">Property</span></span> | <span data-ttu-id="40a79-1574">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1574">Description</span></span> | <span data-ttu-id="40a79-1575">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1575">Allowed values</span></span> | <span data-ttu-id="40a79-1576">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40a79-1577">writeBatchTimeout</span></span> |<span data-ttu-id="40a79-1578">Temps d’attente pour que l’opération d’insertion de lot soit terminée avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="40a79-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="40a79-1579">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="40a79-1579">timespan</span></span><br/><br/> <span data-ttu-id="40a79-1580">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="40a79-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="40a79-1581">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1581">No</span></span> |
| <span data-ttu-id="40a79-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-1582">writeBatchSize</span></span> |<span data-ttu-id="40a79-1583">Insère des données dans la table SQL lorsque la taille du tampon atteint writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40a79-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="40a79-1584">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="40a79-1584">Integer (number of rows)</span></span> |<span data-ttu-id="40a79-1585">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="40a79-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="40a79-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="40a79-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="40a79-1587">Spécifiez une requête pour exécuter l'activité de copie de sorte que les données d'un segment spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="40a79-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="40a79-1588">Consultez la [section sur la répétition](#repeatability-during-copy) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="40a79-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="40a79-1589">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="40a79-1589">A query statement.</span></span> |<span data-ttu-id="40a79-1590">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1590">No</span></span> |
| <span data-ttu-id="40a79-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="40a79-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="40a79-1592">Spécifiez le nom de la colonne que l’activité de copie doit remplir avec l’identificateur de segment généré automatiquement, et qui est utilisée pour nettoyer les données d’un segment spécifique lors de la réexécution.</span><span class="sxs-lookup"><span data-stu-id="40a79-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="40a79-1593">Consultez la [section sur la répétition](#repeatability-during-copy) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="40a79-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="40a79-1594">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="40a79-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="40a79-1595">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1595">No</span></span> |
| <span data-ttu-id="40a79-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40a79-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="40a79-1597">Nom de la procédure stockée qui met à jour/insère les données dans la table cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="40a79-1598">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="40a79-1599">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1599">No</span></span> |
| <span data-ttu-id="40a79-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40a79-1600">storedProcedureParameters</span></span> |<span data-ttu-id="40a79-1601">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40a79-1602">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1602">Name/value pairs.</span></span> <span data-ttu-id="40a79-1603">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40a79-1604">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1604">No</span></span> |
| <span data-ttu-id="40a79-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="40a79-1605">sqlWriterTableType</span></span> |<span data-ttu-id="40a79-1606">Spécifiez le nom du type de table à utiliser dans la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="40a79-1607">L’activité de copie place les données déplacées disponibles dans une table temporaire avec ce type de table.</span><span class="sxs-lookup"><span data-stu-id="40a79-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="40a79-1608">Le code de procédure stockée peut ensuite fusionner les données copiées avec les données existantes.</span><span class="sxs-lookup"><span data-stu-id="40a79-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="40a79-1609">Nom de type de table.</span><span class="sxs-lookup"><span data-stu-id="40a79-1609">A table type name.</span></span> |<span data-ttu-id="40a79-1610">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1611">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1611">Example</span></span>
<span data-ttu-id="40a79-1612">Le pipeline contient une activité de copie qui est configurée pour utiliser ces jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="40a79-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="40a79-1613">Dans la définition du pipeline JSON, le type **source** est défini sur **BlobSource** et le type **sink** est défini sur **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-1614">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="40a79-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="40a79-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1616">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1616">Linked service</span></span>
<span data-ttu-id="40a79-1617">Pour définir un service lié Sybase, définissez le **type** du service lié sur **OnPremisesSybase** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1618">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1618">Property</span></span> | <span data-ttu-id="40a79-1619">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1619">Description</span></span> | <span data-ttu-id="40a79-1620">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1621">server</span><span class="sxs-lookup"><span data-stu-id="40a79-1621">server</span></span> |<span data-ttu-id="40a79-1622">Nom du serveur Sybase.</span><span class="sxs-lookup"><span data-stu-id="40a79-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="40a79-1623">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1623">Yes</span></span> |
| <span data-ttu-id="40a79-1624">database</span><span class="sxs-lookup"><span data-stu-id="40a79-1624">database</span></span> |<span data-ttu-id="40a79-1625">Nom de la base de données Sybase.</span><span class="sxs-lookup"><span data-stu-id="40a79-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="40a79-1626">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1626">Yes</span></span> |
| <span data-ttu-id="40a79-1627">schema</span><span class="sxs-lookup"><span data-stu-id="40a79-1627">schema</span></span> |<span data-ttu-id="40a79-1628">Nom du schéma dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="40a79-1629">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1629">No</span></span> |
| <span data-ttu-id="40a79-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-1630">authenticationType</span></span> |<span data-ttu-id="40a79-1631">Type d'authentification utilisé pour se connecter à la base de données Sybase.</span><span class="sxs-lookup"><span data-stu-id="40a79-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="40a79-1632">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40a79-1633">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1633">Yes</span></span> |
| <span data-ttu-id="40a79-1634">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1634">username</span></span> |<span data-ttu-id="40a79-1635">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="40a79-1636">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1636">No</span></span> |
| <span data-ttu-id="40a79-1637">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1637">password</span></span> |<span data-ttu-id="40a79-1638">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40a79-1639">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1639">No</span></span> |
| <span data-ttu-id="40a79-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1640">gatewayName</span></span> |<span data-ttu-id="40a79-1641">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données Sybase locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="40a79-1642">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1643">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="40a79-1644">Pour plus d’informations, consultez l’article [Sybase connector (connecteur Sybase)](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-1645">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1645">Dataset</span></span>
<span data-ttu-id="40a79-1646">Pour définir un jeu de données Sybase, définissez le **type** du jeu de données sur **RelationalTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1647">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1647">Property</span></span> | <span data-ttu-id="40a79-1648">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1648">Description</span></span> | <span data-ttu-id="40a79-1649">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1650">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-1650">tableName</span></span> |<span data-ttu-id="40a79-1651">Nom de la table dans l'instance de base de données Sybase à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="40a79-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="40a79-1652">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1653">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-1654">Pour plus d’informations, consultez l’article [Sybase connector (connecteur Sybase)](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-1655">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1656">Si vous copiez des données à partir d’une base de données Sybase, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-1657">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1657">Property</span></span> | <span data-ttu-id="40a79-1658">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1658">Description</span></span> | <span data-ttu-id="40a79-1659">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1659">Allowed values</span></span> | <span data-ttu-id="40a79-1660">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1661">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1661">query</span></span> |<span data-ttu-id="40a79-1662">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1663">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1663">SQL query string.</span></span> <span data-ttu-id="40a79-1664">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40a79-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40a79-1665">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1666">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="40a79-1667">Pour plus d’informations, consultez l’article [Sybase connector (connecteur Sybase)](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="40a79-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="40a79-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1669">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1669">Linked service</span></span>
<span data-ttu-id="40a79-1670">Pour définir un service lié Teradata, définissez le **type** du service lié sur **OnPremisesTeradata** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1671">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1671">Property</span></span> | <span data-ttu-id="40a79-1672">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1672">Description</span></span> | <span data-ttu-id="40a79-1673">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1674">server</span><span class="sxs-lookup"><span data-stu-id="40a79-1674">server</span></span> |<span data-ttu-id="40a79-1675">Nom du serveur Teradata.</span><span class="sxs-lookup"><span data-stu-id="40a79-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="40a79-1676">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1676">Yes</span></span> |
| <span data-ttu-id="40a79-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-1677">authenticationType</span></span> |<span data-ttu-id="40a79-1678">Type d'authentification utilisé pour se connecter à la base de données Teradata.</span><span class="sxs-lookup"><span data-stu-id="40a79-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="40a79-1679">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40a79-1680">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1680">Yes</span></span> |
| <span data-ttu-id="40a79-1681">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1681">username</span></span> |<span data-ttu-id="40a79-1682">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="40a79-1683">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1683">No</span></span> |
| <span data-ttu-id="40a79-1684">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1684">password</span></span> |<span data-ttu-id="40a79-1685">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40a79-1686">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1686">No</span></span> |
| <span data-ttu-id="40a79-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1687">gatewayName</span></span> |<span data-ttu-id="40a79-1688">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données Teradata locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="40a79-1689">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1690">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="40a79-1691">Pour plus d’informations, consultez l’article [Teradata connector (connecteur Teradata)](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-1692">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1692">Dataset</span></span>
<span data-ttu-id="40a79-1693">Pour définir un jeu de données d’objet blob Teradata, définissez le **type** du jeu de données sur **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="40a79-1694">Il n’existe actuellement aucune propriété type prise en charge pour le jeu de données Teradata.</span><span class="sxs-lookup"><span data-stu-id="40a79-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="40a79-1695">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-1696">Pour plus d’informations, consultez l’article [Teradata connector (connecteur Teradata)](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-1697">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1698">Si vous copiez des données à partir d’une base de données Teradata, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-1699">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1699">Property</span></span> | <span data-ttu-id="40a79-1700">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1700">Description</span></span> | <span data-ttu-id="40a79-1701">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1701">Allowed values</span></span> | <span data-ttu-id="40a79-1702">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1703">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1703">query</span></span> |<span data-ttu-id="40a79-1704">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1705">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1705">SQL query string.</span></span> <span data-ttu-id="40a79-1706">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40a79-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40a79-1707">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1708">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="40a79-1709">Pour plus d’informations, consultez l’article [Teradata connector (connecteur Teradata)](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="40a79-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="40a79-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="40a79-1711">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1711">Linked service</span></span>
<span data-ttu-id="40a79-1712">Pour définir un service lié Cassandra, définissez le **type** du service lié sur **OnPremisesCassandra** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1713">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1713">Property</span></span> | <span data-ttu-id="40a79-1714">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1714">Description</span></span> | <span data-ttu-id="40a79-1715">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1716">host</span><span class="sxs-lookup"><span data-stu-id="40a79-1716">host</span></span> |<span data-ttu-id="40a79-1717">Une ou plusieurs adresses IP ou noms d’hôte de serveurs Cassandra.</span><span class="sxs-lookup"><span data-stu-id="40a79-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="40a79-1718">Renseignez une liste des adresses IP ou des noms d’hôte séparée par des virgules pour vous connecter simultanément à tous les serveurs.</span><span class="sxs-lookup"><span data-stu-id="40a79-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="40a79-1719">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1719">Yes</span></span> |
| <span data-ttu-id="40a79-1720">port</span><span class="sxs-lookup"><span data-stu-id="40a79-1720">port</span></span> |<span data-ttu-id="40a79-1721">Le port TCP utilisé par le serveur Cassandra pour écouter les connexions clientes.</span><span class="sxs-lookup"><span data-stu-id="40a79-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="40a79-1722">Non, valeur par défaut : 9042</span><span class="sxs-lookup"><span data-stu-id="40a79-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="40a79-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-1723">authenticationType</span></span> |<span data-ttu-id="40a79-1724">Basique ou anonyme</span><span class="sxs-lookup"><span data-stu-id="40a79-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="40a79-1725">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1725">Yes</span></span> |
| <span data-ttu-id="40a79-1726">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1726">username</span></span> |<span data-ttu-id="40a79-1727">Spécifiez le nom d’utilisateur du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="40a79-1728">Oui, si authenticationType est défini sur De base.</span><span class="sxs-lookup"><span data-stu-id="40a79-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="40a79-1729">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1729">password</span></span> |<span data-ttu-id="40a79-1730">Spécifiez le mot de passe du compte d'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1730">Specify password for the user account.</span></span> |<span data-ttu-id="40a79-1731">Oui, si authenticationType est défini sur De base.</span><span class="sxs-lookup"><span data-stu-id="40a79-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="40a79-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1732">gatewayName</span></span> |<span data-ttu-id="40a79-1733">Le nom de la passerelle qui est utilisée pour se connecter à la base de données Cassandra locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="40a79-1734">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1734">Yes</span></span> |
| <span data-ttu-id="40a79-1735">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-1735">encryptedCredential</span></span> |<span data-ttu-id="40a79-1736">Informations d’identification chiffrées par la passerelle.</span><span class="sxs-lookup"><span data-stu-id="40a79-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="40a79-1737">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1738">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="40a79-1739">Pour plus d’informations, consultez l’article [Cassandra connector (connecteur Cassandra)](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-1740">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1740">Dataset</span></span>
<span data-ttu-id="40a79-1741">Pour définir un jeu de données Cassandra, définissez le **type** du jeu de données sur **CassandraTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1742">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1742">Property</span></span> | <span data-ttu-id="40a79-1743">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1743">Description</span></span> | <span data-ttu-id="40a79-1744">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1745">espace de clé</span><span class="sxs-lookup"><span data-stu-id="40a79-1745">keyspace</span></span> |<span data-ttu-id="40a79-1746">Nom de l’espace de clé ou du schéma dans la base de données Cassandra.</span><span class="sxs-lookup"><span data-stu-id="40a79-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="40a79-1747">Oui (si la **requête** pour **CassandraSource** n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="40a79-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="40a79-1748">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-1748">tableName</span></span> |<span data-ttu-id="40a79-1749">Nom de la table dans la base de données Cassandra.</span><span class="sxs-lookup"><span data-stu-id="40a79-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="40a79-1750">Oui (si la **requête** pour **CassandraSource** n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="40a79-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1751">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-1752">Pour plus d’informations, consultez l’article [Cassandra connector (connecteur Cassandra)](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="40a79-1753">Source Cassandra dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1754">Si vous copiez des données depuis un système Cassandra, définissez le **type de source** de l’activité de copie sur **CassandraSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-1755">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1755">Property</span></span> | <span data-ttu-id="40a79-1756">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1756">Description</span></span> | <span data-ttu-id="40a79-1757">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1757">Allowed values</span></span> | <span data-ttu-id="40a79-1758">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1759">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1759">query</span></span> |<span data-ttu-id="40a79-1760">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1761">Requête SQL-92 ou requête CQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="40a79-1762">Reportez-vous à [référence CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="40a79-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="40a79-1763">Lorsque vous utilisez la requête SQL, indiquez **keyspace name.table name** pour représenter la table que vous souhaitez interroger.</span><span class="sxs-lookup"><span data-stu-id="40a79-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="40a79-1764">Non (si tableName et keyspace sur le jeu de données sont définis).</span><span class="sxs-lookup"><span data-stu-id="40a79-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="40a79-1765">Niveau de cohérence</span><span class="sxs-lookup"><span data-stu-id="40a79-1765">consistencyLevel</span></span> |<span data-ttu-id="40a79-1766">Le niveau de cohérence spécifie le nombre de réplicas devant répondre à une demande de lecture avant de renvoyer des données à l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="40a79-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="40a79-1767">Cassandra vérifie le nombre de réplicas spécifié pour permettre aux données de répondre à la demande de lecture.</span><span class="sxs-lookup"><span data-stu-id="40a79-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="40a79-1768">UN, DEUX, TROIS, QUORUM, TOUT, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="40a79-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="40a79-1769">Reportez-vous à [Configuring data consistency (Configuration de la cohérence des données)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="40a79-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="40a79-1770">Non.</span><span class="sxs-lookup"><span data-stu-id="40a79-1770">No.</span></span> <span data-ttu-id="40a79-1771">La valeur par défaut est UN.</span><span class="sxs-lookup"><span data-stu-id="40a79-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1772">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-1773">Pour plus d’informations, consultez l’article [Cassandra connector (connecteur Cassandra)](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="40a79-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="40a79-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-1775">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1775">Linked service</span></span>
<span data-ttu-id="40a79-1776">Pour définir un service lié MongoDB, définissez le **type** du service lié sur **OnPremisesMongoDB** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1777">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1777">Property</span></span> | <span data-ttu-id="40a79-1778">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1778">Description</span></span> | <span data-ttu-id="40a79-1779">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1780">server</span><span class="sxs-lookup"><span data-stu-id="40a79-1780">server</span></span> |<span data-ttu-id="40a79-1781">Nom d’hôte ou adresse IP du serveur MongoDB.</span><span class="sxs-lookup"><span data-stu-id="40a79-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="40a79-1782">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1782">Yes</span></span> |
| <span data-ttu-id="40a79-1783">port</span><span class="sxs-lookup"><span data-stu-id="40a79-1783">port</span></span> |<span data-ttu-id="40a79-1784">Le port TCP utilisé par le serveur MongoDB pour écouter les connexions clientes.</span><span class="sxs-lookup"><span data-stu-id="40a79-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="40a79-1785">Facultatif, valeur par défaut : 27017</span><span class="sxs-lookup"><span data-stu-id="40a79-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="40a79-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-1786">authenticationType</span></span> |<span data-ttu-id="40a79-1787">De base ou anonyme.</span><span class="sxs-lookup"><span data-stu-id="40a79-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="40a79-1788">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1788">Yes</span></span> |
| <span data-ttu-id="40a79-1789">username</span><span class="sxs-lookup"><span data-stu-id="40a79-1789">username</span></span> |<span data-ttu-id="40a79-1790">Compte d’utilisateur pour accéder à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="40a79-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="40a79-1791">Oui (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="40a79-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="40a79-1792">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1792">password</span></span> |<span data-ttu-id="40a79-1793">Mot de passe pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1793">Password for the user.</span></span> |<span data-ttu-id="40a79-1794">Oui (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="40a79-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="40a79-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="40a79-1795">authSource</span></span> |<span data-ttu-id="40a79-1796">Nom de la base de données MongoDB que vous souhaitez utiliser pour vérifier vos informations d’identification pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="40a79-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="40a79-1797">Facultatif (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="40a79-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="40a79-1798">Par défaut : utilise le compte d’administrateur et la base de données spécifiée à l’aide de la propriété databaseName.</span><span class="sxs-lookup"><span data-stu-id="40a79-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="40a79-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="40a79-1799">databaseName</span></span> |<span data-ttu-id="40a79-1800">Nom de la base de données MongoDB à laquelle vous souhaitez accéder.</span><span class="sxs-lookup"><span data-stu-id="40a79-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="40a79-1801">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1801">Yes</span></span> |
| <span data-ttu-id="40a79-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1802">gatewayName</span></span> |<span data-ttu-id="40a79-1803">Nom de la passerelle qui accède au magasin de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="40a79-1804">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1804">Yes</span></span> |
| <span data-ttu-id="40a79-1805">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-1805">encryptedCredential</span></span> |<span data-ttu-id="40a79-1806">Informations d’identification chiffrées par la passerelle.</span><span class="sxs-lookup"><span data-stu-id="40a79-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="40a79-1807">Facultatif</span><span class="sxs-lookup"><span data-stu-id="40a79-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1808">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="40a79-1809">Pour plus d’informations, consultez l’article [MongoDB connector (connecteur MongoDB)](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="40a79-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-1810">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1810">Dataset</span></span>
<span data-ttu-id="40a79-1811">Pour définir un jeu de données MongoDB, définissez le **type** du jeu de données sur **MongoDbCollection** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1812">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1812">Property</span></span> | <span data-ttu-id="40a79-1813">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1813">Description</span></span> | <span data-ttu-id="40a79-1814">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="40a79-1815">collectionName</span></span> |<span data-ttu-id="40a79-1816">Nom de la collection dans la base de données MongoDB.</span><span class="sxs-lookup"><span data-stu-id="40a79-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="40a79-1817">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1818">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="40a79-1819">Pour plus d’informations, consultez l’article [MongoDB connector (connecteur MongoDB)](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="40a79-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="40a79-1820">Source MongoDB dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1821">Si vous copiez des données à partir de MongoDB, définissez le **type de source** de l’activité de copie sur **MongoDbSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-1822">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1822">Property</span></span> | <span data-ttu-id="40a79-1823">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1823">Description</span></span> | <span data-ttu-id="40a79-1824">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1824">Allowed values</span></span> | <span data-ttu-id="40a79-1825">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1826">query</span><span class="sxs-lookup"><span data-stu-id="40a79-1826">query</span></span> |<span data-ttu-id="40a79-1827">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-1828">Chaîne de requête SQL-92.</span><span class="sxs-lookup"><span data-stu-id="40a79-1828">SQL-92 query string.</span></span> <span data-ttu-id="40a79-1829">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40a79-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40a79-1830">Non (si **collectionName** du **jeu de données** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="40a79-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1831">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="40a79-1832">Pour plus d’informations, consultez l’article [MongoDB connector (connecteur MongoDB)](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="40a79-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="40a79-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="40a79-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="40a79-1834">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1834">Linked service</span></span>
<span data-ttu-id="40a79-1835">Pour définir un service lié Amazon S3, définissez le **type** du service lié sur **AwsAccessKey** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-1836">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1836">Property</span></span> | <span data-ttu-id="40a79-1837">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1837">Description</span></span> | <span data-ttu-id="40a79-1838">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1838">Allowed values</span></span> | <span data-ttu-id="40a79-1839">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="40a79-1840">accessKeyID</span></span> |<span data-ttu-id="40a79-1841">ID de la clé d’accès secrète.</span><span class="sxs-lookup"><span data-stu-id="40a79-1841">ID of the secret access key.</span></span> |<span data-ttu-id="40a79-1842">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1842">string</span></span> |<span data-ttu-id="40a79-1843">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1843">Yes</span></span> |
| <span data-ttu-id="40a79-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="40a79-1844">secretAccessKey</span></span> |<span data-ttu-id="40a79-1845">La clé d’accès secrète elle-même.</span><span class="sxs-lookup"><span data-stu-id="40a79-1845">The secret access key itself.</span></span> |<span data-ttu-id="40a79-1846">Chaîne secrète chiffrée</span><span class="sxs-lookup"><span data-stu-id="40a79-1846">Encrypted secret string</span></span> |<span data-ttu-id="40a79-1847">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-1848">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="40a79-1849">Pour plus d’informations, consultez l’article [Amazon S3 connector (connecteur Amazon S3)](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-1850">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1850">Dataset</span></span>
<span data-ttu-id="40a79-1851">Pour définir un jeu de données Amazon S3, définissez le **type** du jeu de données sur **AmazonS3** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1852">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1852">Property</span></span> | <span data-ttu-id="40a79-1853">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1853">Description</span></span> | <span data-ttu-id="40a79-1854">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1854">Allowed values</span></span> | <span data-ttu-id="40a79-1855">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="40a79-1856">bucketName</span></span> |<span data-ttu-id="40a79-1857">Le nom de compartiment S3.</span><span class="sxs-lookup"><span data-stu-id="40a79-1857">The S3 bucket name.</span></span> |<span data-ttu-id="40a79-1858">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1858">String</span></span> |<span data-ttu-id="40a79-1859">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1859">Yes</span></span> |
| <span data-ttu-id="40a79-1860">key</span><span class="sxs-lookup"><span data-stu-id="40a79-1860">key</span></span> |<span data-ttu-id="40a79-1861">La clé d’objet S3.</span><span class="sxs-lookup"><span data-stu-id="40a79-1861">The S3 object key.</span></span> |<span data-ttu-id="40a79-1862">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1862">String</span></span> |<span data-ttu-id="40a79-1863">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1863">No</span></span> |
| <span data-ttu-id="40a79-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="40a79-1864">prefix</span></span> |<span data-ttu-id="40a79-1865">Préfixe de la clé d’objet S3.</span><span class="sxs-lookup"><span data-stu-id="40a79-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="40a79-1866">Les objets dont les clés commencent par ce préfixe sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="40a79-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="40a79-1867">S’applique uniquement lorsque la clé est vide.</span><span class="sxs-lookup"><span data-stu-id="40a79-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="40a79-1868">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1868">String</span></span> |<span data-ttu-id="40a79-1869">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1869">No</span></span> |
| <span data-ttu-id="40a79-1870">version</span><span class="sxs-lookup"><span data-stu-id="40a79-1870">version</span></span> |<span data-ttu-id="40a79-1871">La version de l’objet S3 si le contrôle de version S3 est activé.</span><span class="sxs-lookup"><span data-stu-id="40a79-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="40a79-1872">string</span><span class="sxs-lookup"><span data-stu-id="40a79-1872">String</span></span> |<span data-ttu-id="40a79-1873">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1873">No</span></span> |
| <span data-ttu-id="40a79-1874">format</span><span class="sxs-lookup"><span data-stu-id="40a79-1874">format</span></span> | <span data-ttu-id="40a79-1875">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40a79-1876">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="40a79-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40a79-1877">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40a79-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40a79-1878">Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40a79-1879">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1879">No</span></span> | |
| <span data-ttu-id="40a79-1880">compression</span><span class="sxs-lookup"><span data-stu-id="40a79-1880">compression</span></span> | <span data-ttu-id="40a79-1881">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40a79-1882">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40a79-1883">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40a79-1884">Pour en savoir plus, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40a79-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40a79-1885">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="40a79-1886">bucketName + key spécifient l’emplacement de l’objet S3 où le compartiment est le conteneur racine pour les objets S3 et la clé est le chemin d’accès complet à l’objet S3.</span><span class="sxs-lookup"><span data-stu-id="40a79-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="40a79-1887">Exemple : exemple de jeu de données avec le préfixe</span><span class="sxs-lookup"><span data-stu-id="40a79-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="40a79-1888">Exemple : exemple de jeu de données (avec la version)</span><span class="sxs-lookup"><span data-stu-id="40a79-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="40a79-1889">Exemple : chemins d’accès dynamiques pour S3</span><span class="sxs-lookup"><span data-stu-id="40a79-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="40a79-1890">Dans l’exemple, nous avons utilisé des valeurs fixes pour les propriétés key et bucketName dans le jeu de données Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="40a79-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="40a79-1891">Vous pouvez demander à Data Factory de calculer les propriétés key et bucketName dynamiquement au moment de l’exécution à l’aide de variables système telles que SliceStart.</span><span class="sxs-lookup"><span data-stu-id="40a79-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="40a79-1892">Vous pouvez faire de même pour la propriété « prefix » d’un jeu de données Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="40a79-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="40a79-1893">Pour obtenir la liste des fonctions et variables prises en charge, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="40a79-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="40a79-1894">Pour plus d’informations, consultez l’article [Amazon S3 connector (connecteur Amazon S3)](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40a79-1895">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1896">Si vous copiez des données à partir d’Amazon S3, définissez le **type de source** de l’activité de copie sur **FileSystemSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40a79-1897">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1897">Property</span></span> | <span data-ttu-id="40a79-1898">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1898">Description</span></span> | <span data-ttu-id="40a79-1899">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1899">Allowed values</span></span> | <span data-ttu-id="40a79-1900">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="40a79-1901">recursive</span></span> |<span data-ttu-id="40a79-1902">Spécifie s’il faut répertorier de manière récursive les objets S3 sous le répertoire.</span><span class="sxs-lookup"><span data-stu-id="40a79-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="40a79-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="40a79-1903">true/false</span></span> |<span data-ttu-id="40a79-1904">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="40a79-1905">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="40a79-1906">Pour plus d’informations, consultez l’article [Amazon S3 connector (connecteur Amazon S3)](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="40a79-1907">Système de fichiers</span><span class="sxs-lookup"><span data-stu-id="40a79-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="40a79-1908">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1908">Linked service</span></span>
<span data-ttu-id="40a79-1909">Vous pouvez lier un système de fichiers local à une fabrique de données Azure avec le service lié **Serveur de fichiers local**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="40a79-1910">Le tableau suivant décrit les éléments JSON spécifiques au service lié Serveur de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="40a79-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="40a79-1911">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1911">Property</span></span> | <span data-ttu-id="40a79-1912">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1912">Description</span></span> | <span data-ttu-id="40a79-1913">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1914">type</span><span class="sxs-lookup"><span data-stu-id="40a79-1914">type</span></span> |<span data-ttu-id="40a79-1915">Vérifiez que la propriété type est définie sur **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="40a79-1916">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1916">Yes</span></span> |
| <span data-ttu-id="40a79-1917">host</span><span class="sxs-lookup"><span data-stu-id="40a79-1917">host</span></span> |<span data-ttu-id="40a79-1918">Spécifie le chemin d’accès racine du dossier que vous souhaitez copier.</span><span class="sxs-lookup"><span data-stu-id="40a79-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="40a79-1919">Utilisez le caractère d’échappement « \ » pour les caractères spéciaux contenus dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="40a79-1920">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="40a79-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="40a79-1921">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1921">Yes</span></span> |
| <span data-ttu-id="40a79-1922">userId</span><span class="sxs-lookup"><span data-stu-id="40a79-1922">userid</span></span> |<span data-ttu-id="40a79-1923">Spécifiez l’ID de l’utilisateur qui a accès au serveur.</span><span class="sxs-lookup"><span data-stu-id="40a79-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="40a79-1924">Non (si vous choisissez encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="40a79-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="40a79-1925">password</span><span class="sxs-lookup"><span data-stu-id="40a79-1925">password</span></span> |<span data-ttu-id="40a79-1926">Spécifiez le mot de passe de l’utilisateur (userid).</span><span class="sxs-lookup"><span data-stu-id="40a79-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="40a79-1927">Non (si vous choisissez encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="40a79-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="40a79-1928">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-1928">encryptedCredential</span></span> |<span data-ttu-id="40a79-1929">Spécifiez les informations d’identification chiffrées que vous pouvez obtenir en exécutant l’applet de commande New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="40a79-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="40a79-1930">Non (si vous choisissez de spécifier un nom d'utilisateur et un mot de passe en texte brut)</span><span class="sxs-lookup"><span data-stu-id="40a79-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="40a79-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-1931">gatewayName</span></span> |<span data-ttu-id="40a79-1932">Spécifie le nom de la passerelle que Data Factory doit utiliser pour se connecter au serveur de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="40a79-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="40a79-1933">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="40a79-1934">Exemples de définitions de chemin d’accès du dossier</span><span class="sxs-lookup"><span data-stu-id="40a79-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="40a79-1935">Scénario</span><span class="sxs-lookup"><span data-stu-id="40a79-1935">Scenario</span></span> | <span data-ttu-id="40a79-1936">Hôte dans la définition du service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-1936">Host in linked service definition</span></span> | <span data-ttu-id="40a79-1937">folderPath dans la définition du jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1938">Dossier local sur l’ordinateur passerelle de gestion des données : </span><span class="sxs-lookup"><span data-stu-id="40a79-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="40a79-1939">Exemples : D:\\\* ou D:\dossier\sous-dossier\\*</span><span class="sxs-lookup"><span data-stu-id="40a79-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="40a79-1940">D:\\\\ (pour la passerelle de gestion des données 2.0 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="40a79-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="40a79-1941">hôte local (pour les versions de la passerelle de gestion des données antérieures à 2.0)</span><span class="sxs-lookup"><span data-stu-id="40a79-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="40a79-1942">.\\\\ ou dossier\\\\sous-dossier (pour la passerelle de gestion des données 2.0 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="40a79-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="40a79-1943">D:\\\\ ou D:\\\\dossier\\\\sous-dossier (pour les versions de la passerelle antérieures à 2.0)</span><span class="sxs-lookup"><span data-stu-id="40a79-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="40a79-1944">Dossier partagé distant : </span><span class="sxs-lookup"><span data-stu-id="40a79-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="40a79-1945">Exemples : \\\\myserver\\share\\\* ou \\\\myserver\\share\\dossier\\sous-dossier\\*</span><span class="sxs-lookup"><span data-stu-id="40a79-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="40a79-1946">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="40a79-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="40a79-1947">.\\\\ ou dossier\\\\sous-dossier</span><span class="sxs-lookup"><span data-stu-id="40a79-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="40a79-1948">Exemple : utilisation d’un nom d'utilisateur et d’un mot de passe en texte brut</span><span class="sxs-lookup"><span data-stu-id="40a79-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="40a79-1949">Exemple : utilisation de l’élément encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="40a79-1950">Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-1951">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-1951">Dataset</span></span>
<span data-ttu-id="40a79-1952">Pour définir un jeu de données de système de fichiers, définissez le **type** du jeu de données sur **FileShare** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-1953">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1953">Property</span></span> | <span data-ttu-id="40a79-1954">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1954">Description</span></span> | <span data-ttu-id="40a79-1955">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="40a79-1956">folderPath</span></span> |<span data-ttu-id="40a79-1957">Spécifie le sous-chemin vers le dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="40a79-1958">Utilisez le caractère d’échappement « \ » pour les caractères spéciaux contenus dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="40a79-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="40a79-1959">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="40a79-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="40a79-1960">Vous pouvez également effectuer une combinaison avec la propriété **partitionBy** pour que les chemins d’accès de dossier soient basés sur les dates et heures de démarrage et d’arrêt de la tranche.</span><span class="sxs-lookup"><span data-stu-id="40a79-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="40a79-1961">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-1961">Yes</span></span> |
| <span data-ttu-id="40a79-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="40a79-1962">fileName</span></span> |<span data-ttu-id="40a79-1963">Spécifiez le nom du fichier dans l’élément **folderPath** si vous souhaitez que la table se réfère à un fichier spécifique du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="40a79-1964">Si vous ne spécifiez aucune valeur pour cette propriété, le tableau pointe vers tous les fichiers du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="40a79-1965">Lorsque fileName n’est pas spécifié pour un jeu de données de sortie, le nom du fichier généré est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="40a79-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="40a79-1966">`Data.<Guid>.txt` (Exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="40a79-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="40a79-1967">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1967">No</span></span> |
| <span data-ttu-id="40a79-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="40a79-1968">fileFilter</span></span> |<span data-ttu-id="40a79-1969">Spécifiez un filtre à utiliser pour sélectionner un sous-ensemble de fichiers dans le folderPath plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="40a79-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="40a79-1970">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="40a79-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="40a79-1971">Exemple 1 : « fileFilter » : « *.log »</span><span class="sxs-lookup"><span data-stu-id="40a79-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="40a79-1972">Exemple 2 : « fileFilter » : « 2016-1-?.txt »</span><span class="sxs-lookup"><span data-stu-id="40a79-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="40a79-1973">Remarque : fileFilter s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="40a79-1974">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1974">No</span></span> |
| <span data-ttu-id="40a79-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40a79-1975">partitionedBy</span></span> |<span data-ttu-id="40a79-1976">partitionedBy peut être utilisé pour spécifier un folderPath/fileName dynamique pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="40a79-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="40a79-1977">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="40a79-1978">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1978">No</span></span> |
| <span data-ttu-id="40a79-1979">format</span><span class="sxs-lookup"><span data-stu-id="40a79-1979">format</span></span> | <span data-ttu-id="40a79-1980">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40a79-1981">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="40a79-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40a79-1982">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40a79-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40a79-1983">Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40a79-1984">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1984">No</span></span> |
| <span data-ttu-id="40a79-1985">compression</span><span class="sxs-lookup"><span data-stu-id="40a79-1985">compression</span></span> | <span data-ttu-id="40a79-1986">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40a79-1987">Types pris en charge : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Niveaux pris en charge : **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40a79-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40a79-1988">consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40a79-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40a79-1989">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="40a79-1990">Vous ne pouvez pas utiliser fileName et fileFilter simultanément.</span><span class="sxs-lookup"><span data-stu-id="40a79-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="40a79-1991">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-1992">Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40a79-1993">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="40a79-1994">Si vous copiez des données à partir d’un système de fichiers, définissez le **type de source** de l’activité de copie sur **FileSystemSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-1995">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-1995">Property</span></span> | <span data-ttu-id="40a79-1996">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-1996">Description</span></span> | <span data-ttu-id="40a79-1997">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-1997">Allowed values</span></span> | <span data-ttu-id="40a79-1998">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-1999">recursive</span><span class="sxs-lookup"><span data-stu-id="40a79-1999">recursive</span></span> |<span data-ttu-id="40a79-2000">Indique si les données sont lues de manière récursive à partir des sous-dossiers ou uniquement du dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="40a79-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="40a79-2001">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="40a79-2001">True, False (default)</span></span> |<span data-ttu-id="40a79-2002">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2003">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="40a79-2004">Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="40a79-2005">Récepteur Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="40a79-2006">Si vous copiez des données dans un système de fichiers, définissez le **type de récepteur** de l’activité de copie sur **FileSystemSink** et spécifiez les propriétés suivantes dans la section **sink** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40a79-2007">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2007">Property</span></span> | <span data-ttu-id="40a79-2008">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2008">Description</span></span> | <span data-ttu-id="40a79-2009">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-2009">Allowed values</span></span> | <span data-ttu-id="40a79-2010">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="40a79-2011">copyBehavior</span></span> |<span data-ttu-id="40a79-2012">Cette propriété définit le comportement de copie lorsque la source est BlobSource ou FileSystem.</span><span class="sxs-lookup"><span data-stu-id="40a79-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="40a79-2013">**PreserveHierarchy :** conserve la hiérarchie des fichiers dans le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="40a79-2014">Le chemin d’accès relatif du fichier source vers le dossier source est identique au chemin d’accès relatif du fichier cible vers le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="40a79-2015">**FlattenHierarchy**: tous les fichiers du dossier source sont créés dans le premier niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="40a79-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="40a79-2016">Les fichiers cibles sont créés avec un nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="40a79-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="40a79-2017">**MergeFiles** : fusionne tous les fichiers du dossier source dans un même fichier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="40a79-2018">Si le nom d’objet blob ou le nom de fichier est spécifié, le nom de fichier fusionné est le nom spécifié.</span><span class="sxs-lookup"><span data-stu-id="40a79-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="40a79-2019">Dans le cas contraire, il s’agit d’un nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="40a79-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="40a79-2020">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2020">No</span></span> |
<span data-ttu-id="40a79-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="40a79-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="40a79-2022">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-2023">Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="40a79-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="40a79-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-2025">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2025">Linked service</span></span>
<span data-ttu-id="40a79-2026">Pour définir un service lié FTP, définissez le **type** du service lié sur **FtpServer** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2027">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2027">Property</span></span> | <span data-ttu-id="40a79-2028">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2028">Description</span></span> | <span data-ttu-id="40a79-2029">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2029">Required</span></span> | <span data-ttu-id="40a79-2030">Default</span><span class="sxs-lookup"><span data-stu-id="40a79-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2031">host</span><span class="sxs-lookup"><span data-stu-id="40a79-2031">host</span></span> |<span data-ttu-id="40a79-2032">Nom ou adresse IP du serveur FTP</span><span class="sxs-lookup"><span data-stu-id="40a79-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="40a79-2033">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="40a79-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-2034">authenticationType</span></span> |<span data-ttu-id="40a79-2035">Spécification du type d’authentification</span><span class="sxs-lookup"><span data-stu-id="40a79-2035">Specify authentication type</span></span> |<span data-ttu-id="40a79-2036">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2036">Yes</span></span> |<span data-ttu-id="40a79-2037">Basic, anonyme</span><span class="sxs-lookup"><span data-stu-id="40a79-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="40a79-2038">username</span><span class="sxs-lookup"><span data-stu-id="40a79-2038">username</span></span> |<span data-ttu-id="40a79-2039">L’utilisateur ayant accès au serveur FTP</span><span class="sxs-lookup"><span data-stu-id="40a79-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="40a79-2040">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="40a79-2041">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2041">password</span></span> |<span data-ttu-id="40a79-2042">Mot de passe de l’utilisateur (nom d’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="40a79-2042">Password for the user (username)</span></span> |<span data-ttu-id="40a79-2043">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="40a79-2044">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-2044">encryptedCredential</span></span> |<span data-ttu-id="40a79-2045">Informations d’identification chiffrées pour accéder au serveur FTP</span><span class="sxs-lookup"><span data-stu-id="40a79-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="40a79-2046">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="40a79-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-2047">gatewayName</span></span> |<span data-ttu-id="40a79-2048">Nom de la passerelle de gestion des données pour se connecter à un serveur FTP local</span><span class="sxs-lookup"><span data-stu-id="40a79-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="40a79-2049">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="40a79-2050">port</span><span class="sxs-lookup"><span data-stu-id="40a79-2050">port</span></span> |<span data-ttu-id="40a79-2051">Port sur lequel le serveur FTP écoute</span><span class="sxs-lookup"><span data-stu-id="40a79-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="40a79-2052">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2052">No</span></span> |<span data-ttu-id="40a79-2053">21</span><span class="sxs-lookup"><span data-stu-id="40a79-2053">21</span></span> |
| <span data-ttu-id="40a79-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="40a79-2054">enableSsl</span></span> |<span data-ttu-id="40a79-2055">Indiquez si vous souhaitez utiliser FTP sur un canal SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="40a79-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="40a79-2056">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2056">No</span></span> |<span data-ttu-id="40a79-2057">true</span><span class="sxs-lookup"><span data-stu-id="40a79-2057">true</span></span> |
| <span data-ttu-id="40a79-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="40a79-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="40a79-2059">Spécifiez si vous souhaitez activer validation des certificats SSL lors de l’utilisation de FTP sur un canal SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="40a79-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="40a79-2060">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2060">No</span></span> |<span data-ttu-id="40a79-2061">true</span><span class="sxs-lookup"><span data-stu-id="40a79-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="40a79-2062">Exemple : utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="40a79-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="40a79-2063">Exemple : utilisation d’un nom d’utilisateur et d’un mot de passe en texte brut pour l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="40a79-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="40a79-2064">Exemple : utilisation de port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="40a79-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="40a79-2065">Exemple : utilisation d’encryptedCredential pour l’authentification et la passerelle</span><span class="sxs-lookup"><span data-stu-id="40a79-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="40a79-2066">Pour plus d’informations, consultez l’article [FTP connector (connecteur FTP)](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-2067">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-2067">Dataset</span></span>
<span data-ttu-id="40a79-2068">Pour définir un jeu de données FTP, définissez le **type** du jeu de données sur **FileShare** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-2069">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2069">Property</span></span> | <span data-ttu-id="40a79-2070">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2070">Description</span></span> | <span data-ttu-id="40a79-2071">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="40a79-2072">folderPath</span></span> |<span data-ttu-id="40a79-2073">Sous-chemin du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2073">Sub path to the folder.</span></span> <span data-ttu-id="40a79-2074">Utilisez le caractère d’échappement « \ » pour les caractères spéciaux contenus dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="40a79-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="40a79-2075">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="40a79-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="40a79-2076">Vous pouvez également effectuer une combinaison avec la propriété **partitionBy** pour que les chemins d’accès de dossier soient basés sur les dates et heures de démarrage et d’arrêt de la tranche.</span><span class="sxs-lookup"><span data-stu-id="40a79-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="40a79-2077">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2077">Yes</span></span> 
| <span data-ttu-id="40a79-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="40a79-2078">fileName</span></span> |<span data-ttu-id="40a79-2079">Spécifiez le nom du fichier dans l’élément **folderPath** si vous souhaitez que la table se réfère à un fichier spécifique du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="40a79-2080">Si vous ne spécifiez aucune valeur pour cette propriété, le tableau pointe vers tous les fichiers du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="40a79-2081">Lorsque fileName n’est pas spécifié pour un jeu de données de sortie, le nom du fichier généré aura ce format dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="40a79-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="40a79-2082">Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="40a79-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40a79-2083">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2083">No</span></span> |
| <span data-ttu-id="40a79-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="40a79-2084">fileFilter</span></span> |<span data-ttu-id="40a79-2085">Spécifiez un filtre à utiliser pour sélectionner un sous-ensemble de fichiers dans le folderPath plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="40a79-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="40a79-2086">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="40a79-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="40a79-2087">Exemple 1 : `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="40a79-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="40a79-2088">Exemple 2 : `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="40a79-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="40a79-2089">fileFilter s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="40a79-2090">Cette propriété n’est pas prise en charge avec HDFS.</span><span class="sxs-lookup"><span data-stu-id="40a79-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="40a79-2091">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2091">No</span></span> |
| <span data-ttu-id="40a79-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40a79-2092">partitionedBy</span></span> |<span data-ttu-id="40a79-2093">partitionedBy peut être utilisé pour spécifier un folderPath dynamique, fileName pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="40a79-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="40a79-2094">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="40a79-2095">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2095">No</span></span> |
| <span data-ttu-id="40a79-2096">format</span><span class="sxs-lookup"><span data-stu-id="40a79-2096">format</span></span> | <span data-ttu-id="40a79-2097">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40a79-2098">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="40a79-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40a79-2099">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40a79-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40a79-2100">Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40a79-2101">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2101">No</span></span> |
| <span data-ttu-id="40a79-2102">compression</span><span class="sxs-lookup"><span data-stu-id="40a79-2102">compression</span></span> | <span data-ttu-id="40a79-2103">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40a79-2104">Types pris en charge : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Niveaux pris en charge : **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40a79-2105">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40a79-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40a79-2106">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2106">No</span></span> |
| <span data-ttu-id="40a79-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="40a79-2107">useBinaryTransfer</span></span> |<span data-ttu-id="40a79-2108">Spécifiez si vous voulez utiliser le mode de transfert binaire.</span><span class="sxs-lookup"><span data-stu-id="40a79-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="40a79-2109">True pour le mode binaire et false pour ASCII.</span><span class="sxs-lookup"><span data-stu-id="40a79-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="40a79-2110">Valeur par défaut : true.</span><span class="sxs-lookup"><span data-stu-id="40a79-2110">Default value: True.</span></span> <span data-ttu-id="40a79-2111">Cette propriété peut uniquement être utilisée lorsque le type de service lié associé est : FtpServer.</span><span class="sxs-lookup"><span data-stu-id="40a79-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="40a79-2112">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="40a79-2113">fileName et fileFilter ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="40a79-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="40a79-2114">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="40a79-2115">Pour plus d’informations, consultez l’article [FTP connector (connecteur FTP)](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40a79-2116">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="40a79-2117">Si vous copiez des données à partir d’un serveur FTP, définissez le **type de source** de l’activité de copie sur **FileSystemSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-2118">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2118">Property</span></span> | <span data-ttu-id="40a79-2119">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2119">Description</span></span> | <span data-ttu-id="40a79-2120">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-2120">Allowed values</span></span> | <span data-ttu-id="40a79-2121">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2122">recursive</span><span class="sxs-lookup"><span data-stu-id="40a79-2122">recursive</span></span> |<span data-ttu-id="40a79-2123">Indique si les données sont lues de manière récursive dans les sous-dossiers ou uniquement dans le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="40a79-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40a79-2124">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="40a79-2124">True, False (default)</span></span> |<span data-ttu-id="40a79-2125">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2126">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="40a79-2127">Pour plus d’informations, consultez l’article [FTP connector (connecteur FTP)](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="40a79-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="40a79-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-2129">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2129">Linked service</span></span>
<span data-ttu-id="40a79-2130">Pour définir un service lié HDFS, définissez le **type** du service lié sur **Hdfs** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2131">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2131">Property</span></span> | <span data-ttu-id="40a79-2132">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2132">Description</span></span> | <span data-ttu-id="40a79-2133">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2134">type</span><span class="sxs-lookup"><span data-stu-id="40a79-2134">type</span></span> |<span data-ttu-id="40a79-2135">La propriété de type doit être définie sur **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="40a79-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="40a79-2136">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2136">Yes</span></span> |
| <span data-ttu-id="40a79-2137">Url</span><span class="sxs-lookup"><span data-stu-id="40a79-2137">Url</span></span> |<span data-ttu-id="40a79-2138">URL vers le système HDFS</span><span class="sxs-lookup"><span data-stu-id="40a79-2138">URL to the HDFS</span></span> |<span data-ttu-id="40a79-2139">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2139">Yes</span></span> |
| <span data-ttu-id="40a79-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-2140">authenticationType</span></span> |<span data-ttu-id="40a79-2141">Anonyme ou Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="40a79-2142">Pour utiliser l’**authentification Kerberos** pour le connecteur HDFS, reportez-vous à [cette section](#use-kerberos-authentication-for-hdfs-connector) pour configurer votre environnement local en conséquence.</span><span class="sxs-lookup"><span data-stu-id="40a79-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="40a79-2143">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2143">Yes</span></span> |
| <span data-ttu-id="40a79-2144">userName</span><span class="sxs-lookup"><span data-stu-id="40a79-2144">userName</span></span> |<span data-ttu-id="40a79-2145">Nom d’utilisateur de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="40a79-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="40a79-2146">Oui (pour l’authentification Windows)</span><span class="sxs-lookup"><span data-stu-id="40a79-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="40a79-2147">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2147">password</span></span> |<span data-ttu-id="40a79-2148">Mot de passe de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="40a79-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="40a79-2149">Oui (pour l’authentification Windows)</span><span class="sxs-lookup"><span data-stu-id="40a79-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="40a79-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-2150">gatewayName</span></span> |<span data-ttu-id="40a79-2151">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter au système HDFS.</span><span class="sxs-lookup"><span data-stu-id="40a79-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="40a79-2152">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2152">Yes</span></span> |
| <span data-ttu-id="40a79-2153">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-2153">encryptedCredential</span></span> |<span data-ttu-id="40a79-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) des informations d’accès.</span><span class="sxs-lookup"><span data-stu-id="40a79-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="40a79-2155">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="40a79-2156">Exemple : utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="40a79-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="40a79-2157">Exemple : utilisation de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="40a79-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="40a79-2158">Pour plus d’informations, consultez l’article [HDFS connector (connecteur HDFS)](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-2159">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-2159">Dataset</span></span>
<span data-ttu-id="40a79-2160">Pour définir un jeu de données HDFS, définissez le **type** du jeu de données sur **FileShare** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-2161">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2161">Property</span></span> | <span data-ttu-id="40a79-2162">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2162">Description</span></span> | <span data-ttu-id="40a79-2163">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="40a79-2164">folderPath</span></span> |<span data-ttu-id="40a79-2165">Chemin d'accès au dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2165">Path to the folder.</span></span> <span data-ttu-id="40a79-2166">Exemple : `myfolder`</span><span class="sxs-lookup"><span data-stu-id="40a79-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="40a79-2167">Utilisez le caractère d’échappement « \ » pour les caractères spéciaux contenus dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="40a79-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="40a79-2168">Par exemple : pour dossier\sous-dossier, spécifiez dossier\\\\sous-dossier et pour d:\dossier d’exemple, spécifiez d:\\\\dossier d’exemple.</span><span class="sxs-lookup"><span data-stu-id="40a79-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="40a79-2169">Vous pouvez également effectuer une combinaison avec la propriété **partitionBy** pour que les chemins d’accès de dossier soient basés sur les dates et heures de démarrage et d’arrêt de la tranche.</span><span class="sxs-lookup"><span data-stu-id="40a79-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="40a79-2170">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2170">Yes</span></span> |
| <span data-ttu-id="40a79-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="40a79-2171">fileName</span></span> |<span data-ttu-id="40a79-2172">Spécifiez le nom du fichier dans l’élément **folderPath** si vous souhaitez que la table se réfère à un fichier spécifique du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="40a79-2173">Si vous ne spécifiez aucune valeur pour cette propriété, le tableau pointe vers tous les fichiers du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="40a79-2174">Lorsque fileName n’est pas spécifié pour un jeu de données de sortie, le nom du fichier généré aura ce format dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="40a79-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="40a79-2175">Data<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="40a79-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40a79-2176">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2176">No</span></span> |
| <span data-ttu-id="40a79-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40a79-2177">partitionedBy</span></span> |<span data-ttu-id="40a79-2178">partitionedBy peut être utilisé pour spécifier un folderPath dynamique, fileName pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="40a79-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="40a79-2179">Exemple : folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="40a79-2180">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2180">No</span></span> |
| <span data-ttu-id="40a79-2181">format</span><span class="sxs-lookup"><span data-stu-id="40a79-2181">format</span></span> | <span data-ttu-id="40a79-2182">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40a79-2183">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="40a79-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40a79-2184">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40a79-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40a79-2185">Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40a79-2186">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2186">No</span></span> |
| <span data-ttu-id="40a79-2187">compression</span><span class="sxs-lookup"><span data-stu-id="40a79-2187">compression</span></span> | <span data-ttu-id="40a79-2188">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40a79-2189">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40a79-2190">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40a79-2191">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40a79-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40a79-2192">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="40a79-2193">fileName et fileFilter ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="40a79-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="40a79-2194">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="40a79-2195">Pour plus d’informations, consultez l’article [HDFS connector (connecteur HDFS)](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40a79-2196">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="40a79-2197">Si vous copiez des données à partir de HDFS, définissez le **type de source** de l’activité de copie sur **FileSystemSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="40a79-2198">**FileSystemSource** prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="40a79-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="40a79-2199">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2199">Property</span></span> | <span data-ttu-id="40a79-2200">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2200">Description</span></span> | <span data-ttu-id="40a79-2201">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-2201">Allowed values</span></span> | <span data-ttu-id="40a79-2202">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2203">recursive</span><span class="sxs-lookup"><span data-stu-id="40a79-2203">recursive</span></span> |<span data-ttu-id="40a79-2204">Indique si les données sont lues de manière récursive dans les sous-dossiers ou uniquement dans le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="40a79-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40a79-2205">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="40a79-2205">True, False (default)</span></span> |<span data-ttu-id="40a79-2206">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2207">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="40a79-2208">Pour plus d’informations, consultez l’article [HDFS connector (connecteur HDFS)](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="40a79-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="40a79-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="40a79-2210">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2210">Linked service</span></span>
<span data-ttu-id="40a79-2211">Pour définir un service lié SFTP, définissez le **type** du service lié sur **Sftp** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2212">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2212">Property</span></span> | <span data-ttu-id="40a79-2213">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2213">Description</span></span> | <span data-ttu-id="40a79-2214">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2215">host</span><span class="sxs-lookup"><span data-stu-id="40a79-2215">host</span></span> | <span data-ttu-id="40a79-2216">Nom ou adresse IP du serveur SFTP.</span><span class="sxs-lookup"><span data-stu-id="40a79-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="40a79-2217">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2217">Yes</span></span> |
| <span data-ttu-id="40a79-2218">port</span><span class="sxs-lookup"><span data-stu-id="40a79-2218">port</span></span> |<span data-ttu-id="40a79-2219">Port sur lequel le serveur SFTP écoute.</span><span class="sxs-lookup"><span data-stu-id="40a79-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="40a79-2220">La valeur par défaut est 21</span><span class="sxs-lookup"><span data-stu-id="40a79-2220">The default value is: 21</span></span> |<span data-ttu-id="40a79-2221">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2221">No</span></span> |
| <span data-ttu-id="40a79-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-2222">authenticationType</span></span> |<span data-ttu-id="40a79-2223">Spécification du type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="40a79-2223">Specify authentication type.</span></span> <span data-ttu-id="40a79-2224">Valeurs autorisées : **De base** et **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="40a79-2225">Reportez-vous aux sections [Utilisation de l’authentification par clé publique SSH](#using-basic-authentication) et [Utilisation de l’authentification par clé publique SSH](#using-ssh-public-key-authentication) portant respectivement sur des propriétés supplémentaires et des exemples JSON.</span><span class="sxs-lookup"><span data-stu-id="40a79-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="40a79-2226">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2226">Yes</span></span> |
| <span data-ttu-id="40a79-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="40a79-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="40a79-2228">Spécifiez s’il faut ignorer la validation de la clé hôte.</span><span class="sxs-lookup"><span data-stu-id="40a79-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="40a79-2229">Non.</span><span class="sxs-lookup"><span data-stu-id="40a79-2229">No.</span></span> <span data-ttu-id="40a79-2230">valeur par défaut : false</span><span class="sxs-lookup"><span data-stu-id="40a79-2230">The default value: false</span></span> |
| <span data-ttu-id="40a79-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="40a79-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="40a79-2232">Spécifiez l’empreinte de la clé hôte.</span><span class="sxs-lookup"><span data-stu-id="40a79-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="40a79-2233">Oui, si `skipHostKeyValidation` est défini sur false.</span><span class="sxs-lookup"><span data-stu-id="40a79-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="40a79-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-2234">gatewayName</span></span> |<span data-ttu-id="40a79-2235">Nom de la passerelle de gestion des données pour se connecter à un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="40a79-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="40a79-2236">Oui en cas de copie de données à partir d’un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="40a79-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="40a79-2237">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-2237">encryptedCredential</span></span> | <span data-ttu-id="40a79-2238">Informations d’identification chiffrées pour accéder au serveur SFTP.</span><span class="sxs-lookup"><span data-stu-id="40a79-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="40a79-2239">Généré automatiquement lorsque vous spécifiez l’authentification de base (nom d’utilisateur + mot de passe) ou l’authentification SshPublicKey (nom d’utilisateur + chemin d’accès ou contenu de la clé privée) dans l’Assistant de copie ou la boîte de dialogue contextuelle ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="40a79-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="40a79-2240">Non.</span><span class="sxs-lookup"><span data-stu-id="40a79-2240">No.</span></span> <span data-ttu-id="40a79-2241">S’applique uniquement pour la copie de données à partir d’un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="40a79-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="40a79-2242">Exemple : utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="40a79-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="40a79-2243">Pour utiliser l’authentification de base, définissez `authenticationType` sur `Basic` et spécifiez les propriétés suivantes en plus des propriétés génériques du connecteur SFTP présentées dans la dernière section :</span><span class="sxs-lookup"><span data-stu-id="40a79-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="40a79-2244">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2244">Property</span></span> | <span data-ttu-id="40a79-2245">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2245">Description</span></span> | <span data-ttu-id="40a79-2246">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2247">username</span><span class="sxs-lookup"><span data-stu-id="40a79-2247">username</span></span> | <span data-ttu-id="40a79-2248">Utilisateur ayant accès au serveur SFTP.</span><span class="sxs-lookup"><span data-stu-id="40a79-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="40a79-2249">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2249">Yes</span></span> |
| <span data-ttu-id="40a79-2250">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2250">password</span></span> | <span data-ttu-id="40a79-2251">Mot de passe de l’utilisateur (nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="40a79-2251">Password for the user (username).</span></span> | <span data-ttu-id="40a79-2252">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="40a79-2253">Exemple : authentification de base avec des informations d’identification chiffrées**</span><span class="sxs-lookup"><span data-stu-id="40a79-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="40a79-2254">Utilisation de l’authentification par clé publique SSH : **</span><span class="sxs-lookup"><span data-stu-id="40a79-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="40a79-2255">Pour utiliser l’authentification de base, définissez `authenticationType` sur `SshPublicKey` et spécifiez les propriétés suivantes en plus des propriétés génériques du connecteur SFTP présentées dans la dernière section :</span><span class="sxs-lookup"><span data-stu-id="40a79-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="40a79-2256">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2256">Property</span></span> | <span data-ttu-id="40a79-2257">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2257">Description</span></span> | <span data-ttu-id="40a79-2258">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2259">username</span><span class="sxs-lookup"><span data-stu-id="40a79-2259">username</span></span> |<span data-ttu-id="40a79-2260">Utilisateur ayant accès au serveur SFTP</span><span class="sxs-lookup"><span data-stu-id="40a79-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="40a79-2261">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2261">Yes</span></span> |
| <span data-ttu-id="40a79-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="40a79-2262">privateKeyPath</span></span> | <span data-ttu-id="40a79-2263">Spécifiez le chemin absolu au fichier de clé privée auquel la passerelle peut accéder.</span><span class="sxs-lookup"><span data-stu-id="40a79-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="40a79-2264">Spécifiez soit la propriété `privateKeyPath`, soit la propriété `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="40a79-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="40a79-2265">S’applique uniquement pour la copie de données à partir d’un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="40a79-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="40a79-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="40a79-2266">privateKeyContent</span></span> | <span data-ttu-id="40a79-2267">Une chaîne sérialisée du contenu de la clé privée.</span><span class="sxs-lookup"><span data-stu-id="40a79-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="40a79-2268">L’Assistant de copie peut lire le fichier de clé privée et extraire le contenu de clé privée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="40a79-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="40a79-2269">Si vous utilisez tout autre outil/SDK, utilisez plutôt la propriété privateKeyPath.</span><span class="sxs-lookup"><span data-stu-id="40a79-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="40a79-2270">Spécifiez soit la propriété `privateKeyPath`, soit la propriété `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="40a79-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="40a79-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="40a79-2271">passPhrase</span></span> | <span data-ttu-id="40a79-2272">Spécifiez la phrase secrète/le mot de passe pour déchiffrer la clé privée si le fichier de clé est protégé par une phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="40a79-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="40a79-2273">Oui, si le fichier de clé privée est protégé par une phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="40a79-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="40a79-2274">Exemple : authentification SshPublicKey à l’aide du contenu de clé privée**</span><span class="sxs-lookup"><span data-stu-id="40a79-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="40a79-2275">Pour plus d’informations, consultez l’article [SFTP connector (connecteur SFTP)](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-2276">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-2276">Dataset</span></span>
<span data-ttu-id="40a79-2277">Pour définir un jeu de données SFTP, définissez le **type** du jeu de données sur **FileShare** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-2278">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2278">Property</span></span> | <span data-ttu-id="40a79-2279">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2279">Description</span></span> | <span data-ttu-id="40a79-2280">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="40a79-2281">folderPath</span></span> |<span data-ttu-id="40a79-2282">Sous-chemin du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2282">Sub path to the folder.</span></span> <span data-ttu-id="40a79-2283">Utilisez le caractère d’échappement « \ » pour les caractères spéciaux contenus dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="40a79-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="40a79-2284">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="40a79-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="40a79-2285">Vous pouvez également effectuer une combinaison avec la propriété **partitionBy** pour que les chemins d’accès de dossier soient basés sur les dates et heures de démarrage et d’arrêt de la tranche.</span><span class="sxs-lookup"><span data-stu-id="40a79-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="40a79-2286">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2286">Yes</span></span> |
| <span data-ttu-id="40a79-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="40a79-2287">fileName</span></span> |<span data-ttu-id="40a79-2288">Spécifiez le nom du fichier dans l’élément **folderPath** si vous souhaitez que la table se réfère à un fichier spécifique du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="40a79-2289">Si vous ne spécifiez aucune valeur pour cette propriété, le tableau pointe vers tous les fichiers du dossier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="40a79-2290">Lorsque fileName n’est pas spécifié pour un jeu de données de sortie, le nom du fichier généré aura ce format dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="40a79-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="40a79-2291">Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="40a79-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40a79-2292">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2292">No</span></span> |
| <span data-ttu-id="40a79-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="40a79-2293">fileFilter</span></span> |<span data-ttu-id="40a79-2294">Spécifiez un filtre à utiliser pour sélectionner un sous-ensemble de fichiers dans le folderPath plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="40a79-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="40a79-2295">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="40a79-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="40a79-2296">Exemple 1 : `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="40a79-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="40a79-2297">Exemple 2 : `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="40a79-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="40a79-2298">fileFilter s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="40a79-2299">Cette propriété n’est pas prise en charge avec HDFS.</span><span class="sxs-lookup"><span data-stu-id="40a79-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="40a79-2300">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2300">No</span></span> |
| <span data-ttu-id="40a79-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40a79-2301">partitionedBy</span></span> |<span data-ttu-id="40a79-2302">partitionedBy peut être utilisé pour spécifier un folderPath dynamique, fileName pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="40a79-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="40a79-2303">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="40a79-2304">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2304">No</span></span> |
| <span data-ttu-id="40a79-2305">format</span><span class="sxs-lookup"><span data-stu-id="40a79-2305">format</span></span> | <span data-ttu-id="40a79-2306">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40a79-2307">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="40a79-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40a79-2308">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40a79-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40a79-2309">Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40a79-2310">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2310">No</span></span> |
| <span data-ttu-id="40a79-2311">compression</span><span class="sxs-lookup"><span data-stu-id="40a79-2311">compression</span></span> | <span data-ttu-id="40a79-2312">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40a79-2313">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40a79-2314">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40a79-2315">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40a79-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40a79-2316">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2316">No</span></span> |
| <span data-ttu-id="40a79-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="40a79-2317">useBinaryTransfer</span></span> |<span data-ttu-id="40a79-2318">Spécifiez si vous voulez utiliser le mode de transfert binaire.</span><span class="sxs-lookup"><span data-stu-id="40a79-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="40a79-2319">True pour le mode binaire et false pour ASCII.</span><span class="sxs-lookup"><span data-stu-id="40a79-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="40a79-2320">Valeur par défaut : true.</span><span class="sxs-lookup"><span data-stu-id="40a79-2320">Default value: True.</span></span> <span data-ttu-id="40a79-2321">Cette propriété peut uniquement être utilisée lorsque le type de service lié associé est : FtpServer.</span><span class="sxs-lookup"><span data-stu-id="40a79-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="40a79-2322">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="40a79-2323">fileName et fileFilter ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="40a79-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="40a79-2324">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="40a79-2325">Pour plus d’informations, consultez l’article [SFTP connector (connecteur SFTP)](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40a79-2326">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="40a79-2327">Si vous copiez des données à partir d’une source SFTP, définissez le **type de source** de l’activité de copie sur **FileSystemSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-2328">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2328">Property</span></span> | <span data-ttu-id="40a79-2329">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2329">Description</span></span> | <span data-ttu-id="40a79-2330">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-2330">Allowed values</span></span> | <span data-ttu-id="40a79-2331">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2332">recursive</span><span class="sxs-lookup"><span data-stu-id="40a79-2332">recursive</span></span> |<span data-ttu-id="40a79-2333">Indique si les données sont lues de manière récursive dans les sous-dossiers ou uniquement dans le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="40a79-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40a79-2334">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="40a79-2334">True, False (default)</span></span> |<span data-ttu-id="40a79-2335">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="40a79-2336">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="40a79-2337">Pour plus d’informations, consultez l’article [SFTP connector (connecteur SFTP)](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="40a79-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="40a79-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-2339">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2339">Linked service</span></span>
<span data-ttu-id="40a79-2340">Pour définir un service lié HTTP, définissez le **type** du service lié sur **Http** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2341">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2341">Property</span></span> | <span data-ttu-id="40a79-2342">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2342">Description</span></span> | <span data-ttu-id="40a79-2343">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2344">url</span><span class="sxs-lookup"><span data-stu-id="40a79-2344">url</span></span> | <span data-ttu-id="40a79-2345">URL de base du serveur web</span><span class="sxs-lookup"><span data-stu-id="40a79-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="40a79-2346">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2346">Yes</span></span> |
| <span data-ttu-id="40a79-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-2347">authenticationType</span></span> | <span data-ttu-id="40a79-2348">Spécifie le type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="40a79-2348">Specifies the authentication type.</span></span> <span data-ttu-id="40a79-2349">Les valeurs autorisées sont : **Anonymous** (Anonyme), **Basic** (De base), **Digest**, **Windows**, **ClientCertificate** (Certificat client).</span><span class="sxs-lookup"><span data-stu-id="40a79-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="40a79-2350">Reportez-vous aux sections suivant ce tableau pour accéder à d’autres propriétés et à des exemples JSON sur ces types d’authentification.</span><span class="sxs-lookup"><span data-stu-id="40a79-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="40a79-2351">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2351">Yes</span></span> |
| <span data-ttu-id="40a79-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="40a79-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="40a79-2353">Indiquez si la validation des certificats SSL doit être activée lorsque la source est un serveur web HTTPS.</span><span class="sxs-lookup"><span data-stu-id="40a79-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="40a79-2354">Non, la valeur par défaut est True.</span><span class="sxs-lookup"><span data-stu-id="40a79-2354">No, default is true</span></span> |
| <span data-ttu-id="40a79-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-2355">gatewayName</span></span> | <span data-ttu-id="40a79-2356">Nom de la passerelle de gestion des données pour se connecter à une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="40a79-2357">Oui en cas de copie de données à partir d’une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="40a79-2358">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40a79-2358">encryptedCredential</span></span> | <span data-ttu-id="40a79-2359">Informations d’identification chiffrées pour accéder au point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="40a79-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="40a79-2360">Elles sont générées automatiquement lorsque vous configurez les informations d’authentification dans l’Assistant de copie ou la boîte de dialogue contextuelle ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="40a79-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="40a79-2361">Non.</span><span class="sxs-lookup"><span data-stu-id="40a79-2361">No.</span></span> <span data-ttu-id="40a79-2362">S’applique uniquement pour la copie de données à partir d’un serveur HTTP local.</span><span class="sxs-lookup"><span data-stu-id="40a79-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="40a79-2363">Exemple : utilisation de l’authentification Basic (De base), Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="40a79-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="40a79-2364">Définissez `authenticationType` sur `Basic`, `Digest` ou `Windows` et spécifiez les propriétés suivantes en plus des propriétés génériques du connecteur HTTP présentées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="40a79-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="40a79-2365">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2365">Property</span></span> | <span data-ttu-id="40a79-2366">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2366">Description</span></span> | <span data-ttu-id="40a79-2367">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2368">username</span><span class="sxs-lookup"><span data-stu-id="40a79-2368">username</span></span> | <span data-ttu-id="40a79-2369">Nom d’utilisateur pour accéder au point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="40a79-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="40a79-2370">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2370">Yes</span></span> |
| <span data-ttu-id="40a79-2371">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2371">password</span></span> | <span data-ttu-id="40a79-2372">Mot de passe de l’utilisateur (nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="40a79-2372">Password for the user (username).</span></span> | <span data-ttu-id="40a79-2373">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="40a79-2374">Exemple : utilisation de l’authentification ClientCertificate (Certificat client)</span><span class="sxs-lookup"><span data-stu-id="40a79-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="40a79-2375">Pour utiliser l’authentification de base, définissez `authenticationType` sur `ClientCertificate` et spécifiez les propriétés suivantes en plus des propriétés génériques du connecteur HTTP présentées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="40a79-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="40a79-2376">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2376">Property</span></span> | <span data-ttu-id="40a79-2377">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2377">Description</span></span> | <span data-ttu-id="40a79-2378">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="40a79-2379">embeddedCertData</span></span> | <span data-ttu-id="40a79-2380">Contenu codé en Base64 des données binaires du fichier Personal Information Exchange (PFX).</span><span class="sxs-lookup"><span data-stu-id="40a79-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="40a79-2381">Spécifiez soit la propriété `embeddedCertData`, soit la propriété `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="40a79-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="40a79-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="40a79-2382">certThumbprint</span></span> | <span data-ttu-id="40a79-2383">Empreinte du certificat qui a été installé dans le magasin de certificats de votre ordinateur de passerelle.</span><span class="sxs-lookup"><span data-stu-id="40a79-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="40a79-2384">S’applique uniquement pour la copie de données à partir d’une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="40a79-2385">Spécifiez soit la propriété `embeddedCertData`, soit la propriété `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="40a79-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="40a79-2386">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2386">password</span></span> | <span data-ttu-id="40a79-2387">Mot de passe associé au certificat.</span><span class="sxs-lookup"><span data-stu-id="40a79-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="40a79-2388">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2388">No</span></span> |

<span data-ttu-id="40a79-2389">Si vous utilisez `certThumbprint` pour l’authentification et le certificat est installé dans le magasin personnel de l’ordinateur local, vous devez accorder l’autorisation de lecture au service de passerelle :</span><span class="sxs-lookup"><span data-stu-id="40a79-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="40a79-2390">Lancez Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="40a79-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="40a79-2391">Ajouter le composant logiciel enfichable **Certificats**ciblant l’**ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="40a79-2392">Développez **Certificats**, **Personnel**, puis cliquez sur **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="40a79-2393">Cliquez avec le bouton droit sur le certificat du magasin personnel, puis sélectionnez **Toutes les tâches**->**Gérer les clés privées...**</span><span class="sxs-lookup"><span data-stu-id="40a79-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="40a79-2394">Dans l’onglet **Sécurité**, ajoutez le compte d’utilisateur sous lequel le service hôte de la passerelle de gestion des données s’exécute avec l’accès en lecture au certificat.</span><span class="sxs-lookup"><span data-stu-id="40a79-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="40a79-2395">**Exemple : utilisation d’un certificat client :** ce service lié lie votre fabrique de données à un serveur web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="40a79-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="40a79-2396">Il utilise un certificat client installé sur l’ordinateur doté de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="40a79-2397">Exemple : utilisation d’un certificat client dans un fichier</span><span class="sxs-lookup"><span data-stu-id="40a79-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="40a79-2398">Ce service lié lie votre fabrique de données à un serveur web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="40a79-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="40a79-2399">Il utilise un fichier de certificat client sur l’ordinateur doté de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="40a79-2400">Pour plus d’informations, consultez l’article [HTTP connector (connecteur HTTP)](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-2401">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-2401">Dataset</span></span>
<span data-ttu-id="40a79-2402">Pour définir un jeu de données HTTP, définissez le **type** du jeu de données sur **Http** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-2403">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2403">Property</span></span> | <span data-ttu-id="40a79-2404">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2404">Description</span></span> | <span data-ttu-id="40a79-2405">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="40a79-2406">relativeUrl</span></span> | <span data-ttu-id="40a79-2407">URL relative de la ressource qui contient les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="40a79-2408">Quand le chemin d’accès n’est pas spécifié, seule l’URL spécifiée dans la définition du service lié est utilisée.</span><span class="sxs-lookup"><span data-stu-id="40a79-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="40a79-2409">Pour construire une URL dynamique, vous pouvez utiliser [les variables système et les fonctions de Data Factory](data-factory-functions-variables.md), par exemple : `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="40a79-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="40a79-2410">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2410">No</span></span> |
| <span data-ttu-id="40a79-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="40a79-2411">requestMethod</span></span> | <span data-ttu-id="40a79-2412">Méthode HTTP.</span><span class="sxs-lookup"><span data-stu-id="40a79-2412">Http method.</span></span> <span data-ttu-id="40a79-2413">Les valeurs autorisées sont **GET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="40a79-2414">Non.</span><span class="sxs-lookup"><span data-stu-id="40a79-2414">No.</span></span> <span data-ttu-id="40a79-2415">La valeur par défaut est `GET`.</span><span class="sxs-lookup"><span data-stu-id="40a79-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="40a79-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="40a79-2416">additionalHeaders</span></span> | <span data-ttu-id="40a79-2417">En-têtes de requête HTTP supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="40a79-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="40a79-2418">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2418">No</span></span> |
| <span data-ttu-id="40a79-2419">RequestBody</span><span class="sxs-lookup"><span data-stu-id="40a79-2419">requestBody</span></span> | <span data-ttu-id="40a79-2420">Corps de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="40a79-2420">Body for HTTP request.</span></span> | <span data-ttu-id="40a79-2421">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2421">No</span></span> |
| <span data-ttu-id="40a79-2422">format</span><span class="sxs-lookup"><span data-stu-id="40a79-2422">format</span></span> | <span data-ttu-id="40a79-2423">Si vous souhaitez simplement **récupérer les données du point de terminaison HTTP en l’état**, sans les analyser, ignorez ces paramètres de format.</span><span class="sxs-lookup"><span data-stu-id="40a79-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="40a79-2424">Si vous souhaitez analyser le contenu de la réponse HTTP pendant la copie, les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40a79-2425">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40a79-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="40a79-2426">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2426">No</span></span> |
| <span data-ttu-id="40a79-2427">compression</span><span class="sxs-lookup"><span data-stu-id="40a79-2427">compression</span></span> | <span data-ttu-id="40a79-2428">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40a79-2429">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40a79-2430">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40a79-2431">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40a79-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40a79-2432">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="40a79-2433">Exemple : utilisation de la méthode GET (par défaut)</span><span class="sxs-lookup"><span data-stu-id="40a79-2433">Example: using the GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-the-post-method"></a><span data-ttu-id="40a79-2434">Exemple : utilisation de la méthode POST</span><span class="sxs-lookup"><span data-stu-id="40a79-2434">Example: using the POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="40a79-2435">Pour plus d’informations, consultez l’article [HTTP connector (connecteur HTTP)](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="40a79-2436">Source HTTP dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="40a79-2437">Si vous copiez des données à partir d’une source HTTP, définissez le **type de source** de l’activité de copie sur **HttpSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-2438">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2438">Property</span></span> | <span data-ttu-id="40a79-2439">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2439">Description</span></span> | <span data-ttu-id="40a79-2440">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="40a79-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="40a79-2441">httpRequestTimeout</span></span> | <span data-ttu-id="40a79-2442">Délai d’expiration (TimeSpan) pour l’obtention d’une réponse par la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="40a79-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="40a79-2443">Il s’agit du délai d’expiration pour l’obtention d’une réponse, et non du délai d’expiration pour la lecture des données de la réponse.</span><span class="sxs-lookup"><span data-stu-id="40a79-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="40a79-2444">Non.</span><span class="sxs-lookup"><span data-stu-id="40a79-2444">No.</span></span> <span data-ttu-id="40a79-2445">Valeur par défaut : 00:01:40</span><span class="sxs-lookup"><span data-stu-id="40a79-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="40a79-2446">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-2447">Pour plus d’informations, consultez l’article [HTTP connector (connecteur HTTP)](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="40a79-2448">OData</span><span class="sxs-lookup"><span data-stu-id="40a79-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-2449">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2449">Linked service</span></span>
<span data-ttu-id="40a79-2450">Pour définir un service lié OData, définissez le **type** du service lié sur **OData** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2451">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2451">Property</span></span> | <span data-ttu-id="40a79-2452">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2452">Description</span></span> | <span data-ttu-id="40a79-2453">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2454">url</span><span class="sxs-lookup"><span data-stu-id="40a79-2454">url</span></span> |<span data-ttu-id="40a79-2455">URL du service OData.</span><span class="sxs-lookup"><span data-stu-id="40a79-2455">Url of the OData service.</span></span> |<span data-ttu-id="40a79-2456">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2456">Yes</span></span> |
| <span data-ttu-id="40a79-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-2457">authenticationType</span></span> |<span data-ttu-id="40a79-2458">Type d’authentification utilisé pour se connecter à la source OData.</span><span class="sxs-lookup"><span data-stu-id="40a79-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="40a79-2459">Pour OData dans le cloud, les valeurs possibles sont Anonyme, De base et OAuth (notez qu’à l’heure actuelle, Azure Data Factory prend en charge uniquement l’authentification OAuth basée sur Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="40a79-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="40a79-2460">Pour OData en local, les valeurs possibles sont Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40a79-2461">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2461">Yes</span></span> |
| <span data-ttu-id="40a79-2462">username</span><span class="sxs-lookup"><span data-stu-id="40a79-2462">username</span></span> |<span data-ttu-id="40a79-2463">Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="40a79-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="40a79-2464">Oui (uniquement si vous utilisez l’authentification de base)</span><span class="sxs-lookup"><span data-stu-id="40a79-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="40a79-2465">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2465">password</span></span> |<span data-ttu-id="40a79-2466">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40a79-2467">Oui (uniquement si vous utilisez l’authentification de base)</span><span class="sxs-lookup"><span data-stu-id="40a79-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="40a79-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="40a79-2468">authorizedCredential</span></span> |<span data-ttu-id="40a79-2469">Si vous utilisez OAuth, cliquez sur le bouton **Autoriser** de l’Assistant de copie Data Factory ou de l’éditeur et entrez vos informations d’identification. La valeur de cette propriété sera alors générée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="40a79-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="40a79-2470">Oui (uniquement si vous utilisez l’authentification OAuth)</span><span class="sxs-lookup"><span data-stu-id="40a79-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="40a79-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-2471">gatewayName</span></span> |<span data-ttu-id="40a79-2472">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter au service OData local.</span><span class="sxs-lookup"><span data-stu-id="40a79-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="40a79-2473">Indiquez uniquement si vous copiez des données à partir de la source OData locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="40a79-2474">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="40a79-2475">Exemple : utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="40a79-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="40a79-2476">Exemple : utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="40a79-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="40a79-2477">Exemple : utilisation de l’authentification Windows pour accéder à la source OData locale</span><span class="sxs-lookup"><span data-stu-id="40a79-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="40a79-2478">Exemple : utilisation de l’authentification OAuth pour accéder à la source OData dans le cloud</span><span class="sxs-lookup"><span data-stu-id="40a79-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="40a79-2479">Pour plus d’informations, consultez l’article [OData connector (connecteur OData)](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40a79-2480">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-2480">Dataset</span></span>
<span data-ttu-id="40a79-2481">Pour définir un jeu de données OData, définissez le **type** du jeu de données sur **ODataResource** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-2482">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2482">Property</span></span> | <span data-ttu-id="40a79-2483">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2483">Description</span></span> | <span data-ttu-id="40a79-2484">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2485">chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="40a79-2485">path</span></span> |<span data-ttu-id="40a79-2486">Chemin d'accès à la ressource OData</span><span class="sxs-lookup"><span data-stu-id="40a79-2486">Path to the OData resource</span></span> |<span data-ttu-id="40a79-2487">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2488">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="40a79-2489">Pour plus d’informations, consultez l’article [OData connector (connecteur OData)](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-2490">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-2491">Si vous copiez des données à partir d’une source OData, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-2492">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2492">Property</span></span> | <span data-ttu-id="40a79-2493">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2493">Description</span></span> | <span data-ttu-id="40a79-2494">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2494">Example</span></span> | <span data-ttu-id="40a79-2495">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2496">query</span><span class="sxs-lookup"><span data-stu-id="40a79-2496">query</span></span> |<span data-ttu-id="40a79-2497">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="40a79-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="40a79-2499">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2500">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="40a79-2501">Pour plus d’informations, consultez l’article [OData connector (connecteur OData)](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="40a79-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="40a79-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="40a79-2503">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2503">Linked service</span></span>
<span data-ttu-id="40a79-2504">Pour définir un service lié ODBC, définissez le **type** du service lié sur **OnPremisesOdbc** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2505">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2505">Property</span></span> | <span data-ttu-id="40a79-2506">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2506">Description</span></span> | <span data-ttu-id="40a79-2507">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-2508">connectionString</span></span> |<span data-ttu-id="40a79-2509">Partie de la chaîne de connexion ne contenant pas les informations d’accès, avec des informations d’identification chiffrées facultatives.</span><span class="sxs-lookup"><span data-stu-id="40a79-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="40a79-2510">Consultez les exemples dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="40a79-2510">See examples in the following sections.</span></span> |<span data-ttu-id="40a79-2511">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2511">Yes</span></span> |
| <span data-ttu-id="40a79-2512">credential</span><span class="sxs-lookup"><span data-stu-id="40a79-2512">credential</span></span> |<span data-ttu-id="40a79-2513">Partie de la chaîne de connexion contenant les informations d’accès, spécifiée dans un format de valeurs de propriété spécifique au pilote.</span><span class="sxs-lookup"><span data-stu-id="40a79-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="40a79-2514">Exemple : « Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>; ».</span><span class="sxs-lookup"><span data-stu-id="40a79-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="40a79-2515">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2515">No</span></span> |
| <span data-ttu-id="40a79-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-2516">authenticationType</span></span> |<span data-ttu-id="40a79-2517">Type d’authentification utilisé pour se connecter au magasin de données ODBC.</span><span class="sxs-lookup"><span data-stu-id="40a79-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="40a79-2518">Les valeurs possibles sont : Anonyme et De base.</span><span class="sxs-lookup"><span data-stu-id="40a79-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="40a79-2519">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2519">Yes</span></span> |
| <span data-ttu-id="40a79-2520">username</span><span class="sxs-lookup"><span data-stu-id="40a79-2520">username</span></span> |<span data-ttu-id="40a79-2521">Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="40a79-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="40a79-2522">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2522">No</span></span> |
| <span data-ttu-id="40a79-2523">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2523">password</span></span> |<span data-ttu-id="40a79-2524">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40a79-2525">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2525">No</span></span> |
| <span data-ttu-id="40a79-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-2526">gatewayName</span></span> |<span data-ttu-id="40a79-2527">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter au magasin de données ODBC.</span><span class="sxs-lookup"><span data-stu-id="40a79-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="40a79-2528">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="40a79-2529">Exemple : utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="40a79-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="40a79-2530">Exemple : utilisation de l’authentification de base avec des informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="40a79-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="40a79-2531">Vous pouvez chiffrer les informations d’identification à l’aide de l’applet de commande [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (version 1.0 d’Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (version 0.9 ou antérieure d’Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="40a79-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="40a79-2532">Exemple : utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="40a79-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="40a79-2533">Pour plus d’informations, consultez l’article [ODBC connector (connecteur ODBC)](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-2534">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-2534">Dataset</span></span>
<span data-ttu-id="40a79-2535">Pour définir un jeu de données ODBC, définissez le **type** du jeu de données sur **RelationalTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-2536">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2536">Property</span></span> | <span data-ttu-id="40a79-2537">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2537">Description</span></span> | <span data-ttu-id="40a79-2538">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2539">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-2539">tableName</span></span> |<span data-ttu-id="40a79-2540">Nom de la table dans le magasin de données ODBC.</span><span class="sxs-lookup"><span data-stu-id="40a79-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="40a79-2541">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="40a79-2542">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-2543">Pour plus d’informations, consultez l’article [ODBC connector (connecteur ODBC)](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-2544">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-2545">Si vous copiez des données à partir d’un magasin de données ODBC, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-2546">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2546">Property</span></span> | <span data-ttu-id="40a79-2547">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2547">Description</span></span> | <span data-ttu-id="40a79-2548">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-2548">Allowed values</span></span> | <span data-ttu-id="40a79-2549">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2550">query</span><span class="sxs-lookup"><span data-stu-id="40a79-2550">query</span></span> |<span data-ttu-id="40a79-2551">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-2552">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-2552">SQL query string.</span></span> <span data-ttu-id="40a79-2553">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40a79-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40a79-2554">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2555">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="40a79-2556">Pour plus d’informations, consultez l’article [ODBC connector (connecteur ODBC)](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="40a79-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="40a79-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="40a79-2558">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2558">Linked service</span></span>
<span data-ttu-id="40a79-2559">Pour définir un service lié Salesforce, définissez le **type** du service lié sur **Salesforce** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2560">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2560">Property</span></span> | <span data-ttu-id="40a79-2561">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2561">Description</span></span> | <span data-ttu-id="40a79-2562">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="40a79-2563">environmentUrl</span></span> | <span data-ttu-id="40a79-2564">Spécifiez l’URL de l’instance Salesforce.</span><span class="sxs-lookup"><span data-stu-id="40a79-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="40a79-2565">- L’URL par défaut est « https://login.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="40a79-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="40a79-2566">- Pour copier des données à partir du bac à sable (sandbox), spécifiez « https://test.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="40a79-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="40a79-2567">- Pour copier des données du domaine personnalisé, spécifiez, par exemple : « https://[domain].my.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="40a79-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="40a79-2568">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2568">No</span></span> |
| <span data-ttu-id="40a79-2569">username</span><span class="sxs-lookup"><span data-stu-id="40a79-2569">username</span></span> |<span data-ttu-id="40a79-2570">Spécifiez un nom d’utilisateur pour le compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="40a79-2571">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2571">Yes</span></span> |
| <span data-ttu-id="40a79-2572">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2572">password</span></span> |<span data-ttu-id="40a79-2573">Spécifiez le mot de passe du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="40a79-2574">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2574">Yes</span></span> |
| <span data-ttu-id="40a79-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="40a79-2575">securityToken</span></span> |<span data-ttu-id="40a79-2576">Spécifiez le jeton de sécurité du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="40a79-2577">Consultez l’article [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Obtenir un jeton de sécurité) pour obtenir des instructions sur la réinitialisation et l’obtention d’un jeton de sécurité.</span><span class="sxs-lookup"><span data-stu-id="40a79-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="40a79-2578">Pour en savoir plus sur les jetons de sécurité, consultez l’article [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)(Sécurité et API).</span><span class="sxs-lookup"><span data-stu-id="40a79-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="40a79-2579">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2580">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="40a79-2581">Pour plus d’informations, consultez l’article [Salesforce connector (connecteur Salesforce)](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-2582">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-2582">Dataset</span></span>
<span data-ttu-id="40a79-2583">Pour définir un jeu de données Salesforce, définissez le **type** du jeu de données sur **RelationalTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-2584">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2584">Property</span></span> | <span data-ttu-id="40a79-2585">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2585">Description</span></span> | <span data-ttu-id="40a79-2586">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2587">TableName</span><span class="sxs-lookup"><span data-stu-id="40a79-2587">tableName</span></span> |<span data-ttu-id="40a79-2588">Nom de la table dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="40a79-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="40a79-2589">Non (si une **requête** de type **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="40a79-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2590">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="40a79-2591">Pour plus d’informations, consultez l’article [Salesforce connector (connecteur Salesforce)](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40a79-2592">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40a79-2593">Si vous copiez des données à partir de Salesforce, définissez le **type de source** de l’activité de copie sur **RelationalSource** et spécifiez les propriétés suivantes dans la section **source** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40a79-2594">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2594">Property</span></span> | <span data-ttu-id="40a79-2595">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2595">Description</span></span> | <span data-ttu-id="40a79-2596">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="40a79-2596">Allowed values</span></span> | <span data-ttu-id="40a79-2597">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40a79-2598">query</span><span class="sxs-lookup"><span data-stu-id="40a79-2598">query</span></span> |<span data-ttu-id="40a79-2599">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="40a79-2600">Une requête SQL-92 ou une requête [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="40a79-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="40a79-2601">Par exemple : `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="40a79-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="40a79-2602">Non (si l’attribut **tableName** de l’élément **dataset** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="40a79-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2603">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="40a79-2604">La partie « __c » du nom de l’API est requise pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="40a79-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="40a79-2605">Pour plus d’informations, consultez l’article [Salesforce connector (connecteur Salesforce)](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="40a79-2606">Données Web</span><span class="sxs-lookup"><span data-stu-id="40a79-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40a79-2607">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2607">Linked service</span></span>
<span data-ttu-id="40a79-2608">Pour définir un service lié Web, définissez le **type** du service lié sur **Web** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2609">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2609">Property</span></span> | <span data-ttu-id="40a79-2610">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2610">Description</span></span> | <span data-ttu-id="40a79-2611">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2612">Url</span><span class="sxs-lookup"><span data-stu-id="40a79-2612">Url</span></span> |<span data-ttu-id="40a79-2613">URL de la source web</span><span class="sxs-lookup"><span data-stu-id="40a79-2613">URL to the Web source</span></span> |<span data-ttu-id="40a79-2614">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2614">Yes</span></span> |
| <span data-ttu-id="40a79-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40a79-2615">authenticationType</span></span> |<span data-ttu-id="40a79-2616">Anonyme</span><span class="sxs-lookup"><span data-stu-id="40a79-2616">Anonymous.</span></span> |<span data-ttu-id="40a79-2617">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="40a79-2618">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="40a79-2619">Pour plus d’informations, consultez l’article [Web Table connector (connecteur table web)](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40a79-2620">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="40a79-2620">Dataset</span></span>
<span data-ttu-id="40a79-2621">Pour définir un jeu de données Web, définissez le **type** du jeu de données sur **WebTable** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40a79-2622">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2622">Property</span></span> | <span data-ttu-id="40a79-2623">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2623">Description</span></span> | <span data-ttu-id="40a79-2624">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-2625">type</span><span class="sxs-lookup"><span data-stu-id="40a79-2625">type</span></span> |<span data-ttu-id="40a79-2626">Type du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2626">type of the dataset.</span></span> <span data-ttu-id="40a79-2627">Doit avoir la valeur **WebTable**</span><span class="sxs-lookup"><span data-stu-id="40a79-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="40a79-2628">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2628">Yes</span></span> |
| <span data-ttu-id="40a79-2629">path</span><span class="sxs-lookup"><span data-stu-id="40a79-2629">path</span></span> |<span data-ttu-id="40a79-2630">URL relative de la ressource qui contient la table.</span><span class="sxs-lookup"><span data-stu-id="40a79-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="40a79-2631">Non.</span><span class="sxs-lookup"><span data-stu-id="40a79-2631">No.</span></span> <span data-ttu-id="40a79-2632">Quand le chemin d’accès n’est pas spécifié, seule l’URL spécifiée dans la définition du service lié est utilisée.</span><span class="sxs-lookup"><span data-stu-id="40a79-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="40a79-2633">index</span><span class="sxs-lookup"><span data-stu-id="40a79-2633">index</span></span> |<span data-ttu-id="40a79-2634">Index de la table dans la ressource.</span><span class="sxs-lookup"><span data-stu-id="40a79-2634">The index of the table in the resource.</span></span> <span data-ttu-id="40a79-2635">Pour savoir comment obtenir l’index d’une table dans une page HTML, consultez la section [Obtenir l’index d’une table dans une page HTML](#get-index-of-a-table-in-an-html-page) .</span><span class="sxs-lookup"><span data-stu-id="40a79-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="40a79-2636">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40a79-2637">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="40a79-2638">Pour plus d’informations, consultez l’article [Web Table connector (connecteur table web)](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="40a79-2639">Source Web dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="40a79-2640">Si vous copiez des données à partir d’une table web, définissez le **type de source** de l’activité de copie sur **WebSource**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="40a79-2641">Actuellement, lorsque la source de l’activité de copie est de type **WebSource**, aucune propriété supplémentaire n’est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="40a79-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="40a79-2642">Exemple</span><span class="sxs-lookup"><span data-stu-id="40a79-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="40a79-2643">Pour plus d’informations, consultez l’article [Web Table connector (connecteur table web)](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="40a79-2644">ENVIRONNEMENTS DE CALCUL</span><span class="sxs-lookup"><span data-stu-id="40a79-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="40a79-2645">Le tableau suivant liste les environnements de calcul pris en charge par Azure Data Factory et les activités de transformation qui peuvent s’exécuter sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="40a79-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="40a79-2646">Cliquez sur le lien concernant le calcul qui vous intéresse pour afficher les schémas JSON pour le service lié, pour le lier à une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="40a79-2647">Environnement de calcul</span><span class="sxs-lookup"><span data-stu-id="40a79-2647">Compute environment</span></span> | <span data-ttu-id="40a79-2648">Activités</span><span class="sxs-lookup"><span data-stu-id="40a79-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="40a79-2649">[Cluster HDInsight à la demande](#on-demand-azure-hdinsight-cluster) ou [votre propre cluster HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="40a79-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="40a79-2650">[Activité personnalisée .NET](#net-custom-activity), [Activité Hive](#hdinsight-hive-activity), [Activité pig](#hdinsight-pig-activity, [Activité MapReduce](#hdinsight-mapreduce-activity), [Activité de diffusion en continu Hadoop](#hdinsight-streaming-activityd), [Activité Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="40a79-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="40a79-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="40a79-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="40a79-2652">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="40a79-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="40a79-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="40a79-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="40a79-2654">[Activité d’exécution par lot Machine Learning](#machine-learning-batch-execution-activity), [Activité des ressources de mise à jour de Machine Learning](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="40a79-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="40a79-2655">Service Analytique Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="40a79-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="40a79-2656">Langage U-SQL du service Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="40a79-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="40a79-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="40a79-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="40a79-2658">Procédure stockée</span><span class="sxs-lookup"><span data-stu-id="40a79-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="40a79-2659">Cluster Azure HDInsight à la demande</span><span class="sxs-lookup"><span data-stu-id="40a79-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="40a79-2660">Le service Azure Data Factory peut automatiquement créer un cluster HDInsight à la demande sous Windows/Linux pour traiter les données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="40a79-2661">Le cluster est créé dans la même région que celle du compte de stockage (propriété linkedServiceName dans JSON) associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="40a79-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="40a79-2662">Vous pouvez exécuter les activités de transformation suivantes sur ce service lié : [Activité personnalisée .NET](#net-custom-activity), [Activité Hive](#hdinsight-hive-activity), [Activité pig] (#hdinsight-pig-activity, [Activité MapReduce](#hdinsight-mapreduce-activity), [Activité de diffusion en continu Hadoop](#hdinsight-streaming-activityd), [Activité Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="40a79-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40a79-2663">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2663">Linked service</span></span> 
<span data-ttu-id="40a79-2664">Le tableau suivant décrit les propriétés utilisées dans la définition JSON Azure d’un service lié HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="40a79-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="40a79-2665">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2665">Property</span></span> | <span data-ttu-id="40a79-2666">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2666">Description</span></span> | <span data-ttu-id="40a79-2667">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2668">type</span><span class="sxs-lookup"><span data-stu-id="40a79-2668">type</span></span> |<span data-ttu-id="40a79-2669">La propriété de type doit être définie sur **HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="40a79-2670">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2670">Yes</span></span> |
| <span data-ttu-id="40a79-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="40a79-2671">clusterSize</span></span> |<span data-ttu-id="40a79-2672">Nombre de nœuds worker/données dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="40a79-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="40a79-2673">Le cluster HDInsight est créé avec 2 nœuds principaux et le nombre de nœuds worker que vous spécifiez pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="40a79-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="40a79-2674">Les nœuds étant de taille Standard_D3 à 4 cœurs, un cluster à 4 nœuds de travail prend 24 cœurs (4\*4 = 16 nœuds pour les nœuds de travail + 2\*4 = 8 cœurs pour les nœuds principaux).</span><span class="sxs-lookup"><span data-stu-id="40a79-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="40a79-2675">Pour plus d’informations sur le niveau Standard_D3, voir [Création de clusters Hadoop basés sur Linux dans HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="40a79-2676">yes</span><span class="sxs-lookup"><span data-stu-id="40a79-2676">Yes</span></span> |
| <span data-ttu-id="40a79-2677">timetolive</span><span class="sxs-lookup"><span data-stu-id="40a79-2677">timetolive</span></span> |<span data-ttu-id="40a79-2678">La durée d’inactivité autorisée pour le cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="40a79-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="40a79-2679">Spécifie la durée pendant laquelle le cluster HDInsight à la demande reste actif après l’achèvement d’une exécution d’activité s’il n’existe aucun autre travail actif dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="40a79-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="40a79-2680">Par exemple, si une exécution d’activité prend 6 minutes et si la propriété TimeToLive est définie sur 5 minutes, le cluster reste actif pendant 5 minutes après les 6 minutes du traitement de l’exécution d’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="40a79-2681">Si une autre exécution d’activité intervient dans la fenêtre de 6 minutes, elle est traitée par le même cluster.</span><span class="sxs-lookup"><span data-stu-id="40a79-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="40a79-2682">La création d’un cluster HDInsight à la demande étant une opération coûteuse (elle peut prendre du temps), utilisez ce paramètre selon le besoin pour améliorer les performances d’une fabrique de données en réutilisant un cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="40a79-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="40a79-2683">Si vous définissez la valeur de la propriété TimeToLive sur 0, le cluster est supprimé dès que l’exécution d’activité est traitée.</span><span class="sxs-lookup"><span data-stu-id="40a79-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="40a79-2684">En revanche, si vous définissez une valeur élevée, le cluster peut rester inactif inutilement entraînant des coûts élevés.</span><span class="sxs-lookup"><span data-stu-id="40a79-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="40a79-2685">Par conséquent, il est important de définir la valeur appropriée en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="40a79-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="40a79-2686">Plusieurs pipelines peuvent partager la même instance du cluster HDInsight à la demande si la valeur de la propriété TimeToLive est correctement définie.</span><span class="sxs-lookup"><span data-stu-id="40a79-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="40a79-2687">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2687">Yes</span></span> |
| <span data-ttu-id="40a79-2688">version</span><span class="sxs-lookup"><span data-stu-id="40a79-2688">version</span></span> |<span data-ttu-id="40a79-2689">Version du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a79-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="40a79-2690">Pour plus d’informations, consultez [Versions de HDInsight prises en charge dans Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="40a79-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="40a79-2691">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2691">No</span></span> |
| <span data-ttu-id="40a79-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="40a79-2692">linkedServiceName</span></span> |<span data-ttu-id="40a79-2693">Le service lié Stockage Azure utilisé par le cluster à la demande pour le stockage et le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="40a79-2694">Actuellement, vous ne pouvez pas créer un cluster HDInsight à la demande qui utilise un Azure Data Lake Store en guise de stockage.</span><span class="sxs-lookup"><span data-stu-id="40a79-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="40a79-2695">Si vous souhaitez stocker les données de résultat à partir du traitement HDInsight dans un Azure Data Lake Store, utilisez une activité de copie pour copier les données du stockage Blob Azure dans Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40a79-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="40a79-2696">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2696">Yes</span></span> |
| <span data-ttu-id="40a79-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="40a79-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="40a79-2698">Spécifie les comptes de stockage supplémentaires pour le service lié HDInsight afin que le service Data Factory puisse les enregistrer en votre nom.</span><span class="sxs-lookup"><span data-stu-id="40a79-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="40a79-2699">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2699">No</span></span> |
| <span data-ttu-id="40a79-2700">osType</span><span class="sxs-lookup"><span data-stu-id="40a79-2700">osType</span></span> |<span data-ttu-id="40a79-2701">Type de système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="40a79-2701">Type of operating system.</span></span> <span data-ttu-id="40a79-2702">Les valeurs autorisées sont Windows (par défaut) et Linux.</span><span class="sxs-lookup"><span data-stu-id="40a79-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="40a79-2703">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2703">No</span></span> |
| <span data-ttu-id="40a79-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="40a79-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="40a79-2705">Le nom du service lié à SQL Azure pointant vers la base de données HCatalog.</span><span class="sxs-lookup"><span data-stu-id="40a79-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="40a79-2706">Le cluster HDInsight à la demande est créé en utilisant Azure SQL Database en tant que metastore.</span><span class="sxs-lookup"><span data-stu-id="40a79-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="40a79-2707">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="40a79-2708">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2708">JSON example</span></span>
<span data-ttu-id="40a79-2709">Le JSON suivant définit un service lié HDInsight à la demande sous Linux.</span><span class="sxs-lookup"><span data-stu-id="40a79-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="40a79-2710">Le service Data Factory crée automatiquement un cluster HDInsight **sous Linux** lors du traitement d’une tranche de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="40a79-2711">Pour plus d’informations, consultez l’article [Compute linked services (services liés de calcul)](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="40a79-2712">Cluster Azure HDInsight existant</span><span class="sxs-lookup"><span data-stu-id="40a79-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="40a79-2713">Vous pouvez créer un service lié Azure HDInsight pour inscrire votre propre cluster HDInsight avec Data Factory.</span><span class="sxs-lookup"><span data-stu-id="40a79-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="40a79-2714">Vous pouvez exécuter les activités de transformation de données suivantes sur ce service lié : [Activité personnalisée .NET](#net-custom-activity), [Activité Hive](#hdinsight-hive-activity), [Activité pig] (#hdinsight-pig-activity, [Activité MapReduce](#hdinsight-mapreduce-activity), [Activité de diffusion en continu Hadoop](#hdinsight-streaming-activityd), [Activité Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="40a79-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40a79-2715">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2715">Linked service</span></span>
<span data-ttu-id="40a79-2716">Le tableau suivant décrit les propriétés utilisées dans la définition JSON Azure d’un service lié Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a79-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="40a79-2717">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2717">Property</span></span> | <span data-ttu-id="40a79-2718">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2718">Description</span></span> | <span data-ttu-id="40a79-2719">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2720">type</span><span class="sxs-lookup"><span data-stu-id="40a79-2720">type</span></span> |<span data-ttu-id="40a79-2721">La propriété de type doit être définie sur **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="40a79-2722">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2722">Yes</span></span> |
| <span data-ttu-id="40a79-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="40a79-2723">clusterUri</span></span> |<span data-ttu-id="40a79-2724">L'URI du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a79-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="40a79-2725">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2725">Yes</span></span> |
| <span data-ttu-id="40a79-2726">username</span><span class="sxs-lookup"><span data-stu-id="40a79-2726">username</span></span> |<span data-ttu-id="40a79-2727">Spécifiez le nom de l'utilisateur à utiliser pour se connecter à un cluster HDInsight existant.</span><span class="sxs-lookup"><span data-stu-id="40a79-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="40a79-2728">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2728">Yes</span></span> |
| <span data-ttu-id="40a79-2729">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2729">password</span></span> |<span data-ttu-id="40a79-2730">Spécifiez le mot de passe du compte d'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2730">Specify password for the user account.</span></span> |<span data-ttu-id="40a79-2731">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2731">Yes</span></span> |
| <span data-ttu-id="40a79-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="40a79-2732">linkedServiceName</span></span> | <span data-ttu-id="40a79-2733">Nom du service lié de stockage Azure faisant référence au stockage Blob Azure utilisé par le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a79-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="40a79-2734">Actuellement, vous ne pouvez pas spécifier un service lié Azure Data Lake Store pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="40a79-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="40a79-2735">Vous pouvez accéder aux données d’Azure Data Lake Store à partir de scripts Hive/Pig si le cluster HDInsight a accès à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40a79-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="40a79-2736">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2736">Yes</span></span> |

<span data-ttu-id="40a79-2737">Pour obtenir la liste des versions des clusters HDInsight pris en charge, consultez [Versions de HDInsight prises en charge](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="40a79-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="40a79-2738">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="40a79-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="40a79-2739">Azure Batch</span></span>
<span data-ttu-id="40a79-2740">Vous pouvez créer un service lié Azure Batch pour inscrire un pool Batch de machines virtuelles avec une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2740">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="40a79-2741">Vous pouvez exécuter des activités personnalisées .NET à l'aide d'Azure Batch ou Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a79-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="40a79-2742">Vous pouvez exécuter une [activité personnalisée .NET](#net-custom-activity) sur ce service lié.</span><span class="sxs-lookup"><span data-stu-id="40a79-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40a79-2743">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2743">Linked service</span></span>
<span data-ttu-id="40a79-2744">Le tableau suivant décrit les propriétés utilisées dans la définition JSON Azure d’un service lié Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="40a79-2744">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="40a79-2745">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2745">Property</span></span> | <span data-ttu-id="40a79-2746">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2746">Description</span></span> | <span data-ttu-id="40a79-2747">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2748">type</span><span class="sxs-lookup"><span data-stu-id="40a79-2748">type</span></span> |<span data-ttu-id="40a79-2749">La propriété de type doit être définie sur **AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2749">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="40a79-2750">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2750">Yes</span></span> |
| <span data-ttu-id="40a79-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="40a79-2751">accountName</span></span> |<span data-ttu-id="40a79-2752">Nom du compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="40a79-2752">Name of the Azure Batch account.</span></span> |<span data-ttu-id="40a79-2753">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2753">Yes</span></span> |
| <span data-ttu-id="40a79-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="40a79-2754">accessKey</span></span> |<span data-ttu-id="40a79-2755">Clé d'accès du compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="40a79-2755">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="40a79-2756">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2756">Yes</span></span> |
| <span data-ttu-id="40a79-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="40a79-2757">poolName</span></span> |<span data-ttu-id="40a79-2758">Nom du pool de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="40a79-2758">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="40a79-2759">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2759">Yes</span></span> |
| <span data-ttu-id="40a79-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="40a79-2760">linkedServiceName</span></span> |<span data-ttu-id="40a79-2761">Nom du service lié Azure Storage associé à ce service lié Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="40a79-2761">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="40a79-2762">Ce service lié est utilisé pour présenter les fichiers nécessaires à l'exécution de l'activité et stocker les journaux d'exécution de l'activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-2762">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="40a79-2763">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="40a79-2764">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="40a79-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="40a79-2765">Azure Machine Learning</span></span>
<span data-ttu-id="40a79-2766">Vous créez un service lié Azure Machine Learning pour inscrire un point de terminaison de notation par lot Machine Learning avec une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2766">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="40a79-2767">Deux activités de transformation des données pouvant être exécutées sur ce service lié : [Activité d’exécution par lot Machine Learning](#machine-learning-batch-execution-activity), [Activité des ressources de mise à jour de Machine Learning](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="40a79-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40a79-2768">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2768">Linked service</span></span>
<span data-ttu-id="40a79-2769">Le tableau suivant décrit les propriétés utilisées dans la définition JSON Azure d’un service lié Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="40a79-2769">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="40a79-2770">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2770">Property</span></span> | <span data-ttu-id="40a79-2771">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2771">Description</span></span> | <span data-ttu-id="40a79-2772">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2773">type</span><span class="sxs-lookup"><span data-stu-id="40a79-2773">Type</span></span> |<span data-ttu-id="40a79-2774">La propriété de type doit être définie sur **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2774">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="40a79-2775">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2775">Yes</span></span> |
| <span data-ttu-id="40a79-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="40a79-2776">mlEndpoint</span></span> |<span data-ttu-id="40a79-2777">L'URL de la notation par lot.</span><span class="sxs-lookup"><span data-stu-id="40a79-2777">The batch scoring URL.</span></span> |<span data-ttu-id="40a79-2778">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2778">Yes</span></span> |
| <span data-ttu-id="40a79-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="40a79-2779">apiKey</span></span> |<span data-ttu-id="40a79-2780">L'API du modèle d'espace de travail publié.</span><span class="sxs-lookup"><span data-stu-id="40a79-2780">The published workspace model’s API.</span></span> |<span data-ttu-id="40a79-2781">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="40a79-2782">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="40a79-2783">Service Analytique Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="40a79-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="40a79-2784">Vous créez un service lié **Analytique Azure Data Lake** pour lier un service de calcul Analytique Azure Data Lake Analytics à une fabrique de données Azure avant d’utiliser l’ [activité U-SQL Analytique Data Lake](data-factory-usql-activity.md) dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-2784">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="40a79-2785">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2785">Linked service</span></span>

<span data-ttu-id="40a79-2786">Le tableau suivant décrit les propriétés utilisées dans la définition JSON d’un service lié Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="40a79-2786">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="40a79-2787">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2787">Property</span></span> | <span data-ttu-id="40a79-2788">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2788">Description</span></span> | <span data-ttu-id="40a79-2789">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2790">Type</span><span class="sxs-lookup"><span data-stu-id="40a79-2790">Type</span></span> |<span data-ttu-id="40a79-2791">La propriété de type doit être définie sur **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2791">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="40a79-2792">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2792">Yes</span></span> |
| <span data-ttu-id="40a79-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="40a79-2793">accountName</span></span> |<span data-ttu-id="40a79-2794">Nom du compte du service Analytique Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="40a79-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="40a79-2795">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2795">Yes</span></span> |
| <span data-ttu-id="40a79-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="40a79-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="40a79-2797">URI du service Analytique Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="40a79-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="40a79-2798">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2798">No</span></span> |
| <span data-ttu-id="40a79-2799">autorisation</span><span class="sxs-lookup"><span data-stu-id="40a79-2799">authorization</span></span> |<span data-ttu-id="40a79-2800">Le code d’autorisation est automatiquement récupéré après un clic sur le bouton **Autoriser** dans l’éditeur de la fabrique de données et une fois la connexion OAuth effectuée.</span><span class="sxs-lookup"><span data-stu-id="40a79-2800">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="40a79-2801">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2801">Yes</span></span> |
| <span data-ttu-id="40a79-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="40a79-2802">subscriptionId</span></span> |<span data-ttu-id="40a79-2803">ID d’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-2803">Azure subscription id</span></span> |<span data-ttu-id="40a79-2804">Non (si non spécifié, l’abonnement de la fabrique de données est utilisé).</span><span class="sxs-lookup"><span data-stu-id="40a79-2804">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="40a79-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="40a79-2805">resourceGroupName</span></span> |<span data-ttu-id="40a79-2806">Nom du groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-2806">Azure resource group name</span></span> |<span data-ttu-id="40a79-2807">Non (si non spécifié, le groupe de ressources de la fabrique de données est utilisé).</span><span class="sxs-lookup"><span data-stu-id="40a79-2807">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="40a79-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="40a79-2808">sessionId</span></span> |<span data-ttu-id="40a79-2809">ID de session issu de la session d'autorisation OAuth.</span><span class="sxs-lookup"><span data-stu-id="40a79-2809">session id from the OAuth authorization session.</span></span> <span data-ttu-id="40a79-2810">Chaque ID de session est unique et ne peut être utilisé qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="40a79-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="40a79-2811">Voici l’ID de session généré automatiquement lorsque vous utilisez Data Factory.</span><span class="sxs-lookup"><span data-stu-id="40a79-2811">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="40a79-2812">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="40a79-2813">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2813">JSON example</span></span>
<span data-ttu-id="40a79-2814">L’exemple suivant présente la définition JSON pour le service lié Analytique Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="40a79-2814">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="40a79-2815">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-2815">Azure SQL Database</span></span>
<span data-ttu-id="40a79-2816">Créez un service lié Azure SQL et utilisez-le avec l’ [activité de procédure stockée](#stored-procedure-activity) pour appeler une procédure stockée à partir d’un pipeline Data Factory.</span><span class="sxs-lookup"><span data-stu-id="40a79-2816">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40a79-2817">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2817">Linked service</span></span>
<span data-ttu-id="40a79-2818">Pour définir un service lié Azure SQL Database, définissez le **type** du service lié sur **AzureSqlDatabase** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2818">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2819">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2819">Property</span></span> | <span data-ttu-id="40a79-2820">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2820">Description</span></span> | <span data-ttu-id="40a79-2821">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-2822">connectionString</span></span> |<span data-ttu-id="40a79-2823">Spécifier les informations requises pour la connexion à l’instance de base de données SQL Azure pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="40a79-2823">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="40a79-2824">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="40a79-2825">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="40a79-2826">Pour plus d’informations sur ce service lié, consultez la page [Connecteur SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="40a79-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="40a79-2827">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="40a79-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="40a79-2828">Créez un service lié Azure SQL Data Warehouse et utilisez-le avec l’ [activité de procédure stockée](data-factory-stored-proc-activity.md) pour appeler une procédure stockée à partir d’un pipeline Data Factory.</span><span class="sxs-lookup"><span data-stu-id="40a79-2828">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40a79-2829">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2829">Linked service</span></span>
<span data-ttu-id="40a79-2830">Pour définir un service lié Azure SQL Data Warehouse, définissez le **type** du service lié sur **AzureSqlDW** et spécifiez les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="40a79-2830">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40a79-2831">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2831">Property</span></span> | <span data-ttu-id="40a79-2832">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2832">Description</span></span> | <span data-ttu-id="40a79-2833">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-2834">connectionString</span></span> |<span data-ttu-id="40a79-2835">Spécifier les informations requises pour la connexion à l’instance Azure SQL Data Warehouse pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="40a79-2835">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="40a79-2836">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="40a79-2837">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="40a79-2838">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="40a79-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="40a79-2839">SQL Server</span></span> 
<span data-ttu-id="40a79-2840">Créez un service lié à SQL Server et utilisez-le avec l’ [activité de procédure stockée](data-factory-stored-proc-activity.md) pour appeler une procédure stockée à partir d’un pipeline Data Factory.</span><span class="sxs-lookup"><span data-stu-id="40a79-2840">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40a79-2841">Service lié</span><span class="sxs-lookup"><span data-stu-id="40a79-2841">Linked service</span></span>
<span data-ttu-id="40a79-2842">Vous créez un service lié de type **OnPremisesSqlServer** pour lier une base de données SQL Server locale à une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-2842">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="40a79-2843">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="40a79-2843">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="40a79-2844">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40a79-2844">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="40a79-2845">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2845">Property</span></span> | <span data-ttu-id="40a79-2846">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2846">Description</span></span> | <span data-ttu-id="40a79-2847">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2848">type</span><span class="sxs-lookup"><span data-stu-id="40a79-2848">type</span></span> |<span data-ttu-id="40a79-2849">Le type de propriété doit être défini sur **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2849">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="40a79-2850">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2850">Yes</span></span> |
| <span data-ttu-id="40a79-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="40a79-2851">connectionString</span></span> |<span data-ttu-id="40a79-2852">Spécifiez les informations connectionString nécessaires pour connecter la base de données SQL Server locale à l’aide de l’authentification SQL ou de l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-2852">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="40a79-2853">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2853">Yes</span></span> |
| <span data-ttu-id="40a79-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40a79-2854">gatewayName</span></span> |<span data-ttu-id="40a79-2855">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-2855">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="40a79-2856">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2856">Yes</span></span> |
| <span data-ttu-id="40a79-2857">username</span><span class="sxs-lookup"><span data-stu-id="40a79-2857">username</span></span> |<span data-ttu-id="40a79-2858">Spécifiez le nom d’utilisateur si vous utilisez l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="40a79-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="40a79-2859">Exemple : **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="40a79-2860">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2860">No</span></span> |
| <span data-ttu-id="40a79-2861">password</span><span class="sxs-lookup"><span data-stu-id="40a79-2861">password</span></span> |<span data-ttu-id="40a79-2862">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2862">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40a79-2863">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2863">No</span></span> |

<span data-ttu-id="40a79-2864">Vous pouvez chiffrer les informations d’identification à l’aide de l’applet de commande **New-AzureRmDataFactoryEncryptValue** et les utiliser dans la chaîne de connexion comme indiqué dans l’exemple suivant (propriété **EncryptedCredential**) :</span><span class="sxs-lookup"><span data-stu-id="40a79-2864">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="40a79-2865">Exemple : JSON pour utilisation de l’authentification SQL</span><span class="sxs-lookup"><span data-stu-id="40a79-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="40a79-2866">Exemple : JSON pour utilisation de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="40a79-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="40a79-2867">Si le nom d’utilisateur et le mot de passe sont spécifiés, la passerelle les utilise pour identifier le compte utilisateur spécifié pour connecter la base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="40a79-2867">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="40a79-2868">Dans le cas contraire, la passerelle se connecte directement à SQL Server avec le contexte de sécurité de la passerelle (son compte de démarrage).</span><span class="sxs-lookup"><span data-stu-id="40a79-2868">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="40a79-2869">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40a79-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="40a79-2870">ACTIVITÉS DE TRANSFORMATION DES DONNÉES</span><span class="sxs-lookup"><span data-stu-id="40a79-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="40a79-2871">Activité</span><span class="sxs-lookup"><span data-stu-id="40a79-2871">Activity</span></span> | <span data-ttu-id="40a79-2872">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="40a79-2873">Activité Hive HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a79-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="40a79-2874">L’activité Hive HDInsight d’un pipeline Data Factory exécute des requêtes Hive sur votre propre cluster ou cluster à la demande HDInsight sous Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="40a79-2874">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="40a79-2875">Activité Pig HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a79-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="40a79-2876">L’activité Pig HDInsight d’un pipeline Data Factory exécute des requêtes Pig sur votre propre cluster ou cluster à la demande HDInsight sous Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="40a79-2876">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="40a79-2877">Activité MapReduce HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a79-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="40a79-2878">L’activité MapReduce de HDInsight dans un pipeline Data Factory exécute des programmes MapReduce sur votre cluster HDInsight propre ou à la demande sous Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="40a79-2878">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="40a79-2879">Activité de diffusion en continu HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a79-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="40a79-2880">L’activité de diffusion en continu HDInsight dans un pipeline Data Factory exécute des programmes de diffusion en continu Hadoop sur votre cluster HDInsight propre ou à la demande sous Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="40a79-2880">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="40a79-2881">Activité HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="40a79-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="40a79-2882">L’activité Spark HDInsight d’un pipeline Data Factory exécute des programmes Spark sur votre propre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a79-2882">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="40a79-2883">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="40a79-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="40a79-2884">Azure Data Factory vous permet de créer facilement des pipelines qui utilisent un service web Azure Machine Learning publié pour l’analyse prédictive.</span><span class="sxs-lookup"><span data-stu-id="40a79-2884">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="40a79-2885">À l’aide de l’activité d’exécution par lots dans un pipeline Azure Data Factory, vous pouvez appeler un service web Machine Learning pour effectuer des prédictions sur les données par lots.</span><span class="sxs-lookup"><span data-stu-id="40a79-2885">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="40a79-2886">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="40a79-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="40a79-2887">Au fil du temps, les modèles prédictifs dans les expériences de notation Machine Learning doivent être reformés à l’aide de nouveaux jeux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="40a79-2887">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="40a79-2888">Une fois que vous avez fini la reformation, vous souhaitez mettre à jour le service web de notation avec le modèle Machine Learning reformé.</span><span class="sxs-lookup"><span data-stu-id="40a79-2888">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="40a79-2889">Vous pouvez utiliser l’activité des ressources de mise à jour pour mettre à jour le service web avec le modèle qui vient d’être formé.</span><span class="sxs-lookup"><span data-stu-id="40a79-2889">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="40a79-2890">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="40a79-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="40a79-2891">Vous pouvez utiliser l’activité de procédure stockée dans un pipeline Data Factory pour appeler une procédure stockée dans l’une des banques de données suivantes : Azure SQL Database, Azure SQL Data Warehouse, base de données SQL Server dans votre entreprise ou une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-2891">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="40a79-2892">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="40a79-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="40a79-2893">L’activité U-SQL Data Lake Analytics exécute un script U-SQL sur un cluster Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="40a79-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="40a79-2894">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="40a79-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="40a79-2895">Si vous devez transformer les données d’une manière qui n’est pas prise en charge par Data Factory, créez une activité personnalisée avec votre propre logique de traitement des données et utilisez cette activité dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-2895">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="40a79-2896">Vous pouvez configurer l’activité .NET personnalisée pour l’exécuter en utilisant un service Azure Batch ou un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40a79-2896">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="40a79-2897">Activité Hive HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a79-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="40a79-2898">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité Hive.</span><span class="sxs-lookup"><span data-stu-id="40a79-2898">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="40a79-2899">La propriété de type de l’activité doit être : **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2899">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="40a79-2900">Vous devez d’abord créer un service lié HDInsight, puis spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2900">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40a79-2901">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur HDInsightHive :</span><span class="sxs-lookup"><span data-stu-id="40a79-2901">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="40a79-2902">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2902">Property</span></span> | <span data-ttu-id="40a79-2903">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2903">Description</span></span> | <span data-ttu-id="40a79-2904">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2905">script</span><span class="sxs-lookup"><span data-stu-id="40a79-2905">script</span></span> |<span data-ttu-id="40a79-2906">Spécifier le script en ligne Hive</span><span class="sxs-lookup"><span data-stu-id="40a79-2906">Specify the Hive script inline</span></span> |<span data-ttu-id="40a79-2907">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2907">No</span></span> |
| <span data-ttu-id="40a79-2908">Chemin d'accès du script</span><span class="sxs-lookup"><span data-stu-id="40a79-2908">script path</span></span> |<span data-ttu-id="40a79-2909">Stockez le script Hive dans un stockage d'objets blob Azure et indiquez le chemin d'accès au fichier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2909">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="40a79-2910">Utilisez la propriété ’script’ ou ’scriptPath’.</span><span class="sxs-lookup"><span data-stu-id="40a79-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="40a79-2911">Les deux propriétés ne peuvent pas être utilisées simultanément.</span><span class="sxs-lookup"><span data-stu-id="40a79-2911">Both cannot be used together.</span></span> <span data-ttu-id="40a79-2912">Le nom de fichier respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-2912">The file name is case-sensitive.</span></span> |<span data-ttu-id="40a79-2913">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2913">No</span></span> |
| <span data-ttu-id="40a79-2914">defines</span><span class="sxs-lookup"><span data-stu-id="40a79-2914">defines</span></span> |<span data-ttu-id="40a79-2915">Spécifier les paramètres sous forme de paires clé/valeur pour le référencement au sein du script Hive à l'aide de ’hiveconf’</span><span class="sxs-lookup"><span data-stu-id="40a79-2915">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="40a79-2916">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2916">No</span></span> |

<span data-ttu-id="40a79-2917">Ces propriétés de type sont spécifiques à l’activité Hive.</span><span class="sxs-lookup"><span data-stu-id="40a79-2917">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="40a79-2918">D’autres propriétés (en dehors de la section typeProperties) sont prises en charge pour toutes les activités.</span><span class="sxs-lookup"><span data-stu-id="40a79-2918">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="40a79-2919">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2919">JSON example</span></span>
<span data-ttu-id="40a79-2920">Le JSON suivant définit une Activité Hive HDInsight dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-2920">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

<span data-ttu-id="40a79-2921">Pour plus d’informations, consultez l’article [Hive Activity (activité Hive)](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="40a79-2922">Activité Pig HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a79-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="40a79-2923">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité pig.</span><span class="sxs-lookup"><span data-stu-id="40a79-2923">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="40a79-2924">La propriété de type de l’activité doit être : **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2924">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="40a79-2925">Vous devez d’abord créer un service lié HDInsight, puis spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2925">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40a79-2926">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur HDInsightPig :</span><span class="sxs-lookup"><span data-stu-id="40a79-2926">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="40a79-2927">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2927">Property</span></span> | <span data-ttu-id="40a79-2928">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2928">Description</span></span> | <span data-ttu-id="40a79-2929">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2930">script</span><span class="sxs-lookup"><span data-stu-id="40a79-2930">script</span></span> |<span data-ttu-id="40a79-2931">Spécifier le script en ligne pig</span><span class="sxs-lookup"><span data-stu-id="40a79-2931">Specify the Pig script inline</span></span> |<span data-ttu-id="40a79-2932">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2932">No</span></span> |
| <span data-ttu-id="40a79-2933">chemin d'accès du script</span><span class="sxs-lookup"><span data-stu-id="40a79-2933">script path</span></span> |<span data-ttu-id="40a79-2934">Stockez le script pig dans un stockage d'objets blob Azure et indiquez le chemin d'accès au fichier.</span><span class="sxs-lookup"><span data-stu-id="40a79-2934">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="40a79-2935">Utilisez la propriété ’script’ ou ’scriptPath’.</span><span class="sxs-lookup"><span data-stu-id="40a79-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="40a79-2936">Les deux propriétés ne peuvent pas être utilisées simultanément.</span><span class="sxs-lookup"><span data-stu-id="40a79-2936">Both cannot be used together.</span></span> <span data-ttu-id="40a79-2937">Le nom de fichier respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-2937">The file name is case-sensitive.</span></span> |<span data-ttu-id="40a79-2938">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2938">No</span></span> |
| <span data-ttu-id="40a79-2939">defines</span><span class="sxs-lookup"><span data-stu-id="40a79-2939">defines</span></span> |<span data-ttu-id="40a79-2940">Spécifier les paramètres sous forme de paires clé/valeur pour le référencement au sein du script pig</span><span class="sxs-lookup"><span data-stu-id="40a79-2940">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="40a79-2941">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2941">No</span></span> |

<span data-ttu-id="40a79-2942">Ces propriétés de type sont spécifiques à l’activité pig.</span><span class="sxs-lookup"><span data-stu-id="40a79-2942">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="40a79-2943">D’autres propriétés (en dehors de la section typeProperties) sont prises en charge pour toutes les activités.</span><span class="sxs-lookup"><span data-stu-id="40a79-2943">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="40a79-2944">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2944">JSON example</span></span>

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

<span data-ttu-id="40a79-2945">Pour plus d’informations, consultez l’article [Pig Activity (activité pig)](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="40a79-2946">Activité MapReduce HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a79-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="40a79-2947">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité MapReduce.</span><span class="sxs-lookup"><span data-stu-id="40a79-2947">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="40a79-2948">La propriété de type de l’activité doit être : **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2948">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="40a79-2949">Vous devez d’abord créer un service lié HDInsight, puis spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2949">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40a79-2950">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur HDInsightMapReduce :</span><span class="sxs-lookup"><span data-stu-id="40a79-2950">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="40a79-2951">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2951">Property</span></span> | <span data-ttu-id="40a79-2952">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2952">Description</span></span> | <span data-ttu-id="40a79-2953">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="40a79-2954">jarLinkedService</span></span> | <span data-ttu-id="40a79-2955">Nom du service lié pour le stockage Azure qui contient le fichier JAR.</span><span class="sxs-lookup"><span data-stu-id="40a79-2955">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="40a79-2956">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2956">Yes</span></span> |
| <span data-ttu-id="40a79-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="40a79-2957">jarFilePath</span></span> | <span data-ttu-id="40a79-2958">Chemin d’accès du fichier JAR dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-2958">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="40a79-2959">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2959">Yes</span></span> | 
| <span data-ttu-id="40a79-2960">className</span><span class="sxs-lookup"><span data-stu-id="40a79-2960">className</span></span> | <span data-ttu-id="40a79-2961">Nom de la classe principale dans le fichier JAR.</span><span class="sxs-lookup"><span data-stu-id="40a79-2961">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="40a79-2962">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-2962">Yes</span></span> | 
| <span data-ttu-id="40a79-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="40a79-2963">arguments</span></span> | <span data-ttu-id="40a79-2964">Une liste séparée par des virgules des arguments du programme MapReduce.</span><span class="sxs-lookup"><span data-stu-id="40a79-2964">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="40a79-2965">Lors de l’exécution, vous verrez quelques arguments supplémentaires (par exemple : mapreduce.job.tags) à partir de l’infrastructure MapReduce.</span><span class="sxs-lookup"><span data-stu-id="40a79-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="40a79-2966">Pour différencier vos arguments avec les arguments MapReduce, envisagez d’utiliser l’option et la valeur en tant qu’arguments, comme indiqué dans l’exemple suivant (-s, --entrée, --sortie, etc. sont des options immédiatement suivies par leurs valeurs)</span><span class="sxs-lookup"><span data-stu-id="40a79-2966">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="40a79-2967">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="40a79-2968">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce to generate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="40a79-2969">Pour plus d’informations, consultez l’article [MapReduce Activity (activité MapReduce)](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="40a79-2970">Activité de diffusion en continu HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a79-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="40a79-2971">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité de diffusion en continu Hadoop.</span><span class="sxs-lookup"><span data-stu-id="40a79-2971">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="40a79-2972">La propriété de type de l’activité doit être : **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2972">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="40a79-2973">Vous devez d’abord créer un service lié HDInsight, puis spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40a79-2973">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40a79-2974">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur HDInsightStreaming :</span><span class="sxs-lookup"><span data-stu-id="40a79-2974">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="40a79-2975">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-2975">Property</span></span> | <span data-ttu-id="40a79-2976">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="40a79-2977">mappeur</span><span class="sxs-lookup"><span data-stu-id="40a79-2977">mapper</span></span> | <span data-ttu-id="40a79-2978">Nom du fichier exécutable du mappeur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2978">Name of the mapper executable.</span></span> <span data-ttu-id="40a79-2979">Dans l’exemple, cat.exe est le fichier exécutable du mappeur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2979">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="40a79-2980">raccord de réduction</span><span class="sxs-lookup"><span data-stu-id="40a79-2980">reducer</span></span> | <span data-ttu-id="40a79-2981">Nom du fichier exécutable du raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="40a79-2981">Name of the reducer executable.</span></span> <span data-ttu-id="40a79-2982">Dans l’exemple, wc.exe est le fichier exécutable du raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="40a79-2982">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="40a79-2983">entrée</span><span class="sxs-lookup"><span data-stu-id="40a79-2983">input</span></span> | <span data-ttu-id="40a79-2984">Fichier d’entrée (emplacement compris) pour le mappeur.</span><span class="sxs-lookup"><span data-stu-id="40a79-2984">Input file (including location) for the mapper.</span></span> <span data-ttu-id="40a79-2985">Dans l’exemple « wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt », adfsample est le conteneur de l’objet blob, example/data/Gutenberg est le dossier et davinci.txt est l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="40a79-2985">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="40a79-2986">sortie</span><span class="sxs-lookup"><span data-stu-id="40a79-2986">output</span></span> | <span data-ttu-id="40a79-2987">Fichier de sortie (emplacement compris) pour le raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="40a79-2987">Output file (including location) for the reducer.</span></span> <span data-ttu-id="40a79-2988">La sortie de la tâche de diffusion en continu Hadoop est écrite à l’emplacement spécifié pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="40a79-2988">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="40a79-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="40a79-2989">filePaths</span></span> | <span data-ttu-id="40a79-2990">Chemins d’accès pour les exécutables du mappeur et du raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="40a79-2990">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="40a79-2991">Dans l’exemple « adfsample/example/apps/wc.exe », adfsample est le conteneur de l’objet blob, example/apps est le dossier et wc.exe est le fichier exécutable.</span><span class="sxs-lookup"><span data-stu-id="40a79-2991">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="40a79-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="40a79-2992">fileLinkedService</span></span> | <span data-ttu-id="40a79-2993">Service lié Stockage Azure qui représente le stockage Azure qui contient les fichiers spécifiés dans la section filePaths.</span><span class="sxs-lookup"><span data-stu-id="40a79-2993">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="40a79-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="40a79-2994">arguments</span></span> | <span data-ttu-id="40a79-2995">Une liste séparée par des virgules des arguments du programme MapReduce.</span><span class="sxs-lookup"><span data-stu-id="40a79-2995">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="40a79-2996">Lors de l’exécution, vous verrez quelques arguments supplémentaires (par exemple : mapreduce.job.tags) à partir de l’infrastructure MapReduce.</span><span class="sxs-lookup"><span data-stu-id="40a79-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="40a79-2997">Pour différencier vos arguments avec les arguments MapReduce, envisagez d’utiliser l’option et la valeur en tant qu’arguments, comme indiqué dans l’exemple suivant (-s, --entrée, --sortie, etc. sont des options immédiatement suivies par leurs valeurs)</span><span class="sxs-lookup"><span data-stu-id="40a79-2997">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="40a79-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="40a79-2998">getDebugInfo</span></span> | <span data-ttu-id="40a79-2999">Un élément facultatif.</span><span class="sxs-lookup"><span data-stu-id="40a79-2999">An optional element.</span></span> <span data-ttu-id="40a79-3000">Si sa valeur est Failure, les journaux ne sont téléchargés qu’en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="40a79-3000">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="40a79-3001">Si sa valeur est All, les journaux sont toujours téléchargés, quel que soit l’état de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="40a79-3001">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="40a79-3002">Vous devez spécifier un jeu de données de sortie pour l’activité de diffusion en continu Hadoop pour la propriété **outputs** .</span><span class="sxs-lookup"><span data-stu-id="40a79-3002">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="40a79-3003">Il peut s’agir simplement d’un jeu de données factice qui est nécessaire au fonctionnement de la planification (horaire, quotidienne, etc.) du pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-3003">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="40a79-3004">Si l’activité n’accepte pas d’entrée, vous pouvez ignorer la spécification d’un jeu de données d’entrée relatif à l’activité pour la propriété **inputs**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3004">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="40a79-3005">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-3005">JSON example</span></span>

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="40a79-3006">Pour plus d’informations, consultez l’article [Hadoop Streaming Activity (activité de diffusion en continu Hadoop)](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="40a79-3007">Activité Spark HDInsight</span><span class="sxs-lookup"><span data-stu-id="40a79-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="40a79-3008">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité Spark.</span><span class="sxs-lookup"><span data-stu-id="40a79-3008">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="40a79-3009">La propriété de type de l’activité doit être : **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3009">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="40a79-3010">Vous devez d’abord créer un service lié HDInsight, puis spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3010">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40a79-3011">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur HDInsightSpark :</span><span class="sxs-lookup"><span data-stu-id="40a79-3011">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="40a79-3012">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-3012">Property</span></span> | <span data-ttu-id="40a79-3013">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-3013">Description</span></span> | <span data-ttu-id="40a79-3014">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="40a79-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="40a79-3015">rootPath</span></span> | <span data-ttu-id="40a79-3016">Conteneur d’objets blob Azure et dossier contenant le fichier Spark.</span><span class="sxs-lookup"><span data-stu-id="40a79-3016">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="40a79-3017">Le nom de fichier respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-3017">The file name is case-sensitive.</span></span> | <span data-ttu-id="40a79-3018">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3018">Yes</span></span> |
| <span data-ttu-id="40a79-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="40a79-3019">entryFilePath</span></span> | <span data-ttu-id="40a79-3020">Chemin d’accès relatif au dossier racine du code/package Spark.</span><span class="sxs-lookup"><span data-stu-id="40a79-3020">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="40a79-3021">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3021">Yes</span></span> |
| <span data-ttu-id="40a79-3022">className</span><span class="sxs-lookup"><span data-stu-id="40a79-3022">className</span></span> | <span data-ttu-id="40a79-3023">Classe principale Java/Spark de l’application.</span><span class="sxs-lookup"><span data-stu-id="40a79-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="40a79-3024">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3024">No</span></span> | 
| <span data-ttu-id="40a79-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="40a79-3025">arguments</span></span> | <span data-ttu-id="40a79-3026">Liste d’arguments de ligne de commande du programme Spark.</span><span class="sxs-lookup"><span data-stu-id="40a79-3026">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="40a79-3027">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3027">No</span></span> | 
| <span data-ttu-id="40a79-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="40a79-3028">proxyUser</span></span> | <span data-ttu-id="40a79-3029">Identité du compte d’utilisateur à emprunter pour exécuter le programme Spark.</span><span class="sxs-lookup"><span data-stu-id="40a79-3029">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="40a79-3030">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3030">No</span></span> | 
| <span data-ttu-id="40a79-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="40a79-3031">sparkConfig</span></span> | <span data-ttu-id="40a79-3032">Propriétés de configuration Spark.</span><span class="sxs-lookup"><span data-stu-id="40a79-3032">Spark configuration properties.</span></span> | <span data-ttu-id="40a79-3033">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3033">No</span></span> | 
| <span data-ttu-id="40a79-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="40a79-3034">getDebugInfo</span></span> | <span data-ttu-id="40a79-3035">Spécifie quand les fichiers journaux de Spark sont copiés vers le stockage Azure utilisé par le cluster HDInsight (ou) spécifié par sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="40a79-3035">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="40a79-3036">Valeurs autorisées : Aucun, Toujours ou Échec.</span><span class="sxs-lookup"><span data-stu-id="40a79-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="40a79-3037">Valeur par défaut : Aucun.</span><span class="sxs-lookup"><span data-stu-id="40a79-3037">Default value: None.</span></span> | <span data-ttu-id="40a79-3038">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3038">No</span></span> | 
| <span data-ttu-id="40a79-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="40a79-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="40a79-3040">Service lié de stockage Azure qui contient le fichier de travail, les dépendances et les journaux Spark.</span><span class="sxs-lookup"><span data-stu-id="40a79-3040">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="40a79-3041">Si vous ne spécifiez pas de valeur pour cette propriété, le stockage associé au cluster HDInsight est utilisé.</span><span class="sxs-lookup"><span data-stu-id="40a79-3041">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="40a79-3042">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="40a79-3043">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="40a79-3044">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="40a79-3044">Note the following points:</span></span> 

- <span data-ttu-id="40a79-3045">La propriété **type** est définie sur **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3045">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="40a79-3046">**rootPath** est définie sur **adfspark\\pyFiles**, où adfspark est le conteneur d’objets Blob Azure contenant le dossier pyFiles.</span><span class="sxs-lookup"><span data-stu-id="40a79-3046">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="40a79-3047">Dans cet exemple, le stockage Blob Azure est celui qui est associé au cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="40a79-3047">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="40a79-3048">Vous pouvez charger le fichier vers un autre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="40a79-3048">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="40a79-3049">Si vous procédez ainsi, créez un service lié de stockage Azure pour lier ce compte de stockage à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-3049">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="40a79-3050">Ensuite, spécifiez le nom du service lié en tant que valeur pour la propriété **sparkJobLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3050">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="40a79-3051">Consultez les [propriétés de l’activité Spark](#spark-activity-properties) pour plus d’informations sur cette propriété et d’autres propriétés prises en charge par l’activité Spark.</span><span class="sxs-lookup"><span data-stu-id="40a79-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="40a79-3052">La propriété **entryFilePath** est définie sur **test.py**, c’est-à-dire le fichier python.</span><span class="sxs-lookup"><span data-stu-id="40a79-3052">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="40a79-3053">La propriété **getDebugInfo** est définie sur **Always**, ce qui signifie que les fichiers journaux sont toujours générés (succès ou échec).</span><span class="sxs-lookup"><span data-stu-id="40a79-3053">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="40a79-3054">Nous vous recommandons de ne pas définir cette propriété sur Always dans un environnement de production, sauf si vous dépannez un problème.</span><span class="sxs-lookup"><span data-stu-id="40a79-3054">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="40a79-3055">La section **outputs** possède un jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-3055">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="40a79-3056">Vous devez spécifier un jeu de données de sortie même si le programme Spark ne génère aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-3056">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="40a79-3057">Le jeu de données de sortie pilote la planification du pipeline (horaire, quotidienne, etc.).</span><span class="sxs-lookup"><span data-stu-id="40a79-3057">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="40a79-3058">Pour plus d’informations sur l’activité, consultez l’article [Spark Activity (activité Spark)](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-3058">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="40a79-3059">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="40a79-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="40a79-3060">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité d’exécution par lots Azure ML.</span><span class="sxs-lookup"><span data-stu-id="40a79-3060">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="40a79-3061">La propriété de type de l’activité doit être : **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3061">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="40a79-3062">Vous devez d’abord créer un service lié Azure Machine Learning, puis spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3062">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40a79-3063">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur AzureMLBatchExecution :</span><span class="sxs-lookup"><span data-stu-id="40a79-3063">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="40a79-3064">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-3064">Property</span></span> | <span data-ttu-id="40a79-3065">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-3065">Description</span></span> | <span data-ttu-id="40a79-3066">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="40a79-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="40a79-3067">webServiceInput</span></span> | <span data-ttu-id="40a79-3068">Le jeu de données à transmettre en tant qu’entrée pour le service web Azure ML.</span><span class="sxs-lookup"><span data-stu-id="40a79-3068">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="40a79-3069">Ce jeu de données doit également être inclus dans les entrées de l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-3069">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="40a79-3070">Utilisez webServiceInput ou webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="40a79-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="40a79-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="40a79-3071">webServiceInputs</span></span> | <span data-ttu-id="40a79-3072">Spécifie les jeux de données à transmettre en tant qu’entrées pour le service web Azure ML.</span><span class="sxs-lookup"><span data-stu-id="40a79-3072">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="40a79-3073">Si le service web prend plusieurs entrées, utilisez la propriété webServiceInputs au lieu de la propriété webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="40a79-3073">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="40a79-3074">Les jeux de données référencés par **webServiceInputs** doivent également être inclus dans les **entrées** de l’activité.</span><span class="sxs-lookup"><span data-stu-id="40a79-3074">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="40a79-3075">Utilisez webServiceInput ou webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="40a79-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="40a79-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="40a79-3076">webServiceOutputs</span></span> | <span data-ttu-id="40a79-3077">Les jeux de données qui sont attribués en tant que sorties pour le service web Azure ML.</span><span class="sxs-lookup"><span data-stu-id="40a79-3077">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="40a79-3078">Le service web renvoie des données de sortie dans ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-3078">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="40a79-3079">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3079">Yes</span></span> | 
<span data-ttu-id="40a79-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="40a79-3080">globalParameters</span></span> | <span data-ttu-id="40a79-3081">Spécifie les valeurs pour les paramètres de service web dans cette section.</span><span class="sxs-lookup"><span data-stu-id="40a79-3081">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="40a79-3082">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="40a79-3083">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-3083">JSON example</span></span>
<span data-ttu-id="40a79-3084">Dans cet exemple, l’activité a le jeu de données **MLSqlInput** en tant qu’entrée et **MLSqlOutput** en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-3084">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="40a79-3085">Le jeu de données **MLSqlInput** est transmis en tant qu’entrée au service web à l’aide de la propriété JSON **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3085">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="40a79-3086">Le jeu de données **MLSqlOutput** est transmis en tant que sortie au service web à l’aide de la propriété JSON **webServiceOutputs**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3086">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="40a79-3087">Dans l’exemple JSON, le service web Azure Machine Learning déployé utilise un module lecteur et un module enregistreur pour lire/écrire des données depuis/vers une base de données Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="40a79-3087">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="40a79-3088">Ce service web expose les quatre paramètres suivants : Database server name, Database name, Server user account name et Server user account password.</span><span class="sxs-lookup"><span data-stu-id="40a79-3088">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="40a79-3089">Seules les entrées et sorties de l’activité AzureMLBatchExecution peuvent être transmises en tant que paramètres au service web.</span><span class="sxs-lookup"><span data-stu-id="40a79-3089">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="40a79-3090">Par exemple, dans l’extrait de code JSON ci-dessus, MLSqlInput est une entrée de l’activité AzureMLBatchExecution, qui est transmise comme entrée au service web via le paramètre webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="40a79-3090">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="40a79-3091">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="40a79-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="40a79-3092">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité des ressources de mise à jour Azure ML.</span><span class="sxs-lookup"><span data-stu-id="40a79-3092">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="40a79-3093">La propriété de type de l’activité doit être : **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3093">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="40a79-3094">Vous devez d’abord créer un service lié Azure Machine Learning, puis spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3094">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40a79-3095">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur AzureMLUpdateResource :</span><span class="sxs-lookup"><span data-stu-id="40a79-3095">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="40a79-3096">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-3096">Property</span></span> | <span data-ttu-id="40a79-3097">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-3097">Description</span></span> | <span data-ttu-id="40a79-3098">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="40a79-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="40a79-3099">trainedModelName</span></span> | <span data-ttu-id="40a79-3100">Nom du modèle reformé.</span><span class="sxs-lookup"><span data-stu-id="40a79-3100">Name of the retrained model.</span></span> | <span data-ttu-id="40a79-3101">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3101">Yes</span></span> |  
<span data-ttu-id="40a79-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="40a79-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="40a79-3103">Jeu de données pointant vers le fichier iLearner renvoyé par l’opération de reformation.</span><span class="sxs-lookup"><span data-stu-id="40a79-3103">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="40a79-3104">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="40a79-3105">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-3105">JSON example</span></span>
<span data-ttu-id="40a79-3106">Le pipeline a deux activités : **AzureMLBatchExecution** et **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3106">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="40a79-3107">L’activité d’exécution par lot Azure ML prend les données d’apprentissage comme entrée et génère un fichier .iLearner comme sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-3107">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="40a79-3108">L’activité appelle le service web de formation (expérience de formation exposée comme un service web) avec les données de formation d’entrée et reçoit le fichier iLearner du service web.</span><span class="sxs-lookup"><span data-stu-id="40a79-3108">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="40a79-3109">placeholderBlob est simplement un jeu de données de sortie factice requis par le service Azure Data Factory pour exécuter le pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-3109">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="40a79-3110">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="40a79-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="40a79-3111">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité U-SQL.</span><span class="sxs-lookup"><span data-stu-id="40a79-3111">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="40a79-3112">La propriété de type de l’activité doit être : **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3112">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="40a79-3113">Vous devez créer un service lié Azure Data Lake Analytics et spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3113">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40a79-3114">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur DataLakeAnalyticsU-SQL :</span><span class="sxs-lookup"><span data-stu-id="40a79-3114">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="40a79-3115">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-3115">Property</span></span> | <span data-ttu-id="40a79-3116">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-3116">Description</span></span> | <span data-ttu-id="40a79-3117">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="40a79-3118">scriptPath</span></span> |<span data-ttu-id="40a79-3119">Chemin d'accès au dossier qui contient le script SQL-U.</span><span class="sxs-lookup"><span data-stu-id="40a79-3119">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="40a79-3120">Le nom de fichier respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="40a79-3120">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="40a79-3121">Non (si vous utilisez le script)</span><span class="sxs-lookup"><span data-stu-id="40a79-3121">No (if you use script)</span></span> |
| <span data-ttu-id="40a79-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="40a79-3122">scriptLinkedService</span></span> |<span data-ttu-id="40a79-3123">Service lié qui lie le stockage qui contient le script à la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="40a79-3123">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="40a79-3124">Non (si vous utilisez le script)</span><span class="sxs-lookup"><span data-stu-id="40a79-3124">No (if you use script)</span></span> |
| <span data-ttu-id="40a79-3125">script</span><span class="sxs-lookup"><span data-stu-id="40a79-3125">script</span></span> |<span data-ttu-id="40a79-3126">Spécifiez un script en ligne au lieu de spécifier scriptPath et scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="40a79-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="40a79-3127">Par exemple : « script » : « Test CRÉER BASE DE DONNÉES ».</span><span class="sxs-lookup"><span data-stu-id="40a79-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="40a79-3128">Non (si vous utilisez scriptPath et scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="40a79-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="40a79-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="40a79-3129">degreeOfParallelism</span></span> |<span data-ttu-id="40a79-3130">Le nombre maximal de nœuds utilisés simultanément pour exécuter le travail.</span><span class="sxs-lookup"><span data-stu-id="40a79-3130">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="40a79-3131">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3131">No</span></span> |
| <span data-ttu-id="40a79-3132">priority</span><span class="sxs-lookup"><span data-stu-id="40a79-3132">priority</span></span> |<span data-ttu-id="40a79-3133">Détermine les travaux parmi tous ceux qui sont en file d'attente qui doivent être sélectionnés pour s'exécuter en premier.</span><span class="sxs-lookup"><span data-stu-id="40a79-3133">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="40a79-3134">Plus le numéro est faible, plus la priorité est élevée.</span><span class="sxs-lookup"><span data-stu-id="40a79-3134">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="40a79-3135">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3135">No</span></span> |
| <span data-ttu-id="40a79-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="40a79-3136">parameters</span></span> |<span data-ttu-id="40a79-3137">Paramètres du script U-SQL</span><span class="sxs-lookup"><span data-stu-id="40a79-3137">Parameters for the U-SQL script</span></span> |<span data-ttu-id="40a79-3138">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="40a79-3139">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="40a79-3140">Pour plus d’informations, consultez [Activité U-SQL Data Lake Analytics](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="40a79-3141">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="40a79-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="40a79-3142">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-3142">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="40a79-3143">La propriété de type de l’activité doit être : **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3143">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="40a79-3144">Vous devez créer un des services liés suivants et spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName** :</span><span class="sxs-lookup"><span data-stu-id="40a79-3144">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="40a79-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="40a79-3145">SQL Server</span></span> 
- <span data-ttu-id="40a79-3146">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40a79-3146">Azure SQL Database</span></span>
- <span data-ttu-id="40a79-3147">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="40a79-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="40a79-3148">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur SqlServerStoredProcedure :</span><span class="sxs-lookup"><span data-stu-id="40a79-3148">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="40a79-3149">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-3149">Property</span></span> | <span data-ttu-id="40a79-3150">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-3150">Description</span></span> | <span data-ttu-id="40a79-3151">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a79-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="40a79-3152">storedProcedureName</span></span> |<span data-ttu-id="40a79-3153">Spécifiez le nom de la procédure stockée dans la base de données SQL Azure ou l'entrepôt Azure SQL Data Warehouse qui est représenté(e) par le service lié utilisé par la table de sortie.</span><span class="sxs-lookup"><span data-stu-id="40a79-3153">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="40a79-3154">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3154">Yes</span></span> |
| <span data-ttu-id="40a79-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40a79-3155">storedProcedureParameters</span></span> |<span data-ttu-id="40a79-3156">Spécifiez les valeurs des paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="40a79-3157">Si vous avez besoin de passer null pour un paramètre, utilisez la syntaxe : "param1": null (le tout en minuscules).</span><span class="sxs-lookup"><span data-stu-id="40a79-3157">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="40a79-3158">Consultez l’exemple suivant pour en savoir plus sur l’utilisation de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="40a79-3158">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="40a79-3159">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3159">No</span></span> |

<span data-ttu-id="40a79-3160">Si vous spécifiez un jeu de données d’entrée, il doit être disponible (à l’état Prêt) pour l’activité de procédure stockée à exécuter.</span><span class="sxs-lookup"><span data-stu-id="40a79-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="40a79-3161">Les jeux de données d’entrée ne peuvent pas être utilisés dans la procédure stockée en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="40a79-3161">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="40a79-3162">Cela sert uniquement à vérifier la dépendance avant de commencer l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-3162">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="40a79-3163">Vous devez spécifier un jeu de données de sortie pour une activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="40a79-3164">Le jeu de données de sortie spécifie la **planification** pour l’activité de procédure stockée (horaire, hebdomadaire, mensuelle, etc.).</span><span class="sxs-lookup"><span data-stu-id="40a79-3164">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="40a79-3165">Le jeu de données de sortie doit utiliser un **service lié** qui fait référence à une base de données Azure SQL, à un Azure SQL Data Warehouse ou à une base de données SQL Server dans laquelle vous souhaitez que la procédure stockée soit exécutée.</span><span class="sxs-lookup"><span data-stu-id="40a79-3165">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="40a79-3166">Le jeu de données de sortie peut être un moyen de passer le résultat de la procédure stockée pour traitement ultérieur par une autre activité ([chaînage des activités](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="40a79-3166">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="40a79-3167">Toutefois, Data Factory n’écrit pas automatiquement la sortie d’une procédure stockée pour ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="40a79-3167">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="40a79-3168">C’est la procédure stockée qui écrit dans une table SQL vers laquelle le jeu de données de sortie pointe.</span><span class="sxs-lookup"><span data-stu-id="40a79-3168">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="40a79-3169">Dans certains cas, le jeu de données de sortie peut être un **jeu de données factice**, qui est utilisé uniquement pour spécifier le calendrier d’exécution de l’activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="40a79-3169">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="40a79-3170">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-3170">JSON example</span></span>

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="40a79-3171">Pour plus de détails, consultez l’article [Stored Procedure Activity (activité de procédure stockée)](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="40a79-3172">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="40a79-3172">.NET custom activity</span></span>
<span data-ttu-id="40a79-3173">Vous pouvez spécifier les propriétés suivantes dans une définition JSON d’activité personnalisée .NET.</span><span class="sxs-lookup"><span data-stu-id="40a79-3173">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="40a79-3174">La propriété de type de l’activité doit être : **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3174">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="40a79-3175">Vous devez créer un service lié Azure HDInsight ou Azure Batch et spécifier le nom de celui-ci en tant que valeur de la propriété **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40a79-3176">Les propriétés suivantes sont prises en charge dans la section **typeProperties** lorsque vous définissez le type d’activité sur DotNetActivity :</span><span class="sxs-lookup"><span data-stu-id="40a79-3176">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="40a79-3177">Propriété</span><span class="sxs-lookup"><span data-stu-id="40a79-3177">Property</span></span> | <span data-ttu-id="40a79-3178">Description</span><span class="sxs-lookup"><span data-stu-id="40a79-3178">Description</span></span> | <span data-ttu-id="40a79-3179">Requis</span><span class="sxs-lookup"><span data-stu-id="40a79-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40a79-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="40a79-3180">AssemblyName</span></span> | <span data-ttu-id="40a79-3181">Nom de l’assembly.</span><span class="sxs-lookup"><span data-stu-id="40a79-3181">Name of the assembly.</span></span> <span data-ttu-id="40a79-3182">Dans l’exemple, il s’agit de : **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3182">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="40a79-3183">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3183">Yes</span></span> |
| <span data-ttu-id="40a79-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="40a79-3184">EntryPoint</span></span> |<span data-ttu-id="40a79-3185">Nom de la classe qui implémente l’interface IDotNetActivity.</span><span class="sxs-lookup"><span data-stu-id="40a79-3185">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="40a79-3186">Dans l’exemple, il s’agit de : **MyDotNetActivityNS.MyDotNetActivity** où MyDotNetActivityNS est l’espace de noms et MyDotNetActivity est la classe.</span><span class="sxs-lookup"><span data-stu-id="40a79-3186">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="40a79-3187">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3187">Yes</span></span> | 
| <span data-ttu-id="40a79-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="40a79-3188">PackageLinkedService</span></span> | <span data-ttu-id="40a79-3189">Nom du service lié Stockage Azure qui pointe vers le stockage d’objets blob contenant le fichier .zip de l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="40a79-3189">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="40a79-3190">Dans cet exemple, il s’agit de : **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3190">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="40a79-3191">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3191">Yes</span></span> |
| <span data-ttu-id="40a79-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="40a79-3192">PackageFile</span></span> | <span data-ttu-id="40a79-3193">Nom du fichier zip.</span><span class="sxs-lookup"><span data-stu-id="40a79-3193">Name of the zip file.</span></span> <span data-ttu-id="40a79-3194">Dans l’exemple, il s’agit de : **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="40a79-3194">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="40a79-3195">Oui</span><span class="sxs-lookup"><span data-stu-id="40a79-3195">Yes</span></span> |
| <span data-ttu-id="40a79-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="40a79-3196">extendedProperties</span></span> | <span data-ttu-id="40a79-3197">Propriétés étendues que vous pouvez définir et transmettre au code .NET.</span><span class="sxs-lookup"><span data-stu-id="40a79-3197">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="40a79-3198">Dans cet exemple, la variable **SliceStart** est définie sur une valeur basée sur la variable système SliceStart.</span><span class="sxs-lookup"><span data-stu-id="40a79-3198">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="40a79-3199">Non</span><span class="sxs-lookup"><span data-stu-id="40a79-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="40a79-3200">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="40a79-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="40a79-3201">Pour plus d’informations, consultez l’article [Use custom activities in Data Factory (utiliser des activités personnalisées dans Azure Data Factory)](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="40a79-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="40a79-3202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40a79-3202">Next Steps</span></span>
<span data-ttu-id="40a79-3203">Consultez les didacticiels suivants :</span><span class="sxs-lookup"><span data-stu-id="40a79-3203">See the following tutorials:</span></span> 

- [<span data-ttu-id="40a79-3204">Didacticiel : créer un pipeline avec une activité de copie</span><span class="sxs-lookup"><span data-stu-id="40a79-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="40a79-3205">Didacticiel : créer un pipeline avec une activité Hive</span><span class="sxs-lookup"><span data-stu-id="40a79-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)