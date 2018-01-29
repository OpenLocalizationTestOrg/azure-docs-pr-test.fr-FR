---
title: "Déployer des modèles en production - Azure Machine Learning | Microsoft Docs"
description: "Guide pratique pour déployer des modèles en production, ce qui leur permet de jouer un rôle actif dans les décisions d’entreprise."
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/30/2017
ms.author: bradsev;
ms.openlocfilehash: c7be9eda2d6f37951eb120250861cf4a39b0141b
ms.sourcegitcommit: be0d1aaed5c0bbd9224e2011165c5515bfa8306c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/01/2017
---
# <a name="deploy-models-in-production"></a>Déployer des modèles en production

Le déploiement en production permet à un modèle de jouer un rôle actif dans une entreprise. Les prédictions issues d’un modèle déployé peuvent être utilisées pour les décisions d’entreprise.

## <a name="production-platforms"></a>Plateformes de production
Il existe différentes approches et plateformes pour mettre les modèles en production. Voici quelques options :


- [Déploiement du modèle dans Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/preview/model-management-overview)
- [Déploiement d’un modèle dans SQL Server](https://docs.microsoft.com/sql/advanced-analytics/tutorials/sqldev-py6-operationalize-the-model)
- [Microsoft Machine Learning Server](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone)


>[!NOTE]
>Avant de procéder au déploiement, vous devez vérifier que le niveau de la latence du modèle est suffisamment faible pour permettre l’utilisation de ce dernier dans l’environnement de production.
>


>[!NOTE]
>Pour un déploiement à l’aide de Microsoft Azure Machine Learning Studio, consultez [Déploiement d’un service web Azure Machine Learning](../studio/publish-a-machine-learning-web-service.md).
>

## <a name="ab-testing"></a>Test A/B
Quand plusieurs modèles sont en production, il peut être utile d’effectuer un [test A/B](https://en.wikipedia.org/wiki/A/B_testing) pour comparer les performances des modèles. 

 
## <a name="next-steps"></a>Étapes suivantes

Des procédures pas à pas illustrant toutes les étapes de **scénarios spécifiques** sont également fournies. L’article [Exemples de procédures pas à pas](walkthroughs.md) les répertorie et les décrit brièvement, en les accompagnant de liens. Ces procédures illustrent comment combiner des outils et services locaux ou cloud dans un flux de travail ou un pipeline pour créer une application intelligente. 
 


