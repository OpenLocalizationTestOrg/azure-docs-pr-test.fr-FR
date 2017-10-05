---
title: "Utilisation d’un service web Azure Machine Learning | Microsoft Docs"
description: "Une fois qu’un service Machine Learning a été déployé, le service web RESTful mis à disposition peut être utilisé soit en tant que service de requête-réponse en temps réel, soit en tant que service d’exécution par lot."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: eec9f637b4b2306ab4a888dbd5ef5b9a021bcac5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-consume-an-azure-machine-learning-web-service"></a>Utilisation d’un service web Azure Machine Learning

Une fois que vous avez déployé un modèle prédictif Azure Machine Learning en tant que service Web, vous pouvez utiliser une API REST pour lui envoyer des données et obtenir des prédictions. Vous pouvez envoyer les données en temps réel ou par lot.

Vous trouverez des informations supplémentaires sur la création et le déploiement d’un service web Machine Learning à l’aide de Machine Learning Studio dans les pages suivantes :

* Pour accéder à un didacticiel sur la création d'une expérience dans Machine Learning Studio, consultez [Créer votre première expérience](machine-learning-create-experiment.md).
* Pour plus d’informations sur le déploiement d’un service web, consultez [Déployer un service web Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
* Pour plus d’informations sur Machine Learning en général, consultez le [Centre de documentation Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Vue d'ensemble
Grâce au service web Microsoft Azure Machine Learning, une application externe peut communiquer avec le modèle de notation de workflow Machine Learning et ce, en temps réel. Un appel du service web Machine Learning renvoie les résultats d’une prédiction à une application externe. Pour créer cet appel, vous transmettez une clé API créée quand vous déployez une prédiction. Le service web Machine Learning est basé sur l’architecture REST, souvent choisie pour les projets de programmation web.

Microsoft Azure Machine Learning propose deux types de service :

* Service de requête-réponse (Request-Response Service, RRS) : service hautement évolutif, à faible latence, qui constitue une interface pour les modèles sans état créés et déployés à partir de Machine Learning Studio.
* Service d’exécution de lot (Batch Execution Service, BES) : service asynchrone qui effectue la notation d’un lot pour les enregistrements de données.

Pour plus d’informations sur les services web Machine Learning, consultez [Déployer un service web Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Obtenir une clé d’autorisation Microsoft Azure Machine Learning
Quand vous déployez votre expérimentation, les clés API sont générées pour le service web. Vous pouvez récupérer les clés de plusieurs emplacements.

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a>À partir du portail des services web Microsoft Azure Machine Learning
Connectez-vous au [portail des services web Microsoft Azure Machine Learning](https://services.azureml.net).

Pour récupérer la clé API pour un nouveau service web Machine Learning :

1. Dans le portail Services web Microsoft Azure Machine Learning, cliquez sur **Services web** dans le menu du haut.
2. Cliquez sur le service web pour lequel vous souhaitez récupérer la clé.
3. Cliquez sur **Consommer**dans le menu du haut.
4. Copiez et enregistrez la **clé primaire**.

Pour récupérer la clé API pour un service web Machine Learning classique :

1. Dans le portail Services web Microsoft Azure Machine Learning, cliquez sur **Services web classiques** dans le menu du haut.
2. Cliquez sur le service web que vous utilisez.
3. Cliquez sur le point de terminaison pour lequel vous souhaitez récupérer la clé.
4. Cliquez sur **Consommer**dans le menu du haut.
5. Copiez et enregistrez la **clé primaire**.

### <a name="classic-web-service"></a>Service web classique
 Vous pouvez également récupérer une clé pour un service web classique par le biais de Machine Learning Studio ou du portail Azure Classic.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. Dans Machine Learning Studio, cliquez sur l’option **SERVICES WEB** figurant sur la gauche.
2. Cliquez sur un service web. La **clé API** figure sur l’onglet **TABLEAU DE BORD**.

#### <a name="azure-classic-portal"></a>Portail Azure Classic
1. Cliquez sur l’option **MACHINE LEARNING** figurant sur la gauche.
2. Cliquez sur l’espace de travail dans lequel se trouve votre service web.
3. Cliquez sur **SERVICES WEB**.
4. Cliquez sur un service web.
5. Cliquez sur un point de terminaison. La « CLÉ API » se trouve sur la partie inférieure droite de la fenêtre.

## <a id="connect"></a>Se connecter à un service web Machine Learning
Vous pouvez vous connecter à un service web Machine Learning à l’aide de n’importe quel langage de programmation qui prend en charge les requêtes et réponses HTTP. Vous pouvez consulter des exemples en C#, Python et R sur l’une des pages d’aide du service web Machine Learning.

**Aide de l’API Machine Learning** L’aide de l’API Machine Learning est créée quand vous déployez un service web. Consultez la page [Procédure pas à pas : déploiement du service web Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).
L’aide sur l’API Machine Learning contient des détails sur un service web de prédiction.

1. Cliquez sur le service web que vous utilisez.
2. Cliquez sur le point de terminaison pour lequel vous souhaitez afficher la page d’aide de l’API.
3. Cliquez sur **Consommer**dans le menu du haut.
4. Cliquez sur la **page d’aide de l’API** sous le point de terminaison Requête-réponse ou Exécution par lot.

**Pour afficher l’aide de l’API Machine Learning pour un nouveau service web**

Dans le portail des services web Azure Machine Learning :

1. Cliquez sur **SERVICES WEB** dans le menu du haut.
2. Cliquez sur le service web pour lequel vous souhaitez récupérer la clé.

Cliquez sur **Consommer** pour obtenir l’URI des services requête-réponse et d’exécution par lots et des exemples de code en C#, R et Python.

Cliquez sur **API Swagger** pour obtenir une documentation basée sur Swagger pour les API appelées à partir de l’URI fourni.

### <a name="c-sample"></a>Exemple de code C#
Pour vous connecter à un service web Machine Learning, utilisez un **HttpClient** qui transmet l’élément ScoreData. ScoreData contient un FeatureVector, un vecteur à n dimensions des fonctionnalités numériques qui représente le ScoreData. Vous vous authentifiez auprès du service Machine Learning au moyen d’une clé API.

Pour vous connecter à un service web Machine Learning, le package NuGet **Microsoft.AspNet.WebApi.Client** doit être installé.

**Installer le package NuGet Microsoft.AspNet.WebApi.Client dans Microsoft Visual Studio**

1. Publiez le service web « Téléchargement d’un jeu de données depuis l’UCI : jeu de données de classe Adult 2 ».
2. Cliquez sur **Outils** > **Gestionnaire de package NuGet** > **Console du gestionnaire de package**.
3. Choisissez l'élément **Install-Package Microsoft.AspNet.WebApi.Client**.

**Pour exécuter l’exemple de code**

1. Publiez l’expérience « Exemple 1 : Téléchargement d’un jeu de données depuis l’UCI : jeu de données de classe Adult 2 », inclus dans la collection d’exemples Machine Learning.
2. Attribuez l’élément apiKey avec la clé à partir d’un service web. Consultez **Obtenir une clé d’autorisation Microsoft Azure Machine Learning** plus haut.
3. Affectez l’élément serviceUri avec l’URI de requête.

### <a name="python-sample"></a>Exemple de code Python
Pour vous connecter à un service web Machine Learning, utilisez la bibliothèque **urllib2** qui transmet l’élément ScoreData. ScoreData contient un FeatureVector, vecteur à n dimensions des fonctionnalités numériques qui représente le ScoreData. Vous vous authentifiez auprès du service Machine Learning au moyen d’une clé API.

**Pour exécuter l’exemple de code**

1. Déployez l’expérience « Exemple 1 : Téléchargement d’un jeu de données depuis l’UCI : jeu de données de classe Adult 2 », inclus dans la collection d’exemples Machine Learning.
2. Attribuez l’élément apiKey avec la clé à partir d’un service web. Consultez la section **Obtenir une clé d’autorisation Microsoft Azure Machine Learning** au début de cet article.
3. Affectez l’élément serviceUri avec l’URI de requête.

