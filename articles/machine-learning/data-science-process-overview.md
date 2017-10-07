---
title: "vue d’ensemble du processus de science des données équipe aaaAzure | Documents Microsoft"
description: "Fournit des solutions un analytique toodeliver prédictive méthodologie de science des données et applications intelligentes."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a>Vue d’ensemble du processus TDSP (Team Data Science Process)

Hello, processus de science des données équipe (TDSP) est agile, des données itératives science méthodologie toodeliver analytique prédictive solutions et des applications intelligentes efficacement. Le processus TDSP permet d’améliorer la collaboration et l’apprentissage au sein des équipes. Il contient un Distiller hello meilleures pratiques et des structures à partir de Microsoft et d’autres dans l’industrie de hello qui facilitent la mise en œuvre réussie de hello initiatives de science des données. Hello vise toohelp sociétés exploiter pleinement les avantages hello leur programme analytique.

Cet article fournit une vue d’ensemble du processus TDSP et de ses principaux éléments. Nous fournir une description générique de processus hello qui peut être implémentée avec un large éventail d’outils. Une description plus détaillée des tâches du projet hello et des rôles impliqués dans hello du cycle de vie du processus de hello est fournie dans les rubriques associées supplémentaires. Conseils sur la façon dont les tooimplement hello TDSP à l’aide d’un ensemble spécifique d’outils de Microsoft et l’infrastructure que nous utilisons tooimplement hello TDSP dans nos équipes est également fourni.

## <a name="key-components-of-hello-tdsp"></a>Composants clés de hello TDSP

TDSP se compose de hello suivant composants clés :

- une définition du **cycle de vie de la science des données** ;
- une **structure de projet normalisée** ;
- une **Infrastructure et des ressources** pour les projets de science des données ;
- des **outils et utilitaires** pour mener à bien le projet.


## <a name="data-science-lifecycle"></a>Cycle de vie de la science des données

Hello, processus de science des données équipe (TDSP) fournit un développement de hello toostructure du cycle de vie de vos projets de science des données. cycle de vie Hello décrit les étapes de hello, à partir du début toofinish, que les projets suivent généralement lorsqu’elles sont exécutées.

Si vous utilisez un autre cycle de vie des données scientifiques, tel que [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) ou votre processus personnalisé de l’organisation, vous pouvez toujours utiliser hello basé sur des tâches TDSP dans le contexte de hello du développement de ces cycles de vie. À haut niveau, ces méthodologies ont beaucoup en commun. 

Ce cycle de vie a été conçu pour les projets de sciences des données intégrés à des applications intelligentes. Ces applications déploient des modèles d’apprentissage automatique ou d’intelligence artificielle pour l’analytique prédictive. Les projets de sciences des données exploratoires et les projets d’analytique ad hoc peuvent également tirer parti de ce processus. Mais dans ce cas certaines des étapes hello décrits pas forcément nécessaires.    

cycle de vie Hello TDSP se compose de cinq étapes majeures qui sont exécutées de manière itérative :

* **Présentation de l’entreprise**
* **Acquisition de données et compréhension**
* **Modélisation**
* **Déploiement**
* **Acceptation du client**

Voici une représentation visuelle de hello **cycle de vie des processus de science des données équipe**. 

![Cycle de vie du processus TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

Hello objectifs, des tâches et des artefacts de documentation pour chaque phase du cycle de vie hello dans TDSP sont décrits dans hello [cycle de vie des processus de science des données équipe](data-science-process-lifecycle.md) rubrique. Ces tâches et artefacts sont associés à des rôles de projet :

- Architecte de solution
- Chef de projet
- Scientifique des données
- Coordinateur de projet 

Hello diagramme suivant fournit un affichage de grille des tâches de hello (en bleu) et des artefacts (en vert) associés à chaque étape du cycle de vie hello (sur l’axe horizontal de hello) pour ces rôles (sur l’axe vertical de hello). 

![rôles-et-tâches-du-processus-TDSP](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a>Structure de projet normalisée

Fait de tous les projets partagent une structure de répertoire et utiliser des modèles pour les documents du projet facilite la pour hello équipe membres toofind plus d’informations sur leurs projets. Tous les documents et code sont stockés dans un système de contrôle de version (VCS) comme la collaboration d’équipe Git ou TFS Subversion tooenable. Suivi des tâches et des fonctionnalités dans un projet agile de suivi système, tel que Jira, Rally, Visual Studio Team Services permet de plus près de suivi de code hello pour les fonctionnalités individuelles. Ce suivi permet également de tooobtain équipes mieux les estimations de coût. TDSP recommande la création d’un référentiel distinct pour chaque projet sur hello VCS pour le contrôle de version, la sécurité des informations et la collaboration. Hello normalisé structure pour tous les projets permet de build institutionnelles connaissances de l’entreprise hello.

Nous fournissons des modèles de structure de dossiers hello et documents requis dans les emplacements standards. Cette structure de dossiers organise les fichiers hello qui contiennent du code pour l’exploration de données et de fonctionnalités et qui enregistrent les itérations de modèle. Ces modèles facilitent l’utilisation pour l’équipe membres toounderstand travail effectué par d’autres et tooadd nouveaux membres tooteams. Il est facile tooview et mettre à jour les modèles de document dans le format de markdown. Utilisez les listes de vérification de modèles tooprovide avec questions clés pour chaque tooinsure projet que problème de hello est bien défini et que ce livrables répondent à la qualité hello attendue. Voici quelques exemples :

- un problème d’entreprise projet charte toodocument hello et la portée du projet de hello
- structure de données des rapports toodocument hello et les statistiques de données brutes de hello
- hello de toodocument rapports de modèle dérivée des fonctionnalités
- des modèles de métriques de performances, par exemple les courbes ROC ou MSE.


![Répertoires TDSP](./media/data-science-process-overview/tdsp-dir-structure.png)

structure de répertoire Hello peut être cloné à partir de [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).

## <a name="infrastructure-and-resources-for-data-science-projects"></a>Infrastructure et ressources pour les projets de science des données

Le processus TDSP fournit des recommandations sur la gestion de l’infrastructure partagée d’analytique et de stockage, notamment :

- systèmes de fichiers cloud pour le stockage des jeux de données ; 
- bases de données
- clusters Big Data (Hadoop ou Spark) ; 
- services de Machine Learning. 

Hello analytique infrastructure de stockage et peut être dans le cloud de hello ou localement. C’est à cet endroit que sont stockés les jeux de données bruts et traités. Cette infrastructure permet de reproduire les analyses. Il permet également d’éviter la duplication, ce qui peut entraîner des tooinconsistencies et des coûts d’infrastructure inutiles. Des outils sont fournis tooprovision hello des ressources partagées, assurer leur suivi et permettre à chaque tooconnect de membre d’équipe toothose ressources en toute sécurité. Il est également recommandé que les participants au projet créent un environnement de calcul homogène. Différents membres de l’équipe pourront alors répliquer et valider les expériences.

Voici l’exemple d’une équipe qui travaille sur plusieurs projets et partage différents composants de l’infrastructure d’analytique cloud.

![Infrastructure TDSP](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a>Outils et utilitaires pour mener à bien le projet

Dans la plupart des organisations, il est difficile d’introduire des processus. Outils fournis le cycle de vie et le processus de science des données tooimplement hello améliorer tooand de barrières hello plus faible cohérence hello de leur adoption. TDSP fournit un ensemble initial de scripts et outils adoption toojump-début de TDSP au sein d’une équipe. Il permet également d’automatiser les tâches courantes de hello de cycle de vie de hello données scientifiques telles que l’exploration de données et modélisation de la ligne de base. Est une structure bien définie fournie pour les personnes toocontribute partagé des outils et utilitaires dans le référentiel de code partagé de leur équipe. Ces ressources peuvent être utilisées par d’autres projets dans l’équipe de hello ou de l’organisation de hello. TDSP prévoit également les contributions hello tooenable des outils et utilitaires toohello ensemble de la Communauté. utilitaires TDSP Hello peuvent être clonés à partir de [Github](https://github.com/Azure/Azure-TDSP-Utilities).


## <a name="next-steps"></a>Étapes suivantes

[Team processus de science des données : Rôles et des tâches](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) présente les rôles du personnel clé hello et leurs tâches associées pour une équipe de science des données qui standardise sur ce processus. 
