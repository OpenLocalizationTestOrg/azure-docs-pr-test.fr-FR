---
title: "Présentation des tâches Azure IoT Hub | Microsoft Docs"
description: "Guide du développeur - Planification des travaux à exécuter sur plusieurs appareils connectés à votre IoT Hub. Les tâches peuvent mettre à jour les balises et les propriétés souhaitées, et appeler des méthodes directes sur plusieurs appareils."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="aac4d-104">Planifier des travaux sur plusieurs appareils</span><span class="sxs-lookup"><span data-stu-id="aac4d-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="aac4d-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="aac4d-105">Overview</span></span>
<span data-ttu-id="aac4d-106">Comme décrit dans les articles précédents, Azure IoT Hub utilise un certain nombre de composantes ([balises et propriétés de jumeau d’appareil][lnk-twin-devguide], et [méthodes directes][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="aac4d-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="aac4d-107">Généralement, les applications principales permettent aux administrateurs et opérateurs d’appareil de mettre à jour et d’interagir avec les appareils IoT par lots et à une heure planifiée.</span><span class="sxs-lookup"><span data-stu-id="aac4d-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="aac4d-108">Les travaux englobent l’exécution des mises à jour des jumeaux d’appareil et des méthodes directes sur un ensemble d’appareils à une heure planifiée.</span><span class="sxs-lookup"><span data-stu-id="aac4d-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="aac4d-109">Par exemple, un opérateur peut utiliser une application principale qui lance et suit un travail pour le redémarrage d’un ensemble d’appareils dans le bâtiment 43 à l’étage 3 à une heure qui ne perturbera pas les opérations du bâtiment.</span><span class="sxs-lookup"><span data-stu-id="aac4d-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="aac4d-110">Quand utiliser</span><span class="sxs-lookup"><span data-stu-id="aac4d-110">When to use</span></span>
<span data-ttu-id="aac4d-111">Pensez utiliser les travaux dans ce cas : une solution principale doit planifier et suivre la progression des activités suivantes sur un ensemble d’appareils :</span><span class="sxs-lookup"><span data-stu-id="aac4d-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="aac4d-112">Mettre à jour les propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="aac4d-112">Update desired properties</span></span>
* <span data-ttu-id="aac4d-113">Mettre à jour les balises</span><span class="sxs-lookup"><span data-stu-id="aac4d-113">Update tags</span></span>
* <span data-ttu-id="aac4d-114">Appeler des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="aac4d-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="aac4d-115">Cycle de vie de tâche</span><span class="sxs-lookup"><span data-stu-id="aac4d-115">Job lifecycle</span></span>
<span data-ttu-id="aac4d-116">Les travaux sont lancés par l’application principale de la solution et maintenus par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="aac4d-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="aac4d-117">Vous pouvez lancer un travail via une URI de service (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) et vérifier la progression d’un travail en cours via une URI de service (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="aac4d-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="aac4d-118">Une fois qu’un travail est initialisé, la vérification des travaux permet à l’application principale d’actualiser l’état des tâches en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="aac4d-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="aac4d-119">Lorsque vous lancez une tâche, les noms et valeurs de propriété peuvent contenir uniquement des caractères alphanumériques US-ASCII imprimables, à l’exception des caractères suivants : ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="aac4d-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="aac4d-120">Rubriques de référence :</span><span class="sxs-lookup"><span data-stu-id="aac4d-120">Reference topics:</span></span>
<span data-ttu-id="aac4d-121">Les rubriques de référence suivantes vous fournissent des informations supplémentaires sur l’utilisation des travaux.</span><span class="sxs-lookup"><span data-stu-id="aac4d-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="aac4d-122">Tâches pour exécuter des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="aac4d-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="aac4d-123">Voici les détails de la requête HTTP 1.1 pour exécuter une [méthode directe][lnk-dev-methods] sur un ensemble d’appareils en utilisant un travail :</span><span class="sxs-lookup"><span data-stu-id="aac4d-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
<span data-ttu-id="aac4d-124">La condition de requête peut également être un ID d’appareil unique ou figurer sur une liste d’ID comme illustré ci-dessous</span><span class="sxs-lookup"><span data-stu-id="aac4d-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="aac4d-125">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="aac4d-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="aac4d-126">Le [langage de requête IoT Hub][lnk-query] couvre le langage de requête IoT Hub plus en détail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="aac4d-127">Travaux pour mettre à jour les propriétés d’un jumeau d’appareil</span><span class="sxs-lookup"><span data-stu-id="aac4d-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="aac4d-128">Voici les détails de la requête HTTP 1.1 pour mettre à jour les propriétés d’un jumeau d’appareil à l’aide d’un travail :</span><span class="sxs-lookup"><span data-stu-id="aac4d-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="aac4d-129">Vérification de la progression des travaux</span><span class="sxs-lookup"><span data-stu-id="aac4d-129">Querying for progress on jobs</span></span>
<span data-ttu-id="aac4d-130">Voici les détails de la requête HTTP 1.1 pour [interroger des travaux][lnk-query] :</span><span class="sxs-lookup"><span data-stu-id="aac4d-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="aac4d-131">Le paramètre continuationToken est fourni dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="aac4d-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="aac4d-132">Propriétés des travaux</span><span class="sxs-lookup"><span data-stu-id="aac4d-132">Jobs Properties</span></span>
<span data-ttu-id="aac4d-133">Voici une liste de propriétés et de descriptions correspondantes qui peuvent être utilisées lors de la vérification de travaux ou des résultats de travaux.</span><span class="sxs-lookup"><span data-stu-id="aac4d-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="aac4d-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="aac4d-134">Property</span></span> | <span data-ttu-id="aac4d-135">Description</span><span class="sxs-lookup"><span data-stu-id="aac4d-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aac4d-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="aac4d-136">**jobId**</span></span> |<span data-ttu-id="aac4d-137">L’application a fourni un ID pour le travail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="aac4d-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="aac4d-138">**startTime**</span></span> |<span data-ttu-id="aac4d-139">L’application a fourni l’heure de début (ISO-8601) pour le travail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="aac4d-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="aac4d-140">**endTime**</span></span> |<span data-ttu-id="aac4d-141">IoT Hub a fourni la date (ISO-8601) de fin du travail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="aac4d-142">Valide uniquement lorsque la tâche atteint l’état « terminé ».</span><span class="sxs-lookup"><span data-stu-id="aac4d-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="aac4d-143">**type**</span><span class="sxs-lookup"><span data-stu-id="aac4d-143">**type**</span></span> |<span data-ttu-id="aac4d-144">Types de tâches :</span><span class="sxs-lookup"><span data-stu-id="aac4d-144">Types of jobs:</span></span> |
| <span data-ttu-id="aac4d-145">**scheduledUpdateTwin** : travail permettant de mettre à jour un ensemble de propriétés souhaitées ou de balises.</span><span class="sxs-lookup"><span data-stu-id="aac4d-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="aac4d-146">**scheduledDeviceMethod** : travail permettant d’appeler une méthode d’appareil sur un ensemble de jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="aac4d-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="aac4d-147">**statut**</span><span class="sxs-lookup"><span data-stu-id="aac4d-147">**status**</span></span> |<span data-ttu-id="aac4d-148">État actuel du travail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-148">Current state of the job.</span></span> <span data-ttu-id="aac4d-149">Valeurs possibles pour l'état :</span><span class="sxs-lookup"><span data-stu-id="aac4d-149">Possible values for status:</span></span> |
| <span data-ttu-id="aac4d-150">**pending** : planifié et en attente de récupération par le service du travail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="aac4d-151">**scheduled** : planifié pour une date ultérieure.</span><span class="sxs-lookup"><span data-stu-id="aac4d-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="aac4d-152">**running** : le travail est actuellement actif.</span><span class="sxs-lookup"><span data-stu-id="aac4d-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="aac4d-153">**cancelled** : le travail a été annulé.</span><span class="sxs-lookup"><span data-stu-id="aac4d-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="aac4d-154">**failed** : échec de la tâche.</span><span class="sxs-lookup"><span data-stu-id="aac4d-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="aac4d-155">**completed** : le travail est terminé..</seg></span><span class="sxs-lookup"><span data-stu-id="aac4d-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="aac4d-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="aac4d-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="aac4d-157">Statistiques relatives à l’exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="aac4d-158">Propriétés **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="aac4d-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="aac4d-159">Propriété</span><span class="sxs-lookup"><span data-stu-id="aac4d-159">Property</span></span> | <span data-ttu-id="aac4d-160">Description</span><span class="sxs-lookup"><span data-stu-id="aac4d-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aac4d-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="aac4d-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="aac4d-162">Nombre d’appareils du travail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="aac4d-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="aac4d-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="aac4d-164">Nombre d’appareils sur lesquels le travail a échoué.</span><span class="sxs-lookup"><span data-stu-id="aac4d-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="aac4d-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="aac4d-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="aac4d-166">Nombre d’appareils sur lesquels le travail a réussi.</span><span class="sxs-lookup"><span data-stu-id="aac4d-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="aac4d-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="aac4d-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="aac4d-168">Nombre d’appareils qui exécutent actuellement le travail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="aac4d-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="aac4d-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="aac4d-170">Nombre d’appareils en attente d’exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="aac4d-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="aac4d-171">Matériel de référence supplémentaire</span><span class="sxs-lookup"><span data-stu-id="aac4d-171">Additional reference material</span></span>
<span data-ttu-id="aac4d-172">Les autres rubriques de référence dans le Guide du développeur IoT Hub comprennent :</span><span class="sxs-lookup"><span data-stu-id="aac4d-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="aac4d-173">La rubrique [Points de terminaison IoT Hub][lnk-endpoints] décrit les différents points de terminaison que chaque IoT Hub expose pour les opérations d’exécution et de gestion.</span><span class="sxs-lookup"><span data-stu-id="aac4d-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="aac4d-174">La rubrique [Quotas et limitation][lnk-quotas] décrit les quotas appliqués au service IoT Hub, et le comportement de limitation auquel s’attendre en cas d’utilisation du service.</span><span class="sxs-lookup"><span data-stu-id="aac4d-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="aac4d-175">La section [Azure IoT device et service SDK][lnk-sdks] répertorie les Kits de développement logiciel (SDK) en différents langages que vous pouvez utiliser lors du développement d’applications d’appareil et de service qui interagissent avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="aac4d-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="aac4d-176">L’article [Langage de requête d’IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages][lnk-query] décrit le langage de requête d’IoT Hub permettant de récupérer, à partir d’IoT Hub, des informations relatives à vos jumeaux d’appareil et à vos travaux.</span><span class="sxs-lookup"><span data-stu-id="aac4d-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="aac4d-177">La rubrique [Prise en charge de MQTT au niveau d’IoT Hub][lnk-devguide-mqtt] fournit des informations supplémentaires sur la prise en charge du protocole MQTT par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="aac4d-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aac4d-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aac4d-178">Next steps</span></span>
<span data-ttu-id="aac4d-179">Si vous souhaitez tenter de mettre en pratique certains des concepts décrits dans cet article, vous serez peut-être intéressé par les didacticiels IoT Hub suivants :</span><span class="sxs-lookup"><span data-stu-id="aac4d-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="aac4d-180">[Planifier et diffuser des travaux][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="aac4d-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
