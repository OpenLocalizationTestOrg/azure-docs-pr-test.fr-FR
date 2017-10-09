---
title: "aaaOverview des modèles de mise à l’échelle courants | Documents Microsoft"
description: "Découvrez que certaines hello courantes modèles tooauto l’échelle vos ressources dans Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a>Vue d’ensemble des modèles courants de mise à l’échelle automatique
Cet article décrit certaines des hello courantes modèles tooscale vos ressources dans Azure.

Azure à l’échelle automatique analyse s’applique uniquement tooVirtual jeux de mise à l’échelle de Machine (mise), services de cloud computing, les plans de service d’application et les environnements app service. 

# <a name="lets-get-started"></a>Prise en main

Cet article suppose que vous êtes familiarisé avec la mise à l’échelle automatique. Vous pouvez [obtenir tooscale ici démarré votre ressource][1]. Hello Voici quelques-uns des modèles de mise à l’échelle hello courants.

## <a name="scale-based-on-cpu"></a>Mise à l’échelle en fonction du processeur

Vous avez une application web (/VMSS/rôle de service cloud) et 

- Vous souhaitez tooscale hors/mise à l’échelle en fonction de processeur.
- En outre, vous souhaitez que tooensure est un nombre minimal d’instances. 
- En outre, vous souhaitez tooensure que vous définissez un nombre de toohello le nombre maximal d’instances, à que vous pouvez faire évoluer.

![Mise à l’échelle en fonction du processeur][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Mettre à l’échelle différemment durant les week-ends et jours de la semaine

Vous avez une application web (/VMSS/rôle de service cloud) et

- Vous voulez 3 instances par défaut (pour les jours de la semaine)
- Vous ne prévoyez pas le trafic sur les week-ends, et par conséquent, vous souhaitez tooscale too1 instance vers le bas sur les week-ends.

![Mettre à l’échelle différemment durant les week-ends et jours de la semaine][3]

## <a name="scale-differently-during-holidays"></a>Mettre à l’échelle différemment pendant les jours fériés

Vous avez une application web (/VMSS/rôle de service cloud) et 

- Vous souhaitez tooscale haut/bas en fonction de l’utilisation du processeur par défaut
- Toutefois, pendant la saison (ou des jours spécifiques qui sont importants pour votre entreprise) vous toooverride, hello par défaut et souhaitez davantage de capacité à votre disposition.

![Mettre à l’échelle différemment lors des jours fériés][4]

## <a name="scale-based-on-custom-metric"></a>Mise à l’échelle en fonction de métriques personnalisées

Vous avez un serveur web frontal et un niveau d’API qui communique avec le serveur principal hello. 

- Vous souhaitez que le niveau de hello API tooscale basé sur des événements personnalisés dans frontal hello (exemple : vous souhaitez tooscale votre processus de validation basé sur le nombre de hello d’éléments de panier d’achat de hello)

![Mise à l’échelle en fonction de métriques personnalisées][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png