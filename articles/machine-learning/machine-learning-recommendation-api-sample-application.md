---
title: "opérations aaaCommon Bonjour Machine Learning recommandations API | Documents Microsoft"
description: Exemple d'application Azure ML Recommendation
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>Procédure pas à pas d’exemple d’application d’API Recommendations
> [!NOTE]
> Vous devez commencer à l’aide de hello Service cognitifs de recommandations API au lieu de cette version. Hello Service cognitifs recommandations remplacera ce service et toutes les hello nouvelles fonctionnalités seront développées il. Il propose de nouvelles fonctionnalités telles que la prise en charge du traitement par lot, un meilleur Explorateur d’API, une surface d’API plus propre, une expérience d’inscription/de facturation plus cohérente, etc.
> En savoir plus sur [migration toohello nouveau Service cognitifs](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>Objectif
Ce document illustre l’utilisation de hello Hello Azure Machine Learning recommandations API via une [exemple d’application](https://code.msdn.microsoft.com/Recommendations-144df403).

Cette application n’est pas prévue tooinclude toutes les fonctionnalités, ni utilise-t-elle hello toutes les API. Il illustre certains tooperform opérations courantes lorsque vous souhaitez tout d’abord tooplay avec hello service de recommandation d’apprentissage. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a>Introduction tooMachine service de recommandation d’apprentissage
Recommandations via hello service de recommandation d’apprentissage sont activées lorsque vous générez un modèle de recommandation basé sur hello données suivantes :

* Un référentiel des éléments hello toorecommend, également connu en tant que catalogue
* Représentation de l’utilisation de hello d’éléments par l’utilisateur ou de session (Cela peut être acquis au fil du temps via l’acquisition de données, pas dans le cadre de l’application d’exemple hello) de données

Une fois un modèle de recommandation est généré, vous pouvez l’utiliser des éléments de toopredict un utilisateur d’intéresser, en fonction de tooa utilisateur sélectionne hello de jeu d’éléments (ou un élément unique).

tooenable hello scénario précédent, procédez comme suit hello dans hello service de recommandation d’apprentissage :

* Créer un modèle : il s’agit d’un conteneur logique qui contient les données hello (catalogue et utilisation) et les modèles de prédiction hello. Chaque conteneur de modèle est identifié par un identifiant unique attribué lors de sa création. Cet ID est appelé ID de modèle hello, et il est utilisé par la plupart des API de hello. 
* Télécharger toocatalog : création d’un conteneur de modèle, vous pouvez associer tooit un catalogue.

**Remarque**: création d’un modèle et le téléchargement de tooa catalogue sont généralement effectuées une seule fois pour le modèle du cycle de vie hello.

* Télécharger l’utilisation : cette opération ajoute le conteneur de modèle toohello l’utilisation des données.
* Générer un modèle de recommandation : une fois que vous avez suffisamment de données, vous pouvez générer le modèle de recommandation hello. Cette opération utilise hello supérieur apprentissage algorithmes toocreate un modèle de recommandation. Chaque génération est associée à un identifiant unique. Vous devez tookeep un enregistrement de cet ID, car il n’est nécessaire pour la fonctionnalité de hello de certaines API.
* Hello analyse processus de création : construction d’un modèle de recommandation est une opération asynchrone, et peut prendre plusieurs minutes tooseveral heures, selon la quantité de hello de données (catalogue et utilisation) et hello des paramètres de génération. Par conséquent, vous devez générer de hello toomonitor. Un modèle de recommandation est créé uniquement si sa génération associée est réalisée avec succès.
* (Facultatif) Choisissez la génération active d’un modèle de recommandation. Cette étape est nécessaire uniquement si vous avez associé plusieurs modèles de recommandation à votre conteneur de modèle. Les recommandations de tooget demande sans indiquer le modèle de recommandation active hello est automatiquement redirigée par hello toohello par défaut active la version du système. 

**Remarque**: un modèle de recommandation actif est prêt pour la production et est conçu pour une charge de production. Il diffère d’un modèle de recommandation non actif, qui reste dans un environnement similaire à celui d’un test (parfois appelé intermédiaire).

* Obtenez la recommandation : une fois que vous disposez d’un modèle de recommandation, vous pouvez déclencher la recommandation pour un seul élément ou pour une liste d’éléments que vous avez sélectionnés. 

En général, l'appel de la fonction Obtenez une recommandation dure un certain temps. Pendant cette période de temps, vous pouvez rediriger l’utilisation des données toohello système de recommandation d’apprentissage qui ajoute ce conteneur de modèle spécifié de toohello de données. Lorsque vous avez suffisamment de données d’utilisation, vous pouvez générer un nouveau modèle de recommandation qui incorpore des données d’utilisation supplémentaires hello. 

## <a name="prerequisites"></a>Composants requis
* Visual Studio 2013 ou une version ultérieure
* Accès à Internet 
* Abonnement toohello recommandations API (https://datamarket.azure.com/dataset/amla/recommendations).

## <a name="azure-machine-learning-sample-app-solution"></a>Solution de la version d’évaluation de l’application Azure Machine Learning
Cette solution contient le code source de hello, exemple d’utilisation, fichier de catalogue et directives toodownload hello packages qui sont requises pour la compilation.

## <a name="hello-apis-used"></a>Hello API utilisés
application Hello utilise la fonctionnalité de recommandation d’apprentissage grâce à un sous-ensemble d’API disponibles. Hello Qu'api suivantes sont illustrées dans l’application hello :

* Créer des modèles : créer un conteneur logique de toohold les modèles de données et des recommandations. Un modèle est identifié par un nom, et vous ne peut pas créer plusieurs modèles avec hello même nom.
* Télécharger le fichier catalogue : utilisez les données du catalogue tooupload.
* Télécharger le fichier d’utilisation : données tooupload sur l’utilisation.
* Déclencher la build : utilisez toocreate un modèle de recommandation.
* Surveiller l’exécution de la build : utilisation de l’état de hello toomonitor une recommandation de création du modèle.
* Choisissez un modèle de génération de recommandation : utiliser tooindicate le toouse de modèle de recommandation par défaut pour un certain conteneur de modèle. Cette étape est nécessaire uniquement si vous avez plusieurs modèles de recommandation et que vous souhaitez tooactivate non actif générer en tant que modèle de recommandation active hello.
* Obtenir la recommandation : utiliser tooretrieve éléments selon tooa fonction élément unique ou un ensemble d’éléments recommandé. 

Pour obtenir une description complète de hello API, consultez la documentation de Microsoft Azure Marketplace hello. 

**Remarque**: un modèle peut posséder plusieurs générations au fil du temps (pas simultanément). Chaque build est créée avec hello même ou à une mise à jour catalogue et les données d’utilisation supplémentaires.

## <a name="common-pitfalls"></a>Pièges courants
* Vous devez tooprovide votre nom d’utilisateur et votre application exemple hello de toorun clé de compte principal Microsoft Azure Marketplace.
* Exemple hello en cours d’exécution d’application de manière consécutive échoue. flux de l’application Hello inclut la création, de chargement, de création d’analyse de hello et de mise en route de recommandations à partir d’un modèle prédéfini ; Par conséquent, il échouera sur consécutives d’exécution si vous ne modifiez pas le nom du modèle hello entre les appels.
* Recommandation peut ne pas renvoyer de données. Hello, exemple d’application utilise un fichier de catalogue et d’utilisation très faible. Par conséquent, certains éléments du catalogue de hello n’aura aucune éléments recommandés.

## <a name="disclaimer"></a>Clause d'exclusion de responsabilité
exemple d’application Hello n’est pas prévue toobe s’exécutent dans un environnement de production. données Hello fournies dans le catalogue de hello sont très faible, et elle ne fournit pas d’un modèle de recommandation explicite. les données de salutation sont fournies comme une démonstration. 

