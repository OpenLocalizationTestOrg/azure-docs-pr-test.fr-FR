---
title: "aaaAzure Data Factory - référence des scripts JSON | Documents Microsoft"
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
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="0ccf0-103">Azure Data Factory - Référence de script JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="0ccf0-104">Cet article fournit des schémas JSON et des exemples pour la définition des entités Azure Data Factory (pipeline, activité, jeu de données et service lié).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="0ccf0-105">Pipeline</span><span class="sxs-lookup"><span data-stu-id="0ccf0-105">Pipeline</span></span> 
<span data-ttu-id="0ccf0-106">structure de haut niveau Hello pour une définition de pipeline est la suivante :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="0ccf0-107">Tableau suivant décrit les propriétés de hello au sein de la définition JSON du pipeline hello :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="0ccf0-108">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-108">Property</span></span> | <span data-ttu-id="0ccf0-109">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-109">Description</span></span> | <span data-ttu-id="0ccf0-110">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="0ccf0-111">name</span><span class="sxs-lookup"><span data-stu-id="0ccf0-111">name</span></span> | <span data-ttu-id="0ccf0-112">Nom du pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-112">Name of hello pipeline.</span></span> <span data-ttu-id="0ccf0-113">Spécifiez un nom qui représente l’action hello hello activité ou le pipeline est configuré toodo</span><span class="sxs-lookup"><span data-stu-id="0ccf0-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="0ccf0-114">Nombre maximal de caractères : 260</span><span class="sxs-lookup"><span data-stu-id="0ccf0-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="0ccf0-115">Doit commencer par une lettre, un chiffre ou un trait de soulignement (_)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="0ccf0-116">Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</span><span class="sxs-lookup"><span data-stu-id="0ccf0-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="0ccf0-117">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-117">Yes</span></span> |
| <span data-ttu-id="0ccf0-118">description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-118">description</span></span> |<span data-ttu-id="0ccf0-119">Texte décrivant les activité hello ou un pipeline est utilisé pour</span><span class="sxs-lookup"><span data-stu-id="0ccf0-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="0ccf0-120">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-120">No</span></span> |
| <span data-ttu-id="0ccf0-121">activités</span><span class="sxs-lookup"><span data-stu-id="0ccf0-121">activities</span></span> | <span data-ttu-id="0ccf0-122">Contient une liste d’activités.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-122">Contains a list of activities.</span></span> | <span data-ttu-id="0ccf0-123">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-123">Yes</span></span> |
| <span data-ttu-id="0ccf0-124">start</span><span class="sxs-lookup"><span data-stu-id="0ccf0-124">start</span></span> |<span data-ttu-id="0ccf0-125">Date-heure de début pour le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="0ccf0-126">Doit se trouver au [format ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="0ccf0-127">Par exemple : 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="0ccf0-128">Il est possible de toospecify une heure locale, par exemple une heure EST.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="0ccf0-129">Voici un exemple : `2016-02-27T06:00:00**-05:00`, qui correspond à 6h EST.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="0ccf0-130">Hello propriétés start et end spécifient ensemble la période active pour le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="0ccf0-131">Les tranches de sortie sont uniquement générées pendant cette période active.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="0ccf0-132">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-132">No</span></span><br/><br/><span data-ttu-id="0ccf0-133">Si vous spécifiez une valeur pour la propriété de fin hello, vous devez spécifier la valeur de propriété de début hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="0ccf0-134">Hello heures de début et de fin peuvent tous deux être vide toocreate un pipeline.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="0ccf0-135">Vous devez spécifier les deux valeurs tooset une période active pour hello pipeline toorun.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="0ccf0-136">Si vous ne spécifiez pas les heures de début et de fin lors de la création d’un pipeline, vous pouvez les définir à l’aide d’applet de commande hello ensemble-AzureRmDataFactoryPipelineActivePeriod plus tard.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="0ccf0-137">end</span><span class="sxs-lookup"><span data-stu-id="0ccf0-137">end</span></span> |<span data-ttu-id="0ccf0-138">Date-heure de fin pour le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="0ccf0-139">Si spécifiée, doit être au format ISO.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-139">If specified must be in ISO format.</span></span> <span data-ttu-id="0ccf0-140">Par exemple : 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="0ccf0-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="0ccf0-141">Il est possible de toospecify une heure locale, par exemple une heure EST.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="0ccf0-142">Voici un exemple : `2016-02-27T06:00:00**-05:00`, qui correspond à 6h EST.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="0ccf0-143">pipeline de hello toorun spécifiez indéfiniment, 9999-09-09 en tant que valeur hello pour la propriété de fin hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="0ccf0-144">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-144">No</span></span> <br/><br/><span data-ttu-id="0ccf0-145">Si vous spécifiez une valeur pour la propriété de démarrage hello, vous devez spécifier la valeur de propriété de fin hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="0ccf0-146">Consultez les remarques pour hello **Démarrer** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="0ccf0-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="0ccf0-147">isPaused</span></span> |<span data-ttu-id="0ccf0-148">Si set tootrue hello pipeline ne s’exécute pas.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="0ccf0-149">Valeur par défaut = false.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-149">Default value = false.</span></span> <span data-ttu-id="0ccf0-150">Vous pouvez utiliser cette propriété tooenable ou désactiver.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="0ccf0-151">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-151">No</span></span> |
| <span data-ttu-id="0ccf0-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="0ccf0-152">pipelineMode</span></span> |<span data-ttu-id="0ccf0-153">méthode Hello pour la planification s’exécute pour le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="0ccf0-154">Les valeurs autorisées sont : scheduled (par défaut) et onetime.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="0ccf0-155">'Planifiée' indique ce pipeline hello s’exécute sur un intervalle de temps spécifié selon la période active de tooits (heure de début et de fin).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="0ccf0-156">« Unique » indique que ce pipeline hello s’exécute qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="0ccf0-157">Une fois créés, les pipelines de type onetime ne peuvent pas être modifiés ni mis à jour pour le moment.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="0ccf0-158">Consultez la page [Pipeline onetime](data-factory-create-pipelines.md#onetime-pipeline) pour plus d’informations sur le paramètre onetime.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="0ccf0-159">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-159">No</span></span> |
| <span data-ttu-id="0ccf0-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="0ccf0-160">expirationTime</span></span> |<span data-ttu-id="0ccf0-161">Durée de temps après sa création pour le hello pipeline est valide et doit rester mis en service.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="0ccf0-162">Si elle n’a pas tout actif, échec, ou en attente d’exécution, le pipeline de hello est supprimé automatiquement lorsqu’il atteint le délai d’expiration de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="0ccf0-163">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="0ccf0-164">Activité</span><span class="sxs-lookup"><span data-stu-id="0ccf0-164">Activity</span></span> 
<span data-ttu-id="0ccf0-165">structure de haut niveau Hello pour une activité dans une définition de pipeline (élément activités) est la suivante :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="0ccf0-166">Tableau suivant décrivent les propriétés hello dans l’activité hello définition JSON :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="0ccf0-167">Tag</span><span class="sxs-lookup"><span data-stu-id="0ccf0-167">Tag</span></span> | <span data-ttu-id="0ccf0-168">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-168">Description</span></span> | <span data-ttu-id="0ccf0-169">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-170">name</span><span class="sxs-lookup"><span data-stu-id="0ccf0-170">name</span></span> |<span data-ttu-id="0ccf0-171">Nom de l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-171">Name of hello activity.</span></span> <span data-ttu-id="0ccf0-172">Spécifiez un nom qui représente l’action de hello activité hello est configuré toodo</span><span class="sxs-lookup"><span data-stu-id="0ccf0-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="0ccf0-173">Nombre maximal de caractères : 260</span><span class="sxs-lookup"><span data-stu-id="0ccf0-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="0ccf0-174">Doit commencer par une lettre, un chiffre ou un trait de soulignement (_)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="0ccf0-175">Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</span><span class="sxs-lookup"><span data-stu-id="0ccf0-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="0ccf0-176">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-176">Yes</span></span> |
| <span data-ttu-id="0ccf0-177">description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-177">description</span></span> |<span data-ttu-id="0ccf0-178">Texte décrivant de quelle activité hello est destiné.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="0ccf0-179">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-179">Yes</span></span> |
| <span data-ttu-id="0ccf0-180">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-180">type</span></span> |<span data-ttu-id="0ccf0-181">Spécifie le type hello d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="0ccf0-182">Consultez hello [banques de données](#data-stores) et [activités de TRANSFORMATION des données](#data-transformation-activities) sections pour les différents types d’activités.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="0ccf0-183">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-183">Yes</span></span> |
| <span data-ttu-id="0ccf0-184">inputs</span><span class="sxs-lookup"><span data-stu-id="0ccf0-184">inputs</span></span> |<span data-ttu-id="0ccf0-185">Tables d’entrée utilisés par l’activité hello</span><span class="sxs-lookup"><span data-stu-id="0ccf0-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="0ccf0-186">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-186">Yes</span></span> |
| <span data-ttu-id="0ccf0-187">outputs</span><span class="sxs-lookup"><span data-stu-id="0ccf0-187">outputs</span></span> |<span data-ttu-id="0ccf0-188">Tables de sortie utilisés par l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="0ccf0-189">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-189">Yes</span></span> |
| <span data-ttu-id="0ccf0-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-190">linkedServiceName</span></span> |<span data-ttu-id="0ccf0-191">Nom du service hello lié utilisé par l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="0ccf0-192">Une activité peut nécessiter que vous spécifiez service hello lié qui lie l’environnement de calcul requis toohello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="0ccf0-193">Oui pour les activités HDInsight, les activités de Azure Machine Learning et les activités de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="0ccf0-194">Non pour toutes les autres</span><span class="sxs-lookup"><span data-stu-id="0ccf0-194">No for all others</span></span> |
| <span data-ttu-id="0ccf0-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="0ccf0-195">typeProperties</span></span> |<span data-ttu-id="0ccf0-196">Propriétés dans la section de typeProperties hello dépendent du type d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="0ccf0-197">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-197">No</span></span> |
| <span data-ttu-id="0ccf0-198">policy</span><span class="sxs-lookup"><span data-stu-id="0ccf0-198">policy</span></span> |<span data-ttu-id="0ccf0-199">Stratégies qui affectent le comportement d’exécution hello d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="0ccf0-200">Si aucune valeur n’est spécifiée, les stratégies par défaut sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="0ccf0-201">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-201">No</span></span> |
| <span data-ttu-id="0ccf0-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="0ccf0-202">scheduler</span></span> |<span data-ttu-id="0ccf0-203">propriété de « planificateur » est utilisé toodefine souhaité pour l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="0ccf0-204">Sous-propriétés sont hello identique à celle de hello hello [propriété de disponibilité dans un jeu de données](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="0ccf0-205">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="0ccf0-206">Stratégies</span><span class="sxs-lookup"><span data-stu-id="0ccf0-206">Policies</span></span>
<span data-ttu-id="0ccf0-207">Stratégies affectent le comportement d’exécution hello d’une activité, en particulier lors du traitement de hello une tranche de table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="0ccf0-208">Hello tableau suivant fournit des détails de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="0ccf0-209">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-209">Property</span></span> | <span data-ttu-id="0ccf0-210">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-210">Permitted values</span></span> | <span data-ttu-id="0ccf0-211">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="0ccf0-211">Default Value</span></span> | <span data-ttu-id="0ccf0-212">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-213">accès concurrentiel</span><span class="sxs-lookup"><span data-stu-id="0ccf0-213">concurrency</span></span> |<span data-ttu-id="0ccf0-214">Entier </span><span class="sxs-lookup"><span data-stu-id="0ccf0-214">Integer</span></span> <br/><br/><span data-ttu-id="0ccf0-215">Valeur max : 10</span><span class="sxs-lookup"><span data-stu-id="0ccf0-215">Max value: 10</span></span> |<span data-ttu-id="0ccf0-216">1</span><span class="sxs-lookup"><span data-stu-id="0ccf0-216">1</span></span> |<span data-ttu-id="0ccf0-217">Nombre d’exécutions simultanées de l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="0ccf0-218">Il détermine le nombre de hello d’exécutions d’activité parallèles qui peuvent se produire sur différentes tranches.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="0ccf0-219">Par exemple, si une activité doit toogo via un grand ensemble de données disponibles, une plus grande valeur d’accès concurrentiel accélère le traitement des données hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="0ccf0-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="0ccf0-220">executionPriorityOrder</span></span> |<span data-ttu-id="0ccf0-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="0ccf0-221">NewestFirst</span></span><br/><br/><span data-ttu-id="0ccf0-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="0ccf0-222">OldestFirst</span></span> |<span data-ttu-id="0ccf0-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="0ccf0-223">OldestFirst</span></span> |<span data-ttu-id="0ccf0-224">Détermine hello classement de tranches de données qui sont en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="0ccf0-225">Par exemple, si vous avez 2 segments (l’un se produisant à 16 heures et l’autre à 17 heures) et que les deux sont en attente d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="0ccf0-226">Si vous définissez hello executionPriorityOrder toobe NewestFirst, tranche hello à 17 h 00 est traitée en premier.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="0ccf0-227">Même si vous définissez executionPriorityORder de hello toobe OldestFIrst, tranche hello à 16 h 00 est traité.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="0ccf0-228">retry</span><span class="sxs-lookup"><span data-stu-id="0ccf0-228">retry</span></span> |<span data-ttu-id="0ccf0-229">Entier </span><span class="sxs-lookup"><span data-stu-id="0ccf0-229">Integer</span></span><br/><br/><span data-ttu-id="0ccf0-230">La valeur max peut être 10</span><span class="sxs-lookup"><span data-stu-id="0ccf0-230">Max value can be 10</span></span> |<span data-ttu-id="0ccf0-231">0</span><span class="sxs-lookup"><span data-stu-id="0ccf0-231">0</span></span> |<span data-ttu-id="0ccf0-232">Nombre de tentatives avant le traitement des données de la tranche de hello hello est marqué comme défectueux.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="0ccf0-233">Exécution de l’activité pour une tranche de données est retentée des toohello spécifié nombre de tentatives.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="0ccf0-234">nouvelle tentative de Hello est faite dès que possible après l’échec de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="0ccf0-235">timeout</span><span class="sxs-lookup"><span data-stu-id="0ccf0-235">timeout</span></span> |<span data-ttu-id="0ccf0-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ccf0-236">TimeSpan</span></span> |<span data-ttu-id="0ccf0-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="0ccf0-237">00:00:00</span></span> |<span data-ttu-id="0ccf0-238">Délai d’expiration pour l’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-238">Timeout for hello activity.</span></span> <span data-ttu-id="0ccf0-239">Exemple : 00:10:00 (implique un délai d’expiration de 10 minutes)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="0ccf0-240">Si une valeur n’est pas spécifiée ou est égal à 0, hello est infini.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="0ccf0-241">Si le temps de traitement de données hello sur une tranche dépasse la valeur de délai d’attente de hello, elle est annulée et le traitement de hello tooretry tente de système de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="0ccf0-242">nombre de Hello de nouvelles tentatives dépend de la propriété de nouvelle tentative hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="0ccf0-243">En cas de délai d’attente, état de hello a la valeur tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="0ccf0-244">delay</span><span class="sxs-lookup"><span data-stu-id="0ccf0-244">delay</span></span> |<span data-ttu-id="0ccf0-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ccf0-245">TimeSpan</span></span> |<span data-ttu-id="0ccf0-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="0ccf0-246">00:00:00</span></span> |<span data-ttu-id="0ccf0-247">Spécifier le délai de hello avant le traitement des données de hello tranche commence.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="0ccf0-248">exécution de Hello d’activité pour une tranche de données est démarrée une fois hello délai passé hello attendu des temps d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="0ccf0-249">Exemple : 00:10:00 (implique un délai de 10 minutes)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="0ccf0-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="0ccf0-250">longRetry</span></span> |<span data-ttu-id="0ccf0-251">Entier </span><span class="sxs-lookup"><span data-stu-id="0ccf0-251">Integer</span></span><br/><br/><span data-ttu-id="0ccf0-252">Valeur max : 10</span><span class="sxs-lookup"><span data-stu-id="0ccf0-252">Max value: 10</span></span> |<span data-ttu-id="0ccf0-253">1</span><span class="sxs-lookup"><span data-stu-id="0ccf0-253">1</span></span> |<span data-ttu-id="0ccf0-254">nombre de Hello de long tentatives avant l’échec de l’exécution de la tranche hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="0ccf0-255">Les tentatives longRetry sont espacées par longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="0ccf0-256">Par conséquent, si vous devez toospecify une heure entre chaque tentative, utilisez longRetry.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="0ccf0-257">Si les valeurs Retry et longRetry sont spécifiées, chaque tentative longRetry inclut de nouvelles tentatives et le nombre maximal de hello de tentatives est de nouvelle tentative * longRetry.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="0ccf0-258">Par exemple, si nous avons hello suivant les paramètres de stratégie d’activité hello :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="0ccf0-259">Retry : 3</span><span class="sxs-lookup"><span data-stu-id="0ccf0-259">Retry: 3</span></span><br/><span data-ttu-id="0ccf0-260">longRetry : 2</span><span class="sxs-lookup"><span data-stu-id="0ccf0-260">longRetry: 2</span></span><br/><span data-ttu-id="0ccf0-261">longRetryInterval : 01:00:00</span><span class="sxs-lookup"><span data-stu-id="0ccf0-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="0ccf0-262">Supposons qu’une seule tranche tooexecute (l’état est en attente) et de l’exécution de l’activité hello échoue à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="0ccf0-263">Au départ, il y aurait 3 tentatives consécutives d'exécution.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="0ccf0-264">Après chaque tentative, état hello de la tranche est Retry.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="0ccf0-265">Une fois les 3 premiers tentatives sur, état hello de la tranche est LongRetry.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="0ccf0-266">Après une heure (c’est-à-dire la valeur de longRetryInterval), il y aurait un autre ensemble de 3 tentatives consécutives d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="0ccf0-267">Après cela, état de la tranche hello est Failed et aucune nouvelle tentative n’a lieu.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="0ccf0-268">Par conséquent, 6 tentatives ont été exécutées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="0ccf0-269">Si toute exécution réussit, état de la tranche hello est prêt et aucune nouvelle tentative n’est tentées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="0ccf0-270">longRetry peut être utilisé dans les situations où les données dépendantes arrivent à des moments non déterministe ou hello environnement global est instable sous laquelle le traitement de données se produit.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="0ccf0-271">Dans ce cas, effectuant une après l’autre les nouvelles tentatives ne permettra pas de, et cela après un intervalle de résultats en temps Bonjour souhaitée de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="0ccf0-272">Mise en garde : ne définissez pas de valeurs élevées pour longRetry ou longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="0ccf0-273">En règle générale, des valeurs plus élevées impliquent d’autres problèmes systémiques.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="0ccf0-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="0ccf0-274">longRetryInterval</span></span> |<span data-ttu-id="0ccf0-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ccf0-275">TimeSpan</span></span> |<span data-ttu-id="0ccf0-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="0ccf0-276">00:00:00</span></span> |<span data-ttu-id="0ccf0-277">délai de Hello entre les nouvelles tentatives longues</span><span class="sxs-lookup"><span data-stu-id="0ccf0-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="0ccf0-278">Section typeProperties</span><span class="sxs-lookup"><span data-stu-id="0ccf0-278">typeProperties section</span></span>
<span data-ttu-id="0ccf0-279">section de typeProperties Hello est différente pour chaque activité.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="0ccf0-280">Les activités de transformation ont uniquement des propriétés de type hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="0ccf0-281">Consultez la section [Activités de transformation des données](#data-transformation-activities) dans cet article pour obtenir des exemples JSON qui définissent les activités de transformation dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="0ccf0-282">**Activité de copie** a deux sous-sections suivantes dans la section de typeProperties hello : **source** et **récepteur**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="0ccf0-283">Consultez [banques de données](#data-stores) section de cet article pour JSON exemples qui montrent comment stocker des toouse données comme une source et/ou un récepteur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="0ccf0-284">Exemple de pipeline de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-284">Sample copy pipeline</span></span>
<span data-ttu-id="0ccf0-285">Bonjour suivant l’exemple de pipeline, il existe une activité de type **copie** Bonjour **activités** section.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="0ccf0-286">Dans cet exemple, hello [activité de copie](data-factory-data-movement-activities.md) copie les données à partir d’une base de données SQL Azure de tooan stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
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

<span data-ttu-id="0ccf0-287">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-287">Note hello following points:</span></span>

* <span data-ttu-id="0ccf0-288">Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="0ccf0-289">Entrée d’activité hello est définie trop**InputDataset** et de sortie d’activité hello est définie trop**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="0ccf0-290">Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="0ccf0-291">Consultez [banques de données](#data-stores) section de cet article pour JSON exemples qui montrent comment stocker des toouse données comme une source et/ou un récepteur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="0ccf0-292">Pour obtenir une description complète de la création de ce pipeline, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="0ccf0-293">Exemple de pipeline de transformation</span><span class="sxs-lookup"><span data-stu-id="0ccf0-293">Sample transformation pipeline</span></span>
<span data-ttu-id="0ccf0-294">Bonjour suivant l’exemple de pipeline, il existe une activité de type **HDInsightHive** Bonjour **activités** section.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="0ccf0-295">Dans cet exemple, hello [activité HDInsight Hive](data-factory-hive-activity.md) transforme les données d’un stockage d’objets Blob Azure en exécutant un fichier de script Hive sur un cluster Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="0ccf0-296">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-296">Note hello following points:</span></span> 

* <span data-ttu-id="0ccf0-297">Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="0ccf0-298">fichier de script Hive Hello, **partitionweblogs.hql**, est stocké dans hello compte de stockage Azure (spécifié par scriptLinkedService hello, appelé **AzureStorageLinkedService**) et dans  **script** dossier dans le conteneur de hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="0ccf0-299">Hello **définit** section est de paramètres d’exécution utilisés toospecify hello script hive de toohello passés en tant que valeurs de configuration Hive (par exemple `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="0ccf0-300">Consultez la section [Activités de transformation des données](#data-transformation-activities) dans cet article pour obtenir des exemples JSON qui définissent les activités de transformation dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="0ccf0-301">Pour obtenir une description complète de la création de ce pipeline, consultez [didacticiel : créer vos premières données tooprocess de pipeline à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="0ccf0-302">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-302">Linked service</span></span>
<span data-ttu-id="0ccf0-303">structure de haut niveau Hello pour une définition de service lié est comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="0ccf0-304">Tableau suivant décrivent les propriétés hello dans l’activité hello définition JSON :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="0ccf0-305">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-305">Property</span></span> | <span data-ttu-id="0ccf0-306">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-306">Description</span></span> | <span data-ttu-id="0ccf0-307">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="0ccf0-308">name</span><span class="sxs-lookup"><span data-stu-id="0ccf0-308">name</span></span> | <span data-ttu-id="0ccf0-309">Nom du service de hello lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-309">Name of hello linked service.</span></span> | <span data-ttu-id="0ccf0-310">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-310">Yes</span></span> | 
| <span data-ttu-id="0ccf0-311">propriétés - type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-311">properties - type</span></span> | <span data-ttu-id="0ccf0-312">Type de service de hello lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-312">Type of hello linked service.</span></span> <span data-ttu-id="0ccf0-313">Par exemple : Stockage Azure, Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="0ccf0-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="0ccf0-314">typeProperties</span></span> | <span data-ttu-id="0ccf0-315">section de typeProperties Hello comporte des éléments qui sont différents pour chaque magasin de données ou l’environnement de calcul.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="0ccf0-316">Consultez [banques de données](#datastores) section pour toutes les données hello magasin des services liés et [environnements de calcul](#compute-environments) pourquoi tous les services liés de calcul.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="0ccf0-317">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-317">Dataset</span></span> 
<span data-ttu-id="0ccf0-318">Un jeu de données dans Azure Data Factory est défini comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-318">A dataset in Azure Data Factory is defined as follows:</span></span>

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

<span data-ttu-id="0ccf0-319">Hello tableau suivant décrit les propriétés dans hello ci-dessus JSON :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="0ccf0-320">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-320">Property</span></span> | <span data-ttu-id="0ccf0-321">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-321">Description</span></span> | <span data-ttu-id="0ccf0-322">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-322">Required</span></span> | <span data-ttu-id="0ccf0-323">Default</span><span class="sxs-lookup"><span data-stu-id="0ccf0-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-324">name</span><span class="sxs-lookup"><span data-stu-id="0ccf0-324">name</span></span> | <span data-ttu-id="0ccf0-325">Nom du jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-325">Name of hello dataset.</span></span> <span data-ttu-id="0ccf0-326">Pour connaître les règles d’affectation des noms, voir [Azure Data Factory - Règles d’affectation des noms](data-factory-naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="0ccf0-327">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-327">Yes</span></span> |<span data-ttu-id="0ccf0-328">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-328">NA</span></span> |
| <span data-ttu-id="0ccf0-329">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-329">type</span></span> | <span data-ttu-id="0ccf0-330">Type de jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-330">Type of hello dataset.</span></span> <span data-ttu-id="0ccf0-331">Spécifiez un des types hello pris en charge par Azure Data Factory (par exemple : AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="0ccf0-332">Consultez [banques de données](#data-stores) section tous hello banques de données et les types de jeu de données pris en charge par la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="0ccf0-333">structure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-333">structure</span></span> | <span data-ttu-id="0ccf0-334">Schéma du jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-334">Schema of hello dataset.</span></span> <span data-ttu-id="0ccf0-335">Il contient des colonnes, leurs types, etc.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="0ccf0-336">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-336">No</span></span> |<span data-ttu-id="0ccf0-337">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-337">NA</span></span> |
| <span data-ttu-id="0ccf0-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="0ccf0-338">typeProperties</span></span> | <span data-ttu-id="0ccf0-339">Les propriétés correspondant toohello le type sélectionné.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="0ccf0-340">Consultez la section [Magasins de données](#data-stores) pour en savoir plus sur les types pris en charge et leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="0ccf0-341">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-341">Yes</span></span> |<span data-ttu-id="0ccf0-342">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-342">NA</span></span> |
| <span data-ttu-id="0ccf0-343">external</span><span class="sxs-lookup"><span data-stu-id="0ccf0-343">external</span></span> | <span data-ttu-id="0ccf0-344">Indicateur booléen toospecify si un jeu de données est explicitement généré par un pipeline de fabrique de données ou non.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="0ccf0-345">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-345">No</span></span> |<span data-ttu-id="0ccf0-346">false</span><span class="sxs-lookup"><span data-stu-id="0ccf0-346">false</span></span> |
| <span data-ttu-id="0ccf0-347">availability</span><span class="sxs-lookup"><span data-stu-id="0ccf0-347">availability</span></span> | <span data-ttu-id="0ccf0-348">Définit hello du traitement de fenêtre ou hello le découpage du modèle pour la production de dataset hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="0ccf0-349">Pour plus d’informations sur le dataset hello le découpage du modèle, consultez [de planification et de l’exécution](data-factory-scheduling-and-execution.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="0ccf0-350">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-350">Yes</span></span> |<span data-ttu-id="0ccf0-351">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-351">NA</span></span> |
| <span data-ttu-id="0ccf0-352">policy</span><span class="sxs-lookup"><span data-stu-id="0ccf0-352">policy</span></span> |<span data-ttu-id="0ccf0-353">Définit les critères de hello ou une condition hello tranches de dataset hello doivent répondre.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="0ccf0-354">Pour plus d’informations, consultez la section [Disponibilité du jeu de données](#Policy) .</span><span class="sxs-lookup"><span data-stu-id="0ccf0-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="0ccf0-355">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-355">No</span></span> |<span data-ttu-id="0ccf0-356">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-356">NA</span></span> |

<span data-ttu-id="0ccf0-357">Chaque colonne de hello **structure** section contient hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="0ccf0-358">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-358">Property</span></span> | <span data-ttu-id="0ccf0-359">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-359">Description</span></span> | <span data-ttu-id="0ccf0-360">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-361">name</span><span class="sxs-lookup"><span data-stu-id="0ccf0-361">name</span></span> |<span data-ttu-id="0ccf0-362">Nom de colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-362">Name of hello column.</span></span> |<span data-ttu-id="0ccf0-363">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-363">Yes</span></span> |
| <span data-ttu-id="0ccf0-364">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-364">type</span></span> |<span data-ttu-id="0ccf0-365">Type de données de colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-365">Data type of hello column.</span></span>  |<span data-ttu-id="0ccf0-366">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-366">No</span></span> |
| <span data-ttu-id="0ccf0-367">culture</span><span class="sxs-lookup"><span data-stu-id="0ccf0-367">culture</span></span> |<span data-ttu-id="0ccf0-368">.NET basé toobe culture utilisée lorsque le type est spécifié et qu’il est de type .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="0ccf0-369">La valeur par défaut est `en-us`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-369">Default is `en-us`.</span></span> |<span data-ttu-id="0ccf0-370">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-370">No</span></span> |
| <span data-ttu-id="0ccf0-371">format</span><span class="sxs-lookup"><span data-stu-id="0ccf0-371">format</span></span> |<span data-ttu-id="0ccf0-372">Mettre en forme toobe de chaîne utilisé lorsque le type est spécifié et qu’il est de type .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="0ccf0-373">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-373">No</span></span> |

<span data-ttu-id="0ccf0-374">Dans l’exemple suivant de hello, jeu de données hello possède trois colonnes `slicetimestamp`, `projectname`, et `pageviews` et ils sont de type : chaîne, chaîne et Decimal respectivement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="0ccf0-375">Hello tableau suivant décrit les propriétés que vous pouvez utiliser Bonjour **disponibilité** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="0ccf0-376">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-376">Property</span></span> | <span data-ttu-id="0ccf0-377">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-377">Description</span></span> | <span data-ttu-id="0ccf0-378">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-378">Required</span></span> | <span data-ttu-id="0ccf0-379">Default</span><span class="sxs-lookup"><span data-stu-id="0ccf0-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-380">frequency</span><span class="sxs-lookup"><span data-stu-id="0ccf0-380">frequency</span></span> |<span data-ttu-id="0ccf0-381">Spécifie l’unité de temps hello pour la production de tranche de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="0ccf0-382"><b>Fréquence prise en charge</b>: minute, heure, jour, semaine, mois</span><span class="sxs-lookup"><span data-stu-id="0ccf0-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="0ccf0-383">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-383">Yes</span></span> |<span data-ttu-id="0ccf0-384">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-384">NA</span></span> |
| <span data-ttu-id="0ccf0-385">interval</span><span class="sxs-lookup"><span data-stu-id="0ccf0-385">interval</span></span> |<span data-ttu-id="0ccf0-386">Spécifie un multiplicateur de fréquence</span><span class="sxs-lookup"><span data-stu-id="0ccf0-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="0ccf0-387">« Intervalle de fréquence x » détermine la fréquence à laquelle hello tranche est produite.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="0ccf0-388">Si vous avez besoin de hello toobe dataset découpée sur toutes les heures, vous définissez <b>fréquence</b> trop<b>heure</b>, et <b>intervalle</b> trop<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="0ccf0-389"><b>Remarque</b>: Si vous spécifiez la fréquence de minutes, nous vous recommandons de définir hello intervalle toono inférieur à 15</span><span class="sxs-lookup"><span data-stu-id="0ccf0-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="0ccf0-390">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-390">Yes</span></span> |<span data-ttu-id="0ccf0-391">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-391">NA</span></span> |
| <span data-ttu-id="0ccf0-392">style</span><span class="sxs-lookup"><span data-stu-id="0ccf0-392">style</span></span> |<span data-ttu-id="0ccf0-393">Spécifie si la tranche de hello doit être produite au hello début/fin d’intervalle de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="0ccf0-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="0ccf0-394">StartOfInterval</span></span></li><li><span data-ttu-id="0ccf0-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="0ccf0-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="0ccf0-396">Si tooMonth est définie à la fréquence et le style a la valeur tooEndOfInterval, hello tranche est produite hello dernier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="0ccf0-397">Si le style de hello a la valeur tooStartOfInterval, hello tranche est produite hello premier jour du mois.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="0ccf0-398">Si tooDay est définie à la fréquence et le style a la valeur tooEndOfInterval, tranche de hello est produite dans hello dernière heure du jour de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="0ccf0-399">Si tooHour est définie à la fréquence et le style a la valeur tooEndOfInterval, tranche de hello est produite à fin hello d’heure de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="0ccf0-400">Par exemple, pour une tranche de période de 13 h 00 à 14 h 00, la tranche de hello est produite à 14 heures.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="0ccf0-401">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-401">No</span></span> |<span data-ttu-id="0ccf0-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="0ccf0-402">EndOfInterval</span></span> |
| <span data-ttu-id="0ccf0-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="0ccf0-403">anchorDateTime</span></span> |<span data-ttu-id="0ccf0-404">Définit la position absolue de hello dans le temps utilisé par les limites de la section Planificateur toocompute jeu de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="0ccf0-405"><b>Remarque</b>: si hello AnchorDateTime comporte des parties de date qui sont plus précis que la fréquence de hello, hello plus granulaires parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="0ccf0-406">Par exemple, si hello <b>intervalle</b> est <b>toutes les heures</b> (fréquence : heure et intervalle : 1) et hello <b>AnchorDateTime</b> contient <b>minutes et secondes</b>puis hello <b>minutes et secondes</b> parties Hello AnchorDateTime sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="0ccf0-407">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-407">No</span></span> |<span data-ttu-id="0ccf0-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="0ccf0-408">01/01/0001</span></span> |
| <span data-ttu-id="0ccf0-409">Offset</span><span class="sxs-lookup"><span data-stu-id="0ccf0-409">offset</span></span> |<span data-ttu-id="0ccf0-410">Intervalle de temps par le hello début et fin de toutes les tranches de jeu de données sont déplacées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="0ccf0-411"><b>Remarque</b>: si anchorDateTime et offset sont spécifiés, hello résulte hello combinée MAJ.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="0ccf0-412">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-412">No</span></span> |<span data-ttu-id="0ccf0-413">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-413">NA</span></span> |

<span data-ttu-id="0ccf0-414">Hello suivant la section disponibilité spécifie ce jeu de données de sortie hello est produit toutes les heures (ou) entrée jeu de données est disponible, toutes les heures :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="0ccf0-415">Hello **stratégie** section dans la définition de dataset définit des critères de hello ou condition hello hello tranches de jeu de données doit répondre.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="0ccf0-416">Nom de la stratégie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-416">Policy Name</span></span> | <span data-ttu-id="0ccf0-417">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-417">Description</span></span> | <span data-ttu-id="0ccf0-418">Appliqué trop</span><span class="sxs-lookup"><span data-stu-id="0ccf0-418">Applied too</span></span>| <span data-ttu-id="0ccf0-419">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-419">Required</span></span> | <span data-ttu-id="0ccf0-420">Default</span><span class="sxs-lookup"><span data-stu-id="0ccf0-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="0ccf0-421">minimumSizeMB</span></span> |<span data-ttu-id="0ccf0-422">Valide les données hello dans un **objets blob Azure** répond aux hello exigences de taille minimale (en mégaoctets).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="0ccf0-423">Objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-423">Azure Blob</span></span> |<span data-ttu-id="0ccf0-424">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-424">No</span></span> |<span data-ttu-id="0ccf0-425">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-425">NA</span></span> |
| <span data-ttu-id="0ccf0-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="0ccf0-426">minimumRows</span></span> |<span data-ttu-id="0ccf0-427">Valide les données hello dans un **base de données SQL Azure** ou un **table Azure** contient hello le nombre minimal de lignes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="0ccf0-428">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-428">Azure SQL Database</span></span></li><li><span data-ttu-id="0ccf0-429">table Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-429">Azure Table</span></span></li></ul> |<span data-ttu-id="0ccf0-430">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-430">No</span></span> |<span data-ttu-id="0ccf0-431">N/D</span><span class="sxs-lookup"><span data-stu-id="0ccf0-431">NA</span></span> |

<span data-ttu-id="0ccf0-432">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="0ccf0-433">À moins qu’un jeu de données ne soit généré par Azure Data Factory, il doit être marqué comme **external**(externe).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="0ccf0-434">Ce paramètre s’applique généralement toohello les entrées de la première activité dans un pipeline, sauf si l’activité ou le chaînage des propriétés de pipeline sont utilisé.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="0ccf0-435">Nom</span><span class="sxs-lookup"><span data-stu-id="0ccf0-435">Name</span></span> | <span data-ttu-id="0ccf0-436">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-436">Description</span></span> | <span data-ttu-id="0ccf0-437">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-437">Required</span></span> | <span data-ttu-id="0ccf0-438">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="0ccf0-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="0ccf0-439">dataDelay</span></span> |<span data-ttu-id="0ccf0-440">Vérification de hello toodelay temps sur la disponibilité de données externes de hello pour hello donné tranche hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="0ccf0-441">Par exemple, si les données de salutation sont disponibles, toutes les heures, hello vérification toosee hello externe des données sont disponibles et hello la tranche correspondante est prêt peut être différée à l’aide de dataDelay.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="0ccf0-442">S’applique uniquement toohello moment présent.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-442">Only applies toohello present time.</span></span>  <span data-ttu-id="0ccf0-443">Par exemple, si elle est de 1:00 PM maintenant et cette valeur est de 10 minutes, la validation hello démarre à 1 h 10.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="0ccf0-444">Ce paramètre n’affecte pas les tranches Bonjour passées (tranches Slice End Time + dataDelay < maintenant) sont traitées sans délai.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="0ccf0-445">Durée supérieure à 23:59 heures doivent toospecified à l’aide de hello `day.hours:minutes:seconds` format.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="0ccf0-446">Par exemple, toospecify 24 heures, n’utilisez pas 24:00:00 ; au lieu de cela, utilisez 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="0ccf0-447">Si vous utilisez 24:00:00, cette valeur est traitée comme 24 jours (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="0ccf0-448">Pour 1 jour et 4 heures, spécifiez 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="0ccf0-449">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-449">No</span></span> |<span data-ttu-id="0ccf0-450">0</span><span class="sxs-lookup"><span data-stu-id="0ccf0-450">0</span></span> |
| <span data-ttu-id="0ccf0-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="0ccf0-451">retryInterval</span></span> |<span data-ttu-id="0ccf0-452">temps d’attente Hello entre une défaillance et hello suivant nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="0ccf0-453">Si une tentative échoue, la prochaine tentative de hello est après retryInterval.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="0ccf0-454">S’il s’agit de 1:00 PM dès maintenant, nous commençons hello première tentative.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="0ccf0-455">Si hello durée toocomplete hello premier contrôle de validation est 1 minute et échoué de l’opération hello, nouvelle tentative suivante d’hello est à 1:00 + 1 min (durée) + 1 minute (intervalle avant nouvelle tentative) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="0ccf0-456">Aux tranches passées de hello, il n’existe aucun délai.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="0ccf0-457">nouvelle tentative de Hello se produit immédiatement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-457">hello retry happens immediately.</span></span> |<span data-ttu-id="0ccf0-458">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-458">No</span></span> |<span data-ttu-id="0ccf0-459">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="0ccf0-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="0ccf0-460">retryTimeout</span></span> |<span data-ttu-id="0ccf0-461">délai d’expiration de Hello pour chaque nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="0ccf0-462">Si cette propriété a la valeur too10 minutes, hello toobe de besoins de validation s’est terminée dans les 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="0ccf0-463">Si elle dure plus longtemps que la validation de 10 minutes tooperform hello, hello recommencez arrive à expiration.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="0ccf0-464">Si toutes les tentatives pour la validation de hello expire, la tranche de hello est marquée comme TimedOut.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="0ccf0-465">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-465">No</span></span> |<span data-ttu-id="0ccf0-466">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="0ccf0-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="0ccf0-467">maximumRetry</span></span> |<span data-ttu-id="0ccf0-468">Nombre de fois où toocheck pour la disponibilité de données externes de hello hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="0ccf0-469">Hello autorisé la valeur maximale est 10.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="0ccf0-470">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-470">No</span></span> |<span data-ttu-id="0ccf0-471">3</span><span class="sxs-lookup"><span data-stu-id="0ccf0-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="0ccf0-472">MAGASINS DE DONNÉES</span><span class="sxs-lookup"><span data-stu-id="0ccf0-472">DATA STORES</span></span>
<span data-ttu-id="0ccf0-473">Hello [service lié](#linked-service) descriptions section fournie pour les éléments JSON qui sont des types courants de tooall de services liés.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="0ccf0-474">Cette section fournit des détails sur les éléments JSON qui sont le magasin de données tooeach spécifique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="0ccf0-475">Hello [Dataset](#dataset) descriptions section fournie pour les éléments JSON qui sont des types courants de tooall des jeux de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="0ccf0-476">Cette section fournit des détails sur les éléments JSON qui sont le magasin de données tooeach spécifique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="0ccf0-477">Hello [activité](#activity) des descriptions de section fournie pour les éléments JSON qui sont des types tooall communs d’activités.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="0ccf0-478">Cette section fournit des détails sur les éléments JSON qui sont le magasin de données tooeach spécifique lorsqu’elle est utilisée comme un source/récepteur dans une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="0ccf0-479">Cliquez sur lien hello magasin hello vous intéressez dans les schémas JSON toosee hello pour le service lié, le jeu de données et hello source/récepteur pour l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="0ccf0-480">Catégorie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-480">Category</span></span> | <span data-ttu-id="0ccf0-481">Banque de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="0ccf0-482">**Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-482">**Azure**</span></span> |[<span data-ttu-id="0ccf0-483">stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="0ccf0-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0ccf0-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="0ccf0-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0ccf0-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="0ccf0-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0ccf0-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="0ccf0-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0ccf0-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="0ccf0-488">Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="0ccf0-489">Stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="0ccf0-490">**Bases de données**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-490">**Databases**</span></span> |[<span data-ttu-id="0ccf0-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="0ccf0-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="0ccf0-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="0ccf0-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="0ccf0-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="0ccf0-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="0ccf0-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="0ccf0-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="0ccf0-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="0ccf0-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="0ccf0-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="0ccf0-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="0ccf0-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0ccf0-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="0ccf0-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="0ccf0-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="0ccf0-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="0ccf0-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="0ccf0-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="0ccf0-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-501">**NoSQL**</span></span> |[<span data-ttu-id="0ccf0-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="0ccf0-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="0ccf0-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="0ccf0-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="0ccf0-504">**File**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-504">**File**</span></span> |[<span data-ttu-id="0ccf0-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="0ccf0-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="0ccf0-506">Système de fichiers</span><span class="sxs-lookup"><span data-stu-id="0ccf0-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="0ccf0-507">FTP</span><span class="sxs-lookup"><span data-stu-id="0ccf0-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="0ccf0-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="0ccf0-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="0ccf0-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="0ccf0-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="0ccf0-510">**Autres**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-510">**Others**</span></span> |[<span data-ttu-id="0ccf0-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="0ccf0-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="0ccf0-512">OData</span><span class="sxs-lookup"><span data-stu-id="0ccf0-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="0ccf0-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="0ccf0-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="0ccf0-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="0ccf0-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="0ccf0-515">Table web</span><span class="sxs-lookup"><span data-stu-id="0ccf0-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="0ccf0-516">un stockage Azure Blob</span><span class="sxs-lookup"><span data-stu-id="0ccf0-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-517">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-517">Linked service</span></span>
<span data-ttu-id="0ccf0-518">Il existe deux types de services liés : les services liés de stockage Azure et les services liés SAP de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="0ccf0-519">Service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="0ccf0-520">toolink votre fabrique de données tooa compte stockage Azure à l’aide de hello **clé de compte**, créez un service lié Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="0ccf0-521">le service ensemble hello lié toodefine un stockage Azure **type** Hello service lié trop**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="0ccf0-522">Ensuite, vous pouvez spécifier les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-523">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-523">Property</span></span> | <span data-ttu-id="0ccf0-524">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-524">Description</span></span> | <span data-ttu-id="0ccf0-525">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-526">connectionString</span></span> |<span data-ttu-id="0ccf0-527">Spécifiez les informations nécessaires tooconnect tooAzure stockage pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="0ccf0-528">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="0ccf0-529">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="0ccf0-530">Service lié SAP de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="0ccf0-531">Hello SAS de stockage Azure lié service vous permet de toolink une fabrique de données Azure tooan compte de stockage Azure à l’aide d’une Signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="0ccf0-532">Il fournit des fabrique de données hello avec l’accès restreint/limitées dans le temps de tooall/spécifiques des ressources (objet blob/conteneur) dans le stockage hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="0ccf0-533">toolink votre fabrique de données tooa compte stockage Azure à l’aide de Signature d’accès partagé, créez un service de SAS de stockage Azure lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="0ccf0-534">le service ensemble hello lié toodefine un SAS de stockage Azure **type** Hello service lié trop**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="0ccf0-535">Ensuite, vous pouvez spécifier les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="0ccf0-536">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-536">Property</span></span> | <span data-ttu-id="0ccf0-537">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-537">Description</span></span> | <span data-ttu-id="0ccf0-538">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="0ccf0-539">sasUri</span></span> |<span data-ttu-id="0ccf0-540">Spécifier des ressources de stockage Azure toohello URI de Signature d’accès partagé comme objet blob, conteneur ou une table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="0ccf0-541">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="0ccf0-542">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-542">Example</span></span>

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

<span data-ttu-id="0ccf0-543">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Blob Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-544">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-544">Dataset</span></span>
<span data-ttu-id="0ccf0-545">toodefine un jeu de données d’objets Blob Azure, jeu hello **type** du jeu de données hello trop**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="0ccf0-546">Ensuite, spécifiez hello propriétés spécifiques d’objets Blob Azure Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-547">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-547">Property</span></span> | <span data-ttu-id="0ccf0-548">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-548">Description</span></span> | <span data-ttu-id="0ccf0-549">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-550">folderPath</span></span> |<span data-ttu-id="0ccf0-551">Conteneur toohello de chemin d’accès et le dossier de stockage d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="0ccf0-552">Exemple : monconteneurblob\mondossierblob\\</span><span class="sxs-lookup"><span data-stu-id="0ccf0-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="0ccf0-553">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-553">Yes</span></span> |
| <span data-ttu-id="0ccf0-554">fileName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-554">fileName</span></span> |<span data-ttu-id="0ccf0-555">Nom de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-555">Name of hello blob.</span></span> <span data-ttu-id="0ccf0-556">fileName est facultatif et sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="0ccf0-557">Si vous spécifiez un nom de fichier, le hello activité (y compris la copie) fonctionne sur hello Blob spécifique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="0ccf0-558">Lorsque le nom de fichier n’est pas spécifié, copie inclut tous les objets BLOB dans folderPath hello pour le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="0ccf0-559">Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format : données. <Guid>.txt (par exemple : : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="0ccf0-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="0ccf0-560">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-560">No</span></span> |
| <span data-ttu-id="0ccf0-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="0ccf0-561">partitionedBy</span></span> |<span data-ttu-id="0ccf0-562">partitionedBy est une propriété facultative.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="0ccf0-563">Vous pouvez utiliser il toospecify un folderPath dynamique et le nom de fichier de données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="0ccf0-564">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="0ccf0-565">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-565">No</span></span> |
| <span data-ttu-id="0ccf0-566">format</span><span class="sxs-lookup"><span data-stu-id="0ccf0-566">format</span></span> | <span data-ttu-id="0ccf0-567">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0ccf0-568">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="0ccf0-569">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0ccf0-570">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0ccf0-571">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-571">No</span></span> |
| <span data-ttu-id="0ccf0-572">compression</span><span class="sxs-lookup"><span data-stu-id="0ccf0-572">compression</span></span> | <span data-ttu-id="0ccf0-573">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="0ccf0-574">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="0ccf0-575">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0ccf0-576">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0ccf0-577">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-578">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-578">Example</span></span>

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


<span data-ttu-id="0ccf0-579">Pour plus d’informations, consultez l’article [Azure Blob connector (connecteur d’objet blob Azure)](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="0ccf0-580">BlobSource dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="0ccf0-581">Si vous copiez des données à partir d’un stockage d’objets Blob Azure, la valeur hello **type de source de** Hello activité de copie trop**BlobSource**et spécifiez les propriétés Bonjour suivantes ** source ** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="0ccf0-582">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-582">Property</span></span> | <span data-ttu-id="0ccf0-583">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-583">Description</span></span> | <span data-ttu-id="0ccf0-584">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-584">Allowed values</span></span> | <span data-ttu-id="0ccf0-585">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-586">recursive</span><span class="sxs-lookup"><span data-stu-id="0ccf0-586">recursive</span></span> |<span data-ttu-id="0ccf0-587">Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="0ccf0-588">True (valeur par défaut), False</span><span class="sxs-lookup"><span data-stu-id="0ccf0-588">True (default value), False</span></span> |<span data-ttu-id="0ccf0-589">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="0ccf0-590">Exemple : BlobSource**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-590">Example: BlobSource**</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="0ccf0-591">BlobSink dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-592">Si vous copiez des données tooan stockage d’objets Blob Azure, la valeur hello **type de récepteur** Hello activité de copie trop**BlobSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-593">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-593">Property</span></span> | <span data-ttu-id="0ccf0-594">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-594">Description</span></span> | <span data-ttu-id="0ccf0-595">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-595">Allowed values</span></span> | <span data-ttu-id="0ccf0-596">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="0ccf0-597">copyBehavior</span></span> |<span data-ttu-id="0ccf0-598">Définit le comportement de copie de hello lors de la source de hello est BlobSource ou système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="0ccf0-599"><b>PreserveHierarchy</b>: préserve hello hiérarchie de fichiers dans le dossier cible de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="0ccf0-600">chemin d’accès relatif de Hello du dossier source du fichier toosource est identique toohello un chemin d’accès relatif du dossier tootarget de fichier cible.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="0ccf0-601"><b>FlattenHierarchy</b>: tous les fichiers à partir du dossier source hello sont Bonjour tout d’abord au niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="0ccf0-602">les fichiers cibles Hello ont un nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="0ccf0-603"><b>MergeFiles (valeur par défaut) :</b> fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="0ccf0-604">Si hello nom de fichier/objet Blob est spécifié, le nom de fichier fusionné hello serait nom spécifié de hello ; dans le cas contraire, serait de nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="0ccf0-605">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="0ccf0-606">Exemple : BlobSink</span><span class="sxs-lookup"><span data-stu-id="0ccf0-606">Example: BlobSink</span></span>

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

<span data-ttu-id="0ccf0-607">Pour plus d’informations, consultez l’article [Azure Blob connector (connecteur d’objet blob Azure)](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="0ccf0-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0ccf0-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-609">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-609">Linked service</span></span>
<span data-ttu-id="0ccf0-610">toodefine un service Azure Data Lake Store lié, définir le type de hello de hello service lié trop**AzureDataLakeStore**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-611">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-611">Property</span></span> | <span data-ttu-id="0ccf0-612">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-612">Description</span></span> | <span data-ttu-id="0ccf0-613">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-614">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-614">type</span></span> | <span data-ttu-id="0ccf0-615">propriété de type Hello doit indiquer : **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="0ccf0-616">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-616">Yes</span></span> |
| <span data-ttu-id="0ccf0-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="0ccf0-617">dataLakeStoreUri</span></span> | <span data-ttu-id="0ccf0-618">Indiquez les informations hello compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="0ccf0-619">Il se trouve dans hello suivant le format : `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="0ccf0-620">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-620">Yes</span></span> |
| <span data-ttu-id="0ccf0-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0ccf0-621">subscriptionId</span></span> | <span data-ttu-id="0ccf0-622">Abonnement Azure Id toowhich Data Lake Store appartient.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="0ccf0-623">Requis pour le récepteur</span><span class="sxs-lookup"><span data-stu-id="0ccf0-623">Required for sink</span></span> |
| <span data-ttu-id="0ccf0-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-624">resourceGroupName</span></span> | <span data-ttu-id="0ccf0-625">Toowhich de nom du groupe de ressources Azure Data Lake Store appartient.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="0ccf0-626">Requis pour le récepteur</span><span class="sxs-lookup"><span data-stu-id="0ccf0-626">Required for sink</span></span> |
| <span data-ttu-id="0ccf0-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="0ccf0-627">servicePrincipalId</span></span> | <span data-ttu-id="0ccf0-628">Spécifiez l’ID client de. l’application hello</span><span class="sxs-lookup"><span data-stu-id="0ccf0-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="0ccf0-629">Oui (pour l’authentification du principal du service)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="0ccf0-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="0ccf0-630">servicePrincipalKey</span></span> | <span data-ttu-id="0ccf0-631">Spécifiez la clé de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-631">Specify hello application's key.</span></span> | <span data-ttu-id="0ccf0-632">Oui (pour l’authentification du principal du service)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="0ccf0-633">locataire</span><span class="sxs-lookup"><span data-stu-id="0ccf0-633">tenant</span></span> | <span data-ttu-id="0ccf0-634">Spécifiez les informations de locataire hello (ID client ou le nom de domaine) dans lequel réside votre application.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="0ccf0-635">Vous pouvez le récupérer par pointage de souris hello en hello en haut à droite de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="0ccf0-636">Oui (pour l’authentification du principal du service)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="0ccf0-637">autorisation</span><span class="sxs-lookup"><span data-stu-id="0ccf0-637">authorization</span></span> | <span data-ttu-id="0ccf0-638">Cliquez sur **Authorize** bouton Bonjour **éditeur Data Factory** et entrez vos informations d’identification qui lui attribue hello généré automatiquement l’autorisation URL toothis.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="0ccf0-639">Oui (pour l’authentification des informations d’identification utilisateur)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="0ccf0-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="0ccf0-640">sessionId</span></span> | <span data-ttu-id="0ccf0-641">Id de session OAuth à partir de la session de d’autorisation OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="0ccf0-642">Chaque ID de session est unique et ne peut être utilisé qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="0ccf0-643">Ce paramètre est généré automatiquement lorsque vous utilisez Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="0ccf0-644">Oui (pour l’authentification des informations d’identification utilisateur)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="0ccf0-645">Exemple : utilisation de l’authentification d’un principal du service</span><span class="sxs-lookup"><span data-stu-id="0ccf0-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="0ccf0-646">Exemple : utilisation de l’authentification des informations d’identification utilisateur</span><span class="sxs-lookup"><span data-stu-id="0ccf0-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="0ccf0-647">Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-648">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-648">Dataset</span></span>
<span data-ttu-id="0ccf0-649">toodefine un dataset Azure Data Lake Store, jeu hello **type** du jeu de données hello trop**AzureDataLakeStore**et spécifiez hello propriétés Bonjour suivantes **typeProperties**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-650">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-650">Property</span></span> | <span data-ttu-id="0ccf0-651">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-651">Description</span></span> | <span data-ttu-id="0ccf0-652">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-653">folderPath</span></span> |<span data-ttu-id="0ccf0-654">Conteneur toohello de chemin d’accès et le dossier à hello Azure Data Lake stockent.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="0ccf0-655">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-655">Yes</span></span> |
| <span data-ttu-id="0ccf0-656">fileName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-656">fileName</span></span> |<span data-ttu-id="0ccf0-657">Nom du fichier hello dans le magasin d’Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="0ccf0-658">fileName est facultatif et sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="0ccf0-659">Si vous spécifiez un nom de fichier, activité hello (y compris la copie) fonctionne sur un fichier spécifique hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="0ccf0-660">Lorsque le nom de fichier n’est pas spécifié, la copie inclut tous les fichiers dans folderPath hello pour le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="0ccf0-661">Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format : données. <Guid>.txt (par exemple : : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="0ccf0-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="0ccf0-662">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-662">No</span></span> |
| <span data-ttu-id="0ccf0-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="0ccf0-663">partitionedBy</span></span> |<span data-ttu-id="0ccf0-664">partitionedBy est une propriété facultative.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="0ccf0-665">Vous pouvez utiliser il toospecify un folderPath dynamique et le nom de fichier de données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="0ccf0-666">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="0ccf0-667">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-667">No</span></span> |
| <span data-ttu-id="0ccf0-668">format</span><span class="sxs-lookup"><span data-stu-id="0ccf0-668">format</span></span> | <span data-ttu-id="0ccf0-669">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0ccf0-670">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="0ccf0-671">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0ccf0-672">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0ccf0-673">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-673">No</span></span> |
| <span data-ttu-id="0ccf0-674">compression</span><span class="sxs-lookup"><span data-stu-id="0ccf0-674">compression</span></span> | <span data-ttu-id="0ccf0-675">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="0ccf0-676">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="0ccf0-677">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0ccf0-678">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0ccf0-679">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-680">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-680">Example</span></span>
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

<span data-ttu-id="0ccf0-681">Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="0ccf0-682">Source Azure Data Lake Store dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-683">Si vous copiez des données à partir d’un Azure Data Lake Store, la valeur hello **type de source de** Hello activité de copie trop**AzureDataLakeStoreSource**et spécifiez les propriétés Bonjour suivantes **source**  section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="0ccf0-684">**AzureDataLakeStoreSource** prend en charge les propriétés suivantes de hello **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="0ccf0-685">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-685">Property</span></span> | <span data-ttu-id="0ccf0-686">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-686">Description</span></span> | <span data-ttu-id="0ccf0-687">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-687">Allowed values</span></span> | <span data-ttu-id="0ccf0-688">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-689">recursive</span><span class="sxs-lookup"><span data-stu-id="0ccf0-689">recursive</span></span> |<span data-ttu-id="0ccf0-690">Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="0ccf0-691">True (valeur par défaut), False</span><span class="sxs-lookup"><span data-stu-id="0ccf0-691">True (default value), False</span></span> |<span data-ttu-id="0ccf0-692">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="0ccf0-693">Exemple : AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="0ccf0-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="0ccf0-694">Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="0ccf0-695">Récepteur Azure Data Lake Store dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-696">Si vous copiez des données tooan Azure Data Lake Store, la valeur hello **type de récepteur** Hello activité de copie trop**AzureDataLakeStoreSink**et spécifiez les propriétés Bonjour suivantes **récepteur**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-697">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-697">Property</span></span> | <span data-ttu-id="0ccf0-698">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-698">Description</span></span> | <span data-ttu-id="0ccf0-699">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-699">Allowed values</span></span> | <span data-ttu-id="0ccf0-700">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="0ccf0-701">copyBehavior</span></span> |<span data-ttu-id="0ccf0-702">Spécifie le comportement de copie hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="0ccf0-703"><b>PreserveHierarchy</b>: préserve hello hiérarchie de fichiers dans le dossier cible de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="0ccf0-704">chemin d’accès relatif de Hello du dossier source du fichier toosource est identique toohello un chemin d’accès relatif du dossier tootarget de fichier cible.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="0ccf0-705"><b>FlattenHierarchy</b>: tous les fichiers à partir du dossier source hello sont créés dans hello premier niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="0ccf0-706">les fichiers cibles Hello sont créés avec le nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="0ccf0-707"><b>MergeFiles</b>: fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="0ccf0-708">Si hello nom de fichier/objet Blob est spécifié, le nom de fichier fusionné hello serait nom spécifié de hello ; dans le cas contraire, serait de nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="0ccf0-709">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="0ccf0-710">Exemple : AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="0ccf0-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="0ccf0-711">Pour plus d’informations, consultez l’article [Azure Data Lake Store connector (connecteur Azure Data Lake Store)](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="0ccf0-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0ccf0-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="0ccf0-713">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-713">Linked service</span></span>
<span data-ttu-id="0ccf0-714">toodefine une base de données Azure Cosmos le service ensemble hello lié **type** Hello service lié trop**DocumentDb**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-715">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-715">**Property**</span></span> | <span data-ttu-id="0ccf0-716">**Description**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-716">**Description**</span></span> | <span data-ttu-id="0ccf0-717">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-718">connectionString</span></span> |<span data-ttu-id="0ccf0-719">Spécifiez les informations nécessaires de base de données de base de données Cosmos tooconnect tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="0ccf0-720">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-721">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-721">Example</span></span>

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
<span data-ttu-id="0ccf0-722">Pour plus d’informations, consultez l’article sur le [connecteur d’objet blob Azure](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-723">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-723">Dataset</span></span>
<span data-ttu-id="0ccf0-724">toodefine un jeu de données de base de données Azure Cosmos, jeu hello **type** du jeu de données hello trop**DocumentDbCollection**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-725">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-725">**Property**</span></span> | <span data-ttu-id="0ccf0-726">**Description**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-726">**Description**</span></span> | <span data-ttu-id="0ccf0-727">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-728">collectionName</span></span> |<span data-ttu-id="0ccf0-729">Nom de collection de base de données Azure Cosmos de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="0ccf0-730">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-731">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-731">Example</span></span>

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
<span data-ttu-id="0ccf0-732">Pour plus d’informations, consultez l’article sur le [connecteur Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="0ccf0-733">Source de la collection Azure Cosmos DB dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-734">Si vous copiez des données à partir d’une base de données Azure Cosmos, définissez hello **type de source de** Hello activité de copie trop**DocumentDbCollectionSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-735">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-735">**Property**</span></span> | <span data-ttu-id="0ccf0-736">**Description**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-736">**Description**</span></span> | <span data-ttu-id="0ccf0-737">**Valeurs autorisées**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-737">**Allowed values**</span></span> | <span data-ttu-id="0ccf0-738">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-739">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-739">query</span></span> |<span data-ttu-id="0ccf0-740">Spécifier les données de tooread requête hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="0ccf0-741">Chaîne de requête prise en charge par Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="0ccf0-742">Exemple : `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="0ccf0-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="0ccf0-743">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-743">No</span></span> <br/><br/><span data-ttu-id="0ccf0-744">Si ce n’est pas spécifié, hello instruction SQL exécutée :`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="0ccf0-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="0ccf0-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="0ccf0-745">nestingSeparator</span></span> |<span data-ttu-id="0ccf0-746">Tooindicate caractère spécial qui hello document est imbriquée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="0ccf0-747">Tout caractère.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-747">Any character.</span></span> <br/><br/><span data-ttu-id="0ccf0-748">Azure Cosmos DB est une banque NoSQL de documents JSON, où les structures imbriquées sont autorisées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="0ccf0-749">Azure Data Factory permet de hiérarchie de toodenote utilisateur via nestingSeparator, qui est «. »</span><span class="sxs-lookup"><span data-stu-id="0ccf0-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="0ccf0-750">Bonjour exemples ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-750">in hello above examples.</span></span> <span data-ttu-id="0ccf0-751">Avec séparateur de hello, activité de copie hello génère un objet de « Name » hello avec des éléments de trois enfants too"Name.First première, intermédiaire et dernière, en fonction », « Name.Middle » et « Name.Last « Bonjour de définition de table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="0ccf0-752">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-753">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-753">Example</span></span>

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

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="0ccf0-754">Récepteur de collection Azure Cosmos DB dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-755">Si vous copiez des données tooAzure Cosmos DB, la valeur hello **type de récepteur** Hello activité de copie trop**DocumentDbCollectionSink**et spécifiez les propriétés Bonjour suivantes **récepteur**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-756">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-756">**Property**</span></span> | <span data-ttu-id="0ccf0-757">**Description**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-757">**Description**</span></span> | <span data-ttu-id="0ccf0-758">**Valeurs autorisées**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-758">**Allowed values**</span></span> | <span data-ttu-id="0ccf0-759">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="0ccf0-760">nestingSeparator</span></span> |<span data-ttu-id="0ccf0-761">Un caractère spécial dans tooindicate de nom hello source colonne imbriquées de document est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="0ccf0-762">Par exemple ci-dessus : `Name.First` dans la sortie de hello table génère hello suivant structure JSON dans le document de base de données Cosmos hello :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="0ccf0-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="0ccf0-763">"Name": {</span></span><br/>    <span data-ttu-id="0ccf0-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="0ccf0-764">"First": "John"</span></span><br/><span data-ttu-id="0ccf0-765">},</span><span class="sxs-lookup"><span data-stu-id="0ccf0-765">},</span></span> |<span data-ttu-id="0ccf0-766">Caractère utilisé tooseparate des niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="0ccf0-767">La valeur par défaut est `.` (point).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="0ccf0-768">Caractère utilisé tooseparate des niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="0ccf0-769">La valeur par défaut est `.` (point).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="0ccf0-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0ccf0-770">writeBatchSize</span></span> |<span data-ttu-id="0ccf0-771">Nombre de parallèle demandes documents toocreate de service de base de données Cosmos tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="0ccf0-772">Vous pouvez affiner les performances des hello lors de la copie des données à partir de base de données Azure Cosmos à l’aide de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="0ccf0-773">Vous pouvez vous attendre de meilleures performances lorsque vous augmentez la valeur writeBatchSize, car plusieurs demandes parallèles tooAzure Cosmos DB sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="0ccf0-774">Toutefois, vous devez tooavoid la limitation peut lever de message d’erreur hello : « Requête taux est grand ».</span><span class="sxs-lookup"><span data-stu-id="0ccf0-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="0ccf0-775">Une limitation dépend de divers facteurs, dont la taille des documents, le nombre de termes qu’ils contiennent, la stratégie d’indexation de la collection cible, etc. Pour les opérations de copie, vous pouvez utiliser la plupart des débit disponible à une meilleure hello de toohave de collection (par exemple, S3) (2 500 demande unités par seconde).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="0ccf0-776">Entier </span><span class="sxs-lookup"><span data-stu-id="0ccf0-776">Integer</span></span> |<span data-ttu-id="0ccf0-777">Non (valeur par défaut : 5)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-777">No (default: 5)</span></span> |
| <span data-ttu-id="0ccf0-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0ccf0-778">writeBatchTimeout</span></span> |<span data-ttu-id="0ccf0-779">Temps d’attente pour hello opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="0ccf0-780">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="0ccf0-780">timespan</span></span><br/><br/> <span data-ttu-id="0ccf0-781">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="0ccf0-782">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-783">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-783">Example</span></span>

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
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
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

<span data-ttu-id="0ccf0-784">Pour plus d’informations, consultez l’article sur le [connecteur Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="0ccf0-785">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-786">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-786">Linked service</span></span>
<span data-ttu-id="0ccf0-787">le service ensemble hello lié toodefine une base de données SQL Azure **type** Hello service lié trop**AzureSqlDatabase**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-788">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-788">Property</span></span> | <span data-ttu-id="0ccf0-789">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-789">Description</span></span> | <span data-ttu-id="0ccf0-790">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-791">connectionString</span></span> |<span data-ttu-id="0ccf0-792">Spécifiez les informations nécessaires d’instance de base de données SQL Azure tooconnect toohello pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="0ccf0-793">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-794">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-794">Example</span></span>
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

<span data-ttu-id="0ccf0-795">Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-796">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-796">Dataset</span></span>
<span data-ttu-id="0ccf0-797">toodefine un jeu de données de base de données SQL Azure, jeu hello **type** du jeu de données hello trop**AzureSqlTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-798">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-798">Property</span></span> | <span data-ttu-id="0ccf0-799">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-799">Description</span></span> | <span data-ttu-id="0ccf0-800">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-801">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-801">tableName</span></span> |<span data-ttu-id="0ccf0-802">Nom de la table de hello ou la vue d’instance de base de données SQL Azure hello service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="0ccf0-803">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-804">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-804">Example</span></span>

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
<span data-ttu-id="0ccf0-805">Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="0ccf0-806">Source SQL dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-807">Si vous copiez des données à partir d’une base de données SQL Azure, la valeur hello **type de source de** Hello activité de copie trop**SqlSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-808">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-808">Property</span></span> | <span data-ttu-id="0ccf0-809">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-809">Description</span></span> | <span data-ttu-id="0ccf0-810">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-810">Allowed values</span></span> | <span data-ttu-id="0ccf0-811">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="0ccf0-812">sqlReaderQuery</span></span> |<span data-ttu-id="0ccf0-813">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-814">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-814">SQL query string.</span></span> <span data-ttu-id="0ccf0-815">Exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="0ccf0-816">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-816">No</span></span> |
| <span data-ttu-id="0ccf0-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="0ccf0-818">Nom de hello procédure stockée qui lit les données à partir de la table de source de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="0ccf0-819">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-820">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-820">No</span></span> |
| <span data-ttu-id="0ccf0-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="0ccf0-821">storedProcedureParameters</span></span> |<span data-ttu-id="0ccf0-822">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-823">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-823">Name/value pairs.</span></span> <span data-ttu-id="0ccf0-824">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="0ccf0-825">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-826">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-826">Example</span></span>

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
<span data-ttu-id="0ccf0-827">Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="0ccf0-828">Récepteur SQL dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-829">Si vous copiez des données tooAzure base de données SQL, la valeur hello **type de récepteur** Hello activité de copie trop**SqlSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-830">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-830">Property</span></span> | <span data-ttu-id="0ccf0-831">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-831">Description</span></span> | <span data-ttu-id="0ccf0-832">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-832">Allowed values</span></span> | <span data-ttu-id="0ccf0-833">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0ccf0-834">writeBatchTimeout</span></span> |<span data-ttu-id="0ccf0-835">Temps d’attente pour hello lot insert opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="0ccf0-836">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="0ccf0-836">timespan</span></span><br/><br/> <span data-ttu-id="0ccf0-837">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="0ccf0-838">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-838">No</span></span> |
| <span data-ttu-id="0ccf0-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0ccf0-839">writeBatchSize</span></span> |<span data-ttu-id="0ccf0-840">Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="0ccf0-841">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-841">Integer (number of rows)</span></span> |<span data-ttu-id="0ccf0-842">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-842">No (default: 10000)</span></span> |
| <span data-ttu-id="0ccf0-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="0ccf0-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="0ccf0-844">Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="0ccf0-845">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-845">A query statement.</span></span> |<span data-ttu-id="0ccf0-846">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-846">No</span></span> |
| <span data-ttu-id="0ccf0-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="0ccf0-848">Spécifiez un nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="0ccf0-849">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="0ccf0-850">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-850">No</span></span> |
| <span data-ttu-id="0ccf0-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="0ccf0-852">Nom de hello procédure stockée que les données upserts (mises à jour/insertion) dans la table cible hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="0ccf0-853">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-854">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-854">No</span></span> |
| <span data-ttu-id="0ccf0-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="0ccf0-855">storedProcedureParameters</span></span> |<span data-ttu-id="0ccf0-856">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-857">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-857">Name/value pairs.</span></span> <span data-ttu-id="0ccf0-858">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="0ccf0-859">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-859">No</span></span> |
| <span data-ttu-id="0ccf0-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-860">sqlWriterTableType</span></span> |<span data-ttu-id="0ccf0-861">Spécifiez un toobe de nom de type de table utilisée dans la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="0ccf0-862">Activité de copie rend les données de hello déplacées disponibles dans une table temporaire avec ce type de table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="0ccf0-863">Code de procédure stockée puis de fusionner des données hello copiées avec les données existantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="0ccf0-864">Nom de type de table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-864">A table type name.</span></span> |<span data-ttu-id="0ccf0-865">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-866">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-866">Example</span></span>

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

<span data-ttu-id="0ccf0-867">Pour plus d’informations, consultez l’article [Azure SQL connector (connecteur Azure SQL)](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="0ccf0-868">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0ccf0-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-869">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-869">Linked service</span></span>
<span data-ttu-id="0ccf0-870">le service ensemble hello lié toodefine un entrepôt de données SQL Azure **type** Hello service lié trop**AzureSqlDW**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-871">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-871">Property</span></span> | <span data-ttu-id="0ccf0-872">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-872">Description</span></span> | <span data-ttu-id="0ccf0-873">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-874">connectionString</span></span> |<span data-ttu-id="0ccf0-875">Spécifiez les informations nécessaires d’instance d’Azure SQL Data Warehouse tooconnect toohello pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="0ccf0-876">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="0ccf0-877">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-877">Example</span></span>

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

<span data-ttu-id="0ccf0-878">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-879">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-879">Dataset</span></span>
<span data-ttu-id="0ccf0-880">toodefine un jeu de données Azure SQL Data Warehouse, jeu hello **type** du jeu de données hello trop**AzureSqlDWTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-881">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-881">Property</span></span> | <span data-ttu-id="0ccf0-882">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-882">Description</span></span> | <span data-ttu-id="0ccf0-883">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-884">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-884">tableName</span></span> |<span data-ttu-id="0ccf0-885">Nom de la table de hello ou une vue dans la base de données Azure SQL Data Warehouse hello qui hello service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="0ccf0-886">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-887">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-887">Example</span></span>

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

<span data-ttu-id="0ccf0-888">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="0ccf0-889">Source SQL DW dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-890">Si vous copiez des données à partir de l’entrepôt de données SQL Azure, la valeur hello **type de source de** Hello activité de copie trop**SqlDWSource**et spécifiez les propriétés Bonjour suivantes **source**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-891">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-891">Property</span></span> | <span data-ttu-id="0ccf0-892">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-892">Description</span></span> | <span data-ttu-id="0ccf0-893">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-893">Allowed values</span></span> | <span data-ttu-id="0ccf0-894">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="0ccf0-895">sqlReaderQuery</span></span> |<span data-ttu-id="0ccf0-896">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-897">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-897">SQL query string.</span></span> <span data-ttu-id="0ccf0-898">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="0ccf0-899">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-899">No</span></span> |
| <span data-ttu-id="0ccf0-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="0ccf0-901">Nom de hello procédure stockée qui lit les données à partir de la table de source de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="0ccf0-902">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-903">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-903">No</span></span> |
| <span data-ttu-id="0ccf0-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="0ccf0-904">storedProcedureParameters</span></span> |<span data-ttu-id="0ccf0-905">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-906">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-906">Name/value pairs.</span></span> <span data-ttu-id="0ccf0-907">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="0ccf0-908">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-909">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-909">Example</span></span>

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

<span data-ttu-id="0ccf0-910">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="0ccf0-911">Récepteur SQL DW dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-912">Si vous copiez des données tooAzure SQL Data Warehouse, définissez hello **type de récepteur** Hello activité de copie trop**SqlDWSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-913">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-913">Property</span></span> | <span data-ttu-id="0ccf0-914">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-914">Description</span></span> | <span data-ttu-id="0ccf0-915">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-915">Allowed values</span></span> | <span data-ttu-id="0ccf0-916">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="0ccf0-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="0ccf0-918">Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="0ccf0-919">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-919">A query statement.</span></span> |<span data-ttu-id="0ccf0-920">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-920">No</span></span> |
| <span data-ttu-id="0ccf0-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="0ccf0-921">allowPolyBase</span></span> |<span data-ttu-id="0ccf0-922">Indique si toouse PolyBase (le cas échéant) au lieu de mécanisme BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="0ccf0-923">**À l’aide de PolyBase est hello recommandé la façon dont les données tooload dans SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="0ccf0-924">true</span><span class="sxs-lookup"><span data-stu-id="0ccf0-924">True</span></span> <br/><span data-ttu-id="0ccf0-925">False (valeur par défaut)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-925">False (default)</span></span> |<span data-ttu-id="0ccf0-926">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-926">No</span></span> |
| <span data-ttu-id="0ccf0-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="0ccf0-927">polyBaseSettings</span></span> |<span data-ttu-id="0ccf0-928">Un groupe de propriétés qui peuvent être spécifiés lorsque hello **allowPolybase** propriété a la valeur trop**true**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="0ccf0-929">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-929">No</span></span> |
| <span data-ttu-id="0ccf0-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="0ccf0-930">rejectValue</span></span> |<span data-ttu-id="0ccf0-931">Spécifie le nombre de hello ou un pourcentage de lignes peut être rejetée avant l’échec de la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="0ccf0-932">En savoir plus sur de PolyBase hello rejettent options Bonjour **Arguments** section de [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) rubrique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="0ccf0-933">0 (par défaut), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="0ccf0-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="0ccf0-934">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-934">No</span></span> |
| <span data-ttu-id="0ccf0-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-935">rejectType</span></span> |<span data-ttu-id="0ccf0-936">Spécifie si l’option de rejectValue hello est spécifiée comme une valeur littérale ou pourcentage.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="0ccf0-937">Value (par défaut), Percentage</span><span class="sxs-lookup"><span data-stu-id="0ccf0-937">Value (default), Percentage</span></span> |<span data-ttu-id="0ccf0-938">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-938">No</span></span> |
| <span data-ttu-id="0ccf0-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="0ccf0-939">rejectSampleValue</span></span> |<span data-ttu-id="0ccf0-940">Détermine le nombre hello de lignes tooretrieve avant hello PolyBase recalcule le pourcentage de hello de lignes rejetées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="0ccf0-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="0ccf0-941">1, 2, …</span></span> |<span data-ttu-id="0ccf0-942">Oui, si le **rejectType** est **percentage**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="0ccf0-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="0ccf0-943">useTypeDefault</span></span> |<span data-ttu-id="0ccf0-944">Spécifie comment toohandle manque des valeurs dans le fichiers texte délimités lorsque PolyBase récupère les données à partir du fichier de texte hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="0ccf0-945">En savoir plus sur cette propriété à partir de la section Arguments hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="0ccf0-946">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-946">True, False (default)</span></span> |<span data-ttu-id="0ccf0-947">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-947">No</span></span> |
| <span data-ttu-id="0ccf0-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0ccf0-948">writeBatchSize</span></span> |<span data-ttu-id="0ccf0-949">Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0ccf0-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="0ccf0-950">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-950">Integer (number of rows)</span></span> |<span data-ttu-id="0ccf0-951">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-951">No (default: 10000)</span></span> |
| <span data-ttu-id="0ccf0-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0ccf0-952">writeBatchTimeout</span></span> |<span data-ttu-id="0ccf0-953">Temps d’attente pour hello lot insert opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="0ccf0-954">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="0ccf0-954">timespan</span></span><br/><br/> <span data-ttu-id="0ccf0-955">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="0ccf0-956">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-957">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-957">Example</span></span>

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

<span data-ttu-id="0ccf0-958">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="0ccf0-959">Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-960">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-960">Linked service</span></span>
<span data-ttu-id="0ccf0-961">le service ensemble hello lié toodefine un indexeur Azure Search **type** Hello service lié trop**AzureSearch**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-962">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-962">Property</span></span> | <span data-ttu-id="0ccf0-963">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-963">Description</span></span> | <span data-ttu-id="0ccf0-964">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="0ccf0-965">url</span><span class="sxs-lookup"><span data-stu-id="0ccf0-965">url</span></span> | <span data-ttu-id="0ccf0-966">URL de hello service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="0ccf0-967">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-967">Yes</span></span> |
| <span data-ttu-id="0ccf0-968">key</span><span class="sxs-lookup"><span data-stu-id="0ccf0-968">key</span></span> | <span data-ttu-id="0ccf0-969">Clé d’administration pour hello service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="0ccf0-970">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-971">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-971">Example</span></span>

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

<span data-ttu-id="0ccf0-972">Pour plus d’informations, consultez l’article [Connecteur Recherche Azure](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-973">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-973">Dataset</span></span>
<span data-ttu-id="0ccf0-974">toodefine un jeu de données Azure Search, jeu hello **type** du jeu de données hello trop**AzureSearchIndex**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-975">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-975">Property</span></span> | <span data-ttu-id="0ccf0-976">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-976">Description</span></span> | <span data-ttu-id="0ccf0-977">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="0ccf0-978">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-978">type</span></span> | <span data-ttu-id="0ccf0-979">propriété de type Hello doit être définie trop**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="0ccf0-980">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-980">Yes</span></span> |
| <span data-ttu-id="0ccf0-981">indexName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-981">indexName</span></span> | <span data-ttu-id="0ccf0-982">Nom de l’index de recherche de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="0ccf0-983">Fabrique de données ne crée pas d’index de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="0ccf0-984">index de Hello doit exister dans Azure Search.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="0ccf0-985">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-986">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-986">Example</span></span>

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

<span data-ttu-id="0ccf0-987">Pour plus d’informations, consultez l’article [Connecteur Recherche Azure](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="0ccf0-988">Récepteur Index Recherche Azure dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-989">Si vous copiez des index de recherche de Azure tooan de données, la valeur hello **type de récepteur** Hello activité de copie trop**AzureSearchIndexSink**et spécifiez les propriétés Bonjour suivantes **récepteur**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-990">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-990">Property</span></span> | <span data-ttu-id="0ccf0-991">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-991">Description</span></span> | <span data-ttu-id="0ccf0-992">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-992">Allowed values</span></span> | <span data-ttu-id="0ccf0-993">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="0ccf0-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="0ccf0-994">WriteBehavior</span></span> | <span data-ttu-id="0ccf0-995">Spécifie si toomerge ou remplacer un document existe déjà dans l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="0ccf0-996">Merge (par défaut)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-996">Merge (default)</span></span><br/><span data-ttu-id="0ccf0-997">Télécharger</span><span class="sxs-lookup"><span data-stu-id="0ccf0-997">Upload</span></span>| <span data-ttu-id="0ccf0-998">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-998">No</span></span> |
| <span data-ttu-id="0ccf0-999">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0ccf0-999">WriteBatchSize</span></span> | <span data-ttu-id="0ccf0-1000">Télécharge des données dans l’index de recherche de Azure hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="0ccf0-1001">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1001">1 too1,000.</span></span> <span data-ttu-id="0ccf0-1002">Valeur par défaut : 1 000.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1002">Default value is 1000.</span></span> | <span data-ttu-id="0ccf0-1003">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1004">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1004">Example</span></span>

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

<span data-ttu-id="0ccf0-1005">Pour plus d’informations, consultez l’article [Connecteur Recherche Azure](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="0ccf0-1006">Stockage de table Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1007">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1007">Linked service</span></span>
<span data-ttu-id="0ccf0-1008">Il existe deux types de services liés : les services liés de stockage Azure et les services liés SAP de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="0ccf0-1009">Service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="0ccf0-1010">toolink votre fabrique de données tooa compte stockage Azure à l’aide de hello **clé de compte**, créez un service lié Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="0ccf0-1011">le service ensemble hello lié toodefine un stockage Azure **type** Hello service lié trop**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="0ccf0-1012">Ensuite, vous pouvez spécifier les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1013">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1013">Property</span></span> | <span data-ttu-id="0ccf0-1014">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1014">Description</span></span> | <span data-ttu-id="0ccf0-1015">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-1016">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1016">type</span></span> |<span data-ttu-id="0ccf0-1017">propriété de type Hello doit indiquer : **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="0ccf0-1018">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1018">Yes</span></span> |
| <span data-ttu-id="0ccf0-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1019">connectionString</span></span> |<span data-ttu-id="0ccf0-1020">Spécifiez les informations nécessaires tooconnect tooAzure stockage pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="0ccf0-1021">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1021">Yes</span></span> |

<span data-ttu-id="0ccf0-1022">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="0ccf0-1023">Service lié SAP de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="0ccf0-1024">Hello SAS de stockage Azure lié service vous permet de toolink une fabrique de données Azure tooan compte de stockage Azure à l’aide d’une Signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="0ccf0-1025">Il fournit des fabrique de données hello avec l’accès restreint/limitées dans le temps de tooall/spécifiques des ressources (objet blob/conteneur) dans le stockage hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="0ccf0-1026">toolink votre fabrique de données tooa compte stockage Azure à l’aide de Signature d’accès partagé, créez un service de SAS de stockage Azure lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="0ccf0-1027">le service ensemble hello lié toodefine un SAS de stockage Azure **type** Hello service lié trop**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="0ccf0-1028">Ensuite, vous pouvez spécifier les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="0ccf0-1029">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1029">Property</span></span> | <span data-ttu-id="0ccf0-1030">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1030">Description</span></span> | <span data-ttu-id="0ccf0-1031">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-1032">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1032">type</span></span> |<span data-ttu-id="0ccf0-1033">propriété de type Hello doit indiquer : **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="0ccf0-1034">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1034">Yes</span></span> |
| <span data-ttu-id="0ccf0-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1035">sasUri</span></span> |<span data-ttu-id="0ccf0-1036">Spécifier des ressources de stockage Azure toohello URI de Signature d’accès partagé comme objet blob, conteneur ou une table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="0ccf0-1037">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1037">Yes</span></span> |

<span data-ttu-id="0ccf0-1038">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1038">**Example:**</span></span>

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

<span data-ttu-id="0ccf0-1039">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-1040">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1040">Dataset</span></span>
<span data-ttu-id="0ccf0-1041">toodefine un jeu de données de Table Azure, jeu hello **type** du jeu de données hello trop**AzureTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1042">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1042">Property</span></span> | <span data-ttu-id="0ccf0-1043">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1043">Description</span></span> | <span data-ttu-id="0ccf0-1044">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1045">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1045">tableName</span></span> |<span data-ttu-id="0ccf0-1046">Nom de table hello dans l’instance de base de données de Table Azure hello ce service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="0ccf0-1047">Oui.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1047">Yes.</span></span> <span data-ttu-id="0ccf0-1048">Lorsqu’un nom de table est spécifié sans un azureTableSourceQuery, tous les enregistrements à partir de la table de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="0ccf0-1049">Si un azureTableSourceQuery est également spécifiée, les enregistrements de la table hello qui répond aux requêtes de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1050">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1050">Example</span></span>

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

<span data-ttu-id="0ccf0-1051">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure)](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1052">Source Table Azure dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1053">Si vous copiez des données depuis le stockage de Table Azure, la valeur hello **type de source de** Hello activité de copie trop**AzureTableSource**et spécifiez les propriétés Bonjour suivantes **source**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-1054">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1054">Property</span></span> | <span data-ttu-id="0ccf0-1055">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1055">Description</span></span> | <span data-ttu-id="0ccf0-1056">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1056">Allowed values</span></span> | <span data-ttu-id="0ccf0-1057">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="0ccf0-1059">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1060">Chaîne de requête de table Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1060">Azure table query string.</span></span> <span data-ttu-id="0ccf0-1061">Consultez les exemples dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1061">See examples in hello next section.</span></span> |<span data-ttu-id="0ccf0-1062">Non.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1062">No.</span></span> <span data-ttu-id="0ccf0-1063">Lorsqu’un nom de table est spécifié sans un azureTableSourceQuery, tous les enregistrements à partir de la table de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="0ccf0-1064">Si un azureTableSourceQuery est également spécifiée, les enregistrements de la table hello qui répond aux requêtes de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="0ccf0-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="0ccf0-1066">Indiquer si exception de hello avale de table n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="0ccf0-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1067">TRUE</span></span><br/><span data-ttu-id="0ccf0-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1068">FALSE</span></span> |<span data-ttu-id="0ccf0-1069">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1070">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1070">Example</span></span>

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

<span data-ttu-id="0ccf0-1071">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure)](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="0ccf0-1072">Récepteur Table Azure dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1073">Si vous copiez des données tooAzure le stockage de Table, la valeur hello **type de récepteur** Hello activité de copie trop**AzureTableSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-1074">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1074">Property</span></span> | <span data-ttu-id="0ccf0-1075">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1075">Description</span></span> | <span data-ttu-id="0ccf0-1076">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1076">Allowed values</span></span> | <span data-ttu-id="0ccf0-1077">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="0ccf0-1079">Valeur par défaut partition clé qui peut être utilisé par le récepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="0ccf0-1080">Valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1080">A string value.</span></span> |<span data-ttu-id="0ccf0-1081">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1081">No</span></span> |
| <span data-ttu-id="0ccf0-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="0ccf0-1083">Spécifiez le nom de colonne hello dont les valeurs sont utilisées comme clés de partition.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="0ccf0-1084">Si non spécifié, AzureTableDefaultPartitionKeyValue est utilisé comme clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="0ccf0-1085">Nom de colonne.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1085">A column name.</span></span> |<span data-ttu-id="0ccf0-1086">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1086">No</span></span> |
| <span data-ttu-id="0ccf0-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="0ccf0-1088">Spécifiez le nom de colonne hello dont les valeurs de colonne sont utilisées comme clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="0ccf0-1089">Si aucune valeur n'est spécifiée, un GUID est utilisé pour chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="0ccf0-1090">Nom de colonne.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1090">A column name.</span></span> |<span data-ttu-id="0ccf0-1091">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1091">No</span></span> |
| <span data-ttu-id="0ccf0-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1092">azureTableInsertType</span></span> |<span data-ttu-id="0ccf0-1093">Hello mode tooinsert les données dans Azure table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="0ccf0-1094">Cette propriété contrôle si les lignes existantes dans la table de sortie hello avec les clés de partition et de ligne correspondantes ont leurs valeurs remplacé ou fusionnées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="0ccf0-1095">toolearn sur le fonctionnement de ces paramètres (fusion et remplacement), consultez [insertion ou l’entité de fusion](https://msdn.microsoft.com/library/azure/hh452241.aspx) et [insérer ou remplacer une entité](https://msdn.microsoft.com/library/azure/hh452242.aspx) rubriques.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="0ccf0-1096">Ce paramètre s’applique au niveau de ligne hello, pas de niveau de table d’hello, et aucune de ces options supprime des lignes dans la table de sortie hello qui n’existent pas dans l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="0ccf0-1097">fusionner (par défaut)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1097">merge (default)</span></span><br/><span data-ttu-id="0ccf0-1098">remplacer</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1098">replace</span></span> |<span data-ttu-id="0ccf0-1099">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1099">No</span></span> |
| <span data-ttu-id="0ccf0-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1100">writeBatchSize</span></span> |<span data-ttu-id="0ccf0-1101">Insère des données dans hello table Azure quand la valeur de hello writeBatchSize ou writeBatchTimeout est atteinte.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="0ccf0-1102">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1102">Integer (number of rows)</span></span> |<span data-ttu-id="0ccf0-1103">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="0ccf0-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1104">writeBatchTimeout</span></span> |<span data-ttu-id="0ccf0-1105">Insère des données dans hello table Azure quand la valeur de hello writeBatchSize ou writeBatchTimeout est atteinte</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="0ccf0-1106">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1106">timespan</span></span><br/><br/><span data-ttu-id="0ccf0-1107">Exemple : « 00: 20:00 » (20 minutes)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="0ccf0-1108">Non (le délai d’expiration de valeur par défaut toostorage client par défaut la valeur 90 s)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1109">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1109">Example</span></span>

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
<span data-ttu-id="0ccf0-1110">Pour plus d’informations sur ces services liés, consultez l’article [Connecteur de stockage Table Azure)](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="0ccf0-1111">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1112">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1112">Linked service</span></span>
<span data-ttu-id="0ccf0-1113">toodefine un Amazon Redshift le service ensemble hello lié **type** Hello service lié trop**AmazonRedshift**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1114">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1114">Property</span></span> | <span data-ttu-id="0ccf0-1115">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1115">Description</span></span> | <span data-ttu-id="0ccf0-1116">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1117">server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1117">server</span></span> |<span data-ttu-id="0ccf0-1118">Nom hôte ou adresse IP du serveur d’Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="0ccf0-1119">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1119">Yes</span></span> |
| <span data-ttu-id="0ccf0-1120">port</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1120">port</span></span> |<span data-ttu-id="0ccf0-1121">nombre de Hello de port TCP hello hello Amazon Redshift serveur utilise toolisten pour les connexions client.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="0ccf0-1122">Non, valeur par défaut : 5439</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="0ccf0-1123">database</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1123">database</span></span> |<span data-ttu-id="0ccf0-1124">Nom de la base de données Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="0ccf0-1125">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1125">Yes</span></span> |
| <span data-ttu-id="0ccf0-1126">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1126">username</span></span> |<span data-ttu-id="0ccf0-1127">Nom d’utilisateur qui a la base de données access toohello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="0ccf0-1128">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1128">Yes</span></span> |
| <span data-ttu-id="0ccf0-1129">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1129">password</span></span> |<span data-ttu-id="0ccf0-1130">Mot de passe pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1130">Password for hello user account.</span></span> |<span data-ttu-id="0ccf0-1131">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1132">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1132">Example</span></span>

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

<span data-ttu-id="0ccf0-1133">Pour plus d’informations, consultez l’article [Amazon Redshift connector (connecteur Amazon Redshift)](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-1134">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1134">Dataset</span></span>
<span data-ttu-id="0ccf0-1135">toodefine un jeu de données Amazon Redshift, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1136">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1136">Property</span></span> | <span data-ttu-id="0ccf0-1137">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1137">Description</span></span> | <span data-ttu-id="0ccf0-1138">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1139">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1139">tableName</span></span> |<span data-ttu-id="0ccf0-1140">Nom de table hello dans la base de données Amazon Redshift hello ce service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="0ccf0-1141">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="0ccf0-1142">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1142">Example</span></span>

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
<span data-ttu-id="0ccf0-1143">Pour plus d’informations, consultez l’article [Amazon Redshift connector (connecteur Amazon Redshift)](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1144">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="0ccf0-1145">Si vous copiez des données à partir d’Amazon Redshift, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-1146">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1146">Property</span></span> | <span data-ttu-id="0ccf0-1147">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1147">Description</span></span> | <span data-ttu-id="0ccf0-1148">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1148">Allowed values</span></span> | <span data-ttu-id="0ccf0-1149">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1150">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1150">query</span></span> |<span data-ttu-id="0ccf0-1151">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1152">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1152">SQL query string.</span></span> <span data-ttu-id="0ccf0-1153">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="0ccf0-1154">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1155">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1155">Example</span></span>

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
<span data-ttu-id="0ccf0-1156">Pour plus d’informations, consultez l’article [Amazon Redshift connector (connecteur Amazon Redshift)](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="0ccf0-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1158">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1158">Linked service</span></span>
<span data-ttu-id="0ccf0-1159">toodefine un IBM DB2 lié service, jeu hello **type** Hello service lié trop**OnPremisesDB2**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1160">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1160">Property</span></span> | <span data-ttu-id="0ccf0-1161">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1161">Description</span></span> | <span data-ttu-id="0ccf0-1162">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1163">server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1163">server</span></span> |<span data-ttu-id="0ccf0-1164">Nom du serveur de hello DB2.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="0ccf0-1165">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1165">Yes</span></span> |
| <span data-ttu-id="0ccf0-1166">database</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1166">database</span></span> |<span data-ttu-id="0ccf0-1167">Nom de la base de données hello DB2.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="0ccf0-1168">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1168">Yes</span></span> |
| <span data-ttu-id="0ccf0-1169">schema</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1169">schema</span></span> |<span data-ttu-id="0ccf0-1170">Nom de schéma hello hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="0ccf0-1171">nom du schéma Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="0ccf0-1172">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1172">No</span></span> |
| <span data-ttu-id="0ccf0-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1173">authenticationType</span></span> |<span data-ttu-id="0ccf0-1174">Type d’authentification utilisé tooconnect toohello base de données DB2.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="0ccf0-1175">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="0ccf0-1176">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1176">Yes</span></span> |
| <span data-ttu-id="0ccf0-1177">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1177">username</span></span> |<span data-ttu-id="0ccf0-1178">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="0ccf0-1179">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1179">No</span></span> |
| <span data-ttu-id="0ccf0-1180">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1180">password</span></span> |<span data-ttu-id="0ccf0-1181">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0ccf0-1182">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1182">No</span></span> |
| <span data-ttu-id="0ccf0-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1183">gatewayName</span></span> |<span data-ttu-id="0ccf0-1184">Nom de passerelle hello hello service Data Factory doit utiliser la base de données DB2 tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="0ccf0-1185">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1186">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1186">Example</span></span>
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
<span data-ttu-id="0ccf0-1187">Pour plus d’informations, consultez l’article [IBM DB2 connector (connecteur IBM DB2)](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-1188">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1188">Dataset</span></span>
<span data-ttu-id="0ccf0-1189">dataset toodefine DB2, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="0ccf0-1190">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1190">Property</span></span> | <span data-ttu-id="0ccf0-1191">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1191">Description</span></span> | <span data-ttu-id="0ccf0-1192">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1193">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1193">tableName</span></span> |<span data-ttu-id="0ccf0-1194">Nom de table hello dans l’instance de base de données DB2 hello ce service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="0ccf0-1195">Hello tableName respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="0ccf0-1196">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="0ccf0-1197">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1197">Example</span></span>
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

<span data-ttu-id="0ccf0-1198">Pour plus d’informations, consultez l’article [IBM DB2 connector (connecteur IBM DB2)](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1199">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1200">Si vous copiez des données à partir d’IBM DB2, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-1201">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1201">Property</span></span> | <span data-ttu-id="0ccf0-1202">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1202">Description</span></span> | <span data-ttu-id="0ccf0-1203">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1203">Allowed values</span></span> | <span data-ttu-id="0ccf0-1204">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1205">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1205">query</span></span> |<span data-ttu-id="0ccf0-1206">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1207">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1207">SQL query string.</span></span> <span data-ttu-id="0ccf0-1208">Par exemple : `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="0ccf0-1209">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1210">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1210">Example</span></span>
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
<span data-ttu-id="0ccf0-1211">Pour plus d’informations, consultez l’article [IBM DB2 connector (connecteur IBM DB2)](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="0ccf0-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1213">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1213">Linked service</span></span>
<span data-ttu-id="0ccf0-1214">toodefine un MySQL le service ensemble hello lié **type** Hello service lié trop**OnPremisesMySql**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1215">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1215">Property</span></span> | <span data-ttu-id="0ccf0-1216">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1216">Description</span></span> | <span data-ttu-id="0ccf0-1217">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1218">server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1218">server</span></span> |<span data-ttu-id="0ccf0-1219">Nom du serveur de MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="0ccf0-1220">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1220">Yes</span></span> |
| <span data-ttu-id="0ccf0-1221">database</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1221">database</span></span> |<span data-ttu-id="0ccf0-1222">Nom de la base de données MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="0ccf0-1223">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1223">Yes</span></span> |
| <span data-ttu-id="0ccf0-1224">schema</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1224">schema</span></span> |<span data-ttu-id="0ccf0-1225">Nom de schéma hello hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="0ccf0-1226">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1226">No</span></span> |
| <span data-ttu-id="0ccf0-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1227">authenticationType</span></span> |<span data-ttu-id="0ccf0-1228">Type d’authentification utilisé tooconnect toohello base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="0ccf0-1229">Les valeurs possibles sont les suivantes : `Basic`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="0ccf0-1230">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1230">Yes</span></span> |
| <span data-ttu-id="0ccf0-1231">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1231">username</span></span> |<span data-ttu-id="0ccf0-1232">Spécifiez la base de données utilisateur nom tooconnect toohello MySQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="0ccf0-1233">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1233">Yes</span></span> |
| <span data-ttu-id="0ccf0-1234">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1234">password</span></span> |<span data-ttu-id="0ccf0-1235">Spécifiez le mot de passe de compte d’utilisateur hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="0ccf0-1236">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1236">Yes</span></span> |
| <span data-ttu-id="0ccf0-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1237">gatewayName</span></span> |<span data-ttu-id="0ccf0-1238">Nom de passerelle hello hello service Data Factory doit utiliser la base de données MySQL tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="0ccf0-1239">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1240">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1240">Example</span></span>

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

<span data-ttu-id="0ccf0-1241">Pour plus d’informations, consultez l’article [MySQL connector (connecteur MySQL)](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-1242">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1242">Dataset</span></span>
<span data-ttu-id="0ccf0-1243">toodefine un jeu de données MySQL, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1244">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1244">Property</span></span> | <span data-ttu-id="0ccf0-1245">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1245">Description</span></span> | <span data-ttu-id="0ccf0-1246">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1247">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1247">tableName</span></span> |<span data-ttu-id="0ccf0-1248">Nom de table hello Bonjour instance de base de données MySQL service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="0ccf0-1249">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1250">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1250">Example</span></span>

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
<span data-ttu-id="0ccf0-1251">Pour plus d’informations, consultez l’article [MySQL connector (connecteur MySQL)](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1252">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1253">Si vous copiez des données à partir d’une base de données MySQL, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-1254">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1254">Property</span></span> | <span data-ttu-id="0ccf0-1255">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1255">Description</span></span> | <span data-ttu-id="0ccf0-1256">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1256">Allowed values</span></span> | <span data-ttu-id="0ccf0-1257">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1258">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1258">query</span></span> |<span data-ttu-id="0ccf0-1259">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1260">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1260">SQL query string.</span></span> <span data-ttu-id="0ccf0-1261">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="0ccf0-1262">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="0ccf0-1263">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1263">Example</span></span>
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

<span data-ttu-id="0ccf0-1264">Pour plus d’informations, consultez l’article [MySQL connector (connecteur MySQL)](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="0ccf0-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1266">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1266">Linked service</span></span>
<span data-ttu-id="0ccf0-1267">toodefine Oracle lié service, jeu hello **type** Hello service lié trop**OnPremisesOracle**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1268">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1268">Property</span></span> | <span data-ttu-id="0ccf0-1269">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1269">Description</span></span> | <span data-ttu-id="0ccf0-1270">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1271">driverType</span></span> | <span data-ttu-id="0ccf0-1272">Spécifier les données de toocopy toouse pilote à partir de / tooOracle de base de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="0ccf0-1273">Valeurs autorisées : **Microsoft** ou **ODP** (par défaut).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="0ccf0-1274">Consultez la section [Version prise en charge et installation](#supported-versions-and-installation) sur les détails du pilote.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="0ccf0-1275">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1275">No</span></span> |
| <span data-ttu-id="0ccf0-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1276">connectionString</span></span> | <span data-ttu-id="0ccf0-1277">Spécifiez les informations nécessaires d’instance de base de données Oracle tooconnect toohello pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="0ccf0-1278">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1278">Yes</span></span> |
| <span data-ttu-id="0ccf0-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1279">gatewayName</span></span> | <span data-ttu-id="0ccf0-1280">Nom de la passerelle hello qui est utilisé tooconnect toohello serveur Oracle locale</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="0ccf0-1281">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1282">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1282">Example</span></span>
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

<span data-ttu-id="0ccf0-1283">Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-1284">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1284">Dataset</span></span>
<span data-ttu-id="0ccf0-1285">toodefine un jeu de données Oracle, set hello **type** du jeu de données hello trop**OracleTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1286">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1286">Property</span></span> | <span data-ttu-id="0ccf0-1287">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1287">Description</span></span> | <span data-ttu-id="0ccf0-1288">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1289">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1289">tableName</span></span> |<span data-ttu-id="0ccf0-1290">Nom de table hello Bonjour base de données Oracle hello service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="0ccf0-1291">Non (si **oracleReaderQuery** de **OracleSource** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1292">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1292">Example</span></span>

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
<span data-ttu-id="0ccf0-1293">Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1294">Source Oracle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1295">Si vous copiez des données à partir d’une base de données Oracle, la valeur hello **type de source de** Hello activité de copie trop**OracleSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-1296">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1296">Property</span></span> | <span data-ttu-id="0ccf0-1297">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1297">Description</span></span> | <span data-ttu-id="0ccf0-1298">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1298">Allowed values</span></span> | <span data-ttu-id="0ccf0-1299">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1300">oracleReaderQuery</span></span> |<span data-ttu-id="0ccf0-1301">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1302">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1302">SQL query string.</span></span> <span data-ttu-id="0ccf0-1303">Par exemple : `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="0ccf0-1304">Si ce n’est pas spécifié, hello instruction SQL exécutée :`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="0ccf0-1305">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1306">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1306">Example</span></span>

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

<span data-ttu-id="0ccf0-1307">Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="0ccf0-1308">Récepteur Oracle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1309">Si vous copiez une base de données Oracle de données tooam, définissez hello **type de récepteur** Hello activité de copie trop**OracleSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-1310">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1310">Property</span></span> | <span data-ttu-id="0ccf0-1311">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1311">Description</span></span> | <span data-ttu-id="0ccf0-1312">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1312">Allowed values</span></span> | <span data-ttu-id="0ccf0-1313">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1314">writeBatchTimeout</span></span> |<span data-ttu-id="0ccf0-1315">Temps d’attente pour hello lot insert opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="0ccf0-1316">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1316">timespan</span></span><br/><br/> <span data-ttu-id="0ccf0-1317">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="0ccf0-1318">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1318">No</span></span> |
| <span data-ttu-id="0ccf0-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1319">writeBatchSize</span></span> |<span data-ttu-id="0ccf0-1320">Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="0ccf0-1321">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1321">Integer (number of rows)</span></span> |<span data-ttu-id="0ccf0-1322">Non (valeur par défaut : 100)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1322">No (default: 100)</span></span> |
| <span data-ttu-id="0ccf0-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="0ccf0-1324">Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="0ccf0-1325">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1325">A query statement.</span></span> |<span data-ttu-id="0ccf0-1326">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1326">No</span></span> |
| <span data-ttu-id="0ccf0-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="0ccf0-1328">Spécifiez nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="0ccf0-1329">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="0ccf0-1330">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1331">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1331">Example</span></span>
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
<span data-ttu-id="0ccf0-1332">Pour plus d’informations, consultez l’article [Oracle connector (connecteur Oracle)](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="0ccf0-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1334">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1334">Linked service</span></span>
<span data-ttu-id="0ccf0-1335">toodefine un PostgreSQL le service ensemble hello lié **type** Hello service lié trop**OnPremisesPostgreSql**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1336">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1336">Property</span></span> | <span data-ttu-id="0ccf0-1337">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1337">Description</span></span> | <span data-ttu-id="0ccf0-1338">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1339">server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1339">server</span></span> |<span data-ttu-id="0ccf0-1340">Nom du serveur de PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="0ccf0-1341">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1341">Yes</span></span> |
| <span data-ttu-id="0ccf0-1342">database</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1342">database</span></span> |<span data-ttu-id="0ccf0-1343">Nom de la base de données PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="0ccf0-1344">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1344">Yes</span></span> |
| <span data-ttu-id="0ccf0-1345">schema</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1345">schema</span></span> |<span data-ttu-id="0ccf0-1346">Nom de schéma hello hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="0ccf0-1347">nom du schéma Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="0ccf0-1348">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1348">No</span></span> |
| <span data-ttu-id="0ccf0-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1349">authenticationType</span></span> |<span data-ttu-id="0ccf0-1350">Type d’authentification utilisé tooconnect toohello base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="0ccf0-1351">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="0ccf0-1352">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1352">Yes</span></span> |
| <span data-ttu-id="0ccf0-1353">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1353">username</span></span> |<span data-ttu-id="0ccf0-1354">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="0ccf0-1355">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1355">No</span></span> |
| <span data-ttu-id="0ccf0-1356">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1356">password</span></span> |<span data-ttu-id="0ccf0-1357">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0ccf0-1358">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1358">No</span></span> |
| <span data-ttu-id="0ccf0-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1359">gatewayName</span></span> |<span data-ttu-id="0ccf0-1360">Nom de passerelle hello hello service Data Factory doit utiliser la base de données PostgreSQL tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="0ccf0-1361">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1362">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1362">Example</span></span>

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
<span data-ttu-id="0ccf0-1363">Pour plus d’informations, consultez l’article [PostgreSQL connector (connecteur PostgreSQL)](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-1364">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1364">Dataset</span></span>
<span data-ttu-id="0ccf0-1365">toodefine un jeu de données PostgreSQL, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1366">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1366">Property</span></span> | <span data-ttu-id="0ccf0-1367">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1367">Description</span></span> | <span data-ttu-id="0ccf0-1368">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1369">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1369">tableName</span></span> |<span data-ttu-id="0ccf0-1370">Nom de table hello Bonjour instance de base de données PostgreSQL service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="0ccf0-1371">Hello tableName respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="0ccf0-1372">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1373">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1373">Example</span></span>
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
<span data-ttu-id="0ccf0-1374">Pour plus d’informations, consultez l’article [PostgreSQL connector (connecteur PostgreSQL)](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1375">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1376">Si vous copiez des données à partir d’une base de données PostgreSQL, définissez hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-1377">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1377">Property</span></span> | <span data-ttu-id="0ccf0-1378">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1378">Description</span></span> | <span data-ttu-id="0ccf0-1379">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1379">Allowed values</span></span> | <span data-ttu-id="0ccf0-1380">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1381">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1381">query</span></span> |<span data-ttu-id="0ccf0-1382">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1383">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1383">SQL query string.</span></span> <span data-ttu-id="0ccf0-1384">Par exemple : "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="0ccf0-1385">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1386">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1386">Example</span></span>

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

<span data-ttu-id="0ccf0-1387">Pour plus d’informations, consultez l’article [PostgreSQL connector (connecteur PostgreSQL)](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="0ccf0-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="0ccf0-1389">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1389">Linked service</span></span>
<span data-ttu-id="0ccf0-1390">toodefine une SAP Business Warehouse (BW) le service ensemble hello lié **type** Hello service lié trop**SapBw**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="0ccf0-1391">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1391">Property</span></span> | <span data-ttu-id="0ccf0-1392">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1392">Description</span></span> | <span data-ttu-id="0ccf0-1393">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1393">Allowed values</span></span> | <span data-ttu-id="0ccf0-1394">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="0ccf0-1395">server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1395">server</span></span> | <span data-ttu-id="0ccf0-1396">Nom du serveur hello sur quel hello SAP BW instance réside.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="0ccf0-1397">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1397">string</span></span> | <span data-ttu-id="0ccf0-1398">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1398">Yes</span></span>
<span data-ttu-id="0ccf0-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1399">systemNumber</span></span> | <span data-ttu-id="0ccf0-1400">Numéro de système de hello système SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="0ccf0-1401">Nombre décimal à deux chiffres représenté sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="0ccf0-1402">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1402">Yes</span></span>
<span data-ttu-id="0ccf0-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1403">clientId</span></span> | <span data-ttu-id="0ccf0-1404">ID client du client hello Bonjour système SAP W.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="0ccf0-1405">Nombre décimal à trois chiffres représenté sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="0ccf0-1406">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1406">Yes</span></span>
<span data-ttu-id="0ccf0-1407">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1407">username</span></span> | <span data-ttu-id="0ccf0-1408">Nom d’utilisateur de hello qui a le serveur d’accès toohello SAP</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="0ccf0-1409">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1409">string</span></span> | <span data-ttu-id="0ccf0-1410">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1410">Yes</span></span>
<span data-ttu-id="0ccf0-1411">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1411">password</span></span> | <span data-ttu-id="0ccf0-1412">Mot de passe utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1412">Password for hello user.</span></span> | <span data-ttu-id="0ccf0-1413">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1413">string</span></span> | <span data-ttu-id="0ccf0-1414">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1414">Yes</span></span>
<span data-ttu-id="0ccf0-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1415">gatewayName</span></span> | <span data-ttu-id="0ccf0-1416">Nom de passerelle hello hello service Data Factory doit utiliser l’instance de SAP BW tooconnect toohello sur site.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="0ccf0-1417">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1417">string</span></span> | <span data-ttu-id="0ccf0-1418">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1418">Yes</span></span>
<span data-ttu-id="0ccf0-1419">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1419">encryptedCredential</span></span> | <span data-ttu-id="0ccf0-1420">chaîne d’identification de Hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="0ccf0-1421">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1421">string</span></span> | <span data-ttu-id="0ccf0-1422">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="0ccf0-1423">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1423">Example</span></span>

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

<span data-ttu-id="0ccf0-1424">Pour plus d’informations, consultez l’article [SAP Business Warehouse connector (connecteur SAP Business Warehouse)](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-1425">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1425">Dataset</span></span>
<span data-ttu-id="0ccf0-1426">toodefine un jeu de données SAP BW, jeu hello **type** du jeu de données hello trop**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="0ccf0-1427">Aucune propriété spécifique au type pris en charge pour le jeu de données hello SAP BW de type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="0ccf0-1428">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1428">Example</span></span>

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
<span data-ttu-id="0ccf0-1429">Pour plus d’informations, consultez l’article [SAP Business Warehouse connector (connecteur SAP Business Warehouse)](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1430">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1431">Si vous copiez des données à partir de SAP Business Warehouse, définissez hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-1432">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1432">Property</span></span> | <span data-ttu-id="0ccf0-1433">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1433">Description</span></span> | <span data-ttu-id="0ccf0-1434">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1434">Allowed values</span></span> | <span data-ttu-id="0ccf0-1435">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1436">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1436">query</span></span> | <span data-ttu-id="0ccf0-1437">Spécifie les données de tooread requête hello MDX à partir de l’instance de SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="0ccf0-1438">Requête MDX.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1438">MDX query.</span></span> | <span data-ttu-id="0ccf0-1439">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1440">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1440">Example</span></span>

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

<span data-ttu-id="0ccf0-1441">Pour plus d’informations, consultez l’article [SAP Business Warehouse connector (connecteur SAP Business Warehouse)](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="0ccf0-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1443">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1443">Linked service</span></span>
<span data-ttu-id="0ccf0-1444">toodefine une SAP HANA le service ensemble hello lié **type** Hello service lié trop**SapHana**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="0ccf0-1445">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1445">Property</span></span> | <span data-ttu-id="0ccf0-1446">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1446">Description</span></span> | <span data-ttu-id="0ccf0-1447">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1447">Allowed values</span></span> | <span data-ttu-id="0ccf0-1448">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="0ccf0-1449">server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1449">server</span></span> | <span data-ttu-id="0ccf0-1450">Nom du serveur hello sur quel hello SAP HANA instance réside.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="0ccf0-1451">Si votre serveur utilise un port personnalisé, spécifiez `server:port`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="0ccf0-1452">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1452">string</span></span> | <span data-ttu-id="0ccf0-1453">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1453">Yes</span></span>
<span data-ttu-id="0ccf0-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1454">authenticationType</span></span> | <span data-ttu-id="0ccf0-1455">Type d'authentification.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1455">Type of authentication.</span></span> | <span data-ttu-id="0ccf0-1456">chaîne.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1456">string.</span></span> <span data-ttu-id="0ccf0-1457">« Basic » ou « Windows »</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="0ccf0-1458">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1458">Yes</span></span> 
<span data-ttu-id="0ccf0-1459">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1459">username</span></span> | <span data-ttu-id="0ccf0-1460">Nom d’utilisateur de hello qui a le serveur d’accès toohello SAP</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="0ccf0-1461">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1461">string</span></span> | <span data-ttu-id="0ccf0-1462">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1462">Yes</span></span>
<span data-ttu-id="0ccf0-1463">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1463">password</span></span> | <span data-ttu-id="0ccf0-1464">Mot de passe utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1464">Password for hello user.</span></span> | <span data-ttu-id="0ccf0-1465">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1465">string</span></span> | <span data-ttu-id="0ccf0-1466">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1466">Yes</span></span>
<span data-ttu-id="0ccf0-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1467">gatewayName</span></span> | <span data-ttu-id="0ccf0-1468">Nom de passerelle hello hello service Data Factory doit utiliser l’instance de SAP HANA tooconnect toohello sur site.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="0ccf0-1469">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1469">string</span></span> | <span data-ttu-id="0ccf0-1470">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1470">Yes</span></span>
<span data-ttu-id="0ccf0-1471">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1471">encryptedCredential</span></span> | <span data-ttu-id="0ccf0-1472">chaîne d’identification de Hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="0ccf0-1473">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1473">string</span></span> | <span data-ttu-id="0ccf0-1474">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="0ccf0-1475">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1475">Example</span></span>

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
<span data-ttu-id="0ccf0-1476">Pour plus d’informations, consultez l’article [SAP HANA connector (connecteur SAP HANA)](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="0ccf0-1477">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1477">Dataset</span></span>
<span data-ttu-id="0ccf0-1478">toodefine un jeu de données SAP HANA, jeu hello **type** du jeu de données hello trop**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="0ccf0-1479">Aucune propriété spécifique au type pris en charge pour le dataset de SAP HANA hello de type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="0ccf0-1480">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1480">Example</span></span>

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
<span data-ttu-id="0ccf0-1481">Pour plus d’informations, consultez l’article [SAP HANA connector (connecteur SAP HANA)](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1482">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1483">Si vous copiez des données à partir d’un magasin de données SAP HANA, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-1484">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1484">Property</span></span> | <span data-ttu-id="0ccf0-1485">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1485">Description</span></span> | <span data-ttu-id="0ccf0-1486">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1486">Allowed values</span></span> | <span data-ttu-id="0ccf0-1487">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1488">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1488">query</span></span> | <span data-ttu-id="0ccf0-1489">Spécifie les hello requête tooread de données SQL à partir de l’instance de SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="0ccf0-1490">Requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1490">SQL query.</span></span> | <span data-ttu-id="0ccf0-1491">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="0ccf0-1492">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1492">Example</span></span>


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

<span data-ttu-id="0ccf0-1493">Pour plus d’informations, consultez l’article [SAP HANA connector (connecteur SAP HANA)](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="0ccf0-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1495">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1495">Linked service</span></span>
<span data-ttu-id="0ccf0-1496">Vous créez un service lié de type **OnPremisesSqlServer** toolink une fabrique de données de tooa de base de données locale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="0ccf0-1497">Hello tableau suivant fournit la description du service de SQL Server lié JSON éléments tooon local spécifique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="0ccf0-1498">Hello tableau suivant fournit la description pour JSON éléments tooSQL spécifique service du serveur lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="0ccf0-1499">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1499">Property</span></span> | <span data-ttu-id="0ccf0-1500">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1500">Description</span></span> | <span data-ttu-id="0ccf0-1501">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1502">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1502">type</span></span> |<span data-ttu-id="0ccf0-1503">propriété de type Hello doit indiquer : **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="0ccf0-1504">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1504">Yes</span></span> |
| <span data-ttu-id="0ccf0-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1505">connectionString</span></span> |<span data-ttu-id="0ccf0-1506">Spécifiez les informations connectionString nécessaires de base de données SQL Server tooconnect toohello local à l’aide de l’authentification Windows ou authentification SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="0ccf0-1507">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1507">Yes</span></span> |
| <span data-ttu-id="0ccf0-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1508">gatewayName</span></span> |<span data-ttu-id="0ccf0-1509">Nom de passerelle hello hello service Data Factory doit utiliser la base de données SQL Server tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="0ccf0-1510">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1510">Yes</span></span> |
| <span data-ttu-id="0ccf0-1511">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1511">username</span></span> |<span data-ttu-id="0ccf0-1512">Spécifiez le nom d’utilisateur si vous utilisez l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="0ccf0-1513">Exemple : **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="0ccf0-1514">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1514">No</span></span> |
| <span data-ttu-id="0ccf0-1515">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1515">password</span></span> |<span data-ttu-id="0ccf0-1516">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0ccf0-1517">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1517">No</span></span> |

<span data-ttu-id="0ccf0-1518">Vous pouvez chiffrer les informations d’identification à l’aide de hello **New-AzureRmDataFactoryEncryptValue** applet de commande et les utiliser dans la chaîne de connexion hello comme indiqué dans hello exemple suivant (**EncryptedCredential** propriété) :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="0ccf0-1519">Exemple : JSON pour utilisation de l’authentification SQL</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="0ccf0-1520">Exemple : JSON pour utilisation de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="0ccf0-1521">Si le nom d’utilisateur et mot de passe sont spécifiés, la passerelle les utilise tooimpersonate hello base de données utilisateur spécifié compte tooconnect toohello locale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="0ccf0-1522">Dans le cas contraire, la passerelle connecte toohello SQL Server directement avec le contexte de sécurité hello de passerelle (son compte de démarrage).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="0ccf0-1523">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-1524">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1524">Dataset</span></span>
<span data-ttu-id="0ccf0-1525">toodefine un jeu de données SQL Server, jeu hello **type** du jeu de données hello trop**SqlServerTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1526">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1526">Property</span></span> | <span data-ttu-id="0ccf0-1527">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1527">Description</span></span> | <span data-ttu-id="0ccf0-1528">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1529">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1529">tableName</span></span> |<span data-ttu-id="0ccf0-1530">Nom de la table de hello ou la vue d’instance de base de données SQL Server hello service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="0ccf0-1531">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1532">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1532">Example</span></span>
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

<span data-ttu-id="0ccf0-1533">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1534">Source SQL dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1535">Si vous copiez des données à partir d’une base de données SQL Server, la valeur hello **type de source de** Hello activité de copie trop**SqlSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-1536">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1536">Property</span></span> | <span data-ttu-id="0ccf0-1537">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1537">Description</span></span> | <span data-ttu-id="0ccf0-1538">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1538">Allowed values</span></span> | <span data-ttu-id="0ccf0-1539">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1540">sqlReaderQuery</span></span> |<span data-ttu-id="0ccf0-1541">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1542">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1542">SQL query string.</span></span> <span data-ttu-id="0ccf0-1543">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="0ccf0-1544">Peut faire référence à plusieurs tables de base de données hello référencé par le jeu de données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="0ccf0-1545">Si non spécifié, hello instruction SQL exécutée : select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="0ccf0-1546">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1546">No</span></span> |
| <span data-ttu-id="0ccf0-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="0ccf0-1548">Nom de hello procédure stockée qui lit les données à partir de la table de source de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="0ccf0-1549">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-1550">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1550">No</span></span> |
| <span data-ttu-id="0ccf0-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1551">storedProcedureParameters</span></span> |<span data-ttu-id="0ccf0-1552">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-1553">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1553">Name/value pairs.</span></span> <span data-ttu-id="0ccf0-1554">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="0ccf0-1555">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1555">No</span></span> |

<span data-ttu-id="0ccf0-1556">Si hello **sqlReaderQuery** est spécifié pour hello SqlSource, hello activité de copie s’exécute cette requête sur des données hello tooget hello base de données SQL Server source.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="0ccf0-1557">Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="0ccf0-1558">Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello sont utilisée toobuild un toorun requête select sur hello de base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="0ccf0-1559">Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="0ccf0-1560">Lorsque vous utilisez **sqlReaderStoredProcedureName**, vous devez toujours toospecify une valeur pour hello **tableName** propriété dans le dataset hello JSON.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="0ccf0-1561">Cependant, il n’existe aucune validation effectuée pour cette table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="0ccf0-1562">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1562">Example</span></span>
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

<span data-ttu-id="0ccf0-1563">Dans cet exemple, **sqlReaderQuery** est spécifié pour hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="0ccf0-1564">Hello activité de copie s’exécute cette requête par rapport aux données de base de données SQL Server source tooget hello de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="0ccf0-1565">Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="0ccf0-1566">Hello sqlReaderQuery permettre faire référence à plusieurs tables de base de données hello référencé par le jeu de données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="0ccf0-1567">Il n’est pas limité tooonly hello tableau comme hello typeProperty de tableName du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="0ccf0-1568">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello sont utilisée toobuild un toorun requête select sur hello de base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="0ccf0-1569">Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="0ccf0-1570">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="0ccf0-1571">Récepteur SQL dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1572">Si vous copiez des données tooa base de données SQL, la valeur hello **type de récepteur** Hello activité de copie trop**SqlSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-1573">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1573">Property</span></span> | <span data-ttu-id="0ccf0-1574">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1574">Description</span></span> | <span data-ttu-id="0ccf0-1575">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1575">Allowed values</span></span> | <span data-ttu-id="0ccf0-1576">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1577">writeBatchTimeout</span></span> |<span data-ttu-id="0ccf0-1578">Temps d’attente pour hello lot insert opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="0ccf0-1579">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1579">timespan</span></span><br/><br/> <span data-ttu-id="0ccf0-1580">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="0ccf0-1581">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1581">No</span></span> |
| <span data-ttu-id="0ccf0-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1582">writeBatchSize</span></span> |<span data-ttu-id="0ccf0-1583">Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="0ccf0-1584">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1584">Integer (number of rows)</span></span> |<span data-ttu-id="0ccf0-1585">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="0ccf0-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="0ccf0-1587">Spécifier la requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="0ccf0-1588">Consultez la [section sur la répétition](#repeatability-during-copy) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="0ccf0-1589">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1589">A query statement.</span></span> |<span data-ttu-id="0ccf0-1590">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1590">No</span></span> |
| <span data-ttu-id="0ccf0-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="0ccf0-1592">Spécifiez nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="0ccf0-1593">Consultez la [section sur la répétition](#repeatability-during-copy) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="0ccf0-1594">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="0ccf0-1595">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1595">No</span></span> |
| <span data-ttu-id="0ccf0-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="0ccf0-1597">Nom de hello procédure stockée que les données upserts (mises à jour/insertion) dans la table cible hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="0ccf0-1598">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-1599">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1599">No</span></span> |
| <span data-ttu-id="0ccf0-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1600">storedProcedureParameters</span></span> |<span data-ttu-id="0ccf0-1601">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="0ccf0-1602">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1602">Name/value pairs.</span></span> <span data-ttu-id="0ccf0-1603">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="0ccf0-1604">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1604">No</span></span> |
| <span data-ttu-id="0ccf0-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1605">sqlWriterTableType</span></span> |<span data-ttu-id="0ccf0-1606">Spécifiez toobe de nom de type de table utilisée dans la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="0ccf0-1607">Activité de copie rend les données de hello déplacées disponibles dans une table temporaire avec ce type de table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="0ccf0-1608">Code de procédure stockée puis de fusionner des données hello copiées avec les données existantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="0ccf0-1609">Nom de type de table.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1609">A table type name.</span></span> |<span data-ttu-id="0ccf0-1610">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1611">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1611">Example</span></span>
<span data-ttu-id="0ccf0-1612">pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="0ccf0-1613">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

<span data-ttu-id="0ccf0-1614">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="0ccf0-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1616">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1616">Linked service</span></span>
<span data-ttu-id="0ccf0-1617">toodefine un Sybase le service ensemble hello lié **type** Hello service lié trop**OnPremisesSybase**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1618">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1618">Property</span></span> | <span data-ttu-id="0ccf0-1619">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1619">Description</span></span> | <span data-ttu-id="0ccf0-1620">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1621">server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1621">server</span></span> |<span data-ttu-id="0ccf0-1622">Nom du serveur de Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="0ccf0-1623">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1623">Yes</span></span> |
| <span data-ttu-id="0ccf0-1624">database</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1624">database</span></span> |<span data-ttu-id="0ccf0-1625">Nom de la base de données Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="0ccf0-1626">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1626">Yes</span></span> |
| <span data-ttu-id="0ccf0-1627">schema</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1627">schema</span></span> |<span data-ttu-id="0ccf0-1628">Nom de schéma hello hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="0ccf0-1629">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1629">No</span></span> |
| <span data-ttu-id="0ccf0-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1630">authenticationType</span></span> |<span data-ttu-id="0ccf0-1631">Type d’authentification utilisé tooconnect toohello base de données Sybase.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="0ccf0-1632">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="0ccf0-1633">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1633">Yes</span></span> |
| <span data-ttu-id="0ccf0-1634">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1634">username</span></span> |<span data-ttu-id="0ccf0-1635">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="0ccf0-1636">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1636">No</span></span> |
| <span data-ttu-id="0ccf0-1637">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1637">password</span></span> |<span data-ttu-id="0ccf0-1638">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0ccf0-1639">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1639">No</span></span> |
| <span data-ttu-id="0ccf0-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1640">gatewayName</span></span> |<span data-ttu-id="0ccf0-1641">Nom de passerelle hello hello service Data Factory doit utiliser la base de données Sybase tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="0ccf0-1642">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1643">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1643">Example</span></span>
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

<span data-ttu-id="0ccf0-1644">Pour plus d’informations, consultez l’article [Sybase connector (connecteur Sybase)](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-1645">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1645">Dataset</span></span>
<span data-ttu-id="0ccf0-1646">toodefine un jeu de données Sybase, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1647">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1647">Property</span></span> | <span data-ttu-id="0ccf0-1648">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1648">Description</span></span> | <span data-ttu-id="0ccf0-1649">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1650">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1650">tableName</span></span> |<span data-ttu-id="0ccf0-1651">Nom de table hello Bonjour instance de base de données Sybase service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="0ccf0-1652">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1653">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1653">Example</span></span>

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

<span data-ttu-id="0ccf0-1654">Pour plus d’informations, consultez l’article [Sybase connector (connecteur Sybase)](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1655">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1656">Si vous copiez des données à partir d’une base de données Sybase, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-1657">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1657">Property</span></span> | <span data-ttu-id="0ccf0-1658">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1658">Description</span></span> | <span data-ttu-id="0ccf0-1659">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1659">Allowed values</span></span> | <span data-ttu-id="0ccf0-1660">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1661">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1661">query</span></span> |<span data-ttu-id="0ccf0-1662">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1663">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1663">SQL query string.</span></span> <span data-ttu-id="0ccf0-1664">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="0ccf0-1665">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1666">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1666">Example</span></span>

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

<span data-ttu-id="0ccf0-1667">Pour plus d’informations, consultez l’article [Sybase connector (connecteur Sybase)](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="0ccf0-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1669">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1669">Linked service</span></span>
<span data-ttu-id="0ccf0-1670">toodefine un Teradata le service ensemble hello lié **type** Hello service lié trop**OnPremisesTeradata**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1671">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1671">Property</span></span> | <span data-ttu-id="0ccf0-1672">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1672">Description</span></span> | <span data-ttu-id="0ccf0-1673">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1674">server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1674">server</span></span> |<span data-ttu-id="0ccf0-1675">Nom du serveur de Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="0ccf0-1676">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1676">Yes</span></span> |
| <span data-ttu-id="0ccf0-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1677">authenticationType</span></span> |<span data-ttu-id="0ccf0-1678">Type d’authentification utilisé tooconnect toohello base de données Teradata.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="0ccf0-1679">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="0ccf0-1680">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1680">Yes</span></span> |
| <span data-ttu-id="0ccf0-1681">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1681">username</span></span> |<span data-ttu-id="0ccf0-1682">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="0ccf0-1683">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1683">No</span></span> |
| <span data-ttu-id="0ccf0-1684">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1684">password</span></span> |<span data-ttu-id="0ccf0-1685">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0ccf0-1686">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1686">No</span></span> |
| <span data-ttu-id="0ccf0-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1687">gatewayName</span></span> |<span data-ttu-id="0ccf0-1688">Nom de passerelle hello hello service Data Factory doit utiliser la base de données Teradata tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="0ccf0-1689">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1690">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1690">Example</span></span>
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

<span data-ttu-id="0ccf0-1691">Pour plus d’informations, consultez l’article [Teradata connector (connecteur Teradata)](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-1692">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1692">Dataset</span></span>
<span data-ttu-id="0ccf0-1693">toodefine un jeu de données Teradata Blob, jeu hello **type** du jeu de données hello trop**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="0ccf0-1694">Actuellement, il n’y a aucune propriété de type pris en charge pour le jeu de données Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="0ccf0-1695">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1695">Example</span></span>
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

<span data-ttu-id="0ccf0-1696">Pour plus d’informations, consultez l’article [Teradata connector (connecteur Teradata)](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1697">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1698">Si vous copiez des données à partir d’une base de données Teradata, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-1699">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1699">Property</span></span> | <span data-ttu-id="0ccf0-1700">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1700">Description</span></span> | <span data-ttu-id="0ccf0-1701">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1701">Allowed values</span></span> | <span data-ttu-id="0ccf0-1702">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1703">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1703">query</span></span> |<span data-ttu-id="0ccf0-1704">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1705">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1705">SQL query string.</span></span> <span data-ttu-id="0ccf0-1706">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="0ccf0-1707">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1708">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1708">Example</span></span>

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

<span data-ttu-id="0ccf0-1709">Pour plus d’informations, consultez l’article [Teradata connector (connecteur Teradata)](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="0ccf0-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="0ccf0-1711">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1711">Linked service</span></span>
<span data-ttu-id="0ccf0-1712">toodefine un Cassandra le service ensemble hello lié **type** Hello service lié trop**OnPremisesCassandra**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1713">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1713">Property</span></span> | <span data-ttu-id="0ccf0-1714">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1714">Description</span></span> | <span data-ttu-id="0ccf0-1715">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1716">host</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1716">host</span></span> |<span data-ttu-id="0ccf0-1717">Une ou plusieurs adresses IP ou noms d’hôte de serveurs Cassandra.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="0ccf0-1718">Spécifiez une liste séparée par des virgules des adresses IP ou hôte noms tooconnect tooall serveurs simultanément.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="0ccf0-1719">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1719">Yes</span></span> |
| <span data-ttu-id="0ccf0-1720">port</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1720">port</span></span> |<span data-ttu-id="0ccf0-1721">Hello le port TCP qui hello du serveur de Cassandra utilise toolisten pour les connexions client.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="0ccf0-1722">Non, valeur par défaut : 9042</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="0ccf0-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1723">authenticationType</span></span> |<span data-ttu-id="0ccf0-1724">Basique ou anonyme</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="0ccf0-1725">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1725">Yes</span></span> |
| <span data-ttu-id="0ccf0-1726">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1726">username</span></span> |<span data-ttu-id="0ccf0-1727">Spécifiez le nom d’utilisateur pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="0ccf0-1728">Oui, si authenticationType a la valeur tooBasic.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="0ccf0-1729">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1729">password</span></span> |<span data-ttu-id="0ccf0-1730">Spécifiez le mot de passe de compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="0ccf0-1731">Oui, si authenticationType a la valeur tooBasic.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="0ccf0-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1732">gatewayName</span></span> |<span data-ttu-id="0ccf0-1733">nom Hello de passerelle hello est utilisé tooconnect toohello Cassandra base de données locale.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="0ccf0-1734">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1734">Yes</span></span> |
| <span data-ttu-id="0ccf0-1735">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1735">encryptedCredential</span></span> |<span data-ttu-id="0ccf0-1736">Informations d’identification chiffrées par la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="0ccf0-1737">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1738">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1738">Example</span></span>

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

<span data-ttu-id="0ccf0-1739">Pour plus d’informations, consultez l’article [Cassandra connector (connecteur Cassandra)](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-1740">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1740">Dataset</span></span>
<span data-ttu-id="0ccf0-1741">toodefine un dataset Cassandra, jeu hello **type** du jeu de données hello trop**CassandraTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1742">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1742">Property</span></span> | <span data-ttu-id="0ccf0-1743">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1743">Description</span></span> | <span data-ttu-id="0ccf0-1744">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1745">espace de clé</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1745">keyspace</span></span> |<span data-ttu-id="0ccf0-1746">Nom de l’espace de clés hello ou un schéma de base de données Cassandra.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="0ccf0-1747">Oui (si la **requête** pour **CassandraSource** n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="0ccf0-1748">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1748">tableName</span></span> |<span data-ttu-id="0ccf0-1749">Nom de table hello Cassandra de base de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="0ccf0-1750">Oui (si la **requête** pour **CassandraSource** n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1751">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1751">Example</span></span>

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

<span data-ttu-id="0ccf0-1752">Pour plus d’informations, consultez l’article [Cassandra connector (connecteur Cassandra)](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1753">Source Cassandra dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1754">Si vous copiez des données à partir de Cassandra, définissez hello **type de source de** Hello activité de copie trop**CassandraSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-1755">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1755">Property</span></span> | <span data-ttu-id="0ccf0-1756">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1756">Description</span></span> | <span data-ttu-id="0ccf0-1757">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1757">Allowed values</span></span> | <span data-ttu-id="0ccf0-1758">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1759">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1759">query</span></span> |<span data-ttu-id="0ccf0-1760">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1761">Requête SQL-92 ou requête CQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="0ccf0-1762">Reportez-vous à [référence CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="0ccf0-1763">Lorsque vous utilisez la requête SQL, spécifiez **nom d’espace de clés name.table** toorepresent hello tableau tooquery.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="0ccf0-1764">Non (si tableName et keyspace sur le jeu de données sont définis).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="0ccf0-1765">Niveau de cohérence</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1765">consistencyLevel</span></span> |<span data-ttu-id="0ccf0-1766">niveau de cohérence Hello Spécifie le nombre de réplicas doit répondre de requête de lecture tooa avant de retourner l’application data toohello client.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="0ccf0-1767">Les vérifications Cassandra hello un nombre spécifié de réplicas pour la requête de lecture hello toosatisfy de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="0ccf0-1768">UN, DEUX, TROIS, QUORUM, TOUT, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="0ccf0-1769">Reportez-vous à [Configuring data consistency (Configuration de la cohérence des données)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="0ccf0-1770">Non.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1770">No.</span></span> <span data-ttu-id="0ccf0-1771">La valeur par défaut est UN.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1772">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
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

<span data-ttu-id="0ccf0-1773">Pour plus d’informations, consultez l’article [Cassandra connector (connecteur Cassandra)](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="0ccf0-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-1775">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1775">Linked service</span></span>
<span data-ttu-id="0ccf0-1776">toodefine un MongoDB le service ensemble hello lié **type** Hello service lié trop**OnPremisesMongoDB**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1777">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1777">Property</span></span> | <span data-ttu-id="0ccf0-1778">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1778">Description</span></span> | <span data-ttu-id="0ccf0-1779">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1780">server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1780">server</span></span> |<span data-ttu-id="0ccf0-1781">Nom hôte ou adresse IP du serveur de MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="0ccf0-1782">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1782">Yes</span></span> |
| <span data-ttu-id="0ccf0-1783">port</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1783">port</span></span> |<span data-ttu-id="0ccf0-1784">Le port TCP qui hello MongoDB serveur utilise toolisten pour les connexions client.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="0ccf0-1785">Facultatif, valeur par défaut : 27017</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="0ccf0-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1786">authenticationType</span></span> |<span data-ttu-id="0ccf0-1787">De base ou anonyme.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="0ccf0-1788">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1788">Yes</span></span> |
| <span data-ttu-id="0ccf0-1789">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1789">username</span></span> |<span data-ttu-id="0ccf0-1790">Tooaccess du compte utilisateur MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="0ccf0-1791">Oui (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="0ccf0-1792">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1792">password</span></span> |<span data-ttu-id="0ccf0-1793">Mot de passe utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1793">Password for hello user.</span></span> |<span data-ttu-id="0ccf0-1794">Oui (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="0ccf0-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1795">authSource</span></span> |<span data-ttu-id="0ccf0-1796">Nom de la base de données MongoDB hello que vous souhaitez toouse toocheck vos informations d’identification pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="0ccf0-1797">Facultatif (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="0ccf0-1798">par défaut : utilise le compte d’administrateur hello et de la base de données de hello spécifié à l’aide de la propriété databaseName.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="0ccf0-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1799">databaseName</span></span> |<span data-ttu-id="0ccf0-1800">Nom de la base de données MongoDB hello que vous souhaitez tooaccess.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="0ccf0-1801">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1801">Yes</span></span> |
| <span data-ttu-id="0ccf0-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1802">gatewayName</span></span> |<span data-ttu-id="0ccf0-1803">Nom de la passerelle hello qui accède au magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="0ccf0-1804">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1804">Yes</span></span> |
| <span data-ttu-id="0ccf0-1805">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1805">encryptedCredential</span></span> |<span data-ttu-id="0ccf0-1806">Informations d’identification chiffrées par la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="0ccf0-1807">Facultatif</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1808">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="0ccf0-1809">Pour plus d’informations, consultez l’article [MongoDB connector (connecteur MongoDB)](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-1810">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1810">Dataset</span></span>
<span data-ttu-id="0ccf0-1811">toodefine un jeu de données MongoDB, jeu hello **type** du jeu de données hello trop**MongoDbCollection**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1812">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1812">Property</span></span> | <span data-ttu-id="0ccf0-1813">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1813">Description</span></span> | <span data-ttu-id="0ccf0-1814">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1815">collectionName</span></span> |<span data-ttu-id="0ccf0-1816">Nom de collection hello dans la base de données MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="0ccf0-1817">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1818">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1818">Example</span></span>

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

<span data-ttu-id="0ccf0-1819">Pour plus d’informations, consultez l’article [MongoDB connector (connecteur MongoDB)](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1820">Source MongoDB dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1821">Si vous copiez des données à partir de MongoDB, définissez hello **type de source de** Hello activité de copie trop**MongoDbSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-1822">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1822">Property</span></span> | <span data-ttu-id="0ccf0-1823">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1823">Description</span></span> | <span data-ttu-id="0ccf0-1824">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1824">Allowed values</span></span> | <span data-ttu-id="0ccf0-1825">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1826">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1826">query</span></span> |<span data-ttu-id="0ccf0-1827">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-1828">Chaîne de requête SQL-92.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1828">SQL-92 query string.</span></span> <span data-ttu-id="0ccf0-1829">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="0ccf0-1830">Non (si **collectionName** du **jeu de données** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1831">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1831">Example</span></span>

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

<span data-ttu-id="0ccf0-1832">Pour plus d’informations, consultez l’article [MongoDB connector (connecteur MongoDB)](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="0ccf0-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="0ccf0-1834">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1834">Linked service</span></span>
<span data-ttu-id="0ccf0-1835">toodefine un S3 Amazon le service ensemble hello lié **type** Hello service lié trop**AwsAccessKey**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-1836">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1836">Property</span></span> | <span data-ttu-id="0ccf0-1837">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1837">Description</span></span> | <span data-ttu-id="0ccf0-1838">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1838">Allowed values</span></span> | <span data-ttu-id="0ccf0-1839">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1840">accessKeyID</span></span> |<span data-ttu-id="0ccf0-1841">ID de clé d’accès de clé secrète hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="0ccf0-1842">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1842">string</span></span> |<span data-ttu-id="0ccf0-1843">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1843">Yes</span></span> |
| <span data-ttu-id="0ccf0-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1844">secretAccessKey</span></span> |<span data-ttu-id="0ccf0-1845">clé d’accès de clé secrète Hello elle-même.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1845">hello secret access key itself.</span></span> |<span data-ttu-id="0ccf0-1846">Chaîne secrète chiffrée</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1846">Encrypted secret string</span></span> |<span data-ttu-id="0ccf0-1847">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-1848">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1848">Example</span></span>
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

<span data-ttu-id="0ccf0-1849">Pour plus d’informations, consultez l’article [Amazon S3 connector (connecteur Amazon S3)](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-1850">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1850">Dataset</span></span>
<span data-ttu-id="0ccf0-1851">toodefine un S3 Amazon dataset, ensemble hello **type** du jeu de données hello trop**AmazonS3**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1852">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1852">Property</span></span> | <span data-ttu-id="0ccf0-1853">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1853">Description</span></span> | <span data-ttu-id="0ccf0-1854">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1854">Allowed values</span></span> | <span data-ttu-id="0ccf0-1855">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1856">bucketName</span></span> |<span data-ttu-id="0ccf0-1857">nom du compartiment Hello S3.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="0ccf0-1858">String</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1858">String</span></span> |<span data-ttu-id="0ccf0-1859">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1859">Yes</span></span> |
| <span data-ttu-id="0ccf0-1860">key</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1860">key</span></span> |<span data-ttu-id="0ccf0-1861">clé d’objet Hello S3.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1861">hello S3 object key.</span></span> |<span data-ttu-id="0ccf0-1862">String</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1862">String</span></span> |<span data-ttu-id="0ccf0-1863">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1863">No</span></span> |
| <span data-ttu-id="0ccf0-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1864">prefix</span></span> |<span data-ttu-id="0ccf0-1865">Préfixe de la clé d’objet hello S3.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="0ccf0-1866">Les objets dont les clés commencent par ce préfixe sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="0ccf0-1867">S’applique uniquement lorsque la clé est vide.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="0ccf0-1868">string</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1868">String</span></span> |<span data-ttu-id="0ccf0-1869">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1869">No</span></span> |
| <span data-ttu-id="0ccf0-1870">version</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1870">version</span></span> |<span data-ttu-id="0ccf0-1871">version Hello d’objet S3 si le contrôle de version S3 est activé.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="0ccf0-1872">String</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1872">String</span></span> |<span data-ttu-id="0ccf0-1873">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1873">No</span></span> |
| <span data-ttu-id="0ccf0-1874">format</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1874">format</span></span> | <span data-ttu-id="0ccf0-1875">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0ccf0-1876">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="0ccf0-1877">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0ccf0-1878">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0ccf0-1879">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1879">No</span></span> | |
| <span data-ttu-id="0ccf0-1880">compression</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1880">compression</span></span> | <span data-ttu-id="0ccf0-1881">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="0ccf0-1882">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="0ccf0-1883">les niveaux de Hello pris en charge sont : **Optimal** et **plus rapide**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0ccf0-1884">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0ccf0-1885">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="0ccf0-1886">bucketName + clé spécifie l’emplacement hello d’objet hello S3 où compartiment est le conteneur racine hello S3 objets et la clé est hello chemin d’accès complet tooS3 objet.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="0ccf0-1887">Exemple : exemple de jeu de données avec le préfixe</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="0ccf0-1888">Exemple : exemple de jeu de données (avec la version)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="0ccf0-1889">Exemple : chemins d’accès dynamiques pour S3</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="0ccf0-1890">Dans l’exemple hello, nous utilisons des valeurs fixes pour les propriétés de clé et bucketName dans le jeu de données hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="0ccf0-1891">Vous pouvez avoir Data Factory calculer la clé de hello et bucketName dynamiquement au moment de l’exécution à l’aide de variables système tels que SliceStart.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="0ccf0-1892">Vous pouvez effectuer même hello pour la propriété de préfixe hello d’un jeu de données Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="0ccf0-1893">Pour obtenir la liste des fonctions et variables prises en charge, consultez [Variables système et fonctions Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="0ccf0-1894">Pour plus d’informations, consultez l’article [Amazon S3 connector (connecteur Amazon S3)](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1895">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1896">Si vous copiez des données à partir d’Amazon S3, définissez hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="0ccf0-1897">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1897">Property</span></span> | <span data-ttu-id="0ccf0-1898">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1898">Description</span></span> | <span data-ttu-id="0ccf0-1899">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1899">Allowed values</span></span> | <span data-ttu-id="0ccf0-1900">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1901">recursive</span></span> |<span data-ttu-id="0ccf0-1902">Spécifie si la liste de toorecursively S3 objets sous le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="0ccf0-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1903">true/false</span></span> |<span data-ttu-id="0ccf0-1904">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="0ccf0-1905">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1905">Example</span></span>


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

<span data-ttu-id="0ccf0-1906">Pour plus d’informations, consultez l’article [Amazon S3 connector (connecteur Amazon S3)](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="0ccf0-1907">Système de fichiers</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="0ccf0-1908">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1908">Linked service</span></span>
<span data-ttu-id="0ccf0-1909">Vous pouvez lier une fabrique de données Azure local fichier système tooan avec hello **serveur de fichiers local** service lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="0ccf0-1910">Hello tableau suivant fournit des descriptions pour les éléments JSON qui sont spécifique toohello service serveur de fichiers local lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="0ccf0-1911">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1911">Property</span></span> | <span data-ttu-id="0ccf0-1912">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1912">Description</span></span> | <span data-ttu-id="0ccf0-1913">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1914">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1914">type</span></span> |<span data-ttu-id="0ccf0-1915">Assurez-vous que les propriétés de type hello sont définie trop**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="0ccf0-1916">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1916">Yes</span></span> |
| <span data-ttu-id="0ccf0-1917">host</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1917">host</span></span> |<span data-ttu-id="0ccf0-1918">Spécifie le chemin d’accès racine de hello du dossier hello que vous souhaitez toocopy.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="0ccf0-1919">Utilisez le caractère d’échappement de hello ' \ ' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="0ccf0-1920">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="0ccf0-1921">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1921">Yes</span></span> |
| <span data-ttu-id="0ccf0-1922">userId</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1922">userid</span></span> |<span data-ttu-id="0ccf0-1923">Spécifiez des ID de hello de serveur d’accès toohello utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="0ccf0-1924">Non (si vous choisissez encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="0ccf0-1925">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1925">password</span></span> |<span data-ttu-id="0ccf0-1926">Spécifiez le mot de passe hello pour hello (userid).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="0ccf0-1927">Non (si vous choisissez encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="0ccf0-1928">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1928">encryptedCredential</span></span> |<span data-ttu-id="0ccf0-1929">Spécifiez les informations d’identification de hello chiffré que vous pouvez obtenir en exécutant l’applet de commande New-AzureRmDataFactoryEncryptValue de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="0ccf0-1930">Non (si vous choisissez toospecify nom d’utilisateur et mot de passe en texte brut)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="0ccf0-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1931">gatewayName</span></span> |<span data-ttu-id="0ccf0-1932">Spécifie le nom hello de passerelle hello que Data Factory doit utiliser de serveur de fichiers local tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="0ccf0-1933">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="0ccf0-1934">Exemples de définitions de chemin d’accès du dossier</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="0ccf0-1935">Scénario</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1935">Scenario</span></span> | <span data-ttu-id="0ccf0-1936">Hôte dans la définition du service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1936">Host in linked service definition</span></span> | <span data-ttu-id="0ccf0-1937">folderPath dans la définition du jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1938">Dossier local sur l’ordinateur passerelle de gestion des données : </span><span class="sxs-lookup"><span data-stu-id="0ccf0-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="0ccf0-1939">Exemples : D:\\\* ou D:\dossier\sous-dossier\\*</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="0ccf0-1940">D:\\\\ (pour la passerelle de gestion des données 2.0 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="0ccf0-1941">hôte local (pour les versions de la passerelle de gestion des données antérieures à 2.0)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="0ccf0-1942">.\\\\ ou dossier\\\\sous-dossier (pour la passerelle de gestion des données 2.0 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="0ccf0-1943">D:\\\\ ou D:\\\\dossier\\\\sous-dossier (pour les versions de la passerelle antérieures à 2.0)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="0ccf0-1944">Dossier partagé distant : </span><span class="sxs-lookup"><span data-stu-id="0ccf0-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="0ccf0-1945">Exemples : \\\\myserver\\share\\\* ou \\\\myserver\\share\\dossier\\sous-dossier\\*</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="0ccf0-1946">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="0ccf0-1947">.\\\\ ou dossier\\\\sous-dossier</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="0ccf0-1948">Exemple : utilisation d’un nom d'utilisateur et d’un mot de passe en texte brut</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="0ccf0-1949">Exemple : utilisation de l’élément encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="0ccf0-1950">Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-1951">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1951">Dataset</span></span>
<span data-ttu-id="0ccf0-1952">toodefine un jeu de données du système de fichiers, jeu hello **type** du jeu de données hello trop**le partage de fichiers**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-1953">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1953">Property</span></span> | <span data-ttu-id="0ccf0-1954">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1954">Description</span></span> | <span data-ttu-id="0ccf0-1955">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1956">folderPath</span></span> |<span data-ttu-id="0ccf0-1957">Spécifie le dossier de toohello sous-chemin hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="0ccf0-1958">Utilisez le caractère d’échappement de hello ' \' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="0ccf0-1959">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="0ccf0-1960">Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="0ccf0-1961">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1961">Yes</span></span> |
| <span data-ttu-id="0ccf0-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1962">fileName</span></span> |<span data-ttu-id="0ccf0-1963">Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="0ccf0-1964">Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="0ccf0-1965">Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré est hello suivant le format suivant :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="0ccf0-1966">`Data.<Guid>.txt` (Exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="0ccf0-1967">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1967">No</span></span> |
| <span data-ttu-id="0ccf0-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1968">fileFilter</span></span> |<span data-ttu-id="0ccf0-1969">Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="0ccf0-1970">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="0ccf0-1971">Exemple 1 : « fileFilter » : « *.log »</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="0ccf0-1972">Exemple 2 : « fileFilter » : « 2016-1-?.txt »</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="0ccf0-1973">Remarque : fileFilter s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="0ccf0-1974">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1974">No</span></span> |
| <span data-ttu-id="0ccf0-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1975">partitionedBy</span></span> |<span data-ttu-id="0ccf0-1976">Vous pouvez utiliser partitionedBy toospecify folderPath/nom de fichier dynamique pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="0ccf0-1977">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="0ccf0-1978">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1978">No</span></span> |
| <span data-ttu-id="0ccf0-1979">format</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1979">format</span></span> | <span data-ttu-id="0ccf0-1980">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0ccf0-1981">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="0ccf0-1982">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0ccf0-1983">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0ccf0-1984">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1984">No</span></span> |
| <span data-ttu-id="0ccf0-1985">compression</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1985">compression</span></span> | <span data-ttu-id="0ccf0-1986">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="0ccf0-1987">Types pris en charge : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Niveaux pris en charge : **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0ccf0-1988">consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0ccf0-1989">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="0ccf0-1990">Vous ne pouvez pas utiliser fileName et fileFilter simultanément.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="0ccf0-1991">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1991">Example</span></span>

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

<span data-ttu-id="0ccf0-1992">Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="0ccf0-1993">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-1994">Si vous copiez des données à partir du système de fichiers, la valeur hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-1995">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1995">Property</span></span> | <span data-ttu-id="0ccf0-1996">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1996">Description</span></span> | <span data-ttu-id="0ccf0-1997">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1997">Allowed values</span></span> | <span data-ttu-id="0ccf0-1998">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-1999">recursive</span><span class="sxs-lookup"><span data-stu-id="0ccf0-1999">recursive</span></span> |<span data-ttu-id="0ccf0-2000">Indique si les données de salutation sont lu de manière récursive des sous-dossiers de hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="0ccf0-2001">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2001">True, False (default)</span></span> |<span data-ttu-id="0ccf0-2002">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2003">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2003">Example</span></span>

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
<span data-ttu-id="0ccf0-2004">Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="0ccf0-2005">Récepteur Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="0ccf0-2006">Si vous copiez des données tooFile système, la valeur hello **type de récepteur** Hello activité de copie trop**FileSystemSink**et spécifiez les propriétés Bonjour suivantes **récepteur** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="0ccf0-2007">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2007">Property</span></span> | <span data-ttu-id="0ccf0-2008">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2008">Description</span></span> | <span data-ttu-id="0ccf0-2009">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2009">Allowed values</span></span> | <span data-ttu-id="0ccf0-2010">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2011">copyBehavior</span></span> |<span data-ttu-id="0ccf0-2012">Définit le comportement de copie de hello lors de la source de hello est BlobSource ou système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="0ccf0-2013">**PreserveHierarchy :** conserve la hiérarchie des fichiers dans le dossier cible de hello hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="0ccf0-2014">Autrement dit, chemin d’accès relatif de hello du dossier source de hello source fichier toohello est hello identique au chemin d’accès relatif de hello du dossier cible de hello cible fichier toohello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="0ccf0-2015">**FlattenHierarchy :** tous les fichiers à partir du dossier source hello sont créés dans hello premier niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="0ccf0-2016">les fichiers cibles Hello sont créés avec un nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="0ccf0-2017">**MergeFiles :** fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="0ccf0-2018">Si le nom de blob/nom de fichier hello est spécifié, nom de fichier fusionné hello désigne hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="0ccf0-2019">Dans le cas contraire, il s’agit d’un nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="0ccf0-2020">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2020">No</span></span> |
<span data-ttu-id="0ccf0-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="0ccf0-2022">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2022">Example</span></span>

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

<span data-ttu-id="0ccf0-2023">Pour plus d’informations, consultez l’article [File System connector (connecteur Système de fichiers)](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="0ccf0-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2025">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2025">Linked service</span></span>
<span data-ttu-id="0ccf0-2026">toodefine FTP le service ensemble hello lié **type** Hello service lié trop**détails**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2027">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2027">Property</span></span> | <span data-ttu-id="0ccf0-2028">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2028">Description</span></span> | <span data-ttu-id="0ccf0-2029">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2029">Required</span></span> | <span data-ttu-id="0ccf0-2030">Default</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2031">host</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2031">host</span></span> |<span data-ttu-id="0ccf0-2032">Nom ou adresse IP du serveur FTP de hello</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="0ccf0-2033">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="0ccf0-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2034">authenticationType</span></span> |<span data-ttu-id="0ccf0-2035">Spécification du type d’authentification</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2035">Specify authentication type</span></span> |<span data-ttu-id="0ccf0-2036">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2036">Yes</span></span> |<span data-ttu-id="0ccf0-2037">Basic, anonyme</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="0ccf0-2038">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2038">username</span></span> |<span data-ttu-id="0ccf0-2039">Utilisateur qui possède le serveur d’accès toohello FTP</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="0ccf0-2040">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="0ccf0-2041">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2041">password</span></span> |<span data-ttu-id="0ccf0-2042">Mot de passe utilisateur de hello (nom d’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2042">Password for hello user (username)</span></span> |<span data-ttu-id="0ccf0-2043">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="0ccf0-2044">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2044">encryptedCredential</span></span> |<span data-ttu-id="0ccf0-2045">Serveur FTP de d’informations d’identification chiffrées tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="0ccf0-2046">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="0ccf0-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2047">gatewayName</span></span> |<span data-ttu-id="0ccf0-2048">Nom de hello passerelle de gestion des données passerelle tooconnect tooan FTP serveur local</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="0ccf0-2049">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="0ccf0-2050">port</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2050">port</span></span> |<span data-ttu-id="0ccf0-2051">Port d’écoute sur le hello FTP serveur</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="0ccf0-2052">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2052">No</span></span> |<span data-ttu-id="0ccf0-2053">21</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2053">21</span></span> |
| <span data-ttu-id="0ccf0-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2054">enableSsl</span></span> |<span data-ttu-id="0ccf0-2055">Spécifiez si les toouse FTP sur le canal SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="0ccf0-2056">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2056">No</span></span> |<span data-ttu-id="0ccf0-2057">true</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2057">true</span></span> |
| <span data-ttu-id="0ccf0-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="0ccf0-2059">Spécifiez si le serveur tooenable SSL la validation des certificats lorsque vous utilisez FTP sur un canal SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="0ccf0-2060">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2060">No</span></span> |<span data-ttu-id="0ccf0-2061">true</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="0ccf0-2062">Exemple : utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="0ccf0-2063">Exemple : utilisation d’un nom d’utilisateur et d’un mot de passe en texte brut pour l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="0ccf0-2064">Exemple : utilisation de port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="0ccf0-2065">Exemple : utilisation d’encryptedCredential pour l’authentification et la passerelle</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="0ccf0-2066">Pour plus d’informations, consultez l’article [FTP connector (connecteur FTP)](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-2067">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2067">Dataset</span></span>
<span data-ttu-id="0ccf0-2068">dataset toodefine FTP, jeu hello **type** du jeu de données hello trop**le partage de fichiers**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-2069">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2069">Property</span></span> | <span data-ttu-id="0ccf0-2070">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2070">Description</span></span> | <span data-ttu-id="0ccf0-2071">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2072">folderPath</span></span> |<span data-ttu-id="0ccf0-2073">Sous-dossier des toohello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2073">Sub path toohello folder.</span></span> <span data-ttu-id="0ccf0-2074">Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="0ccf0-2075">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="0ccf0-2076">Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="0ccf0-2077">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2077">Yes</span></span> 
| <span data-ttu-id="0ccf0-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2078">fileName</span></span> |<span data-ttu-id="0ccf0-2079">Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="0ccf0-2080">Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="0ccf0-2081">Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="0ccf0-2082">Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="0ccf0-2083">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2083">No</span></span> |
| <span data-ttu-id="0ccf0-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2084">fileFilter</span></span> |<span data-ttu-id="0ccf0-2085">Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="0ccf0-2086">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="0ccf0-2087">Exemple 1 : `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="0ccf0-2088">Exemple 2 : `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="0ccf0-2089">fileFilter s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="0ccf0-2090">Cette propriété n’est pas prise en charge avec HDFS.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="0ccf0-2091">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2091">No</span></span> |
| <span data-ttu-id="0ccf0-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2092">partitionedBy</span></span> |<span data-ttu-id="0ccf0-2093">partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="0ccf0-2094">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="0ccf0-2095">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2095">No</span></span> |
| <span data-ttu-id="0ccf0-2096">format</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2096">format</span></span> | <span data-ttu-id="0ccf0-2097">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0ccf0-2098">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="0ccf0-2099">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0ccf0-2100">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0ccf0-2101">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2101">No</span></span> |
| <span data-ttu-id="0ccf0-2102">compression</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2102">compression</span></span> | <span data-ttu-id="0ccf0-2103">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="0ccf0-2104">Types pris en charge : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Niveaux pris en charge : **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0ccf0-2105">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0ccf0-2106">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2106">No</span></span> |
| <span data-ttu-id="0ccf0-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2107">useBinaryTransfer</span></span> |<span data-ttu-id="0ccf0-2108">Spécifiez si vous voulez utiliser le mode de transfert binaire.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="0ccf0-2109">True pour le mode binaire et false pour ASCII.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="0ccf0-2110">Valeur par défaut : true.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2110">Default value: True.</span></span> <span data-ttu-id="0ccf0-2111">Cette propriété peut uniquement être utilisée lorsque le type de service lié associé est : FtpServer.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="0ccf0-2112">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="0ccf0-2113">fileName et fileFilter ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="0ccf0-2114">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="0ccf0-2115">Pour plus d’informations, consultez l’article [FTP connector (connecteur FTP)](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="0ccf0-2116">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-2117">Si vous copiez des données à partir d’un serveur FTP, définissez hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-2118">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2118">Property</span></span> | <span data-ttu-id="0ccf0-2119">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2119">Description</span></span> | <span data-ttu-id="0ccf0-2120">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2120">Allowed values</span></span> | <span data-ttu-id="0ccf0-2121">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2122">recursive</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2122">recursive</span></span> |<span data-ttu-id="0ccf0-2123">Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="0ccf0-2124">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2124">True, False (default)</span></span> |<span data-ttu-id="0ccf0-2125">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2126">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2126">Example</span></span>

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

<span data-ttu-id="0ccf0-2127">Pour plus d’informations, consultez l’article [FTP connector (connecteur FTP)](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="0ccf0-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2129">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2129">Linked service</span></span>
<span data-ttu-id="0ccf0-2130">toodefine un HDFS le service ensemble hello lié **type** Hello service lié trop**Hdfs**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2131">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2131">Property</span></span> | <span data-ttu-id="0ccf0-2132">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2132">Description</span></span> | <span data-ttu-id="0ccf0-2133">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2134">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2134">type</span></span> |<span data-ttu-id="0ccf0-2135">propriété de type Hello doit indiquer : **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="0ccf0-2136">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2136">Yes</span></span> |
| <span data-ttu-id="0ccf0-2137">Url</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2137">Url</span></span> |<span data-ttu-id="0ccf0-2138">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2138">URL toohello HDFS</span></span> |<span data-ttu-id="0ccf0-2139">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2139">Yes</span></span> |
| <span data-ttu-id="0ccf0-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2140">authenticationType</span></span> |<span data-ttu-id="0ccf0-2141">Anonyme ou Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="0ccf0-2142">toouse **l’authentification Kerberos** pour le connecteur HDFS, consultez trop[cette section](#use-kerberos-authentication-for-hdfs-connector) tooset votre environnement local en conséquence.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="0ccf0-2143">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2143">Yes</span></span> |
| <span data-ttu-id="0ccf0-2144">userName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2144">userName</span></span> |<span data-ttu-id="0ccf0-2145">Nom d’utilisateur de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="0ccf0-2146">Oui (pour l’authentification Windows)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="0ccf0-2147">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2147">password</span></span> |<span data-ttu-id="0ccf0-2148">Mot de passe de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="0ccf0-2149">Oui (pour l’authentification Windows)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="0ccf0-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2150">gatewayName</span></span> |<span data-ttu-id="0ccf0-2151">Nom de passerelle hello hello service Data Factory doit utiliser tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="0ccf0-2152">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2152">Yes</span></span> |
| <span data-ttu-id="0ccf0-2153">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2153">encryptedCredential</span></span> |<span data-ttu-id="0ccf0-2154">[Nouveau-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) sortie des informations d’identification de l’accès hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="0ccf0-2155">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="0ccf0-2156">Exemple : utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="0ccf0-2157">Exemple : utilisation de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="0ccf0-2158">Pour plus d’informations, consultez l’article [HDFS connector (connecteur HDFS)](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-2159">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2159">Dataset</span></span>
<span data-ttu-id="0ccf0-2160">toodefine un jeu de données HDFS, jeu hello **type** du jeu de données hello trop**le partage de fichiers**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-2161">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2161">Property</span></span> | <span data-ttu-id="0ccf0-2162">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2162">Description</span></span> | <span data-ttu-id="0ccf0-2163">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2164">folderPath</span></span> |<span data-ttu-id="0ccf0-2165">Dossier toohello de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2165">Path toohello folder.</span></span> <span data-ttu-id="0ccf0-2166">Exemple : `myfolder`</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="0ccf0-2167">Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="0ccf0-2168">Par exemple : pour dossier\sous-dossier, spécifiez dossier\\\\sous-dossier et pour d:\dossier d’exemple, spécifiez d:\\\\dossier d’exemple.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="0ccf0-2169">Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="0ccf0-2170">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2170">Yes</span></span> |
| <span data-ttu-id="0ccf0-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2171">fileName</span></span> |<span data-ttu-id="0ccf0-2172">Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="0ccf0-2173">Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="0ccf0-2174">Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="0ccf0-2175">Data<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="0ccf0-2176">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2176">No</span></span> |
| <span data-ttu-id="0ccf0-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2177">partitionedBy</span></span> |<span data-ttu-id="0ccf0-2178">partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="0ccf0-2179">Exemple : folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="0ccf0-2180">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2180">No</span></span> |
| <span data-ttu-id="0ccf0-2181">format</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2181">format</span></span> | <span data-ttu-id="0ccf0-2182">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0ccf0-2183">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="0ccf0-2184">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0ccf0-2185">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0ccf0-2186">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2186">No</span></span> |
| <span data-ttu-id="0ccf0-2187">compression</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2187">compression</span></span> | <span data-ttu-id="0ccf0-2188">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="0ccf0-2189">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="0ccf0-2190">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0ccf0-2191">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0ccf0-2192">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="0ccf0-2193">fileName et fileFilter ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="0ccf0-2194">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2194">Example</span></span>

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

<span data-ttu-id="0ccf0-2195">Pour plus d’informations, consultez l’article [HDFS connector (connecteur HDFS)](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="0ccf0-2196">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-2197">Si vous copiez des données à partir de HDFS, la valeur hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="0ccf0-2198">**FileSystemSource** prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="0ccf0-2199">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2199">Property</span></span> | <span data-ttu-id="0ccf0-2200">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2200">Description</span></span> | <span data-ttu-id="0ccf0-2201">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2201">Allowed values</span></span> | <span data-ttu-id="0ccf0-2202">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2203">recursive</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2203">recursive</span></span> |<span data-ttu-id="0ccf0-2204">Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="0ccf0-2205">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2205">True, False (default)</span></span> |<span data-ttu-id="0ccf0-2206">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2207">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2207">Example</span></span>

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

<span data-ttu-id="0ccf0-2208">Pour plus d’informations, consultez l’article [HDFS connector (connecteur HDFS)](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="0ccf0-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="0ccf0-2210">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2210">Linked service</span></span>
<span data-ttu-id="0ccf0-2211">toodefine un SFTP le service ensemble hello lié **type** Hello service lié trop**Sftp**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2212">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2212">Property</span></span> | <span data-ttu-id="0ccf0-2213">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2213">Description</span></span> | <span data-ttu-id="0ccf0-2214">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2215">host</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2215">host</span></span> | <span data-ttu-id="0ccf0-2216">Nom ou adresse IP du serveur SFTP de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="0ccf0-2217">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2217">Yes</span></span> |
| <span data-ttu-id="0ccf0-2218">port</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2218">port</span></span> |<span data-ttu-id="0ccf0-2219">Port d’écoute sur le hello SFTP serveur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="0ccf0-2220">la valeur par défaut Hello est : 21</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2220">hello default value is: 21</span></span> |<span data-ttu-id="0ccf0-2221">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2221">No</span></span> |
| <span data-ttu-id="0ccf0-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2222">authenticationType</span></span> |<span data-ttu-id="0ccf0-2223">Spécification du type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2223">Specify authentication type.</span></span> <span data-ttu-id="0ccf0-2224">Valeurs autorisées : **De base** et **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="0ccf0-2225">Consultez trop[l’authentification de base à l’aide](#using-basic-authentication) et [à l’aide de SSH authentification par clé publique](#using-ssh-public-key-authentication) sections respectivement sur plus de propriétés et des exemples JSON.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="0ccf0-2226">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2226">Yes</span></span> |
| <span data-ttu-id="0ccf0-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="0ccf0-2228">Spécifiez si tooskip validation de clé de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="0ccf0-2229">Non.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2229">No.</span></span> <span data-ttu-id="0ccf0-2230">Hello la valeur par défaut : false</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2230">hello default value: false</span></span> |
| <span data-ttu-id="0ccf0-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="0ccf0-2232">Spécifier les empreintes hello de clé d’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="0ccf0-2233">Oui si hello `skipHostKeyValidation` a la valeur toofalse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="0ccf0-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2234">gatewayName</span></span> |<span data-ttu-id="0ccf0-2235">Nom de hello passerelle de gestion des données tooconnect tooan local serveur SFTP.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="0ccf0-2236">Oui en cas de copie de données à partir d’un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="0ccf0-2237">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2237">encryptedCredential</span></span> | <span data-ttu-id="0ccf0-2238">Les informations d’identification chiffrées tooaccess hello SFTP le serveur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="0ccf0-2239">Généré automatiquement lorsque vous spécifiez l’authentification de base (nom d’utilisateur + mot de passe) ou paramètres SshPublicKey (nom d’utilisateur + chemin d’accès de la clé privée ou contenu) dans la copie Assistant ou hello ClickOnce boîte de dialogue contextuelle.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="0ccf0-2240">Non.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2240">No.</span></span> <span data-ttu-id="0ccf0-2241">S’applique uniquement pour la copie de données à partir d’un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="0ccf0-2242">Exemple : utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="0ccf0-2243">l’authentification de base toouse, définissez `authenticationType` comme `Basic`et spécifiez les propriétés suivantes en plus de hello connecteur SFTP génériques introduits dans la dernière section de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="0ccf0-2244">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2244">Property</span></span> | <span data-ttu-id="0ccf0-2245">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2245">Description</span></span> | <span data-ttu-id="0ccf0-2246">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2247">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2247">username</span></span> | <span data-ttu-id="0ccf0-2248">Utilisateur a accès toohello SFTP serveur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="0ccf0-2249">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2249">Yes</span></span> |
| <span data-ttu-id="0ccf0-2250">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2250">password</span></span> | <span data-ttu-id="0ccf0-2251">Mot de passe pour l’utilisateur hello (nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2251">Password for hello user (username).</span></span> | <span data-ttu-id="0ccf0-2252">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="0ccf0-2253">Exemple : authentification de base avec des informations d’identification chiffrées**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2253">Example: Basic authentication with encrypted credential**</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="0ccf0-2254">Utilisation de l’authentification par clé publique SSH : **</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="0ccf0-2255">l’authentification de base toouse, définissez `authenticationType` comme `SshPublicKey`et spécifiez les propriétés suivantes en plus de hello connecteur SFTP génériques introduits dans la dernière section de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="0ccf0-2256">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2256">Property</span></span> | <span data-ttu-id="0ccf0-2257">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2257">Description</span></span> | <span data-ttu-id="0ccf0-2258">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2259">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2259">username</span></span> |<span data-ttu-id="0ccf0-2260">Utilisateur qui a accès toohello SFTP serveur</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="0ccf0-2261">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2261">Yes</span></span> |
| <span data-ttu-id="0ccf0-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2262">privateKeyPath</span></span> | <span data-ttu-id="0ccf0-2263">Spécifiez le chemin d’accès absolu toohello cette passerelle peut accéder à fichier de clé privée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="0ccf0-2264">Spécifiez soit hello `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="0ccf0-2265">S’applique uniquement pour la copie de données à partir d’un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="0ccf0-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2266">privateKeyContent</span></span> | <span data-ttu-id="0ccf0-2267">Une chaîne sérialisée de contenu de clé privée hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="0ccf0-2268">Hello Assistant copie peut lire le fichier de clé privée hello et extraire le contenu de clé privée hello automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="0ccf0-2269">Si vous utilisez n’importe quel autre outil/Kit de développement logiciel, utilisez à la place des propriétés de privateKeyPath hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="0ccf0-2270">Spécifiez soit hello `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="0ccf0-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2271">passPhrase</span></span> | <span data-ttu-id="0ccf0-2272">Spécifiez hello expression/mot de passe toodecrypt hello privée clé si le fichier de clé hello est protégé par un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="0ccf0-2273">Oui si le fichier de clé privée hello est protégé par un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="0ccf0-2274">Exemple : authentification SshPublicKey à l’aide du contenu de clé privée**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2274">Example: SshPublicKey authentication using private key content**</span></span>

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
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="0ccf0-2275">Pour plus d’informations, consultez l’article [SFTP connector (connecteur SFTP)](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-2276">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2276">Dataset</span></span>
<span data-ttu-id="0ccf0-2277">toodefine un dataset SFTP, jeu hello **type** du jeu de données hello trop**le partage de fichiers**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-2278">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2278">Property</span></span> | <span data-ttu-id="0ccf0-2279">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2279">Description</span></span> | <span data-ttu-id="0ccf0-2280">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2281">folderPath</span></span> |<span data-ttu-id="0ccf0-2282">Sous-dossier des toohello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2282">Sub path toohello folder.</span></span> <span data-ttu-id="0ccf0-2283">Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="0ccf0-2284">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="0ccf0-2285">Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="0ccf0-2286">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2286">Yes</span></span> |
| <span data-ttu-id="0ccf0-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2287">fileName</span></span> |<span data-ttu-id="0ccf0-2288">Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="0ccf0-2289">Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="0ccf0-2290">Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="0ccf0-2291">Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="0ccf0-2292">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2292">No</span></span> |
| <span data-ttu-id="0ccf0-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2293">fileFilter</span></span> |<span data-ttu-id="0ccf0-2294">Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="0ccf0-2295">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="0ccf0-2296">Exemple 1 : `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="0ccf0-2297">Exemple 2 : `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="0ccf0-2298">fileFilter s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="0ccf0-2299">Cette propriété n’est pas prise en charge avec HDFS.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="0ccf0-2300">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2300">No</span></span> |
| <span data-ttu-id="0ccf0-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2301">partitionedBy</span></span> |<span data-ttu-id="0ccf0-2302">partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="0ccf0-2303">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="0ccf0-2304">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2304">No</span></span> |
| <span data-ttu-id="0ccf0-2305">format</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2305">format</span></span> | <span data-ttu-id="0ccf0-2306">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0ccf0-2307">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="0ccf0-2308">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0ccf0-2309">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0ccf0-2310">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2310">No</span></span> |
| <span data-ttu-id="0ccf0-2311">compression</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2311">compression</span></span> | <span data-ttu-id="0ccf0-2312">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="0ccf0-2313">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="0ccf0-2314">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0ccf0-2315">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0ccf0-2316">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2316">No</span></span> |
| <span data-ttu-id="0ccf0-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2317">useBinaryTransfer</span></span> |<span data-ttu-id="0ccf0-2318">Spécifiez si vous voulez utiliser le mode de transfert binaire.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="0ccf0-2319">True pour le mode binaire et false pour ASCII.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="0ccf0-2320">Valeur par défaut : true.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2320">Default value: True.</span></span> <span data-ttu-id="0ccf0-2321">Cette propriété peut uniquement être utilisée lorsque le type de service lié associé est : FtpServer.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="0ccf0-2322">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="0ccf0-2323">fileName et fileFilter ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="0ccf0-2324">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="0ccf0-2325">Pour plus d’informations, consultez l’article [SFTP connector (connecteur SFTP)](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="0ccf0-2326">Source Système de fichiers dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-2327">Si vous copiez des données à partir d’une source SFTP, la valeur hello **type de source de** Hello activité de copie trop**FileSystemSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-2328">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2328">Property</span></span> | <span data-ttu-id="0ccf0-2329">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2329">Description</span></span> | <span data-ttu-id="0ccf0-2330">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2330">Allowed values</span></span> | <span data-ttu-id="0ccf0-2331">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2332">recursive</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2332">recursive</span></span> |<span data-ttu-id="0ccf0-2333">Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="0ccf0-2334">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2334">True, False (default)</span></span> |<span data-ttu-id="0ccf0-2335">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="0ccf0-2336">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2336">Example</span></span>

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

<span data-ttu-id="0ccf0-2337">Pour plus d’informations, consultez l’article [SFTP connector (connecteur SFTP)](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="0ccf0-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2339">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2339">Linked service</span></span>
<span data-ttu-id="0ccf0-2340">le service ensemble hello lié toodefine un HTTP **type** Hello service lié trop**Http**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2341">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2341">Property</span></span> | <span data-ttu-id="0ccf0-2342">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2342">Description</span></span> | <span data-ttu-id="0ccf0-2343">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2344">url</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2344">url</span></span> | <span data-ttu-id="0ccf0-2345">Toohello de l’URL du serveur Web de base</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="0ccf0-2346">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2346">Yes</span></span> |
| <span data-ttu-id="0ccf0-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2347">authenticationType</span></span> | <span data-ttu-id="0ccf0-2348">Spécifie le type d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="0ccf0-2349">Les valeurs autorisées sont : **Anonymous** (Anonyme), **Basic** (De base), **Digest**, **Windows**, **ClientCertificate** (Certificat client).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="0ccf0-2350">Font respectivement référence toosections sous ce tableau sur plus de propriétés et des exemples JSON pour ces types d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="0ccf0-2351">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2351">Yes</span></span> |
| <span data-ttu-id="0ccf0-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="0ccf0-2353">Spécifiez si le serveur tooenable SSL la validation des certificats si la source est le serveur de Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="0ccf0-2354">Non, la valeur par défaut est True.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2354">No, default is true</span></span> |
| <span data-ttu-id="0ccf0-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2355">gatewayName</span></span> | <span data-ttu-id="0ccf0-2356">Nom de tooan de tooconnect hello passerelle de gestion des données sur site source HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="0ccf0-2357">Oui en cas de copie de données à partir d’une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="0ccf0-2358">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2358">encryptedCredential</span></span> | <span data-ttu-id="0ccf0-2359">Les informations d’identification chiffrées tooaccess hello de point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="0ccf0-2360">Généré automatiquement lorsque vous configurez des informations d’authentification hello dans copie Assistant ou hello ClickOnce boîte de dialogue contextuelle.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="0ccf0-2361">Non.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2361">No.</span></span> <span data-ttu-id="0ccf0-2362">S’applique uniquement pour la copie de données à partir d’un serveur HTTP local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="0ccf0-2363">Exemple : utilisation de l’authentification Basic (De base), Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="0ccf0-2364">Définissez `authenticationType` en tant que `Basic`, `Digest`, ou `Windows`et spécifiez hello propriétés suivantes en plus de hello du connecteur HTTP générique celles présentées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="0ccf0-2365">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2365">Property</span></span> | <span data-ttu-id="0ccf0-2366">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2366">Description</span></span> | <span data-ttu-id="0ccf0-2367">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2368">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2368">username</span></span> | <span data-ttu-id="0ccf0-2369">Nom d’utilisateur tooaccess hello de point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="0ccf0-2370">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2370">Yes</span></span> |
| <span data-ttu-id="0ccf0-2371">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2371">password</span></span> | <span data-ttu-id="0ccf0-2372">Mot de passe pour l’utilisateur hello (nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2372">Password for hello user (username).</span></span> | <span data-ttu-id="0ccf0-2373">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="0ccf0-2374">Exemple : utilisation de l’authentification ClientCertificate (Certificat client)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="0ccf0-2375">l’authentification de base toouse, définissez `authenticationType` comme `ClientCertificate`et spécifiez hello propriétés suivantes en plus de hello du connecteur HTTP générique celles présentées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="0ccf0-2376">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2376">Property</span></span> | <span data-ttu-id="0ccf0-2377">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2377">Description</span></span> | <span data-ttu-id="0ccf0-2378">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2379">embeddedCertData</span></span> | <span data-ttu-id="0ccf0-2380">contenu codé en Base64 Hello de données binaires du fichier d’informations Exchange PFX (Personal) hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="0ccf0-2381">Spécifiez soit hello `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="0ccf0-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2382">certThumbprint</span></span> | <span data-ttu-id="0ccf0-2383">Bonjour empreinte numérique du certificat hello qui a été installé sur le magasin de certificats de l’ordinateur de votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="0ccf0-2384">S’applique uniquement pour la copie de données à partir d’une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="0ccf0-2385">Spécifiez soit hello `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="0ccf0-2386">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2386">password</span></span> | <span data-ttu-id="0ccf0-2387">Mot de passe associé au certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="0ccf0-2388">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2388">No</span></span> |

<span data-ttu-id="0ccf0-2389">Si vous utilisez `certThumbprint` pour l’authentification et hello du certificat est installé dans le magasin personnel de l’ordinateur local de hello de hello, vous devez le service passerelle toohello toogrant hello autorisation de lecture :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="0ccf0-2390">Lancez Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="0ccf0-2391">Ajouter hello **certificats** que hello cibles du composant logiciel enfichable **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="0ccf0-2392">Développez **Certificats**, **Personnel**, puis cliquez sur **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="0ccf0-2393">Certificat hello magasin personnel de hello d’avec le bouton droit, puis sélectionnez **toutes les tâches**->**gérer les clés privées...**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="0ccf0-2394">Sur hello **sécurité** onglet, ajoutez le compte d’utilisateur hello sous lequel le Service hôte de passerelle de gestion des données s’exécute avec le certificat de toohello hello accès en lecture.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="0ccf0-2395">**Exemple : utilisation de certificat client :** cela les liaisons de service vos données fabrique tooan local HTTP web serveur lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="0ccf0-2396">Il utilise un certificat de client est installé sur l’ordinateur de hello avec la passerelle de gestion des données installé.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="0ccf0-2397">Exemple : utilisation d’un certificat client dans un fichier</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="0ccf0-2398">Cela les liaisons de service vos données fabrique tooan local HTTP web serveur lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="0ccf0-2399">Elle utilise un fichier de certificat client sur l’ordinateur de hello avec la passerelle de gestion des données installé.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="0ccf0-2400">Pour plus d’informations, consultez l’article [HTTP connector (connecteur HTTP)](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-2401">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2401">Dataset</span></span>
<span data-ttu-id="0ccf0-2402">toodefine un HTTP dataset, ensemble hello **type** du jeu de données hello trop**Http**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-2403">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2403">Property</span></span> | <span data-ttu-id="0ccf0-2404">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2404">Description</span></span> | <span data-ttu-id="0ccf0-2405">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2406">relativeUrl</span></span> | <span data-ttu-id="0ccf0-2407">Une ressource URL toohello relative qui contient les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="0ccf0-2408">Lorsque le chemin d’accès n’est pas spécifié, seul hello URL spécifiée dans la définition de service hello lié est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="0ccf0-2409">tooconstruct des URL dynamique, vous pouvez utiliser [les variables système et les fonctions de Data Factory](data-factory-functions-variables.md), exemple : `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="0ccf0-2410">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2410">No</span></span> |
| <span data-ttu-id="0ccf0-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2411">requestMethod</span></span> | <span data-ttu-id="0ccf0-2412">Méthode HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2412">Http method.</span></span> <span data-ttu-id="0ccf0-2413">Les valeurs autorisées sont **GET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="0ccf0-2414">Non.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2414">No.</span></span> <span data-ttu-id="0ccf0-2415">La valeur par défaut est `GET`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="0ccf0-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2416">additionalHeaders</span></span> | <span data-ttu-id="0ccf0-2417">En-têtes de requête HTTP supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="0ccf0-2418">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2418">No</span></span> |
| <span data-ttu-id="0ccf0-2419">RequestBody</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2419">requestBody</span></span> | <span data-ttu-id="0ccf0-2420">Corps de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2420">Body for HTTP request.</span></span> | <span data-ttu-id="0ccf0-2421">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2421">No</span></span> |
| <span data-ttu-id="0ccf0-2422">format</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2422">format</span></span> | <span data-ttu-id="0ccf0-2423">Si vous souhaitez toosimply **hello de données à partir du point de terminaison HTTP en tant que-est** sans qu’il analyse, ignorer les paramètres de ce format.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="0ccf0-2424">Si vous souhaitez la réponse de hello HTTP tooparse contenu pendant la copie, hello les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0ccf0-2425">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="0ccf0-2426">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2426">No</span></span> |
| <span data-ttu-id="0ccf0-2427">compression</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2427">compression</span></span> | <span data-ttu-id="0ccf0-2428">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="0ccf0-2429">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="0ccf0-2430">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0ccf0-2431">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0ccf0-2432">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="0ccf0-2433">Exemple : utilisation de méthode GET (par défaut) de hello</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2433">Example: using hello GET (default) method</span></span>

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

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="0ccf0-2434">Exemple : utilisation de méthode POST hello</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2434">Example: using hello POST method</span></span>

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
<span data-ttu-id="0ccf0-2435">Pour plus d’informations, consultez l’article [HTTP connector (connecteur HTTP)](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="0ccf0-2436">Source HTTP dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-2437">Si vous copiez des données à partir d’une source de HTTP, définissez hello **type de source de** Hello activité de copie trop**HttpSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-2438">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2438">Property</span></span> | <span data-ttu-id="0ccf0-2439">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2439">Description</span></span> | <span data-ttu-id="0ccf0-2440">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="0ccf0-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2441">httpRequestTimeout</span></span> | <span data-ttu-id="0ccf0-2442">Bonjour le délai d’attente (TimeSpan) pour tooget de demande HTTP hello une réponse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="0ccf0-2443">Il est tooget hello du délai d’attente de réponse, pas les données de réponse du tooread hello du délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="0ccf0-2444">Non.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2444">No.</span></span> <span data-ttu-id="0ccf0-2445">Valeur par défaut : 00:01:40</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="0ccf0-2446">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
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

<span data-ttu-id="0ccf0-2447">Pour plus d’informations, consultez l’article [HTTP connector (connecteur HTTP)](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="0ccf0-2448">OData</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2449">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2449">Linked service</span></span>
<span data-ttu-id="0ccf0-2450">toodefine OData liée service, jeu hello **type** Hello service lié trop**OData**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2451">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2451">Property</span></span> | <span data-ttu-id="0ccf0-2452">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2452">Description</span></span> | <span data-ttu-id="0ccf0-2453">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2454">url</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2454">url</span></span> |<span data-ttu-id="0ccf0-2455">URL de hello service OData.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2455">Url of hello OData service.</span></span> |<span data-ttu-id="0ccf0-2456">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2456">Yes</span></span> |
| <span data-ttu-id="0ccf0-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2457">authenticationType</span></span> |<span data-ttu-id="0ccf0-2458">Type d’authentification utilisé tooconnect toohello OData source.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="0ccf0-2459">Pour OData dans le cloud, les valeurs possibles sont Anonyme, De base et OAuth (notez qu’à l’heure actuelle, Azure Data Factory prend en charge uniquement l’authentification OAuth basée sur Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="0ccf0-2460">Pour OData en local, les valeurs possibles sont Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="0ccf0-2461">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2461">Yes</span></span> |
| <span data-ttu-id="0ccf0-2462">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2462">username</span></span> |<span data-ttu-id="0ccf0-2463">Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="0ccf0-2464">Oui (uniquement si vous utilisez l’authentification de base)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="0ccf0-2465">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2465">password</span></span> |<span data-ttu-id="0ccf0-2466">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0ccf0-2467">Oui (uniquement si vous utilisez l’authentification de base)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="0ccf0-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2468">authorizedCredential</span></span> |<span data-ttu-id="0ccf0-2469">Si vous utilisez OAuth, cliquez sur **Authorize** bouton de hello Assistant copie de fabrique de données ou de l’éditeur et entrez vos informations d’identification, puis de la valeur hello de cette propriété sera généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="0ccf0-2470">Oui (uniquement si vous utilisez l’authentification OAuth)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="0ccf0-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2471">gatewayName</span></span> |<span data-ttu-id="0ccf0-2472">Nom de passerelle hello hello service Data Factory doit utiliser le service OData de tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="0ccf0-2473">Indiquez uniquement si vous copiez des données à partir de la source OData locale.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="0ccf0-2474">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="0ccf0-2475">Exemple : utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="0ccf0-2476">Exemple : utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="0ccf0-2477">Exemple : utilisation de l’authentification Windows pour accéder à la source OData locale</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="0ccf0-2478">Exemple : utilisation de l’authentification OAuth pour accéder à la source OData dans le cloud</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="0ccf0-2479">Pour plus d’informations, consultez l’article [OData connector (connecteur OData)](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="0ccf0-2480">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2480">Dataset</span></span>
<span data-ttu-id="0ccf0-2481">toodefine un jeu de données OData, jeu hello **type** du jeu de données hello trop**ODataResource**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-2482">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2482">Property</span></span> | <span data-ttu-id="0ccf0-2483">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2483">Description</span></span> | <span data-ttu-id="0ccf0-2484">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2485">path</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2485">path</span></span> |<span data-ttu-id="0ccf0-2486">Chemin d’accès toohello ressource OData</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2486">Path toohello OData resource</span></span> |<span data-ttu-id="0ccf0-2487">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2488">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2488">Example</span></span>

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

<span data-ttu-id="0ccf0-2489">Pour plus d’informations, consultez l’article [OData connector (connecteur OData)](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-2490">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-2491">Si vous copiez des données à partir d’une source OData, définissez hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-2492">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2492">Property</span></span> | <span data-ttu-id="0ccf0-2493">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2493">Description</span></span> | <span data-ttu-id="0ccf0-2494">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2494">Example</span></span> | <span data-ttu-id="0ccf0-2495">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2496">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2496">query</span></span> |<span data-ttu-id="0ccf0-2497">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="0ccf0-2499">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2500">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2500">Example</span></span>

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

<span data-ttu-id="0ccf0-2501">Pour plus d’informations, consultez l’article [OData connector (connecteur OData)](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="0ccf0-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="0ccf0-2503">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2503">Linked service</span></span>
<span data-ttu-id="0ccf0-2504">le service ensemble hello lié toodefine une application ODBC **type** Hello service lié trop**OnPremisesOdbc**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2505">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2505">Property</span></span> | <span data-ttu-id="0ccf0-2506">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2506">Description</span></span> | <span data-ttu-id="0ccf0-2507">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2508">connectionString</span></span> |<span data-ttu-id="0ccf0-2509">partie des informations d’identification de l’accès non Hello de chaîne de connexion hello et éventuellement un chiffrées d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="0ccf0-2510">Consultez les exemples dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="0ccf0-2511">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2511">Yes</span></span> |
| <span data-ttu-id="0ccf0-2512">credential</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2512">credential</span></span> |<span data-ttu-id="0ccf0-2513">Hello accès informations d’identification la partie de chaîne de connexion hello spécifié au format de la valeur de propriété spécifiques au pilote.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="0ccf0-2514">Exemple : « Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>; ».</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="0ccf0-2515">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2515">No</span></span> |
| <span data-ttu-id="0ccf0-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2516">authenticationType</span></span> |<span data-ttu-id="0ccf0-2517">Type d’authentification utilisé le magasin de données ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="0ccf0-2518">Les valeurs possibles sont : Anonyme et De base.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="0ccf0-2519">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2519">Yes</span></span> |
| <span data-ttu-id="0ccf0-2520">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2520">username</span></span> |<span data-ttu-id="0ccf0-2521">Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="0ccf0-2522">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2522">No</span></span> |
| <span data-ttu-id="0ccf0-2523">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2523">password</span></span> |<span data-ttu-id="0ccf0-2524">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0ccf0-2525">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2525">No</span></span> |
| <span data-ttu-id="0ccf0-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2526">gatewayName</span></span> |<span data-ttu-id="0ccf0-2527">Nom de passerelle hello hello service Data Factory doit utiliser le magasin de données ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="0ccf0-2528">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="0ccf0-2529">Exemple : utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="0ccf0-2530">Exemple : utilisation de l’authentification de base avec des informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="0ccf0-2531">Vous pouvez chiffrer les informations d’identification hello à l’aide de hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) applet de commande (1.0 version d’Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 version ou antérieure de hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="0ccf0-2532">Exemple : utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="0ccf0-2533">Pour plus d’informations, consultez l’article [ODBC connector (connecteur ODBC)](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-2534">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2534">Dataset</span></span>
<span data-ttu-id="0ccf0-2535">toodefine un jeu de données ODBC, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-2536">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2536">Property</span></span> | <span data-ttu-id="0ccf0-2537">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2537">Description</span></span> | <span data-ttu-id="0ccf0-2538">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2539">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2539">tableName</span></span> |<span data-ttu-id="0ccf0-2540">Nom de table hello dans le magasin de données ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="0ccf0-2541">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="0ccf0-2542">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2542">Example</span></span>

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

<span data-ttu-id="0ccf0-2543">Pour plus d’informations, consultez l’article [ODBC connector (connecteur ODBC)](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-2544">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-2545">Si vous copiez des données à partir d’une banque de données ODBC, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-2546">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2546">Property</span></span> | <span data-ttu-id="0ccf0-2547">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2547">Description</span></span> | <span data-ttu-id="0ccf0-2548">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2548">Allowed values</span></span> | <span data-ttu-id="0ccf0-2549">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2550">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2550">query</span></span> |<span data-ttu-id="0ccf0-2551">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-2552">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2552">SQL query string.</span></span> <span data-ttu-id="0ccf0-2553">Par exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="0ccf0-2554">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2555">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2555">Example</span></span>

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

<span data-ttu-id="0ccf0-2556">Pour plus d’informations, consultez l’article [ODBC connector (connecteur ODBC)](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="0ccf0-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="0ccf0-2558">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2558">Linked service</span></span>
<span data-ttu-id="0ccf0-2559">le service ensemble hello lié toodefine une force de vente **type** Hello service lié trop**Salesforce**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2560">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2560">Property</span></span> | <span data-ttu-id="0ccf0-2561">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2561">Description</span></span> | <span data-ttu-id="0ccf0-2562">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2563">environmentUrl</span></span> | <span data-ttu-id="0ccf0-2564">Spécifier l’instance d’URL de la force de vente hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="0ccf0-2565">- L’URL par défaut est « https://login.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="0ccf0-2566">-toocopy des données à partir de bac à sable, spécifiez « https://test.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="0ccf0-2567">-toocopy des données à partir d’un domaine personnalisé, spécifiez, par exemple, « https://[domain].my.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="0ccf0-2568">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2568">No</span></span> |
| <span data-ttu-id="0ccf0-2569">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2569">username</span></span> |<span data-ttu-id="0ccf0-2570">Spécifiez un nom d’utilisateur pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="0ccf0-2571">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2571">Yes</span></span> |
| <span data-ttu-id="0ccf0-2572">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2572">password</span></span> |<span data-ttu-id="0ccf0-2573">Spécifiez un mot de passe pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="0ccf0-2574">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2574">Yes</span></span> |
| <span data-ttu-id="0ccf0-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2575">securityToken</span></span> |<span data-ttu-id="0ccf0-2576">Spécifier un jeton de sécurité pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="0ccf0-2577">Consultez [obtenir jeton de sécurité](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) pour obtenir des instructions sur la façon de tooreset/obtenir un jeton de sécurité.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="0ccf0-2578">toolearn sur les jetons de sécurité en général, consultez [API de sécurité et hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="0ccf0-2579">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2580">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2580">Example</span></span>

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

<span data-ttu-id="0ccf0-2581">Pour plus d’informations, consultez l’article [Salesforce connector (connecteur Salesforce)](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-2582">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2582">Dataset</span></span>
<span data-ttu-id="0ccf0-2583">toodefine un jeu de données Salesforce, jeu hello **type** du jeu de données hello trop**RelationalTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-2584">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2584">Property</span></span> | <span data-ttu-id="0ccf0-2585">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2585">Description</span></span> | <span data-ttu-id="0ccf0-2586">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2587">TableName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2587">tableName</span></span> |<span data-ttu-id="0ccf0-2588">Nom de table hello dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="0ccf0-2589">Non (si une **requête** de type **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2590">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2590">Example</span></span>

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

<span data-ttu-id="0ccf0-2591">Pour plus d’informations, consultez l’article [Salesforce connector (connecteur Salesforce)](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="0ccf0-2592">Source relationnelle dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-2593">Si vous copiez des données à partir de la force de vente, la valeur hello **type de source de** Hello activité de copie trop**RelationalSource**et spécifiez les propriétés Bonjour suivantes **source** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="0ccf0-2594">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2594">Property</span></span> | <span data-ttu-id="0ccf0-2595">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2595">Description</span></span> | <span data-ttu-id="0ccf0-2596">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2596">Allowed values</span></span> | <span data-ttu-id="0ccf0-2597">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ccf0-2598">query</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2598">query</span></span> |<span data-ttu-id="0ccf0-2599">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ccf0-2600">Une requête SQL-92 ou une requête [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="0ccf0-2601">Par exemple : `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="0ccf0-2602">Non (si hello **tableName** Hello **dataset** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2603">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="0ccf0-2604">Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="0ccf0-2605">Pour plus d’informations, consultez l’article [Salesforce connector (connecteur Salesforce)](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="0ccf0-2606">Données Web</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2607">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2607">Linked service</span></span>
<span data-ttu-id="0ccf0-2608">le service ensemble hello lié toodefine un site Web **type** Hello service lié trop**Web**et spécifiez les propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2609">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2609">Property</span></span> | <span data-ttu-id="0ccf0-2610">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2610">Description</span></span> | <span data-ttu-id="0ccf0-2611">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2612">Url</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2612">Url</span></span> |<span data-ttu-id="0ccf0-2613">Source de l’URL toohello Web</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2613">URL toohello Web source</span></span> |<span data-ttu-id="0ccf0-2614">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2614">Yes</span></span> |
| <span data-ttu-id="0ccf0-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2615">authenticationType</span></span> |<span data-ttu-id="0ccf0-2616">Anonyme</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2616">Anonymous.</span></span> |<span data-ttu-id="0ccf0-2617">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="0ccf0-2618">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2618">Example</span></span>


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

<span data-ttu-id="0ccf0-2619">Pour plus d’informations, consultez l’article [Web Table connector (connecteur table web)](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="0ccf0-2620">Jeu de données</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2620">Dataset</span></span>
<span data-ttu-id="0ccf0-2621">toodefine un jeu de données Web, jeu hello **type** du jeu de données hello trop**WebTable**et spécifiez hello propriétés Bonjour suivantes **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="0ccf0-2622">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2622">Property</span></span> | <span data-ttu-id="0ccf0-2623">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2623">Description</span></span> | <span data-ttu-id="0ccf0-2624">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-2625">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2625">type</span></span> |<span data-ttu-id="0ccf0-2626">Type de jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2626">type of hello dataset.</span></span> <span data-ttu-id="0ccf0-2627">doit être défini trop**WebTable**</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="0ccf0-2628">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2628">Yes</span></span> |
| <span data-ttu-id="0ccf0-2629">path</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2629">path</span></span> |<span data-ttu-id="0ccf0-2630">Une ressource URL toohello relative qui contient la table de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="0ccf0-2631">Non.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2631">No.</span></span> <span data-ttu-id="0ccf0-2632">Lorsque le chemin d’accès n’est pas spécifié, seul hello URL spécifiée dans la définition de service hello lié est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="0ccf0-2633">index</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2633">index</span></span> |<span data-ttu-id="0ccf0-2634">index de Hello de table hello dans la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="0ccf0-2635">Consultez [Get index d’une table dans une page HTML](#get-index-of-a-table-in-an-html-page) section pour l’index de toogetting étapes d’une table dans une page HTML.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="0ccf0-2636">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="0ccf0-2637">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2637">Example</span></span>

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

<span data-ttu-id="0ccf0-2638">Pour plus d’informations, consultez l’article [Web Table connector (connecteur table web)](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="0ccf0-2639">Source Web dans l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="0ccf0-2640">Si vous copiez des données à partir d’une table de web, définissez hello **type de source de** Hello activité de copie trop**WebSource**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="0ccf0-2641">Actuellement, lorsque source hello dans l’activité de copie est de type **WebSource**, aucune des propriétés supplémentaires ne sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="0ccf0-2642">Exemple</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
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

<span data-ttu-id="0ccf0-2643">Pour plus d’informations, consultez l’article [Web Table connector (connecteur table web)](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="0ccf0-2644">ENVIRONNEMENTS DE CALCUL</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="0ccf0-2645">Hello tableau suivant répertorie les environnements de calcul hello pris en charge par les activités de transformation de Data Factory et hello pouvant s’exécuter sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="0ccf0-2646">Cliquez sur lien hello pour le calcul de hello vous intéresser dans les schémas JSON toosee hello pour le service lié toolink de fabrique de données tooa.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="0ccf0-2647">Environnement de calcul</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2647">Compute environment</span></span> | <span data-ttu-id="0ccf0-2648">Activités</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="0ccf0-2649">[Cluster HDInsight à la demande](#on-demand-azure-hdinsight-cluster) ou [votre propre cluster HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="0ccf0-2650">[Activité personnalisée .NET](#net-custom-activity), [Activité Hive](#hdinsight-hive-activity), [Activité pig](#hdinsight-pig-activity, [Activité MapReduce](#hdinsight-mapreduce-activity), [Activité de diffusion en continu Hadoop](#hdinsight-streaming-activityd), [Activité Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="0ccf0-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="0ccf0-2652">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="0ccf0-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="0ccf0-2654">[Activité d’exécution par lot Machine Learning](#machine-learning-batch-execution-activity), [Activité des ressources de mise à jour de Machine Learning](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="0ccf0-2655">Service Analytique Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="0ccf0-2656">Langage U-SQL du service Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="0ccf0-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="0ccf0-2658">Procédure stockée</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="0ccf0-2659">Cluster Azure HDInsight à la demande</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="0ccf0-2660">Hello service Azure Data Factory peut créer automatiquement un données de tooprocess cluster basé sur Windows/Linux à la demande HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="0ccf0-2661">cluster de Hello est créé dans la même région que le compte de stockage hello (propriété linkedServiceName Bonjour JSON) associée au cluster de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="0ccf0-2662">Vous pouvez exécuter hello suivant des activités de transformation de ce service lié : [les activités personnalisées .NET](#net-custom-activity), [Hive activité](#hdinsight-hive-activity), [porc activité] (#hdinsight--activité pig, [activité MapReduce ](#hdinsight-mapreduce-activity), [Activité de diffusion en continu Hadoop](#hdinsight-streaming-activityd), [nouvelles activités](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2663">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2663">Linked service</span></span> 
<span data-ttu-id="0ccf0-2664">Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition de Azure JSON hello d’un service lié HDInsight de la demande.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="0ccf0-2665">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2665">Property</span></span> | <span data-ttu-id="0ccf0-2666">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2666">Description</span></span> | <span data-ttu-id="0ccf0-2667">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2668">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2668">type</span></span> |<span data-ttu-id="0ccf0-2669">propriété de type Hello doit être définie trop**HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="0ccf0-2670">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2670">Yes</span></span> |
| <span data-ttu-id="0ccf0-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2671">clusterSize</span></span> |<span data-ttu-id="0ccf0-2672">Nombre de nœuds de données des collaborateurs de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="0ccf0-2673">cluster HDInsight de Hello est créé avec 2 nœuds principal, ainsi que le nombre de hello de nœuds de travail que vous spécifiez pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="0ccf0-2674">les nœuds de Hello sont de taille D3 standard qui a 4 cœurs, pour un cluster de nœuds 4 worker prend 24 cœurs (4\*4 = 16 cœurs pour les nœuds de travail, ainsi que 2\*4 = 8 cœurs pour les nœuds principal).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="0ccf0-2675">Consultez [Hadoop basé sur Linux de créer des clusters dans HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) pour plus d’informations sur la couche de hello D3 standard.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="0ccf0-2676">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2676">Yes</span></span> |
| <span data-ttu-id="0ccf0-2677">timetolive</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2677">timetolive</span></span> |<span data-ttu-id="0ccf0-2678">Hello autorisé de temps d’inactivité pour le cluster de HDInsight hello à la demande.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="0ccf0-2679">Spécifie la durée pendant laquelle hello à la demande HDInsight cluster reste actif après l’achèvement d’une activité à exécuter s’il en existe aucune autre tâche active dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="0ccf0-2680">Par exemple, si une activité exécuter prend 6 minutes et la propriété timetolive est défini à too5 minutes, hello reste de cluster actif pendant 5 minutes après hello 6 minutes du traitement d’exécution de l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="0ccf0-2681">Si l’exécution à une autre activité est exécutée avec la fenêtre de 6 minutes hello, il est traité par hello même cluster.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="0ccf0-2682">Création d’un cluster de HDInsight à la demande est une opération coûteuse (Impossible de prendre un certain temps), par conséquent, utilisez ce paramètre d’une fabrique de données de performances tooimprove nécessaires en réutilisant un cluster de HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="0ccf0-2683">Si vous définissez la propriété timetolive valeur too0, cluster de hello est supprimé dès que l’activité hello exécuter dans traité.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="0ccf0-2684">Sur hello autre part, si vous définissez une valeur élevée, le cluster de hello peut rester inactif inutilement entraîne des coûts élevés.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="0ccf0-2685">Par conséquent, il est important que valeur hello approprié selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="0ccf0-2686">Plusieurs pipelines peuvent partager hello la même instance de cluster de HDInsight à la demande hello si la valeur de la propriété timetolive hello est configuré correctement</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="0ccf0-2687">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2687">Yes</span></span> |
| <span data-ttu-id="0ccf0-2688">version</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2688">version</span></span> |<span data-ttu-id="0ccf0-2689">Version du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="0ccf0-2690">Pour plus d’informations, consultez [Versions de HDInsight prises en charge dans Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="0ccf0-2691">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2691">No</span></span> |
| <span data-ttu-id="0ccf0-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2692">linkedServiceName</span></span> |<span data-ttu-id="0ccf0-2693">Toobe de service lié de stockage Azure utilisé par le cluster à la demande de hello pour le stockage et le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="0ccf0-2694">Actuellement, vous ne peut pas créer un cluster HDInsight à la demande qui utilise une Azure Data Lake Store en tant que stockage de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="0ccf0-2695">Si vous souhaitez que les données de résultat hello toostore de HDInsight de traitement dans un Azure Data Lake Store, utilisez un activité de copie toocopy hello des données de toohello de stockage d’objets Blob Azure hello Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="0ccf0-2696">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2696">Yes</span></span> |
| <span data-ttu-id="0ccf0-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="0ccf0-2698">Spécifie les comptes de stockage supplémentaires pour hello HDInsight le service lié afin que le service de fabrique de données hello de les inscrire à votre place.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="0ccf0-2699">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2699">No</span></span> |
| <span data-ttu-id="0ccf0-2700">osType</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2700">osType</span></span> |<span data-ttu-id="0ccf0-2701">Type de système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2701">Type of operating system.</span></span> <span data-ttu-id="0ccf0-2702">Les valeurs autorisées sont Windows (par défaut) et Linux.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="0ccf0-2703">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2703">No</span></span> |
| <span data-ttu-id="0ccf0-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="0ccf0-2705">nom de Hello de lié SQL Azure service point toohello HCatalog base de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="0ccf0-2706">cluster de HDInsight Hello à la demande est créée à l’aide de la base de données SQL Azure hello en tant que le magasin de métadonnées hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="0ccf0-2707">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="0ccf0-2708">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2708">JSON example</span></span>
<span data-ttu-id="0ccf0-2709">Hello suivant JSON définit un service lié HDInsight à la demande sur Linux.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="0ccf0-2710">Hello service Data Factory crée automatiquement un **basés sur Linux** cluster HDInsight lors du traitement d’une tranche de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="0ccf0-2711">Pour plus d’informations, consultez l’article [Compute linked services (services liés de calcul)](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="0ccf0-2712">Cluster Azure HDInsight existant</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="0ccf0-2713">Vous pouvez créer un tooregister de service lié HDInsight Azure à votre propre cluster HDInsight avec la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="0ccf0-2714">Vous pouvez exécuter hello suivant des activités de transformation des données de ce service lié : [les activités personnalisées .NET](#net-custom-activity), [Hive activité](#hdinsight-hive-activity), [porc activité] (#hdinsight--activité pig, [MapReduce activité](#hdinsight-mapreduce-activity), [activité de diffusion en continu Hadoop](#hdinsight-streaming-activityd), [nouvelles activités](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2715">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2715">Linked service</span></span>
<span data-ttu-id="0ccf0-2716">Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition de Azure JSON hello d’un service lié HDInsight Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="0ccf0-2717">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2717">Property</span></span> | <span data-ttu-id="0ccf0-2718">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2718">Description</span></span> | <span data-ttu-id="0ccf0-2719">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2720">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2720">type</span></span> |<span data-ttu-id="0ccf0-2721">propriété de type Hello doit être définie trop**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="0ccf0-2722">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2722">Yes</span></span> |
| <span data-ttu-id="0ccf0-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2723">clusterUri</span></span> |<span data-ttu-id="0ccf0-2724">Hello URI du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="0ccf0-2725">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2725">Yes</span></span> |
| <span data-ttu-id="0ccf0-2726">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2726">username</span></span> |<span data-ttu-id="0ccf0-2727">Spécifier le nom hello de hello utilisateur toobe utilisé cluster HDInsight existant de tooconnect tooan.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="0ccf0-2728">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2728">Yes</span></span> |
| <span data-ttu-id="0ccf0-2729">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2729">password</span></span> |<span data-ttu-id="0ccf0-2730">Spécifiez le mot de passe de compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="0ccf0-2731">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2731">Yes</span></span> |
| <span data-ttu-id="0ccf0-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2732">linkedServiceName</span></span> | <span data-ttu-id="0ccf0-2733">Nom du service lié Azure Storage qui fait référence le stockage d’objets blob Azure toohello de hello utilisé par hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="0ccf0-2734">Actuellement, vous ne pouvez pas spécifier un service lié Azure Data Lake Store pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="0ccf0-2735">Données Bonjour Azure Data Lake Store sont accessibles à partir de scripts Hive/Pig si le cluster HDInsight de hello a accès toohello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="0ccf0-2736">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2736">Yes</span></span> |

<span data-ttu-id="0ccf0-2737">Pour obtenir la liste des versions des clusters HDInsight pris en charge, consultez [Versions de HDInsight prises en charge](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="0ccf0-2738">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2738">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="0ccf0-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2739">Azure Batch</span></span>
<span data-ttu-id="0ccf0-2740">Vous pouvez créer un tooregister de service lié Azure Batch un pool de traitement par lots de machines virtuelles (VM) avec une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="0ccf0-2741">Vous pouvez exécuter des activités personnalisées .NET à l'aide d'Azure Batch ou Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="0ccf0-2742">Vous pouvez exécuter une [activité personnalisée .NET](#net-custom-activity) sur ce service lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2743">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2743">Linked service</span></span>
<span data-ttu-id="0ccf0-2744">Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition de Azure JSON hello d’un service lié Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="0ccf0-2745">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2745">Property</span></span> | <span data-ttu-id="0ccf0-2746">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2746">Description</span></span> | <span data-ttu-id="0ccf0-2747">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2748">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2748">type</span></span> |<span data-ttu-id="0ccf0-2749">propriété de type Hello doit être définie trop**AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="0ccf0-2750">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2750">Yes</span></span> |
| <span data-ttu-id="0ccf0-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2751">accountName</span></span> |<span data-ttu-id="0ccf0-2752">Nom du compte Azure Batch de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="0ccf0-2753">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2753">Yes</span></span> |
| <span data-ttu-id="0ccf0-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2754">accessKey</span></span> |<span data-ttu-id="0ccf0-2755">Clé d’accès pour hello compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="0ccf0-2756">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2756">Yes</span></span> |
| <span data-ttu-id="0ccf0-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2757">poolName</span></span> |<span data-ttu-id="0ccf0-2758">Nom du pool hello d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="0ccf0-2759">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2759">Yes</span></span> |
| <span data-ttu-id="0ccf0-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2760">linkedServiceName</span></span> |<span data-ttu-id="0ccf0-2761">Nom de hello service lié Azure Storage associé à ce service lié Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="0ccf0-2762">Ce service lié est utilisé pour organiser des fichiers requis d’activité de hello toorun et le stockage des journaux de l’exécution d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="0ccf0-2763">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="0ccf0-2764">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2764">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="0ccf0-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2765">Azure Machine Learning</span></span>
<span data-ttu-id="0ccf0-2766">Vous créez un tooregister de service lié Azure Machine Learning un lot d’apprentissage calcul du score du point de terminaison avec une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="0ccf0-2767">Deux activités de transformation des données pouvant être exécutées sur ce service lié : [Activité d’exécution par lot Machine Learning](#machine-learning-batch-execution-activity), [Activité des ressources de mise à jour de Machine Learning](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2768">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2768">Linked service</span></span>
<span data-ttu-id="0ccf0-2769">Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition de Azure JSON hello d’un service lié Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="0ccf0-2770">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2770">Property</span></span> | <span data-ttu-id="0ccf0-2771">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2771">Description</span></span> | <span data-ttu-id="0ccf0-2772">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2773">Type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2773">Type</span></span> |<span data-ttu-id="0ccf0-2774">propriété de type Hello doit indiquer : **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="0ccf0-2775">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2775">Yes</span></span> |
| <span data-ttu-id="0ccf0-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2776">mlEndpoint</span></span> |<span data-ttu-id="0ccf0-2777">lot Hello URL de calcul de score.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="0ccf0-2778">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2778">Yes</span></span> |
| <span data-ttu-id="0ccf0-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2779">apiKey</span></span> |<span data-ttu-id="0ccf0-2780">Hello publiée API du modèle d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="0ccf0-2781">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="0ccf0-2782">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2782">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="0ccf0-2783">Service Analytique Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="0ccf0-2784">Vous créez un **Analytique de LAC de données Azure** lié service toolink une fabrique de données Azure Analytique de LAC de données Azure compute service tooan avant d’utiliser hello [activité données Lake Analytique U-SQL](data-factory-usql-activity.md) dans un pipeline .</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2785">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2785">Linked service</span></span>

<span data-ttu-id="0ccf0-2786">Hello tableau suivant fournit des descriptions pour les propriétés de hello utilisées dans la définition JSON de hello d’un service Azure données Lake Analytique est lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="0ccf0-2787">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2787">Property</span></span> | <span data-ttu-id="0ccf0-2788">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2788">Description</span></span> | <span data-ttu-id="0ccf0-2789">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2790">Type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2790">Type</span></span> |<span data-ttu-id="0ccf0-2791">propriété de type Hello doit indiquer : **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="0ccf0-2792">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2792">Yes</span></span> |
| <span data-ttu-id="0ccf0-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2793">accountName</span></span> |<span data-ttu-id="0ccf0-2794">Nom du compte du service Analytique Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="0ccf0-2795">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2795">Yes</span></span> |
| <span data-ttu-id="0ccf0-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="0ccf0-2797">URI du service Analytique Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="0ccf0-2798">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2798">No</span></span> |
| <span data-ttu-id="0ccf0-2799">autorisation</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2799">authorization</span></span> |<span data-ttu-id="0ccf0-2800">Code d’autorisation est automatiquement récupérée après avoir cliqué sur **Authorize** bouton hello éditeur Data Factory et de fin de connexion OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="0ccf0-2801">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2801">Yes</span></span> |
| <span data-ttu-id="0ccf0-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2802">subscriptionId</span></span> |<span data-ttu-id="0ccf0-2803">ID d’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2803">Azure subscription id</span></span> |<span data-ttu-id="0ccf0-2804">Non (si non spécifié, abonnement Hello fabrique de données est utilisée).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="0ccf0-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2805">resourceGroupName</span></span> |<span data-ttu-id="0ccf0-2806">Nom du groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2806">Azure resource group name</span></span> |<span data-ttu-id="0ccf0-2807">Non (si non spécifié, groupe de ressources de hello fabrique de données est utilisée).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="0ccf0-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2808">sessionId</span></span> |<span data-ttu-id="0ccf0-2809">id de session à partir de la session de d’autorisation OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="0ccf0-2810">Chaque ID de session est unique et ne peut être utilisé qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="0ccf0-2811">Lorsque vous utilisez hello éditeur Data Factory, cet ID est généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="0ccf0-2812">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="0ccf0-2813">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2813">JSON example</span></span>
<span data-ttu-id="0ccf0-2814">Hello l’exemple suivant fournit la définition JSON pour un service Azure données Lake Analytique est lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="0ccf0-2815">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2815">Azure SQL Database</span></span>
<span data-ttu-id="0ccf0-2816">Vous créez un service lié SQL Azure et l’utiliser avec hello [activité de procédure stockée](#stored-procedure-activity) tooinvoke une procédure stockée à partir d’un pipeline de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2817">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2817">Linked service</span></span>
<span data-ttu-id="0ccf0-2818">le service ensemble hello lié toodefine une base de données SQL Azure **type** Hello service lié trop**AzureSqlDatabase**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2819">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2819">Property</span></span> | <span data-ttu-id="0ccf0-2820">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2820">Description</span></span> | <span data-ttu-id="0ccf0-2821">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2822">connectionString</span></span> |<span data-ttu-id="0ccf0-2823">Spécifiez les informations nécessaires d’instance de base de données SQL Azure tooconnect toohello pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="0ccf0-2824">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="0ccf0-2825">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2825">JSON example</span></span>

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

<span data-ttu-id="0ccf0-2826">Pour plus d’informations sur ce service lié, consultez la page [Connecteur SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="0ccf0-2827">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="0ccf0-2828">Vous créez un service Azure SQL Data Warehouse lié et l’utiliser avec hello [activité de procédure stockée](data-factory-stored-proc-activity.md) tooinvoke une procédure stockée à partir d’un pipeline de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2829">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2829">Linked service</span></span>
<span data-ttu-id="0ccf0-2830">le service ensemble hello lié toodefine un entrepôt de données SQL Azure **type** Hello service lié trop**AzureSqlDW**et spécifiez les propriétés Bonjour suivantes **typeProperties**section :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="0ccf0-2831">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2831">Property</span></span> | <span data-ttu-id="0ccf0-2832">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2832">Description</span></span> | <span data-ttu-id="0ccf0-2833">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2834">connectionString</span></span> |<span data-ttu-id="0ccf0-2835">Spécifiez les informations nécessaires d’instance d’Azure SQL Data Warehouse tooconnect toohello pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="0ccf0-2836">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="0ccf0-2837">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2837">JSON example</span></span>

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

<span data-ttu-id="0ccf0-2838">Pour plus d’informations, consultez l’article [Azure SQL Data Warehouse connector (connecteur Azure SQL Data Warehouse)](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="0ccf0-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2839">SQL Server</span></span> 
<span data-ttu-id="0ccf0-2840">Vous créez un service lié SQL Server et l’utiliser avec hello [activité de procédure stockée](data-factory-stored-proc-activity.md) tooinvoke une procédure stockée à partir d’un pipeline de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="0ccf0-2841">Service lié</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2841">Linked service</span></span>
<span data-ttu-id="0ccf0-2842">Vous créez un service lié de type **OnPremisesSqlServer** toolink une fabrique de données de tooa de base de données locale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="0ccf0-2843">Hello tableau suivant fournit la description du service de SQL Server lié JSON éléments tooon local spécifique.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="0ccf0-2844">Hello tableau suivant fournit la description pour JSON éléments tooSQL spécifique service du serveur lié.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="0ccf0-2845">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2845">Property</span></span> | <span data-ttu-id="0ccf0-2846">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2846">Description</span></span> | <span data-ttu-id="0ccf0-2847">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2848">type</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2848">type</span></span> |<span data-ttu-id="0ccf0-2849">propriété de type Hello doit indiquer : **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="0ccf0-2850">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2850">Yes</span></span> |
| <span data-ttu-id="0ccf0-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2851">connectionString</span></span> |<span data-ttu-id="0ccf0-2852">Spécifiez les informations connectionString nécessaires de base de données SQL Server tooconnect toohello local à l’aide de l’authentification Windows ou authentification SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="0ccf0-2853">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2853">Yes</span></span> |
| <span data-ttu-id="0ccf0-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2854">gatewayName</span></span> |<span data-ttu-id="0ccf0-2855">Nom de passerelle hello hello service Data Factory doit utiliser la base de données SQL Server tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="0ccf0-2856">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2856">Yes</span></span> |
| <span data-ttu-id="0ccf0-2857">username</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2857">username</span></span> |<span data-ttu-id="0ccf0-2858">Spécifiez le nom d’utilisateur si vous utilisez l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="0ccf0-2859">Exemple : **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="0ccf0-2860">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2860">No</span></span> |
| <span data-ttu-id="0ccf0-2861">password</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2861">password</span></span> |<span data-ttu-id="0ccf0-2862">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0ccf0-2863">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2863">No</span></span> |

<span data-ttu-id="0ccf0-2864">Vous pouvez chiffrer les informations d’identification à l’aide de hello **New-AzureRmDataFactoryEncryptValue** applet de commande et les utiliser dans la chaîne de connexion hello comme indiqué dans hello exemple suivant (**EncryptedCredential** propriété) :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="0ccf0-2865">Exemple : JSON pour utilisation de l’authentification SQL</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2865">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="0ccf0-2866">Exemple : JSON pour utilisation de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="0ccf0-2867">Si le nom d’utilisateur et mot de passe sont spécifiés, la passerelle les utilise tooimpersonate hello base de données utilisateur spécifié compte tooconnect toohello locale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="0ccf0-2868">Dans le cas contraire, la passerelle connecte toohello SQL Server directement avec le contexte de sécurité hello de passerelle (son compte de démarrage).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="0ccf0-2869">Pour plus d’informations, consultez l’article [SQL Server connector (connecteur SQL Server)](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="0ccf0-2870">ACTIVITÉS DE TRANSFORMATION DES DONNÉES</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="0ccf0-2871">Activité</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2871">Activity</span></span> | <span data-ttu-id="0ccf0-2872">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="0ccf0-2873">Activité Hive HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="0ccf0-2874">Hello activité HDInsight Hive dans un pipeline de fabrique de données exécute des requêtes Hive vous-même ou un cluster de basés sur Windows/Linux de HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="0ccf0-2875">Activité Pig HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="0ccf0-2876">Hello activité HDInsight Pig dans un pipeline de fabrique de données exécute des requêtes Pig vous-même ou un cluster de basés sur Windows/Linux de HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="0ccf0-2877">Activité MapReduce HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="0ccf0-2878">Hello activité HDInsight MapReduce dans un pipeline Azure Data Factory exécute les programmes MapReduce vous-même ou un cluster de basés sur Windows/Linux de HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="0ccf0-2879">Activité de diffusion en continu HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="0ccf0-2880">Hello activité de diffusion en continu HDInsight dans un pipeline Azure Data Factory exécute les programmes de diffusion en continu Hadoop sur votre propre ou un cluster de Windows/Linux-based de HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="0ccf0-2881">Activité HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="0ccf0-2882">Hello activité HDInsight Spark dans un pipeline Azure Data Factory exécute les programmes Spark sur votre propre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="0ccf0-2883">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="0ccf0-2884">Azure Data Factory permet tooeasily vous créer des pipelines qui utilisent un publiée Azure Machine Learning web de service pour l’analytique prédictive.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="0ccf0-2885">À l’aide de hello activité d’exécution du lot dans un pipeline Azure Data Factory, vous pouvez appeler une prédictions de toomake du service web Machine Learning sur des données hello dans le lot.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="0ccf0-2886">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="0ccf0-2887">Au fil du temps, d’entrée de modèles prédictifs de hello Bonjour apprentissage expériences score doivent toobe reformé à l’aide de nouveaux jeux de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="0ccf0-2888">Une fois que vous avez terminé avec le réapprentissage, vous souhaitez hello tooupdate calcul du score du service web avec hello reformés modèle d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="0ccf0-2889">Vous pouvez utiliser hello du service web hello tooupdate activité de ressources de mise à jour avec le modèle de hello qui vient d’être formé.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="0ccf0-2890">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="0ccf0-2891">Vous pouvez utiliser l’activité de procédure stockée hello dans un tooinvoke de pipeline de fabrique de données dans une procédure stockée dans un des hello suivant des magasins de données : Azure SQL Database, Azure SQL Data Warehouse, base de données SQL Server dans votre entreprise ou d’une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="0ccf0-2892">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="0ccf0-2893">L’activité U-SQL Data Lake Analytics exécute un script U-SQL sur un cluster Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="0ccf0-2894">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="0ccf0-2895">Si vous avez besoin de données tootransform d’une manière qui n’est pas pris en charge par la fabrique de données, vous pouvez créer une activité personnalisée avec votre propre logique de traitement des données et utiliser l’activité hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="0ccf0-2896">Vous pouvez configurer hello personnalisées .NET activité toorun à l’aide d’un service de traitement par lots Azure ou un cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="0ccf0-2897">Activité Hive HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="0ccf0-2898">Vous pouvez spécifier hello propriétés dans une définition JSON d’activité Hive suivantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="0ccf0-2899">propriété de type Hello pour l’activité de hello doit être : **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="0ccf0-2900">Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="0ccf0-2901">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightHive d’activité :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="0ccf0-2902">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2902">Property</span></span> | <span data-ttu-id="0ccf0-2903">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2903">Description</span></span> | <span data-ttu-id="0ccf0-2904">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2905">script</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2905">script</span></span> |<span data-ttu-id="0ccf0-2906">Spécifiez le script inline Hive de hello</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="0ccf0-2907">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2907">No</span></span> |
| <span data-ttu-id="0ccf0-2908">chemin d'accès du script</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2908">script path</span></span> |<span data-ttu-id="0ccf0-2909">Hello du magasin Hive script dans un stockage d’objets blob Azure et fournir hello chemin d’accès toohello fichier.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="0ccf0-2910">Utilisez la propriété ’script’ ou ’scriptPath’.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="0ccf0-2911">Les deux propriétés ne peuvent pas être utilisées simultanément.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2911">Both cannot be used together.</span></span> <span data-ttu-id="0ccf0-2912">nom de fichier Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="0ccf0-2913">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2913">No</span></span> |
| <span data-ttu-id="0ccf0-2914">defines</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2914">defines</span></span> |<span data-ttu-id="0ccf0-2915">Spécifiez les paramètres en tant que paires clé/valeur pour le référencement dans le script Hive de hello à l’aide de 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="0ccf0-2916">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2916">No</span></span> |

<span data-ttu-id="0ccf0-2917">Ces propriétés sont spécifique toohello activité de la ruche.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="0ccf0-2918">Autres propriétés (à l’extérieur de la section typeProperties hello) sont pris en charge pour toutes les activités.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="0ccf0-2919">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2919">JSON example</span></span>
<span data-ttu-id="0ccf0-2920">Hello suivant JSON définit une activité HDInsight Hive dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="0ccf0-2921">Pour plus d’informations, consultez l’article [Hive Activity (activité Hive)](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="0ccf0-2922">Activité Pig HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="0ccf0-2923">Vous pouvez spécifier des propriétés dans une définition JSON d’activité Pig suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="0ccf0-2924">propriété de type Hello pour l’activité de hello doit être : **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="0ccf0-2925">Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="0ccf0-2926">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightPig d’activité :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="0ccf0-2927">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2927">Property</span></span> | <span data-ttu-id="0ccf0-2928">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2928">Description</span></span> | <span data-ttu-id="0ccf0-2929">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2930">script</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2930">script</span></span> |<span data-ttu-id="0ccf0-2931">Spécifiez hello Pig script inline</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="0ccf0-2932">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2932">No</span></span> |
| <span data-ttu-id="0ccf0-2933">chemin d'accès du script</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2933">script path</span></span> |<span data-ttu-id="0ccf0-2934">Stocker le script Pig hello dans un stockage d’objets blob Azure et fournir hello chemin d’accès toohello fichier.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="0ccf0-2935">Utilisez la propriété ’script’ ou ’scriptPath’.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="0ccf0-2936">Les deux propriétés ne peuvent pas être utilisées simultanément.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2936">Both cannot be used together.</span></span> <span data-ttu-id="0ccf0-2937">nom de fichier Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="0ccf0-2938">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2938">No</span></span> |
| <span data-ttu-id="0ccf0-2939">defines</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2939">defines</span></span> |<span data-ttu-id="0ccf0-2940">Spécifiez les paramètres en tant que paires clé/valeur pour le référencement dans hello script Pig</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="0ccf0-2941">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2941">No</span></span> |

<span data-ttu-id="0ccf0-2942">Ces propriétés sont spécifique toohello activité Pig.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="0ccf0-2943">Autres propriétés (à l’extérieur de la section typeProperties hello) sont pris en charge pour toutes les activités.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="0ccf0-2944">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2944">JSON example</span></span>

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

<span data-ttu-id="0ccf0-2945">Pour plus d’informations, consultez l’article [Pig Activity (activité pig)](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="0ccf0-2946">Activité MapReduce HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="0ccf0-2947">Vous pouvez spécifier des propriétés dans une définition JSON d’activité MapReduce suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="0ccf0-2948">propriété de type Hello pour l’activité de hello doit être : **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="0ccf0-2949">Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="0ccf0-2950">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightMapReduce d’activité :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="0ccf0-2951">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2951">Property</span></span> | <span data-ttu-id="0ccf0-2952">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2952">Description</span></span> | <span data-ttu-id="0ccf0-2953">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2954">jarLinkedService</span></span> | <span data-ttu-id="0ccf0-2955">Nom de hello lié service pourquoi le stockage Azure qui contient le fichier JAR hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="0ccf0-2956">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2956">Yes</span></span> |
| <span data-ttu-id="0ccf0-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2957">jarFilePath</span></span> | <span data-ttu-id="0ccf0-2958">Chemin d’accès le fichier JAR toohello Bonjour Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="0ccf0-2959">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2959">Yes</span></span> | 
| <span data-ttu-id="0ccf0-2960">className</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2960">className</span></span> | <span data-ttu-id="0ccf0-2961">Nom de la classe principale hello dans le fichier JAR hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="0ccf0-2962">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2962">Yes</span></span> | 
| <span data-ttu-id="0ccf0-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2963">arguments</span></span> | <span data-ttu-id="0ccf0-2964">Une liste séparée par des virgules des arguments de programme MapReduce de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="0ccf0-2965">Lors de l’exécution, vous consultez quelques arguments supplémentaires (par exemple : mapreduce.job.tags) à partir de l’infrastructure de MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="0ccf0-2966">toodifferentiate vos arguments avec des arguments de MapReduce hello, envisagez d’utiliser des option et la valeur en tant qu’arguments comme indiqué dans hello exemple suivant (- s,--entrée,--sortie, etc., sont immédiatement suivies par les valeurs des options)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="0ccf0-2967">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="0ccf0-2968">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
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
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="0ccf0-2969">Pour plus d’informations, consultez l’article [MapReduce Activity (activité MapReduce)](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="0ccf0-2970">Activité de diffusion en continu HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="0ccf0-2971">Vous pouvez spécifier hello propriétés dans une définition JSON d’activité de diffusion en continu Hadoop suivantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="0ccf0-2972">propriété de type Hello pour l’activité de hello doit être : **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="0ccf0-2973">Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="0ccf0-2974">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightStreaming d’activité :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="0ccf0-2975">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2975">Property</span></span> | <span data-ttu-id="0ccf0-2976">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="0ccf0-2977">mappeur</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2977">mapper</span></span> | <span data-ttu-id="0ccf0-2978">Nom de l’exécutable du mappeur de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="0ccf0-2979">Dans l’exemple de hello, cat.exe est le Mappeur hello exécutable.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="0ccf0-2980">raccord de réduction</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2980">reducer</span></span> | <span data-ttu-id="0ccf0-2981">Nom de l’exécutable du réducteur de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="0ccf0-2982">Dans l’exemple de hello, wc.exe est hello fichier exécutable du réducteur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="0ccf0-2983">entrée</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2983">input</span></span> | <span data-ttu-id="0ccf0-2984">Fichier d’entrée (y compris l’emplacement) pour le Mappeur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="0ccf0-2985">Dans l’exemple de hello : « wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt » : adfsample est le conteneur d’objets blob hello, exemple/data/Gutenberg est hello dossier, et davinci.txt est l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="0ccf0-2986">sortie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2986">output</span></span> | <span data-ttu-id="0ccf0-2987">Fichier de sortie (y compris l’emplacement) pour le réducteur de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="0ccf0-2988">sortie de Hello du travail de diffusion en continu Hadoop hello est écrite emplacement toohello spécifiée pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="0ccf0-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2989">filePaths</span></span> | <span data-ttu-id="0ccf0-2990">Chemins d’accès pour les exécutables du Mappeur et du réducteur hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="0ccf0-2991">Dans l’exemple de hello : « adfsample/example/apps/wc.exe », adfsample est le conteneur d’objets blob hello, exemple/apps est le dossier de hello et wc.exe est hello exécutable.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="0ccf0-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2992">fileLinkedService</span></span> | <span data-ttu-id="0ccf0-2993">Service lié de stockage Azure qui représente hello le stockage Azure qui contient les fichiers hello spécifiés dans la section de filePaths hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="0ccf0-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2994">arguments</span></span> | <span data-ttu-id="0ccf0-2995">Une liste séparée par des virgules des arguments de programme MapReduce de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="0ccf0-2996">Lors de l’exécution, vous consultez quelques arguments supplémentaires (par exemple : mapreduce.job.tags) à partir de l’infrastructure de MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="0ccf0-2997">toodifferentiate vos arguments avec des arguments de MapReduce hello, envisagez d’utiliser des option et la valeur en tant qu’arguments comme indiqué dans hello exemple suivant (- s,--entrée,--sortie, etc., sont immédiatement suivies par les valeurs des options)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="0ccf0-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2998">getDebugInfo</span></span> | <span data-ttu-id="0ccf0-2999">Un élément facultatif.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-2999">An optional element.</span></span> <span data-ttu-id="0ccf0-3000">Lorsqu’il est défini tooFailure, les journaux de hello sont téléchargés uniquement en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="0ccf0-3001">Lorsqu’il est défini tooAll, les journaux sont toujours téléchargées quel que soit l’état d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="0ccf0-3002">Vous devez spécifier un dataset de sortie pour une activité de Streaming Hadoop de hello pour hello **génère** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="0ccf0-3003">Ce jeu de données peut être uniquement un jeu de données factice qui est requis toodrive hello pipeline planification (horaire, quotidienne, etc.).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="0ccf0-3004">Si l’activité hello n’accepte une entrée, vous pouvez ignorer la spécification d’un jeu de données d’entrée pour l’activité hello pour hello **entrées** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="0ccf0-3005">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3005">JSON example</span></span>

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

<span data-ttu-id="0ccf0-3006">Pour plus d’informations, consultez l’article [Hadoop Streaming Activity (activité de diffusion en continu Hadoop)](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="0ccf0-3007">Activité Spark HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="0ccf0-3008">Vous pouvez spécifier hello propriétés dans une définition JSON d’activité Spark suivantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="0ccf0-3009">propriété de type Hello pour l’activité de hello doit être : **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="0ccf0-3010">Vous devez créer un service lié HDInsight tout d’abord et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="0ccf0-3011">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooHDInsightSpark d’activité :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="0ccf0-3012">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3012">Property</span></span> | <span data-ttu-id="0ccf0-3013">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3013">Description</span></span> | <span data-ttu-id="0ccf0-3014">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="0ccf0-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3015">rootPath</span></span> | <span data-ttu-id="0ccf0-3016">conteneur d’objets Blob Azure Hello et le dossier qui contient le fichier de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="0ccf0-3017">nom de fichier Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="0ccf0-3018">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3018">Yes</span></span> |
| <span data-ttu-id="0ccf0-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3019">entryFilePath</span></span> | <span data-ttu-id="0ccf0-3020">Dossier racine du toohello chemin d’accès relatif de hello Spark/package de code.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="0ccf0-3021">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3021">Yes</span></span> |
| <span data-ttu-id="0ccf0-3022">className</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3022">className</span></span> | <span data-ttu-id="0ccf0-3023">Classe principale Java/Spark de l’application.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="0ccf0-3024">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3024">No</span></span> | 
| <span data-ttu-id="0ccf0-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3025">arguments</span></span> | <span data-ttu-id="0ccf0-3026">Une liste de programme de Spark toohello des arguments de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="0ccf0-3027">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3027">No</span></span> | 
| <span data-ttu-id="0ccf0-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3028">proxyUser</span></span> | <span data-ttu-id="0ccf0-3029">programme Spark de Hello utilisateur compte tooimpersonate tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="0ccf0-3030">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3030">No</span></span> | 
| <span data-ttu-id="0ccf0-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3031">sparkConfig</span></span> | <span data-ttu-id="0ccf0-3032">Propriétés de configuration Spark.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3032">Spark configuration properties.</span></span> | <span data-ttu-id="0ccf0-3033">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3033">No</span></span> | 
| <span data-ttu-id="0ccf0-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3034">getDebugInfo</span></span> | <span data-ttu-id="0ccf0-3035">Spécifie les fichiers journaux hello Spark toohello copié le stockage Azure utilisé par le cluster HDInsight (ou) spécifié par sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="0ccf0-3036">Valeurs autorisées : Aucun, Toujours ou Échec.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="0ccf0-3037">Valeur par défaut : Aucun.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3037">Default value: None.</span></span> | <span data-ttu-id="0ccf0-3038">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3038">No</span></span> | 
| <span data-ttu-id="0ccf0-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="0ccf0-3040">Hello service lié Azure Storage qui contient les journaux, les dépendances et les fichiers de travail hello Spark.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="0ccf0-3041">Si vous ne spécifiez pas une valeur pour cette propriété, le stockage de hello associé au cluster HDInsight est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="0ccf0-3042">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="0ccf0-3043">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3043">JSON example</span></span>

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
<span data-ttu-id="0ccf0-3044">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3044">Note hello following points:</span></span> 

- <span data-ttu-id="0ccf0-3045">Hello **type** propriété a la valeur trop**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="0ccf0-3046">Hello **rootPath** est défini trop**adfspark\\pyFiles** où adfspark est le conteneur d’objets Blob Azure hello et pyFiles est un dossier précis dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="0ccf0-3047">Dans cet exemple, hello stockage d’objets Blob Azure est hello qui est associé au cluster de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="0ccf0-3048">Vous pouvez télécharger hello fichier tooa stockage Azure différent.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="0ccf0-3049">Si vous procédez ainsi, vous pouvez créer un toolink de service lié Azure Storage cette fabrique de données de stockage compte toohello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="0ccf0-3050">Ensuite, spécifiez le nom hello du service de hello lié en tant que valeur pour hello **sparkJobLinkedService** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="0ccf0-3051">Consultez [propriétés de l’activité de Spark](#spark-activity-properties) pour plus d’informations sur cette propriété et d’autres propriétés prises en charge par hello Spark activité.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="0ccf0-3052">Hello **entryFilePath** a la valeur toohello **test.py**, qui est le fichier de python hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="0ccf0-3053">Hello **getDebugInfo** propriété a la valeur trop**toujours**, ce qui signifie que les fichiers journaux de hello est toujours généré (succès ou échec).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="0ccf0-3054">Nous recommandons que vous ne définissez pas cette tooAlways de propriété dans un environnement de production, sauf si vous dépannez un problème.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="0ccf0-3055">Hello **génère** section a un jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="0ccf0-3056">Vous devez spécifier un jeu de données de sortie même si le programme de spark hello ne produit pas de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="0ccf0-3057">planification de hello lecteurs Hello sortie dataset pour le pipeline de hello (horaire, quotidienne, etc.).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="0ccf0-3058">Pour plus d’informations sur l’activité hello, consultez [Spark activité](data-factory-spark.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="0ccf0-3059">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="0ccf0-3060">Vous pouvez spécifier hello propriétés dans une définition JSON d’activité l’exécution du lot Azure ML suivantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="0ccf0-3061">propriété de type Hello pour l’activité de hello doit être : **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="0ccf0-3062">Vous devez créer une Machine Azure tout d’abord le service lié d’apprentissage et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="0ccf0-3063">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooAzureMLBatchExecution d’activité :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="0ccf0-3064">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3064">Property</span></span> | <span data-ttu-id="0ccf0-3065">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3065">Description</span></span> | <span data-ttu-id="0ccf0-3066">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="0ccf0-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3067">webServiceInput</span></span> | <span data-ttu-id="0ccf0-3068">Hello dataset toobe passé en tant qu’entrée pour le service web de Azure ML de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="0ccf0-3069">Ce jeu de données doit également être inclus dans les entrées de hello pour l’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="0ccf0-3070">Utilisez webServiceInput ou webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="0ccf0-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3071">webServiceInputs</span></span> | <span data-ttu-id="0ccf0-3072">Spécifier toobe de jeux de données transmises en tant qu’entrées pour le service web de Azure ML de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="0ccf0-3073">Si le service web de hello accepte plusieurs entrées, utilisez la propriété de webServiceInputs de hello au lieu d’utiliser la propriété de webServiceInput hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="0ccf0-3074">Jeux de données qui est référencées par hello **webServiceInputs** doit également être inclus dans hello activité **entrées**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="0ccf0-3075">Utilisez webServiceInput ou webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="0ccf0-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3076">webServiceOutputs</span></span> | <span data-ttu-id="0ccf0-3077">jeux de données Hello assignés en tant que sorties pour le service web de Azure ML hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="0ccf0-3078">service web de Hello retourne des données de sortie dans ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="0ccf0-3079">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3079">Yes</span></span> | 
<span data-ttu-id="0ccf0-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3080">globalParameters</span></span> | <span data-ttu-id="0ccf0-3081">Spécifiez les valeurs des paramètres de service web hello dans cette section.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="0ccf0-3082">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="0ccf0-3083">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3083">JSON example</span></span>
<span data-ttu-id="0ccf0-3084">Dans cet exemple, activité hello a hello dataset **MLSqlInput** en tant qu’entrée et **MLSqlOutput** en tant que sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="0ccf0-3085">Hello **MLSqlInput** est passée comme un service web toohello d’entrée à l’aide de hello **webServiceInput** propriété JSON.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="0ccf0-3086">Hello **MLSqlOutput** est passé en tant que sortie toohello Web service par à l’aide de hello **webServiceOutputs** propriété JSON.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="0ccf0-3087">Dans l’exemple de JSON hello, hello déployé Azure Machine Learning service Web utilise un lecteur et une writer module tooread/écrire des données à partir de / tooan base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="0ccf0-3088">Ce service Web expose hello quatre paramètres suivants : nom du serveur, nom de la base de données, le nom de compte d’utilisateur serveur et mot de passe utilisateur serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="0ccf0-3089">Uniquement les entrées et sorties de hello AzureMLBatchExecution activité peuvent être passés en tant que paramètres toohello service Web.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="0ccf0-3090">Par exemple, Bonjour ci-dessus extrait de code JSON, MLSqlInput est une activité AzureMLBatchExecution, qui est passée comme un service Web de toohello d’entrée via un paramètre de webServiceInput de toohello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="0ccf0-3091">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="0ccf0-3092">Vous pouvez spécifier hello propriétés dans une définition JSON d’activité ressource Azure ML mise à jour suivantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="0ccf0-3093">propriété de type Hello pour l’activité de hello doit être : **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="0ccf0-3094">Vous devez créer une Machine Azure tout d’abord le service lié d’apprentissage et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="0ccf0-3095">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooAzureMLUpdateResource d’activité :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="0ccf0-3096">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3096">Property</span></span> | <span data-ttu-id="0ccf0-3097">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3097">Description</span></span> | <span data-ttu-id="0ccf0-3098">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="0ccf0-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3099">trainedModelName</span></span> | <span data-ttu-id="0ccf0-3100">Nom de hello reformés modèle.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="0ccf0-3101">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3101">Yes</span></span> |  
<span data-ttu-id="0ccf0-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="0ccf0-3103">Pointage toohello iLearner fichier DataSet retourné par hello réapprentissage d’opération.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="0ccf0-3104">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="0ccf0-3105">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3105">JSON example</span></span>
<span data-ttu-id="0ccf0-3106">pipeline de Hello a deux activités : **AzureMLBatchExecution** et **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="0ccf0-3107">Hello activité d’exécution du lot Azure ML prend les données d’apprentissage hello comme entrée et produit un fichier iLearner comme sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="0ccf0-3108">activité Hello appelle le service web de formation hello (expérience d’apprentissage exposé comme service web) avec une entrée hello données d’apprentissage et reçoit de fichier ilearner de hello de hello webservice.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="0ccf0-3109">Hello placeholderBlob est simplement un dataset de sortie factice est requis par le pipeline hello toorun hello Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="0ccf0-3110">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="0ccf0-3111">Vous pouvez spécifier hello propriétés dans une définition JSON d’activité U-SQL suivantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="0ccf0-3112">propriété de type Hello pour l’activité de hello doit être : **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="0ccf0-3113">Vous devez créer un service Analytique de LAC de données Azure lié et spécifier le nom hello de celui-ci en tant que valeur pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="0ccf0-3114">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello activité tooDataLakeAnalyticsU-SQL :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="0ccf0-3115">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3115">Property</span></span> | <span data-ttu-id="0ccf0-3116">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3116">Description</span></span> | <span data-ttu-id="0ccf0-3117">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3118">scriptPath</span></span> |<span data-ttu-id="0ccf0-3119">Toofolder de chemin d’accès qui contient le script de hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="0ccf0-3120">Nom du fichier de hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="0ccf0-3121">Non (si vous utilisez le script)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3121">No (if you use script)</span></span> |
| <span data-ttu-id="0ccf0-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3122">scriptLinkedService</span></span> |<span data-ttu-id="0ccf0-3123">Service lié qui établit un lien stockage hello qui contient la fabrique de données hello script toohello</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="0ccf0-3124">Non (si vous utilisez le script)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3124">No (if you use script)</span></span> |
| <span data-ttu-id="0ccf0-3125">script</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3125">script</span></span> |<span data-ttu-id="0ccf0-3126">Spécifiez un script en ligne au lieu de spécifier scriptPath et scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="0ccf0-3127">Par exemple : « script » : « Test CRÉER BASE DE DONNÉES ».</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="0ccf0-3128">Non (si vous utilisez scriptPath et scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="0ccf0-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3129">degreeOfParallelism</span></span> |<span data-ttu-id="0ccf0-3130">nombre maximal de Hello de nœuds utilisés simultanément tâche hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="0ccf0-3131">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3131">No</span></span> |
| <span data-ttu-id="0ccf0-3132">priority</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3132">priority</span></span> |<span data-ttu-id="0ccf0-3133">Détermine les tâches en dehors de tout ce qui sont en attente doivent être sélectionné toorun tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="0ccf0-3134">Hello hello numéro inférieur, une priorité plus élevée hello hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="0ccf0-3135">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3135">No</span></span> |
| <span data-ttu-id="0ccf0-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3136">parameters</span></span> |<span data-ttu-id="0ccf0-3137">Paramètres de script de hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="0ccf0-3138">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="0ccf0-3139">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3139">JSON example</span></span>

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

<span data-ttu-id="0ccf0-3140">Pour plus d’informations, consultez [Activité U-SQL Data Lake Analytics](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="0ccf0-3141">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="0ccf0-3142">Vous pouvez spécifier hello propriétés dans une définition JSON d’activité procédure stockée suivantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="0ccf0-3143">propriété de type Hello pour l’activité de hello doit être : **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="0ccf0-3144">Vous devez créer une un Hello suivant des services liés et nommez hello du service de hello lié en tant que valeur pour hello **linkedServiceName** propriété :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="0ccf0-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3145">SQL Server</span></span> 
- <span data-ttu-id="0ccf0-3146">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3146">Azure SQL Database</span></span>
- <span data-ttu-id="0ccf0-3147">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="0ccf0-3148">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooSqlServerStoredProcedure d’activité :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="0ccf0-3149">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3149">Property</span></span> | <span data-ttu-id="0ccf0-3150">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3150">Description</span></span> | <span data-ttu-id="0ccf0-3151">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccf0-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3152">storedProcedureName</span></span> |<span data-ttu-id="0ccf0-3153">Spécifiez le nom hello de procédure stockée hello dans la base de données SQL Azure hello ou d’entrepôt de données SQL Azure qui est représenté par le service hello lié hello utilisations de table de sortie.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="0ccf0-3154">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3154">Yes</span></span> |
| <span data-ttu-id="0ccf0-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3155">storedProcedureParameters</span></span> |<span data-ttu-id="0ccf0-3156">Spécifiez les valeurs des paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="0ccf0-3157">Si vous avez besoin de toopass null pour un paramètre, utilisez la syntaxe de hello : « param1 » : null (toutes les minuscules).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="0ccf0-3158">Consultez hello suivant toolearn exemple sur l’utilisation de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="0ccf0-3159">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3159">No</span></span> |

<span data-ttu-id="0ccf0-3160">Si vous ne spécifiez pas un jeu de données d’entrée, il doit être disponible (en état « Prêt ») pour hello stockées toorun d’activité de procédure.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="0ccf0-3161">Hello de jeu de données d’entrée ne peut pas être utilisé dans la procédure stockée hello en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="0ccf0-3162">Il est uniquement des dépendances hello toocheck utilisé avant l’activité de procédure stockée de départ hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="0ccf0-3163">Vous devez spécifier un jeu de données de sortie pour une activité de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="0ccf0-3164">Dataset de sortie spécifie hello **planification** pour hello stockées activité de procédure (horaire, hebdomadaire, mensuelle, etc.).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="0ccf0-3165">Hello dataset de sortie doit utiliser un **service lié** qui fait référence tooan de base de données SQL Azure ou d’un entrepôt de données SQL Azure ou d’une base de données SQL Server dans lequel vous souhaitez hello toorun de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="0ccf0-3166">Hello dataset de sortie puisse agir comme un moyen toopass hello de résultats de la procédure stockée hello pour un traitement ultérieur par une autre activité ([chaînage des propriétés des activités](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="0ccf0-3167">Toutefois, la fabrique de données n’écrit pas automatiquement sortie hello d’un dataset toothis de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="0ccf0-3168">Il est hello table SQL tooa écritures hello points de jeu de données de sortie à procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="0ccf0-3169">Dans certains cas, le jeu de données de sortie hello peut être un **dataset factice**, qui est utilisé uniquement de l’activité de procédure stockée de toospecify hello planification de l’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="0ccf0-3170">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3170">JSON example</span></span>

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

<span data-ttu-id="0ccf0-3171">Pour plus de détails, consultez l’article [Stored Procedure Activity (activité de procédure stockée)](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="0ccf0-3172">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3172">.NET custom activity</span></span>
<span data-ttu-id="0ccf0-3173">Vous pouvez spécifier hello propriétés dans une activité personnalisée de .NET définition JSON suivantes.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="0ccf0-3174">propriété de type Hello pour l’activité de hello doit être : **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="0ccf0-3175">Vous devez créer un service lié HDInsight Azure ou un traitement par lots Azure liés de service et spécifiez nom hello du service de hello lié en tant que valeur pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="0ccf0-3176">Hello propriétés suivantes sont prises en charge hello **typeProperties** section lorsque vous définissez le type hello de tooDotNetActivity d’activité :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="0ccf0-3177">Propriété</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3177">Property</span></span> | <span data-ttu-id="0ccf0-3178">Description</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3178">Description</span></span> | <span data-ttu-id="0ccf0-3179">Requis</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ccf0-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3180">AssemblyName</span></span> | <span data-ttu-id="0ccf0-3181">Nom de l’assembly hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3181">Name of hello assembly.</span></span> <span data-ttu-id="0ccf0-3182">Dans l’exemple de hello, il est : **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="0ccf0-3183">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3183">Yes</span></span> |
| <span data-ttu-id="0ccf0-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3184">EntryPoint</span></span> |<span data-ttu-id="0ccf0-3185">Nom de classe hello qui implémente l’interface de IDotNetActivity hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="0ccf0-3186">Dans l’exemple de hello, il est : **MyDotNetActivityNS.MyDotNetActivity** où MyDotNetActivityNS est l’espace de noms hello et MyDotNetActivity est la classe hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="0ccf0-3187">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3187">Yes</span></span> | 
| <span data-ttu-id="0ccf0-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3188">PackageLinkedService</span></span> | <span data-ttu-id="0ccf0-3189">Nom du service lié Azure Storage qui pointe de stockage d’objets blob toohello qui contient le fichier zip d’activité personnalisée hello de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="0ccf0-3190">Dans l’exemple de hello, il est : **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="0ccf0-3191">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3191">Yes</span></span> |
| <span data-ttu-id="0ccf0-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3192">PackageFile</span></span> | <span data-ttu-id="0ccf0-3193">Nom du fichier zip de hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3193">Name of hello zip file.</span></span> <span data-ttu-id="0ccf0-3194">Dans l’exemple de hello, il est : **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="0ccf0-3195">Oui</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3195">Yes</span></span> |
| <span data-ttu-id="0ccf0-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3196">extendedProperties</span></span> | <span data-ttu-id="0ccf0-3197">Propriétés étendues que vous pouvez définir et passer sur toohello de code .NET.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="0ccf0-3198">Dans cet exemple, hello **SliceStart** variable est définie la valeur tooa en fonction de la variable de système SliceStart hello.</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="0ccf0-3199">Non</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="0ccf0-3200">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3200">JSON example</span></span>

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

<span data-ttu-id="0ccf0-3201">Pour plus d’informations, consultez l’article [Use custom activities in Data Factory (utiliser des activités personnalisées dans Azure Data Factory)](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0ccf0-3202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3202">Next Steps</span></span>
<span data-ttu-id="0ccf0-3203">Hello suivant les didacticiels, consultez :</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="0ccf0-3204">Didacticiel : créer un pipeline avec une activité de copie</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="0ccf0-3205">Didacticiel : créer un pipeline avec une activité Hive</span><span class="sxs-lookup"><span data-stu-id="0ccf0-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)