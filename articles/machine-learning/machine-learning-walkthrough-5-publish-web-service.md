---
title: "Étape 5 : Déployer le service web de Machine Learning hello | Documents Microsoft"
description: "Étape 5 de hello développer la procédure pas à pas une solution prédictive : déployer une expérience prédictive dans Machine Learning Studio en tant qu’un service web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a>Procédure pas à pas, étape 5 : Déployer le service web de Azure Machine Learning hello
Voici la cinquième étape de hello hello procédure pas à pas, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Créer un espace de travail Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Télécharger des données existantes](machine-learning-walkthrough-2-upload-data.md)
3. [Créer une expérience](machine-learning-walkthrough-3-create-new-experiment.md)
4. [L’apprentissage et évaluer des modèles de hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. **Déployer le service web de hello**
6. [Service d’accès hello web](machine-learning-walkthrough-6-access-web-service.md)

- - -
toogive d’autres une chance toouse hello modèle prédictif, nous avons développé dans cette procédure pas à pas, nous pouvons déployer en tant que service web sur Azure.

Point de toothis nous avons testé avec notre modèle d’apprentissage. Mais service de hello déployé n’est plus va toodo formation - il va toogenerate nouvelles prédictions par hello l’entrée d’utilisateur en fonction de notre modèle de score. Nous allons toodo certains tooconvert préparation cela faire des essais d’un ***formation*** expérimenter tooa ***prédictive*** faire des essais. 

Ce processus comprend trois étapes :  

1. Supprimez l’un des modèles de hello
2. Convertir hello *expérience de formation* , nous avons créé dans un *expérience prédictive*
3. Déployer l’expérience de prédictive hello comme un service web

## <a name="remove-one-of-hello-models"></a>Supprimez l’un des modèles de hello

Tout d’abord, nous devons tootrim cette expérience vers le bas un peu. Actuellement, nous avons deux modèles différents dans une expérience de hello, mais nous voulons uniquement toouse un modèle lors du déploiement de cela comme un service web.  

Supposons que nous avons décidé de ce modèle d’arbre hello augmenté effectuée de meilleures performances que le modèle SVM hello. Hello première chose toodo est remove hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] module et modules hello qui ont été utilisés pour la formation. Vous souhaiterez peut-être toomake une copie de l’expérience de hello tout d’abord en cliquant sur **Enregistrer sous** bas hello hello expérimenter la zone de dessin.

Nous devons hello toodelete suivant des modules :  

* [Machine à vecteurs de support à deux classes][two-class-support-vector-machine]
* [L’apprentissage du modèle] [ train-model] et [Score Model] [ score-model] modules qui ont été connecté tooit
* [Normaliser les données][normalize-data] (les deux)
* [Évaluation du modèle] [ evaluate-model] (étant donné que nous avons terminé l’évaluation de modèles de hello)

Sélectionnez chaque module et appuyez sur la touche SUPPR de hello ou un module de hello avec le bouton droit et sélectionnez **supprimer**. 

![Supprimer le modèle SVM hello][3a]

Notre modèle doit alors ressembler à ceci :

![Supprimer le modèle SVM hello][3]

Maintenant, nous sommes prêt toodeploy de ce modèle à l’aide de hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Convertir l’expérience prédictive des tooa expérience d’apprentissage hello

tooget de ce modèle prêt pour le déploiement, nous devons tooconvert cette expérience de prédictive tooa expérience d’apprentissage. Cela implique trois étapes :

1. Enregistrer le modèle hello nous avez formé, puis la remplacer nos modules d’apprentissage
2. Trim hello expérience tooremove modules qui ont été nécessaires uniquement pour l’apprentissage
3. Définir où service web de hello accepter l’entrée et où il génère une sortie de hello

Nous pourrions le faire manuellement, mais heureusement les trois étapes peuvent être accomplies en cliquant sur **configurer le Service Web** bas hello du canevas de l’expérience hello (et en sélectionnant hello **prédictive Service Web** option).

> [!TIP]
> Si vous souhaitez plus d’informations sur ce qui se passe lorsque vous convertissez un tooa d’expérience de formation prédictive essayer, consultez [comment tooprepare votre modèle pour le déploiement dans Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Lorsque vous cliquez sur **Configurer le service web**, plusieurs choses se produisent :

* modèle formé Hello est converti tooa unique **formé** module et stockées dans hello module palette toohello gauche Hello expérimenter canevas (vous le trouverez sous **modèles formés**)
* Les modules qui ont été utilisés pour l’apprentissage sont supprimés :
  * [Arbre de décision optimisé à deux classes][two-class-boosted-decision-tree]
  * [Former le modèle][train-model]
  * [Fractionner les données][split]
  * Hello deuxième [Execute R Script] [ execute-r-script] module qui a été utilisée pour les données de test
* modèle formé de Hello enregistré est ajouté dans l’expérience de hello
* **Web service entrée** et **Web de sortie du service** modules sont ajoutés (ces pilotes identifient où les données de l’utilisateur hello Entrez modèle de hello et les données retournées lors de l’accès au service web de hello)

> [!NOTE]
> Vous pouvez voir que l’expérience de hello est enregistré en deux parties, sous les onglets qui ont été ajoutés en haut hello du canevas de l’expérience hello. Bonjour expérience d’apprentissage d’origine est sous l’onglet de hello **expérience de formation**, et hello nouvellement créé expérience prédictive est sous **expérience prédictive**. expérience de prédictive Hello est hello une que nous allons déployer comme un service web.

Nous avons besoin d’une étape supplémentaire tootake avec cette expérience particulier.
Nous avons ajouté deux [Execute R Script] [ execute-r-script] modules tooprovide une pondération de fonction toohello données. Qui était juste un pli qu'il est nécessaire pour l’apprentissage et de test, nous pouvons Retirez les modules dans le modèle final de hello.
Machine Learning Studio supprimé une [Execute R Script] [ execute-r-script] module lorsqu’il supprimé hello [fractionnement] [ split] module. Maintenant que nous pouvons supprimer hello autre et se connecter [éditeur de métadonnées] [ metadata-editor] directement trop[Score Model][score-model].    

Notre expérience doit alors ressembler à cela :  

![Calcul de score formé hello][4]  

> [!NOTE]
> Vous vous demandez peut-être pourquoi nous laissé hello données de carte de crédit allemande UCI dataset dans expérience prédictive de hello. service de Hello va données de l’utilisateur tooscore hello, pas hello de données d’origine, par conséquent, pourquoi laissent hello de jeu de données d’origine dans le modèle de hello ?
> 
> Il est vrai que service de hello ne devez hello des données de carte de crédit d’origine. Mais il a besoin de schéma de hello pour ces données, qui inclut des informations telles que le nombre de colonnes sont et les colonnes qui sont numériques. Ces informations de schéma sont les données de l’utilisateur nécessaire toointerpret hello. Vous conservez ces composants connectés de sorte que hello module calcul de score a un schéma de dataset hello lorsque hello service s’exécute. les données de salutation n’est pas utilisées, que les schéma hello.  
> 
> 

Exécutez l’expérience hello une dernière fois (cliquez sur **exécuter**.) Si vous souhaitez tooverify qui hello modèle fonctionne toujours, cliquez sur sortie hello Hello [Score Model] [ score-model] module et sélectionnez **afficher les résultats**. Vous pouvez voir que les données d’origine hello s’affiche, ainsi que de la valeur de risque de crédit hello (« Scored Labels ») et hello score la valeur de probabilité (« probabilités notées ».) 

## <a name="deploy-hello-web-service"></a>Déployer le service web de hello
Vous pouvez déployer hello expérience comme un service web standard, ou comme un service web qui est basé sur le Gestionnaire de ressources Azure.

### <a name="deploy-as-a-classic-web-service"></a>Déployer comme un service web classique
toodeploy un classique web service dérivé de notre expérience, cliquez sur **déployer le Service Web** ci-dessous hello canevas et sélectionnez **déployer le Service Web [standard]**. Machine Learning Studio déploie l’expérience hello comme un service web et vous toohello le tableau de bord pour ce service web. À partir de cette page, vous pouvez retourner toohello expérience (**afficher l’instantané** ou **afficher les dernières**) et exécuter un test simple du service web de hello (consultez **tester un service web de hello** ci-dessous). Il existe également des informations pour créer des applications qui peuvent accéder au service web de hello (plus à l’étape suivante de hello de cette procédure pas à pas).

![Tableau de bord du service web][6]

Vous pouvez configurer le service de hello en cliquant sur hello **CONFIGURATION** onglet. Ici vous pouvez modifier le nom du service hello (il désigne hello donné expérience par défaut) et lui donner une description. Vous pouvez également donner plus d’étiquettes conviviales hello pour les données d’entrée et de sortie.  

![Configurer le service web de hello][5]  

### <a name="deploy-as-a-new-web-service"></a>Déployer comme un nouveau service web

> [!NOTE] 
> toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans toowhich d’abonnement hello vous déployez hello service web. Pour plus d’informations, consultez [gérer un service web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

toodeploy un nouveau service web dérivé de notre expérience :

1. Cliquez sur **déployer le Service Web** ci-dessous hello canevas et sélectionnez **déployer le Service Web [nouveau]**. Machine Learning Studio transfère les services web de Azure Machine Learning toohello **déployer l’expérience** page.

2. Entrez un nom pour le service web de hello. 

3. Pour **Plan tarifaire**, vous pouvez sélectionner un plan de tarification existant, ou sélectionnez « Créer » et hello permettent de nouveau plan un nom et l’option de plan hello sélectionnez mensuel. plan Hello niveaux par défaut toohello des plans pour votre région par défaut et votre service web est déployé toothat région.

4. Cliquez sur **Déployer**.

Après quelques minutes, hello **Quickstart** page de votre service web s’ouvre.

Vous pouvez configurer le service de hello en cliquant sur hello **configurer** onglet. Ici, vous pouvez modifier les service hello titre et lui donner une description. 

tootest hello service web, cliquez sur hello **Test** onglet (consultez **tester un service web de hello** ci-dessous). Pour plus d’informations sur la création d’applications qui peuvent accéder au service web de hello, cliquez sur hello **consommer** onglet (étape suivante de hello dans cette procédure pas à pas prendront plus de détails).

> [!TIP]
> Vous pouvez mettre à jour de service web de hello une fois que vous avez déployé. Par exemple, si vous souhaitez toochange votre modèle, puis vous pouvez modifier l’expérience de formation hello, ajuster les paramètres du modèle hello et cliquez sur **déployer le Service Web**, en sélectionnant **déployer le Service Web [standard]** ou  **Déployer le Service Web [nouveau]**. Lorsque vous déployez à nouveau d’expérience de hello, il remplace le service web de hello, maintenant en utilisant votre modèle mis à jour.  
> 
> 

## <a name="test-hello-web-service"></a>Tester un service web de hello

Lorsque le service web de hello est accessible, les données de l’utilisateur hello entre via hello **Web service entrée** module où il a passé toohello [Score Model] [ score-model] module et évalués. façon Hello que nous avons configuré expérience prédictive de hello, modèle de hello attend des données dans le même format que les données de risque de crédit d’origine hello de hello.
Hello les résultats toohello utilisateur à partir du service web de hello via hello **Web de sortie du service** module.

> [!TIP]
> méthode Hello nous avons hello prédictive expérience configuré, hello ensemble résultant de hello [Score Model] [ score-model] module sont retournés. Cela inclut toutes les données d’entrée de hello plus valeur risque de crédit hello et hello score de probabilité. Mais vous pouvez retourner quelque chose de différent si vous le souhaitez ; par exemple, vous pouvez retourner uniquement les valeur de risque de crédit hello. toodo, insérer un [Project Columns] [ project-columns] module entre [Score Model] [ score-model] et hello **Web de sortie du service** tooeliminate les colonnes que vous ne souhaitez hello tooreturn de service web. 
> 
> 

Vous pouvez tester un site web classique dans service **Machine Learning Studio** ou Bonjour **Azure Machine Learning Services Web** portail.
Vous pouvez tester un service web uniquement dans hello **les Services Web Machine Learning** portal.

> [!TIP]
> Lorsque vous testez dans le portail de Services Web de Azure Machine Learning hello, vous pouvez avoir portal de hello pour créer des exemples de données que vous pouvez utiliser le service de requête-réponse de hello tootest. Sur hello **configurer** , sélectionnez « Oui » pour **activé des données d’exemple ?**. Lorsque vous ouvrez l’onglet hello requête-réponse sur hello **Test** , page de portail de hello renseigne les exemples de données obtenues à partir des données de risque de crédit d’origine hello.

### <a name="test-a-classic-web-service"></a>Tester un service web classique

Vous pouvez tester un service web de classique dans Machine Learning Studio ou dans le portail de Services Web de Machine Learning hello. 

#### <a name="test-in-machine-learning-studio"></a>Tester dans Machine Learning Studio

1. Sur hello **tableau de bord** pour le service web de hello, cliquez sur hello **Test** sous **le point de terminaison par défaut**. Une boîte de dialogue s’affiche et vous demande de données d’entrée de hello pour le service de hello. Il existe des colonnes mêmes est apparu dans le dataset de risque de crédit d’origine hello hello.  

2. Entrez un jeu de données, puis cliquez sur **OK**. 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a>Dans le portail de Services Web de Machine Learning hello de test

1. Sur hello **tableau de bord** pour le service web de hello, cliquez sur hello **aperçu de Test** lien sous **le point de terminaison par défaut**. page de test Hello dans le portail de Services Web de Azure Machine Learning hello point de terminaison de service web hello s’ouvre et vous demande de données d’entrée de hello pour le service de hello. Il existe des colonnes mêmes est apparu dans le dataset de risque de crédit d’origine hello hello.

2. Cliquez sur **Tester Demande-réponse**. 

### <a name="test-a-new-web-service"></a>Tester un nouveau service web

Vous pouvez tester un service web uniquement dans le portail de Services Web de Machine Learning hello.

1. Bonjour [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portail, cliquez sur **Test** en hello haut hello. Hello **Test** page s’ouvre et vous pouvez entrer des données pour le service de hello. les champs d’entrée Hello affichés correspondent toohello les colonnes qui apparaissent dans le dataset de risque de crédit d’origine hello. 

2. Entrez un jeu de données, puis cliquez sur **Test Request-Response**(Tester la requête-réponse).

Hello résultats de test de hello sont affichés sur le côté droit de hello de page hello dans la colonne de sortie hello. 


## <a name="manage-hello-web-service"></a>Gérer le service web de hello

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a>Gérer un service web de classique Bonjour portail Azure classic

Une fois que vous avez déployé votre service web de classique, vous pouvez gérer à partir de hello [portail Azure classic](https://manage.windowsazure.com).

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com)
2. Dans le panneau de configuration des services de Microsoft Azure de hello, cliquez sur **MACHINE LEARNING**
3. Cliquez sur votre espace de travail.
4. Cliquez sur hello **services Web** onglet
5. Cliquez sur le service web hello, nous avons créé
6. Cliquez sur le point de terminaison hello « default »

À ce stade, vous pouvez faire surveiller le faire du service web de hello et apporter des ajustements de performances en modifiant le service de hello le nombre d’appels simultanés peut gérer.

Pour plus d'informations, consultez la page suivante :

* [Création de points de terminaison](machine-learning-create-endpoint.md)
* [Mise à l’échelle du service web](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a>Gérer un classique ou un nouveau service web dans le portail de Services Web de Azure Machine Learning hello

Une fois que vous avez déployé votre service web, si classique ou nouveaux, vous pouvez gérer à partir de hello [les Services Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portal.

performances de hello toomonitor de votre service web :

1. Connectez-vous à toohello [les Services Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portail
2. Cliquez sur **Services web**.
3. Cliquer sur votre service web
4. Cliquez sur hello **tableau de bord**

- - -
**Ensuite : [accéder au service web de hello](machine-learning-walkthrough-6-access-web-service.md)**

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
