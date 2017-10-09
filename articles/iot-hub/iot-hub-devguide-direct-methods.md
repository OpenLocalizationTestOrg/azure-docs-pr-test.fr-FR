---
title: "aaaUnderstand Azure IoT Hub direct de méthodes | Documents Microsoft"
description: "Guide du développeur - utiliser le code tooinvoke méthodes directes sur vos appareils à partir d’une application de service."
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
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="1725f-103">Comprendre et appeler des méthodes directes à partir d’IoT Hub</span><span class="sxs-lookup"><span data-stu-id="1725f-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="1725f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1725f-104">Overview</span></span>
<span data-ttu-id="1725f-105">IoT Hub vous fournit des méthodes direct de capacité tooinvoke sur des périphériques de cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="1725f-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="1725f-106">Méthodes directes représentent une interaction de demande-réponse avec un tooan similaire de périphérique HTTP appeler dans la mesure où ils réussissent ou échouent immédiatement (après un délai d’attente spécifié par l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="1725f-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="1725f-107">Cela est utile pour les scénarios où les cours hello d’action immédiate est différente selon si l’appareil de hello a été en mesure de toorespond, telles que l’envoi d’un périphérique de veille tooa SMS si un périphérique est hors connexion (SMS qui est plus onéreuse qu’un appel de méthode).</span><span class="sxs-lookup"><span data-stu-id="1725f-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="1725f-108">Chaque méthode d’appareil cible à un seul appareil.</span><span class="sxs-lookup"><span data-stu-id="1725f-108">Each device method targets a single device.</span></span> <span data-ttu-id="1725f-109">[Travaux] [ lnk-devguide-jobs] fournissent un tooinvoke moyen méthodes directes sur plusieurs appareils et planifier l’appel de méthode pour les appareils déconnectés.</span><span class="sxs-lookup"><span data-stu-id="1725f-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="1725f-110">Toute personne disposant d’autorisations **Connexion de service** sur IoT Hub peut appeler une méthode sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="1725f-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="1725f-111">Lorsque toouse</span><span class="sxs-lookup"><span data-stu-id="1725f-111">When toouse</span></span>
<span data-ttu-id="1725f-112">Méthodes directes suivent un modèle de requête-réponse et sont destinés à des communications nécessitant une confirmation immédiate de leurs résultats, un contrôle généralement interactif d’appareil hello, par exemple tooturn sur un ventilateur.</span><span class="sxs-lookup"><span data-stu-id="1725f-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="1725f-113">Consultez trop[des conseils de communication Cloud-à-appareil] [ lnk-c2d-guidance] en cas de doute entre l’utilisation de propriétés souhaitées, diriger les méthodes ou les messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="1725f-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="1725f-114">Cycle de vie de méthode</span><span class="sxs-lookup"><span data-stu-id="1725f-114">Method lifecycle</span></span>
<span data-ttu-id="1725f-115">Méthodes directes sont implémentés sur le périphérique de hello et peuvent nécessiter de zéro ou plusieurs entrées dans toocorrectly de charge utile de méthode hello instancier.</span><span class="sxs-lookup"><span data-stu-id="1725f-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="1725f-116">Vous appelez une méthode directe via un URI côté service (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="1725f-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="1725f-117">Un appareil reçoit des méthodes directes via une rubrique MQTT spécifique de l’appareil (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="1725f-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="1725f-118">Nous pouvons prend en charge les méthodes directes sur les autres protocoles réseau côté appareil Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="1725f-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="1725f-119">Lorsque vous appelez une méthode directe sur un appareil, les valeurs et les noms de propriété ne peuvent contenir US-ASCII imprimable alphanumérique, à l’exception dans l’ensemble suivant de hello : ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="1725f-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="1725f-120">Direct de méthodes synchrones, soit réussir ou échouer après le délai d’attente hello (valeur par défaut : 30 secondes, définissables des too3600 secondes).</span><span class="sxs-lookup"><span data-stu-id="1725f-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="1725f-121">Méthodes directes sont utiles dans les scénarios interactifs où vous souhaitez un tooact périphérique si et seulement si le périphérique de hello est en ligne et de réception commandes, telles que l’activation une lumière à partir d’un téléphone.</span><span class="sxs-lookup"><span data-stu-id="1725f-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="1725f-122">Dans ces scénarios, vous souhaitez toosee immédiate réussite ou l’échec pour que le service cloud hello puisse agir sur le résultat de hello dès que possible.</span><span class="sxs-lookup"><span data-stu-id="1725f-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="1725f-123">Appareil de Hello peut retourner un corps de message en raison de la méthode hello, mais il n’est pas nécessaire pour hello méthode toodo donc.</span><span class="sxs-lookup"><span data-stu-id="1725f-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="1725f-124">Il existe ni garantie de classement, ni sémantique de concurrence sur les appels de méthode.</span><span class="sxs-lookup"><span data-stu-id="1725f-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="1725f-125">Méthode directe sont HTTP uniquement du côté du cloud hello et MQTT uniquement du côté du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="1725f-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="1725f-126">charge utile de Hello pour les demandes de méthodes et des réponses est un document JSON de too8KB.</span><span class="sxs-lookup"><span data-stu-id="1725f-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="1725f-127">Rubriques de référence :</span><span class="sxs-lookup"><span data-stu-id="1725f-127">Reference topics:</span></span>
<span data-ttu-id="1725f-128">Hello rubriques de référence suivantes vous fournissent plus d’informations sur l’utilisation de méthodes directes.</span><span class="sxs-lookup"><span data-stu-id="1725f-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="1725f-129">Appeler une méthode directe à partir d’une application principale</span><span class="sxs-lookup"><span data-stu-id="1725f-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="1725f-130">Appel de méthode</span><span class="sxs-lookup"><span data-stu-id="1725f-130">Method invocation</span></span>
<span data-ttu-id="1725f-131">Les appels de méthode directe sur un appareil sont des appels HTTP qui comprennent les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1725f-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="1725f-132">Hello *URI* toohello spécifique périphérique (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="1725f-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="1725f-133">Hello POST *(méthode)*</span><span class="sxs-lookup"><span data-stu-id="1725f-133">hello POST *method*</span></span>
* <span data-ttu-id="1725f-134">*En-têtes* qui contiennent hello authorization, de demander l’ID, type de contenu et le codage du contenu</span><span class="sxs-lookup"><span data-stu-id="1725f-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="1725f-135">JSON transparent *corps* Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="1725f-135">A transparent JSON *body* in hello following format:</span></span>

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

<span data-ttu-id="1725f-136">Le délai d’attente est exprimé en secondes.</span><span class="sxs-lookup"><span data-stu-id="1725f-136">Timeout is in seconds.</span></span> <span data-ttu-id="1725f-137">Si le délai d’attente n’est pas définie, la valeur par défaut too30 secondes.</span><span class="sxs-lookup"><span data-stu-id="1725f-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="1725f-138">Réponse</span><span class="sxs-lookup"><span data-stu-id="1725f-138">Response</span></span>
<span data-ttu-id="1725f-139">application de back-end Hello reçoit une réponse qui comprend :</span><span class="sxs-lookup"><span data-stu-id="1725f-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="1725f-140">*Code d’état HTTP*, qui est utilisé pour les erreurs provenant de hello IoT Hub, y compris une erreur 404 pour les appareils pas actuellement connecté.</span><span class="sxs-lookup"><span data-stu-id="1725f-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="1725f-141">*En-têtes* qui contiennent des hello ETag, de demander l’ID, type de contenu et le codage du contenu</span><span class="sxs-lookup"><span data-stu-id="1725f-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="1725f-142">JSON *corps* Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="1725f-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="1725f-143">Les deux `status` et `body` sont fournies par le périphérique de hello et utilisées toorespond avec le code d’état du périphérique hello et/ou la description.</span><span class="sxs-lookup"><span data-stu-id="1725f-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="1725f-144">Gérer une méthode directe sur un appareil</span><span class="sxs-lookup"><span data-stu-id="1725f-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="1725f-145">Appel de méthode</span><span class="sxs-lookup"><span data-stu-id="1725f-145">Method invocation</span></span>
<span data-ttu-id="1725f-146">Périphériques de recevoir des demandes de méthode directe sur la rubrique MQTT hello :`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="1725f-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="1725f-147">corps de Hello quel appareil hello reçoit est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="1725f-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="1725f-148">Les demandes de méthode sont QoS 0.</span><span class="sxs-lookup"><span data-stu-id="1725f-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="1725f-149">Réponse</span><span class="sxs-lookup"><span data-stu-id="1725f-149">Response</span></span>
<span data-ttu-id="1725f-150">l’unité Hello envoie des réponses trop`$iothub/methods/res/{status}/?$rid={request id}`, où :</span><span class="sxs-lookup"><span data-stu-id="1725f-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="1725f-151">Hello `status` propriété est l’état fourni par l’appareil de hello d’exécution de la méthode.</span><span class="sxs-lookup"><span data-stu-id="1725f-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="1725f-152">Hello `$rid` propriété est hello demande à partir de l’appel de méthode hello provenant du IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1725f-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="1725f-153">corps de Hello est définie par l’appareil de hello et peut être n’importe quel état.</span><span class="sxs-lookup"><span data-stu-id="1725f-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="1725f-154">Matériel de référence supplémentaire</span><span class="sxs-lookup"><span data-stu-id="1725f-154">Additional reference material</span></span>
<span data-ttu-id="1725f-155">Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="1725f-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="1725f-156">[Points de terminaison IoT Hub] [ lnk-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1725f-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="1725f-157">[Limitation et les quotas] [ lnk-quotas] décrit les quotas hello qui s’appliquent toohello IoT Hub service hello limitation tooexpect de comportement lorsque vous utilisez le service de hello.</span><span class="sxs-lookup"><span data-stu-id="1725f-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="1725f-158">[Azure IoT périphérique et service kits de développement logiciel] [ lnk-sdks] listes hello langue différents kits de développement logiciel vous pouvez utiliser lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1725f-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="1725f-159">[Langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages] [ lnk-query] décrit le langage de requête IoT Hub vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux de hello.</span><span class="sxs-lookup"><span data-stu-id="1725f-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="1725f-160">[Prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] fournit plus d’informations sur la prise en charge IoT Hub pour le protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="1725f-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1725f-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1725f-161">Next steps</span></span>
<span data-ttu-id="1725f-162">Maintenant, vous avez appris comment toouse des méthodes directes, vous pouvez être intéressé hello suivant rubrique du guide de développement IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="1725f-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="1725f-163">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="1725f-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="1725f-164">Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant IoT Hub didacticiel :</span><span class="sxs-lookup"><span data-stu-id="1725f-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="1725f-165">[Utiliser des méthodes directes][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="1725f-165">[Use direct methods][lnk-methods-tutorial]</span></span>

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
