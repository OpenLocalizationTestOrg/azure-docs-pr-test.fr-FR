---
title: "Comprendre le langage de requête d’Azure IoT Hub | Microsoft Docs"
description: "Guide du développeur - Description du langage de requête IoT Hub de type SQL utilisé pour récupérer des informations sur les jumeaux d’appareil et les travaux à partir de votre hub IoT."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: a7650104eda58923558892f6f0f6666d16dbce28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="9ce66-103">Référence - Langage de requête IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages</span><span class="sxs-lookup"><span data-stu-id="9ce66-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="9ce66-104">IoT Hub fournit un puissant langage de type SQL pour récupérer des informations concernant les [jumeaux d’appareil][lnk-twins], les [travaux][lnk-jobs] et le [routage des messages][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="9ce66-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="9ce66-105">Cet article présente les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9ce66-105">This article presents:</span></span>

* <span data-ttu-id="9ce66-106">Une introduction aux principales fonctionnalités du langage de requête d’IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9ce66-106">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="9ce66-107">Une description détaillée du langage</span><span class="sxs-lookup"><span data-stu-id="9ce66-107">The detailed description of the language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="9ce66-108">Bien démarrer avec les requêtes de jumeau d’appareil</span><span class="sxs-lookup"><span data-stu-id="9ce66-108">Get started with device twin queries</span></span>
<span data-ttu-id="9ce66-109">Des [jumeaux d’appareil][lnk-twins] peuvent contenir des objets JSON arbitraires tels que des balises (tags) et des propriétés.</span><span class="sxs-lookup"><span data-stu-id="9ce66-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="9ce66-110">IoT Hub vous permet d’interroger des jumeaux d’appareil sous la forme d’un seul document JSON contenant toutes les informations sur les jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="9ce66-110">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="9ce66-111">Par exemple, supposons que vos jumeaux d’appareil IoT Hub présentent la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="9ce66-111">Assume, for instance, that your IoT hub device twins have the following structure:</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

<span data-ttu-id="9ce66-112">IoT Hub expose les jumeaux d’appareil en tant que collection de documents appelée **appareils**.</span><span class="sxs-lookup"><span data-stu-id="9ce66-112">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="9ce66-113">Par conséquent, la requête suivante récupère l’ensemble des jumeaux d’appareil :</span><span class="sxs-lookup"><span data-stu-id="9ce66-113">So the following query retrieves the whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="9ce66-114">Les kits [Azure IoT SDK][lnk-hub-sdks] prennent en charge la pagination des résultats volumineux.</span><span class="sxs-lookup"><span data-stu-id="9ce66-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="9ce66-115">IoT Hub vous permet de récupérer les jumeaux d’appareil en les filtrant avec des conditions arbitraires.</span><span class="sxs-lookup"><span data-stu-id="9ce66-115">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="9ce66-116">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="9ce66-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="9ce66-117">récupère les jumeaux d’appareil dont la balise **location.region** est définie sur **US**.</span><span class="sxs-lookup"><span data-stu-id="9ce66-117">retrieves the device twins with the **location.region** tag set to **US**.</span></span>
<span data-ttu-id="9ce66-118">Les opérateurs booléens et les comparaisons arithmétiques sont également pris en charge, par exemple,</span><span class="sxs-lookup"><span data-stu-id="9ce66-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="9ce66-119">récupère tous les jumeaux d’appareil situés aux États-Unis qui sont configurés pour envoyer des données de télémétrie moins souvent qu’une fois par minute.</span><span class="sxs-lookup"><span data-stu-id="9ce66-119">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span></span> <span data-ttu-id="9ce66-120">Pour des raisons pratiques, il est également possible d’utiliser des constantes de matrice avec les opérateurs **IN** (dans) et **NIN** (pas dans).</span><span class="sxs-lookup"><span data-stu-id="9ce66-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="9ce66-121">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="9ce66-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="9ce66-122">récupère tous les jumeaux d’appareil ayant signalé une connectivité Wi-Fi ou câblée.</span><span class="sxs-lookup"><span data-stu-id="9ce66-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="9ce66-123">Il est souvent nécessaire d’identifier tous les jumeaux d’appareil qui contiennent une propriété spécifique.</span><span class="sxs-lookup"><span data-stu-id="9ce66-123">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="9ce66-124">IoT Hub prend en charge la fonction `is_defined()` à cette fin.</span><span class="sxs-lookup"><span data-stu-id="9ce66-124">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="9ce66-125">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="9ce66-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="9ce66-126">a récupéré tous les jumeaux d’appareil qui définissent la propriété signalée `connectivity`.</span><span class="sxs-lookup"><span data-stu-id="9ce66-126">retrieved all device twins that define the `connectivity` reported property.</span></span> <span data-ttu-id="9ce66-127">Pour une référence complète sur les fonctionnalités de filtrage, consultez la section [clause WHERE][lnk-query-where].</span><span class="sxs-lookup"><span data-stu-id="9ce66-127">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="9ce66-128">Le regroupement et les agrégations sont également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9ce66-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="9ce66-129">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="9ce66-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="9ce66-130">retourne le nombre d’appareils dans chaque état de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9ce66-130">returns the count of the devices in each telemetry configuration status.</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="9ce66-131">L’exemple précédent illustre une situation où trois appareils ont signalé une configuration réussie, deux d’entre eux appliquant toujours la configuration et le troisième ayant signalé une erreur.</span><span class="sxs-lookup"><span data-stu-id="9ce66-131">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="9ce66-132">Exemple en code C#</span><span class="sxs-lookup"><span data-stu-id="9ce66-132">C# example</span></span>
<span data-ttu-id="9ce66-133">La fonctionnalité de requête est exposée par [Service SDK C#][lnk-hub-sdks] dans la classe **RegistryManager**.</span><span class="sxs-lookup"><span data-stu-id="9ce66-133">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="9ce66-134">Voici un exemple de requête simple :</span><span class="sxs-lookup"><span data-stu-id="9ce66-134">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="9ce66-135">Notez comment l’objet **query** est instancié avec une taille de page (jusqu’à 1 000), puis comment plusieurs pages peuvent être récupérées en appelant la méthode **GetNextAsTwinAsync** plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="9ce66-135">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="9ce66-136">Notez que l’objet query expose plusieurs **Next\***, selon l’option de désérialisation requise par la requête, par exemple des objets jumeau d’appareil ou travail, ou un JSON simple à utiliser en cas d’utilisation de projections.</span><span class="sxs-lookup"><span data-stu-id="9ce66-136">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="9ce66-137">Exemple de Node.js</span><span class="sxs-lookup"><span data-stu-id="9ce66-137">Node.js example</span></span>
<span data-ttu-id="9ce66-138">La fonctionnalité de requête est exposée par le [Kit de développement logiciel (SDK) de service Azure IoT pour Node.js][lnk-hub-sdks] dans l’objet **Registry**.</span><span class="sxs-lookup"><span data-stu-id="9ce66-138">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="9ce66-139">Voici un exemple de requête simple :</span><span class="sxs-lookup"><span data-stu-id="9ce66-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed to fetch the results: ' + err.message);
    } else {
        // Do something with the results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="9ce66-140">Notez comment l’objet **query** est instancié avec une taille de page (jusqu’à 1000), puis comment plusieurs pages peuvent être récupérées en appelant la méthode **nextAsTwin** plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="9ce66-140">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="9ce66-141">Notez que l’objet query expose plusieurs **next\***, selon l’option de désérialisation requise par la requête, par exemple des objets jumeau d’appareil ou travail, ou un JSON simple à utiliser en cas d’utilisation de projections.</span><span class="sxs-lookup"><span data-stu-id="9ce66-141">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="9ce66-142">Limitations</span><span class="sxs-lookup"><span data-stu-id="9ce66-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9ce66-143">Les résultats de la requête peuvent être produits avec quelques minutes de retard par rapport aux dernières valeurs dans les jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="9ce66-143">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="9ce66-144">Lors d’une recherche de jumeaux d’appareil par ID, il est toujours préférable d’utiliser l’API de récupération des jumeaux d’appareil, qui contient toujours les valeurs les plus récentes et qui a un seuil de limitation plus élevé.</span><span class="sxs-lookup"><span data-stu-id="9ce66-144">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span></span>

<span data-ttu-id="9ce66-145">Actuellement, les comparaisons ne sont prises en charge qu’entre types primitifs (aucun objet), par exemple `... WHERE properties.desired.config = properties.reported.config` est pris en charge uniquement si ces propriétés ont des valeurs primitives.</span><span class="sxs-lookup"><span data-stu-id="9ce66-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="9ce66-146">Bien démarrer avec les requêtes de travaux</span><span class="sxs-lookup"><span data-stu-id="9ce66-146">Get started with jobs queries</span></span>
<span data-ttu-id="9ce66-147">Les [travaux][lnk-jobs] constituent un moyen d’exécuter des opérations sur des ensembles d’appareils.</span><span class="sxs-lookup"><span data-stu-id="9ce66-147">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="9ce66-148">Chaque jumeau d’appareil contient les informations des travaux auxquels il participe dans un regroupement nommé **travaux**.</span><span class="sxs-lookup"><span data-stu-id="9ce66-148">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="9ce66-149">Sous forme logique,</span><span class="sxs-lookup"><span data-stu-id="9ce66-149">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="9ce66-150">Actuellement, ce regroupement peut être interrogé en tant que **devices.jobs** dans le langage de requête d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9ce66-150">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ce66-151">Actuellement, la propriété de travaux n’est jamais retournée lorsque des jumeaux d’appareil sont interrogés (c’est-à-dire pour les requêtes qui contiennent « FROM appareils »).</span><span class="sxs-lookup"><span data-stu-id="9ce66-151">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="9ce66-152">Elle est uniquement accessible directement avec des requêtes utilisant `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="9ce66-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="9ce66-153">Par exemple, pour obtenir tous les travaux (passés et planifiés) qui affectent un appareil donné, vous pouvez utiliser la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="9ce66-153">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="9ce66-154">Notez comment cette requête fournit l’état spécifique de l’appareil (et éventuellement la réponse de méthode directe) pour chaque travail retourné.</span><span class="sxs-lookup"><span data-stu-id="9ce66-154">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="9ce66-155">Il est également possible de filtrer avec des conditions booléennes arbitraires sur toutes les propriétés d’objet du regroupement **devices.jobs**.</span><span class="sxs-lookup"><span data-stu-id="9ce66-155">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="9ce66-156">Par exemple, la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="9ce66-156">For instance, the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="9ce66-157">récupère tous les travaux de mise à jour du jumeau de l’appareil **myDeviceId**, qui ont été créés après le mois de septembre 2016.</span><span class="sxs-lookup"><span data-stu-id="9ce66-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="9ce66-158">Il est également possible de récupérer les résultats d’un travail unique par appareil.</span><span class="sxs-lookup"><span data-stu-id="9ce66-158">It is also possible to retrieve the per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="9ce66-159">Limitations</span><span class="sxs-lookup"><span data-stu-id="9ce66-159">Limitations</span></span>
<span data-ttu-id="9ce66-160">Actuellement, les requêtes sur **devices.jobs** ne prennent pas en charge :</span><span class="sxs-lookup"><span data-stu-id="9ce66-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="9ce66-161">Les projections, par conséquent seul `SELECT *` est possible.</span><span class="sxs-lookup"><span data-stu-id="9ce66-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="9ce66-162">Les conditions faisant référence au jumeau d’appareil en plus des propriétés du travail (voir section précédente).</span><span class="sxs-lookup"><span data-stu-id="9ce66-162">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="9ce66-163">L’exécution d’agrégations, par exemple, count, avg, group by.</span><span class="sxs-lookup"><span data-stu-id="9ce66-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="9ce66-164">Bien démarrer avec les expressions de requête d’itinéraires de messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="9ce66-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="9ce66-165">À l’aide des [itinéraires appareil-à-cloud][lnk-devguide-messaging-routes], vous pouvez configurer IoT Hub pour distribuer les messages appareil-à-cloud sur différents points de terminaison sur la base d’expressions évaluées par rapport à des messages individuels.</span><span class="sxs-lookup"><span data-stu-id="9ce66-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="9ce66-166">La [condition][lnk-query-expressions] d’itinéraire utilise le même langage de requête IoT Hub que les conditions des requêtes de jumeau et de travail.</span><span class="sxs-lookup"><span data-stu-id="9ce66-166">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="9ce66-167">Les conditions de routage sont évaluées sur les en-têtes et le corps des messages.</span><span class="sxs-lookup"><span data-stu-id="9ce66-167">Route conditions are evaluated on the message headers and body.</span></span> <span data-ttu-id="9ce66-168">Votre expression de requête de routage peut impliquer uniquement des en-têtes de message, uniquement le corps du message ou à la fois des en-têtes de message et le corps du message.</span><span class="sxs-lookup"><span data-stu-id="9ce66-168">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span></span> <span data-ttu-id="9ce66-169">IoT Hub suppose un schéma spécifique pour les en-têtes et le corps du message afin d’acheminer les messages. Les sections suivantes décrivent ce dont a besoin IoT Hub pour effectuer le routage correctement :</span><span class="sxs-lookup"><span data-stu-id="9ce66-169">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="9ce66-170">Routage sur les en-têtes de message</span><span class="sxs-lookup"><span data-stu-id="9ce66-170">Routing on message headers</span></span>

<span data-ttu-id="9ce66-171">IoT Hub suppose la représentation JSON suivante d’en-têtes de message pour le routage des messages :</span><span class="sxs-lookup"><span data-stu-id="9ce66-171">IoT Hub assumes the following JSON representation of message headers for message routing:</span></span>

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

<span data-ttu-id="9ce66-172">Les propriétés système du message ont pour préfixe le symbole `'$'`.</span><span class="sxs-lookup"><span data-stu-id="9ce66-172">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="9ce66-173">Les propriétés de l’utilisateur sont toujours accessibles par leur nom.</span><span class="sxs-lookup"><span data-stu-id="9ce66-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="9ce66-174">Si un nom de propriété d’utilisateur coïncide avec une propriété système (telle que `$to`), la propriété de l’utilisateur est récupérée avec l’expression `$to`.</span><span class="sxs-lookup"><span data-stu-id="9ce66-174">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span></span>
<span data-ttu-id="9ce66-175">Vous pouvez toujours accéder à la propriété système à l’aide de crochets `{}` : par exemple, vous pouvez utiliser l’expression `{$to}` pour accéder à la propriété système `to`.</span><span class="sxs-lookup"><span data-stu-id="9ce66-175">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span></span> <span data-ttu-id="9ce66-176">Les noms de propriétés entre crochets récupèrent toujours la propriété système correspondante.</span><span class="sxs-lookup"><span data-stu-id="9ce66-176">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="9ce66-177">N’oubliez pas que les noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="9ce66-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="9ce66-178">Toutes les propriétés de message sont des chaînes.</span><span class="sxs-lookup"><span data-stu-id="9ce66-178">All message properties are strings.</span></span> <span data-ttu-id="9ce66-179">Les propriétés système, comme décrit dans le [guide du développeur][lnk-devguide-messaging-format], ne sont actuellement pas disponibles pour utilisation dans les requêtes.</span><span class="sxs-lookup"><span data-stu-id="9ce66-179">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="9ce66-180">Par exemple, si vous utilisez une propriété `messageType`, vous souhaiterez peut-être acheminer toutes les données de télémétrie vers un point de terminaison et toutes les alertes vers un autre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="9ce66-180">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="9ce66-181">Vous pouvez écrire l’expression suivante pour acheminer les données de télémétrie :</span><span class="sxs-lookup"><span data-stu-id="9ce66-181">You can write the following expression to route the telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="9ce66-182">Et l’expression suivante pour acheminer les messages d’alerte :</span><span class="sxs-lookup"><span data-stu-id="9ce66-182">And the following expression to route the alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="9ce66-183">Les fonctions et expressions booléennes sont également prises en charge.</span><span class="sxs-lookup"><span data-stu-id="9ce66-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="9ce66-184">Cette fonctionnalité vous permet de faire la distinction entre les niveaux de gravité, par exemple :</span><span class="sxs-lookup"><span data-stu-id="9ce66-184">This feature enables you to distinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="9ce66-185">Reportez-vous à la section [Expression et conditions][lnk-query-expressions] pour obtenir la liste complète des fonctions et opérateurs pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9ce66-185">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="9ce66-186">Routage sur les corps de message</span><span class="sxs-lookup"><span data-stu-id="9ce66-186">Routing on message bodies</span></span>

<span data-ttu-id="9ce66-187">IoT Hub peut effectuer le routage en fonction du contenu du corps du message seulement si le corps du message se présente sous un format JSON adéquat encodé en UTF-8, UTF-16 ou UTF-32.</span><span class="sxs-lookup"><span data-stu-id="9ce66-187">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="9ce66-188">Pour qu’IoT Hub puisse acheminer le message en fonction du contenu du corps, vous devez définir le type de contenu du message sur `application/json` et l’encodage du contenu sur l’un des encodages UTF pris en charge dans les en-têtes de message.</span><span class="sxs-lookup"><span data-stu-id="9ce66-188">You must set the content type of the message to `application/json` and the content encoding to one of the supported UTF encodings in the message headers to allow IoT Hub to route the message based on the body contents.</span></span> <span data-ttu-id="9ce66-189">Si un des en-têtes n’est pas spécifié, IoT Hub n’évalue aucune expression de requête impliquant le corps de message.</span><span class="sxs-lookup"><span data-stu-id="9ce66-189">If either of the headers is not specified, IoT Hub will not attempt to evaluate any query expression involving the body against the message.</span></span> <span data-ttu-id="9ce66-190">Si votre message n’est pas un message JSON ou que le message ne spécifie pas le type de contenu et l’encodage du contenu, vous pouvez toujours utiliser le routage des messages pour acheminer le message en fonction des en-têtes de message.</span><span class="sxs-lookup"><span data-stu-id="9ce66-190">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you may still use message routing to route the message based on the message headers.</span></span>

<span data-ttu-id="9ce66-191">Vous pouvez utiliser `$body` dans l’expression de requête pour acheminer le message.</span><span class="sxs-lookup"><span data-stu-id="9ce66-191">You can use `$body` in the query expression to route the message.</span></span> <span data-ttu-id="9ce66-192">Vous pouvez utiliser une référence de corps simple, une référence de tableau de corps ou plusieurs références de corps dans l’expression de requête.</span><span class="sxs-lookup"><span data-stu-id="9ce66-192">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span></span> <span data-ttu-id="9ce66-193">Votre expression de requête peut également combiner une référence de corps avec une référence d’en-tête de message.</span><span class="sxs-lookup"><span data-stu-id="9ce66-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="9ce66-194">Par exemple, toutes les expressions de requête suivantes sont valides :</span><span class="sxs-lookup"><span data-stu-id="9ce66-194">For example, the following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="9ce66-195">Principes de base d’une requête IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9ce66-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="9ce66-196">Chaque requête IoT Hub se compose de clauses SELECT et FROM et, en option, de clauses WHERE et GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="9ce66-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="9ce66-197">Chaque requête est exécutée sur un regroupement de documents JSON, par exemple des jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="9ce66-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="9ce66-198">La clause FROM indique le regroupement de documents sur lequel elle doit être itérée (**devices** ou **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="9ce66-198">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="9ce66-199">Ensuite, le filtre dans la clause WHERE est appliqué.</span><span class="sxs-lookup"><span data-stu-id="9ce66-199">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="9ce66-200">Avec les agrégations, les résultats de cette étape sont regroupés comme spécifié dans la clause GROUP BY, puis, pour chaque groupe, une ligne est générée comme spécifié dans la clause SELECT.</span><span class="sxs-lookup"><span data-stu-id="9ce66-200">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="9ce66-201">Clause FROM</span><span class="sxs-lookup"><span data-stu-id="9ce66-201">FROM clause</span></span>
<span data-ttu-id="9ce66-202">La clause **FROM <from_specification>** ne peut supposer que deux valeurs : **FROM devices** pour interroger les jumeaux d’appareil ou **FROM devices.jobs** pour interroger les détails de travaux par appareil.</span><span class="sxs-lookup"><span data-stu-id="9ce66-202">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="9ce66-203">Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="9ce66-203">WHERE clause</span></span>
<span data-ttu-id="9ce66-204">La clause **WHERE <filter_condition>** est facultative.</span><span class="sxs-lookup"><span data-stu-id="9ce66-204">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="9ce66-205">Elle indique une ou plusieurs conditions que les documents JSON du regroupement FROM doivent remplir pour être inclus dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="9ce66-205">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="9ce66-206">Pour être inclus dans le résultat, chaque document JSON doit évaluer les conditions spécifiées comme « true ».</span><span class="sxs-lookup"><span data-stu-id="9ce66-206">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="9ce66-207">Les conditions autorisées sont décrites dans la section [Expressions et conditions][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="9ce66-207">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="9ce66-208">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="9ce66-208">SELECT clause</span></span>
<span data-ttu-id="9ce66-209">La clause SELECT (**SELECT <select_list>**) est obligatoire. Elle spécifie les valeurs qui sont récupérées de la requête.</span><span class="sxs-lookup"><span data-stu-id="9ce66-209">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="9ce66-210">Elle spécifie les valeurs JSON à utiliser pour générer de nouveaux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="9ce66-210">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="9ce66-211">Pour chaque élément du sous-ensemble filtré (et éventuellement groupé) du regroupement FROM, la phase de projection génère un nouvel objet JSON, construit avec les valeurs spécifiées dans la clause SELECT.</span><span class="sxs-lookup"><span data-stu-id="9ce66-211">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="9ce66-212">La grammaire de la clause SELECT est la suivante :</span><span class="sxs-lookup"><span data-stu-id="9ce66-212">Following is the grammar of the SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="9ce66-213">où **attribute_name** fait référence à n’importe quelle propriété du document JSON dans le regroupement FROM.</span><span class="sxs-lookup"><span data-stu-id="9ce66-213">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="9ce66-214">Vous trouverez des exemples de clauses SELECT dans la section [Bien démarrer avec les requêtes de jumeau d’appareil][lnk-query-getstarted].</span><span class="sxs-lookup"><span data-stu-id="9ce66-214">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="9ce66-215">Actuellement, les clauses de sélection autres que **SELECT\*** sont prises en charge uniquement dans les requêtes d’agrégation sur des jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="9ce66-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="9ce66-216">Clause GROUP BY</span><span class="sxs-lookup"><span data-stu-id="9ce66-216">GROUP BY clause</span></span>
<span data-ttu-id="9ce66-217">La clause **GROUP BY <group_specification>** est une étape facultative qui peut être exécutée après le filtre spécifié dans la clause WHERE, et avant la projection spécifiée dans la clause SELECT.</span><span class="sxs-lookup"><span data-stu-id="9ce66-217">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="9ce66-218">Elle groupe des documents en fonction de la valeur d’un attribut.</span><span class="sxs-lookup"><span data-stu-id="9ce66-218">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="9ce66-219">Ces groupes sont utilisés pour générer des valeurs agrégées comme spécifié dans la clause SELECT.</span><span class="sxs-lookup"><span data-stu-id="9ce66-219">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="9ce66-220">Voici un exemple de requête utilisant la clause GROUP BY :</span><span class="sxs-lookup"><span data-stu-id="9ce66-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="9ce66-221">La syntaxe formelle de la clause GROUP BY est la suivante :</span><span class="sxs-lookup"><span data-stu-id="9ce66-221">The formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="9ce66-222">où **attribute_name** fait référence à n’importe quelle propriété du document JSON dans le regroupement FROM.</span><span class="sxs-lookup"><span data-stu-id="9ce66-222">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="9ce66-223">Actuellement, la clause GROUP BY est prise en charge uniquement lors de l’interrogation de jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="9ce66-223">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="9ce66-224">Expressions et conditions</span><span class="sxs-lookup"><span data-stu-id="9ce66-224">Expressions and conditions</span></span>
<span data-ttu-id="9ce66-225">À un niveau élevé, une *expression* :</span><span class="sxs-lookup"><span data-stu-id="9ce66-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="9ce66-226">prend la valeur d’une instance d’un type JSON (par exemple, Boolean, number, string, array ou object) ;</span><span class="sxs-lookup"><span data-stu-id="9ce66-226">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="9ce66-227">est définie en manipulant des données provenant du document JSON de l’appareil et des constantes à l’aide de fonctions et d’opérateurs intégrés.</span><span class="sxs-lookup"><span data-stu-id="9ce66-227">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="9ce66-228">Les *Conditions* sont des expressions qui correspondent à une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="9ce66-228">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="9ce66-229">Toute constante autre que le booléen **true** est considérée comme ayant la valeur **false** (y compris **null**, **undefined**, toute instance d’objet ou de tableau, toute chaîne et clairement le booléen **false**).</span><span class="sxs-lookup"><span data-stu-id="9ce66-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span></span>

<span data-ttu-id="9ce66-230">La syntaxe des expressions est la suivante :</span><span class="sxs-lookup"><span data-stu-id="9ce66-230">The syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="9ce66-231">où :</span><span class="sxs-lookup"><span data-stu-id="9ce66-231">where:</span></span>

| <span data-ttu-id="9ce66-232">Symbole</span><span class="sxs-lookup"><span data-stu-id="9ce66-232">Symbol</span></span> | <span data-ttu-id="9ce66-233">Définition</span><span class="sxs-lookup"><span data-stu-id="9ce66-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="9ce66-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="9ce66-234">attribute_name</span></span> | <span data-ttu-id="9ce66-235">Toute propriété du document JSON dans le regroupement **FROM**.</span><span class="sxs-lookup"><span data-stu-id="9ce66-235">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="9ce66-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="9ce66-236">binary_operator</span></span> | <span data-ttu-id="9ce66-237">Tout opérateur binaire répertorié dans la section [Operators](#operators).</span><span class="sxs-lookup"><span data-stu-id="9ce66-237">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="9ce66-238">function_name</span><span class="sxs-lookup"><span data-stu-id="9ce66-238">function_name</span></span>| <span data-ttu-id="9ce66-239">Toutes les fonctions répertoriées dans la section [Fonctions](#functions).</span><span class="sxs-lookup"><span data-stu-id="9ce66-239">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="9ce66-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="9ce66-240">decimal_literal</span></span> |<span data-ttu-id="9ce66-241">Variable exprimée en notation décimale.</span><span class="sxs-lookup"><span data-stu-id="9ce66-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="9ce66-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="9ce66-242">hexadecimal_literal</span></span> |<span data-ttu-id="9ce66-243">Nombre exprimé par la chaîne « 0x » suivi d’une chaîne de chiffres hexadécimaux.</span><span class="sxs-lookup"><span data-stu-id="9ce66-243">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="9ce66-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="9ce66-244">string_literal</span></span> |<span data-ttu-id="9ce66-245">Les littéraux de chaîne sont des chaînes Unicode représentées par une séquence de zéro ou plusieurs caractères Unicode ou séquences d’échappement.</span><span class="sxs-lookup"><span data-stu-id="9ce66-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="9ce66-246">Les littéraux de chaîne sont placés entre guillemets simples (apostrophes, ’) ou guillemets doubles (").</span><span class="sxs-lookup"><span data-stu-id="9ce66-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="9ce66-247">Échappements autorisés : `\'`, `\"`, `\\`, `\uXXXX` pour les caractères Unicode définis par 4 chiffres hexadécimaux.</span><span class="sxs-lookup"><span data-stu-id="9ce66-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="9ce66-248">Opérateurs</span><span class="sxs-lookup"><span data-stu-id="9ce66-248">Operators</span></span>
<span data-ttu-id="9ce66-249">Les opérateurs suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="9ce66-249">The following operators are supported:</span></span>

| <span data-ttu-id="9ce66-250">Famille</span><span class="sxs-lookup"><span data-stu-id="9ce66-250">Family</span></span> | <span data-ttu-id="9ce66-251">Opérateurs</span><span class="sxs-lookup"><span data-stu-id="9ce66-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="9ce66-252">Opérateurs arithmétiques</span><span class="sxs-lookup"><span data-stu-id="9ce66-252">Arithmetic</span></span> |<span data-ttu-id="9ce66-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="9ce66-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="9ce66-254">Opérateurs logiques</span><span class="sxs-lookup"><span data-stu-id="9ce66-254">Logical</span></span> |<span data-ttu-id="9ce66-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="9ce66-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="9ce66-256">Opérateurs de comparaison</span><span class="sxs-lookup"><span data-stu-id="9ce66-256">Comparison</span></span> |<span data-ttu-id="9ce66-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="9ce66-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="9ce66-258">Fonctions</span><span class="sxs-lookup"><span data-stu-id="9ce66-258">Functions</span></span>
<span data-ttu-id="9ce66-259">Lors des requêtes de jumeaux ou de travaux, la seule fonction prise en charge est :</span><span class="sxs-lookup"><span data-stu-id="9ce66-259">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="9ce66-260">Fonction</span><span class="sxs-lookup"><span data-stu-id="9ce66-260">Function</span></span> | <span data-ttu-id="9ce66-261">Description</span><span class="sxs-lookup"><span data-stu-id="9ce66-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9ce66-262">IS_DEFINED(property)</span><span class="sxs-lookup"><span data-stu-id="9ce66-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="9ce66-263">Retourne une valeur booléenne indiquant si une valeur a été attribuée à la propriété (dont `null`).</span><span class="sxs-lookup"><span data-stu-id="9ce66-263">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="9ce66-264">Dans les conditions d’itinéraire, les fonctions mathématiques suivantes sont prises en charge :</span><span class="sxs-lookup"><span data-stu-id="9ce66-264">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="9ce66-265">Fonction</span><span class="sxs-lookup"><span data-stu-id="9ce66-265">Function</span></span> | <span data-ttu-id="9ce66-266">Description</span><span class="sxs-lookup"><span data-stu-id="9ce66-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9ce66-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-267">ABS(x)</span></span> | <span data-ttu-id="9ce66-268">Retourne la valeur (positive) absolue de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9ce66-268">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="9ce66-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-269">EXP(x)</span></span> | <span data-ttu-id="9ce66-270">Retourne la valeur exponentielle de l'expression numérique spécifiée (e^x).</span><span class="sxs-lookup"><span data-stu-id="9ce66-270">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="9ce66-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="9ce66-271">POWER(x,y)</span></span> | <span data-ttu-id="9ce66-272">Retourne la valeur de l’expression spécifiée élevée à la puissance spécifiée (x^y).</span><span class="sxs-lookup"><span data-stu-id="9ce66-272">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="9ce66-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-273">SQUARE(x)</span></span> | <span data-ttu-id="9ce66-274">Retourne le carré de la valeur numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9ce66-274">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="9ce66-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-275">CEILING(x)</span></span> | <span data-ttu-id="9ce66-276">Retourne le plus petit nombre entier qui est supérieur ou égal à l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9ce66-276">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="9ce66-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-277">FLOOR(x)</span></span> | <span data-ttu-id="9ce66-278">Retourne le plus grand nombre entier qui est inférieur ou égal à l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9ce66-278">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="9ce66-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-279">SIGN(x)</span></span> | <span data-ttu-id="9ce66-280">Retourne le signe positif (+1), nul (0) ou négatif (-1) de l'expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9ce66-280">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="9ce66-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-281">SQRT(x)</span></span> | <span data-ttu-id="9ce66-282">Retourne le carré de la valeur numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9ce66-282">Returns the square of the specified numeric value.</span></span> |

<span data-ttu-id="9ce66-283">Dans les conditions d’itinéraire, les fonctions de vérification et de conversion de type suivantes sont prises en charge :</span><span class="sxs-lookup"><span data-stu-id="9ce66-283">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="9ce66-284">Fonction</span><span class="sxs-lookup"><span data-stu-id="9ce66-284">Function</span></span> | <span data-ttu-id="9ce66-285">Description</span><span class="sxs-lookup"><span data-stu-id="9ce66-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9ce66-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="9ce66-286">AS_NUMBER</span></span> | <span data-ttu-id="9ce66-287">Convertit la chaîne d’entrée en nombre.</span><span class="sxs-lookup"><span data-stu-id="9ce66-287">Converts the input string to a number.</span></span> <span data-ttu-id="9ce66-288">`noop` si l’entrée est un nombre ; `Undefined` si la chaîne ne représente pas un nombre.</span><span class="sxs-lookup"><span data-stu-id="9ce66-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="9ce66-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="9ce66-289">IS_ARRAY</span></span> | <span data-ttu-id="9ce66-290">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type tableau.</span><span class="sxs-lookup"><span data-stu-id="9ce66-290">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="9ce66-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="9ce66-291">IS_BOOL</span></span> | <span data-ttu-id="9ce66-292">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type booléen.</span><span class="sxs-lookup"><span data-stu-id="9ce66-292">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="9ce66-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="9ce66-293">IS_DEFINED</span></span> | <span data-ttu-id="9ce66-294">Retourne une valeur booléenne indiquant si une valeur a été attribuée à la propriété.</span><span class="sxs-lookup"><span data-stu-id="9ce66-294">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="9ce66-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="9ce66-295">IS_NULL</span></span> | <span data-ttu-id="9ce66-296">Retourne une valeur booléenne indiquant si l’expression spécifiée est de type null.</span><span class="sxs-lookup"><span data-stu-id="9ce66-296">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="9ce66-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="9ce66-297">IS_NUMBER</span></span> | <span data-ttu-id="9ce66-298">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type nombre.</span><span class="sxs-lookup"><span data-stu-id="9ce66-298">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="9ce66-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="9ce66-299">IS_OBJECT</span></span> | <span data-ttu-id="9ce66-300">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type objet JSON.</span><span class="sxs-lookup"><span data-stu-id="9ce66-300">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="9ce66-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="9ce66-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="9ce66-302">Retourne une valeur booléenne indiquant si l’expression spécifiée est de type primitif (chaîne, booléen, numérique ou `null`).</span><span class="sxs-lookup"><span data-stu-id="9ce66-302">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="9ce66-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="9ce66-303">IS_STRING</span></span> | <span data-ttu-id="9ce66-304">Retourne une valeur booléenne indiquant si l’expression spécifiée est du type chaîne.</span><span class="sxs-lookup"><span data-stu-id="9ce66-304">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="9ce66-305">Dans les conditions d’itinéraire, les fonctions de chaîne suivantes sont prises en charge :</span><span class="sxs-lookup"><span data-stu-id="9ce66-305">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="9ce66-306">Fonction</span><span class="sxs-lookup"><span data-stu-id="9ce66-306">Function</span></span> | <span data-ttu-id="9ce66-307">Description</span><span class="sxs-lookup"><span data-stu-id="9ce66-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9ce66-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="9ce66-308">CONCAT(x, …)</span></span> | <span data-ttu-id="9ce66-309">Retourne une chaîne qui est le résultat de la concaténation d’au moins deux valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="9ce66-309">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="9ce66-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-310">LENGTH(x)</span></span> | <span data-ttu-id="9ce66-311">Retourne le nombre de caractères de l’expression de chaîne spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9ce66-311">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="9ce66-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-312">LOWER(x)</span></span> | <span data-ttu-id="9ce66-313">Retourne une expression de chaîne après la conversion des caractères majuscules en caractères minuscules.</span><span class="sxs-lookup"><span data-stu-id="9ce66-313">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="9ce66-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="9ce66-314">UPPER(x)</span></span> | <span data-ttu-id="9ce66-315">Retourne une expression de chaîne après la conversion des caractères minuscules en caractères majuscules.</span><span class="sxs-lookup"><span data-stu-id="9ce66-315">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="9ce66-316">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="9ce66-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="9ce66-317">Renvoie une partie d’une expression de chaîne commençant à la position de caractère spécifiée (avec base zéro) et se poursuit jusqu'à la longueur spécifiée ou à la fin de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="9ce66-317">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="9ce66-318">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="9ce66-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="9ce66-319">Retourne la position de départ de la première occurrence de la seconde expression de chaîne dans la première expression de chaîne spécifiée, ou -1 si la chaîne est introuvable.</span><span class="sxs-lookup"><span data-stu-id="9ce66-319">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="9ce66-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="9ce66-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="9ce66-321">Retourne une valeur booléenne indiquant si la première expression de chaîne commence par la seconde.</span><span class="sxs-lookup"><span data-stu-id="9ce66-321">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="9ce66-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="9ce66-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="9ce66-323">Retourne une valeur booléenne indiquant si la première expression de chaîne se termine par la seconde.</span><span class="sxs-lookup"><span data-stu-id="9ce66-323">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="9ce66-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="9ce66-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="9ce66-325">Retourne une valeur booléenne indiquant si la première expression de chaîne contient la seconde.</span><span class="sxs-lookup"><span data-stu-id="9ce66-325">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9ce66-326">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ce66-326">Next steps</span></span>
<span data-ttu-id="9ce66-327">Découvrez comment exécuter des requêtes dans vos applications à l’aide des [Kits de développement logiciel (SDK) Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="9ce66-327">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
