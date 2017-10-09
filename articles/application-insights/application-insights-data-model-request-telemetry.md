---
title: "aaaAzure modèle de données d’Application Insights télémétrie - demande de télémétrie | Documents Microsoft"
description: "Modèle de données Application Insights pour la télémétrie des requêtes"
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
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a>Télémétrie des requêtes : modèle de données Application Insights

Un élément de données de télémétrie de demande (dans [Application Insights](app-insights-overview.md)) représente hello séquence logique d’exécution déclenchée par une application de tooyour demande externe. Chaque exécution de la demande est identifiée par unique `ID` et `url` contenant tous les paramètres de l’exécution de hello. Vous pouvez regrouper des demandes par la logique `name` et définir hello `source` de cette demande. L’exécution du code peut donner `success` ou `duration` et a une certain durée (`fail`). Les échecs et les réussites d’exécution peuvent être regroupés par `resultCode`. Heure de début pour les données de télémétrie hello demande définies sur le niveau de l’enveloppe hello.

Demande de télémétrie prend en charge le modèle d’extensibilité standard hello à l’aide personnalisée `properties` et `measurements`.

## <a name="name"></a>Nom

Nom de la demande de hello représente la demande de code chemin d’accès emprunté tooprocess hello. Tooallow de valeur faible cardinalité mieux regrouper des demandes. Pour les requêtes HTTP qu’il représente hello méthode HTTP et le modèle de chemin d’accès d’URL comme `GET /values/{id}` sans hello réel `id` valeur.

Web de Insights application SDK envoie nom « tel quel » de la demande à ce qui concerne les tooletter cas. Groupement de l’interface utilisateur respecte la casse pour `GET /Home/Index` est comptabilisée séparément à partir de `GET /home/INDEX` même si elles entraînent souvent Bonjour même contrôleur et l’action de l’exécution. Hello qui fait que les URL sont en général [respectant la casse](http://www.w3.org/TR/WD-html40-970708/htmlweb.html). Vous souhaiterez peut-être toosee si toutes les `404` s’est produite pour l’URL de hello tapées en majuscules. Vous pouvez en savoir plus sur demande nom collection par Kit de développement Web ASP.Net Bonjour [billet de blog](http://apmtips.com/blog/2015/02/23/request-name-and-url/).

Longueur maximale : 1024 caractères

## <a name="id"></a>ID

Identificateur d’une instance d’appel de requête. Utilisé pour la corrélation entre la requête et d’autres éléments de télémétrie. L’ID doit être globalement unique. Pour plus d’informations, consultez la page relative à la [corrélation](application-insights-correlation.md).

Longueur maximale : 128 caractères

## <a name="url"></a>Url

URL de requête avec tous les paramètres de chaîne de requête.

Longueur maximale : 2048 caractères

## <a name="source"></a>Source

Source de la demande de hello. Clé d’instrumentation hello de l’appelant de hello ou adresse ip de hello de l’appelant de hello sont des exemples. Pour plus d’informations, consultez la page relative à la [corrélation](application-insights-correlation.md).

Longueur maximale : 1024 caractères

## <a name="duration"></a>Durée

Durée de la requête au format : `DD.HH:MM:SS.MMMMMM`. Doit être positive et inférieure à `1000` jours. Ce champ est obligatoire, comme la télémétrie des requêtes représente l’opération de hello avec hello début et à la fin de hello.

## <a name="response-code"></a>Response code

Résultat de l’exécution d’une requête. Code d’état HTTP des requêtes HTTP. Cela peut-être une valeur `HRESULT` ou un type d’exception pour les autres types de requêtes.

Longueur maximale : 1024 caractères

## <a name="success"></a>Succès

Indication de la réussite ou non d’un appel. Ce champ est obligatoire. Lorsque ne pas défini explicitement trop`false` -demande considérée comme toobe réussie. Définissez cette valeur trop`false` si l’opération a été interrompue par une exception ou a renvoyé un code de résultat d’erreur.

Pour les applications web hello, Application Insights définissent la demande comme ayant échoué lorsque le code de réponse hello est moins hello `400` ou égal à trop`401`. Toutefois il existe des cas lorsque ce mappage par défaut ne correspond pas à la sémantique de l’application hello de hello. Le code de réponse `404` peut indiquer « aucun enregistrement », qui peut faire partie d’un flux régulier. Il peut également indiquer un lien rompu. Pourquoi des liens rompus, vous pouvez même implémenter une logique plus avancée. Vous pouvez marquer des liens rompus sous forme d’échecs uniquement lorsque ces liens sont trouvent sur hello en analysant le point d’accès url du même site. Ou les marquer comme des échecs lors de l’accès à partir de l’application mobile de la société hello. De même `301` et `302` indique un échec lors de l’accès client hello qui ne prennent pas en charge de redirection.

Un contenu partiellement accepté `206` peut indiquer l’échec d’une requête globale. Par exemple, le point de terminaison d’Application Insights reçoit un lot d’éléments de télémétrie sous la forme d’une seule requête. Elle retourne `206` lorsque certains éléments de lot de hello n'ont pas été traités avec succès. Taux d’augmentation de `206` indique un problème qui doit toobe examinée. Une logique similaire s’applique également`207` multi état où la réussite de hello peut-être hello pire des codes de réponse distincts.

Vous pouvez en savoir plus sur résultat de la demande code et code d’état Bonjour [billet de blog](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).

## <a name="custom-properties"></a>Propriétés personnalisées

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Mesures personnalisées

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Étapes suivantes

- [Écrire une télémétrie de demande personnalisée](app-insights-api-custom-events-metrics.md#trackrequest)
- Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).
- Découvrez comment trop[configurer ASP.NET Core](app-insights-asp-net.md) application avec Application Insights.
- Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.
