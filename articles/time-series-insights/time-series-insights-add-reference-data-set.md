---
title: "environnement de Azure temps série Insights aaaAdd référence jeu de données tooyour | Documents Microsoft"
description: "Dans ce didacticiel, vous ajoutez l’environnement de temps série Insights tooyour référence de jeu de données"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Créer un jeu de données de référence pour votre environnement d’un aperçu en temps série à l’aide du portail de Ibiza hello

Un jeu de données de référence est une collection d’éléments qui sont augmentés avec les événements hello à partir de votre source d’événements. Le moteur d’entrée Time Series Insights joint un événement à partir de votre source d’événements à un élément dans votre jeu de données de référence. Cet événement ajouté est ensuite disponible pour la requête. Cette jointure est basée sur les clés hello définies dans votre jeu de données de référence.

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>Étapes tooadd un environnement de tooyour de jeu de données de référence

1. Connectez-vous à toohello [portail Ibiza](https://portal.azure.com).
2. Cliquez sur « Toutes les ressources » dans le menu hello hello situé à gauche du portail de Ibiza hello.
3. Sélectionnez votre environnement Time Series Insights.

    ![Créer le jeu de données de référence de temps série Insights hello](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. Sélectionnez « Jeux de données de référence », puis cliquez sur « + Ajouter ».

    ![Créer le jeu de données de la référence du temps série Insights hello - détails](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Spécifiez le nom hello du jeu de données de référence hello.
6. Spécifiez le nom de la clé hello et son type. Ce nom et le type est toopick utilisé hello de propriété approprié à partir de l’événement hello dans votre source d’événement. Par exemple, si vous fournissez le nom de la clé en tant que « DeviceId » et le type en tant que « String », puis hello un aperçu en temps série entrée moteur recherche une propriété portant le nom hello « DeviceId » de type « String » dans les événements entrants hello. Vous pouvez fournir plusieurs toojoin clé avec les événements hello. correspondance de nom de propriété Hello respecte la casse.

     ![Créer le jeu de données de la référence du temps série Insights hello - détails](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. Cliquez sur « Créer ».

## <a name="next-steps"></a>Étapes suivantes

* [Gérez les données de référence](time-series-insights-manage-reference-data-csharp.md) par programme.
* Pour la référence d’API complète hello, consultez [API de données de référence](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.
