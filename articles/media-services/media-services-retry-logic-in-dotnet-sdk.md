---
title: logique aaaRetry Bonjour Media Services SDK pour .NET | Documents Microsoft
description: "rubrique de Hello donne une vue d’ensemble de la logique de nouvelle tentative dans hello Media Services SDK pour .NET."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>Recommencez logique Bonjour Media Services SDK pour .NET
Lorsque vous utilisez les services Microsoft Azure, des erreurs temporaires peuvent se produire. Si une erreur temporaire se produit, dans la plupart des cas, après plusieurs tentatives hello réussit. Hello Media Services SDK pour .NET implémente hello réessayer logique toohandle transitoires associés aux exceptions et erreurs provoquées par des demandes web, l’exécution de requêtes, l’enregistrement des modifications et les opérations de stockage.  Par défaut, Media Services SDK pour .NET de hello exécute quatre nouvelles tentatives avant application de tooyour hello exception est levée à nouveau. code Hello dans votre application doit gérer puis de cette exception correctement.  

 Hello Voici une brève indication des stratégies de requête Web, le stockage, la requête et les SaveChanges :  

* Hello stratégie de stockage est utilisé pour les opérations de stockage blob (téléchargements ou le téléchargement de fichiers d’éléments multimédias).  
* Hello Web demander une stratégie est utilisée pour les demandes web générique (par exemple, pour obtenir une authentification par jeton et la résolution de point de terminaison de cluster aux utilisateurs de hello).  
* stratégie de requête de Hello est utilisé pour interroger les entités à partir de REST (par exemple, mediaContext.Assets.Where(...)).  
* Hello SaveChanges stratégie est utilisée pour effectuer tout ce qui modifie des données dans service hello (par exemple, la création d’une entité à une entité, en appelant une fonction de service pour une opération de mise à jour).  
  
  Cette rubrique répertorie les types d’exception et la logique de nouvelle tentative des codes d’erreur qui sont gérés par hello Media Services SDK pour .NET.  

## <a name="exception-types"></a>Types d'exceptions
Hello tableau suivant décrit les exceptions que hello Media Services SDK pour .NET gère ou ne gère pas pour certaines opérations qui peuvent provoquer des erreurs temporaires.  

| Exception | Web Request | Storage | Requête | SaveChanges |
| --- | --- | --- | --- | --- |
| WebException<br/>Pour plus d’informations, consultez hello [codes d’état WebException](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus) section. |Oui |Oui |Oui |OUI |
| DataServiceClientException<br/> Pour plus d’informations, voir [Codes d’état d’erreur HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Non |Oui |Oui |OUI |
| DataServiceQueryException<br/> Pour plus d’informations, voir [Codes d’état d’erreur HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Non |Oui |Oui |OUI |
| DataServiceRequestException<br/> Pour plus d’informations, voir [Codes d’état d’erreur HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Non |Oui |Oui |OUI |
| DataServiceTransportException |Non |Non |Oui |OUI |
| TimeoutException |OUI |Oui |Oui |Non |
| SocketException |OUI |Oui |Oui |OUI |
| StorageException |Non |Oui |Non |Non |
| IOException |Non |Oui |Non |Non |

### <a name="WebExceptionStatus"></a> Codes d’état WebException
Hello tableau suivant indique pour quelle erreur WebException logique de nouvelle tentative de codes hello est implémentée. Hello [WebExceptionStatus](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx) énumération définit les codes d’état hello.  

| État | Web Request | Storage | Requête | SaveChanges |
| --- | --- | --- | --- | --- |
| ConnectFailure |OUI |Oui |Oui |OUI |
| NameResolutionFailure |OUI |Oui |Oui |OUI |
| ProxyNameResolutionFailure |OUI |Oui |Oui |OUI |
| SendFailure |OUI |Oui |Oui |OUI |
| PipelineFailure |OUI |Oui |Oui |Non |
| ConnectionClosed |OUI |Oui |Oui |Non |
| KeepAliveFailure |OUI |Oui |Oui |Non |
| UnknownError |OUI |Oui |Oui |Non |
| ReceiveFailure |OUI |Oui |Oui |Non |
| RequestCanceled |OUI |Oui |Oui |Non |
| Délai d'expiration |OUI |Oui |Oui |Non |
| ProtocolError <br/>nouvelle tentative de Hello sur ProtocolError est contrôlé par la gestion hello du code de statut HTTP. Pour plus d’informations, voir [Codes d’état d’erreur HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |OUI |Oui |Oui |OUI |

### <a name="HTTPStatusCode"></a> Codes d’état d’erreur HTTP
Lorsque les opérations de requête et SaveChanges lèvent DataServiceClientException, DataServiceQueryException ou DataServiceQueryException, hello code d’état HTTP erreur est retourné dans hello propriété StatusCode.  Hello tableau suivant répertorie les codes d’erreur logique de nouvelle tentative hello est implémentée.  

| État | Web Request | Storage | Requête | SaveChanges |
| --- | --- | --- | --- | --- |
| 401 |Non |Oui |Non |Non |
| 403 |Non |OUI<br/>Gestion des nouvelles tentatives avec attentes plus longues. |Non |Non |
| 408 |OUI |Oui |Oui |OUI |
| 429 |OUI |Oui |Oui |OUI |
| 500 |OUI |Oui |Oui |Non |
| 502 |OUI |Oui |Oui |Non |
| 503 |OUI |Oui |Oui |OUI |
| 504 |OUI |Oui |Oui |Non |

Si vous souhaitez tootake examiner implémentation réelle de hello Hello SDK Media Services pour la logique de nouvelle tentative de .NET, consultez [azure sdk pour media services](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling).

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

