---
title: aaaConnect tooa Service Web de Machine Learning | Documents Microsoft
description: "Avec c# ou Python, vous connecter tooan service Azure Machine Learning Web à l’aide d’une clé d’autorisation."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a>Se connecter tooan Service Web de Azure Machine Learning
Hello expérience des développeurs Azure Machine Learning est un Web service API toomake des prévisions à partir des données d’entrée en temps réel ou en mode batch. Vous utilisez des prédictions de toocreate Azure Machine Learning Studio et déployez un service Web de Azure Machine Learning.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

toolearn comment toocreate et déployer un service Web d’apprentissage Machine à l’aide de la Machine Learning Studio :

* Pour un didacticiel sur toocreate une expérience dans Machine Learning Studio, voir [créer votre première expérience](machine-learning-create-experiment.md).
* Pour plus d’informations sur la façon de toodeploy un service Web, consultez [déployer un service Web d’apprentissage Machine](machine-learning-publish-a-machine-learning-web-service.md).
* Pour plus d’informations sur la Machine Learning en général, visitez hello [centre de Documentation Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

## <a name="azure-machine-learning-web-service"></a>Service web Microsoft Azure Machine Learning
Avec hello service Azure Machine Learning Web, une application externe communique avec un modèle de score de flux de travail Machine Learning en temps réel. Un appel de service Web d’apprentissage Machine retourne des résultats de prédiction tooan des applications externes. toomake un appel de service Web de la Machine Learning, vous passez une clé d’API qui est créée lorsque vous déployez une prédiction. Hello service Web d’apprentissage Machine est basée sur REST, un choix d’architecture courante pour les projets de programmation web.

Microsoft Azure Machine Learning propose deux types de service :

* Le Service de requête-réponse (RR) – une faible latence, un service hautement évolutif qui fournit une interface toohello des modèles sans état créés et déployés à partir de hello Machine Learning Studio.
* Service d’exécution de lot (Batch Execution Service, BES) : service asynchrone qui effectue la notation d’un lot pour les enregistrements de données.

Pour plus d’informations sur les services web Machine Learning, consultez [Déployer un service web Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Obtenir une clé d’autorisation Microsoft Azure Machine Learning
Lorsque vous déployez votre expérience, les clés API sont générées pour hello service Web. Vous pouvez récupérer les clés de hello depuis plusieurs emplacements.

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>À partir du portail de Services Web de Microsoft Azure Machine Learning hello
Connectez-vous à toohello [les Services Web de Microsoft Azure Machine Learning](https://services.azureml.net) portal.

clé de hello API tooretrieve pour un service d’un site Web Machine Learning :

1. Dans le portail de Services Web de Azure Machine Learning hello, cliquez sur **Services Web** menu du haut hello.
2. Cliquez sur le service Web de hello pour lequel vous voulez tooretrieve hello.
3. Dans le menu supérieur de hello, cliquez sur **consommer**.
4. Copiez et enregistrez hello **clé primaire**.

clé de hello API tooretrieve pour un service Web d’apprentissage Machine classique :

1. Dans le portail de Services Web de Azure Machine Learning hello, cliquez sur **des Services Web classique** menu du haut hello.
2. Cliquez sur le service Web de hello avec lequel vous travaillez.
3. Cliquez sur le point de terminaison hello pour lequel vous voulez tooretrieve hello.
4. Dans le menu supérieur de hello, cliquez sur **consommer**.
5. Copiez et enregistrez hello **clé primaire**.

### <a name="classic-web-service"></a>Service web classique
 Vous pouvez également récupérer une clé pour un service Web classique à partir de la Machine Learning Studio ou hello portail Azure classic.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. Dans la Machine Learning Studio, cliquez sur **SERVICES WEB** sur hello gauche.
2. Cliquez sur un service web. Hello **clé API** sur hello **tableau de bord** onglet.

#### <a name="azure-classic-portal"></a>Portail Azure Classic
1. Cliquez sur **MACHINE LEARNING** sur hello gauche.
2. Cliquez sur espace hello dans lequel se trouve votre service Web.
3. Cliquez sur **SERVICES WEB**.
4. Cliquez sur un service web.
5. Cliquez sur un point de terminaison. Hello « Clé API » s’est arrêté à hello inférieur droit.

## <a id="connect"></a>Connecter tooa Machine Learning Web service
Vous pouvez vous connecter tooa service Web d’apprentissage Machine à l’aide de n’importe quel langage de programmation qui prend en charge de la réponse et requête HTTP. Vous pouvez consulter des exemples en C#, Python et R sur l’une des pages d’aide du service web Machine Learning.

**Aide de l’API Machine Learning** L’aide de l’API Machine Learning est créée quand vous déployez un service web. Consultez la page [Procédure pas à pas : déploiement du service web Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).
Hello aide des API d’apprentissage Machine contient des détails sur une service Web de prédiction.

1. Cliquez sur le service Web de hello avec lequel vous travaillez.
2. Cliquez sur le point de terminaison hello pour lequel vous souhaitez tooview hello Page d’aide API.
3. Dans le menu supérieur de hello, cliquez sur **consommer**.
4. Cliquez sur **page d’aide API** sous hello demande-réponse ou de points de terminaison de l’exécution par lots.

**aide de Machine Learning API tooview pour un service d’un site Web**

Bonjour portail de Services Web Azure Machine Learning :

1. Cliquez sur **SERVICES WEB** sur le menu du haut hello.
2. Cliquez sur le service Web de hello pour lequel vous voulez tooretrieve hello.

Cliquez sur **consommer** tooget hello URI pour hello Reposonse de demande et de Services d’exécution de lot exemple de code en c#, R et Python.

Cliquez sur **API de Swagger** tooget Swagger en fonction de documentation pour hello API appelée à partir de hello fourni URI.

### <a name="c-sample"></a>Exemple de code C#
tooconnect tooa service Machine Learning Web, utilisez un **HttpClient** passage ScoreData. ScoreData contient un FeatureVector, un vecteur de fonctionnalités numériques à n dimensions représente hello ScoreData. Vous authentifier le service de Machine Learning toohello avec une clé d’API.

tooconnect tooa service Web d’apprentissage Machine, hello **Microsoft.AspNet.WebApi.Client** le package NuGet doit être installé.

**Installer le package NuGet Microsoft.AspNet.WebApi.Client dans Microsoft Visual Studio**

1. Publier le dataset téléchargement hello UCI : 2 adulte classe dataset Service Web.
2. Cliquez sur **Outils** > **Gestionnaire de package NuGet** > **Console du gestionnaire de package**.
3. Choisissez l'élément **Install-Package Microsoft.AspNet.WebApi.Client**.

**exemple de code hello toorun**

1. Publier « exemple 1 : télécharger le jeu de données à partir de UCI : adulte 2 classe dataset « expérience, de la part de hello, exemple de collection de Machine Learning.
2. Affecter apiKey avec la clé de hello à partir d’un service Web. Consultez **Obtenir une clé d’autorisation Microsoft Azure Machine Learning** plus haut.
3. Affecter serviceUri avec hello URI de requête.

### <a name="python-sample"></a>Exemple de code Python
tooconnect tooa service Machine Learning Web, utilisez hello **urllib2** ScoreData de passage de bibliothèque. ScoreData contient un FeatureVector, un vecteur de fonctionnalités numériques à n dimensions représente hello ScoreData. Vous authentifier le service de Machine Learning toohello avec une clé d’API.

**exemple de code hello toorun**

1. Déployer « exemple 1 : télécharger le jeu de données à partir de UCI : adulte 2 classe dataset « expérience, de la part de hello, exemple de collection de Machine Learning.
2. Affecter apiKey avec la clé de hello à partir d’un service Web. Consultez hello **obtenir une clé d’autorisation d’Azure Machine Learning** section près de début de hello de cet article.
3. Affecter serviceUri avec hello URI de requête.

