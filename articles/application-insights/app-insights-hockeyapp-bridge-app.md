---
title: "aaaExploring HockeyApp des données dans une Application Azure Insights | Documents Microsoft"
description: "Analysez l’utilisation et les performances de votre application Azure avec Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a>Exploration des données HockeyApp dans Application Insights
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello est recommandé de plateforme pour l’analyse des applications de bureau et mobiles dynamiques. À partir de HockeyApp, vous pouvez envoyer personnalisé et l’utilisation de télémétrie toomonitor de trace et faciliter le diagnostic (dans les données de panne plus toogetting). Ce flux de données de télémétrie peut être interrogé à l’aide de hello puissant [Analytique](app-insights-analytics.md) fonctionnalité de [Azure Application Insights](app-insights-overview.md). En outre, vous pouvez [exporter hello personnalisée et la télémétrie des traces](app-insights-export-telemetry.md). tooenable ces fonctionnalités, vous avez configuré un pont qui transfère les données personnalisées de HockeyApp tooApplication Insights.

## <a name="hello-hockeyapp-bridge-app"></a>application de HockeyApp pont Hello
Hello HockeyApp pont App est fonction principale hello qui vous permet de tooaccess votre HockeyApp personnalisée et la télémétrie des traces dans Application Insights via hello Analytique et les fonctionnalités de l’exportation continue. Événements personnalisé et trace collectées par HockeyApp après la création de hello Hello HockeyApp pont application seront accessibles à partir de ces fonctionnalités. Nous allons voir comment tooset une de ces applications de pont.

Dans HockeyApp, ouvrez Paramètres de compte, [Jetons d’API](https://rink.hockeyapp.net/manage/auth_tokens). Créez un nouveau jeton ou réutilisez un jeton existant. les droits minimaux Hello requis sont « lecture seule ». Création d’une copie de hello API jeton.

![Obtenir un jeton d’API HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

Portail de Microsoft Azure hello ouvert et [créer une ressource Application Insights](app-insights-create-new-resource.md). Définir le Type d’Application trop « Application de pont HockeyApp » :

![Nouvelle ressource Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

Vous n’avez pas besoin tooset un nom, il sera automatiquement configuré à partir du nom de HockeyApp hello.

champs de pont HockeyApp Hello s’affichent. 

![Renseignez les champs de pont](./media/app-insights-hockeyapp-bridge-app/03.png)

Entrez un jeton de HockeyApp hello notées précédemment. Cette action remplit le menu de liste déroulante « Application HockeyApp » hello avec toutes vos applications HockeyApp. Sélectionnez hello une vous voulez toouse et reste hello complète des champs de hello. 

Ouvrez la nouvelle ressource de hello. 

Notez que les données de salutation prennent un certain temps toostart flux.

![Ressource Application Insights en attente de données](./media/app-insights-hockeyapp-bridge-app/04.png)

Et voilà ! Personnalisé et la trace les données collectées dans votre application instrumentée HockeyApp à partir de ce point sont désormais également disponible tooyou Bonjour Analytique et l’exportation continue des fonctionnalités d’Application Insights.

Nous allons brièvement chacun de ces tooyou désormais disponible de fonctionnalités.

## <a name="analytics"></a>Analyse
Analytique est un outil puissant pour l’interrogation de vos données, ce qui vous toodiagnose ad hoc et analyse vos données de télémétrie et rapidement découverte les causes et les modèles.

![Analyse](./media/app-insights-hockeyapp-bridge-app/05.png)

* [En savoir plus sur Analyse](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>Exportation continue
Exportation continue vous permet de tooexport vos données dans un conteneur de stockage d’objets Blob Azure. Cela est très utile si vous avez besoin tookeep vos données plus longtemps que la période de rétention hello actuellement proposée par Application Insights. Vous pouvez conserver les données de salutation dans le stockage blob, le traiter dans une base de données SQL ou de votre solution d’entrepôt de données par défaut.

[En savoir plus sur l’exportation continue](app-insights-export-telemetry.md)

## <a name="next-steps"></a>Étapes suivantes
* [Appliquer des données tooyour Analytique](app-insights-analytics-tour.md)

