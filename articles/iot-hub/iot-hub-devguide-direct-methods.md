---
title: "Présentation des méthodes directes Azure IoT Hub | Microsoft Docs"
description: "Guide de développeur - Utiliser des méthodes directes pour appeler du code sur vos appareils à partir d’une application de service."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="53de7-103">Comprendre et appeler des méthodes directes à partir d’IoT Hub</span><span class="sxs-lookup"><span data-stu-id="53de7-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="53de7-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="53de7-104">Overview</span></span>
<span data-ttu-id="53de7-105">IoT Hub vous donne la possibilité d’appeler des méthodes directes sur des appareils à partir du cloud.</span><span class="sxs-lookup"><span data-stu-id="53de7-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="53de7-106">Les méthodes directes représentent une interaction de demande-réponse avec un appareil, similaire à un appel HTTP, dans la mesure où elles réussissent ou échouent immédiatement (après un délai d’attente spécifié par l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="53de7-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="53de7-107">Cela est utile pour les scénarios où la conduite à suivre immédiate diffère selon que l’appareil a ou non pu répondre, comme l’envoi d’un SMS d’activation à un appareil quand celui-ci est hors connexion (un SMS étant plus onéreux qu’un appel de méthode).</span><span class="sxs-lookup"><span data-stu-id="53de7-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="53de7-108">Chaque méthode d’appareil cible à un seul appareil.</span><span class="sxs-lookup"><span data-stu-id="53de7-108">Each device method targets a single device.</span></span> <span data-ttu-id="53de7-109">Les [travaux][lnk-devguide-jobs] offrent un moyen d’appeler des méthodes directes sur plusieurs appareils, et de planifier un appel de méthode pour des appareils déconnectés.</span><span class="sxs-lookup"><span data-stu-id="53de7-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="53de7-110">Toute personne disposant d’autorisations **Connexion de service** sur IoT Hub peut appeler une méthode sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="53de7-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="53de7-111">Quand utiliser</span><span class="sxs-lookup"><span data-stu-id="53de7-111">When to use</span></span>
<span data-ttu-id="53de7-112">Les méthodes directes suivent un modèle de requête-réponse et sont destinées aux communications qui nécessitent une confirmation immédiate de leur résultat, généralement le contrôle interactif de l’appareil, par exemple, pour activer un ventilateur.</span><span class="sxs-lookup"><span data-stu-id="53de7-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="53de7-113">En cas de doute entre l’utilisation des propriétés souhaitées des méthodes directes ou des messages cloud-à-appareil, voir [Instructions pour la communication appareil-à-cloud][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="53de7-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="53de7-114">Cycle de vie de méthode</span><span class="sxs-lookup"><span data-stu-id="53de7-114">Method lifecycle</span></span>
<span data-ttu-id="53de7-115">Les méthodes directes sont implémentées sur l’appareil et peuvent nécessiter de zéro à plusieurs entrées dans la charge utile pour s’instancier correctement.</span><span class="sxs-lookup"><span data-stu-id="53de7-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="53de7-116">Vous appelez une méthode directe via un URI côté service (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="53de7-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="53de7-117">Un appareil reçoit des méthodes directes via une rubrique MQTT spécifique de l’appareil (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="53de7-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="53de7-118">Nous pourrions prendre en charge des méthodes directes sur des protocoles réseau côté appareil supplémentaires à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="53de7-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="53de7-119">Lorsque vous appelez une méthode directe sur un appareil, les noms et valeurs de propriété peuvent contenir uniquement des caractères alphanumériques US-ASCII imprimables, à l’exception des caractères suivants : ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="53de7-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="53de7-120">Les méthodes directes sont synchrones et réussissent ou échouent à l’issue du délai d’expiration (par défaut, 30 secondes, extensible à 3 600 secondes).</span><span class="sxs-lookup"><span data-stu-id="53de7-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="53de7-121">Les méthodes directes sont utiles dans des scénarios interactifs où vous souhaitez qu’un appareil agisse si et seulement s’il est en ligne et reçoit des commandes, telles que l’allumage d’une lumière, en provenance d’un téléphone.</span><span class="sxs-lookup"><span data-stu-id="53de7-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="53de7-122">Dans ces scénarios, vous souhaitez constater immédiatement la réussite ou l’échec de la commande, de façon à ce que le service cloud puisse agir sur le résultat dès que possible.</span><span class="sxs-lookup"><span data-stu-id="53de7-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="53de7-123">L’appareil peut renvoyer un corps de message résultant de la méthode, mais il n’est pas obligatoire que la méthode procède de la sorte.</span><span class="sxs-lookup"><span data-stu-id="53de7-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="53de7-124">Il existe ni garantie de classement, ni sémantique de concurrence sur les appels de méthode.</span><span class="sxs-lookup"><span data-stu-id="53de7-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="53de7-125">Les méthodes directes sont exclusivement HTTP côté cloud, et exclusivement MQTT côté appareil.</span><span class="sxs-lookup"><span data-stu-id="53de7-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="53de7-126">La charge utile pour les requêtes et les réponses de méthode correspond à un document JSON d’une taille pouvant aller jusqu’à 8 Ko.</span><span class="sxs-lookup"><span data-stu-id="53de7-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="53de7-127">Rubriques de référence :</span><span class="sxs-lookup"><span data-stu-id="53de7-127">Reference topics:</span></span>
<span data-ttu-id="53de7-128">Les rubriques de référence suivantes vous fournissent des informations supplémentaires sur l’utilisation des méthodes directes.</span><span class="sxs-lookup"><span data-stu-id="53de7-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="53de7-129">Appeler une méthode directe à partir d’une application principale</span><span class="sxs-lookup"><span data-stu-id="53de7-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="53de7-130">Appel de méthode</span><span class="sxs-lookup"><span data-stu-id="53de7-130">Method invocation</span></span>
<span data-ttu-id="53de7-131">Les appels de méthode directe sur un appareil sont des appels HTTP qui comprennent les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="53de7-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="53de7-132">l’*URI* spécifique de l’appareil (`{iot hub}/twins/{device id}/methods/`) ;</span><span class="sxs-lookup"><span data-stu-id="53de7-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="53de7-133">la *méthode* POST ;</span><span class="sxs-lookup"><span data-stu-id="53de7-133">The POST *method*</span></span>
* <span data-ttu-id="53de7-134">des *en-têtes* contenant l’autorisation, l’ID de demande, le type de contenu et l’encodage du contenu ;</span><span class="sxs-lookup"><span data-stu-id="53de7-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="53de7-135">un *corps* JSON transparent au format suivant :</span><span class="sxs-lookup"><span data-stu-id="53de7-135">A transparent JSON *body* in the following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="53de7-136">Le délai d’attente est exprimé en secondes.</span><span class="sxs-lookup"><span data-stu-id="53de7-136">Timeout is in seconds.</span></span> <span data-ttu-id="53de7-137">Si le délai d’attente n’est pas défini, sa valeur par défaut est de 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="53de7-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="53de7-138">Réponse</span><span class="sxs-lookup"><span data-stu-id="53de7-138">Response</span></span>
<span data-ttu-id="53de7-139">L’application principale reçoit une réponse qui comprend les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="53de7-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="53de7-140">un *code d’état HTTP*, qui est utilisé pour des erreurs en provenance d’IoT Hub, dont l’erreur 404 pour les appareils non connectés ;</span><span class="sxs-lookup"><span data-stu-id="53de7-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="53de7-141">des *en-têtes* contenant l’ETag, l’ID de demande, le type de contenu et l’encodage du contenu ;</span><span class="sxs-lookup"><span data-stu-id="53de7-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="53de7-142">un *corps* JSON au format suivant :</span><span class="sxs-lookup"><span data-stu-id="53de7-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="53de7-143">Les propriétés `status` et `body` sont fournies par l’appareil et permettent de répondre avec le code d’état et/ou la description spécifiques de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="53de7-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="53de7-144">Gérer une méthode directe sur un appareil</span><span class="sxs-lookup"><span data-stu-id="53de7-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="53de7-145">Appel de méthode</span><span class="sxs-lookup"><span data-stu-id="53de7-145">Method invocation</span></span>
<span data-ttu-id="53de7-146">Les appareils reçoivent des demandes de méthode directe sur la rubrique MQTT : `$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="53de7-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="53de7-147">Le corps que l’appareil reçoit est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="53de7-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="53de7-148">Les demandes de méthode sont QoS 0.</span><span class="sxs-lookup"><span data-stu-id="53de7-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="53de7-149">Réponse</span><span class="sxs-lookup"><span data-stu-id="53de7-149">Response</span></span>
<span data-ttu-id="53de7-150">L’appareil envoie des réponses à `$iothub/methods/res/{status}/?$rid={request id}`, où :</span><span class="sxs-lookup"><span data-stu-id="53de7-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="53de7-151">La propriété `status` est l’état d’exécution de la méthode fourni par l’appareil.</span><span class="sxs-lookup"><span data-stu-id="53de7-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="53de7-152">La propriété `$rid`est l’ID de demande de l’appel de méthode reçu d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="53de7-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="53de7-153">Le corps est défini par l’appareil et peut être n’importe quel état.</span><span class="sxs-lookup"><span data-stu-id="53de7-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="53de7-154">Matériel de référence supplémentaire</span><span class="sxs-lookup"><span data-stu-id="53de7-154">Additional reference material</span></span>
<span data-ttu-id="53de7-155">Les autres rubriques de référence dans le Guide du développeur IoT Hub comprennent :</span><span class="sxs-lookup"><span data-stu-id="53de7-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="53de7-156">La rubrique [Points de terminaison IoT Hub][lnk-endpoints] décrit les différents points de terminaison que chaque IoT Hub expose pour les opérations d’exécution et de gestion.</span><span class="sxs-lookup"><span data-stu-id="53de7-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="53de7-157">La rubrique [Quotas et limitation][lnk-quotas] décrit les quotas appliqués au service IoT Hub, et le comportement de limitation auquel s’attendre en cas d’utilisation du service.</span><span class="sxs-lookup"><span data-stu-id="53de7-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="53de7-158">La section [Azure IoT device et service SDK][lnk-sdks] répertorie les Kits de développement logiciel (SDK) en différents langages que vous pouvez utiliser pour le développement d’applications d’appareil et de service qui interagissent avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="53de7-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="53de7-159">L’article [Langage de requête d’IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages][lnk-query] décrit le langage de requête d’IoT Hub permettant de récupérer, à partir d’IoT Hub, des informations relatives à vos jumeaux d’appareil et à vos travaux.</span><span class="sxs-lookup"><span data-stu-id="53de7-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="53de7-160">La rubrique [Prise en charge de MQTT au niveau d’IoT Hub][lnk-devguide-mqtt] fournit des informations supplémentaires sur la prise en charge du protocole MQTT par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="53de7-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53de7-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="53de7-161">Next steps</span></span>
<span data-ttu-id="53de7-162">À présent que vous savez comment utiliser les méthodes directes, vous serez peut-être intéressé par les rubriques suivantes du Guide du développeur IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="53de7-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="53de7-163">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="53de7-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="53de7-164">Si vous souhaitez tenter de mettre en pratique certains des concepts décrits dans cet article, vous serez peut-être intéressé par le didacticiel IoT Hub suivant :</span><span class="sxs-lookup"><span data-stu-id="53de7-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="53de7-165">[Utiliser des méthodes directes][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="53de7-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
