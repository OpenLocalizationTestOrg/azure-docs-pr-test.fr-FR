---
title: "aaaHow un modèle Azure Machine Learning devient un service web | Documents Microsoft"
description: "Une vue d’ensemble des mécanismes de hello de la façon dont votre progresse de modèle Azure Machine Learning à partir d’un développement expérimenter tooan mis service Web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 25e0c025-f8b0-44ab-beaf-d0f2d485eb91
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 2bbe09fa8fa22662cf8ec4a8b6249d23c87c8ddf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-a-machine-learning-model-progresses-from-an-experiment-tooan-operationalized-web-service"></a>Comment une passe de modèle d’apprentissage à partir d’une expérience de tooan mis service Web
Azure Machine Learning Studio fournit une zone interactive qui vous permet de toodevelop, exécuter, tester et itérer un ***expérimenter*** représentant un modèle d’analyse prédictive. Il existe un large éventail de modules capables d’effectuer les opérations suivantes :

* Entrer des données dans votre expérience
* Manipuler des données de hello
* Former un modèle à l’aide d’algorithmes d’apprentissage automatique
* Modèle de score hello
* Évaluer les résultats de hello
* Sortir les valeurs finales

Une fois que vous êtes satisfait de votre expérience, vous pouvez la déployer en tant que ***service web Azure Machine Learning classique*** ou ***nouveau service web Azure Machine Learning*** afin de permettre aux utilisateurs d’envoyer de nouvelles données et de recevoir les résultats en retour.

Dans cet article, nous donnent une vue d’ensemble des mécanismes de hello de la façon dont votre change de modèle d’apprentissage d’un tooan d’expérience de développement mis service Web.

> [!NOTE]
> Il existe autres façons toodevelop et déployer des modèles d’apprentissage automatique, mais cet article se concentre sur l’utilisation de Machine Learning Studio. Par exemple, tooread une description de la façon dont toocreate un service Web de prédictive classique avec R, consultez hello billet de blog [Build & déployer prédictive Web applications à l’aide de RStudio et Azure ML](http://blogs.technet.com/b/machinelearning/archive/2015/09/25/build-and-deploy-a-predictive-web-app-using-rstudio-and-azure-ml.aspx).
> 
> 

Alors que Azure Machine Learning Studio est conçue toohelp vous développer et déployer un *modèle d’analyse prédictive*, il est possible de toouse Studio toodevelop une expérience qui n’inclut pas un modèle d’analyse prédictive. Par exemple, une expérience peut-être simplement d’entrée de données, manipuler, puis la sortie des résultats hello. Tout comme une expérience d’analyse prédictive, vous pouvez déployer cette expérience non prédictive comme un service Web, mais il est plus simple, car l’expérience de hello n’est pas de formation ou d’évaluation d’un modèle d’apprentissage. S’il n’est pas hello toouse Studio classiques de cette façon, nous allons l’inclure dans la discussion de hello afin que nous pouvons obtenir une explication complète du fonctionne de Studio.

## <a name="developing-and-deploying-a-predictive-web-service"></a>Développement et déploiement d’un service web prédictif
Voici les étapes hello une solution classique suivant lors du développement et de déployer à l’aide de la Machine Learning Studio :

![Flux de déploiement](media/machine-learning-model-progression-experiment-to-web-service/model-stages-from-experiment-to-web-service.png)

*Figure 1 : Étapes d’un modèle d’analyse prédictive classique*

### <a name="hello-training-experiment"></a>expérience de formation Hello
Hello ***expérience de formation*** est la phase initiale de hello du développement de votre service Web dans Machine Learning Studio. Hello expérience de formation hello vise toogive un toodevelop sur place, test, effectuer une itération et finalement l’apprentissage d’un modèle d’apprentissage. Vous pouvez même former plusieurs modèles simultanément que vous recherchez la solution la mieux adaptée hello, mais une fois que vous avez terminé l’expérimentation vous devez sélectionner un seul objet d’un apprentissage de modèle et éliminer reste hello à partir de l’expérience de hello. Pour obtenir un exemple de développement d’une expérience d’analyse prédictive, consultez [Guide pas à pas : développer une solution d’analyse prédictive pour l’évaluation des risques de crédit dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="hello-predictive-experiment"></a>expérience de prédictive Hello
Une fois que vous avez un modèle formé dans votre expérience d’apprentissage, cliquez sur **configurer le Service Web** et sélectionnez **prédictive Web Service** dans le processus de hello Machine Learning Studio tooinitiate de conversion de votre formation faire des essais tooa ***expérience prédictive***. Hello d’objectif de l’expérience de prédictive hello est toouse votre modèle formé tooscore nouvelles données, avec comme objectif hello de mis devenant finalement comme un service Web Azure.

Cette conversion est effectuée automatiquement par le biais hello comme suit :

* Convertir le jeu hello de modules utilisés pour l’apprentissage dans un module unique et l’enregistrer comme un modèle formé
* Éliminer tous les modules superflus ne liés pas tooscoring
* Ajout de l’entrée et sortie hello éventuelle Web service va utiliser des ports

Il peut y avoir plusieurs modifications que vous souhaitez toomake tooget votre toodeploy prêt expérience prédictive comme un service Web. Par exemple, si vous souhaitez hello Web service toooutput uniquement un sous-ensemble des résultats, vous pouvez ajouter un module de filtrage avant de port de sortie hello.

Dans ce processus de conversion, expérience de formation hello n’est pas supprimée. Lorsque hello est terminée, vous avez deux onglets dans Studio : un pour expérience de formation hello et un pour une expérience de prédictive hello. Cette façon, que vous pouvez apporter des modifications expérience de formation toohello avant de déployer votre service Web et de reconstruire l’expérience de prédictive hello. Ou vous pouvez enregistrer une copie de hello formation expérience toostart une autre ligne d’expérimentation.

> [!NOTE]
> Lorsque vous cliquez sur **prédictive Service Web** que vous démarrez un processus automatique de tooconvert votre expérience prédictive de formation expérience tooa et cela fonctionne bien dans la plupart des cas. Si votre expérience d’apprentissage est complexe (par exemple, si vous avez plusieurs chemins d’accès pour l’apprentissage vous joignez), vous préférerez peut-être toodo cette conversion manuellement. Pour plus d’informations, consultez [comment tooprepare votre modèle pour le déploiement dans Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).
> 
> 

### <a name="hello-web-service"></a>Hello service Web
Une fois que vous êtes satisfait et que votre expérience prédictive est prête, vous pouvez déployer votre service en tant que service web classique ou nouveau service web basé sur Azure Resource Manager. toooperationalize votre modèle en le déployant comme un *service Web d’apprentissage Machine classique*, cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [standard]**. toodeploy en tant que *service d’un site Web Machine Learning*, cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [nouveau]**. Les utilisateurs peuvent désormais envoyer le modèle de tooyour de données à l’aide des API REST du service Web hello et recevoir les résultats de retour hello. Pour plus d’informations, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

## <a name="hello-non-typical-case-creating-a-non-predictive-web-service"></a>Hello cas non typique : création d’un service Web non prédictive
Si votre expérience ne pas effectuer l’apprentissage d’un modèle d’analyse prédictive, puis que vous n’avez pas besoin toocreate une expérience d’apprentissage et une expérience de score - il est simplement une expérience, et vous pouvez le déployer comme un service Web. Machine Learning Studio détecte si votre expérience contient un modèle prédictif en analysant les modules hello que vous avez utilisé.

Une fois que vous avez parcouru votre expérience et que vous la jugez satisfaisante :

1. Cliquez sur **Configurer le service web**, puis sélectionnez **Reformation du service web** : les nœuds d’entrée et de sortie sont automatiquement ajoutés.
2. Cliquez sur **Exécuter**.
3. Cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [standard]** ou **déployer le Service Web [nouveau]** selon hello environnement toowhich vous souhaitez toodeploy.

Votre service web est désormais déployé, et vous pouvez y accéder et le gérer de la même manière qu’un service web prédictif.

## <a name="updating-your-web-service"></a>Mise à jour de votre service web
Maintenant que vous avez déployé votre expérience en tant qu’un service Web, que se passe-t-il si vous devez tooupdate il ?

Cela dépend de ce que vous devez tooupdate :

**Toochange hello entrée ou sortie, ou de vous toomodify comment hello service Web manipule les données**

Si vous ne modifiez pas le modèle de hello, mais que vous modifiez simplement comment hello service Web gère les données, vous pouvez modifier l’expérience de prédictive hello et puis cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [standard]** ou **déployer le Service Web [nouveau]** à nouveau. Hello service Web est arrêté, hello expérience prédictive mis à jour est déployée et hello service Web est redémarré.

Voici un exemple : supposons que votre expérience prédictive retourne hello toute ligne de données d’entrée avec hello prédit les résultats. Vous pouvez décider que vous souhaitez le résultat de retour hello toojust hello Web service. Vous pouvez donc ajouter un **Project Columns** module dans expérience prédictive de hello, juste avant que le port de sortie hello tooexclude des colonnes autres que hello entraîner. Lorsque vous cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [standard]** ou **déployer le Service Web [nouveau]** , hello service Web est mis à jour.

**Vous souhaitez que le modèle de hello tooretrain avec de nouvelles données**

Si vous le souhaitez tookeep votre modèle d’apprentissage, mais que vous aimeriez tooretrain il avec de nouvelles données, vous avez deux possibilités :

1. **Recycler le modèle de hello pendant l’exécution de service Web de hello** -si vous souhaitez tooretrain votre modèle en cours service Web prédictif de hello, cela en apportant quelques modifications toohello formation expérience toomake il un *** expérience de recyclage***, puis vous pouvez le déployer en tant qu’un  ***web reconversion* service**. Pour obtenir des instructions sur la façon de toodo, consultez [recycler l’apprentissage des modèles par programme](machine-learning-retrain-models-programmatically.md).
2. **Revenir en arrière expérience d’apprentissage d’origine toohello et utiliser d’apprentissage différentes données toodevelop votre modèle** - votre expérience prédictive est lié toohello service Web, mais expérience de formation hello n’est pas directement liée de cette façon. Si vous modifiez l’expérience d’apprentissage d’origine hello et cliquez sur **configurer le Service Web**, il créera un *nouveau* prédictive expérimenter qui, lors du déploiement, créera un *nouveau* Web service. Il ne simplement mettre le service Web d’origine de hello.
   
   Si vous avez besoin d’expérience de formation toomodify hello, ouvrez-le et cliquez sur **enregistrer en tant que** toomake une copie. Cela rend l’expérience d’apprentissage d’origine intact hello expérience prédictive et service Web. Vous pouvez désormais créer un service web avec vos modifications. Une fois que vous avez déployé un service Web hello, vous pouvez alors décider si toostop hello service Web précédent ou qu’il soit en cours d’exécution en même temps que hello nouveau.

**Vous voulez tootrain un modèle différent**

Si vous souhaitez toomake modifie l’expérience de prédictive tooyour d’origine, telles que la sélection d’un algorithme d’apprentissage différentes lors de la tentative d’apprentissage différentes PROCÉDÉ, etc., vous devez toofollow hello deuxième décrite ci-dessus à instruire de nouveau votre modèle : Ouvrez l’expérience de formation hello, cliquez sur **enregistrer en tant que** toomake une copie et commencez à bas hello nouveau chemin de développer votre modèle, la création d’expérience de prédictive hello et le déploiement de service web hello. Cette opération crée un nouveau service Web non toohello d’origine, vous pouvez décider quels tookeep un, ou les deux, en cours d’exécution.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les processus de hello de développement et d’expérience, consultez hello suivant des articles :

* conversion d’expérience de hello - [comment tooprepare votre modèle pour le déploiement dans Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md)
* déploiement de service hello - [déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* modèle de la reconversion hello - [recycler l’apprentissage des modèles par programme](machine-learning-retrain-models-programmatically.md)

Pour obtenir des exemples de l’ensemble du processus hello, consultez :

* [Didacticiel sur l'apprentissage automatique : création de votre première expérience dans Azure Machine Learning Studio](machine-learning-create-experiment.md)
* [Guide pas à pas : développer une solution d’analyse prédictive pour l’évaluation des risques de crédit dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

