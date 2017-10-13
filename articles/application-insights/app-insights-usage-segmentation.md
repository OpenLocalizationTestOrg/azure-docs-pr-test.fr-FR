---
title: "Analyse des utilisateurs, des sessions et des événements dans Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: b154a01d1690bff4950ebc1ff5a5b89894d4d111
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Analyse des utilisateurs, des sessions et des événements dans Application Insights

Découvrez quand des personnes utilisent votre application web, les pages qui les intéressent le plus, où vos utilisateurs se trouvent, les navigateurs et les systèmes d’exploitation qu’ils utilisent. Analysez les données de télémétrie d’utilisation et d’activité à l’aide d’[Azure Application Insights](app-insights-overview.md).

## <a name="get-started"></a>Prise en main

Si aucune donnée n’apparaît dans les panneaux des utilisateurs, des sessions ou des événements du portail Application Insights, [découvrez comment prendre en main les outils d’utilisation](app-insights-usage-overview.md).

## <a name="the-users-sessions-and-events-segmentation-tool"></a>L’outil de segmentation Utilisateurs, Sessions et Événements

Trois des panneaux d’utilisation exploitent le même outil pour segmenter et traiter les données de télémétrie fournies par votre application web selon trois perspectives. En filtrant et en segmentant les données, vous pouvez découvrir des informations sur l’utilisation relative des différentes fonctionnalités et pages.

* **Outil Utilisateurs** : nombre de personnes ayant utilisé votre application et ses fonctionnalités.  Les utilisateurs sont comptabilisés à l’aide des ID anonymes stockés dans les cookies du navigateur. Une seule personne utilisant plusieurs navigateurs ou ordinateurs est comptabilisée comme plusieurs utilisateurs.
* **Outil Sessions** : nombre de sessions d’activité utilisateur ayant inclus certaines pages et fonctionnalités de votre application. Une session est comptabilisée après une demi-heure d’inactivité de l’utilisateur ou après 24 heures d’utilisation continue.
* **Outil Événements** : fréquence à laquelle certaines pages et fonctionnalités de votre application sont utilisées. L’affichage d’une page est comptabilisé lorsqu’un navigateur charge la page à partir de votre application, à condition que vous l’ayez [instrumentée](app-insights-javascript.md). 

    Un événement personnalisé représente une occurrence de quelque chose qui se produit dans votre application, souvent une interaction utilisateur, comme un clic sur un bouton ou l’achèvement d’une tâche. Vous insérez le code dans votre application pour [générer des événements personnalisés](app-insights-api-custom-events-metrics.md#trackevent).

![Outil d’utilisation](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>Interrogation de certains utilisateurs 

Explorez les différents groupes d’utilisateurs en ajustant les options d’interrogation en haut de l’outil Utilisateurs : 

* Qui a utilisé : choisissez les événements personnalisés et les affichages de pages. 
* Pendant : choisissez un intervalle de temps. 
* Par : choisissez comment compartimenter les données, soit par période temporelle, soit par une autre propriété telle que le navigateur ou la ville. 
* Fractionner par : choisissez une propriété selon laquelle fractionner ou segmenter les données. 
* Ajouter des filtres : limitez la requête à certains utilisateurs, certaines sessions ou certains événements en fonction de leurs propriétés, telles que le navigateur ou la ville. 
 
## <a name="saving-and-sharing-reports"></a>Enregistrement et partage de rapports 
Vous pouvez enregistrer des rapports d’utilisateurs, privés (uniquement pour vous) dans la section Mes rapports, ou partagés avec tout le monde, avec un accès à cette ressource Application Insights dans la section Rapports partagés.  
 
Lors de l’enregistrement d’un rapport ou de la modification de ses propriétés, choisissez « Current Relative Time Range » (Intervalle de temps relatif actuel) pour enregistrer un rapport avec des données actualisées en permanence, jusqu’à un instant donné.  
 
Choisissez « Current Absolute Time Range » (Intervalle de temps absolu actuel) pour enregistrer un rapport avec un ensemble fixe de données. N’oubliez pas que les données d’Application Insights sont uniquement stockées pendant 90 jours. Si plus de 90 jours se sont écoulés depuis l’enregistrement d’un rapport avec un intervalle de temps absolu, le rapport apparaîtra vide. 
 
## <a name="example-instances"></a>Exemples d’instances

La section Exemples d’instances affiche des informations sur un certain nombre d’utilisateurs, de sessions ou d’événements individuels qui correspondent à la requête actuelle. La prise en compte et l’analyse des comportements des personnes, en plus des agrégats, fournissent des informations sur la façon dont les personnes utilisent réellement votre application. 
 
## <a name="insights"></a>Insights 

La barre latérale Insights regroupe des clusters volumineux d’utilisateurs qui partagent des propriétés communes. Ces clusters peuvent révéler des tendances surprenantes sur la manière dont les personnes utilisent votre application. Par exemple, 40 % de l’utilisation globale de votre application provient de personnes utilisant une fonctionnalité unique.  


## <a name="next-steps"></a>Étapes suivantes
- Pour activer les expériences d’utilisation, commencez à envoyer des [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou des [affichages de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si vous envoyez déjà des événements personnalisés ou des affichages de page, explorez les outils d’utilisation pour savoir comment les utilisateurs emploient votre service.
    - [Entonnoirs](usage-funnels.md)
    - [Rétention](app-insights-usage-retention.md)
    - [Flux d’utilisateurs](app-insights-usage-flows.md)
    - [Classeurs](app-insights-usage-workbooks.md)
    - [Ajouter du contexte utilisateur](app-insights-usage-send-user-context.md)

