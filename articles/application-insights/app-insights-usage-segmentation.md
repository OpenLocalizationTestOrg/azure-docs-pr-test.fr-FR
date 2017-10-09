---
title: "analyse aaaUser, de session et d’événement dans une Application Azure Insights | Documents Microsoft"
description: "Analyse démographique des utilisateurs de votre application web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Analyse des utilisateurs, des sessions et des événements dans Application Insights

Découvrez quand des personnes utilisent votre application web, les pages qui les intéressent le plus, où vos utilisateurs se trouvent, les navigateurs et les systèmes d’exploitation qu’ils utilisent. Analysez les données de télémétrie d’utilisation et d’activité à l’aide d’[Azure Application Insights](app-insights-overview.md).

## <a name="get-started"></a>Prise en main

Si vous ne voyez encore des données d’utilisateurs de hello, sessions ou panneaux d’événements dans le portail Application Insights hello, [apprendre comment tooget démarrer avec les outils de l’utilisation de hello](app-insights-usage-overview.md).

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>outil de segmentation des utilisateurs, les Sessions et les événements Hello

Trois des utilisation hello panneaux utiliser hello même outil tooslice dés données de télémétrie et à partir de votre application web à partir de trois perspectives. En filtrant et en fractionnant les données de salutation, vous pouvez découvrir des informations sur l’utilisation de relative hello des pages différentes et des fonctionnalités.

* **Outil Utilisateurs** : nombre de personnes ayant utilisé votre application et ses fonctionnalités.  Les utilisateurs sont comptabilisés à l’aide des ID anonymes stockés dans les cookies du navigateur. Une seule personne utilisant plusieurs navigateurs ou ordinateurs est comptabilisée comme plusieurs utilisateurs.
* **Outil Sessions** : nombre de sessions d’activité utilisateur ayant inclus certaines pages et fonctionnalités de votre application. Une session est comptabilisée après une demi-heure d’inactivité de l’utilisateur ou après 24 heures d’utilisation continue.
* **Outil Événements** : fréquence à laquelle certaines pages et fonctionnalités de votre application sont utilisées. L’affichage d’une page est comptabilisé lorsqu’un navigateur charge la page à partir de votre application, à condition que vous l’ayez [instrumentée](app-insights-javascript.md). 

    Un événement personnalisé représente une occurrence de quelque chose se passe dans votre application, souvent une intervention de l’utilisateur comme un bouton, cliquez sur ou hello d’achèvement d’une tâche. Vous insérez le code de votre application trop[générer des événements personnalisés](app-insights-api-custom-events-metrics.md#trackevent).

![Outil d’utilisation](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>Interrogation de certains utilisateurs 

Explorer les différents groupes d’utilisateurs à l’aide des options de requête hello haut hello d’outil d’utilisateurs hello : 

* Qui a utilisé : choisissez les événements personnalisés et les affichages de pages. 
* Pendant : choisissez un intervalle de temps. 
* Par : Choisissez comment toobucket hello des données, d’une période de temps ou par une autre propriété tels que navigateur ou de la ville. 
* Fractionner par : Pour choisir une propriété par les données hello toosplit ou le segment. 
* Ajouter des filtres : Limitez hello interroger toocertain utilisateurs, les sessions ou les événements en fonction de leurs propriétés, telles que le navigateur ou de la ville. 
 
## <a name="saving-and-sharing-reports"></a>Enregistrement et partage de rapports 
Vous pouvez enregistrer des rapports d’utilisateurs, soit privé tooyou simplement dans la section de Mes rapports hello, ou partagé avec tous les autres avec accès toothis ressource Application Insights Bonjour section rapports partagés.  
 
Lors de l’enregistrement d’un rapport ou modifier ses propriétés, choisissez toosave « Relatif intervalle de temps actuel » un rapport est en permanence actualisé les données, si vous revenez en une durée fixe.  
 
Choisissez « Absolu intervalle de temps actuel » toosave un rapport avec un ensemble fixe de données. N’oubliez pas que les données d’Application Insights uniquement stockées pendant 90 jours, donc si plus de 90 jours se sont écoulés depuis un rapport avec une plage de temps absolu a été enregistré, le rapport de hello apparaîtra vide. 
 
## <a name="example-instances"></a>Exemples d’instances

Hello section instances d’exemple affiche des informations sur un ensemble d’utilisateurs individuels, les sessions ou les événements qui correspondent à la requête en cours hello. Prise en compte et d’Explorer les comportements hello de personnes, de tooaggregates d’addition, peuvent fournir des informations sur la manière dont les personnes utilisent réellement votre application. 
 
## <a name="insights"></a>Insights 

barre latérale de Hello Insights montre les grands groupes d’utilisateurs qui partagent des propriétés communes. Ces clusters peuvent révéler des tendances surprenantes sur la manière dont les personnes utilisent votre application. Par exemple, si 40 % de toutes les utilisation hello de votre application provient des personnes à l’aide d’une fonctionnalité unique.  


## <a name="next-steps"></a>Étapes suivantes
- l’utilisation de tooenable rencontre, démarrer l’envoi de [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [des consultations de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si vous envoyez déjà hello l’utilisation des outils toolearn Explorer les événements personnalisés ou des vues de la page, comment les utilisateurs utiliser votre service.
    - [Entonnoirs](usage-funnels.md)
    - [Rétention](app-insights-usage-retention.md)
    - [Flux d’utilisateurs](app-insights-usage-flows.md)
    - [Classeurs](app-insights-usage-workbooks.md)
    - [Ajouter du contexte utilisateur](app-insights-usage-send-user-context.md)

