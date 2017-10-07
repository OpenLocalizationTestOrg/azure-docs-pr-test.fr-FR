---
title: "aaaAzure de corrélation de télémétrie Application Insights | Documents Microsoft"
description: "Corrélation de télémétrie dans Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Corrélation de télémétrie dans Application Insights

Dans hello world services micro, chaque opération logique nécessite le travail effectué dans les différents composants du service de hello. Chacun de ces composants peut être surveillé séparément par [Application Insights](app-insights-overview.md). composant d’application Hello web communique avec les informations d’identification de l’authentification fournisseur composant toovalidate utilisateur et avec les données de tooget hello API composant de visualisation. composant d’API Hello à son tour peut interroger les données à partir d’autres services et utiliser les composants du fournisseur de cache et notifier le composant de facturation hello sur cet appel. Application Insights prend en charge la corrélation de télémétrie distribuée. Il vous permet de toodetect composant qui est chargé de défaillances ou une dégradation des performances.

Cet article explique le modèle de données hello utilisé par les données de télémétrie Application Insights toocorrelate envoyées par plusieurs composants. Elle couvre les protocoles et les techniques de propagation de contexte hello. Elle traite également implémentation hello des concepts de corrélation hello sur les plateformes et des langues différentes.

## <a name="telemetry-correlation-data-model"></a>Modèle de données de corrélation de télémétrie

Application Insights définit le [modèle de données](application-insights-data-model.md) pour la corrélation de télémétrie distribuée. télémétrie tooassociate avec opération logique de hello, chaque élément de données de télémétrie a un champ de contexte appelé `operation_Id`. Cet identificateur est partagé par chaque élément de données de télémétrie dans la trace de hello distribué. Par conséquent, même en perdant la télémétrie d’une seule couche, vous pouvez toujours associer la télémétrie communiquée par d’autres composants.

Opération logique distribuée se compose généralement d’un ensemble d’opérations plus petits - demandes traitées par un des composants de hello. Ces opérations sont définies par la [télémétrie des requêtes](application-insights-data-model-request-telemetry.md). Chaque télémétrie de requête possède son propre `id` qui l’identifie globalement de façon unique. Et toutes les données de télémétrie - traces, les exceptions, etc. associé à cette requête doivent définir hello `operation_parentId` valeur toohello de demande de hello `id`.

Chaque opération sortante comme composant de tooanother appel http représenté par [télémétrie des dépendances](application-insights-data-model-dependency-telemetry.md). La télémétrie des dépendances définit également son propre `id` globalement unique. La télémétrie des requêtes, initiée par cet appel de dépendances, l’utilise en tant que `operation_parentId`.

Vous pouvez générer vue hello d’à l’aide de l’opération logique distribuée `operation_Id`, `operation_parentId`, et `request.id` avec `dependency.id`. Ces champs également définissent des commandes de causalité hello d’appels de télémétrie.

Dans l’environnement de services micro, des traces à partir des composants peuvent passer toohello les stockages différents. Chaque composant peut avoir sa propre clé d’instrumentation dans Application Insights. télémétrie tooget pour l’opération logique de hello, vous devez tooquery des données à partir de chaque stockage. Lorsque le nombre de stockages est volumineux, vous devez toohave une indication sur l’emplacement toolook suivant.

Application Insights, modèle de données définit deux champs toosolve ce problème : `request.source` et `dependency.target`. premier champ de Hello identifie le composant hello qui a initié la demande de dépendance hello et hello identifie ensuite le composant a retourné une réponse hello d’appel de dépendance hello.


## <a name="example"></a>Exemple

Prenons un exemple d’un prix de STOCK application affichant hello cours d’une action à l’aide des API externe de hello appelé API des STOCKS. Hello application du cours de l’action a une page `Stock page` ouvert en utilisant du navigateur web hello client `GET /Home/Stock`. requêtes de l’application Hello hello API de STOCK à l’aide d’un appel HTTP `GET /api/stock/value`.

Vous pouvez analyser la télémétrie obtenue en exécutant une requête :

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

Dans la note de vue hello résultat que tous les éléments de télémétrie partagent la racine de hello `operation_Id`. Lorsque ajax appelez effectuées à partir de la page hello - nouvel id unique `qJSXU` est attribué toohello télémétrie des dépendances et les id de page de d’affichage est utilisé en tant que `operation_ParentId`. À son tour, la requête du serveur utilise l’ID d’ajax en tant que `operation_ParentId`, etc.

| itemType   | name                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| pageView   | Stock page                |              | STYz               | STYz         |
| dependency | GET /Home/Stock           | qJSXU        | STYz               | STYz         |
| request    | GET Home/Stock            | KqKwlrSt9PA= | qJSXU              | STYz         |
| dependency | GET /api/stock/value      | bBrf2L7mm2g= | KqKwlrSt9PA=       | STYz         |

Désormais, lorsque hello appel `GET /api/stock/value` apportées service externe de tooan vous souhaitez identité de hello tooknow de ce serveur. Vous pouvez définir le champ `dependency.target` de manière appropriée. Lorsque le service externe de hello ne prend pas en charge l’analyse - `target` a la valeur toohello nom d’hôte de service hello comme `stock-prices-api.com`. Toutefois si ce service s’identifie en retournant prédéfini en-tête HTTP - `target` contient l’identité du service hello qui permet de trace de toobuild distribué Application Insights en interrogeant les données de télémétrie à partir de ce service. 

## <a name="correlation-headers"></a>En-têtes de corrélation

Nous travaillons sur la proposition RFC pour hello [corrélation de protocole HTTP](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md). Cette proposition définit deux en-têtes :

- `Request-Id`exécuter l’identificateur global unique de hello d’appel de hello
- `Correlation-Context`-exécuter hello collection nom/valeur paires de propriétés de la trace hello distribué

Hello standard définit également les deux schémas de `Request-Id` génération - plate et hiérarchique. Un schéma plat hello, il est bien connu `Id` clé définie pour hello `Correlation-Context` collection.

Application Insights définit hello [extension](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md) pour la corrélation de hello le protocole HTTP. Il utilise `Request-Context` nom paires valeur collection de hello toopropagate des propriétés utilisées par l’appelant immédiat de hello ou de l’appelé. Application Insights SDK utilise ce tooset en-tête `dependency.target` et `request.source` champs.

## <a name="open-tracing-and-application-insights"></a>Open Tracing et Application Insights

Les modèles de données Application Insights et [Open Tracing](http://opentracing.io/) regardent si 

- `request`, `pageView` mappe trop**étendue** avec`span.kind = server`
- `dependency`mappe trop**étendue** avec`span.kind = client`
- `id`d’un `request` et `dependency` mappe trop**Span.Id**
- `operation_Id`mappe trop**TraceId**
- `operation_ParentId`mappe trop**référence** de type`ChileOf`

Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).

Pour des définitions des concepts Open Tracing, consultez les pages [specification](https://github.com/opentracing/specification/blob/master/specification.md) et [semantic_conventions](https://github.com/opentracing/specification/blob/master/semantic_conventions.md).


## <a name="telemetry-correlation-in-net"></a>Corrélation de télémétrie dans .NET

Au fil du temps .NET défini le nombre de façons toocorrelate télémesure et diagnostics des journaux. Il est `System.Diagnostics.CorrelationManager` autorisant tootrack [LogicalOperationStack et ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx). `System.Diagnostics.Tracing.EventSource`et Windows ETW définissent la méthode hello [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx). `ILogger` utilise les [étendues de journaux](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes). WCF et Http lient la propagation de contexte « en cours ».

Toutefois, ces méthodes n’ont pas activé le traçage distribué automatique. `DiagnosticsSource`est un toosupport de manière automatique entre la corrélation de l’ordinateur. Bibliothèques .NET prend en charge de la Source de Diagnostics et permettent la propagation automatique entre les ordinateurs du contexte de corrélation hello via le transport http, par exemple hello.

Hello [guide tooActivities](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) dans la Source de Diagnostics présente les notions de base de hello de suivi des activités. 

ASP.NET Core 2.0 prend en charge l’extraction des en-têtes Http et démarrage hello nouvelle activité. 

`System.Net.HttpClient`version de départ `<fill in>` prend en charge automatique d’injection de corrélation de hello en-têtes Http et le suivi des appels http de hello en tant qu’activité.

Il existe un nouveau Http Module [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) pour hello ASP.NET classique. Ce module implémente la corrélation de télémétrie à l’aide de DiagnosticsSource. Il démarre l’activité en fonction des en-têtes de requête entrante. Il met également en corrélation télémétrie hello différentes étapes de traitement de la requête. Même pour les cas de hello lors de chaque étape de traitement IIS s’exécute sur un autre gérer des threads.

Version de départ application Insights SDK `2.4.0-beta1` utilise les données de télémétrie toocollect DiagnosticsSource et l’activité et l’associer à l’activité en cours hello. 

## <a name="next-steps"></a>Étapes suivantes

- [Écrire des données de télémétrie personnalisées](app-insights-api-custom-events-metrics.md)
- Intégrez tous les composants de votre microservice sur Application Insights. Consultez les [plateformes prises en charge](app-insights-platforms.md).
- Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).
- Découvrez comment trop[étendre et de filtrer les données de télémétrie](app-insights-api-filtering-sampling.md).
