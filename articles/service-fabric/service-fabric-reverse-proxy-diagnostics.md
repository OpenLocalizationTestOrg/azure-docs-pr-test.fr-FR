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
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>Surveiller et diagnostiquer le traitement de la demande au serveur de proxy inverse hello

À partir de la version de hello 5.7 de l’infrastructure de Service, les événements de proxy inverse sont disponibles pour la collection. événements de Hello sont disponibles dans deux canaux, l’autre avec uniquement les événements d’erreur Erreur liée à la toorequest le traitement au deuxième canal contenant les événements détaillés avec des entrées pour les demandes réussies et échouées et de proxy inverse de hello.

Consultez trop[collecter les événements de proxy inverse](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable collecte d’événements à partir de ces chaînes dans les locaux et les clusters Azure Service Fabric.

## <a name="troubleshoot-using-diagnostics-logs"></a>Résoudre les problèmes à l’aide de journaux de diagnostic
Voici quelques exemples sur comment les journaux des échecs courants toointerpret hello que peut rencontrer :

1. Le proxy inverse retourne un code d’état de réponse 504 (délai d’expiration).

    L’une des raisons peut être en raison de l’échec du service toohello tooreply au sein de la période de délai d’attente de demande hello.
premier événement Hello ci-dessous enregistre les détails hello de demande de salutation reçu au proxy inverse de hello. Hello second événement indique que hello demande a échoué lors de la transmission tooservice, en raison trop « erreur interne = ERROR_WINHTTP_TIMEOUT » 

    charge utile de Hello comprend :

    *  **traceId**: ce GUID peut être utilisé toocorrelate tous les événements hello correspondant tooa une seule demande. Bonjour ci-dessous deux événements, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, ce qui implique qu’ils appartiennent toohello même demande.
    *  **requestUrl**: hello URL (URL de proxy inverse) toowhich hello demande a été envoyée.
    *  **verb** : verbe HTTP.
    *  **remoteAddress**: adresse du client qui envoie la demande de hello.
    *  **resolvedServiceUrl**: demande entrante hello du toowhich URL Service point de terminaison a été résolu. 
    *  **errorDetails**: plus d’informations sur les échecs de hello.

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

2. Le proxy inverse retourne un code d’état de réponse 404 (Introuvable). 
    
    Voici un exemple d’événement où le proxy inverse retourne 404, car il a échoué hello toofind correspondant du point de terminaison de service.
    entrées de charge utile Hello d’intérêt ici sont :
    *  **processRequestPhase**: indique la phase hello pendant le traitement de requête lors de la défaillance de hello, ***TryGetEndpoint*** ex : lors de la tentative de toofetch hello service point de terminaison tooforward à. 
    *  **errorDetails**: répertorie les critères de recherche de point de terminaison hello. Ici, vous pouvez voir que listenerName hello spécifié = **FrontEndListener** alors que la liste de réplicas du point de terminaison hello contienne uniquement un écouteur portant le nom de hello **OldListener**.
    
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
    Un autre exemple où proxy inverse peut renvoyer l’erreur 404 introuvable est : le paramètre de configuration ApplicationGateway\Http **SecureOnlyMode** a la valeur tootrue avec l’écoute sur le proxy inverse hello **HTTPS**, Toutefois, tous les points de terminaison hello réplica sont non sécurisés (à l’écoute HTTP).
    Inverser retourne de proxy 404, car il ne peut pas trouver un point de terminaison HTTPS tooforward hello demande à l’écoute. Analyse des paramètres de hello dans la charge utile d’événement hello permet toonarrow problème de hello :
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. Proxy inverse de toohello demande échoue avec une erreur de délai d’attente. 
    journaux des événements Hello contenir un événement avec les détails de la demande hello reçu (non illustrés ici).
    événement Hello montre que le service de hello ont répondu avec un code de 404 état et proxy inverse lance un nouveau résoudre. 

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
    Lors de la collecte de tous les événements de hello, vous consultez un train d’événements indiquant chaque résolution et la tentative de transfert.
    dernier événement de série de hello Hello montre le traitement des demandes hello a échoué avec un délai d’attente, ainsi que nombre de hello de tentatives de résolution réussie.
    
    > [!NOTE]
    > Il est recommandé de collecte d’événements détaillés de canal hello tookeep désactivée par défaut et l’activer pour la résolution des problèmes selon les besoins.

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
    
    Si la collection est activée pour les événements critique/erreur uniquement, vous consultez un événement avec des détails sur le délai d’attente hello et nombre hello de tentatives de résolution. 
    
    Si le service de hello envisage toosend un utilisateur toohello précédent 404 état, elle doit être accompagnée d’un en-tête « X-ServiceFabric ». Après avoir corrigé ceci, vous verrez ce client de proxy inverse transfère hello état code toohello précédent.  

4. Cas où hello client s’est déconnecté hello demande.

    Hello ci-dessous l’événement est enregistré lorsque le proxy inverse est transfert hello réponse tooclient mais hello client se déconnecte :

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
> Le traitement des événements connexes toowebsocket demandes ne sont pas actuellement connecté. Il est ajouté dans la prochaine version de hello.

## <a name="next-steps"></a>Étapes suivantes
* [Agrégation et collecte d’événements à l’aide de Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) pour activer la collecte des journaux dans les clusters Azure.
* événements du Service Fabric tooview dans Visual Studio, consultez [analyse et de diagnostiquer localement](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).
* Consultez trop[configurer les services de proxy inverse tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) exemples de modèle pour le Gestionnaire de ressources Azure tooconfigure un proxy inverse sécurisée avec les options de validation de certificat de service différent hello.
* Lecture [l’infrastructure de Service de proxy inverse](service-fabric-reverseproxy.md) toolearn plus.
