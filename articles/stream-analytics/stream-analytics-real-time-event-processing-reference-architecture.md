---
title: "événement aaaReal au moment du traitement de traitement des événements de flux de données Analytique | Documents Microsoft"
description: "Découvrez comment un ensemble de services Azure peut interagir pour l’analyse et le traitement des événements en temps réel."
keywords: "traitement en temps réel, traitement des événements, architecture de référence"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Architecture de référence : Traitement d’événements en temps réel avec Microsoft Azure Stream Analytics
architecture de référence Hello pour les événements en temps réel avec Azure flux Analytique de traitement est prévue tooprovide un modèle générique pour le déploiement d’une plateforme en temps réel comme solution de traitement de flux de service (PaaS) avec Microsoft Azure.

## <a name="summary"></a>Résumé
En règle générale, les solutions analytique s’appuient sur des fonctionnalités telles que ETL (extraction, transformation, chargement) et d’entreposage de données, où les données sont stockées tooanalysis préalable. Évolutions, y compris les données plus rapidement entrantes repoussent cette limite toohello de modèle existant. données de tooanalyze possibilité Hello dans Mobile toostorage préalable de flux de données sont une solution, et s’il n’est pas une nouvelle fonctionnalité, approche de hello n’a pas été largement adopté dans tous les secteurs de l’industrie. 

Microsoft Azure fournit un catalogue étendu de technologies d’analyse compatibles avec de nombreuses solutions et spécifications. En sélectionnant le toodeploy services Azure pour une solution de bout en bout peut être difficile étant donné la gamme hello des offres. Ce document est conçue toodescribe hello capacités et interopérabilité de hello divers services Azure qui prennent en charge une solution d’événements de diffusion en continu. Elle explique également certains des scénarios hello dans lesquels les clients peuvent tirer parti de ce type d’approche.

## <a name="contents"></a>Sommaire
* Résumé
* Introduction au moment de le tooReal Analytique
* Proposition de valeur des données en temps réel dans Azure
* Scénarios courants d’analyse en temps réel
* Architecture et composants
  * Sources de données
  * Couche d’intégration de données
  * Couche d’analyse en temps réel
  * Couche de stockage des données
  * Couche présentation/consommation
* Conclusion

**Auteur :** Charles Feddersen, architecte de solutions, Data Insights Center of Excellence, Microsoft Corporation

**Publié :** janvier 2015

**Révision :** 1.0

**Téléchargement :**[Traitement d’événements en temps réel avec Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

