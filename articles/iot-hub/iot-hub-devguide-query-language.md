---
title: "aaaUnderstand hello langage de requête Azure IoT Hub | Documents Microsoft"
description: "Guide du développeur - description du langage de requête de type SQL IoT Hub hello utilisée tooretrieve informations jumeaux de périphérique et les travaux à partir de votre hub IoT."
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
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="0b1a0-103">Référence - Langage de requête IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages</span><span class="sxs-lookup"><span data-stu-id="0b1a0-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="0b1a0-104">IoT Hub fournit un puissant langage de type SQL des informations de tooretrieve concernant [jumeaux de périphérique] [ lnk-twins] et [travaux][lnk-jobs]et [routage des messages][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="0b1a0-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="0b1a0-105">Cet article présente les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-105">This article presents:</span></span>

* <span data-ttu-id="0b1a0-106">Une introduction toohello principales fonctionnalités de langage de requête IoT Hub, de hello et</span><span class="sxs-lookup"><span data-stu-id="0b1a0-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="0b1a0-107">Hello description détaillée du langage de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="0b1a0-108">Bien démarrer avec les requêtes de jumeau d’appareil</span><span class="sxs-lookup"><span data-stu-id="0b1a0-108">Get started with device twin queries</span></span>
<span data-ttu-id="0b1a0-109">Des [jumeaux d’appareil][lnk-twins] peuvent contenir des objets JSON arbitraires tels que des balises (tags) et des propriétés.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="0b1a0-110">IoT Hub vous permet de jumeaux de périphérique tooquery en tant qu’un seul document JSON contenant toutes les informations de périphérique double.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="0b1a0-111">Supposons, par exemple, que vos jumeaux de périphérique de hub IoT ont hello suivant la structure :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

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

<span data-ttu-id="0b1a0-112">IoT Hub expose jumeaux de périphérique hello en tant que document collection appelée **périphériques**.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="0b1a0-113">Par conséquent, hello suivant la requête récupère définition hello de jumeaux du périphérique :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="0b1a0-114">Les kits [Azure IoT SDK][lnk-hub-sdks] prennent en charge la pagination des résultats volumineux.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="0b1a0-115">IoT Hub permet jumeaux de périphérique tooretrieve filtrage avec des conditions arbitraires.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="0b1a0-116">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="0b1a0-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="0b1a0-117">Récupère hello jumeaux de périphérique avec hello **location.region** ensemble trop de balises**US**.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="0b1a0-118">Les opérateurs booléens et les comparaisons arithmétiques sont également pris en charge, par exemple,</span><span class="sxs-lookup"><span data-stu-id="0b1a0-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="0b1a0-119">Récupère tous les jumeaux périphérique situé dans hello nous configuré toosend télémétrie moins souvent que toutes les minutes.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="0b1a0-120">Pour des raisons pratiques, il est également possible toouse les constantes de matrice avec hello **IN** et **NDANS** (pas dans) les opérateurs.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="0b1a0-121">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="0b1a0-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="0b1a0-122">récupère tous les jumeaux d’appareil ayant signalé une connectivité Wi-Fi ou câblée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="0b1a0-123">Il est souvent nécessaire tooidentify tous les jumeaux de périphérique qui contiennent une propriété spécifique.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="0b1a0-124">IoT Hub prend en charge la fonction hello `is_defined()` à cet effet.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="0b1a0-125">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="0b1a0-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="0b1a0-126">récupérer tous les jumeaux de périphérique qui définissent hello `connectivity` a signalé de propriété.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="0b1a0-127">Consultez toohello [clause WHERE] [ lnk-query-where] section de référence complète de hello Hello des fonctionnalités de filtre.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="0b1a0-128">Le regroupement et les agrégations sont également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="0b1a0-129">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="0b1a0-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="0b1a0-130">Retourne le nombre hello de périphériques de hello dans chaque état de configuration de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="0b1a0-131">Hello exemple précédent illustre une situation où trois unités signalé configuration réussie, deux sont toujours l’application configuration de hello, et un a signalé une erreur.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="0b1a0-132">Exemple en code C#</span><span class="sxs-lookup"><span data-stu-id="0b1a0-132">C# example</span></span>
<span data-ttu-id="0b1a0-133">fonctionnalités de requête Hello sont exposée par hello [SDK du service C#] [ lnk-hub-sdks] Bonjour **RegistryManager** classe.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="0b1a0-134">Voici un exemple de requête simple :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="0b1a0-135">Notez comment hello **requête** objet est instancié avec une taille de page (haut too1000), et puis plusieurs pages peuvent être récupérés en appelant hello **GetNextAsTwinAsync** méthodes plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="0b1a0-136">Notez que cet objet de requête hello expose plusieurs **suivant\***, selon l’option de la désérialisation de hello requis par la requête hello, tels que les objets périphériques double ou de travail, ou brut JSON toobe utilisé lors de l’utilisation de projections.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="0b1a0-137">Exemple de Node.js</span><span class="sxs-lookup"><span data-stu-id="0b1a0-137">Node.js example</span></span>
<span data-ttu-id="0b1a0-138">fonctionnalités de requête Hello sont exposée par hello [Azure IoT service SDK pour Node.js] [ lnk-hub-sdks] Bonjour **Registre** objet.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="0b1a0-139">Voici un exemple de requête simple :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
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

<span data-ttu-id="0b1a0-140">Notez comment hello **requête** objet est instancié avec une taille de page (haut too1000), et puis plusieurs pages peuvent être récupérés en appelant hello **nextAsTwin** méthodes plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="0b1a0-141">Notez que cet objet de requête hello expose plusieurs **suivant\***, selon l’option de la désérialisation de hello requis par la requête hello, tels que les objets périphériques double ou de travail, ou brut JSON toobe utilisé lors de l’utilisation de projections.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="0b1a0-142">Limites</span><span class="sxs-lookup"><span data-stu-id="0b1a0-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0b1a0-143">Résultats de la requête peuvent contenir quelques minutes de retard avec les valeurs les plus récentes en ce qui concerne toohello jumeaux de périphérique.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="0b1a0-144">Si vous interrogez jumeaux de périphérique par id, il est toujours préférable toouse hello récupérer les API de double de l’appareil, qui contient les valeurs les plus récentes hello et a plus la limitation limites toujours.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="0b1a0-145">Actuellement, les comparaisons ne sont prises en charge qu’entre types primitifs (aucun objet), par exemple `... WHERE properties.desired.config = properties.reported.config` est pris en charge uniquement si ces propriétés ont des valeurs primitives.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="0b1a0-146">Bien démarrer avec les requêtes de travaux</span><span class="sxs-lookup"><span data-stu-id="0b1a0-146">Get started with jobs queries</span></span>
<span data-ttu-id="0b1a0-147">[Travaux] [ lnk-jobs] fournissent un moyen tooexecute des opérations sur des ensembles de périphériques.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="0b1a0-148">Chaque double périphérique contient des informations de hello de travaux hello dont il fait partie d’une collection appelée **travaux**.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="0b1a0-149">Sous forme logique,</span><span class="sxs-lookup"><span data-stu-id="0b1a0-149">Logically,</span></span>

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

<span data-ttu-id="0b1a0-150">Actuellement, cette collection ne peut être interrogée comme **devices.jobs** Bonjour langage de requête IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b1a0-151">Actuellement, propriété des travaux hello n’est jamais retournée lors de l’interrogation jumeaux d’appareil (autrement dit, les requêtes qui contient « à partir d’appareils »).</span><span class="sxs-lookup"><span data-stu-id="0b1a0-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="0b1a0-152">Elle est uniquement accessible directement avec des requêtes utilisant `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="0b1a0-153">Par exemple, tooget tous les travaux (passées et planifiées) qui affectent un seul appareil, vous pouvez utiliser hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="0b1a0-154">Notez comment cette requête fournit l’état de spécifique au périphérique hello (et éventuellement réponse de la méthode directe hello) de chaque tâche retournée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="0b1a0-155">Il est également possible de toofilter avec des conditions booléennes arbitraires sur toutes les propriétés de l’objet Bonjour **devices.jobs** collection.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="0b1a0-156">Par exemple, hello requête suivante :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="0b1a0-157">récupère tous les travaux de mise à jour du jumeau de l’appareil **myDeviceId**, qui ont été créés après le mois de septembre 2016.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="0b1a0-158">Il est également des résultats de chaque appareil hello tooretrieve possibles d’une tâche unique.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="0b1a0-159">Limites</span><span class="sxs-lookup"><span data-stu-id="0b1a0-159">Limitations</span></span>
<span data-ttu-id="0b1a0-160">Actuellement, les requêtes sur **devices.jobs** ne prennent pas en charge :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="0b1a0-161">Les projections, par conséquent seul `SELECT *` est possible.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="0b1a0-162">Conditions qui font référence à double d’appareil toohello dans les propriétés de toojob d’addition (voir hello précédant la section).</span><span class="sxs-lookup"><span data-stu-id="0b1a0-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="0b1a0-163">L’exécution d’agrégations, par exemple, count, avg, group by.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="0b1a0-164">Bien démarrer avec les expressions de requête d’itinéraires de messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="0b1a0-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="0b1a0-165">À l’aide de [appareil-à-cloud itinéraires][lnk-devguide-messaging-routes], vous pouvez configurer IoT Hub toodispatch appareil-à-cloud messages toodifferent de points de terminaison basé sur des expressions évaluées par rapport à des messages individuels.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="0b1a0-166">itinéraire de Hello [condition] [ lnk-query-expressions] utilise hello même langage de requête IoT Hub en tant que les conditions dans les requêtes double et de travail.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="0b1a0-167">Conditions de routage sont évaluées sur le corps et en-têtes de message hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="0b1a0-168">Votre expression de requête de routage peut impliquer seulement des en-têtes de message, uniquement hello corps du message, ou les deux en-têtes de message et le corps du message.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="0b1a0-169">IoT Hub suppose un schéma spécifique pour les en-têtes de hello et de corps du message dans les messages d’ordre tooroute et hello les sections suivantes décrire ce qui est obligatoire pour l’itinéraire de tooproperly IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="0b1a0-170">Routage sur les en-têtes de message</span><span class="sxs-lookup"><span data-stu-id="0b1a0-170">Routing on message headers</span></span>

<span data-ttu-id="0b1a0-171">IoT Hub suppose hello suivant la représentation JSON d’en-têtes de message pour le routage des messages :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="0b1a0-172">Propriétés des messages système sont précédées de hello `'$'` symbole.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="0b1a0-173">Les propriétés de l’utilisateur sont toujours accessibles par leur nom.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="0b1a0-174">Si un nom de propriété utilisateur produit toocoincide avec une propriété système (tel que `$to`), propriété hello de l’utilisateur est récupérée avec hello `$to` expression.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="0b1a0-175">Vous pouvez toujours accéder à l’aide de crochets de la propriété du système hello `{}`: par exemple, vous pouvez utiliser l’expression de hello `{$to}` tooaccess hello propriété système `to`.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="0b1a0-176">Noms de propriété entre crochets récupèrent toujours le propriété système correspondante de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="0b1a0-177">N’oubliez pas que les noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="0b1a0-178">Toutes les propriétés de message sont des chaînes.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-178">All message properties are strings.</span></span> <span data-ttu-id="0b1a0-179">Propriétés du système, comme décrit dans hello [guide du développeur][lnk-devguide-messaging-format], ne sont pas actuellement disponible toouse dans les requêtes.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="0b1a0-180">Par exemple, si vous utilisez un `messageType` propriété, vous pourriez tooroute le point de terminaison de tooone toutes les données de télémétrie et le point de terminaison de tooanother toutes les alertes.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="0b1a0-181">Vous pouvez écrire hello suivant de télémétrie de hello tooroute expression :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="0b1a0-182">Et hello suivant des messages d’alerte hello tooroute expression :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="0b1a0-183">Les fonctions et expressions booléennes sont également prises en charge.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="0b1a0-184">Cette fonctionnalité permet de vous toodistinguish entre le niveau de gravité, par exemple :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="0b1a0-185">Consultez toohello [Expression et conditions] [ lnk-query-expressions] section pour la liste complète hello des fonctions et opérateurs pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="0b1a0-186">Routage sur les corps de message</span><span class="sxs-lookup"><span data-stu-id="0b1a0-186">Routing on message bodies</span></span>

<span data-ttu-id="0b1a0-187">IoT Hub peut uniquement acheminer basé sur le corps du message contenu si le corps du message hello est correctement formé JSON encodé en UTF-8, UTF-16 ou UTF-32.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="0b1a0-188">Vous devez définir les type de contenu hello de message de type hello trop`application/json` et tooone de codage contenu hello Hello pris en charge les encodages UTF dans tooallow d’en-têtes de message hello message de type hello IoT Hub tooroute basé sur le contenu du corps de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="0b1a0-189">Si un des en-têtes de hello n’est pas spécifié, IoT Hub tentera pas tooevaluate toute expression de requête impliquant des corps hello contre le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="0b1a0-190">Si votre message n’est pas un message JSON, ou si le message de type hello ne spécifie pas de type de contenu hello et l’encodage du contenu, vous pouvez toujours utiliser le message de type hello tooroute basée sur les en-têtes de message hello de routage des messages.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="0b1a0-191">Vous pouvez utiliser `$body` dans le message de type hello tooroute expression requête hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="0b1a0-192">Vous pouvez utiliser une référence simple corps, référence de tableau de corps ou plusieurs références de corps dans l’expression de requête hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="0b1a0-193">Votre expression de requête peut également combiner une référence de corps avec une référence d’en-tête de message.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="0b1a0-194">Par exemple, hello Voici toutes les expressions de requête valide :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="0b1a0-195">Principes de base d’une requête IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0b1a0-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="0b1a0-196">Chaque requête IoT Hub se compose de clauses SELECT et FROM et, en option, de clauses WHERE et GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="0b1a0-197">Chaque requête est exécutée sur un regroupement de documents JSON, par exemple des jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="0b1a0-198">clause FROM de Hello indique hello document collection toobe itéré sur (**périphériques** ou **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="0b1a0-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="0b1a0-199">Ensuite, hello filtre Bonjour où clause est appliquée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="0b1a0-200">Avec des agrégations, les résultats de hello de cette étape sont regroupés comme spécifié dans hello clause GROUP BY et, pour chaque groupe, une ligne est générée comme spécifié dans la clause SELECT de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="0b1a0-201">Clause FROM</span><span class="sxs-lookup"><span data-stu-id="0b1a0-201">FROM clause</span></span>
<span data-ttu-id="0b1a0-202">Hello **à partir de < from_specification >** clause peut supposer que deux valeurs : **à partir d’appareils**, tooquery jumeaux de périphérique, ou **de devices.jobs**, par périphérique du travail tooquery Détails.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="0b1a0-203">Clause WHERE</span><span class="sxs-lookup"><span data-stu-id="0b1a0-203">WHERE clause</span></span>
<span data-ttu-id="0b1a0-204">Hello **où < filter_condition >** clause est facultative.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="0b1a0-205">Elle spécifie une ou plusieurs des conditions que les documents JSON hello dans la collection de FROM hello doivent satisfaire toobe inclus en tant que partie du résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="0b1a0-206">N’importe quel document JSON doit évaluer hello spécifié conditions trop « true » toobe inclus dans le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="0b1a0-207">Hello autorisés sont décrites dans la section [Expressions et les conditions][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="0b1a0-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="0b1a0-208">Clause SELECT</span><span class="sxs-lookup"><span data-stu-id="0b1a0-208">SELECT clause</span></span>
<span data-ttu-id="0b1a0-209">clause SELECT de Hello (**sélectionnez < select_list >**) est obligatoire et spécifie que les valeurs sont récupérées à partir de la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="0b1a0-210">Il spécifie toobe de valeurs JSON hello utilisé toogenerate de nouveaux objets JSON.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="0b1a0-211">Pour chaque élément de hello sous-ensemble filtré (et éventuellement groupée) de collection de FROM hello, la phase de projection hello génère un nouvel objet JSON, construit avec les valeurs hello spécifiés dans la clause SELECT de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="0b1a0-212">Voici la grammaire hello de la clause SELECT de hello :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-212">Following is hello grammar of hello SELECT clause:</span></span>

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

<span data-ttu-id="0b1a0-213">où **attribute_name** fait référence de propriété tooany document JSON de hello dans la collection de FROM hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="0b1a0-214">Vous trouverez des exemples de clauses SELECT Bonjour [mise en route avec les requêtes de double périphérique] [ lnk-query-getstarted] section.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="0b1a0-215">Actuellement, les clauses de sélection autres que **SELECT\*** sont prises en charge uniquement dans les requêtes d’agrégation sur des jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="0b1a0-216">Clause GROUP BY</span><span class="sxs-lookup"><span data-stu-id="0b1a0-216">GROUP BY clause</span></span>
<span data-ttu-id="0b1a0-217">Hello **GROUP BY < group_specification >** clause est une étape facultative qui peut être exécutée une fois que le filtre de hello spécifié Bonjour clause WHERE et avant de projection hello spécifiée dans hello sélectionner.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="0b1a0-218">Il regroupe des documents en fonction de la valeur hello d’un attribut.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="0b1a0-219">Ces groupes sont utilisés toogenerate agrégée des valeurs comme spécifié dans la clause SELECT de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="0b1a0-220">Voici un exemple de requête utilisant la clause GROUP BY :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="0b1a0-221">une syntaxe de Hello pour GROUP BY est la suivante :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="0b1a0-222">où **attribute_name** fait référence de propriété tooany document JSON de hello dans la collection de FROM hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="0b1a0-223">Actuellement, clause GROUP BY hello est uniquement pris en charge lors de l’interrogation jumeaux de périphérique.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="0b1a0-224">Expressions et conditions</span><span class="sxs-lookup"><span data-stu-id="0b1a0-224">Expressions and conditions</span></span>
<span data-ttu-id="0b1a0-225">À un niveau élevé, une *expression* :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="0b1a0-226">Évalue l’instance tooan d’un type JSON (par exemple, les booléen, nombre, chaîne, tableau ou objet), et</span><span class="sxs-lookup"><span data-stu-id="0b1a0-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="0b1a0-227">Est défini par la manipulation de données provenant d’un document JSON de périphérique hello et constantes à l’aide des fonctions et opérateurs intégrés.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="0b1a0-228">*Conditions* sont des expressions qui évaluent tooa booléen.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="0b1a0-229">N’importe quelle autre qu’une valeur booléenne de constante **true** est considéré comme **false** (y compris **null**, **non défini**, n’importe quelle instance d’objet ou un tableau, toute chaîne et clairement hello booléen **false**).</span><span class="sxs-lookup"><span data-stu-id="0b1a0-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="0b1a0-230">syntaxe des expressions de Hello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-230">hello syntax for expressions is:</span></span>

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

<span data-ttu-id="0b1a0-231">où :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-231">where:</span></span>

| <span data-ttu-id="0b1a0-232">Symbole</span><span class="sxs-lookup"><span data-stu-id="0b1a0-232">Symbol</span></span> | <span data-ttu-id="0b1a0-233">Définition</span><span class="sxs-lookup"><span data-stu-id="0b1a0-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="0b1a0-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="0b1a0-234">attribute_name</span></span> | <span data-ttu-id="0b1a0-235">N’importe quelle propriété de document JSON de hello Bonjour **FROM** collection.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="0b1a0-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="0b1a0-236">binary_operator</span></span> | <span data-ttu-id="0b1a0-237">Tout opérateur binaire répertoriés dans hello [opérateurs](#operators) section.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="0b1a0-238">function_name</span><span class="sxs-lookup"><span data-stu-id="0b1a0-238">function_name</span></span>| <span data-ttu-id="0b1a0-239">Toutes les fonctions répertoriées dans hello [fonctions](#functions) section.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="0b1a0-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="0b1a0-240">decimal_literal</span></span> |<span data-ttu-id="0b1a0-241">Variable exprimée en notation décimale.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="0b1a0-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="0b1a0-242">hexadecimal_literal</span></span> |<span data-ttu-id="0b1a0-243">Un nombre exprimé par la chaîne de hello '0 x' suivi d’une chaîne de chiffres hexadécimaux.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="0b1a0-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="0b1a0-244">string_literal</span></span> |<span data-ttu-id="0b1a0-245">Les littéraux de chaîne sont des chaînes Unicode représentées par une séquence de zéro ou plusieurs caractères Unicode ou séquences d’échappement.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="0b1a0-246">Les littéraux de chaîne sont placés entre guillemets simples (apostrophes, ’) ou guillemets doubles (").</span><span class="sxs-lookup"><span data-stu-id="0b1a0-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="0b1a0-247">Échappements autorisés : `\'`, `\"`, `\\`, `\uXXXX` pour les caractères Unicode définis par 4 chiffres hexadécimaux.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="0b1a0-248">Operators</span><span class="sxs-lookup"><span data-stu-id="0b1a0-248">Operators</span></span>
<span data-ttu-id="0b1a0-249">Hello après les opérateurs est pris en charge :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-249">hello following operators are supported:</span></span>

| <span data-ttu-id="0b1a0-250">Famille</span><span class="sxs-lookup"><span data-stu-id="0b1a0-250">Family</span></span> | <span data-ttu-id="0b1a0-251">Opérateurs</span><span class="sxs-lookup"><span data-stu-id="0b1a0-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="0b1a0-252">Opérateurs arithmétiques</span><span class="sxs-lookup"><span data-stu-id="0b1a0-252">Arithmetic</span></span> |<span data-ttu-id="0b1a0-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="0b1a0-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="0b1a0-254">Opérateurs logiques</span><span class="sxs-lookup"><span data-stu-id="0b1a0-254">Logical</span></span> |<span data-ttu-id="0b1a0-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="0b1a0-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="0b1a0-256">Opérateurs de comparaison</span><span class="sxs-lookup"><span data-stu-id="0b1a0-256">Comparison</span></span> |<span data-ttu-id="0b1a0-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="0b1a0-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="0b1a0-258">Fonctions</span><span class="sxs-lookup"><span data-stu-id="0b1a0-258">Functions</span></span>
<span data-ttu-id="0b1a0-259">Lors de l’interrogation hello jumeaux et tâches de prise en charge uniquement la fonction est :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="0b1a0-260">Fonction</span><span class="sxs-lookup"><span data-stu-id="0b1a0-260">Function</span></span> | <span data-ttu-id="0b1a0-261">Description</span><span class="sxs-lookup"><span data-stu-id="0b1a0-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="0b1a0-262">IS_DEFINED(property)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="0b1a0-263">Retourne une valeur booléenne indiquant si une valeur a été assignée à la propriété de hello (y compris `null`).</span><span class="sxs-lookup"><span data-stu-id="0b1a0-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="0b1a0-264">Dans les conditions d’itinéraires, hello suivant des fonctions mathématiques est prises en charge :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="0b1a0-265">Fonction</span><span class="sxs-lookup"><span data-stu-id="0b1a0-265">Function</span></span> | <span data-ttu-id="0b1a0-266">Description</span><span class="sxs-lookup"><span data-stu-id="0b1a0-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="0b1a0-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-267">ABS(x)</span></span> | <span data-ttu-id="0b1a0-268">Retourne hello valeur absolue (positive) de hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="0b1a0-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-269">EXP(x)</span></span> | <span data-ttu-id="0b1a0-270">Retourne la valeur exponentielle hello Hello de l’expression numérique spécifiée (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="0b1a0-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="0b1a0-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-271">POWER(x,y)</span></span> | <span data-ttu-id="0b1a0-272">Retourne hello valeur Hello spécifié toohello de l’expression spécifiée d’alimentation (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="0b1a0-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="0b1a0-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-273">SQUARE(x)</span></span> | <span data-ttu-id="0b1a0-274">Hello retourne carrée hello la valeur numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="0b1a0-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-275">CEILING(x)</span></span> | <span data-ttu-id="0b1a0-276">Retourne hello plus petit entier supérieur à, ou être égal, hello expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="0b1a0-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-277">FLOOR(x)</span></span> | <span data-ttu-id="0b1a0-278">Retourne des hello plus grand entier inférieur ou égal toohello l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="0b1a0-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-279">SIGN(x)</span></span> | <span data-ttu-id="0b1a0-280">Retourne hello positif (+ 1), zéro (0), ou un signe négatif (-1) de hello de l’expression numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="0b1a0-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-281">SQRT(x)</span></span> | <span data-ttu-id="0b1a0-282">Hello retourne carrée hello la valeur numérique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="0b1a0-283">Dans les conditions d’itinéraires, hello suivant le type de vérification et de la conversion des fonctions est prises en charge :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="0b1a0-284">Fonction</span><span class="sxs-lookup"><span data-stu-id="0b1a0-284">Function</span></span> | <span data-ttu-id="0b1a0-285">Description</span><span class="sxs-lookup"><span data-stu-id="0b1a0-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="0b1a0-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="0b1a0-286">AS_NUMBER</span></span> | <span data-ttu-id="0b1a0-287">Convertit le nombre de tooa hello chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="0b1a0-288">`noop` si l’entrée est un nombre ; `Undefined` si la chaîne ne représente pas un nombre.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="0b1a0-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="0b1a0-289">IS_ARRAY</span></span> | <span data-ttu-id="0b1a0-290">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un tableau.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="0b1a0-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="0b1a0-291">IS_BOOL</span></span> | <span data-ttu-id="0b1a0-292">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="0b1a0-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="0b1a0-293">IS_DEFINED</span></span> | <span data-ttu-id="0b1a0-294">Retourne une valeur booléenne indiquant si une valeur a été assignée à la propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="0b1a0-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="0b1a0-295">IS_NULL</span></span> | <span data-ttu-id="0b1a0-296">Retourne une valeur booléenne indiquant si le type hello Hello spécifié expression est null.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="0b1a0-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="0b1a0-297">IS_NUMBER</span></span> | <span data-ttu-id="0b1a0-298">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un nombre.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="0b1a0-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0b1a0-299">IS_OBJECT</span></span> | <span data-ttu-id="0b1a0-300">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="0b1a0-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="0b1a0-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="0b1a0-302">Retourne une valeur booléenne indiquant si le type hello Hello spécifié expression est un type primitif (chaîne, booléen, numérique ou `null`).</span><span class="sxs-lookup"><span data-stu-id="0b1a0-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="0b1a0-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="0b1a0-303">IS_STRING</span></span> | <span data-ttu-id="0b1a0-304">Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est une chaîne.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="0b1a0-305">Dans les conditions d’itinéraires, hello suivant des fonctions de chaîne est pris en charge :</span><span class="sxs-lookup"><span data-stu-id="0b1a0-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="0b1a0-306">Fonction</span><span class="sxs-lookup"><span data-stu-id="0b1a0-306">Function</span></span> | <span data-ttu-id="0b1a0-307">Description</span><span class="sxs-lookup"><span data-stu-id="0b1a0-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="0b1a0-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-308">CONCAT(x, …)</span></span> | <span data-ttu-id="0b1a0-309">Retourne une chaîne qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="0b1a0-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-310">LENGTH(x)</span></span> | <span data-ttu-id="0b1a0-311">Retourne hello nombre de caractères de hello spécifié l’expression de chaîne.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="0b1a0-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-312">LOWER(x)</span></span> | <span data-ttu-id="0b1a0-313">Retourne une expression de chaîne après la conversion de toolowercase de données de caractères majuscules en caractères.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="0b1a0-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-314">UPPER(x)</span></span> | <span data-ttu-id="0b1a0-315">Retourne une expression de chaîne après la conversion de toouppercase de données de caractères en minuscules.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="0b1a0-316">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="0b1a0-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="0b1a0-317">Retourne dans une expression de chaîne commençant à hello spécifié le caractère de base zéro et continue toohello spécifié longueur, ou à la fin de toohello de chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="0b1a0-318">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="0b1a0-319">Retourne hello position de départ des hello première occurrence de hello deuxième expression de chaîne hello première expression de chaîne spécifiée, ou -1 si la chaîne de hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="0b1a0-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="0b1a0-321">Retourne une valeur booléenne indiquant si les première expression de chaîne hello commence par hello ensuite.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="0b1a0-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="0b1a0-323">Retourne une valeur booléenne indiquant si les première expression de chaîne hello se termine ensuite par hello.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="0b1a0-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="0b1a0-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="0b1a0-325">Retourne une valeur booléenne qui indique si le première expression de chaîne hello contient hello ensuite.</span><span class="sxs-lookup"><span data-stu-id="0b1a0-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0b1a0-326">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b1a0-326">Next steps</span></span>
<span data-ttu-id="0b1a0-327">Découvrez comment tooexecute les requêtes dans vos applications à l’aide de [kits de développement logiciel Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="0b1a0-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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
