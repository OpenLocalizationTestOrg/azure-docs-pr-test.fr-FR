---
title: aaaAzure Service Fabric inverser les diagnostics de proxy | Documents Microsoft
description: "Découvrez comment toomonitor et de diagnostiquer le traitement de la demande au serveur de proxy inverse hello."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a><span data-ttu-id="46069-103">Surveiller et diagnostiquer le traitement de la demande au serveur de proxy inverse hello</span><span class="sxs-lookup"><span data-stu-id="46069-103">Monitor and diagnose request processing at hello reverse proxy</span></span>

<span data-ttu-id="46069-104">À partir de la version de hello 5.7 de l’infrastructure de Service, les événements de proxy inverse sont disponibles pour la collection.</span><span class="sxs-lookup"><span data-stu-id="46069-104">Starting with hello 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="46069-105">événements de Hello sont disponibles dans deux canaux, l’autre avec uniquement les événements d’erreur Erreur liée à la toorequest le traitement au deuxième canal contenant les événements détaillés avec des entrées pour les demandes réussies et échouées et de proxy inverse de hello.</span><span class="sxs-lookup"><span data-stu-id="46069-105">hello events are available in two channels, one with only error events related toorequest processing failure at hello reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="46069-106">Consultez trop[collecter les événements de proxy inverse](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable collecte d’événements à partir de ces chaînes dans les locaux et les clusters Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="46069-106">Refer too[Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="46069-107">Résoudre les problèmes à l’aide de journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="46069-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="46069-108">Voici quelques exemples sur comment les journaux des échecs courants toointerpret hello que peut rencontrer :</span><span class="sxs-lookup"><span data-stu-id="46069-108">Here are some examples on how toointerpret hello common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="46069-109">Le proxy inverse retourne un code d’état de réponse 504 (délai d’expiration).</span><span class="sxs-lookup"><span data-stu-id="46069-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="46069-110">L’une des raisons peut être en raison de l’échec du service toohello tooreply au sein de la période de délai d’attente de demande hello.</span><span class="sxs-lookup"><span data-stu-id="46069-110">One reason could be due toohello service failing tooreply within hello request timeout period.</span></span>
<span data-ttu-id="46069-111">premier événement Hello ci-dessous enregistre les détails hello de demande de salutation reçu au proxy inverse de hello.</span><span class="sxs-lookup"><span data-stu-id="46069-111">hello first event below logs hello details of hello request received at hello reverse proxy.</span></span> <span data-ttu-id="46069-112">Hello second événement indique que hello demande a échoué lors de la transmission tooservice, en raison trop « erreur interne = ERROR_WINHTTP_TIMEOUT »</span><span class="sxs-lookup"><span data-stu-id="46069-112">hello second event indicates that hello request failed while forwarding tooservice, due too"internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="46069-113">charge utile de Hello comprend :</span><span class="sxs-lookup"><span data-stu-id="46069-113">hello payload includes:</span></span>

    *  <span data-ttu-id="46069-114">**traceId**: ce GUID peut être utilisé toocorrelate tous les événements hello correspondant tooa une seule demande.</span><span class="sxs-lookup"><span data-stu-id="46069-114">**traceId**: This GUID can be used toocorrelate all hello events corresponding tooa single request.</span></span> <span data-ttu-id="46069-115">Bonjour ci-dessous deux événements, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, ce qui implique qu’ils appartiennent toohello même demande.</span><span class="sxs-lookup"><span data-stu-id="46069-115">In hello below two events, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong toohello same request.</span></span>
    *  <span data-ttu-id="46069-116">**requestUrl**: hello URL (URL de proxy inverse) toowhich hello demande a été envoyée.</span><span class="sxs-lookup"><span data-stu-id="46069-116">**requestUrl**: hello URL (Reverse proxy URL) toowhich hello request was sent.</span></span>
    *  <span data-ttu-id="46069-117">**verb** : verbe HTTP.</span><span class="sxs-lookup"><span data-stu-id="46069-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="46069-118">**remoteAddress**: adresse du client qui envoie la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="46069-118">**remoteAddress**: Address of client sending hello request.</span></span>
    *  <span data-ttu-id="46069-119">**resolvedServiceUrl**: demande entrante hello du toowhich URL Service point de terminaison a été résolu.</span><span class="sxs-lookup"><span data-stu-id="46069-119">**resolvedServiceUrl**: Service endpoint URL toowhich hello incoming request was resolved.</span></span> 
    *  <span data-ttu-id="46069-120">**errorDetails**: plus d’informations sur les échecs de hello.</span><span class="sxs-lookup"><span data-stu-id="46069-120">**errorDetails**: Additional information about hello failure.</span></span>

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. <span data-ttu-id="46069-121">Le proxy inverse retourne un code d’état de réponse 404 (Introuvable).</span><span class="sxs-lookup"><span data-stu-id="46069-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="46069-122">Voici un exemple d’événement où le proxy inverse retourne 404, car il a échoué hello toofind correspondant du point de terminaison de service.</span><span class="sxs-lookup"><span data-stu-id="46069-122">Here is an example event where reverse proxy returns 404 since it failed toofind hello matching service endpoint.</span></span>
    <span data-ttu-id="46069-123">entrées de charge utile Hello d’intérêt ici sont :</span><span class="sxs-lookup"><span data-stu-id="46069-123">hello payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="46069-124">**processRequestPhase**: indique la phase hello pendant le traitement de requête lors de la défaillance de hello, ***TryGetEndpoint*** ex :</span><span class="sxs-lookup"><span data-stu-id="46069-124">**processRequestPhase**: Indicates hello phase during request processing when hello failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="46069-125">lors de la tentative de toofetch hello service point de terminaison tooforward à.</span><span class="sxs-lookup"><span data-stu-id="46069-125">while trying toofetch hello service endpoint tooforward to.</span></span> 
    *  <span data-ttu-id="46069-126">**errorDetails**: répertorie les critères de recherche de point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="46069-126">**errorDetails**: Lists hello endpoint search criteria.</span></span> <span data-ttu-id="46069-127">Ici, vous pouvez voir que listenerName hello spécifié = **FrontEndListener** alors que la liste de réplicas du point de terminaison hello contienne uniquement un écouteur portant le nom de hello **OldListener**.</span><span class="sxs-lookup"><span data-stu-id="46069-127">Here you can see that hello listenerName specified = **FrontEndListener** whereas hello replica endpoint list only contains a listener with hello name **OldListener**.</span></span>
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    <span data-ttu-id="46069-128">Un autre exemple où proxy inverse peut renvoyer l’erreur 404 introuvable est : le paramètre de configuration ApplicationGateway\Http **SecureOnlyMode** a la valeur tootrue avec l’écoute sur le proxy inverse hello **HTTPS**, Toutefois, tous les points de terminaison hello réplica sont non sécurisés (à l’écoute HTTP).</span><span class="sxs-lookup"><span data-stu-id="46069-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set tootrue with hello reverse proxy listening on **HTTPS**, however all of hello replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="46069-129">Inverser retourne de proxy 404, car il ne peut pas trouver un point de terminaison HTTPS tooforward hello demande à l’écoute.</span><span class="sxs-lookup"><span data-stu-id="46069-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS tooforward hello request.</span></span> <span data-ttu-id="46069-130">Analyse des paramètres de hello dans la charge utile d’événement hello permet toonarrow problème de hello :</span><span class="sxs-lookup"><span data-stu-id="46069-130">Analyzing hello parameters in hello event payload helps toonarrow down hello issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="46069-131">Proxy inverse de toohello demande échoue avec une erreur de délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="46069-131">Request toohello reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="46069-132">journaux des événements Hello contenir un événement avec les détails de la demande hello reçu (non illustrés ici).</span><span class="sxs-lookup"><span data-stu-id="46069-132">hello event logs contain an event with hello received request details (not shown here).</span></span>
    <span data-ttu-id="46069-133">événement Hello montre que le service de hello ont répondu avec un code de 404 état et proxy inverse lance un nouveau résoudre.</span><span class="sxs-lookup"><span data-stu-id="46069-133">hello next event shows that hello service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    <span data-ttu-id="46069-134">Lors de la collecte de tous les événements de hello, vous consultez un train d’événements indiquant chaque résolution et la tentative de transfert.</span><span class="sxs-lookup"><span data-stu-id="46069-134">When collecting all hello events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="46069-135">dernier événement de série de hello Hello montre le traitement des demandes hello a échoué avec un délai d’attente, ainsi que nombre de hello de tentatives de résolution réussie.</span><span class="sxs-lookup"><span data-stu-id="46069-135">hello last event in hello series shows hello request processing has failed with a timeout, along with hello number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="46069-136">Il est recommandé de collecte d’événements détaillés de canal hello tookeep désactivée par défaut et l’activer pour la résolution des problèmes selon les besoins.</span><span class="sxs-lookup"><span data-stu-id="46069-136">It is recommended tookeep hello  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    <span data-ttu-id="46069-137">Si la collection est activée pour les événements critique/erreur uniquement, vous consultez un événement avec des détails sur le délai d’attente hello et nombre hello de tentatives de résolution.</span><span class="sxs-lookup"><span data-stu-id="46069-137">If collection is enabled for critical/error events only, you see one event with details about hello timeout and hello number of resolve attempts.</span></span> 
    
    <span data-ttu-id="46069-138">Si le service de hello envisage toosend un utilisateur toohello précédent 404 état, elle doit être accompagnée d’un en-tête « X-ServiceFabric ».</span><span class="sxs-lookup"><span data-stu-id="46069-138">If hello service intends toosend a 404 status code back toohello user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="46069-139">Après avoir corrigé ceci, vous verrez ce client de proxy inverse transfère hello état code toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="46069-139">After fixing this, you will see that reverse proxy forwards hello status code back toohello client.</span></span>  

4. <span data-ttu-id="46069-140">Cas où hello client s’est déconnecté hello demande.</span><span class="sxs-lookup"><span data-stu-id="46069-140">Cases when hello client has disconnected hello request.</span></span>

    <span data-ttu-id="46069-141">Hello ci-dessous l’événement est enregistré lorsque le proxy inverse est transfert hello réponse tooclient mais hello client se déconnecte :</span><span class="sxs-lookup"><span data-stu-id="46069-141">hello below event is recorded when reverse proxy is forwarding hello response tooclient but hello client disconnects:</span></span>

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> <span data-ttu-id="46069-142">Le traitement des événements connexes toowebsocket demandes ne sont pas actuellement connecté.</span><span class="sxs-lookup"><span data-stu-id="46069-142">Events related toowebsocket request processing are not currently logged.</span></span> <span data-ttu-id="46069-143">Il est ajouté dans la prochaine version de hello.</span><span class="sxs-lookup"><span data-stu-id="46069-143">This will be added in hello next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46069-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="46069-144">Next steps</span></span>
* <span data-ttu-id="46069-145">[Agrégation et collecte d’événements à l’aide de Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) pour activer la collecte des journaux dans les clusters Azure.</span><span class="sxs-lookup"><span data-stu-id="46069-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="46069-146">événements du Service Fabric tooview dans Visual Studio, consultez [analyse et de diagnostiquer localement](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="46069-146">tooview Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="46069-147">Consultez trop[configurer les services de proxy inverse tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) exemples de modèle pour le Gestionnaire de ressources Azure tooconfigure un proxy inverse sécurisée avec les options de validation de certificat de service différent hello.</span><span class="sxs-lookup"><span data-stu-id="46069-147">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="46069-148">Lecture [l’infrastructure de Service de proxy inverse](service-fabric-reverseproxy.md) toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="46069-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) toolearn more.</span></span>
