---
title: "aaaHow tooprepare votre modèle pour le déploiement dans Azure Machine Learning Studio | Documents Microsoft"
description: "Comment tooprepare votre modèle formé pour le déploiement sous la forme d’un site web de service en convertissant votre apprentissage Machine Learning Studio expérimenter expérience prédictive de tooa."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: d25bc68be63679a803bfc24a9e29e009a9263f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprepare-your-model-for-deployment-in-azure-machine-learning-studio"></a>Comment tooprepare votre modèle pour le déploiement dans Azure Machine Learning Studio

Azure propose de Machine Learning Studio que vous hello outils dont vous devez toodevelop un modèle prédictif analytique et puis de le mettre en la déployant en tant que service web Azure.

toodo, vous utilisez Studio toocreate une expérience - appelée un *expérience de formation* - où vous l’apprentissage, évaluer et modifier votre modèle. Une fois que vous êtes satisfait, vous obtenez votre toodeploy prêt de modèle en convertissant votre tooa d’expérience de formation *expérience prédictive* qui a configuré les données de l’utilisateur tooscore.

Vous trouverez un exemple de ce processus à la page [Procédure pas à pas : développer une solution d’analyse prédictive pour l’évaluation des risques de crédit dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

Cet article est une présentation approfondie les détails de hello de la façon dont une expérience d’apprentissage est convertie en une expérience prédictive et comment cette expérience prédictive est déployé. En comprenant les détails suivants, vous allez apprendre comment tooconfigure votre toomake modèle déployé il est plus efficace.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Vue d'ensemble 

processus de Hello de conversion d’une expérience prédictive de formation expérience tooa implique trois étapes :

1. Remplacez les modules de l’algorithme avec votre modèle formé d’apprentissage hello.
2. Trim hello expérience tooonly les modules qui sont nécessaires pour calculer les scores. Une expérience de formation inclut un nombre de modules qui sont nécessaires pour l’apprentissage, mais ne sont pas nécessaires une fois que l’apprentissage du modèle hello.
3. Définir comment votre modèle accepte les données à partir de l’utilisateur du service web hello et quelles données seront retournées.

> [!TIP]
> Dans votre expérience de formation, vous vous êtes concentré sur la formation et la notation de votre modèle avec vos propres données. Mais une fois déployé, les utilisateurs peuvent envoyer le nouveau modèle de données tooyour et il retourne les résultats de prédiction. Par conséquent, lorsque vous convertissez votre expérience de formation tooa tooget prédictive expérience qu’il est prêt pour le déploiement, gardez à l’esprit comment hello modèle sera utilisé par d’autres.
> 
> 

## <a name="set-up-web-service-button"></a>Définir le bouton de service web
Après avoir exécuté votre expérience (cliquez sur **exécuter** bas hello du canevas de l’expérience hello), cliquez sur hello **configurer le Service Web** bouton (sélectionnez hello **prédictive Service Web** option). **Configurer le Service Web** effectue pour hello de trois étapes de conversion de votre expérience de prédictive de tooa expérience d’apprentissage :

1. Elle enregistre votre modèle formé dans hello **modèles formés** section de la palette de module hello (toohello à gauche du canevas de l’expérience hello). Il remplace ensuite l’algorithme d’apprentissage automatique hello et [Train Model] [ train-model] modèle de modules avec hello enregistré formés.
2. Il analyse votre expérience et supprime les modules qui ont clairement été utilisés exclusivement pour la formation et ne sont plus nécessaires.
3. Il insère les modules _Web service input_ et de _Web service output_ aux emplacements par défaut de votre expérience (ces modules acceptent et renvoient des données utilisateur).

Par exemple, suivant de hello expérimenter trains un modèle d’arbre de décision augmentés de deux classes à l’aide des exemples de données de recensement :

![expérience de formation][figure1]

modules Hello dans cette expérience des fonctions en fait quatre différentes :

![Fonctions du module][figure2]

Lorsque vous convertissez cette expérience prédictive de formation expérience tooa, certaines de ces modules ne sont plus nécessaires ou qu’elles servent maintenant un objectif différent :

* **Données** -données hello dans cet exemple de dataset ne sont pas utilisées lors de la notation - utilisateur hello du service web de hello fournira hello toobe de données au score calculé. Toutefois, hello des métadonnées à partir de ce jeu de données, tels que des types de données, sont utilisée par le modèle formé de hello. Vous avez besoin de jeu de données tookeep hello dans expérience prédictive de hello afin qu’il puisse fournir ces métadonnées.

* **Préparation du** - en fonction des données utilisateur hello qui seront soumises pour calculer les scores, ces modules peuvent être ou non nécessaires tooprocess les données entrantes hello. Hello **configurer le Service Web** bouton ne touche pas ces - vous devez toodecide comment vous souhaitez que toohandle les.
  
    Par exemple, dans cet exemple hello échantillon de dataset peut avoir des valeurs manquantes, par conséquent, un [Clean Missing Data] [ clean-missing-data] module a été inclus toodeal avec eux. En outre, jeu de données exemple hello inclut des colonnes qui ne sont pas de modèle de hello tootrain nécessaires. Par conséquent, un [sélectionner les colonnes dans le jeu de données] [ select-columns] module a été inclus tooexclude ces colonnes supplémentaires de hello du flux de données. Si vous connaissez ces données hello qui seront soumises pour calculer les scores via hello service web n’aura pas les valeurs manquantes, puis vous pouvez supprimer hello [Clean Missing Data] [ clean-missing-data] module. Toutefois, puisque hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module permet de définir des colonnes de hello de données attend ce modèle formé hello, tooremain a besoin de ce module.

* **Train** -ces modules sont le modèle de hello tootrain utilisé. Lorsque vous cliquez sur **configurer le Service Web**, ces modules sont remplacés par un seul module qui contient le modèle hello vous avez formé. Ce nouveau module est enregistré dans hello **modèles formés** section de la palette de module hello.

* **Score** : dans cet exemple, hello [données fractionnées] [ split] module est le flux de données hello toodivide utilisés dans les données de test et les données d’apprentissage. Dans l’expérience prédictive hello, nous ne mettons pas formation, donc [données fractionnées] [ split] peuvent être supprimés. De même, hello deuxième [Score Model] [ score-model] module et hello [modèle Evaluate] [ evaluate-model] module sont toocompare utilisé les résultats du test de hello données, ces modules ne sont pas nécessitent dans hello prédictive faire des essais. Hello restant [Score Model] [ score-model] module, toutefois, est nécessaire tooreturn un score de résultats via le service web de hello.

Voici comment notre exemple apparaît une fois que vous avez cliqué sur **Définir un service Web**:

![Expérience prédictive convertie][figure3]

Hello du travail effectué par **configurer le Service Web** peut être suffisamment tooprepare votre toobe expérience déployé comme un service web. Toutefois, vous souhaiterez peut-être toodo certains expérience tooyour spécifique de travail supplémentaires.

### <a name="adjust-input-and-output-modules"></a>Ajuster des modules d’entrée et de sortie
Dans votre expérience d’apprentissage, vous avez utilisé un jeu de données d’apprentissage et puis certaines tooget de traitement a hello les données dans un formulaire qui hello algorithme d’apprentissage automatique si nécessaire. Si les données hello attendues tooreceive via le service web de hello ne seront pas besoin de ce traitement, vous pouvez l’ignorer : connectez sortie hello Hello **module d’entrée du service Web** tooa autre module de votre expérience. données de l’utilisateur Hello arriveront maintenant dans le modèle hello à cet emplacement.

Par exemple, par défaut **configurer le Service Web** met hello **Web service entrée** module haut hello de votre flux de données, comme indiqué dans la figure hello ci-dessus. Mais nous pouvons positionner manuellement hello **Web service entrée** au-delà de modules de traitement des données hello :

![Entrée du service web mobile hello][figure4]

Hello les données d’entrée fournies par le biais hello service web passera désormais directement dans le module du modèle de Score hello sans prétraitement.

De même, par défaut **configurer le Service Web** met hello module de sortie de service Web bas hello de votre flux de données. Dans cet exemple, service web de hello retournera le résultat de hello utilisateur toohello de hello [Score Model] [ score-model] module, qui comprend le vecteur de données d’entrée complète hello plus hello score des résultats.
Toutefois, si vous préférez tooreturn quelque chose de différent, vous pouvez ajouter des modules supplémentaires avant hello **Web de sortie du service** module. 

Par exemple, n’entraîne la notation hello tooreturn et pas hello entière vecteur de données d’entrée, ajoutez un [sélectionner les colonnes dans le jeu de données] [ select-columns] tooexclude module toutes les colonnes sauf hello score des résultats. Puis déplacez hello **Web de sortie du service** sortie toohello de module de hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module. expérience de Hello ressemble à ceci :

![Déplacement de sortie du service web hello][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a>Ajouter ou supprimer des modules de traitement des données supplémentaires
Si votre expérience inclut un plus grand nombre de modules que nécessaire pour le calcul de la notation, vous pouvez en supprimer. Par exemple, étant donné que nous avons déplacé hello **Web service entrée** tooa de module pointe après hello modules de traitement des données, nous pouvons supprimer hello [Clean Missing Data] [ clean-missing-data] module à partir de expérience de prédictive Hello.

Notre expérience de notation ressemble à présent à ce qui suit :

![Suppression du module supplémentaire][figure6]


### <a name="add-optional-web-service-parameters"></a>Ajouter des paramètres de service web facultatifs
Dans certains cas, vous souhaiterez utilisateur hello tooallow votre comportement hello toochange du service web de modules lors de l’accès au service de hello. *Paramètres de Service Web* permettent de toodo cela.

Un exemple courant consiste à configurer un [importer des données] [ import-data] module donc utilisateur hello Hello déployé le service web peut spécifier une autre source de données lors de l’accès au service web de hello. Il est également possible de configurer un module [Exporter les données][export-data] de façon à spécifier une destination différente.

Vous pouvez définir des paramètres de service web et les associer à un ou plusieurs paramètres de module, en spécifiant s’ils sont obligatoires ou facultatifs. utilisateur Hello du service web de hello fournit des valeurs pour ces paramètres lors de l’accès au service de hello et actions du module hello sont modifiées en conséquence.

Pour plus d’informations sur les paramètres de Service Web sont et toouse, voir [utilisant les paramètres du Service Web Azure Machine Learning][webserviceparameters].

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-hello-predictive-experiment-as-a-web-service"></a>Déployer l’expérience de prédictive hello comme un service web
Maintenant que l’expérience de prédictive hello suffisamment préparé, vous pouvez le déployer en tant que service web Azure. À l’aide du service web de hello, les utilisateurs peuvent envoyer le modèle de données tooyour et modèle de hello retourne ses prédictions.

Pour plus d’informations sur le processus de déploiement complet hello, consultez [déployer un service web Azure Machine Learning][deploy]

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
