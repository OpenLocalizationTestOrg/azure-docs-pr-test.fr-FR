---
title: "aaaWhat est Azure Machine Learning Studio ? | Microsoft Docs"
description: "Vue d'ensemble d'Azure ML Studio, un outil de glisser-déplacer pour créer rapidement des modèles à partir d'une bibliothèque prête à l'emploi d'algorithmes et de modules."
keywords: azure machine learning,azure ml, ml studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a>Azure Machine Learning Studio - De quoi s'agit-il ?
Microsoft Azure Machine Learning Studio est un outil de collaboration, glisser-déplacer vous pouvez utiliser toobuild, tester et déployer des solutions d’analytique prédictive sur vos données. Machine Learning Studio publie des modèles en tant que services web pouvant facilement être consommés par des applications personnalisées ou des outils décisionnels tels qu'Excel.

Machine Learning Studio : là où convergent votre connaissance des données, l'analyse prédictive, les ressources cloud et vos données.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a>espace de travail interactive Hello Machine Learning Studio
toodevelop un modèle d’analyse prédictive, vous utilisez généralement les données à partir d’une ou plusieurs sources, transformer et analyser ces données via les diverses fonctions statistiques et de manipulation de données et générer un jeu de résultats. Le développement d'un modèle de ce type est un processus itératif. Lorsque vous modifiez des hello diverses fonctions et leurs paramètres, vos résultats de faire converger jusqu'à ce que vous êtes satisfait que vous disposez d’un modèle formé et efficace.

**Azure Machine Learning Studio** fournit vous un tooeasily de l’espace de travail interactive visual générez, tester et effectuer une itération sur un modèle d’analyse prédictive. Vous faites glisser-déposer ***datasets*** et analyse ***modules*** sur un canevas interactif, qui les connectent tooform ensemble un ***faire des essais***, exécutée dans l’apprentissage Studio. tooiterate sur la conception du modèle, vous modifiez l’expérience hello, enregistrer une copie si vous le souhaitez et exécutez à nouveau. Lorsque vous êtes prêt, vous pouvez convertir votre ***expérience de formation*** tooa ***expérience prédictive***, puis le publier en tant qu’un ***service web*** afin que votre modèle est accessible par d’autres utilisateurs.

Il n’existe aucune programmation n’est requise, simplement visuellement connexion tooconstruct de jeux de données et les modules de votre modèle d’analyse prédictive.

> [!TIP]
> toodownload et imprimer un diagramme qui donne une vue d’ensemble des fonctionnalités de hello de Machine Learning Studio, consultez [diagramme de vue d’ensemble des fonctionnalités d’Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
> 
> 

![Diagramme Azure ML Studio : créer des expériences, lire les données de nombreuses sources, écrire des données évaluées, écrire des modèles.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a>Prise en main de Machine Learning Studio
Lorsque vous entrez [Machine Learning Studio](https://studio.azureml.net) vous consultez hello **accueil** page. À partir de là, vous pouvez afficher la documentation, des vidéos, des webinaires et rechercher d’autres ressources précieuses.

Cliquez sur le menu de gauche hello ![Menu](media/machine-learning-what-is-ml-studio/menu.png) pour voir apparaître différentes options.

### <a name="cortana-intelligence"></a>Cortana Intelligence
Cliquez sur **Cortana Intelligence** et vous serez dirigé toohello page d’accueil de hello [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite). Hello Cortana Intelligence Suite est de type données big entièrement gérées et avancé analytique suite tootransform vos données en action intelligente. Consultez la page d’accueil Suite hello pour une documentation complète, y compris les expériences clients.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Il existe deux options ici, **accueil**, page hello où vous avez démarré, et **Studio**.

Cliquez sur **Studio** et vous serez dirigé toohello **Azure Machine Learning Studio**. Tout d’abord vous inviterons toosign à l’aide de votre compte Microsoft ou votre compte professionnel ou scolaire. Une fois connecté, vous verrez hello suivant des onglets de hello gauche :

* **PROJETS** - Collections d’expériences, de DataSets, de notebooks et d’autres ressources représentant un projet spécifique
* **EXPÉRIENCES** : expériences que vous avez créées et exécutées ou enregistrées comme brouillons
* **SERVICES WEB** : services que vous avez déployés à partir de vos expériences web
* **NOTEBOOKS** : notebooks Jupyter que vous avez créés
* **JEUX DE DONNÉES** : jeux de données que vous avez téléchargés dans Studio
* **MODÈLES FORMÉS** : modèles que vous avez formés dans les expériences, puis enregistrés dans Studio
* **PARAMÈTRES** -une collection de paramètres que vous pouvez utiliser tooconfigure votre compte et vos ressources.

### <a name="gallery"></a>Galerie
Cliquez sur **galerie** et vous serez dirigé toohello  **[Cortana Intelligence galerie](http://gallery.cortanaintelligence.com/)**. Hello galerie est l’endroit où une Communauté de chercheurs de données et les développeurs partagent des solutions créées à l’aide de composants de hello Cortana Intelligence Suite.

Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir les solutions de hello Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).

## <a name="components-of-an-experiment"></a>Composants d'une expérience
Une expérience se compose de datasets qui fournissent des données tooanalytical modules, ce qui vous interconnecter tooconstruct un modèle d’analyse prédictive. En particulier, une expérience valide a les caractéristiques suivantes :

* expérience de Hello a au moins un jeu de données et d’un module
* Jeux de données peut être connecté toomodules uniquement
* Modules peuvent être connecté tooeither de jeux de données ou d’autres modules
* Tous les ports d’entrée pour les modules doivent avoir une connexion de données de toohello flux
* Tous les paramètres obligatoires de chaque module doivent être configurés

Vous pouvez créer une expérience à partir de zéro, ou utiliser un exemple d’expérience existante comme modèle. Pour plus d’informations, consultez [toocreate nouvelles expériences d’apprentissage automatique exemple d'expériences](machine-learning-sample-experiments.md).

Pour obtenir un exemple de création d'une expérience simple, consultez la rubrique [Création d'une expérience simple dans Azure Machine Learning Studio](machine-learning-create-experiment.md).

Pour une description plus complète de la création d'une solution d'analyse prédictive, consultez la rubrique [Développement d'une solution prédictive avec Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="datasets"></a>JEUX DE DONNÉES
Un jeu de données est de données qui a été téléchargement tooMachine Learning Studio afin qu’il peut être utilisé dans le processus de modélisation de hello. Un nombre de jeux de données exemple est inclus avec Machine Learning Studio pour vous tooexperiment avec, et vous pouvez télécharger des jeux de données dont vous avez besoin. Voici quelques exemples de jeux de données fournis :

* **Données sur la quantité de litres au 100 pour différents véhicules automobiles** : valeurs de quantité de litres au 100 pour des automobiles identifiées par leur nombre de cylindres, leur puissance, etc.
* **Données sur le cancer du sein** : données de diagnostics sur le cancer du sein.
* **Données sur les feux de forêts** : tailles des incendies de forêts au nord-est du Portugal.

Lorsque vous générez une expérience vous pouvez choisir de liste de hello des datasets disponibles toohello à gauche de la zone de dessin hello.

Pour obtenir la liste des jeux de données exemple inclus dans Machine Learning Studio, consultez [utiliser des jeux de données d’exemple hello dans Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).

### <a name="modules"></a>Modules
Un module est un algorithme que vous appliquez à vos données. Machine Learning Studio a un nombre de modules allant de données entrée fonctions tootraining, le calcul de score et la validation des processus. Voici quelques exemples de modules fournis :

* [Convertir tooARFF] [ convert-to-arff] -convertit une jeu de données sérialisés .NET tooAttribute-Relation File Format ARFF ().
* [Statistiques de calcul élémentaires][elementary-statistics] : calcule des statistiques élémentaires (par exemple, moyenne, écart type, etc.).
* [Régression linéaire][linear-regression] : crée un modèle de régression linéaire à gradient décroissant en ligne.
* [Noter le modèle][score-model] : note un modèle de classification ou de régression formé.

Lorsque vous générez une expérience vous pouvez choisir parmi la liste hello des modules disponibles toohello à gauche de la zone de dessin hello.  

Un module peut avoir un ensemble de paramètres que vous pouvez utiliser les algorithmes internes du module tooconfigure hello. Lorsque vous sélectionnez un module dans la zone de dessin hello, les paramètres du module hello sont affichés dans hello **propriétés** toohello volet à droite de la zone de dessin hello. Vous pouvez modifier les paramètres hello dans ce volet de tootune votre modèle.

Pour certains aide Parcourir hello grande bibliothèque d’algorithmes d’apprentissage automatique disponibles, consultez [comment toochoose des algorithmes pour Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).

## <a name="deploying-a-predictive-analytics-web-service"></a>Déploiement d'un service web d'analyse prédictive
Une fois votre modèle d'analyse prédictive prêt, vous pouvez le déployer comme un service web directement à partir de Machine Learning Studio. Pour plus de détails sur ce processus, consultez [Déploiement d’un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
