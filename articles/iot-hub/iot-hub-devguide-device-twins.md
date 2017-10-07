---
title: "jumeaux de périphérique Azure IoT Hub aaaUnderstand | Documents Microsoft"
description: "Guide du développeur - utiliser le périphérique jumeaux toosynchronize les données de configuration et d’état entre IoT Hub et vos périphériques"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="09da0-103">Comprendre et utiliser les jumeaux d’appareil IoT Hub</span><span class="sxs-lookup"><span data-stu-id="09da0-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="09da0-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="09da0-104">Overview</span></span>
<span data-ttu-id="09da0-105">Les *jumeaux d’appareil* sont des documents JSON qui stockent des informations sur l’état des appareils (métadonnées, configurations et conditions).</span><span class="sxs-lookup"><span data-stu-id="09da0-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="09da0-106">IoT Hub conserve un double du périphérique pour chaque périphérique que vous vous connectez tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09da0-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="09da0-107">Cet article explique :</span><span class="sxs-lookup"><span data-stu-id="09da0-107">This article describes:</span></span>

* <span data-ttu-id="09da0-108">Hello structure de double de périphérique hello : *balises*, *souhaitée* et *signalé propriétés*, et</span><span class="sxs-lookup"><span data-stu-id="09da0-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="09da0-109">opérations de Hello que les applications de périphérique et back-end peut effectuer sur jumeaux de périphérique.</span><span class="sxs-lookup"><span data-stu-id="09da0-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="09da0-110">Actuellement, jumeaux de périphérique est accessibles uniquement à partir d’appareils qui se connectent tooIoT concentrateur à l’aide du protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="09da0-111">Consultez toohello [prise en charge MQTT] [ lnk-devguide-mqtt] article pour obtenir des instructions sur la façon de tooconvert existant appareil application toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="09da0-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="09da0-112">Lorsque toouse</span><span class="sxs-lookup"><span data-stu-id="09da0-112">When toouse</span></span>
<span data-ttu-id="09da0-113">Vous pouvez utiliser des représentations d’appareil pour répondre aux besoins suivants :</span><span class="sxs-lookup"><span data-stu-id="09da0-113">Use device twins to:</span></span>

* <span data-ttu-id="09da0-114">Stocker les métadonnées spécifiques au périphérique dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="09da0-115">Par exemple, hello emplacement de déploiement d’un distributeur automatique.</span><span class="sxs-lookup"><span data-stu-id="09da0-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="09da0-116">Signaler les informations d’état actuel, telles que les capacités disponibles et les conditions, à partir de votre application pour appareil,</span><span class="sxs-lookup"><span data-stu-id="09da0-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="09da0-117">Par exemple, un périphérique est connecté tooyour IoT hub over cellulaire ou Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="09da0-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="09da0-118">Synchroniser l’état hello de flux de travail de longue entre l’application et d’applications principal.</span><span class="sxs-lookup"><span data-stu-id="09da0-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="09da0-119">Par exemple, lors de la solution de hello fin spécifie hello nouvelle tooinstall de version du microprogramme et les rapports application hello périphériques hello différentes étapes du processus de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="09da0-120">Interroger les métadonnées, la configuration ou l’état de vos appareils</span><span class="sxs-lookup"><span data-stu-id="09da0-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="09da0-121">Consultez trop[des conseils de communication de périphérique dans le cloud] [ lnk-d2c-guidance] pour obtenir des conseils sur l’utilisation de propriétés signalées, messages appareil-à-cloud ou téléchargement du fichier.</span><span class="sxs-lookup"><span data-stu-id="09da0-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="09da0-122">Consultez trop[des conseils de communication Cloud-à-appareil] [ lnk-c2d-guidance] pour obtenir des conseils sur l’utilisation de propriétés souhaitées, des méthodes directes ou des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="09da0-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="09da0-123">Jumeaux d’appareil</span><span class="sxs-lookup"><span data-stu-id="09da0-123">Device twins</span></span>
<span data-ttu-id="09da0-124">Les jumeaux d’appareil stockent des informations relatives aux appareils, dont l’utilité est la suivante :</span><span class="sxs-lookup"><span data-stu-id="09da0-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="09da0-125">Se termine, puis dans l’appareil peut utiliser configuration et les conditions de périphérique toosynchronize.</span><span class="sxs-lookup"><span data-stu-id="09da0-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="09da0-126">Hello solution back-end tooquery et de cibler les opérations longues.</span><span class="sxs-lookup"><span data-stu-id="09da0-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="09da0-127">Hello de cycle de vie d’un double de l’appareil est lié toohello correspondant [identité d’appareil][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="09da0-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="09da0-128">Des jumeaux d’appareil sont implicitement créés et supprimés lors de la création ou de la suppression d’une identité d’appareil dans IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09da0-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="09da0-129">Un jumeau d’appareil est un document JSON incluant les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="09da0-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="09da0-130">**Tags** (balises).</span><span class="sxs-lookup"><span data-stu-id="09da0-130">**Tags**.</span></span> <span data-ttu-id="09da0-131">Une section du document JSON hello hello back-end solution peut lire et écrire dans.</span><span class="sxs-lookup"><span data-stu-id="09da0-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="09da0-132">Les balises ne sont pas visibles toodevice applications.</span><span class="sxs-lookup"><span data-stu-id="09da0-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="09da0-133">**Propriétés souhaitées (Desired)**.</span><span class="sxs-lookup"><span data-stu-id="09da0-133">**Desired properties**.</span></span> <span data-ttu-id="09da0-134">Utilisé avec la configuration de l’appareil toosynchronize propriétés déclarées ou conditions.</span><span class="sxs-lookup"><span data-stu-id="09da0-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="09da0-135">Propriétés souhaitées ne peuvent être définies par la solution hello précédent fin et peuvent être lues par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="09da0-136">application Hello peut également être notifiée en temps réel des modifications dans les propriétés de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="09da0-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="09da0-137">**Propriétés signalées (Reported)**.</span><span class="sxs-lookup"><span data-stu-id="09da0-137">**Reported properties**.</span></span> <span data-ttu-id="09da0-138">Utilisée avec la configuration de l’appareil toosynchronize propriétés souhaitées ou de conditions.</span><span class="sxs-lookup"><span data-stu-id="09da0-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="09da0-139">Les propriétés déclarées ne peut être définies par l’application d’appareil hello et pouvant être lus et interrogées par hello solution back-end.</span><span class="sxs-lookup"><span data-stu-id="09da0-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="09da0-140">En outre, racine hello du document JSON de hello appareil double contient les propriétés d’en lecture seule de hello d’identité appareil correspondant de hello stockées dans hello [Registre des identités][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="09da0-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="09da0-141">Hello, l’exemple suivant montre un document JSON de double appareil :</span><span class="sxs-lookup"><span data-stu-id="09da0-141">hello following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="09da0-142">Dans l’objet racine de hello, est des propriétés système hello et conteneur des objets pour `tags` et `reported` et `desired` propriétés.</span><span class="sxs-lookup"><span data-stu-id="09da0-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="09da0-143">Hello `properties` conteneur contient des éléments en lecture seule (`$metadata`, `$etag`, et `$version`) décrit dans hello [appareil double métadonnées] [ lnk-twin-metadata] et [ L’accès concurrentiel optimiste] [ lnk-concurrency] sections.</span><span class="sxs-lookup"><span data-stu-id="09da0-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="09da0-144">Exemple de propriété signalée (Reported)</span><span class="sxs-lookup"><span data-stu-id="09da0-144">Reported property example</span></span>
<span data-ttu-id="09da0-145">Dans l’exemple précédent de hello, double du périphérique hello contient un `batteryLevel` propriété qui est signalée par l’application d’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="09da0-146">Cette propriété rend possible tooquery et opérer sur les périphériques en fonction du niveau de batterie signalé dernier hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="09da0-147">Autres exemples incluent des fonctions de rapport appareil hello appareil app ou des options de connectivité.</span><span class="sxs-lookup"><span data-stu-id="09da0-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="09da0-148">Les propriétés déclarées simplifient les scénarios où hello solution back-end est intéressé par hello dernière connue de valeur d’une propriété.</span><span class="sxs-lookup"><span data-stu-id="09da0-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="09da0-149">Utilisez [messages appareil-à-cloud] [ lnk-d2c] si hello solution back-end a besoin de télémétrie de l’appareil tooprocess sous forme de hello de séquences d’événements horodaté, telles que de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="09da0-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="09da0-150">Exemple de propriété souhaitée</span><span class="sxs-lookup"><span data-stu-id="09da0-150">Desired property example</span></span>
<span data-ttu-id="09da0-151">Dans l’exemple précédent de hello, hello `telemetryConfig` double de l’appareil souhaité et propriétés déclarées sont utilisées par hello solution back-end hello configuration et appareils application toosynchronize hello télémétrie pour cet appareil.</span><span class="sxs-lookup"><span data-stu-id="09da0-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="09da0-152">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="09da0-152">For example:</span></span>

1. <span data-ttu-id="09da0-153">Hello solution back-end définit la propriété hello souhaitée avec la valeur de configuration hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="09da0-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="09da0-154">Voici la partie hello du document hello avec le jeu de propriétés hello souhaité :</span><span class="sxs-lookup"><span data-stu-id="09da0-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="09da0-155">application d’appareil Hello est avertie de modification hello immédiatement si connecté, ou à hello tout d’abord vous reconnecter.</span><span class="sxs-lookup"><span data-stu-id="09da0-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="09da0-156">Hello application puis signale hello mise à jour de configuration (ou une condition d’erreur à l’aide de hello `status` propriété).</span><span class="sxs-lookup"><span data-stu-id="09da0-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="09da0-157">Voici partie hello Hello signalé propriétés :</span><span class="sxs-lookup"><span data-stu-id="09da0-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="09da0-158">Hello solution back-end peut effectuer le suivi des résultats de l’opération de configuration hello hello sur plusieurs périphériques, par [interrogation] [ lnk-query] jumeaux de périphérique.</span><span class="sxs-lookup"><span data-stu-id="09da0-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="09da0-159">Hello des extraits de code précédents sont des exemples, optimisé pour une meilleure lisibilité, d’une façon tooencode une configuration de l’appareil et son état.</span><span class="sxs-lookup"><span data-stu-id="09da0-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="09da0-160">IoT Hub n’impose pas un schéma spécifique pour double du périphérique hello souhaitée et a signalé des propriétés dans jumeaux de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="09da0-161">Vous pouvez utiliser jumeaux toosynchronize opérations longues telles que des mises à jour du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="09da0-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="09da0-162">Pour plus d’informations sur comment toouse propriétés toosynchronize et suivre une opération longue pour les appareils, consultez [utilisation souhaitée propriétés tooconfigure dispositifs][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="09da0-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="09da0-163">Opérations principales</span><span class="sxs-lookup"><span data-stu-id="09da0-163">Back-end operations</span></span>
<span data-ttu-id="09da0-164">Hello solution back-end fonctionne sur le double de périphérique hello à l’aide de hello suivant des opérations atomiques, exposées via le protocole HTTP :</span><span class="sxs-lookup"><span data-stu-id="09da0-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="09da0-165">**Récupérer la représentation d’appareil par son id**. Cette opération renvoie le document de double hello périphérique, y compris les balises et que vous le souhaitez, est signalé et les propriétés système.</span><span class="sxs-lookup"><span data-stu-id="09da0-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="09da0-166">**Mettre à jour partiellement le jumeau d’appareil**.</span><span class="sxs-lookup"><span data-stu-id="09da0-166">**Partially update device twin**.</span></span> <span data-ttu-id="09da0-167">Cette opération permet de balises de hello hello solution back-end toopartially mise à jour les propriétés souhaitées dans un double de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="09da0-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="09da0-168">mise à jour partielle de Hello est exprimée sous forme de document JSON qui ajoute ou met à jour n’importe quelle propriété.</span><span class="sxs-lookup"><span data-stu-id="09da0-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="09da0-169">Propriétés définies trop`null` sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="09da0-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="09da0-170">Hello exemple suivant crée une nouvelle propriété souhaitée avec la valeur `{"newProperty": "newValue"}`, remplace la valeur existante de hello de `existingProperty` avec `"otherNewValue"`et supprime `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="09da0-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="09da0-171">Aucuns autres modifications ne sont apportées tooexisting souhaité propriétés ou les balises :</span><span class="sxs-lookup"><span data-stu-id="09da0-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="09da0-172">**Remplacer des propriétés souhaitées**.</span><span class="sxs-lookup"><span data-stu-id="09da0-172">**Replace desired properties**.</span></span> <span data-ttu-id="09da0-173">Cette toocompletely back-end de solution opération active hello remplacer toutes les propriétés de votre choisies et la remplacer par un nouveau document JSON pour `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="09da0-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="09da0-174">**Remplacer des Tags**.</span><span class="sxs-lookup"><span data-stu-id="09da0-174">**Replace tags**.</span></span> <span data-ttu-id="09da0-175">Cette toocompletely back-end de solution opération active hello remplacer toutes les balises existantes et les remplacer par un nouveau document JSON pour `tags`.</span><span class="sxs-lookup"><span data-stu-id="09da0-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="09da0-176">**Recevoir des notifications jumelles**.</span><span class="sxs-lookup"><span data-stu-id="09da0-176">**Receive twin notifications**.</span></span> <span data-ttu-id="09da0-177">Cette opération permet de hello solution back-end toobe informé double de hello est modifiée.</span><span class="sxs-lookup"><span data-stu-id="09da0-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="09da0-178">toodo, votre solution IoT doit donc toocreate un itinéraire et égal de Source de données tooset hello trop*twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="09da0-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="09da0-179">Par défaut, aucune notification jumelle n’est envoyée. Autrement dit, aucun itinéraire n’existe préalablement.</span><span class="sxs-lookup"><span data-stu-id="09da0-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="09da0-180">Si hello des taux de modification est trop élevé, ou pour d’autres raisons, telles que des défaillances internes, hello IoT Hub peut envoyer une notification qu’une seule qui contient toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="09da0-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="09da0-181">Par conséquent, si l’audit et la journalisation fiables de tous les états intermédiaires sont nécessaires pour votre application, il est toujours recommandé d’utiliser les messages D2C.</span><span class="sxs-lookup"><span data-stu-id="09da0-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="09da0-182">message de notification de double Hello inclut le corps et les propriétés.</span><span class="sxs-lookup"><span data-stu-id="09da0-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="09da0-183">Propriétés</span><span class="sxs-lookup"><span data-stu-id="09da0-183">Properties</span></span>

    | <span data-ttu-id="09da0-184">Name</span><span class="sxs-lookup"><span data-stu-id="09da0-184">Name</span></span> | <span data-ttu-id="09da0-185">Valeur</span><span class="sxs-lookup"><span data-stu-id="09da0-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="09da0-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="09da0-186">$content-type</span></span> | <span data-ttu-id="09da0-187">application/json</span><span class="sxs-lookup"><span data-stu-id="09da0-187">application/json</span></span> |
    <span data-ttu-id="09da0-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="09da0-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="09da0-189">Heure à laquelle la notification de hello a été envoyée</span><span class="sxs-lookup"><span data-stu-id="09da0-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="09da0-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="09da0-190">$iothub-message-source</span></span> | <span data-ttu-id="09da0-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="09da0-191">twinChangeEvents</span></span> |
    <span data-ttu-id="09da0-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="09da0-192">$content-encoding</span></span> | <span data-ttu-id="09da0-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="09da0-193">utf-8</span></span> |
    <span data-ttu-id="09da0-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="09da0-194">deviceId</span></span> | <span data-ttu-id="09da0-195">ID de périphérique de hello</span><span class="sxs-lookup"><span data-stu-id="09da0-195">Id of hello device</span></span> |
    <span data-ttu-id="09da0-196">hubName</span><span class="sxs-lookup"><span data-stu-id="09da0-196">hubName</span></span> | <span data-ttu-id="09da0-197">Nom de l’IoT Hub</span><span class="sxs-lookup"><span data-stu-id="09da0-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="09da0-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="09da0-198">operationTimestamp</span></span> | <span data-ttu-id="09da0-199">Horodatage [ISO8601] de l’opération</span><span class="sxs-lookup"><span data-stu-id="09da0-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="09da0-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="09da0-200">iothub-message-schema</span></span> | <span data-ttu-id="09da0-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="09da0-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="09da0-202">opType</span><span class="sxs-lookup"><span data-stu-id="09da0-202">opType</span></span> | <span data-ttu-id="09da0-203">« replaceTwin » ou « updateTwin »</span><span class="sxs-lookup"><span data-stu-id="09da0-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="09da0-204">Propriétés des messages système sont précédées de hello `'$'` symbole.</span><span class="sxs-lookup"><span data-stu-id="09da0-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="09da0-205">Corps</span><span class="sxs-lookup"><span data-stu-id="09da0-205">Body</span></span>
        
    <span data-ttu-id="09da0-206">Cette section inclut toutes les modifications de double hello dans un format JSON.</span><span class="sxs-lookup"><span data-stu-id="09da0-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="09da0-207">Elle utilise hello même format comme un correctif, avec différence de hello qu’elle peut contenir toutes les sections de double : balises, properties.reported, properties.desired et qu’il contient des éléments de hello « $metadata ».</span><span class="sxs-lookup"><span data-stu-id="09da0-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="09da0-208">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="09da0-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="09da0-209">Tous les hello prise en charge des opérations précédentes [d’accès concurrentiel optimiste] [ lnk-concurrency] et nécessitent hello **ServiceConnect** autorisation, tel que défini dans hello [sécurité ] [ lnk-security] l’article.</span><span class="sxs-lookup"><span data-stu-id="09da0-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="09da0-210">En outre les opérations toothese, solution de hello sauvegarder fin peut :</span><span class="sxs-lookup"><span data-stu-id="09da0-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="09da0-211">Requête jumeaux de périphérique hello à l’aide de hello type SQL [langage de requête IoT Hub][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="09da0-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="09da0-212">Effectuer des opérations sur les grands ensembles de jumeaux d’appareil à l’aide de [travaux][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="09da0-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="09da0-213">Opérations d’appareil</span><span class="sxs-lookup"><span data-stu-id="09da0-213">Device operations</span></span>
<span data-ttu-id="09da0-214">application d’appareil Hello opère sur double d’appareil hello à l’aide de hello suivant des opérations atomiques :</span><span class="sxs-lookup"><span data-stu-id="09da0-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="09da0-215">**Récupérer le jumeau d’appareil**.</span><span class="sxs-lookup"><span data-stu-id="09da0-215">**Retrieve device twin**.</span></span> <span data-ttu-id="09da0-216">Cette opération retourne le document de double hello appareil (y compris les balises et vous le souhaitez, signalée et les propriétés système) pour hello connecté actuellement le périphérique.</span><span class="sxs-lookup"><span data-stu-id="09da0-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="09da0-217">**Mettre à jour partiellement les propriétés signalées (Reported)**.</span><span class="sxs-lookup"><span data-stu-id="09da0-217">**Partially update reported properties**.</span></span> <span data-ttu-id="09da0-218">Cette opération active hello mise à jour partielle de hello a signalé des propriétés d’appareil actuellement connectée de hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="09da0-219">Cette hello d’utilise opération JSON même mettre à jour de format qui utilise retour de fin hello solution pour une mise à jour partielle de propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="09da0-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="09da0-220">**Observer les propriétés souhaitées (Desired)**.</span><span class="sxs-lookup"><span data-stu-id="09da0-220">**Observe desired properties**.</span></span> <span data-ttu-id="09da0-221">la possibilité de toobe averti des propriétés toohello souhaité de mises à jour lorsqu’elles surviennent, Hello un périphérique actuellement connecté.</span><span class="sxs-lookup"><span data-stu-id="09da0-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="09da0-222">Hello reçoit hello même formulaire de mise à jour (remplacement partiel ou complet) exécutée par hello solution back-end.</span><span class="sxs-lookup"><span data-stu-id="09da0-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="09da0-223">Tous les hello opérations précédentes nécessitent hello **DeviceConnect** autorisation, tel que défini dans hello [sécurité] [ lnk-security] l’article.</span><span class="sxs-lookup"><span data-stu-id="09da0-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="09da0-224">Hello [Azure IoT appareil kits de développement logiciel] [ lnk-sdks] rendre hello toouse facile à partir de nombreuses langues et plateformes, les opérations précédentes.</span><span class="sxs-lookup"><span data-stu-id="09da0-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="09da0-225">Vous trouverez plus d’informations sur les détails de hello de primitives IoT Hub pour la synchronisation de propriétés souhaitées dans [flux reconnexion de périphérique][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="09da0-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="09da0-226">Actuellement, jumeaux de périphérique est accessibles uniquement à partir d’appareils qui se connectent tooIoT concentrateur à l’aide du protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="09da0-227">Rubriques de référence :</span><span class="sxs-lookup"><span data-stu-id="09da0-227">Reference topics:</span></span>
<span data-ttu-id="09da0-228">Hello rubriques de référence suivantes vous fournissent plus d’informations sur tooyour IoT hub de contrôler l’accès.</span><span class="sxs-lookup"><span data-stu-id="09da0-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="09da0-229">Format des Tags et propriétés</span><span class="sxs-lookup"><span data-stu-id="09da0-229">Tags and properties format</span></span>
<span data-ttu-id="09da0-230">Balises, les propriétés souhaitées et signalées sont des objets JSON avec hello suivant restrictions :</span><span class="sxs-lookup"><span data-stu-id="09da0-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="09da0-231">Toutes les clés dans des objets JSON sont des chaînes UNICODE UTF-8 de 64 octets respectant la casse.</span><span class="sxs-lookup"><span data-stu-id="09da0-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="09da0-232">Les caractères autorisés excluent les caractères de contrôle UNICODE (segments C0 et C1), ainsi que `'.'`, `' '` et `'$'`.</span><span class="sxs-lookup"><span data-stu-id="09da0-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="09da0-233">Toutes les valeurs dans des objets JSON peuvent être de hello JSON types suivants : booléen, nombre, chaîne, objet.</span><span class="sxs-lookup"><span data-stu-id="09da0-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="09da0-234">Les tableaux ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="09da0-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="09da0-235">Tous les objets JSON dans les balises ainsi que dans les propriétés souhaitées et signalées, peuvent avoir une profondeur maximale de 5.</span><span class="sxs-lookup"><span data-stu-id="09da0-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="09da0-236">Par exemple, hello objet est valide :</span><span class="sxs-lookup"><span data-stu-id="09da0-236">For instance, hello following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="09da0-237">Aucune valeur de chaîne ne peut avoir une longueur supérieure à 512 octets.</span><span class="sxs-lookup"><span data-stu-id="09da0-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="09da0-238">Taille de jumeau d’appareil</span><span class="sxs-lookup"><span data-stu-id="09da0-238">Device twin size</span></span>
<span data-ttu-id="09da0-239">IoT Hub impose une limite de taille de 8 Ko sur les valeurs hello de `tags`, `properties/desired`, et `properties/reported`, à l’exclusion des éléments en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="09da0-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="09da0-240">Hello taille est calculée en comptant tous les caractères UNICODE contrôlent caractères (segments C0 et C1) et l’espace `' '` lorsqu’il apparaît en dehors d’une constante de chaîne.</span><span class="sxs-lookup"><span data-stu-id="09da0-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="09da0-241">IoT Hub rejette, avec une erreur, toutes les opérations qui augmentent taille hello de ces documents dépasse la limite de hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="09da0-242">Métadonnées de jumeau d’appareil</span><span class="sxs-lookup"><span data-stu-id="09da0-242">Device twin metadata</span></span>
<span data-ttu-id="09da0-243">IoT Hub conserve timestamp hello de hello dernière mise à jour pour chaque objet JSON en double de l’appareil souhaité et qu’il a signalé des propriétés.</span><span class="sxs-lookup"><span data-stu-id="09da0-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="09da0-244">Hello horodatages sont au format UTC et encodé dans hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="09da0-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="09da0-245">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="09da0-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="09da0-246">Ces informations sont conservées à chaque niveau (feuilles hello pas simplement de hello structure JSON) toopreserve mises à jour de supprimer des clés de l’objet.</span><span class="sxs-lookup"><span data-stu-id="09da0-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="09da0-247">Accès concurrentiel optimiste</span><span class="sxs-lookup"><span data-stu-id="09da0-247">Optimistic concurrency</span></span>
<span data-ttu-id="09da0-248">Les Tags ainsi que les propriétés souhaitées (Desired) et signalées (Reported) prennent en charge l’accès concurrentiel optimiste.</span><span class="sxs-lookup"><span data-stu-id="09da0-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="09da0-249">Balises ont un ETag, comme par [RFC7232], qui représente la représentation JSON de la balise hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="09da0-250">Vous pouvez utiliser les ETags dans les opérations de mise à jour conditionnelle à partir de la cohérence de tooensure hello solution back-end.</span><span class="sxs-lookup"><span data-stu-id="09da0-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="09da0-251">Double du périphérique souhaité et signalés propriétés ETag est inutile, mais ont un `$version` valeur est garantie toobe incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="09da0-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="09da0-252">Même tooan ETag, version de hello peut être utilisée par hello mise à jour de la cohérence de tooenforce tiers des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="09da0-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="09da0-253">Par exemple, une application de périphérique pour signalé propriété ou hello solution principale pour une propriété de votre choix.</span><span class="sxs-lookup"><span data-stu-id="09da0-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="09da0-254">Les versions sont également utiles lorsqu’un agent observation (par exemple, application de périphérique hello en observant les propriétés hello souhaité) devez rapprocher courses entre le résultat de hello d’une opération de récupération et une notification de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="09da0-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="09da0-255">Hello section [flux reconnexion de périphérique] [ lnk-reconnection] fournit plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="09da0-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="09da0-256">Flux de reconnexion d’appareil</span><span class="sxs-lookup"><span data-stu-id="09da0-256">Device reconnection flow</span></span>
<span data-ttu-id="09da0-257">IoT Hub ne conserve pas les notifications de mise à jour de propriétés souhaitées pour les appareils déconnectés.</span><span class="sxs-lookup"><span data-stu-id="09da0-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="09da0-258">Il en résulte qu’un périphérique qui se connecte doit récupérer hello complète souhaitée document des propriétés, dans toosubscribing d’addition pour les notifications de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="09da0-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="09da0-259">Étant donné le risque de hello de courses entre les notifications de mise à jour et de récupération complète, hello suit flux doit être assurée :</span><span class="sxs-lookup"><span data-stu-id="09da0-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="09da0-260">Application de l’appareil connecte tooan IoT hub.</span><span class="sxs-lookup"><span data-stu-id="09da0-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="09da0-261">L’application d’appareil s’abonne aux notifications de mise à jour des propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="09da0-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="09da0-262">Application d’appareil récupère hello complète pour le document pour les propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="09da0-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="09da0-263">application d’appareil Hello peut ignorer toutes les notifications avec `$version` inférieure ou égale à la version de hello de hello complète récupérées pour le document.</span><span class="sxs-lookup"><span data-stu-id="09da0-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="09da0-264">Cette approche est possible, car IoT Hub garantit que les numéros de version sont toujours incrémentiels.</span><span class="sxs-lookup"><span data-stu-id="09da0-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="09da0-265">Cette logique est déjà implémentée dans hello [Azure IoT appareil kits de développement logiciel][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="09da0-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="09da0-266">Cette description est utile uniquement si l’application hello ne peut pas utiliser une de l’appareil Azure IoT kits de développement logiciel et devez programmer interface MQTT de hello directement.</span><span class="sxs-lookup"><span data-stu-id="09da0-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="09da0-267">Matériel de référence supplémentaire</span><span class="sxs-lookup"><span data-stu-id="09da0-267">Additional reference material</span></span>
<span data-ttu-id="09da0-268">Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="09da0-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="09da0-269">Hello [points de terminaison IoT Hub] [ lnk-endpoints] hello décrit les différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.</span><span class="sxs-lookup"><span data-stu-id="09da0-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="09da0-270">Hello [limitation et les quotas] [ lnk-quotas] décrit les quotas hello qui s’appliquent toohello IoT Hub service hello limitation tooexpect de comportement lorsque vous utilisez le service de hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="09da0-271">Hello [SDK de périphérique et le service Azure IoT] [ lnk-sdks] article listes hello différents langage SDK, vous pouvez utiliser lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09da0-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="09da0-272">Hello [langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages] [ lnk-query] décrit le langage de requête IoT Hub vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux de hello .</span><span class="sxs-lookup"><span data-stu-id="09da0-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="09da0-273">Hello [prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] article fournit plus d’informations sur la prise en charge de IoT Hub pour le protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="09da0-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09da0-274">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09da0-274">Next steps</span></span>
<span data-ttu-id="09da0-275">Maintenant vous avez permis de découvrir jumeaux de périphérique, peut vous intéresser hello IoT Hub développeur guide rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="09da0-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="09da0-276">[Appeler une méthode directe sur un appareil][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="09da0-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="09da0-277">[Planifier des travaux sur plusieurs appareils][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="09da0-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="09da0-278">Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant les didacticiels IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="09da0-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="09da0-279">[Comment toouse hello double de l’appareil][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="09da0-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="09da0-280">[Comment toouse appareil à deux propriétés][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="09da0-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
