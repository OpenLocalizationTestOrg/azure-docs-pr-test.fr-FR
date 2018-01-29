---
title: "Phase de déploiement du cycle de vie du processus TDSP (Team Data Science Process) - Azure | Microsoft Docs"
description: "Objectifs, tâches et livrables associés à la phase de déploiement de vos projets de science des données"
services: machine-learning
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
ms.date: 11/04/2017
ms.author: bradsev;
ms.openlocfilehash: 45d801bf0096879143f91feb230445625559379f
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/09/2017
---
# <a name="deployment"></a>Déploiement

Cet article présente les objectifs, tâches et livrables associés au déploiement du processus TDSP. Ce processus indique un cycle de vie recommandé que vous pouvez utiliser pour structurer vos projets de science des données. Le cycle de vie expose les principales phases que les projets exécutent généralement, souvent de manière itérative :

   1. **Présentation de l’entreprise**
   2. **Acquisition et compréhension des données**
   3. **Modélisation**
   4. **Déploiement**
   5. **Acceptation du client**

Voici une représentation visuelle du cycle de vie TDSP : 

![Cycle de vie TDSP](./media/lifecycle/tdsp-lifecycle2.png) 


## <a name="goal"></a>Objectif
Déployer des modèles comportant un pipeline de données dans un environnement de production ou similaire en vue de leur acceptation par l’utilisateur final. 

## <a name="how-to-do-it"></a>Marche à suivre
Une tâche principale est traitée dans cette phase :

**Faire fonctionner le modèle** : déployez le modèle et le pipeline sur un environnement de production ou similaire en vue de l’utilisation de l’application.

### <a name="operationalize-a-model"></a>Faire fonctionner un modèle
Une fois que votre ensemble de modèles fonctionne correctement, vous pouvez l’utiliser pour les autres applications. En fonction des exigences de l’entreprise, les prédictions sont faites en temps réel ou par lot. Pour déployer des modèles, vous les exposez avec une interface API ouverte. Cette interface permet au modèle d’être facilement utilisé dans différentes applications :

   * Sites web en ligne
   * Tableurs 
   * Tableaux de bord
   * applications métier ; 
   * Applications principales 

Pour obtenir des exemples de mise en œuvre de modèle avec un service web Azure Machine Learning, consultez [Déploiement d’un service web Azure Machine Learning](../studio/publish-a-machine-learning-web-service.md). Il est recommandé de générer des données de télémétrie et de surveillance dans le modèle de production et le pipeline de données que vous déployez. Cette pratique facilite la création de rapports sur l’état subséquent du système et le dépannage de ce dernier.  

## <a name="artifacts"></a>Artefacts

* Tableau de bord d’état affichant les mesures clés et l’intégrité du système
* Rapport de modélisation final contenant les détails du déploiement
* Document final de l’architecture de la solution


## <a name="next-steps"></a>Étapes suivantes

Voici les liens vers chaque étape du cycle de vie TDSP :

   1. [Présentation de l’entreprise](lifecycle-business-understanding.md)
   2. [Acquisition et compréhension des données](lifecycle-data.md)
   3. [Modélisation](lifecycle-modeling.md)
   4. [Déploiement](lifecycle-deployment.md)
   5. [Acceptation du client](lifecycle-acceptance.md)

Nous indiquons des procédures pas à pas complètes qui illustrent toutes les étapes du processus correspondant à des scénarios spécifiques. L’article [Example walkthroughs](walkthroughs.md) (Exemples de procédures pas à pas) contient une liste des scénarios ainsi que des liens et des descriptions de miniatures. Les procédures pas à pas montrent comment combiner les outils et services dans le cloud et sur site dans un flux de travail ou un pipeline pour créer une application intelligente. 

Pour obtenir des exemples sur l’exécution de procédures dans les processus TDSP utilisant Azure Machine Learning Studio, consultez [Utilisation du processus de science des données avec Azure Machine Learning](http://aka.ms/datascienceprocess).
