---
title: "aaaVisualize et résoudre les tâches de flux de données Analytique | Documents Microsoft"
description: "Découvrez comment toovisualize une tâche de flux de données Analytique de pipeline pour le dépannage à l’aide de la fonctionnalité de diagramme hello diagnostics de libre-service."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Visualisation et dépannage de travaux Stream Analytics
Dans le flux de données Analytique, comme avec d’autres technologies de nuage, résolution des problèmes sont parfois toolook nécessaire en raison pour laquelle une tâche ne produit pas de sortie de hello attendu (ou de sortie d’ailleurs). Dans cet esprit, flux de données Analytique fournit une fonctionnalité hello pour visualiser un travail de diffusion en continu. Cela est également utile comme outil de modélisation et a hello autre avantage pour celles qui nécessitent une documentation de leur travail.

Dans la visualisation de hello entrées hello de panneau de configuration sont visibles, ainsi que la requête hello en cours d’exécution, et ensuite toutes les sorties hello configuré. Problèmes de connectivité ou de configuration peuvent deviennent plus évidents et il peut également être utile toosee une représentation visuelle de votre configuration.

## <a name="using-hello-diagnosis-diagram-tool"></a>À l’aide des outils de diagramme de diagnostic hello
tooaccess ce visualiseur, cliquez simplement sur hello bouton « Diagramme de diagnostic » dans hello panneau « Paramètres » de hello de tâche de flux de données Analytique hello.

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Chaque entrée et la sortie sont codée par couleur tooindicate hello état actuel de ce composant, comme indiqué ci-dessous.

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

Lorsque l’utilisateur hello veut toolook requête intermédiaire étapes toounderstand hello données flux modèles à l’intérieur d’un travail, outil de visualisation hello fournit une vue de répartition hello de requête de hello dans ses étapes et la séquence de flux de hello. En cliquant sur chaque étape de requête affiche la section correspondante de hello dans une requête de modification de volet, comme illustré. 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

