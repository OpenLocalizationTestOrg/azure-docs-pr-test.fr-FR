---
title: "aaaHow tooscale votre environnement Azure temps série Insights | Documents Microsoft"
description: "Ce didacticiel décrit comment tooscale votre environnement de la série de temps Azure Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>Comment tooscale votre environnement un aperçu en temps série

Ce didacticiel décrit comment tooscale votre environnement Insights de série de temps.

> [!NOTE]
> La mise à l’échelle sur différents types de référence n’est pas autorisée. Un environnement avec une référence S1 ne peut pas être converti en environnement S2.

## <a name="s1-sku-ingress-rates-and-capacities"></a>Capacités et débits d’entrée de la référence S1

| Capacité de la référence S1 | Débit d’entrée | Capacité de stockage maximale
| --- | --- | --- |
| 1 | 1 Go (1 million d’événements) | 30 Go (30 millions d’événements) par mois |
| 10 | 10 Go (10 millions d’événements) | 300 Go (300 millions d’événements) par mois |

## <a name="s2-sku-ingress-rates-and-capacities"></a>Capacités et débits d’entrée de la référence S2

| Capacité de la référence S2 | Débit d’entrée | Capacité de stockage maximale
| --- | --- | --- |
| 1 | 10 Go (10 millions d’événements) | 300 Go (300 millions d’événements) par mois |
| 10 | 100 Go (100 millions d’événements) | 3 To (3 milliards d’événements) par mois |

Les capacités sont mises à l’échelle de façon linéaire. Par conséquent, une référence S1 avec la capacité 2 prend en charge 2 Go (2 millions) d’événements par débit d’entrée par jour et 60 Go (60 millions d’événements) par mois.

## <a name="changing-hello-capacity-of-your-environment"></a>Modification de la capacité de hello de votre environnement

1. Bonjour portail Azure, sélectionnez hello environnement dont vous souhaitez toochange.
1. Sous Paramètres, cliquez sur Configurer.
1. Utilisez hello capacité curseur tooselect hello capacité qui répond aux exigences de hello pour vos tarifs en entrée et la capacité de stockage.

## <a name="next-steps"></a>Étapes suivantes

* Vérifiez que la nouvelle capacité de hello est suffisante tooprevent de limitation. Pour plus d’informations, consultez hello *votre environnement peut être mise en route limitée* section [ici](time-series-insights-diagnose-and-solve-problems.md).
