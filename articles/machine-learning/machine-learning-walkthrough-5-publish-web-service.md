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
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a><span data-ttu-id="b6d3a-103">Procédure pas à pas, étape 5 : Déployer le service web de Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-103">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>
<span data-ttu-id="b6d3a-104">Voici la cinquième étape de hello hello procédure pas à pas, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="b6d3a-104">This is hello fifth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="b6d3a-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b6d3a-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="b6d3a-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="b6d3a-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="b6d3a-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="b6d3a-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="b6d3a-108">L’apprentissage et évaluer des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="b6d3a-109">**Déployer le service web de hello**</span><span class="sxs-lookup"><span data-stu-id="b6d3a-109">**Deploy hello web service**</span></span>
6. [<span data-ttu-id="b6d3a-110">Service d’accès hello web</span><span class="sxs-lookup"><span data-stu-id="b6d3a-110">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="b6d3a-111">toogive d’autres une chance toouse hello modèle prédictif, nous avons développé dans cette procédure pas à pas, nous pouvons déployer en tant que service web sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-111">toogive others a chance toouse hello predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="b6d3a-112">Point de toothis nous avons testé avec notre modèle d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-112">Up toothis point we've been experimenting with training our model.</span></span> <span data-ttu-id="b6d3a-113">Mais service de hello déployé n’est plus va toodo formation - il va toogenerate nouvelles prédictions par hello l’entrée d’utilisateur en fonction de notre modèle de score.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-113">But hello deployed service is no longer going toodo training - it's going toogenerate new predictions by scoring hello user's input based on our model.</span></span> <span data-ttu-id="b6d3a-114">Nous allons toodo certains tooconvert préparation cela faire des essais d’un ***formation*** expérimenter tooa ***prédictive*** faire des essais.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-114">So we're going toodo some preparation tooconvert this experiment from a ***training*** experiment tooa ***predictive*** experiment.</span></span> 

<span data-ttu-id="b6d3a-115">Ce processus comprend trois étapes :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="b6d3a-116">Supprimez l’un des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-116">Remove one of hello models</span></span>
2. <span data-ttu-id="b6d3a-117">Convertir hello *expérience de formation* , nous avons créé dans un *expérience prédictive*</span><span class="sxs-lookup"><span data-stu-id="b6d3a-117">Convert hello *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="b6d3a-118">Déployer l’expérience de prédictive hello comme un service web</span><span class="sxs-lookup"><span data-stu-id="b6d3a-118">Deploy hello predictive experiment as a web service</span></span>

## <a name="remove-one-of-hello-models"></a><span data-ttu-id="b6d3a-119">Supprimez l’un des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-119">Remove one of hello models</span></span>

<span data-ttu-id="b6d3a-120">Tout d’abord, nous devons tootrim cette expérience vers le bas un peu.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-120">First, we need tootrim this experiment down a little.</span></span> <span data-ttu-id="b6d3a-121">Actuellement, nous avons deux modèles différents dans une expérience de hello, mais nous voulons uniquement toouse un modèle lors du déploiement de cela comme un service web.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-121">We currently have two different models in hello experiment, but we only want toouse one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="b6d3a-122">Supposons que nous avons décidé de ce modèle d’arbre hello augmenté effectuée de meilleures performances que le modèle SVM hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-122">Let's say we've decided that hello boosted tree model performed better than hello SVM model.</span></span> <span data-ttu-id="b6d3a-123">Hello première chose toodo est remove hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] module et modules hello qui ont été utilisés pour la formation.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-123">So hello first thing toodo is remove hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module and hello modules that were used for training it.</span></span> <span data-ttu-id="b6d3a-124">Vous souhaiterez peut-être toomake une copie de l’expérience de hello tout d’abord en cliquant sur **Enregistrer sous** bas hello hello expérimenter la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-124">You may want toomake a copy of hello experiment first by clicking **Save As** at hello bottom of hello experiment canvas.</span></span>

<span data-ttu-id="b6d3a-125">Nous devons hello toodelete suivant des modules :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-125">We need toodelete hello following modules:</span></span>  

* <span data-ttu-id="b6d3a-126">[Machine à vecteurs de support à deux classes][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="b6d3a-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="b6d3a-127">[L’apprentissage du modèle] [ train-model] et [Score Model] [ score-model] modules qui ont été connecté tooit</span><span class="sxs-lookup"><span data-stu-id="b6d3a-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected tooit</span></span>
* <span data-ttu-id="b6d3a-128">[Normaliser les données][normalize-data] (les deux)</span><span class="sxs-lookup"><span data-stu-id="b6d3a-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="b6d3a-129">[Évaluation du modèle] [ evaluate-model] (étant donné que nous avons terminé l’évaluation de modèles de hello)</span><span class="sxs-lookup"><span data-stu-id="b6d3a-129">[Evaluate Model][evaluate-model] (because we're finished evaluating hello models)</span></span>

<span data-ttu-id="b6d3a-130">Sélectionnez chaque module et appuyez sur la touche SUPPR de hello ou un module de hello avec le bouton droit et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-130">Select each module and press hello Delete key, or right-click hello module and select **Delete**.</span></span> 

![Supprimer le modèle SVM hello][3a]

<span data-ttu-id="b6d3a-132">Notre modèle doit alors ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-132">Our model should now look something like this:</span></span>

![Supprimer le modèle SVM hello][3]

<span data-ttu-id="b6d3a-134">Maintenant, nous sommes prêt toodeploy de ce modèle à l’aide de hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="b6d3a-134">Now we're ready toodeploy this model using hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="b6d3a-135">Convertir l’expérience prédictive des tooa expérience d’apprentissage hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-135">Convert hello training experiment tooa predictive experiment</span></span>

<span data-ttu-id="b6d3a-136">tooget de ce modèle prêt pour le déploiement, nous devons tooconvert cette expérience de prédictive tooa expérience d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-136">tooget this model ready for deployment, we need tooconvert this training experiment tooa predictive experiment.</span></span> <span data-ttu-id="b6d3a-137">Cela implique trois étapes :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-137">This involves three steps:</span></span>

1. <span data-ttu-id="b6d3a-138">Enregistrer le modèle hello nous avez formé, puis la remplacer nos modules d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="b6d3a-138">Save hello model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="b6d3a-139">Trim hello expérience tooremove modules qui ont été nécessaires uniquement pour l’apprentissage</span><span class="sxs-lookup"><span data-stu-id="b6d3a-139">Trim hello experiment tooremove modules that were only needed for training</span></span>
3. <span data-ttu-id="b6d3a-140">Définir où service web de hello accepter l’entrée et où il génère une sortie de hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-140">Define where hello web service will accept input and where it generates hello output</span></span>

<span data-ttu-id="b6d3a-141">Nous pourrions le faire manuellement, mais heureusement les trois étapes peuvent être accomplies en cliquant sur **configurer le Service Web** bas hello du canevas de l’expérience hello (et en sélectionnant hello **prédictive Service Web** option).</span><span class="sxs-lookup"><span data-stu-id="b6d3a-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at hello bottom of hello experiment canvas (and selecting hello **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="b6d3a-142">Si vous souhaitez plus d’informations sur ce qui se passe lorsque vous convertissez un tooa d’expérience de formation prédictive essayer, consultez [comment tooprepare votre modèle pour le déploiement dans Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="b6d3a-142">If you want more details on what happens when you convert a training experiment tooa predictive experiment, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="b6d3a-143">Lorsque vous cliquez sur **Configurer le service web**, plusieurs choses se produisent :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="b6d3a-144">modèle formé Hello est converti tooa unique **formé** module et stockées dans hello module palette toohello gauche Hello expérimenter canevas (vous le trouverez sous **modèles formés**)</span><span class="sxs-lookup"><span data-stu-id="b6d3a-144">hello trained model is converted tooa single **Trained Model** module and stored in hello module palette toohello left of hello experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="b6d3a-145">Les modules qui ont été utilisés pour l’apprentissage sont supprimés :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="b6d3a-146">[Arbre de décision optimisé à deux classes][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="b6d3a-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="b6d3a-147">[Former le modèle][train-model]</span><span class="sxs-lookup"><span data-stu-id="b6d3a-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="b6d3a-148">[Fractionner les données][split]</span><span class="sxs-lookup"><span data-stu-id="b6d3a-148">[Split Data][split]</span></span>
  * <span data-ttu-id="b6d3a-149">Hello deuxième [Execute R Script] [ execute-r-script] module qui a été utilisée pour les données de test</span><span class="sxs-lookup"><span data-stu-id="b6d3a-149">hello second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="b6d3a-150">modèle formé de Hello enregistré est ajouté dans l’expérience de hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-150">hello saved trained model is added back into hello experiment</span></span>
* <span data-ttu-id="b6d3a-151">**Web service entrée** et **Web de sortie du service** modules sont ajoutés (ces pilotes identifient où les données de l’utilisateur hello Entrez modèle de hello et les données retournées lors de l’accès au service web de hello)</span><span class="sxs-lookup"><span data-stu-id="b6d3a-151">**Web service input** and **Web service output** modules are added (these identify where hello user's data will enter hello model, and what data is returned, when hello web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="b6d3a-152">Vous pouvez voir que l’expérience de hello est enregistré en deux parties, sous les onglets qui ont été ajoutés en haut hello du canevas de l’expérience hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-152">You can see that hello experiment is saved in two parts under tabs that have been added at hello top of hello experiment canvas.</span></span> <span data-ttu-id="b6d3a-153">Bonjour expérience d’apprentissage d’origine est sous l’onglet de hello **expérience de formation**, et hello nouvellement créé expérience prédictive est sous **expérience prédictive**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-153">hello original training experiment is under hello tab **Training experiment**, and hello newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="b6d3a-154">expérience de prédictive Hello est hello une que nous allons déployer comme un service web.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-154">hello predictive experiment is hello one we'll deploy as a web service.</span></span>

<span data-ttu-id="b6d3a-155">Nous avons besoin d’une étape supplémentaire tootake avec cette expérience particulier.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-155">We need tootake one additional step with this particular experiment.</span></span>
<span data-ttu-id="b6d3a-156">Nous avons ajouté deux [Execute R Script] [ execute-r-script] modules tooprovide une pondération de fonction toohello données.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-156">We added two [Execute R Script][execute-r-script] modules tooprovide a weighting function toohello data.</span></span> <span data-ttu-id="b6d3a-157">Qui était juste un pli qu'il est nécessaire pour l’apprentissage et de test, nous pouvons Retirez les modules dans le modèle final de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-157">That was just a trick we needed for training and testing, so we can take out those modules in hello final model.</span></span>
<span data-ttu-id="b6d3a-158">Machine Learning Studio supprimé une [Execute R Script] [ execute-r-script] module lorsqu’il supprimé hello [fractionnement] [ split] module.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed hello [Split][split] module.</span></span> <span data-ttu-id="b6d3a-159">Maintenant que nous pouvons supprimer hello autre et se connecter [éditeur de métadonnées] [ metadata-editor] directement trop[Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="b6d3a-159">Now we can remove hello other and connect [Metadata Editor][metadata-editor] directly too[Score Model][score-model].</span></span>    

<span data-ttu-id="b6d3a-160">Notre expérience doit alors ressembler à cela :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-160">Our experiment should now look like this:</span></span>  

![Calcul de score formé hello][4]  

> [!NOTE]
> <span data-ttu-id="b6d3a-162">Vous vous demandez peut-être pourquoi nous laissé hello données de carte de crédit allemande UCI dataset dans expérience prédictive de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-162">You may be wondering why we left hello UCI German Credit Card Data dataset in hello predictive experiment.</span></span> <span data-ttu-id="b6d3a-163">service de Hello va données de l’utilisateur tooscore hello, pas hello de données d’origine, par conséquent, pourquoi laissent hello de jeu de données d’origine dans le modèle de hello ?</span><span class="sxs-lookup"><span data-stu-id="b6d3a-163">hello service is going tooscore hello user's data, not hello original dataset, so why leave hello original dataset in hello model?</span></span>
> 
> <span data-ttu-id="b6d3a-164">Il est vrai que service de hello ne devez hello des données de carte de crédit d’origine.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-164">It's true that hello service doesn't need hello original credit card data.</span></span> <span data-ttu-id="b6d3a-165">Mais il a besoin de schéma de hello pour ces données, qui inclut des informations telles que le nombre de colonnes sont et les colonnes qui sont numériques.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-165">But it does need hello schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="b6d3a-166">Ces informations de schéma sont les données de l’utilisateur nécessaire toointerpret hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-166">This schema information is necessary toointerpret hello user's data.</span></span> <span data-ttu-id="b6d3a-167">Vous conservez ces composants connectés de sorte que hello module calcul de score a un schéma de dataset hello lorsque hello service s’exécute.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-167">We leave these components connected so that hello scoring module has hello dataset schema when hello service is running.</span></span> <span data-ttu-id="b6d3a-168">les données de salutation n’est pas utilisées, que les schéma hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-168">hello data isn't used, just hello schema.</span></span>  
> 
> 

<span data-ttu-id="b6d3a-169">Exécutez l’expérience hello une dernière fois (cliquez sur **exécuter**.) Si vous souhaitez tooverify qui hello modèle fonctionne toujours, cliquez sur sortie hello Hello [Score Model] [ score-model] module et sélectionnez **afficher les résultats**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-169">Run hello experiment one last time (click **Run**.) If you want tooverify that hello model is still working, click hello output of hello [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="b6d3a-170">Vous pouvez voir que les données d’origine hello s’affiche, ainsi que de la valeur de risque de crédit hello (« Scored Labels ») et hello score la valeur de probabilité (« probabilités notées ».)</span><span class="sxs-lookup"><span data-stu-id="b6d3a-170">You can see that hello original data is displayed, along with hello credit risk value ("Scored Labels") and hello scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-hello-web-service"></a><span data-ttu-id="b6d3a-171">Déployer le service web de hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-171">Deploy hello web service</span></span>
<span data-ttu-id="b6d3a-172">Vous pouvez déployer hello expérience comme un service web standard, ou comme un service web qui est basé sur le Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-172">You can deploy hello experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="b6d3a-173">Déployer comme un service web classique</span><span class="sxs-lookup"><span data-stu-id="b6d3a-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="b6d3a-174">toodeploy un classique web service dérivé de notre expérience, cliquez sur **déployer le Service Web** ci-dessous hello canevas et sélectionnez **déployer le Service Web [standard]**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-174">toodeploy a Classic web service derived from our experiment, click **Deploy Web Service** below hello canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="b6d3a-175">Machine Learning Studio déploie l’expérience hello comme un service web et vous toohello le tableau de bord pour ce service web.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-175">Machine Learning Studio deploys hello experiment as a web service and takes you toohello dashboard for that web service.</span></span> <span data-ttu-id="b6d3a-176">À partir de cette page, vous pouvez retourner toohello expérience (**afficher l’instantané** ou **afficher les dernières**) et exécuter un test simple du service web de hello (consultez **tester un service web de hello** ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="b6d3a-176">From this page you can return toohello experiment (**View snapshot** or **View latest**) and run a simple test of hello web service (see **Test hello web service** below).</span></span> <span data-ttu-id="b6d3a-177">Il existe également des informations pour créer des applications qui peuvent accéder au service web de hello (plus à l’étape suivante de hello de cette procédure pas à pas).</span><span class="sxs-lookup"><span data-stu-id="b6d3a-177">There is also information here for creating applications that can access hello web service (more on that in hello next step of this walkthrough).</span></span>

![Tableau de bord du service web][6]

<span data-ttu-id="b6d3a-179">Vous pouvez configurer le service de hello en cliquant sur hello **CONFIGURATION** onglet. Ici vous pouvez modifier le nom du service hello (il désigne hello donné expérience par défaut) et lui donner une description.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-179">You can configure hello service by clicking hello **CONFIGURATION** tab. Here you can modify hello service name (it's given hello experiment name by default) and give it a description.</span></span> <span data-ttu-id="b6d3a-180">Vous pouvez également donner plus d’étiquettes conviviales hello pour les données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-180">You can also give more friendly labels for hello input and output data.</span></span>  

![Configurer le service web de hello][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="b6d3a-182">Déployer comme un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="b6d3a-182">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="b6d3a-183">toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans toowhich d’abonnement hello vous déployez hello service web.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-183">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you are deploying hello web service.</span></span> <span data-ttu-id="b6d3a-184">Pour plus d’informations, consultez [gérer un service web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="b6d3a-184">For more information, see [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="b6d3a-185">toodeploy un nouveau service web dérivé de notre expérience :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-185">toodeploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="b6d3a-186">Cliquez sur **déployer le Service Web** ci-dessous hello canevas et sélectionnez **déployer le Service Web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-186">Click **Deploy Web Service** below hello canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="b6d3a-187">Machine Learning Studio transfère les services web de Azure Machine Learning toohello **déployer l’expérience** page.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-187">Machine Learning Studio transfers you toohello Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="b6d3a-188">Entrez un nom pour le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-188">Enter a name for hello web service.</span></span> 

3. <span data-ttu-id="b6d3a-189">Pour **Plan tarifaire**, vous pouvez sélectionner un plan de tarification existant, ou sélectionnez « Créer » et hello permettent de nouveau plan un nom et l’option de plan hello sélectionnez mensuel.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-189">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give hello new plan a name and select hello monthly plan option.</span></span> <span data-ttu-id="b6d3a-190">plan Hello niveaux par défaut toohello des plans pour votre région par défaut et votre service web est déployé toothat région.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-190">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

4. <span data-ttu-id="b6d3a-191">Cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-191">Click **Deploy**.</span></span>

<span data-ttu-id="b6d3a-192">Après quelques minutes, hello **Quickstart** page de votre service web s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-192">After a few minutes, hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="b6d3a-193">Vous pouvez configurer le service de hello en cliquant sur hello **configurer** onglet. Ici, vous pouvez modifier les service hello titre et lui donner une description.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-193">You can configure hello service by clicking hello **Configure** tab. Here you can modify hello service title and give it a description.</span></span> 

<span data-ttu-id="b6d3a-194">tootest hello service web, cliquez sur hello **Test** onglet (consultez **tester un service web de hello** ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="b6d3a-194">tootest hello web service, click hello **Test** tab (see **Test hello web service** below).</span></span> <span data-ttu-id="b6d3a-195">Pour plus d’informations sur la création d’applications qui peuvent accéder au service web de hello, cliquez sur hello **consommer** onglet (étape suivante de hello dans cette procédure pas à pas prendront plus de détails).</span><span class="sxs-lookup"><span data-stu-id="b6d3a-195">For information on creating applications that can access hello web service, click hello **Consume** tab (hello next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="b6d3a-196">Vous pouvez mettre à jour de service web de hello une fois que vous avez déployé.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-196">You can update hello web service after you've deployed it.</span></span> <span data-ttu-id="b6d3a-197">Par exemple, si vous souhaitez toochange votre modèle, puis vous pouvez modifier l’expérience de formation hello, ajuster les paramètres du modèle hello et cliquez sur **déployer le Service Web**, en sélectionnant **déployer le Service Web [standard]** ou  **Déployer le Service Web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-197">For example, if you want toochange your model, then you can edit hello training experiment, tweak hello model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="b6d3a-198">Lorsque vous déployez à nouveau d’expérience de hello, il remplace le service web de hello, maintenant en utilisant votre modèle mis à jour.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-198">When you deploy hello experiment again, it replaces hello web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-hello-web-service"></a><span data-ttu-id="b6d3a-199">Tester un service web de hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-199">Test hello web service</span></span>

<span data-ttu-id="b6d3a-200">Lorsque le service web de hello est accessible, les données de l’utilisateur hello entre via hello **Web service entrée** module où il a passé toohello [Score Model] [ score-model] module et évalués.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-200">When hello web service is accessed, hello user's data enters through hello **Web service input** module where it's passed toohello [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="b6d3a-201">façon Hello que nous avons configuré expérience prédictive de hello, modèle de hello attend des données dans le même format que les données de risque de crédit d’origine hello de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-201">hello way we've set up hello predictive experiment, hello model expects data in hello same format as hello original credit risk dataset.</span></span>
<span data-ttu-id="b6d3a-202">Hello les résultats toohello utilisateur à partir du service web de hello via hello **Web de sortie du service** module.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-202">hello results are returned toohello user from hello web service through hello **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="b6d3a-203">méthode Hello nous avons hello prédictive expérience configuré, hello ensemble résultant de hello [Score Model] [ score-model] module sont retournés.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-203">hello way we have hello predictive experiment configured, hello entire results from hello [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="b6d3a-204">Cela inclut toutes les données d’entrée de hello plus valeur risque de crédit hello et hello score de probabilité.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-204">This includes all hello input data plus hello credit risk value and hello scoring probability.</span></span> <span data-ttu-id="b6d3a-205">Mais vous pouvez retourner quelque chose de différent si vous le souhaitez ; par exemple, vous pouvez retourner uniquement les valeur de risque de crédit hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-205">But you can return something different if you want - for example, you could return just hello credit risk value.</span></span> <span data-ttu-id="b6d3a-206">toodo, insérer un [Project Columns] [ project-columns] module entre [Score Model] [ score-model] et hello **Web de sortie du service** tooeliminate les colonnes que vous ne souhaitez hello tooreturn de service web.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-206">toodo this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and hello **Web service output** tooeliminate columns you don't want hello web service tooreturn.</span></span> 
> 
> 

<span data-ttu-id="b6d3a-207">Vous pouvez tester un site web classique dans service **Machine Learning Studio** ou Bonjour **Azure Machine Learning Services Web** portail.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-207">You can test a Classic web service either in **Machine Learning Studio** or in hello **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="b6d3a-208">Vous pouvez tester un service web uniquement dans hello **les Services Web Machine Learning** portal.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-208">You can test a New web service only in hello **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="b6d3a-209">Lorsque vous testez dans le portail de Services Web de Azure Machine Learning hello, vous pouvez avoir portal de hello pour créer des exemples de données que vous pouvez utiliser le service de requête-réponse de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-209">When testing in hello Azure Machine Learning Web Services portal, you can have hello portal create sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="b6d3a-210">Sur hello **configurer** , sélectionnez « Oui » pour **activé des données d’exemple ?**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-210">On hello **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="b6d3a-211">Lorsque vous ouvrez l’onglet hello requête-réponse sur hello **Test** , page de portail de hello renseigne les exemples de données obtenues à partir des données de risque de crédit d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-211">When you open hello Request-Response tab on hello **Test** page, hello portal fills in sample data taken from hello original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="b6d3a-212">Tester un service web classique</span><span class="sxs-lookup"><span data-stu-id="b6d3a-212">Test a Classic web service</span></span>

<span data-ttu-id="b6d3a-213">Vous pouvez tester un service web de classique dans Machine Learning Studio ou dans le portail de Services Web de Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-213">You can test a Classic web service in Machine Learning Studio or in hello Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="b6d3a-214">Tester dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="b6d3a-214">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="b6d3a-215">Sur hello **tableau de bord** pour le service web de hello, cliquez sur hello **Test** sous **le point de terminaison par défaut**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-215">On hello **DASHBOARD** page for hello web service, click hello **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="b6d3a-216">Une boîte de dialogue s’affiche et vous demande de données d’entrée de hello pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-216">A dialog pops up and asks you for hello input data for hello service.</span></span> <span data-ttu-id="b6d3a-217">Il existe des colonnes mêmes est apparu dans le dataset de risque de crédit d’origine hello hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-217">These are hello same columns that appeared in hello original credit risk dataset.</span></span>  

2. <span data-ttu-id="b6d3a-218">Entrez un jeu de données, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-218">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a><span data-ttu-id="b6d3a-219">Dans le portail de Services Web de Machine Learning hello de test</span><span class="sxs-lookup"><span data-stu-id="b6d3a-219">Test in hello Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="b6d3a-220">Sur hello **tableau de bord** pour le service web de hello, cliquez sur hello **aperçu de Test** lien sous **le point de terminaison par défaut**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-220">On hello **DASHBOARD** page for hello web service, click hello **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="b6d3a-221">page de test Hello dans le portail de Services Web de Azure Machine Learning hello point de terminaison de service web hello s’ouvre et vous demande de données d’entrée de hello pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-221">hello test page in hello Azure Machine Learning Web Services portal for hello web service endpoint opens and asks you for hello input data for hello service.</span></span> <span data-ttu-id="b6d3a-222">Il existe des colonnes mêmes est apparu dans le dataset de risque de crédit d’origine hello hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-222">These are hello same columns that appeared in hello original credit risk dataset.</span></span>

2. <span data-ttu-id="b6d3a-223">Cliquez sur **Tester Demande-réponse**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-223">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="b6d3a-224">Tester un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="b6d3a-224">Test a New web service</span></span>

<span data-ttu-id="b6d3a-225">Vous pouvez tester un service web uniquement dans le portail de Services Web de Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-225">You can test a New web service only in hello Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="b6d3a-226">Bonjour [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portail, cliquez sur **Test** en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-226">In hello [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at hello top of hello page.</span></span> <span data-ttu-id="b6d3a-227">Hello **Test** page s’ouvre et vous pouvez entrer des données pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-227">hello **Test** page opens and you can input data for hello service.</span></span> <span data-ttu-id="b6d3a-228">les champs d’entrée Hello affichés correspondent toohello les colonnes qui apparaissent dans le dataset de risque de crédit d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-228">hello input fields displayed correspond toohello columns that appeared in hello original credit risk dataset.</span></span> 

2. <span data-ttu-id="b6d3a-229">Entrez un jeu de données, puis cliquez sur **Test Request-Response**(Tester la requête-réponse).</span><span class="sxs-lookup"><span data-stu-id="b6d3a-229">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="b6d3a-230">Hello résultats de test de hello sont affichés sur le côté droit de hello de page hello dans la colonne de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-230">hello results of hello test are displayed on hello right-hand side of hello page in hello output column.</span></span> 


## <a name="manage-hello-web-service"></a><span data-ttu-id="b6d3a-231">Gérer le service web de hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-231">Manage hello web service</span></span>

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a><span data-ttu-id="b6d3a-232">Gérer un service web de classique Bonjour portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="b6d3a-232">Manage a Classic web service in hello Azure classic portal</span></span>

<span data-ttu-id="b6d3a-233">Une fois que vous avez déployé votre service web de classique, vous pouvez gérer à partir de hello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b6d3a-233">Once you've deployed your Classic web service, you can manage it from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="b6d3a-234">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="b6d3a-234">Sign in toohello [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="b6d3a-235">Dans le panneau de configuration des services de Microsoft Azure de hello, cliquez sur **MACHINE LEARNING**</span><span class="sxs-lookup"><span data-stu-id="b6d3a-235">In hello Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="b6d3a-236">Cliquez sur votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-236">Click your workspace</span></span>
4. <span data-ttu-id="b6d3a-237">Cliquez sur hello **services Web** onglet</span><span class="sxs-lookup"><span data-stu-id="b6d3a-237">Click hello **Web services** tab</span></span>
5. <span data-ttu-id="b6d3a-238">Cliquez sur le service web hello, nous avons créé</span><span class="sxs-lookup"><span data-stu-id="b6d3a-238">Click hello web service we created</span></span>
6. <span data-ttu-id="b6d3a-239">Cliquez sur le point de terminaison hello « default »</span><span class="sxs-lookup"><span data-stu-id="b6d3a-239">Click hello "default" endpoint</span></span>

<span data-ttu-id="b6d3a-240">À ce stade, vous pouvez faire surveiller le faire du service web de hello et apporter des ajustements de performances en modifiant le service de hello le nombre d’appels simultanés peut gérer.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-240">From here, you can do things like monitor how hello web service is doing and make performance tweaks by changing how many concurrent calls hello service can handle.</span></span>

<span data-ttu-id="b6d3a-241">Pour plus d'informations, consultez la page suivante :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-241">For more details, see:</span></span>

* [<span data-ttu-id="b6d3a-242">Création de points de terminaison</span><span class="sxs-lookup"><span data-stu-id="b6d3a-242">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="b6d3a-243">Mise à l’échelle du service web</span><span class="sxs-lookup"><span data-stu-id="b6d3a-243">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="b6d3a-244">Gérer un classique ou un nouveau service web dans le portail de Services Web de Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="b6d3a-244">Manage a Classic or New web service in hello Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="b6d3a-245">Une fois que vous avez déployé votre service web, si classique ou nouveaux, vous pouvez gérer à partir de hello [les Services Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portal.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-245">Once you've deployed your web service, whether Classic or New, you can manage it from hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="b6d3a-246">performances de hello toomonitor de votre service web :</span><span class="sxs-lookup"><span data-stu-id="b6d3a-246">toomonitor hello performance of your web service:</span></span>

1. <span data-ttu-id="b6d3a-247">Connectez-vous à toohello [les Services Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portail</span><span class="sxs-lookup"><span data-stu-id="b6d3a-247">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="b6d3a-248">Cliquez sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="b6d3a-248">Click **Web services**</span></span>
3. <span data-ttu-id="b6d3a-249">Cliquer sur votre service web</span><span class="sxs-lookup"><span data-stu-id="b6d3a-249">Click your web service</span></span>
4. <span data-ttu-id="b6d3a-250">Cliquez sur hello **tableau de bord**</span><span class="sxs-lookup"><span data-stu-id="b6d3a-250">Click hello **Dashboard**</span></span>

- - -
<span data-ttu-id="b6d3a-251">**Ensuite : [accéder au service web de hello](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="b6d3a-251">**Next: [Access hello web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
