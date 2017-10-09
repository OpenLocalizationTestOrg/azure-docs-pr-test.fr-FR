---
title: travaux de Azure IoT Hub aaaUnderstand | Documents Microsoft
description: "Guide du développeur - planification toorun travaux sur plusieurs périphériques connectés tooyour IoT hub. Les tâches peuvent mettre à jour les balises et les propriétés souhaitées, et appeler des méthodes directes sur plusieurs appareils."
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
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="69a0b-104">Planifier des travaux sur plusieurs appareils</span><span class="sxs-lookup"><span data-stu-id="69a0b-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="69a0b-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="69a0b-105">Overview</span></span>
<span data-ttu-id="69a0b-106">Comme décrit dans les articles précédents, Azure IoT Hub utilise un certain nombre de composantes ([balises et propriétés de jumeau d’appareil][lnk-twin-devguide], et [méthodes directes][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="69a0b-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="69a0b-107">En règle générale, les applications back-end activer tooupdate administrateurs et opérateurs de périphérique et d’interagissent avec des appareils IoT en bloc et à une heure planifiée.</span><span class="sxs-lookup"><span data-stu-id="69a0b-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="69a0b-108">Travaux encapsulent l’exécution de hello de mises à jour des deux périphériques et méthodes directes par rapport à un ensemble d’appareils à la fois de la planification.</span><span class="sxs-lookup"><span data-stu-id="69a0b-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="69a0b-109">Par exemple, un opérateur utiliseriez une application back-end lancer et suivre un travail de tooreboot un ensemble d’appareils dans la construction de 43 et étage 3 à un moment qui ne serait pas toohello sans interruption des opérations de construction de hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="69a0b-110">Lorsque toouse</span><span class="sxs-lookup"><span data-stu-id="69a0b-110">When toouse</span></span>
<span data-ttu-id="69a0b-111">Pensez à l’aide de travaux lorsque : une solution principaux besoins tooschedule et les suivre la progression des hello suivant des activités sur un ensemble de périphériques :</span><span class="sxs-lookup"><span data-stu-id="69a0b-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="69a0b-112">Mettre à jour les propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="69a0b-112">Update desired properties</span></span>
* <span data-ttu-id="69a0b-113">Mettre à jour les balises</span><span class="sxs-lookup"><span data-stu-id="69a0b-113">Update tags</span></span>
* <span data-ttu-id="69a0b-114">Appeler des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="69a0b-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="69a0b-115">Cycle de vie de tâche</span><span class="sxs-lookup"><span data-stu-id="69a0b-115">Job lifecycle</span></span>
<span data-ttu-id="69a0b-116">Tâches sont lancées par hello solution back-end et gérées par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="69a0b-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="69a0b-117">Vous pouvez lancer un travail via une URI de service (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) et vérifier la progression d’un travail en cours via une URI de service (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="69a0b-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="69a0b-118">Une fois qu’un travail est initié, interrogation pour les travaux Active l’état de hello hello principal application toorefresh de travaux en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="69a0b-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="69a0b-119">Lorsque vous lancez un travail, les valeurs et les noms de propriété ne peuvent contenir US-ASCII imprimable alphanumérique, à l’exception dans l’ensemble suivant de hello : ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="69a0b-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="69a0b-120">Rubriques de référence :</span><span class="sxs-lookup"><span data-stu-id="69a0b-120">Reference topics:</span></span>
<span data-ttu-id="69a0b-121">Hello rubriques de référence suivantes vous fournit plus d’informations sur l’utilisation de travaux.</span><span class="sxs-lookup"><span data-stu-id="69a0b-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="69a0b-122">Méthodes de travaux tooexecute directes</span><span class="sxs-lookup"><span data-stu-id="69a0b-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="69a0b-123">Détails pour l’exécution de la demande hello HTTP 1.1 est Hello suivant un [méthode directe] [ lnk-dev-methods] sur un ensemble de périphériques à l’aide d’une tâche :</span><span class="sxs-lookup"><span data-stu-id="69a0b-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="69a0b-124">condition de requête Hello peut également être sur un seul Id de périphérique ou sur une liste d’ID de l’appareil comme indiqué ci-dessous</span><span class="sxs-lookup"><span data-stu-id="69a0b-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="69a0b-125">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="69a0b-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="69a0b-126">Le [langage de requête IoT Hub][lnk-query] couvre le langage de requête IoT Hub plus en détail.</span><span class="sxs-lookup"><span data-stu-id="69a0b-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="69a0b-127">Propriétés de travaux tooupdate périphérique double</span><span class="sxs-lookup"><span data-stu-id="69a0b-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="69a0b-128">Hello Voici des détails de la demande de mise à jour des propriétés de l’appareil double à l’aide d’un travail hello HTTP 1.1 :</span><span class="sxs-lookup"><span data-stu-id="69a0b-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="69a0b-129">Vérification de la progression des travaux</span><span class="sxs-lookup"><span data-stu-id="69a0b-129">Querying for progress on jobs</span></span>
<span data-ttu-id="69a0b-130">Hello Voici hello détails de la demande HTTP 1.1 pour [interrogation pour les travaux][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="69a0b-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="69a0b-131">Hello continuationToken est fournie à partir de la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="69a0b-132">Propriétés des travaux</span><span class="sxs-lookup"><span data-stu-id="69a0b-132">Jobs Properties</span></span>
<span data-ttu-id="69a0b-133">Hello Voici une liste de propriétés et les descriptions correspondantes, ce qui peuvent être utilisées lors de l’interrogation pour les tâches ou les résultats de la tâche.</span><span class="sxs-lookup"><span data-stu-id="69a0b-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="69a0b-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="69a0b-134">Property</span></span> | <span data-ttu-id="69a0b-135">Description</span><span class="sxs-lookup"><span data-stu-id="69a0b-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69a0b-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="69a0b-136">**jobId**</span></span> |<span data-ttu-id="69a0b-137">Application fourni un ID de tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="69a0b-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="69a0b-138">**startTime**</span></span> |<span data-ttu-id="69a0b-139">Heure de début application fournie (ISO-8601) pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="69a0b-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="69a0b-140">**endTime**</span></span> |<span data-ttu-id="69a0b-141">IoT Hub fourni date (ISO-8601) de fin du travail hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="69a0b-142">Valide uniquement lorsque le travail de hello atteint l’état de hello 'terminé'.</span><span class="sxs-lookup"><span data-stu-id="69a0b-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="69a0b-143">**type**</span><span class="sxs-lookup"><span data-stu-id="69a0b-143">**type**</span></span> |<span data-ttu-id="69a0b-144">Types de tâches :</span><span class="sxs-lookup"><span data-stu-id="69a0b-144">Types of jobs:</span></span> |
| <span data-ttu-id="69a0b-145">**scheduledUpdateTwin**: un tooupdate de travail utilisé un ensemble de propriétés souhaitées ou de balises.</span><span class="sxs-lookup"><span data-stu-id="69a0b-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="69a0b-146">**scheduledDeviceMethod**: un tooinvoke de travail utilisé une méthode de l’appareil sur un ensemble de jumeaux de périphérique.</span><span class="sxs-lookup"><span data-stu-id="69a0b-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="69a0b-147">**statut**</span><span class="sxs-lookup"><span data-stu-id="69a0b-147">**status**</span></span> |<span data-ttu-id="69a0b-148">État actuel du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-148">Current state of hello job.</span></span> <span data-ttu-id="69a0b-149">Valeurs possibles pour l'état :</span><span class="sxs-lookup"><span data-stu-id="69a0b-149">Possible values for status:</span></span> |
| <span data-ttu-id="69a0b-150">**en attente** : planifié et en attente toobe récupéré par le service de travail hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="69a0b-151">**planifiée** : planifiée pour une heure dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="69a0b-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="69a0b-152">**running** : le travail est actuellement actif.</span><span class="sxs-lookup"><span data-stu-id="69a0b-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="69a0b-153">**cancelled** : le travail a été annulé.</span><span class="sxs-lookup"><span data-stu-id="69a0b-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="69a0b-154">**failed** : échec de la tâche.</span><span class="sxs-lookup"><span data-stu-id="69a0b-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="69a0b-155">**completed** : le travail est terminé..&lt;/seg&gt;</span><span class="sxs-lookup"><span data-stu-id="69a0b-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="69a0b-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="69a0b-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="69a0b-157">Statistiques sur l’exécution de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="69a0b-158">Propriétés **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="69a0b-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="69a0b-159">Propriété</span><span class="sxs-lookup"><span data-stu-id="69a0b-159">Property</span></span> | <span data-ttu-id="69a0b-160">Description</span><span class="sxs-lookup"><span data-stu-id="69a0b-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69a0b-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="69a0b-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="69a0b-162">Nombre de périphériques dans la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="69a0b-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="69a0b-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="69a0b-164">Nombre d’appareils où le travail de hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="69a0b-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="69a0b-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="69a0b-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="69a0b-166">Nombre de périphériques sur lequel le travail de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="69a0b-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="69a0b-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="69a0b-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="69a0b-168">Nombre de périphériques qui sont en cours d’exécution des travaux de hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="69a0b-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="69a0b-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="69a0b-170">Nombre de périphériques qui sont en attente de travail de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="69a0b-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="69a0b-171">Matériel de référence supplémentaire</span><span class="sxs-lookup"><span data-stu-id="69a0b-171">Additional reference material</span></span>
<span data-ttu-id="69a0b-172">Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="69a0b-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="69a0b-173">[Points de terminaison IoT Hub] [ lnk-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.</span><span class="sxs-lookup"><span data-stu-id="69a0b-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="69a0b-174">[Limitation et les quotas] [ lnk-quotas] décrit les quotas hello qui s’appliquent toohello IoT Hub service hello limitation tooexpect de comportement lorsque vous utilisez le service de hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="69a0b-175">[Azure IoT périphérique et service kits de développement logiciel] [ lnk-sdks] listes hello langue différents kits de développement logiciel vous une utilisation lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="69a0b-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="69a0b-176">[Langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages] [ lnk-query] décrit le langage de requête IoT Hub vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux de hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="69a0b-177">[Prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] fournit plus d’informations sur la prise en charge IoT Hub pour le protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="69a0b-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69a0b-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69a0b-178">Next steps</span></span>
<span data-ttu-id="69a0b-179">Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant IoT Hub didacticiel :</span><span class="sxs-lookup"><span data-stu-id="69a0b-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="69a0b-180">[Planifier et diffuser des travaux][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="69a0b-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
