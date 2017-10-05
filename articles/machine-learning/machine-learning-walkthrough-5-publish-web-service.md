---
title: "Étape 5 : Déploiement du service web Machine Learning | Microsoft Docs"
description: "Étape 5 de la procédure pas à pas de développement d’une solution prédictive : Déploiement d’une expérience prédictive en tant que service web dans Machine Learning Studio."
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
ms.openlocfilehash: cec1bcceea158a20742c7019a266dcefaac4c9cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="d1a5a-103">Étape 5 du didacticiel pas à pas : Déploiement du service web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d1a5a-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="d1a5a-104">Voici la cinquième étape de la procédure pas à pas [Développement d’une solution d’analyse prédictive avec Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="d1a5a-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="d1a5a-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d1a5a-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="d1a5a-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="d1a5a-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="d1a5a-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="d1a5a-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="d1a5a-108">Former et évaluer les modèles</span><span class="sxs-lookup"><span data-stu-id="d1a5a-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="d1a5a-109">**Déployer le service web**</span><span class="sxs-lookup"><span data-stu-id="d1a5a-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="d1a5a-110">Accéder au service web</span><span class="sxs-lookup"><span data-stu-id="d1a5a-110">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="d1a5a-111">Pour que d’autres personnes puissent utiliser le modèle de prévision que nous avons développé dans cette procédure pas à pas, nous pouvons le déployer en tant que service web sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="d1a5a-112">Jusqu’à présent, nous avons réalisé l’expérience avec la formation de notre modèle.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="d1a5a-113">Mais le service déployé n’effectue plus l’apprentissage ; il va produire de nouvelles prédictions en évaluant l’entrée de l’utilisateur en fonction de notre modèle.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="d1a5a-114">Nous allons donc effectuer quelques préparatifs pour convertir cette expérience de ***i*** en expérience ***prédictive***.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="d1a5a-115">Ce processus comprend trois étapes :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="d1a5a-116">Supprimer l’un des modèles</span><span class="sxs-lookup"><span data-stu-id="d1a5a-116">Remove one of the models</span></span>
2. <span data-ttu-id="d1a5a-117">Convertir l’*expérience de formation* que nous avons créée en *expérience prédictive*.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="d1a5a-118">Déploiement de l’expérience prédictive sous la forme d’un service web</span><span class="sxs-lookup"><span data-stu-id="d1a5a-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="d1a5a-119">Supprimer l’un des modèles</span><span class="sxs-lookup"><span data-stu-id="d1a5a-119">Remove one of the models</span></span>

<span data-ttu-id="d1a5a-120">Tout d’abord, nous devons réduire un peu cette expérience.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="d1a5a-121">Nous disposons actuellement de deux modèles différents dans l’expérience, mais nous ne souhaitons utiliser qu’un seul modèle au moment de déployer cette expérience en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="d1a5a-122">Supposons que nous ayons décidé que le modèle Arbre de décision optimisé est plus adapté que le modèle SVM.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="d1a5a-123">La première chose à faire est de supprimer le module [Machine à vecteurs de support à deux classes][two-class-support-vector-machine], ainsi que les modules qui ont été utilisés pour sa formation.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="d1a5a-124">Vous pouvez d'abord copier l'expérience en cliquant sur **Enregistrer sous** dans la partie inférieure de la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="d1a5a-125">Nous devons supprimer les modules suivants :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="d1a5a-126">[Machine à vecteurs de support à deux classes][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="d1a5a-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="d1a5a-127">Modules [Former le modèle][train-model] et [Noter le modèle][score-model] qui lui étaient connectés</span><span class="sxs-lookup"><span data-stu-id="d1a5a-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="d1a5a-128">[Normaliser les données][normalize-data] (les deux)</span><span class="sxs-lookup"><span data-stu-id="d1a5a-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="d1a5a-129">[Évaluer le modèle][evaluate-model] (puisque nous avons terminé d’évaluer les modèles)</span><span class="sxs-lookup"><span data-stu-id="d1a5a-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="d1a5a-130">Sélectionnez chaque module et appuyez sur la touche Suppr, ou cliquez avec le bouton droit sur le module puis sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![Modèle SVM supprimé][3a]

<span data-ttu-id="d1a5a-132">Notre modèle doit alors ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-132">Our model should now look something like this:</span></span>

![Modèle SVM supprimé][3]

<span data-ttu-id="d1a5a-134">À présent, nous sommes prêts à déployer ce modèle avec le module [Arbre de décision optimisé à deux classes][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="d1a5a-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="d1a5a-135">Convertir l'expérience de formation en expérience prédictive</span><span class="sxs-lookup"><span data-stu-id="d1a5a-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="d1a5a-136">Pour préparer ce modèle pour le déploiement, nous devons convertir cette expérience de formation d’une expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="d1a5a-137">Cela implique trois étapes :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-137">This involves three steps:</span></span>

1. <span data-ttu-id="d1a5a-138">Enregistrer le modèle que nous avons formé, puis remplacer nos modules de formation</span><span class="sxs-lookup"><span data-stu-id="d1a5a-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="d1a5a-139">Réduire l’expérience en supprimant les modules uniquement nécessaires à l’apprentissage</span><span class="sxs-lookup"><span data-stu-id="d1a5a-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="d1a5a-140">Définir où le service web doit accepter l’entrée et où il génère la sortie</span><span class="sxs-lookup"><span data-stu-id="d1a5a-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="d1a5a-141">Nous pourrions effectuer cette opération manuellement, mais heureusement il est possible d’accomplir ces trois étapes en cliquant sur **Configurer le service web** dans la partie inférieure de la zone de dessin de l’expérience (sélectionnez l’option **Service web prédictif**).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="d1a5a-142">Pour en savoir plus sur ce qui se passe quand vous convertissez une expérience d’apprentissage en une expérience de prévision, consultez [Guide pratique pour préparer votre modèle au déploiement dans Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="d1a5a-143">Lorsque vous cliquez sur **Configurer le service web**, plusieurs choses se produisent :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="d1a5a-144">Le modèle formé est converti en un module **Modèle formé** et stocké dans la palette de modules située à gauche de la zone de dessin de l’expérience (sous **Modèles formés**).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="d1a5a-145">Les modules qui ont été utilisés pour l’apprentissage sont supprimés :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="d1a5a-146">[Arbre de décision optimisé à deux classes][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="d1a5a-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="d1a5a-147">[Former le modèle][train-model]</span><span class="sxs-lookup"><span data-stu-id="d1a5a-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="d1a5a-148">[Fractionner les données][split]</span><span class="sxs-lookup"><span data-stu-id="d1a5a-148">[Split Data][split]</span></span>
  * <span data-ttu-id="d1a5a-149">Deuxième module [Exécuter le script R][execute-r-script] utilisé pour les données de test</span><span class="sxs-lookup"><span data-stu-id="d1a5a-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="d1a5a-150">Le modèle formé enregistré est rajouté à l’expérience.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="d1a5a-151">Les modules **Entrée du service web** et **Sortie du service web** sont ajoutés (ils identifient où les données de l’utilisateur entrent dans le modèle, ainsi que les données renvoyées lors de l’accès au service web)</span><span class="sxs-lookup"><span data-stu-id="d1a5a-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="d1a5a-152">Vous constatez que l’expérience est enregistrée en deux parties, sous les onglets ajoutés en haut de la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="d1a5a-153">L’expérience de formation d’origine se trouve sous l’onglet **Expérience de formation**, tandis que l’expérience prédictive tout juste créée est sous **Expérience prédictive**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="d1a5a-154">L’expérience prédictive est celle que nous déployons sous la forme d’un service web.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="d1a5a-155">Nous devons effectuer une étape supplémentaire avec cette expérience.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="d1a5a-156">Nous avons ajouté deux modules [Exécuter le script R][execute-r-script] pour pondérer les données.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="d1a5a-157">Cette opération n’étant requise que pour la formation et le test, nous pouvons retirer ces modules du modèle final.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="d1a5a-158">Machine Learning Studio a supprimé un module [Exécuter le script R][execute-r-script] lors de la suppression du module [Fractionner][split].</span><span class="sxs-lookup"><span data-stu-id="d1a5a-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="d1a5a-159">Nous pouvons maintenant supprimer l’autre et relier [Éditeur de métadonnées][metadata-editor] directement à [Noter le modèle][score-model].</span><span class="sxs-lookup"><span data-stu-id="d1a5a-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="d1a5a-160">Notre expérience doit alors ressembler à cela :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-160">Our experiment should now look like this:</span></span>  

![Scoring the trained model][4]  

> [!NOTE]
> <span data-ttu-id="d1a5a-162">Vous vous demandez peut-être pourquoi nous avons laissé le jeu de données Données de carte de crédit allemande UCI dans l’expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="d1a5a-163">Comme ce service va utiliser les données de l’utilisateur et non le jeu de données d’origine, pourquoi conserver ce dernier dans le modèle ?</span><span class="sxs-lookup"><span data-stu-id="d1a5a-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="d1a5a-164">Il est vrai que ce service n'a pas besoin des données de la carte de crédit d'origine.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="d1a5a-165">Mais il a besoin du schéma pour ces données, incluant des informations telles que le nombre de colonnes et lesquelles sont numériques.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="d1a5a-166">Ces informations sur le schéma sont indispensables pour interpréter les données de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="d1a5a-167">Nous laissons ces composants connectés de façon à ce que le module de notation comporte le schéma du jeu de données lorsque le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="d1a5a-168">Les données ne sont pas utilisées, uniquement le schéma.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-168">The data isn't used, just the schema.</span></span>  
> 
> 

<span data-ttu-id="d1a5a-169">Exécutez une dernière fois l’expérience (cliquez sur **Exécuter**). Si vous voulez vérifier que le modèle fonctionne toujours, cliquez sur la sortie du module [Noter le modèle][score-model] et sélectionnez **Afficher les résultats**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-169">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="d1a5a-170">Vous constatez que les données d’origine sont affichées, ainsi que la valeur du risque sur le crédit (« Étiquettes notées ») et la probabilité de la notation (« Probabilités notées »).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-170">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="d1a5a-171">Déploiement du service web</span><span class="sxs-lookup"><span data-stu-id="d1a5a-171">Deploy the web service</span></span>
<span data-ttu-id="d1a5a-172">Vous pouvez déployer l’expérience en tant que service web classique ou nouveau service web basé sur Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-172">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="d1a5a-173">Déployer comme un service web classique</span><span class="sxs-lookup"><span data-stu-id="d1a5a-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="d1a5a-174">Pour déployer un service web classique dérivé de notre expérience, cliquez sur **Déployer le service web** sous la zone de dessin, puis sélectionnez **Déployer le service web [Classique]**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-174">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="d1a5a-175">Machine Learning Studio déploie l’expérience en tant que service web et vous amène au tableau de bord associé à ce service web.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-175">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="d1a5a-176">Depuis cette page, vous pouvez revenir à l’expérience (**Afficher l’instantané** ou **Afficher les dernières**) et exécuter un test simple du service web (voir **Test du service web** ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-176">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="d1a5a-177">En outre, il contient des informations sur la création d’applications pouvant accéder au service web (l’étape suivante de cette procédure pas à pas aborde ce point plus en détail).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-177">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![Tableau de bord du service web][6]

<span data-ttu-id="d1a5a-179">Vous pouvez configurer le service en cliquant sur l'onglet **CONFIGURATION** .</span><span class="sxs-lookup"><span data-stu-id="d1a5a-179">You can configure the service by clicking the **CONFIGURATION** tab.</span></span> <span data-ttu-id="d1a5a-180">Vous pouvez modifier le nom du service (il s'agit par défaut du nom de l'expérience) et lui attribuer une description.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-180">Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="d1a5a-181">Vous pouvez également attribuer des étiquettes plus significatives aux données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-181">You can also give more friendly labels for the input and output data.</span></span>  

![Configuration du service web][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="d1a5a-183">Déployer comme un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="d1a5a-183">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="d1a5a-184">Pour déployer un nouveau service web, vous devez disposer d’autorisations suffisantes dans l’abonnement dans lequel vous déployez le service web.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-184">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="d1a5a-185">Pour en savoir plus, consultez la rubrique [Gérer un service web à l’aide du portail des services web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-185">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="d1a5a-186">Pour déployer un nouveau service web dérivé de notre expérience :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-186">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="d1a5a-187">Cliquez sur **Déployer le service web** sous la zone de dessin, puis sélectionnez **Déployer le service web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-187">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="d1a5a-188">Machine Learning Studio vous redirige vers la page **Deploy Experiment (Déployer l’expérience)** des services web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-188">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="d1a5a-189">Entrez le nom du service web.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-189">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="d1a5a-190">Dans **Price Plan (Plan de tarification)**, choisissez un plan de tarification ou sélectionnez « Créer », nommez le nouveau plan et sélectionnez l’option de plan mensuel.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-190">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="d1a5a-191">Les niveaux de plan s’appliquent par défaut aux plans de votre région par défaut et votre service web est déployé dans cette région.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-191">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="d1a5a-192">Cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-192">Click **Deploy**.</span></span>

<span data-ttu-id="d1a5a-193">Après quelques minutes, la page **Démarrage rapide** de votre service web s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-193">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="d1a5a-194">Vous pouvez configurer le service en cliquant sur l’onglet **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-194">You can configure the service by clicking the **Configure** tab.</span></span> <span data-ttu-id="d1a5a-195">Dans cette page, vous pouvez modifier le nom du service et indiquer une description.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-195">Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="d1a5a-196">Pour tester le service web, cliquez sur l’onglet **Tester** (consultez **Tester le service web** ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="d1a5a-197">Pour plus d’informations sur la création d’applications pouvant accéder au service web, cliquez sur l’onglet **Utiliser** (l’étape suivante de cette procédure pas à pas aborde ce point plus en détail).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="d1a5a-198">Vous pouvez mettre à jour le service web après l’avoir déployé.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="d1a5a-199">Par exemple, si vous souhaitez modifier votre modèle, modifiez l’expérience de formation, ajustez les paramètres du modèle, cliquez sur **Déployer le service web**, puis sélectionnez **Déployer le service web [Classic]** ou **Déployer le service web [Nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="d1a5a-200">Lorsque vous redéployez l’expérience, le service web est remplacé par votre modèle mis à jour.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="d1a5a-201">Test du service web</span><span class="sxs-lookup"><span data-stu-id="d1a5a-201">Test the web service</span></span>

<span data-ttu-id="d1a5a-202">Dans le service web, les données de l’utilisateur transitent par le module **Entrée du service web** puis par le module [Noter le modèle][score-model] où elles sont notées.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="d1a5a-203">Selon notre configuration de l’expérience prédictive, le modèle attend des données dans le même format que le jeu de données de risque de crédit d’origine.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="d1a5a-204">Les résultats sont renvoyés à l’utilisateur par le service web via le module **Sortie du service web**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="d1a5a-205">Conformément à notre configuration de l’expérience prédictive, tous les résultats du module [Noter le modèle][score-model] sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="d1a5a-206">Ces résultats incluent toutes les données d’entrée, ainsi que la valeur du risque de crédit et la probabilité de la notation.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="d1a5a-207">Mais vous pouvez renvoyer quelque chose de différent si vous le souhaitez. Par exemple, vous pouvez retourner simplement la valeur du risque de crédit.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="d1a5a-208">Pour ce faire, insérez un module [Colonnes de projets][project-columns] entre [Noter le modèle][score-model] et **Sortie du service web** pour éliminer les colonnes que vous ne souhaitez pas que le service web renvoie.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="d1a5a-209">Vous pouvez tester le service web Classique dans **Machine Learning Studio** ou dans le portail des **services web Azure Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="d1a5a-210">Vous pouvez tester un nouveau service web uniquement dans le portail **des services web Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="d1a5a-211">Lors du test dans le portail des services web Azure Machine Learning, vous pouvez demander au portail de créer un échantillon de données pour tester le service Demande-Réponse.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="d1a5a-212">Dans la page **Configurer**, sélectionnez « Oui » pour **Échantillon de données activé ?**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="d1a5a-213">Lorsque vous ouvrez l’onglet Demande-Réponse dans la page **Tester**, le portail intègre l’échantillon provenant du jeu de données Risque de crédit.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="d1a5a-214">Tester un service web classique</span><span class="sxs-lookup"><span data-stu-id="d1a5a-214">Test a Classic web service</span></span>

<span data-ttu-id="d1a5a-215">Vous pouvez tester un service web classique dans Machine Learning Studio ou dans le portail des services web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="d1a5a-216">Tester dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="d1a5a-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="d1a5a-217">Sur la page **TABLEAU DE BORD** du service web, cliquez sur le bouton **Test** sous **Point de terminaison par défaut**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="d1a5a-218">La boîte de dialogue qui s’affiche vous demande les données d’entrée du service.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="d1a5a-219">Les colonnes sont identiques à celles du jeu de données d’origine (Risque de crédit).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="d1a5a-220">Entrez un jeu de données, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="d1a5a-221">Tester dans le portail des services web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d1a5a-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="d1a5a-222">Sur la page **TABLEAU DE BORD** du service web, cliquez sur le lien d’aperçu **Test** sous **Point de terminaison par défaut**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="d1a5a-223">La page de test dans le portail des services web Azure Machine Learning pour le point de terminaison de service web s’ouvre en vous invitant à entrer les données du service.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="d1a5a-224">Les colonnes sont identiques à celles du jeu de données d’origine (Risque de crédit).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="d1a5a-225">Cliquez sur **Tester Demande-réponse**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="d1a5a-226">Tester un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="d1a5a-226">Test a New web service</span></span>

<span data-ttu-id="d1a5a-227">Vous pouvez tester un nouveau service web uniquement dans le portail des services web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="d1a5a-228">Dans le portail des [services web Azure Machine Learning](https://services.azureml.net/quickstart), cliquez sur **Tester** en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="d1a5a-229">La page **Test** s’ouvre pour vous permettre d’entrer les données du service.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="d1a5a-230">Les champs d’entrée affichés correspondent à ceux du jeu de données d’origine (Risque de crédit).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="d1a5a-231">Entrez un jeu de données, puis cliquez sur **Test Request-Response**(Tester la requête-réponse).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="d1a5a-232">Les résultats du test apparaissent sur le côté droit de la page, dans la colonne de sortie.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="d1a5a-233">Gérer le service web</span><span class="sxs-lookup"><span data-stu-id="d1a5a-233">Manage the web service</span></span>

### <a name="manage-a-classic-web-service-in-the-azure-classic-portal"></a><span data-ttu-id="d1a5a-234">Gérer un service web classique dans le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="d1a5a-234">Manage a Classic web service in the Azure classic portal</span></span>

<span data-ttu-id="d1a5a-235">Après avoir déployé votre service web classique, vous pouvez le gérer à partir du [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-235">Once you've deployed your Classic web service, you can manage it from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="d1a5a-236">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-236">Sign in to the [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="d1a5a-237">Dans le volet des services Microsoft Azure, cliquez sur **MACHINE LEARNING**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-237">In the Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="d1a5a-238">Cliquez sur votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-238">Click your workspace</span></span>
4. <span data-ttu-id="d1a5a-239">Cliquez sur l’onglet **Services web**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-239">Click the **Web services** tab</span></span>
5. <span data-ttu-id="d1a5a-240">Cliquez sur le service web que nous avons créé</span><span class="sxs-lookup"><span data-stu-id="d1a5a-240">Click the web service we created</span></span>
6. <span data-ttu-id="d1a5a-241">Cliquez sur le point de terminaison « par défaut ».</span><span class="sxs-lookup"><span data-stu-id="d1a5a-241">Click the "default" endpoint</span></span>

<span data-ttu-id="d1a5a-242">À partir de là, vous pouvez effectuer des opérations telles que surveiller le fonctionnement du service web et effectuer des ajustements de performances en modifiant le nombre d’appels simultanés que le service peut gérer.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-242">From here, you can do things like monitor how the web service is doing and make performance tweaks by changing how many concurrent calls the service can handle.</span></span>

<span data-ttu-id="d1a5a-243">Pour plus d'informations, consultez la page suivante :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-243">For more details, see:</span></span>

* [<span data-ttu-id="d1a5a-244">Création de points de terminaison</span><span class="sxs-lookup"><span data-stu-id="d1a5a-244">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="d1a5a-245">Mise à l’échelle du service web</span><span class="sxs-lookup"><span data-stu-id="d1a5a-245">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="d1a5a-246">Gérer un service web classique ou nouveau dans le portail des services web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d1a5a-246">Manage a Classic or New web service in the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="d1a5a-247">Une fois votre service web déployé, qu’il soit classique ou nouveau, vous pouvez le gérer dans le portail [des services web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart).</span><span class="sxs-lookup"><span data-stu-id="d1a5a-247">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="d1a5a-248">Pour surveiller les performances de votre service web :</span><span class="sxs-lookup"><span data-stu-id="d1a5a-248">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="d1a5a-249">Se connecter au [portail des services web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart)</span><span class="sxs-lookup"><span data-stu-id="d1a5a-249">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="d1a5a-250">Cliquez sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-250">Click **Web services**</span></span>
3. <span data-ttu-id="d1a5a-251">Cliquer sur votre service web</span><span class="sxs-lookup"><span data-stu-id="d1a5a-251">Click your web service</span></span>
4. <span data-ttu-id="d1a5a-252">Cliquez sur **Tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="d1a5a-252">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="d1a5a-253">**Étape suivante : [Accéder au service web](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="d1a5a-253">**Next: [Access the web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
