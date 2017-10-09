---
title: "Éviter les interruptions de service avec les travaux Azure Stream Analytics | Microsoft Docs"
description: "Conseils pour rendre votre mise à niveau de travaux Stream Analytics résistante."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Garantir la fiabilité des travaux Stream Analytics lors des mises à jour de service

Fonctionnalité hello toointroduce nouvelles fonctionnalités de service et les améliorations apportées à un rythme rapide est d’être un service entièrement géré. Par conséquent, Stream Analytics peut bénéficier d’un déploiement de mise à jour de service de manière hebdomadaire (ou plus fréquemment). Quel que soit le nombre de tests est terminé, il est toujours un risque qu’un travail existant, en cours d’exécution peut arrêter en raison de l’introduction de toohello d’un bogue. Pour les clients qui exécutent des tâches de traitement de diffusion en continu critiques ces risques doivent toobe évité. Un mécanisme de clients peut utiliser une tooreduce ce risque est d’Azure  **[région associée](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modèle. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Comment les régions jumelées d’Azure résolvent-elles ce problème ?

Stream Analytics garantit que les travaux dans les régions jumelées sont mis à jour dans des lots distincts. Par conséquent il existe un écart de temps suffisant entre les mises à jour hello tooidentify potentielle des bogues et les corrigent.

_Avec l’exception hello du centre de l’Inde_ (dont la région appariée, Inde du Sud, n’a pas de présence de flux de données Analytique), déploiement hello d’un tooStream de mise à jour n’intervient à hello Analytique même temps dans un ensemble de régions associées. Déploiements dans plusieurs régions **Bonjour même groupe** peut se produire **à hello simultanément**.

article Hello sur  **[disponibilité et les régions associées](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  a les informations les plus récentes hello sur lequel les régions sont associées.

Les clients sont conseillées toodeploy travaux identiques tooboth apparié régions. En outre tooStream Analytique interne de surveillance des fonctionnalités, les clients est également conseillé de travaux de hello toomonitor comme si **les deux** sont des tâches de production. Si un saut de ligne est toobe identifié un résultat de la mise à jour de service de flux de données Analytique hello, faire remonter correctement et basculer de sortie de travail sain toohello les consommateurs en aval. Escalade de verrous toosupport empêchera région associée de hello soient affectés par le nouveau déploiement de hello et préserver l’intégrité des hello de travaux de hello associé.
