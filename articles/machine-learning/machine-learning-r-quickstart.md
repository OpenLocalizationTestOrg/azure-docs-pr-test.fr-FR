---
title: "Didacticiel de démarrage rapide sur le langage R pour Machine Learning | Microsoft Docs"
description: "Utilisez ce didacticiel sur la programmation R pour prendre en main rapidement l'utilisation du langage R avec Azure Machine Learning Studio afin de créer une solution de prévision."
keywords: "démarrage rapide,langage r,langage de programmation r,didacticiel de programmation en r"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 598f5ce445e520b6cdc347c80f7f3dcbc9c2c9e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="quickstart-tutorial-for-the-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="80be5-104">Didacticiel de démarrage rapide pour le langage de programmation R pour Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="80be5-104">Quickstart tutorial for the R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="80be5-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="80be5-105">Introduction</span></span>
<span data-ttu-id="80be5-106">Ce didacticiel de démarrage rapide vous aide à vous lancer rapidement dans l'extension d'Azure Machine Learning à l'aide du langage de programmation R.</span><span class="sxs-lookup"><span data-stu-id="80be5-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using the R programming language.</span></span> <span data-ttu-id="80be5-107">Suivez ce didacticiel sur la programmation R pour créer, tester et exécuter du code R dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="80be5-107">Follow this R programming tutorial to create, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="80be5-108">Au cours de ce didacticiel de démarrage rapide, vous allez créer une solution de prévision complète à l'aide du langage R dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="80be5-108">As you work through tutorial, you will create a complete forecasting solution by using the R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="80be5-109">Si Microsoft Azure Machine Learning intègre divers modules d’apprentissage automatique et de manipulation de données très efficaces,</span><span class="sxs-lookup"><span data-stu-id="80be5-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="80be5-110">le puissant langage R a été décrit comme la lingua franca de l'analyse.</span><span class="sxs-lookup"><span data-stu-id="80be5-110">The powerful R language has been described as the lingua franca of analytics.</span></span> <span data-ttu-id="80be5-111">Fort heureusement, l’analyse et la manipulation de données dans Azure Machine Learning peuvent être étendues grâce au langage R, qui conjugue à la fois la grande facilité de déploiement d’Azure Machine Learning avec la souplesse et la capacité d’analyse approfondie du langage R.</span><span class="sxs-lookup"><span data-stu-id="80be5-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides the scalability and ease of deployment of Azure Machine Learning with the flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-the-dataset"></a><span data-ttu-id="80be5-112">Prévision et jeu de données</span><span class="sxs-lookup"><span data-stu-id="80be5-112">Forecasting and the dataset</span></span>
<span data-ttu-id="80be5-113">La prévision est une méthode analytique largement répandue et très utile.</span><span class="sxs-lookup"><span data-stu-id="80be5-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="80be5-114">Elle peut servir à établir des prévisions de ventes d'articles saisonniers, à déterminer les niveaux de stock optimaux ou encore à établir des prévisions sur des variables macroéconomiques.</span><span class="sxs-lookup"><span data-stu-id="80be5-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, to predicting macroeconomic variables.</span></span> <span data-ttu-id="80be5-115">La prévision s'appuie généralement sur des modèles chronologiques.</span><span class="sxs-lookup"><span data-stu-id="80be5-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="80be5-116">Les données chronologiques sont des données dont les valeurs ont un index chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-116">Time series data is data in which the values have a time index.</span></span> <span data-ttu-id="80be5-117">L'index chronologique peut être régulier, c'est-à-dire tous les mois ou toutes les minutes, ou irrégulier.</span><span class="sxs-lookup"><span data-stu-id="80be5-117">The time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="80be5-118">Un modèle chronologique repose sur des données chronologiques.</span><span class="sxs-lookup"><span data-stu-id="80be5-118">A time series model is based on time series data.</span></span> <span data-ttu-id="80be5-119">Le langage de programmation R offre une infrastructure souple et des analyses étendues pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-119">The R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="80be5-120">Dans ce guide de démarrage rapide, nous allons utiliser les données de production et de tarification des produits laitiers en Californie.</span><span class="sxs-lookup"><span data-stu-id="80be5-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="80be5-121">Ces données comportent des informations mensuelles sur la production de plusieurs produits laitiers, ainsi que le prix de la matière grasse du lait, produit de base de référence.</span><span class="sxs-lookup"><span data-stu-id="80be5-121">This data includes monthly information on the production of several dairy products and the price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="80be5-122">Les données utilisées dans cet article et les scripts R peuvent être [téléchargés ici][download].</span><span class="sxs-lookup"><span data-stu-id="80be5-122">The data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="80be5-123">À l'origine, ces données ont été synthétisées à partir des informations disponibles sur le site de l'Université du Wisconsin à l'adresse http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="80be5-123">This data was originally synthesized from information available from the University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="80be5-124">Organisation</span><span class="sxs-lookup"><span data-stu-id="80be5-124">Organization</span></span>
<span data-ttu-id="80be5-125">À travers plusieurs étapes successives, vous allez apprendrez à créer, tester et exécuter du code R d’analyse et de manipulation de données dans l’environnement Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="80be5-125">We will progress through several steps as you learn how to create, test and execute analytics and data manipulation R code in the Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="80be5-126">Dans un premier temps, nous explorerons les bases de l’utilisation du langage R dans l’environnement Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-126">First we will explore the basics of using the R language in the Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="80be5-127">Après quoi, nous examinerons différents aspects de l’E/S de données, du code R et des graphiques dans l’environnement Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="80be5-127">Then we progress to discussing various aspects of I/O for data, R code and graphics in the Azure Machine Learning environment.</span></span>
* <span data-ttu-id="80be5-128">Nous œuvrerons ensuite à l'élaboration de la première partie de notre solution de prévision en créant du code destiné à nettoyer et transformer les données.</span><span class="sxs-lookup"><span data-stu-id="80be5-128">We will then construct the first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="80be5-129">Après avoir préparé nos données, nous procéderons à l’analyse des corrélations entre plusieurs variables figurant dans notre jeu de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-129">With our data prepared we will perform an analysis of the correlations between several of the variables in our dataset.</span></span>
* <span data-ttu-id="80be5-130">Enfin, nous créerons un modèle de prévision chronologique saisonnier pour la production de lait.</span><span class="sxs-lookup"><span data-stu-id="80be5-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="80be5-131"><a id="mlstudio"></a>Interaction avec le langage R dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="80be5-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="80be5-132">Cette section vous fait découvrir certains concepts de base de l'interaction avec le langage de programmation R dans l'environnement Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-132">This section takes you through some basics of interacting with the R programming language in the Machine Learning Studio environment.</span></span> <span data-ttu-id="80be5-133">Le langage R offre un outil efficace pour créer des modules d’analyse et de manipulation de données personnalisés au sein de l’environnement Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="80be5-133">The R language provides a powerful tool to create customized analytics and data manipulation modules within the Azure Machine Learning environment.</span></span>

<span data-ttu-id="80be5-134">Nous utiliserons RStudio pour développer, tester et déboguer du code R à petite échelle.</span><span class="sxs-lookup"><span data-stu-id="80be5-134">I will use RStudio to develop, test and debug R code on a small scale.</span></span> <span data-ttu-id="80be5-135">Ce code sera ensuite coupé et collé dans un module d’exécution de script R (ou [Execute R script][execute-r-script]) dans Studio Machine Learning, prêt à être exécuté.</span><span class="sxs-lookup"><span data-stu-id="80be5-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready to run.</span></span>  

### <a name="the-execute-r-script-module"></a><span data-ttu-id="80be5-136">Module d’exécution de script R</span><span class="sxs-lookup"><span data-stu-id="80be5-136">The Execute R Script module</span></span>
<span data-ttu-id="80be5-137">Dans Machine Learning Studio, les scripts R sont exécutés dans le module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-137">Within Machine Learning Studio, R scripts are run within the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80be5-138">Un exemple du module [d’exécution de script R][execute-r-script] dans Machine Learning Studio est illustré dans la figure 1.</span><span class="sxs-lookup"><span data-stu-id="80be5-138">An example of the [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Langage de programmation R : module Execute R Script sélectionné dans Machine Learning Studio][1]

<span data-ttu-id="80be5-140">*Figure 1 : environnement Machine Learning Studio avec le module d’exécution de script R sélectionné.*</span><span class="sxs-lookup"><span data-stu-id="80be5-140">*Figure 1. The Machine Learning Studio environment showing the Execute R Script module selected.*</span></span>

<span data-ttu-id="80be5-141">Dans la figure 1, examinons les principaux éléments de l’environnement Machine Learning Studio permettant de travailler avec le module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-141">Referring to Figure 1, let's look at some of the key parts of the Machine Learning Studio environment for working with the [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="80be5-142">Les modules utilisés dans l'expérimentation se trouvent dans le volet central.</span><span class="sxs-lookup"><span data-stu-id="80be5-142">The modules in the experiment are shown in the center pane.</span></span>
* <span data-ttu-id="80be5-143">La partie supérieure du volet droit contient une fenêtre permettant d'afficher et de modifier les scripts R.</span><span class="sxs-lookup"><span data-stu-id="80be5-143">The upper part of the right pane contains a window to view and edit your R scripts.</span></span>  
* <span data-ttu-id="80be5-144">La partie inférieure du volet droit présente certaines propriétés du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-144">The lower part of right pane shows some properties of the [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="80be5-145">Vous pouvez afficher les journaux d'erreurs et de sortie en cliquant aux endroits appropriés de ce volet.</span><span class="sxs-lookup"><span data-stu-id="80be5-145">You can view the error and output logs by clicking on the appropriate spots of this pane.</span></span>

<span data-ttu-id="80be5-146">Bien entendu, nous reviendrons plus en détail sur le module [d’exécution de script R][execute-r-script] au fil du présent document.</span><span class="sxs-lookup"><span data-stu-id="80be5-146">We will, of course, be discussing the [Execute R Script][execute-r-script] in greater detail in the rest of this document.</span></span>

<span data-ttu-id="80be5-147">Lorsqu'il s'agit d'utiliser des fonctions R complexes, je vous recommande de modifier, tester et déboguer dans RStudio.</span><span class="sxs-lookup"><span data-stu-id="80be5-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="80be5-148">Comme pour tout projet de développement logiciel, développez votre code graduellement et testez-le dans un petit cas de test simple.</span><span class="sxs-lookup"><span data-stu-id="80be5-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="80be5-149">Ensuite, coupez vos fonctions et collez-les dans la fenêtre de script R du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-149">Then cut and paste your functions into the R script window of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80be5-150">Cette approche vous permet d’exploiter l’environnement de développement intégré (IDE) de RStudio et la puissance d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="80be5-150">This approach allows you to harness both the RStudio integrated development environment (IDE) and the power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="80be5-151">Exécution du code R</span><span class="sxs-lookup"><span data-stu-id="80be5-151">Execute R code</span></span>
<span data-ttu-id="80be5-152">Pour exécuter du code R dans le module [d’exécution de script R][execute-r-script], il suffit d’exécuter l’expérimentation en cliquant sur le bouton **Run** (Exécuter).</span><span class="sxs-lookup"><span data-stu-id="80be5-152">Any R code in the [Execute R Script][execute-r-script] module will execute when you run the experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="80be5-153">Une fois l’exécution terminée, une coche apparaît sur l’icône du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-153">When execution has completed, a check mark will appear on the [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="80be5-154">Codage R défensif pour Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="80be5-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="80be5-155">Si vous développez du code R pour, par exemple, un service Web à l’aide d’Azure Machine Learning, vous devez absolument prévoir la façon dont votre code traitera une entrée de données inattendue et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="80be5-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="80be5-156">Dans un souci de clarté, j'ai évité de surcharger les exemples présentés dans ce document de code relevant de la vérification et de la gestion des exceptions.</span><span class="sxs-lookup"><span data-stu-id="80be5-156">To maintain clarity, I have not included much in the way of checking or exception handling in most of the code examples shown.</span></span> <span data-ttu-id="80be5-157">Cependant, je vous montrerai par la suite plusieurs exemples de fonctions qui font appel à la fonctionnalité de gestion des exceptions du langage R.</span><span class="sxs-lookup"><span data-stu-id="80be5-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="80be5-158">Si vous avez besoin d’un exposé plus complet sur la gestion des exceptions R, je vous recommande de lire les sections appropriées du livre de Hadley Wickham cité en référence dans l’ [Annexe B – Informations supplémentaires](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="80be5-158">If you need a more complete treatment of R exception handling, I recommend you read the applicable sections of the book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="80be5-159">Débogage et test du langage R dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="80be5-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="80be5-160">Encore une fois, je vous recommande de tester et de déboguer votre code R à petite échelle dans RStudio.</span><span class="sxs-lookup"><span data-stu-id="80be5-160">To reiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="80be5-161">Cependant, dans certains cas, vous devrez analyser les problèmes de code R dans le module [d’exécution de script R][execute-r-script] lui-même.</span><span class="sxs-lookup"><span data-stu-id="80be5-161">However, there are cases where you will need to track down R code problems in the [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="80be5-162">De plus, vous aurez tout intérêt à vérifier les résultats dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-162">In addition, it is good practice to check your results in Machine Learning Studio.</span></span>

<span data-ttu-id="80be5-163">La sortie résultant de l’exécution de votre code R sur la plateforme Azure Machine Learning se trouve principalement dans le fichier output.log.</span><span class="sxs-lookup"><span data-stu-id="80be5-163">Output from the execution of your R code and on the Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="80be5-164">Vous pourrez trouver des informations complémentaires dans le fichier error.log.</span><span class="sxs-lookup"><span data-stu-id="80be5-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="80be5-165">Si une erreur se produit dans Machine Learning Studio pendant l’exécution de votre code R, vous devez dans un premier temps examiner le fichier error.log.</span><span class="sxs-lookup"><span data-stu-id="80be5-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be to look at error.log.</span></span> <span data-ttu-id="80be5-166">Ce fichier peut contenir des messages d’erreur utiles susceptibles de vous aider à cerner l’erreur et à la corriger.</span><span class="sxs-lookup"><span data-stu-id="80be5-166">This file can contain useful error messages to help you understand and correct your error.</span></span> <span data-ttu-id="80be5-167">Pour afficher le fichier error.log, cliquez sur **View error log** (Afficher le journal d’erreurs) dans le **volet de propriétés** du module [d’exécution de script R][execute-r-script] contenant l’erreur.</span><span class="sxs-lookup"><span data-stu-id="80be5-167">To view error.log, click on **View error log** on the **properties pane** for the [Execute R Script][execute-r-script] containing the error.</span></span>

<span data-ttu-id="80be5-168">Par exemple, j’ai exécuté le code R ci-dessous, avec une variable y non définie, dans un module [d’exécution de script R][execute-r-script] :</span><span class="sxs-lookup"><span data-stu-id="80be5-168">For example, I ran the following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="80be5-169">L'exécution de ce code échoue, ce qui se traduit par une condition d'erreur.</span><span class="sxs-lookup"><span data-stu-id="80be5-169">This code fails to execute, resulting in an error condition.</span></span> <span data-ttu-id="80be5-170">En cliquant sur **Afficher le journal des erreurs** dans le **volet des propriétés**, nous obtenons l’affichage présenté à la figure 2.</span><span class="sxs-lookup"><span data-stu-id="80be5-170">Clicking on **View error log** on the **properties pane** produces the display shown in Figure 2.</span></span>

  ![fenêtre contextuelle de message d’erreur][2]

<span data-ttu-id="80be5-172">*Figure 2 : fenêtre contextuelle de message d’erreur.*</span><span class="sxs-lookup"><span data-stu-id="80be5-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="80be5-173">Il apparaît ici nécessaire de regarder dans le fichier output.log pour consulter le message d’erreur R.</span><span class="sxs-lookup"><span data-stu-id="80be5-173">It looks like we need to look in output.log to see the R error message.</span></span> <span data-ttu-id="80be5-174">Il convient pour cela de cliquer sur le module [d’exécution de script R][execute-r-script] et sur l’élément **View output.log** (Afficher output.log) dans le **volet de propriétés** à droite.</span><span class="sxs-lookup"><span data-stu-id="80be5-174">Click on the [Execute R Script][execute-r-script] and then click on the **View output.log** item on the **properties pane** to the right.</span></span> <span data-ttu-id="80be5-175">Dans la nouvelle fenêtre de navigateur qui s’ouvre, voici les informations qui s’affichent :</span><span class="sxs-lookup"><span data-stu-id="80be5-175">A new browser window opens, and I see the following.</span></span>

    [Critical]     Error: Error 0063: The following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="80be5-176">Ce message d'erreur ne réserve aucune surprise et identifie clairement le problème.</span><span class="sxs-lookup"><span data-stu-id="80be5-176">This error message contains no surprises and clearly identifies the problem.</span></span>

<span data-ttu-id="80be5-177">Pour inspecter la valeur d’un objet dans le code R, vous pouvez imprimer les valeurs dans le fichier output.log.</span><span class="sxs-lookup"><span data-stu-id="80be5-177">To inspect the value of any object in R, you can print these values to the output.log file.</span></span> <span data-ttu-id="80be5-178">Les règles pour examiner les valeurs d'objets sont, pour l'essentiel, identiques à celles d'une session R interactive.</span><span class="sxs-lookup"><span data-stu-id="80be5-178">The rules for examining object values are essentially the same as in an interactive R session.</span></span> <span data-ttu-id="80be5-179">Par exemple, si vous tapez un nom de variable sur une ligne, la valeur de l'objet s'imprime dans le fichier output.log.</span><span class="sxs-lookup"><span data-stu-id="80be5-179">For example, if you type a variable name on a line, the value of the object will be printed to the output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="80be5-180">Packages dans Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="80be5-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="80be5-181">Azure Machine Learning est fourni avec plus de 350 packages de langage R préinstallés.</span><span class="sxs-lookup"><span data-stu-id="80be5-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="80be5-182">Vous pouvez utiliser le code ci-dessous dans le module [d’exécution de script R][execute-r-script] pour extraire la liste des packages préinstallés.</span><span class="sxs-lookup"><span data-stu-id="80be5-182">You can use the following code in the [Execute R Script][execute-r-script] module to retrieve a list of the preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="80be5-183">Si, pour l’heure, vous ne comprenez pas la dernière ligne de ce code, poursuivez la lecture de ce document.</span><span class="sxs-lookup"><span data-stu-id="80be5-183">If you don't understand the last line of this code at the moment, read on.</span></span> <span data-ttu-id="80be5-184">Vous trouverez, dans le reste du présent document, un exposé complet sur l’utilisation du langage R dans l’environnement Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="80be5-184">In the rest of this document we will extensively discuss using R in the Azure Machine Learning environment.</span></span>

### <a name="introduction-to-rstudio"></a><span data-ttu-id="80be5-185">Présentation de RStudio</span><span class="sxs-lookup"><span data-stu-id="80be5-185">Introduction to RStudio</span></span>
<span data-ttu-id="80be5-186">RStudio est un environnement de développement intégré (IDE) pour R couramment utilisé. C’est l’outil que j’utiliserai pour modifier, tester et déboguer une partie du code R utilisé dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="80be5-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of the R code used in this quick start guide.</span></span> <span data-ttu-id="80be5-187">Une fois le code R testé et prêt, il suffit de le couper dans l’éditeur RStudio et de le coller dans un module [d’exécution de script R][execute-r-script] de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-187">Once R code is tested and ready, you simply cut and paste from the RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="80be5-188">Si vous n'avez pas encore installé le langage de programmation R sur votre ordinateur de bureau, je vous conseille de le faire dès maintenant.</span><span class="sxs-lookup"><span data-stu-id="80be5-188">If you do not have the R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="80be5-189">Des versions open source du langage R sont disponibles en téléchargement gratuit dans la section CRAN (Comprehensive R Archive Network) du site [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="80be5-189">Free downloads of open source R language are available at the Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="80be5-190">Il existe des versions Windows, Mac OS et Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="80be5-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="80be5-191">Choisissez un site miroir voisin et suivez les instructions de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="80be5-191">Choose a nearby mirror and follow the download directions.</span></span> <span data-ttu-id="80be5-192">Par ailleurs, le section CRAN contient de nombreux packages d'analyse et de manipulation de données fort utiles.</span><span class="sxs-lookup"><span data-stu-id="80be5-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="80be5-193">Si vous débutez avec RStudio, téléchargez et installez la version pour ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="80be5-193">If you are new to RStudio, you should download and install the desktop version.</span></span> <span data-ttu-id="80be5-194">Les versions Windows, Mac OS et Linux/UNIX de RStudio sont disponibles en téléchargement à l’adresse http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="80be5-194">You can find the RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="80be5-195">Suivez les instructions qui vous sont fournies pour installer RStudio sur votre ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="80be5-195">Follow the directions provided to install RStudio on your desktop machine.</span></span>  

<span data-ttu-id="80be5-196">Un didacticiel de présentation de RStudio est disponible à l’adresse https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="80be5-196">A tutorial introduction to RStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="80be5-197">Vous trouverez des informations complémentaires sur l’utilisation de RStudio dans [l’Annexe A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="80be5-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="80be5-198"><a id="scriptmodule"></a>Obtention de données dans et hors du module d'exécution de script R</span><span class="sxs-lookup"><span data-stu-id="80be5-198"><a id="scriptmodule"></a>Get data in and out of the Execute R Script module</span></span>
<span data-ttu-id="80be5-199">Dans cette section, nous allons voir comment obtenir des données dans et hors du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-199">In this section we will discuss how you get data into and out of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80be5-200">Nous examinerons les façons de gérer les différents types de données lus dans et hors du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-200">We will review how to handle various data types read into and out of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="80be5-201">Le code complet de cette section se trouve dans le fichier zip téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="80be5-201">The complete code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="80be5-202">Chargement et vérification des données dans Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="80be5-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="80be5-203"><a id="loading"></a>Chargement du jeu de données</span><span class="sxs-lookup"><span data-stu-id="80be5-203"><a id="loading"></a>Load the dataset</span></span>
<span data-ttu-id="80be5-204">Nous allons commencer par charger le fichier **csdairydata.csv** dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-204">We will start by loading the **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="80be5-205">Démarrez votre environnement Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="80be5-206">Cliquez sur **+ NEW** en bas à gauche de votre écran, puis sélectionnez **Jeu de données**.</span><span class="sxs-lookup"><span data-stu-id="80be5-206">Click on **+ NEW** at the lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="80be5-207">Sélectionnez **From Local File** (Depuis un fichier local), puis **Browse** (Parcourir) pour sélectionner le fichier.</span><span class="sxs-lookup"><span data-stu-id="80be5-207">Select **From Local File**, and then **Browse** to select the file.</span></span>
* <span data-ttu-id="80be5-208">Veillez à sélectionner **Generic CSV file with header (.csv)** (Fichier CSV générique avec en-tête) comme type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-208">Make sure you have selected **Generic CSV file with header (.csv)** as the type for the dataset.</span></span>
* <span data-ttu-id="80be5-209">Cliquez sur la coche.</span><span class="sxs-lookup"><span data-stu-id="80be5-209">Click the check mark.</span></span>
* <span data-ttu-id="80be5-210">Une fois le jeu de données téléchargé, vous devez voir le nouveau jeu de données en cliquant sur l’onglet **Datasets** (Jeux de données).</span><span class="sxs-lookup"><span data-stu-id="80be5-210">After the dataset has been uploaded, you should see the new dataset by clicking on the **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="80be5-211">Création d'une expérience</span><span class="sxs-lookup"><span data-stu-id="80be5-211">Create an experiment</span></span>
<span data-ttu-id="80be5-212">Maintenant que Machine Learning Studio contient des données, nous devons créer une expérimentation pour faire l’analyse.</span><span class="sxs-lookup"><span data-stu-id="80be5-212">Now that we have some data in Machine Learning Studio, we need to create an experiment to do the analysis.</span></span>  

* <span data-ttu-id="80be5-213">Cliquez sur **+ NEW** en bas à gauche, sélectionnez **Experiment** (Expérimentation), puis **Blank Experiment** (Expérimentation à blanc).</span><span class="sxs-lookup"><span data-stu-id="80be5-213">Click on **+ NEW** at the lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="80be5-214">Vous pouvez nommer votre expérimentation en sélectionnant et en modifiant le titre **Experiment created on...** (Expérimentation créée sur) en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="80be5-214">You can name your experiment by selecting, and modifying, the **Experiment created on ...** title at the top of the page.</span></span> <span data-ttu-id="80be5-215">Vous pouvez par exemple le modifier en **CA Dairy Analysis**.</span><span class="sxs-lookup"><span data-stu-id="80be5-215">For example, changing it to **CA Dairy Analysis**.</span></span>
* <span data-ttu-id="80be5-216">Sur la gauche de la page d’expérimentation, développez **Saved Datasets** (Jeux de données enregistrés), puis **My Datasets** (Mes jeux de données).</span><span class="sxs-lookup"><span data-stu-id="80be5-216">On the left of the experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="80be5-217">Vous devez voir le fichier **cadairydata.csv** que vous avez téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="80be5-217">You should see the **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="80be5-218">Glissez-déplacez le **jeu de données csdairydata.csv** vers l’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="80be5-218">Drag and drop the **csdairydata.csv dataset** onto the experiment.</span></span>
* <span data-ttu-id="80be5-219">Dans la zone **Search experiment items** (Rechercher dans les éléments de l’expérimentation) en haut du volet gauche, tapez [Execute R Script][execute-r-script] (Exécution de script R).</span><span class="sxs-lookup"><span data-stu-id="80be5-219">In the **Search experiment items** box on the top of the left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="80be5-220">Le module s'affiche alors dans la liste de recherche.</span><span class="sxs-lookup"><span data-stu-id="80be5-220">You will see the module appear in the search list.</span></span>
* <span data-ttu-id="80be5-221">Glissez-déplacez le module [d’exécution de script R][execute-r-script] vers votre palette.</span><span class="sxs-lookup"><span data-stu-id="80be5-221">Drag and drop the [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="80be5-222">Reliez la sortie du **jeu de données csdairydata.csv** à la première entrée (**Jeu de données 1**) du module [d’exécution de script R][execute-r-script] en partant de la gauche.</span><span class="sxs-lookup"><span data-stu-id="80be5-222">Connect the output of the **csdairydata.csv dataset** to the leftmost input (**Dataset1**) of the [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="80be5-223">**N’oubliez pas de cliquer sur « Save » (Enregistrer) !**</span><span class="sxs-lookup"><span data-stu-id="80be5-223">**Don't forget to click on 'Save'!**</span></span>  

<span data-ttu-id="80be5-224">À ce stade, votre expérimentation doit être similaire à la figure 3.</span><span class="sxs-lookup"><span data-stu-id="80be5-224">At this point your experiment should look something like Figure 3.</span></span>

![l’expérimentation CA Dairy Analysis avec le jeu de données et le module d’exécution de script R][3]

<span data-ttu-id="80be5-226">*Figure 3 : l’expérimentation CA Dairy Analysis avec le jeu de données et le module d’exécution de script R.*</span><span class="sxs-lookup"><span data-stu-id="80be5-226">*Figure 3. The CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-the-data"></a><span data-ttu-id="80be5-227">Vérification des données</span><span class="sxs-lookup"><span data-stu-id="80be5-227">Check on the data</span></span>
<span data-ttu-id="80be5-228">Examinons les données que nous avons chargées dans l'expérimentation.</span><span class="sxs-lookup"><span data-stu-id="80be5-228">Let's have a look at the data we have loaded into our experiment.</span></span> <span data-ttu-id="80be5-229">Dans l’expérimentation, cliquez sur la sortie du **jeu de données cadairydata.csv**, puis sélectionnez **Visualize** (Visualiser).</span><span class="sxs-lookup"><span data-stu-id="80be5-229">In the experiment, click on the output of the **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="80be5-230">Vous obtenez un résultat analogue à la figure 4.</span><span class="sxs-lookup"><span data-stu-id="80be5-230">You should see something like Figure 4.</span></span>  

![aperçu du jeu de données cadairydata.csv][4]

<span data-ttu-id="80be5-232">*Figure 4 : aperçu du jeu de données cadairydata.csv.*</span><span class="sxs-lookup"><span data-stu-id="80be5-232">*Figure 4. Summary of the cadairydata.csv dataset.*</span></span>

<span data-ttu-id="80be5-233">Cette vue contient de nombreuses informations utiles.</span><span class="sxs-lookup"><span data-stu-id="80be5-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="80be5-234">Les premières lignes de ce jeu de données apparaissent également.</span><span class="sxs-lookup"><span data-stu-id="80be5-234">We can see the first several rows of that dataset.</span></span> <span data-ttu-id="80be5-235">Si nous sélectionnons une colonne, la section des statistiques affiche plus d'informations sur cette colonne.</span><span class="sxs-lookup"><span data-stu-id="80be5-235">If we select a column, the Statistics section shows more information about the column.</span></span> <span data-ttu-id="80be5-236">Par exemple, la ligne Feature Type indique les types de données qui sont affectés à la colonne par Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-236">For example, the Feature Type row shows us what data types Azure Machine Learning Studio assigned to the column.</span></span> <span data-ttu-id="80be5-237">Il est judicieux d'effectuer un contrôle rapide de ce type avant de se lancer dans un travail sérieux.</span><span class="sxs-lookup"><span data-stu-id="80be5-237">Having a quick look like this is a good sanity check before we start to do any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="80be5-238">Premier script R</span><span class="sxs-lookup"><span data-stu-id="80be5-238">First R script</span></span>
<span data-ttu-id="80be5-239">Créons un premier script R simple pour l’expérimenter dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-239">Let's create a simple first R script to experiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="80be5-240">J’ai créé et testé le script suivant dans RStudio :</span><span class="sxs-lookup"><span data-stu-id="80be5-240">I have created and tested the following script in RStudio.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="80be5-241">Je dois maintenant transférer ce script dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-241">Now I need to transfer this script to Azure Machine Learning Studio.</span></span> <span data-ttu-id="80be5-242">Je pourrais simplement effectuer un couper-coller.</span><span class="sxs-lookup"><span data-stu-id="80be5-242">I could simply cut and paste.</span></span> <span data-ttu-id="80be5-243">Mais je vais ici transférer le script R via un fichier zip.</span><span class="sxs-lookup"><span data-stu-id="80be5-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-to-the-execute-r-script-module"></a><span data-ttu-id="80be5-244">Entrée de données dans le module d'exécution de script R</span><span class="sxs-lookup"><span data-stu-id="80be5-244">Data input to the Execute R Script module</span></span>
<span data-ttu-id="80be5-245">Penchons-nous sur les entrées du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-245">Let's have a look at the inputs to the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80be5-246">En l’occurrence, nous allons examiner les données du secteur laitier californien dans le module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-246">In this example we will read the California dairy data into the [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="80be5-247">Il existe trois types d’entrée possibles pour le module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-247">There are three possible inputs for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80be5-248">Selon votre application, vous pouvez utiliser une ou toutes ces entrées.</span><span class="sxs-lookup"><span data-stu-id="80be5-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="80be5-249">Il est aussi tout à fait envisageable d’utiliser un script R qui ne prenne aucune entrée.</span><span class="sxs-lookup"><span data-stu-id="80be5-249">It is also perfectly reasonable to use an R script that takes no input at all.</span></span>  

<span data-ttu-id="80be5-250">Passons en revue chacune de ces entrées, de gauche à droite.</span><span class="sxs-lookup"><span data-stu-id="80be5-250">Let's look at each of these inputs, going from left to right.</span></span> <span data-ttu-id="80be5-251">Pour afficher le nom d’une entrée, il suffit de placer le curseur sur l’entrée en question et de lire l’infobulle.</span><span class="sxs-lookup"><span data-stu-id="80be5-251">You can see the names of each of the inputs by placing your cursor over the input and reading the tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="80be5-252">Script groupé</span><span class="sxs-lookup"><span data-stu-id="80be5-252">Script Bundle</span></span>
<span data-ttu-id="80be5-253">L’entrée de script groupé permet de transmettre le contenu d’un fichier zip au module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-253">The Script Bundle input allows you to pass the contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80be5-254">Vous pouvez utiliser l’une des commandes suivantes pour lire le contenu du fichier zip dans votre code R :</span><span class="sxs-lookup"><span data-stu-id="80be5-254">You can use one of the following commands to read the contents of the zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="80be5-255">Azure Machine Learning traite les fichiers contenus dans le zip comme s’ils se trouvaient dans le répertoire src/. Il est donc nécessaire de faire précéder les noms des fichiers du nom de ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="80be5-255">Azure Machine Learning treats files in the zip as if they are in the src/ directory, so you need to prefix your file names with this directory name.</span></span> <span data-ttu-id="80be5-256">Par exemple, si le fichier zip contient les fichiers `yourfile.R` et `yourData.rdata` à sa racine, vous devez les traiter en tant que `src/yourfile.R` et `src/yourData.rdata` quand vous utilisez `source` et `load`.</span><span class="sxs-lookup"><span data-stu-id="80be5-256">For example, if the zip contains the files `yourfile.R` and `yourData.rdata` in the root of the zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="80be5-257">Nous avons déjà abordé la question du chargement des jeux de données dans la section [Chargement du jeu de données](#loading).</span><span class="sxs-lookup"><span data-stu-id="80be5-257">We already discussed loading datasets in [Loading the dataset](#loading).</span></span> <span data-ttu-id="80be5-258">Dès que vous avez créé et testé le script R présenté dans la section précédente, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80be5-258">Once you have created and tested the R script shown in the previous section, do the following:</span></span>

1. <span data-ttu-id="80be5-259">Enregistrez le script R dans un fichier .R.</span><span class="sxs-lookup"><span data-stu-id="80be5-259">Save the R script into a .R file.</span></span> <span data-ttu-id="80be5-260">J'appelle mon fichier de script « simpleplot.R ».</span><span class="sxs-lookup"><span data-stu-id="80be5-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="80be5-261">Voici le contenu.</span><span class="sxs-lookup"><span data-stu-id="80be5-261">Here's the contents.</span></span>
   
        ## Only one of the following two lines should be used
        ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
        ## If in RStudio, use the second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## The following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="80be5-262">Créez un fichier zip et copiez votre script dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="80be5-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="80be5-263">Dans Windows, vous pouvez cliquer avec le bouton droit sur le fichier, sélectionner **Envoyer vers**, puis **Dossier compressé**.</span><span class="sxs-lookup"><span data-stu-id="80be5-263">On Windows, you can right-click on the file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="80be5-264">Vous créez ainsi un fichier zip contenant le fichier « simpleplot.R ».</span><span class="sxs-lookup"><span data-stu-id="80be5-264">This will create a new zip file containing the "simpleplot.R" file.</span></span>
3. <span data-ttu-id="80be5-265">Ajoutez ce dernier aux **jeux de données** dans Machine Learning Studio, en spécifiant le type **zip**.</span><span class="sxs-lookup"><span data-stu-id="80be5-265">Add your file to the **datasets** in Machine Learning Studio, specifying the type as **zip**.</span></span> <span data-ttu-id="80be5-266">Le fichier zip doit dès lors figurer dans vos jeux de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-266">You should now see the zip file in your datasets.</span></span>
4. <span data-ttu-id="80be5-267">Glissez-déplacez le fichier zip des **jeux de données** vers le **canevas ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="80be5-267">Drag and drop the zip file from **datasets** onto the **ML Studio canvas**.</span></span>
5. <span data-ttu-id="80be5-268">Reliez la sortie de l’icône des **données zip** à l’entrée de **script groupé** du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-268">Connect the output of the **zip data** icon to the **Script Bundle** input of the [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="80be5-269">Tapez la fonction `source()` avec le nom de votre fichier zip dans la fenêtre de code du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-269">Type the `source()` function with your zip file name into the code window for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80be5-270">Dans mon cas, j’ai saisi `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="80be5-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="80be5-271">Pensez à cliquer sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="80be5-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="80be5-272">Une fois ces étapes effectuées, le module [d’exécution de script R][execute-r-script] exécute le script R du fichier zip quand l’expérimentation est exécutée.</span><span class="sxs-lookup"><span data-stu-id="80be5-272">Once these steps are complete, the [Execute R Script][execute-r-script] module will execute the R script in the zip file when the experiment is run.</span></span> <span data-ttu-id="80be5-273">À ce stade, votre expérimentation doit être similaire à la figure 5.</span><span class="sxs-lookup"><span data-stu-id="80be5-273">At this point your experiment should look something like Figure 5.</span></span>

![expérimentation utilisant le script R compressé][6]

<span data-ttu-id="80be5-275">*Figure 5 : expérimentation utilisant le script R compressé.*</span><span class="sxs-lookup"><span data-stu-id="80be5-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="80be5-276">Jeu de données 1</span><span class="sxs-lookup"><span data-stu-id="80be5-276">Dataset1</span></span>
<span data-ttu-id="80be5-277">Vous pouvez transmettre une table de données rectangulaire à votre code R utilisant l’entrée Jeu de données 1.</span><span class="sxs-lookup"><span data-stu-id="80be5-277">You can pass a rectangular table of data to your R code by using the Dataset1 input.</span></span> <span data-ttu-id="80be5-278">Dans notre script simple, la fonction `maml.mapInputPort(1)` lit les données du port 1.</span><span class="sxs-lookup"><span data-stu-id="80be5-278">In our simple script the `maml.mapInputPort(1)` function reads the data from port 1.</span></span> <span data-ttu-id="80be5-279">Ces données sont ensuite affectées à un nom de variable de tableau de données (« dataframe ») dans votre code.</span><span class="sxs-lookup"><span data-stu-id="80be5-279">This data is then assigned to a dataframe variable name in your code.</span></span> <span data-ttu-id="80be5-280">Dans notre script simple, la première ligne de code mène à bien l'affectation.</span><span class="sxs-lookup"><span data-stu-id="80be5-280">In our simple script the first line of code performs the assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="80be5-281">Exécutez votre expérimentation en cliquant sur le bouton **Run** (Exécuter).</span><span class="sxs-lookup"><span data-stu-id="80be5-281">Execute your experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="80be5-282">À la fin de l’exécution, cliquez sur le module [d’exécution de script R][execute-r-script], puis sur **View output log** (Afficher le journal de sortie) dans le volet de propriétés.</span><span class="sxs-lookup"><span data-stu-id="80be5-282">When the execution finishes, click on the [Execute R Script][execute-r-script] module and then click **View output log** on the properties pane.</span></span> <span data-ttu-id="80be5-283">Une nouvelle page doit s’ouvrir dans votre navigateur en affichant le contenu du fichier output.log.</span><span class="sxs-lookup"><span data-stu-id="80be5-283">A new page should appear in your browser showing the contents of the output.log file.</span></span> <span data-ttu-id="80be5-284">Si vous faites défiler l’écran vers le bas, vous devez voir quelque chose de similaire à ceci :</span><span class="sxs-lookup"><span data-stu-id="80be5-284">When you scroll down you should see something like the following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="80be5-285">Plus bas dans la page, vous trouverez des informations détaillées sur les colonnes, qui ressemblent à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="80be5-285">Farther down the page is more detailed information on the columns, which will look something like the following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="80be5-286">Pour l'essentiel, ces résultats sont conformes aux attentes, avec 228 observations et 9 colonnes dans le tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-286">These results are mostly as expected, with 228 observations and 9 columns in the dataframe.</span></span> <span data-ttu-id="80be5-287">Nous pouvons voir les noms de colonnes, le type de données R et un exemple de chaque colonne.</span><span class="sxs-lookup"><span data-stu-id="80be5-287">We can see the column names, the R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="80be5-288">Pratique, cette même sortie imprimée est disponible depuis la sortie de l’appareil R du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-288">This same printed output is conveniently available from the R Device output of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80be5-289">Nous évoquerons les sorties du module [d’exécution de script R][execute-r-script] dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="80be5-289">We will discuss the outputs of the [Execute R Script][execute-r-script] module in the next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="80be5-290">Jeu de données 2</span><span class="sxs-lookup"><span data-stu-id="80be5-290">Dataset2</span></span>
<span data-ttu-id="80be5-291">Le comportement de l'entrée Jeu de données 2 est identique à Jeu de données 1.</span><span class="sxs-lookup"><span data-stu-id="80be5-291">The behavior of the Dataset2 input is identical to that of Dataset1.</span></span> <span data-ttu-id="80be5-292">Avec cette entrée, vous pouvez transmettre une deuxième table de données rectangulaire à votre code R.</span><span class="sxs-lookup"><span data-stu-id="80be5-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="80be5-293">Pour transmettre ces données, la fonction `maml.mapInputPort(2)`est utilisée avec l’argument 2.</span><span class="sxs-lookup"><span data-stu-id="80be5-293">The function `maml.mapInputPort(2)`, with the argument 2, is used to pass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="80be5-294">Sorties du module d'exécution de script R</span><span class="sxs-lookup"><span data-stu-id="80be5-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="80be5-295">Sortie d'un tableau de données</span><span class="sxs-lookup"><span data-stu-id="80be5-295">Output a dataframe</span></span>
<span data-ttu-id="80be5-296">Vous pouvez sortir le contenu d’un tableau de données R sous forme de table rectangulaire via le port du Jeu de données 1 de résultat en utilisant la fonction `maml.mapOutputPort()` .</span><span class="sxs-lookup"><span data-stu-id="80be5-296">You can output the contents of an R dataframe as a rectangular table through the Result Dataset1 port by using the `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="80be5-297">Dans notre script R simple, cette opération est exécutée par la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="80be5-297">In our simple R script this is performed by the following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="80be5-298">Après avoir exécuté l’expérimentation, cliquez sur le port de sortie du Jeu de données 1 de résultat, puis sur **Visualize**(Visualiser).</span><span class="sxs-lookup"><span data-stu-id="80be5-298">After running the experiment, click on the Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="80be5-299">Vous obtenez un résultat analogue à la figure 6.</span><span class="sxs-lookup"><span data-stu-id="80be5-299">You should see something like Figure 6.</span></span>

![visualisation de la sortie des données du secteur laitier californien][7]

<span data-ttu-id="80be5-301">*Figure 6 : visualisation de la sortie des données du secteur laitier californien.*</span><span class="sxs-lookup"><span data-stu-id="80be5-301">*Figure 6. The visualization of the output of the California dairy data.*</span></span>

<span data-ttu-id="80be5-302">Cette sortie est identique à l'entrée, exactement comme nous l'attendions.</span><span class="sxs-lookup"><span data-stu-id="80be5-302">This output looks identical to the input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="80be5-303">Sortie de l’appareil R</span><span class="sxs-lookup"><span data-stu-id="80be5-303">R Device output</span></span>
<span data-ttu-id="80be5-304">La sortie de l’appareil du module [d’exécution de script R][execute-r-script] contient des messages et une sortie graphique.</span><span class="sxs-lookup"><span data-stu-id="80be5-304">The Device output of the [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="80be5-305">La sortie et les messages d'erreur standard de R sont envoyés au port de sortie de l’appareil R.</span><span class="sxs-lookup"><span data-stu-id="80be5-305">Both standard output and standard error messages from R are sent to the R Device output port.</span></span>  

<span data-ttu-id="80be5-306">Pour afficher la sortie de l’appareil R, cliquez sur le port, puis sur **Visualize**(Visualiser).</span><span class="sxs-lookup"><span data-stu-id="80be5-306">To view the R Device output, click on the port and then on **Visualize**.</span></span> <span data-ttu-id="80be5-307">La sortie et l'erreur standard du script R sont présentées dans la figure 7.</span><span class="sxs-lookup"><span data-stu-id="80be5-307">We see the standard output and standard error from the R script in Figure 7.</span></span>

![sortie et erreur standard du port de l’appareil R][8]

<span data-ttu-id="80be5-309">*Figure 7 : sortie et erreur standard du port de l’appareil R.*</span><span class="sxs-lookup"><span data-stu-id="80be5-309">*Figure 7. Standard output and standard error from the R Device port.*</span></span>

<span data-ttu-id="80be5-310">En faisant défiler l'écran vers le bas, nous voyons la sortie graphique de notre script R, qui est présentée dans la figure 8.</span><span class="sxs-lookup"><span data-stu-id="80be5-310">Scrolling down we see the graphics output from our R script in Figure 8.</span></span>  

![sortie graphique du port de l’appareil R][9]

<span data-ttu-id="80be5-312">*Figure 8 : sortie graphique du port d’appareil R.*</span><span class="sxs-lookup"><span data-stu-id="80be5-312">*Figure 8. Graphics output from the R Device port.*</span></span>  

## <span data-ttu-id="80be5-313"><a id="filtering"></a>Filtrage et transformation des données</span><span class="sxs-lookup"><span data-stu-id="80be5-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="80be5-314">Dans cette section, nous allons effectuer certaines opérations de filtrage et de transformation de données de base sur les données du secteur laitier californien.</span><span class="sxs-lookup"><span data-stu-id="80be5-314">In this section we will perform some basic data filtering and transformation operations on the California dairy data.</span></span> <span data-ttu-id="80be5-315">À la fin de cette section, les données seront dans un format idoine pour générer un modèle d'analyse.</span><span class="sxs-lookup"><span data-stu-id="80be5-315">By the end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="80be5-316">Plus particulièrement, nous allons effectuer dans cette section plusieurs tâches courantes de nettoyage et de transformation de données ; de transformation de types, de filtrage sur des tableaux de données, d’ajout de nouvelles colonnes calculées et de transformation de valeurs.</span><span class="sxs-lookup"><span data-stu-id="80be5-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="80be5-317">Cette expérience vous aidera à faire face aux diverses cas de figure rencontrés dans les problèmes réels.</span><span class="sxs-lookup"><span data-stu-id="80be5-317">This background should help you deal with the many variations encountered in real-world problems.</span></span>

<span data-ttu-id="80be5-318">Le code R complet de cette section est disponible dans le fichier zip que vous avez téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="80be5-318">The complete R code for this section is available in the zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="80be5-319">Transformations de types</span><span class="sxs-lookup"><span data-stu-id="80be5-319">Type transformations</span></span>
<span data-ttu-id="80be5-320">Maintenant que nous pouvons lire les données du secteur laitier californien dans le code R du module [d’exécution de script R][execute-r-script], nous devons nous assurer que les données contenues dans les colonnes ont un type et un format appropriés.</span><span class="sxs-lookup"><span data-stu-id="80be5-320">Now that we can read the California dairy data into the R code in the [Execute R Script][execute-r-script] module, we need to ensure that the data in the columns has the intended type and format.</span></span>  

<span data-ttu-id="80be5-321">Le langage R est dynamiquement typé, ce qui signifie que les types de données sont convertis de force d'un type vers un autre, selon les besoins.</span><span class="sxs-lookup"><span data-stu-id="80be5-321">R is a dynamically typed language, which means that data types are coerced from one to another as required.</span></span> <span data-ttu-id="80be5-322">Le langage R compte les types de données atomiques suivants : numérique, logique et caractère.</span><span class="sxs-lookup"><span data-stu-id="80be5-322">The atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="80be5-323">Le type facteur est utilisé pour stocker de manière compacte les données relatives aux catégories.</span><span class="sxs-lookup"><span data-stu-id="80be5-323">The factor type is used to compactly store categorical data.</span></span> <span data-ttu-id="80be5-324">Vous trouverez des informations bien plus complètes sur les types de données dans les références fournies dans l’ [Annexe B - Informations supplémentaires](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="80be5-324">You can find much more information on data types in the references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="80be5-325">Quand des données tabulaires sont lues dans du code R à partir d'une source externe, il est toujours judicieux de vérifier les types résultants dans les colonnes.</span><span class="sxs-lookup"><span data-stu-id="80be5-325">When tabular data is read into R from an external source, it is always a good idea to check the resulting types in the columns.</span></span> <span data-ttu-id="80be5-326">Vous pouvez espérer obtenir une colonne de type caractère, mais dans de nombreux cas, elle se présentera sous forme de facteur ou inversement.</span><span class="sxs-lookup"><span data-stu-id="80be5-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="80be5-327">Dans d’autres cas, une colonne qui selon vous devrait être de type numérique pourra être représentée par des données caractères, par exemple, « 1,23 » au lieu du nombre à virgule flottante 1,23.</span><span class="sxs-lookup"><span data-stu-id="80be5-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="80be5-328">Heureusement, il est facile de convertir un type dans un autre, dans la mesure où le mappage est possible.</span><span class="sxs-lookup"><span data-stu-id="80be5-328">Fortunately, it is easy to convert one type to another, as long as mapping is possible.</span></span> <span data-ttu-id="80be5-329">Par exemple, vous ne pouvez pas convertir « Nevada » en valeur numérique, mais vous pouvez la convertir en facteur (variable catégorique).</span><span class="sxs-lookup"><span data-stu-id="80be5-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it to a factor (categorical variable).</span></span> <span data-ttu-id="80be5-330">De même, vous pouvez convertir la valeur numérique 1 en caractère « 1 » ou en facteur.</span><span class="sxs-lookup"><span data-stu-id="80be5-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="80be5-331">La syntaxe utilisée pour ces conversions est simple : `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="80be5-331">The syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="80be5-332">Ces fonctions de conversion de type sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="80be5-332">These type conversion functions include the following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="80be5-333">En examinant les types des données affichées dans les colonnes que nous avons entrées à la section précédente, nous constatons que toutes les colonnes sont de type numérique, à l’exception de la colonne intitulée « Month », qui est de type caractère.</span><span class="sxs-lookup"><span data-stu-id="80be5-333">Looking at the data types of the columns we input in the previous section: all columns are of type numeric, except for the column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="80be5-334">Convertissons-la en facteur et vérifions les résultats.</span><span class="sxs-lookup"><span data-stu-id="80be5-334">Let's convert this to a factor and test the results.</span></span>  

<span data-ttu-id="80be5-335">J’ai supprimé la ligne qui a créé la matrice de nuage de points et ajouté une ligne convertissant la colonne « Month » en facteur.</span><span class="sxs-lookup"><span data-stu-id="80be5-335">I have deleted the line that created the scatterplot matrix and added a line converting the 'Month' column to a factor.</span></span> <span data-ttu-id="80be5-336">Dans mon expérimentation, je vais simplement couper et coller le code R dans la fenêtre de code du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-336">In my experiment I will just cut and paste the R code into the code window of the [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="80be5-337">Une autre possibilité aurait été de mettre à jour le fichier zip et de le télécharger dans Azure Machine Learning Studio, mais cette opération nécessite plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="80be5-337">You could also update the zip file and upload it to Azure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check the result
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="80be5-338">Exécutons ce code et examinons le journal de sortie pour le script R.</span><span class="sxs-lookup"><span data-stu-id="80be5-338">Let's execute this code and look at the output log for the R script.</span></span> <span data-ttu-id="80be5-339">Les données pertinentes du journal sont affichées dans la figure 9.</span><span class="sxs-lookup"><span data-stu-id="80be5-339">The relevant data from the log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="80be5-340">*Figure 9 : aperçu du tableau de données avec une variable facteur.*</span><span class="sxs-lookup"><span data-stu-id="80be5-340">*Figure 9. Summary of the dataframe with a factor variable.*</span></span>

<span data-ttu-id="80be5-341">Le type de la colonne Month doit à présent indiquer «**Factor w/ 14 levels**» (Facteur à 14 niveaux).</span><span class="sxs-lookup"><span data-stu-id="80be5-341">The type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="80be5-342">C'est un problème, car une année ne compte que 12 mois.</span><span class="sxs-lookup"><span data-stu-id="80be5-342">This is a problem since there are only 12 months in the year.</span></span> <span data-ttu-id="80be5-343">Vous pouvez aussi vérifier que le type qui apparaît dans la **visualisation** du port du jeu de données de résultat est **Categorical** (Catégorique).</span><span class="sxs-lookup"><span data-stu-id="80be5-343">You can also check to see that the type in **Visualize** of the Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="80be5-344">Le problème, c'est que la colonne « Month » n'a pas été codée de façon systématique.</span><span class="sxs-lookup"><span data-stu-id="80be5-344">The problem is that the 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="80be5-345">Le nom du mois sera dans certains cas affiché en toutes lettres (avril) et dans d’autres, il sera abrégé (avr.). Ce problème peut être résolu en limitant la chaîne à 3 caractères.</span><span class="sxs-lookup"><span data-stu-id="80be5-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming the string to 3 characters.</span></span> <span data-ttu-id="80be5-346">La ligne de code se présente désormais comme suit :</span><span class="sxs-lookup"><span data-stu-id="80be5-346">The line of code now looks like the following:</span></span>

    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="80be5-347">Relancez l'expérimentation et affichez le journal de sortie.</span><span class="sxs-lookup"><span data-stu-id="80be5-347">Rerun the experiment and view the output log.</span></span> <span data-ttu-id="80be5-348">Les résultats attendus sont présentés dans la figure 10.</span><span class="sxs-lookup"><span data-stu-id="80be5-348">The expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="80be5-349">*Figure 10 : aperçu du tableau de données avec le nombre correct de niveaux de facteur.*</span><span class="sxs-lookup"><span data-stu-id="80be5-349">*Figure 10. Summary of the dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="80be5-350">Notre variable facteur possède désormais les 12 niveaux souhaités.</span><span class="sxs-lookup"><span data-stu-id="80be5-350">Our factor variable now has the desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="80be5-351">Filtrage de base des tableaux de données</span><span class="sxs-lookup"><span data-stu-id="80be5-351">Basic data frame filtering</span></span>
<span data-ttu-id="80be5-352">Les tableaux de données R prennent en charge des fonctionnalités de filtrage efficaces.</span><span class="sxs-lookup"><span data-stu-id="80be5-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="80be5-353">Il est possible de créer des sous-ensembles de jeux de données en appliquant des filtres logiques aux lignes ou colonnes.</span><span class="sxs-lookup"><span data-stu-id="80be5-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="80be5-354">Dans de nombreux cas, des critères de filtre complexes sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="80be5-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="80be5-355">Parmi les références indiquées dans l’ [annexe B - informations supplémentaires](#appendixb) figurent des exemples détaillés de filtrage de tableaux de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-355">The references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="80be5-356">Notre jeu de données a besoin d'être filtré.</span><span class="sxs-lookup"><span data-stu-id="80be5-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="80be5-357">En effet, si l’on examine les colonnes du tableau de données cadiarydata, on constate qu’il y a deux colonnes inutiles.</span><span class="sxs-lookup"><span data-stu-id="80be5-357">If you look at the columns in the cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="80be5-358">La première colonne contient seulement un numéro de ligne, ce qui n'est pas très utile.</span><span class="sxs-lookup"><span data-stu-id="80be5-358">The first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="80be5-359">La deuxième colonne, Year.Month, contient des informations redondantes.</span><span class="sxs-lookup"><span data-stu-id="80be5-359">The second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="80be5-360">Nous pouvons facilement exclure ces colonnes à l’aide du code R suivant.</span><span class="sxs-lookup"><span data-stu-id="80be5-360">We can easily exclude these columns by using the following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="80be5-361">À partir de maintenant, dans cette section, je ne vous montrerai que le code supplémentaire que j’ajoute dans le module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-361">From now on in this section, I will just show you the additional code I am adding in the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="80be5-362">Chaque nouvelle ligne sera ajoutée **avant** la fonction `str()`.</span><span class="sxs-lookup"><span data-stu-id="80be5-362">I will add each new line **before** the `str()` function.</span></span> <span data-ttu-id="80be5-363">J’utilise cette fonction pour vérifier les résultats dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-363">I use this function to verify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="80be5-364">J’ajoute la ligne suivante à mon code R dans le module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-364">I add the following line to my R code in the [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="80be5-365">Exécutez ce code dans votre expérimentation et vérifiez le résultat dans le journal de sortie.</span><span class="sxs-lookup"><span data-stu-id="80be5-365">Run this code in your experiment and check the result from the output log.</span></span> <span data-ttu-id="80be5-366">Ces résultats sont présentés dans la figure 11.</span><span class="sxs-lookup"><span data-stu-id="80be5-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="80be5-367">*Figure 11 : aperçu du tableau de données après la suppression des deux colonnes.*</span><span class="sxs-lookup"><span data-stu-id="80be5-367">*Figure 11. Summary of the dataframe with two columns removed.*</span></span>

<span data-ttu-id="80be5-368">Bonne nouvelle !</span><span class="sxs-lookup"><span data-stu-id="80be5-368">Good news!</span></span> <span data-ttu-id="80be5-369">Les résultats obtenus sont conformes aux attentes.</span><span class="sxs-lookup"><span data-stu-id="80be5-369">We get the expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="80be5-370">Ajout d'une nouvelle colonne</span><span class="sxs-lookup"><span data-stu-id="80be5-370">Add a new column</span></span>
<span data-ttu-id="80be5-371">Pour créer des modèles chronologiques, il va nous être utile de disposer d'une colonne contenant les mois depuis le début de la série chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-371">To create time series models it will be convenient to have a column containing the months since the start of the time series.</span></span> <span data-ttu-id="80be5-372">À cet effet, nous allons créer la colonne « Month.Count ».</span><span class="sxs-lookup"><span data-stu-id="80be5-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="80be5-373">Pour une meilleure organisation du code, nous allons créer notre première fonction simple : `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="80be5-373">To help organize the code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="80be5-374">Nous appliquerons ensuite cette fonction de façon à créer une colonne dans le tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-374">We will then apply this function to create a new column in the dataframe.</span></span> <span data-ttu-id="80be5-375">Le nouveau code se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="80be5-375">The new code is as follows.</span></span>

    ## Create a new column with the month count
    ## Function to find the number of months from the first
    ## month of the time series
    num.month <- function(Year, Month) {
      ## Find the starting year
      min.year  <- min(Year)

      ## Compute the number of months from the start of the time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute the new column for the dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="80be5-376">À présent, exécutez l'expérimentation mise à jour et utilisez le journal de sortie pour afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="80be5-376">Now run the updated experiment and use the output log to view the results.</span></span> <span data-ttu-id="80be5-377">Ces résultats sont présentés dans la figure 12.</span><span class="sxs-lookup"><span data-stu-id="80be5-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="80be5-378">*Figure 12 : aperçu du tableau de données avec la colonne supplémentaire.*</span><span class="sxs-lookup"><span data-stu-id="80be5-378">*Figure 12. Summary of the dataframe with the additional column.*</span></span>

<span data-ttu-id="80be5-379">Tout semble fonctionner.</span><span class="sxs-lookup"><span data-stu-id="80be5-379">It looks like everything is working.</span></span> <span data-ttu-id="80be5-380">Nous disposons de la nouvelle colonne et le tableau de données contient les valeurs attendues.</span><span class="sxs-lookup"><span data-stu-id="80be5-380">We have the new column with the expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="80be5-381">Transformations de valeurs</span><span class="sxs-lookup"><span data-stu-id="80be5-381">Value transformations</span></span>
<span data-ttu-id="80be5-382">Dans cette section, nous allons effectuer quelques transformations simples sur les valeurs de certaines colonnes du tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-382">In this section we will perform some simple transformations on the values in some of the columns of our dataframe.</span></span> <span data-ttu-id="80be5-383">Le langage R prend en charge les transformations de valeurs presque arbitraires.</span><span class="sxs-lookup"><span data-stu-id="80be5-383">The R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="80be5-384">Parmi les références indiquées dans l’ [annexe B - informations supplémentaires](#appendixb) figurent des exemples détaillés.</span><span class="sxs-lookup"><span data-stu-id="80be5-384">The references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="80be5-385">Si on examine les valeurs contenues dans les aperçus du tableau de données, on note certaines incohérences.</span><span class="sxs-lookup"><span data-stu-id="80be5-385">If you look at the values in the summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="80be5-386">Par exemple, produit-on vraiment plus de crème glacée que de lait en Californie ?</span><span class="sxs-lookup"><span data-stu-id="80be5-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="80be5-387">Bien sûr que non, au grand dam peut-être des amateurs de glaces.</span><span class="sxs-lookup"><span data-stu-id="80be5-387">No, of course not, as this makes no sense, sad as this fact may be to some of us ice cream lovers.</span></span> <span data-ttu-id="80be5-388">Les unités sont différentes.</span><span class="sxs-lookup"><span data-stu-id="80be5-388">The units are different.</span></span> <span data-ttu-id="80be5-389">Le prix est exprimé en unités de livres américaines, le lait en unités de 1 M de livres américaines, la crème glacée en unités de 1 000 gallons américains et le fromage blanc en unités de 1 000 livres américaines.</span><span class="sxs-lookup"><span data-stu-id="80be5-389">The price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="80be5-390">En supposant que le poids de la crème glacée est d’environ 6,5 livres par gallon, nous pouvons facilement effectuer la conversion en multipliant les valeurs pour qu’elles soient toutes exprimées dans les mêmes unités de 1 000 livres.</span><span class="sxs-lookup"><span data-stu-id="80be5-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do the multiplication to convert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="80be5-391">Pour notre modèle de prévision, nous utilisons un modèle multiplicatif de façon à ajuster ces données en fonction des variations saisonnières et tendancielles.</span><span class="sxs-lookup"><span data-stu-id="80be5-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="80be5-392">Une transformation logarithmique nous permet d'utiliser un modèle linéaire, ce qui simplifie ce processus.</span><span class="sxs-lookup"><span data-stu-id="80be5-392">A log transformation allows us to use a linear model, simplifying this process.</span></span> <span data-ttu-id="80be5-393">Nous pouvons appliquer la transformation logarithmique dans la fonction où le multiplicateur est appliqué.</span><span class="sxs-lookup"><span data-stu-id="80be5-393">We can apply the log transformation in the same function where the multiplier is applied.</span></span>

<span data-ttu-id="80be5-394">Dans le code suivant, je définis une nouvelle fonction, `log.transform()`, et l’applique aux lignes contenant les valeurs numériques.</span><span class="sxs-lookup"><span data-stu-id="80be5-394">In the following code, I define a new function, `log.transform()`, and apply it to the rows containing the numerical values.</span></span> <span data-ttu-id="80be5-395">La fonction R `Map()` est utilisée pour appliquer la fonction `log.transform()` aux colonnes sélectionnées du tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-395">The R `Map()` function is used to apply the `log.transform()` function to the selected columns of the dataframe.</span></span> <span data-ttu-id="80be5-396">Si `Map()` s’apparente à `apply()`, cette fonction accepte cependant plusieurs listes d’arguments.</span><span class="sxs-lookup"><span data-stu-id="80be5-396">`Map()` is similar to `apply()` but allows for more than one list of arguments to the function.</span></span> <span data-ttu-id="80be5-397">À noter qu’une liste de multiplicateurs fournit le deuxième argument à la fonction `log.transform()` .</span><span class="sxs-lookup"><span data-stu-id="80be5-397">Note that a list of multipliers supplies the second argument to the `log.transform()` function.</span></span> <span data-ttu-id="80be5-398">La fonction `na.omit()` est ici utilisée à des fins de nettoyage pour s’assurer qu’il n’y a pas de valeurs manquantes ou non définies dans le tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-398">The `na.omit()` function is used as a bit of cleanup to ensure we do not have missing or undefined values in the dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for the transformation, which is the log
      ## of the input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments to function log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier to funcition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check the input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap the multiplication in tryCatch
      ## If there is an exception, print the warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply the transformation function to the 4 columns
    ## of the dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="80be5-399">Il se passe pas mal de choses dans la fonction `log.transform()` .</span><span class="sxs-lookup"><span data-stu-id="80be5-399">There is quite a bit happening in the `log.transform()` function.</span></span> <span data-ttu-id="80be5-400">La majeure partie de ce code recherche des problèmes potentiels au niveau des arguments ou gère les exceptions qui peuvent toujours survenir pendant les calculs.</span><span class="sxs-lookup"><span data-stu-id="80be5-400">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="80be5-401">En fait, seules quelques lignes de ce code effectuent les calculs.</span><span class="sxs-lookup"><span data-stu-id="80be5-401">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="80be5-402">La programmation défensive vise à éviter l’échec d’une seule fonction, ce qui empêcherait la poursuite du traitement.</span><span class="sxs-lookup"><span data-stu-id="80be5-402">The goal of the defensive programming is to prevent the failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="80be5-403">L’échec soudain d’une analyse au long cours peut s’avérer très contrariant pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="80be5-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="80be5-404">Pour éviter cette situation, il convient de choisir des valeurs de retour par défaut qui limiteront les nuisances à un traitement en aval.</span><span class="sxs-lookup"><span data-stu-id="80be5-404">To avoid this situation, default return values must be chosen that will limit damage to downstream processing.</span></span> <span data-ttu-id="80be5-405">Un message est également généré pour avertir les utilisateurs qu'un problème s'est produit.</span><span class="sxs-lookup"><span data-stu-id="80be5-405">A message is also produced to alert users that something has gone wrong.</span></span>

<span data-ttu-id="80be5-406">Si vous n’êtes pas rompu à la programmation défensive en langage R, tout ce code peut vous paraître insurmontable.</span><span class="sxs-lookup"><span data-stu-id="80be5-406">If you are not used to defensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="80be5-407">Je vous accompagnerai tout au long des étapes principales :</span><span class="sxs-lookup"><span data-stu-id="80be5-407">I will walk you through the major steps:</span></span>

1. <span data-ttu-id="80be5-408">Un vecteur de quatre messages est défini.</span><span class="sxs-lookup"><span data-stu-id="80be5-408">A vector of four messages is defined.</span></span> <span data-ttu-id="80be5-409">Ces messages servent à communiquer des informations sur certaines erreurs et exceptions qui peuvent se produire avec ce code.</span><span class="sxs-lookup"><span data-stu-id="80be5-409">These messages are used to communicate information about some of the possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="80be5-410">Dans chaque cas, la valeur NA est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="80be5-410">I return a value of NA for each case.</span></span> <span data-ttu-id="80be5-411">Il existe de nombreuses autres possibilités susceptibles de produire moins d’effets secondaires.</span><span class="sxs-lookup"><span data-stu-id="80be5-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="80be5-412">Je pourrais renvoyer un vecteur de zéros ou le vecteur d'entrée d'origine, par exemple.</span><span class="sxs-lookup"><span data-stu-id="80be5-412">I could return a vector of zeroes, or the original input vector, for example.</span></span>
3. <span data-ttu-id="80be5-413">Les arguments de la fonction font l'objet de vérifications.</span><span class="sxs-lookup"><span data-stu-id="80be5-413">Checks are run on the arguments to the function.</span></span> <span data-ttu-id="80be5-414">Dans chaque cas, si une erreur est détectée, une valeur par défaut est renvoyée et un message est généré par la fonction `warning()`.</span><span class="sxs-lookup"><span data-stu-id="80be5-414">In each case, if an error is detected, a default value is returned and a message is produced by the `warning()` function.</span></span> <span data-ttu-id="80be5-415">La fonction `warning()` est ici préférée à la fonction `stop()`, car celle-ci met fin à l’exécution, exactement ce que nous voulons éviter.</span><span class="sxs-lookup"><span data-stu-id="80be5-415">I am using `warning()` rather than `stop()` as the latter will terminate execution, exactly what I am trying to avoid.</span></span> <span data-ttu-id="80be5-416">À noter que j'ai écrit ce code dans un style procédural, car dans ce cas, une approche fonctionnelle paraissait complexe et obscure.</span><span class="sxs-lookup"><span data-stu-id="80be5-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="80be5-417">Les calculs logarithmiques sont circonscrits à `tryCatch()` pour éviter que les exceptions n’entraînent un arrêt soudain du traitement.</span><span class="sxs-lookup"><span data-stu-id="80be5-417">The log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt to processing.</span></span> <span data-ttu-id="80be5-418">Sans `tryCatch()` , la plupart des erreurs déclenchées par les fonctions R engendrent un signal d’arrêt, qui est suivi d’un arrêt.</span><span class="sxs-lookup"><span data-stu-id="80be5-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="80be5-419">Exécutez ce code R dans votre expérimentation et examinez la sortie imprimée dans le fichier output.log.</span><span class="sxs-lookup"><span data-stu-id="80be5-419">Execute this R code in your experiment and have a look at the printed output in the output.log file.</span></span> <span data-ttu-id="80be5-420">Les valeurs transformées des quatre colonnes sont visibles apparaissent dans le journal, comme l’illustre la figure 13.</span><span class="sxs-lookup"><span data-stu-id="80be5-420">You will now see the transformed values of the four columns in the log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="80be5-421">*Figure 13 : aperçu des valeurs transformées dans le tableau de données.*</span><span class="sxs-lookup"><span data-stu-id="80be5-421">*Figure 13. Summary of the transformed values in the dataframe.*</span></span>

<span data-ttu-id="80be5-422">Comme nous pouvons le constater, les valeurs ont été transformées.</span><span class="sxs-lookup"><span data-stu-id="80be5-422">We see the values have been transformed.</span></span> <span data-ttu-id="80be5-423">À présent, la production de lait dépasse nettement la production de tous les autres produits laitiers, ce qui nous rappelle que nous avons maintenant sous nos yeux une échelle logarithmique.</span><span class="sxs-lookup"><span data-stu-id="80be5-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="80be5-424">À ce stade, nos données sont nettoyées et nous sommes prêts à procéder à une modélisation.</span><span class="sxs-lookup"><span data-stu-id="80be5-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="80be5-425">Au vu de l’aperçu de visualisation de la sortie du jeu de données de résultat du module [d’exécution de script R][execute-r-script], vous pouvez constater que la colonne « Month » est de type « catégorique » et qu’elle contient 12 valeurs uniques, là encore comme prévu.</span><span class="sxs-lookup"><span data-stu-id="80be5-425">Looking at the visualization summary for the Result Dataset output of our [Execute R Script][execute-r-script] module, you will see the 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="80be5-426"><a id="timeseries"></a>Objets de série chronologique et analyse des corrélations</span><span class="sxs-lookup"><span data-stu-id="80be5-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="80be5-427">Dans cette section, nous allons explorer quelques objets de série chronologique R de base et analyser les corrélations entre certaines variables.</span><span class="sxs-lookup"><span data-stu-id="80be5-427">In this section we will explore a few basic R time series objects and analyze the correlations between some of the variables.</span></span> <span data-ttu-id="80be5-428">Notre objectif est ici de sortir un tableau de données contenant les informations de corrélation par paire à plusieurs décalages.</span><span class="sxs-lookup"><span data-stu-id="80be5-428">Our goal is to output a dataframe containing the pairwise correlation information at several lags.</span></span>

<span data-ttu-id="80be5-429">Le code complet de cette section se trouve dans le fichier zip que vous avez téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="80be5-429">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="80be5-430">Objets de série chronologique en langage R</span><span class="sxs-lookup"><span data-stu-id="80be5-430">Time series objects in R</span></span>
<span data-ttu-id="80be5-431">Comme nous l'avons déjà vu, une série chronologique est une série de valeurs de données indexées par le temps.</span><span class="sxs-lookup"><span data-stu-id="80be5-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="80be5-432">Les objets de série chronologique R servent à créer et gérer l'index chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-432">R time series objects are used to create and manage the time index.</span></span> <span data-ttu-id="80be5-433">Il y a plusieurs avantages à utiliser des objets de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-433">There are several advantages to using time series objects.</span></span> <span data-ttu-id="80be5-434">Les objets de série chronologique vous affranchissent de nombreuses tâches de gestion qu’imposent les valeurs d’index chronologique qui sont encapsulées dans les objets.</span><span class="sxs-lookup"><span data-stu-id="80be5-434">Time series objects free you from the many details of managing the time series index values that are encapsulated in the object.</span></span> <span data-ttu-id="80be5-435">De plus, ils vous permettent d'utiliser les diverses méthodes associées aux séries chronologiques, comme le traçage, l'impression, la modélisation, etc.</span><span class="sxs-lookup"><span data-stu-id="80be5-435">In addition, time series objects allow you to use the many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="80be5-436">La classe de série chronologique POSIXct est couramment utilisée et relativement simple.</span><span class="sxs-lookup"><span data-stu-id="80be5-436">The POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="80be5-437">Cette classe de série chronologique mesure le temps à partir du début de l'époque, soit le 1er janvier 1970.</span><span class="sxs-lookup"><span data-stu-id="80be5-437">This time series class measures time from the start of the epoch, January 1, 1970.</span></span> <span data-ttu-id="80be5-438">Nous utiliserons dans cet exemple des objets de série chronologique POSIXct.</span><span class="sxs-lookup"><span data-stu-id="80be5-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="80be5-439">Parmi les autres classes d'objet de série chronologique R souvent utilisées, citons zoo et xts, qui concernent les séries chronologiques extensibles.</span><span class="sxs-lookup"><span data-stu-id="80be5-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in the references in Section 5.7. [commenting because this section doesn't exist, even in the original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="80be5-440">Exemple d’objet de série chronologique</span><span class="sxs-lookup"><span data-stu-id="80be5-440">Time series object example</span></span>
<span data-ttu-id="80be5-441">Commençons notre exemple.</span><span class="sxs-lookup"><span data-stu-id="80be5-441">Let's get started with our example.</span></span> <span data-ttu-id="80be5-442">Glissez-déplacez un **nouveau** module [d’exécution de script R][execute-r-script] dans votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="80be5-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="80be5-443">Reliez le port de sortie du jeu de données 1 de résultat du module [d’exécution de script R][execute-r-script] existant au port d’entrée du jeu de données 1 du nouveau module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-443">Connect the Result Dataset1 output port of the existing [Execute R Script][execute-r-script] module to the Dataset1 input port of the new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="80be5-444">Comme dans les premiers exemples, à mesure que nous avancerons dans l’exemple, je ne vous montrerai que les lignes de code R supplémentaires ajoutées à certains points de chaque étape.</span><span class="sxs-lookup"><span data-stu-id="80be5-444">As I did for the first examples, as we progress through the example, at some points I will show only the incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-the-dataframe"></a><span data-ttu-id="80be5-445">Lecture du tableau de données</span><span class="sxs-lookup"><span data-stu-id="80be5-445">Reading the dataframe</span></span>
<span data-ttu-id="80be5-446">Pour commencer, lisons un tableau de données et vérifions que nous obtenons les résultats attendus.</span><span class="sxs-lookup"><span data-stu-id="80be5-446">As a first step, let's read in a dataframe and make sure we get the expected results.</span></span> <span data-ttu-id="80be5-447">Le code suivant devrait le permettre :</span><span class="sxs-lookup"><span data-stu-id="80be5-447">The following code should do the job.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check the results

<span data-ttu-id="80be5-448">À présent, exécutez l'expérimentation.</span><span class="sxs-lookup"><span data-stu-id="80be5-448">Now, run the experiment.</span></span> <span data-ttu-id="80be5-449">Le journal de la nouvelle forme d'exécution du script R devrait ressembler à la figure 14.</span><span class="sxs-lookup"><span data-stu-id="80be5-449">The log of the new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="80be5-450">*Figure 14 : aperçu du tableau de données dans le module d’exécution de script R.*</span><span class="sxs-lookup"><span data-stu-id="80be5-450">*Figure 14. Summary of the dataframe in the Execute R Script module.*</span></span>

<span data-ttu-id="80be5-451">Ces données présentent le type et le format prévus.</span><span class="sxs-lookup"><span data-stu-id="80be5-451">This data is of the expected types and format.</span></span> <span data-ttu-id="80be5-452">Notez que la colonne « Month » est de type facteur et qu'elle affiche le nombre de niveaux attendu.</span><span class="sxs-lookup"><span data-stu-id="80be5-452">Note that the 'Month' column is of type factor and has the expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="80be5-453">Création d’un objet de série chronologique</span><span class="sxs-lookup"><span data-stu-id="80be5-453">Creating a time series object</span></span>
<span data-ttu-id="80be5-454">Nous devons ajouter un objet de série chronologique au tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-454">We need to add a time series object to our dataframe.</span></span> <span data-ttu-id="80be5-455">Remplacez le code actuel par le suivant, qui ajoute une nouvelle colonne de classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="80be5-455">Replace the current code with the following, which adds a new column of class POSIXct.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check the results

<span data-ttu-id="80be5-456">Maintenant, consultez le journal.</span><span class="sxs-lookup"><span data-stu-id="80be5-456">Now, check the log.</span></span> <span data-ttu-id="80be5-457">Elle doit être similaire à la figure 15.</span><span class="sxs-lookup"><span data-stu-id="80be5-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="80be5-458">*Figure 15 : aperçu du tableau de données avec un objet de série chronologique.*</span><span class="sxs-lookup"><span data-stu-id="80be5-458">*Figure 15. Summary of the dataframe with a time series object.*</span></span>

<span data-ttu-id="80be5-459">Comme le montre l'aperçu, la nouvelle colonne appartient en réalité à la classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="80be5-459">We can see from the summary that the new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-the-data"></a><span data-ttu-id="80be5-460">Exploration et transformation des données</span><span class="sxs-lookup"><span data-stu-id="80be5-460">Exploring and transforming the data</span></span>
<span data-ttu-id="80be5-461">Examinons certaines variables de ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-461">Let's explore some of the variables in this dataset.</span></span> <span data-ttu-id="80be5-462">Une matrice de nuage de points offre un bon moyen d'obtenir un aperçu rapide.</span><span class="sxs-lookup"><span data-stu-id="80be5-462">A scatterplot matrix is a good way to produce a quick look.</span></span> <span data-ttu-id="80be5-463">Je remplace la fonction `str()` du code R précédent par la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="80be5-463">I am replacing the `str()` function in the previous R code with the following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="80be5-464">Exécutez ce code et regardez ce qu'il se passe.</span><span class="sxs-lookup"><span data-stu-id="80be5-464">Run this code and see what happens.</span></span> <span data-ttu-id="80be5-465">Le graphique généré au niveau du port de l’appareil R doit être similaire à la figure 16.</span><span class="sxs-lookup"><span data-stu-id="80be5-465">The plot produced at the R Device port should look like Figure 16.</span></span>

![matrice de nuage de points des variables sélectionnées][17]

<span data-ttu-id="80be5-467">*Figure 16 : matrice de nuage de points des variables sélectionnées.*</span><span class="sxs-lookup"><span data-stu-id="80be5-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="80be5-468">Les relations entre ces variables sont structurées de manière inhabituelle.</span><span class="sxs-lookup"><span data-stu-id="80be5-468">There is some odd-looking structure in the relationships between these variables.</span></span> <span data-ttu-id="80be5-469">Peut-être est-ce lié aux tendances des données et au fait que nous n'avons pas standardisé les variables.</span><span class="sxs-lookup"><span data-stu-id="80be5-469">Perhaps this arises from trends in the data and from the fact that we have not standardized the variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="80be5-470">Analyse des corrélations</span><span class="sxs-lookup"><span data-stu-id="80be5-470">Correlation analysis</span></span>
<span data-ttu-id="80be5-471">Pour procéder à l'analyse des corrélations, nous devons éliminer la tendance et standardiser les variables.</span><span class="sxs-lookup"><span data-stu-id="80be5-471">To perform correlation analysis we need to both de-trend and standardize the variables.</span></span> <span data-ttu-id="80be5-472">Nous aurions pu nous contenter d’utiliser la fonction R `scale()` , qui centre et dimensionne les variables.</span><span class="sxs-lookup"><span data-stu-id="80be5-472">We could simply use the R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="80be5-473">D'autant que son exécution peut même s'avérer plus rapide.</span><span class="sxs-lookup"><span data-stu-id="80be5-473">This function might well run faster.</span></span> <span data-ttu-id="80be5-474">Or, mon intention est de vous montrer un exemple de programmation défensive en langage R.</span><span class="sxs-lookup"><span data-stu-id="80be5-474">However, I want to show you an example of defensive programing in R.</span></span>

<span data-ttu-id="80be5-475">La fonction `ts.detrend()` présentée ci-dessous effectue ces deux opérations.</span><span class="sxs-lookup"><span data-stu-id="80be5-475">The `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="80be5-476">Les deux lignes de code suivantes permettent d'éliminer la tendance des données et de standardiser les valeurs.</span><span class="sxs-lookup"><span data-stu-id="80be5-476">The following two lines of code de-trend the data and then standardize the values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function to de-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time to have the same length',
                    'ERROR: ts.detrend requires argument ts to be of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros to return as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # The input arguments are not of the same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If the ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If the ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that the Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend the time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply the detrend.ts function to the variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot the results to look at the relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="80be5-477">Il se passe pas mal de choses dans la fonction `ts.detrend()` .</span><span class="sxs-lookup"><span data-stu-id="80be5-477">There is quite a bit happening in the `ts.detrend()` function.</span></span> <span data-ttu-id="80be5-478">La majeure partie de ce code recherche des problèmes potentiels au niveau des arguments ou gère les exceptions qui peuvent toujours survenir pendant les calculs.</span><span class="sxs-lookup"><span data-stu-id="80be5-478">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="80be5-479">En fait, seules quelques lignes de ce code effectuent les calculs.</span><span class="sxs-lookup"><span data-stu-id="80be5-479">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="80be5-480">Nous avons déjà vu un exemple de programmation défensive dans la section [Transformations de valeurs](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="80be5-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="80be5-481">Les deux blocs de calcul sont circonscrits à `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="80be5-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="80be5-482">Pour certaines erreurs, il est judicieux de renvoyer le vecteur d'entrée d'origine. Dans d'autres cas, je renvoie un vecteur de zéros.</span><span class="sxs-lookup"><span data-stu-id="80be5-482">For some errors it makes sense to return the original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="80be5-483">Notez que la régression linéaire utilisée pour éliminer la tendance est une régression chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-483">Note that the linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="80be5-484">La variable explicative est un objet de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-484">The predictor variable is a time series object.</span></span>  

<span data-ttu-id="80be5-485">Une fois que la fonction `ts.detrend()` est définie, nous l’appliquons aux variables appropriées du tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-485">Once `ts.detrend()` is defined we apply it to the variables of interest in our dataframe.</span></span> <span data-ttu-id="80be5-486">Nous devons convertir de force la liste obtenue créée par `lapply()` en tableau de données à l’aide de `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="80be5-486">We must coerce the resulting list created by `lapply()` to data dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="80be5-487">Compte tenu des aspects défensifs de `ts.detrend()`, l’échec du traitement de l’une des variables n’empêchera pas le traitement correct des autres.</span><span class="sxs-lookup"><span data-stu-id="80be5-487">Because of defensive aspects of `ts.detrend()`, failure to process one of the variables will not prevent correct processing of the others.</span></span>  

<span data-ttu-id="80be5-488">La dernière ligne de code crée un nuage de points par paire.</span><span class="sxs-lookup"><span data-stu-id="80be5-488">The final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="80be5-489">Les résultats du nuage de points obtenu après l’exécution du code R sont illustrés dans la figure 17.</span><span class="sxs-lookup"><span data-stu-id="80be5-489">After running the R code, the results of the scatterplot are shown in Figure 17.</span></span>

![nuage de points par paire de la série chronologique après élimination de la tendance et standardisation][18]

<span data-ttu-id="80be5-491">*Figure 17 : nuage de points par paire de la série chronologique après élimination de la tendance et standardisation.*</span><span class="sxs-lookup"><span data-stu-id="80be5-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="80be5-492">Vous pouvez comparer ces résultats à ceux présentés à la figure 16.</span><span class="sxs-lookup"><span data-stu-id="80be5-492">You can compare these results to those shown in Figure 16.</span></span> <span data-ttu-id="80be5-493">L'élimination de la tendance et la standardisation des variables ont nettement déstructuré les relations entre ces variables.</span><span class="sxs-lookup"><span data-stu-id="80be5-493">With the trend removed and the variables standardized, we see a lot less structure in the relationships between these variables.</span></span>

<span data-ttu-id="80be5-494">Le code permettant de calculer les corrélations en tant qu’objets ccf R est le suivant :</span><span class="sxs-lookup"><span data-stu-id="80be5-494">The code to compute the correlations as R ccf objects is as follows.</span></span>

    ## A function to compute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of the pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute the list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="80be5-495">L'exécution de ce code génère le journal présenté dans la figure 18.</span><span class="sxs-lookup"><span data-stu-id="80be5-495">Running this code produces the log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="80be5-496">*Figure 18 : liste des objets ccf résultant de l’analyse des corrélations par paire.*</span><span class="sxs-lookup"><span data-stu-id="80be5-496">*Figure 18. List of ccf objects from the pairwise correlation analysis.*</span></span>

<span data-ttu-id="80be5-497">À chaque décalage correspond une valeur de corrélation.</span><span class="sxs-lookup"><span data-stu-id="80be5-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="80be5-498">Aucune de ces valeurs de corrélation n'est suffisamment grande pour être significative.</span><span class="sxs-lookup"><span data-stu-id="80be5-498">None of these correlation values is large enough to be significant.</span></span> <span data-ttu-id="80be5-499">Nous pouvons donc en conclure qu'il est possible de modéliser chaque variable de façon indépendante.</span><span class="sxs-lookup"><span data-stu-id="80be5-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="80be5-500">Sortie d'un tableau de données</span><span class="sxs-lookup"><span data-stu-id="80be5-500">Output a dataframe</span></span>
<span data-ttu-id="80be5-501">Nous avons calculé les corrélations par paire en tant que liste d'objets ccf R.</span><span class="sxs-lookup"><span data-stu-id="80be5-501">We have computed the pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="80be5-502">Cela pose un léger problème dans le sens où le port de sortie du jeu de données de résultat a vraiment besoin d'un tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-502">This presents a bit of a problem as the Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="80be5-503">En outre, l’objet ccf est lui-même une liste et nous voulons uniquement les valeurs contenues dans le premier élément de cette liste, c’est-à-dire les corrélations aux différents décalages.</span><span class="sxs-lookup"><span data-stu-id="80be5-503">Further, the ccf object is itself a list and we want only the values in the first element of this list, the correlations at the various lags.</span></span>

<span data-ttu-id="80be5-504">Le code suivant permet d’extraire les valeurs de décalage de la liste d’objets ccf, qui sont eux-mêmes des listes :</span><span class="sxs-lookup"><span data-stu-id="80be5-504">The following code extracts the lag values from the list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with the row names column and the
    ## correlation data frame and assign the column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## The following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="80be5-505">La première ligne de code est un peu compliquée et vous pourriez avoir besoin d’une explication vous aider à la comprendre.</span><span class="sxs-lookup"><span data-stu-id="80be5-505">The first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="80be5-506">Voici ce que l'on a :</span><span class="sxs-lookup"><span data-stu-id="80be5-506">Working from the inside out we have the following:</span></span>

1. <span data-ttu-id="80be5-507">L’opérateur « **[[** » associé à l’argument « **1** » sélectionne le vecteur de corrélations au niveau des décalages dans le premier élément de la liste d’objets ccf.</span><span class="sxs-lookup"><span data-stu-id="80be5-507">The '**[[**' operator with the argument '**1**' selects the vector of correlations at the lags from the first element of the ccf object list.</span></span>
2. <span data-ttu-id="80be5-508">La fonction `do.call()` applique la fonction `rbind()` aux éléments de la liste renvoyée par `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="80be5-508">The `do.call()` function applies the `rbind()` function over the elements of the list returns by `lapply()`.</span></span>
3. <span data-ttu-id="80be5-509">La fonction `data.frame()` convertit de force le résultat généré par `do.call()` en tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-509">The `data.frame()` function coerces the result produced by `do.call()` to a dataframe.</span></span>

<span data-ttu-id="80be5-510">Notez que les noms de lignes se trouvent dans une colonne du tableau de données.</span><span class="sxs-lookup"><span data-stu-id="80be5-510">Note that the row names are in a column of the dataframe.</span></span> <span data-ttu-id="80be5-511">Cela préserve les noms de lignes quand ils sont générés à partir du module [d’exécution de script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80be5-511">Doing so preserves the row names when they are output from the [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="80be5-512">L’exécution du code génère la sortie présentée dans la figure 19 après avoir actionné la commande **Visualize** (Visualiser) au niveau du port du jeu de données de résultat.</span><span class="sxs-lookup"><span data-stu-id="80be5-512">Running the code produces the output shown in Figure 19 when I **Visualize** the output at the Result Dataset port.</span></span> <span data-ttu-id="80be5-513">Les noms de lignes se trouvent dans la première colonne, comme prévu.</span><span class="sxs-lookup"><span data-stu-id="80be5-513">The row names are in the first column, as intended.</span></span>

![résultats générés par l’analyse des corrélations][20]

<span data-ttu-id="80be5-515">*Figure 19 : résultats générés par l’analyse des corrélations.*</span><span class="sxs-lookup"><span data-stu-id="80be5-515">*Figure 19. Results output from the correlation analysis.*</span></span>

## <span data-ttu-id="80be5-516"><a id="seasonalforecasting"></a>Exemple de série chronologique : prévision saisonnière</span><span class="sxs-lookup"><span data-stu-id="80be5-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="80be5-517">Les données se trouvent maintenant dans un format adapté à l’analyse et nous avons déterminé qu’il n’y avait pas de corrélations significatives entre les variables.</span><span class="sxs-lookup"><span data-stu-id="80be5-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between the variables.</span></span> <span data-ttu-id="80be5-518">Continuons et créons un modèle de prévision chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="80be5-519">Nous nous servirons de ce modèle pour établir des prévisions concernant la production de lait californienne au cours des 12 mois de 2013.</span><span class="sxs-lookup"><span data-stu-id="80be5-519">Using this model we will forecast California milk production for the 12 months of 2013.</span></span>

<span data-ttu-id="80be5-520">Notre modèle de prévision aura deux composantes : une tendancielle et une saisonnière.</span><span class="sxs-lookup"><span data-stu-id="80be5-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="80be5-521">La prévision complète est le fruit de ces deux composantes.</span><span class="sxs-lookup"><span data-stu-id="80be5-521">The complete forecast is the product of these two components.</span></span> <span data-ttu-id="80be5-522">Ce type de modèle est connu sous le nom de modèle multiplicatif.</span><span class="sxs-lookup"><span data-stu-id="80be5-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="80be5-523">Le modèle alternatif est appelé modèle additif.</span><span class="sxs-lookup"><span data-stu-id="80be5-523">The alternative is an additive model.</span></span> <span data-ttu-id="80be5-524">Nous avons déjà appliqué une transformation logarithmique aux variables qui nous intéressent, ce qui rend cette analyse malléable.</span><span class="sxs-lookup"><span data-stu-id="80be5-524">We have already applied a log transformation to the variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="80be5-525">Le code complet de cette section se trouve dans le fichier zip que vous avez téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="80be5-525">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="creating-the-dataframe-for-analysis"></a><span data-ttu-id="80be5-526">Création du tableau de données pour l’analyse</span><span class="sxs-lookup"><span data-stu-id="80be5-526">Creating the dataframe for analysis</span></span>
<span data-ttu-id="80be5-527">Commencez par ajouter un **nouveau** module [d’exécution de script R][execute-r-script] à votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="80be5-527">Start by adding a **new** [Execute R Script][execute-r-script] module to your experiment.</span></span> <span data-ttu-id="80be5-528">Reliez la sortie de **jeu de données de résultat** du module [d’exécution de script R][execute-r-script] existant à l’entrée **Jeu de données 1** du nouveau module.</span><span class="sxs-lookup"><span data-stu-id="80be5-528">Connect the **Result Dataset** output of the existing [Execute R Script][execute-r-script] module to the **Dataset1** input of the new module.</span></span> <span data-ttu-id="80be5-529">Le résultat doit être similaire à la figure 20.</span><span class="sxs-lookup"><span data-stu-id="80be5-529">The result should look something like Figure 20.</span></span>

![l’expérimentation après l’ajout du nouveau module d’exécution de script R][21]

<span data-ttu-id="80be5-531">*Figure 20 : l’expérimentation après l’ajout du nouveau module d’exécution de script R.*</span><span class="sxs-lookup"><span data-stu-id="80be5-531">*Figure 20. The experiment with the new Execute R Script module added.*</span></span>

<span data-ttu-id="80be5-532">Comme pour l'analyse des corrélations que nous venons d'effectuer, nous devons ajouter une colonne avec un objet de série chronologique POSIXct.</span><span class="sxs-lookup"><span data-stu-id="80be5-532">As with the correlation analysis we just completed, we need to add a column with a POSIXct time series object.</span></span> <span data-ttu-id="80be5-533">C’est exactement ce que fait le code suivant :</span><span class="sxs-lookup"><span data-stu-id="80be5-533">The following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment the first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="80be5-534">Exécutez ce code et consultez le journal.</span><span class="sxs-lookup"><span data-stu-id="80be5-534">Run this code and look at the log.</span></span> <span data-ttu-id="80be5-535">Le résultat doit être similaire à la figure 21.</span><span class="sxs-lookup"><span data-stu-id="80be5-535">The result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="80be5-536">*Figure 21 : aperçu du tableau de données.*</span><span class="sxs-lookup"><span data-stu-id="80be5-536">*Figure 21. A summary of the dataframe.*</span></span>

<span data-ttu-id="80be5-537">Avec ce résultat, nous sommes en mesure de lancer l'analyse.</span><span class="sxs-lookup"><span data-stu-id="80be5-537">With this result, we are ready to start our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="80be5-538">Création d’un jeu de données d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="80be5-538">Create a training dataset</span></span>
<span data-ttu-id="80be5-539">Après avoir construit le tableau de données, nous devons maintenant créer un jeu de données d'apprentissage.</span><span class="sxs-lookup"><span data-stu-id="80be5-539">With the dataframe constructed we need to create a training dataset.</span></span> <span data-ttu-id="80be5-540">Ces données engloberont toutes les observations à l'exception des 12 dernières de l'année 2013, ce qui correspond à notre jeu de données de test.</span><span class="sxs-lookup"><span data-stu-id="80be5-540">This data will include all of the observations except the last 12, of the year 2013, which is our test dataset.</span></span> <span data-ttu-id="80be5-541">Le code suivant scinde le tableau de données en sous-ensembles et crée des graphiques des variables de production et de prix des produits laitiers.</span><span class="sxs-lookup"><span data-stu-id="80be5-541">The following code subsets the dataframe and creates plots of the dairy production and price variables.</span></span> <span data-ttu-id="80be5-542">Je crée ensuite des graphiques des quatre variables de production et de prix.</span><span class="sxs-lookup"><span data-stu-id="80be5-542">I then create plots of the four production and price variables.</span></span> <span data-ttu-id="80be5-543">Une fonction anonyme est utilisée pour définir des arguments pour le graphique, puis pour itérer sur la liste des deux autres arguments à l’aide de `Map()`.</span><span class="sxs-lookup"><span data-stu-id="80be5-543">An anonymous function is used to define some augments for plot, and then iterate over the list of the other two arguments with `Map()`.</span></span> <span data-ttu-id="80be5-544">Vous vous dites peut-être qu'une boucle for aurait ici fait l'affaire.</span><span class="sxs-lookup"><span data-stu-id="80be5-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="80be5-545">Vous avez raison, mais comme le langage R est un langage fonctionnel, je vous montre une approche fonctionnelle.</span><span class="sxs-lookup"><span data-stu-id="80be5-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="80be5-546">L'exécution du code génère la série de graphiques chronologiques à partir de la sortie de l’appareil R présentée dans la figure 22.</span><span class="sxs-lookup"><span data-stu-id="80be5-546">Running the code produces the series of time series plots from the R Device output shown in Figure 22.</span></span> <span data-ttu-id="80be5-547">Notez que l'axe du temps est exprimé en unités de dates, avantage appréciable de la méthode de graphique chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-547">Note that the time axis is in units of dates, a nice benefit of the time series plot method.</span></span>

![premier graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![deuxième graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![troisième graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![quatrième graphique chronologique des données de production et de prix des produits laitiers californiens](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="80be5-552">*Figure 22 : graphiques chronologiques des données de production et de prix des produits laitiers californiens.*</span><span class="sxs-lookup"><span data-stu-id="80be5-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="80be5-553">Modèle de tendance</span><span class="sxs-lookup"><span data-stu-id="80be5-553">A trend model</span></span>
<span data-ttu-id="80be5-554">Après avoir créé un objet de série chronologique et examiné les données, lançons-nous dans l'élaboration d'un modèle de tendance pour les données de production de produits laitiers californiens.</span><span class="sxs-lookup"><span data-stu-id="80be5-554">Having created a time series object and having had a look at the data, let's start to construct a trend model for the California milk production data.</span></span> <span data-ttu-id="80be5-555">Pour cela, nous pouvons utiliser une régression chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-555">We can do this with a time series regression.</span></span> <span data-ttu-id="80be5-556">Toutefois, il apparaît évident au vu du graphique que nous aurons besoin de plusieurs pentes et intercepts pour modéliser avec précision la tendance observée dans les données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="80be5-556">However, it is clear from the plot that we will need more than a slope and intercept to accurately model the observed trend in the training data.</span></span>

<span data-ttu-id="80be5-557">Compte tenu de la petite échelle des données, je vais générer le modèle de tendance dans RStudio, puis couper et coller le modèle obtenu dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="80be5-557">Given the small scale of the data, I will build the model for trend in RStudio and then cut and paste the resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="80be5-558">RStudio offre un environnement interactif pour ce type d'analyse interactive.</span><span class="sxs-lookup"><span data-stu-id="80be5-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="80be5-559">Dans un premier temps, je vais tenter une régression polynomiale avec des puissances maximales de 3.</span><span class="sxs-lookup"><span data-stu-id="80be5-559">As a first attempt, I will try a polynomial regression with powers up to 3.</span></span> <span data-ttu-id="80be5-560">Il existe un risque réel de surapprentissage de ces types de modèles.</span><span class="sxs-lookup"><span data-stu-id="80be5-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="80be5-561">Par conséquent, il est préférable d'éviter les termes d'ordre élevé.</span><span class="sxs-lookup"><span data-stu-id="80be5-561">Therefore, it is best to avoid high order terms.</span></span> <span data-ttu-id="80be5-562">La fonction `I()` empêche l’interprétation des contenus (elle les interprète « tels quels ») et vous permet d’écrire une fonction interprétée littéralement dans une équation de régression.</span><span class="sxs-lookup"><span data-stu-id="80be5-562">The `I()` function inhibits interpretation of the contents (interprets the contents 'as is') and allows you to write a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="80be5-563">Voici ce que cela génère :</span><span class="sxs-lookup"><span data-stu-id="80be5-563">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="80be5-564">Si l'on considère les valeurs P (Pr(>|t|)) de cette sortie, nous pouvons constater que le terme au carré n'est peut-être pas significatif.</span><span class="sxs-lookup"><span data-stu-id="80be5-564">From P values (Pr(>|t|)) in this output, we can see that the squared term may not be significant.</span></span> <span data-ttu-id="80be5-565">Je vais utiliser la fonction `update()` pour modifier ce modèle en éliminant le terme au carré.</span><span class="sxs-lookup"><span data-stu-id="80be5-565">I will use the `update()` function to modify this model by dropping the squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="80be5-566">Voici ce que cela génère :</span><span class="sxs-lookup"><span data-stu-id="80be5-566">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="80be5-567">Cela semble mieux.</span><span class="sxs-lookup"><span data-stu-id="80be5-567">This looks better.</span></span> <span data-ttu-id="80be5-568">Tous les termes sont significatifs.</span><span class="sxs-lookup"><span data-stu-id="80be5-568">All of the terms are significant.</span></span> <span data-ttu-id="80be5-569">Cependant, la valeur 2e-16 est une valeur par défaut à laquelle il ne faut pas trop prêter attention.</span><span class="sxs-lookup"><span data-stu-id="80be5-569">However, the 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="80be5-570">En guise de test, créons un graphique chronologique à partir des données de production de produits laitiers californiens en affichant la courbe de tendance.</span><span class="sxs-lookup"><span data-stu-id="80be5-570">As a sanity test, let's make a time series plot of the California dairy production data with the trend curve shown.</span></span> <span data-ttu-id="80be5-571">J’ai ajouté le code suivant dans le module [d’exécution de script R][execute-r-script] Azure Machine Learning (pas RStudio) pour créer le modèle et tracer un graphique.</span><span class="sxs-lookup"><span data-stu-id="80be5-571">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) to create the model and make a plot.</span></span> <span data-ttu-id="80be5-572">Ce schéma est illustré dans la Figure 23.</span><span class="sxs-lookup"><span data-stu-id="80be5-572">The result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![données de production laitière californienne avec affichage du modèle de tendance](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="80be5-574">*Figure 23 : données de production laitière californienne avec affichage du modèle de tendance.*</span><span class="sxs-lookup"><span data-stu-id="80be5-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="80be5-575">Il apparaît que le modèle de tendance est assez bien adapté aux données.</span><span class="sxs-lookup"><span data-stu-id="80be5-575">It looks like the trend model fits the data fairly well.</span></span> <span data-ttu-id="80be5-576">En outre, il n'y a visiblement pas de surapprentissage avec, par exemple, des fluctuations incongrues dans la courbe du modèle.</span><span class="sxs-lookup"><span data-stu-id="80be5-576">Further, there does not seem to be evidence of over-fitting, such as odd wiggles in the model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="80be5-577">Modèle saisonnier</span><span class="sxs-lookup"><span data-stu-id="80be5-577">Seasonal model</span></span>
<span data-ttu-id="80be5-578">Maintenant que nous disposons d’un modèle de tendance, nous devons passer à l’étape supérieure et inclure les effets saisonniers.</span><span class="sxs-lookup"><span data-stu-id="80be5-578">With a trend model in hand, we need to push on and include the seasonal effects.</span></span> <span data-ttu-id="80be5-579">Nous allons utiliser le mois de l’année comme variable factice dans le modèle linéaire pour capturer l’effet mois par mois.</span><span class="sxs-lookup"><span data-stu-id="80be5-579">We will use the month of the year as a dummy variable in the linear model to capture the month-by-month effect.</span></span> <span data-ttu-id="80be5-580">Notez que lorsque des variables facteur sont introduites dans un modèle, l'intercept ne doit pas être calculé.</span><span class="sxs-lookup"><span data-stu-id="80be5-580">Note that when you introduce factor variables into a model, the intercept must not be computed.</span></span> <span data-ttu-id="80be5-581">Dans le cas contraire, la formule est surspécifiée et le code R supprime l'un des facteurs souhaités, mais conserve le terme intercept.</span><span class="sxs-lookup"><span data-stu-id="80be5-581">If you do not do this, the formula is over-specified and R will drop one of the desired factors but keep the intercept term.</span></span>

<span data-ttu-id="80be5-582">Comme notre modèle de tendance est satisfaisant, nous pouvons utiliser la fonction `update()` pour ajouter les nouveaux termes au modèle existant.</span><span class="sxs-lookup"><span data-stu-id="80be5-582">Since we have a satisfactory trend model we can use the `update()` function to add the new terms to the existing model.</span></span> <span data-ttu-id="80be5-583">La valeur -1 dans la formule de mise à jour supprime le terme intercept.</span><span class="sxs-lookup"><span data-stu-id="80be5-583">The -1 in the update formula drops the intercept term.</span></span> <span data-ttu-id="80be5-584">Poursuivons dans RStudio pour le moment :</span><span class="sxs-lookup"><span data-stu-id="80be5-584">Continuing in RStudio for the moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="80be5-585">Voici ce que cela génère :</span><span class="sxs-lookup"><span data-stu-id="80be5-585">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="80be5-586">Nous constatons que le modèle n'a plus de terme intercept et qu'il comporte 12 facteurs mois significatifs.</span><span class="sxs-lookup"><span data-stu-id="80be5-586">We see that the model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="80be5-587">C'est exactement ce que nous voulions.</span><span class="sxs-lookup"><span data-stu-id="80be5-587">This is exactly what we wanted to see.</span></span>

<span data-ttu-id="80be5-588">Créons un autre graphique chronologique à partir des données de production laitière californienne pour voir si le modèle saisonnier fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="80be5-588">Let's make another time series plot of the California dairy production data to see how well the seasonal model is working.</span></span> <span data-ttu-id="80be5-589">J’ai ajouté le code suivant dans le module [d’exécution de script R][execute-r-script] Azure Machine Learning pour créer le modèle et tracer un graphique.</span><span class="sxs-lookup"><span data-stu-id="80be5-589">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] to create the model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="80be5-590">L’exécution de ce code dans Azure Machine Learning génère le graphique présenté dans la figure 24.</span><span class="sxs-lookup"><span data-stu-id="80be5-590">Running this code in Azure Machine Learning produces the plot shown in Figure 24.</span></span>

![production laitière californienne avec le modèle incluant les effets saisonniers](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="80be5-592">*Figure 24 : production laitière californienne avec le modèle incluant les effets saisonniers.*</span><span class="sxs-lookup"><span data-stu-id="80be5-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="80be5-593">L'adéquation par rapport aux données présentées dans la figure 24 est plutôt encourageante.</span><span class="sxs-lookup"><span data-stu-id="80be5-593">The fit to the data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="80be5-594">Les effets tendanciel et saisonnier (variation mensuelle) semblent raisonnables.</span><span class="sxs-lookup"><span data-stu-id="80be5-594">Both the trend and the seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="80be5-595">Intéressons-nous à présent aux résidus, autre point de vérification de notre modèle.</span><span class="sxs-lookup"><span data-stu-id="80be5-595">As another check on our model, let's have a look at the residuals.</span></span> <span data-ttu-id="80be5-596">Le code suivant calcule les valeurs prévisionnelles de nos deux modèles, calcule les résidus du modèle saisonnier et élabore ensuite le graphique de ces résidus pour les données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="80be5-596">The following code computes the predicted values from our two models, computes the residuals for the seasonal model, and then plots these residuals for the training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot the residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="80be5-597">Le graphique des résidus est illustré dans la figure 25.</span><span class="sxs-lookup"><span data-stu-id="80be5-597">The residual plot is shown in Figure 25.</span></span>

![résidus du modèle saisonnier pour les données d’apprentissage](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="80be5-599">*Figure 25 : résidus du modèle saisonnier pour les données d’apprentissage.*</span><span class="sxs-lookup"><span data-stu-id="80be5-599">*Figure 25. Residuals of the seasonal model for the training data.*</span></span>

<span data-ttu-id="80be5-600">Ces résidus semblent corrects.</span><span class="sxs-lookup"><span data-stu-id="80be5-600">These residuals look reasonable.</span></span> <span data-ttu-id="80be5-601">Il n'y a pas de structure particulière si l'on excepte l'effet de la récession de 2008-2009, dont notre modèle ne rend pas très bien compte.</span><span class="sxs-lookup"><span data-stu-id="80be5-601">There is no particular structure, except the effect of the 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="80be5-602">Le graphique représenté dans la figure 25 s’avère utile pour détecter les phénomènes temporels dans les résidus.</span><span class="sxs-lookup"><span data-stu-id="80be5-602">The plot shown in Figure 25 is useful for detecting any time-dependent patterns in the residuals.</span></span> <span data-ttu-id="80be5-603">L'approche explicite du calcul et de la représentation des résidus que j'ai utilisée place les résidus dans un ordre chronologique sur le graphique.</span><span class="sxs-lookup"><span data-stu-id="80be5-603">The explicit approach of computing and plotting the residuals I used places the residuals in time order on the plot.</span></span> <span data-ttu-id="80be5-604">Si, en revanche, j’avais représenté `milk.lm$residuals`sur le graphique, celui-ci n’aurait pas été établi dans un ordre chronologique.</span><span class="sxs-lookup"><span data-stu-id="80be5-604">If, on the other hand, I had plotted `milk.lm$residuals`, the plot would not have been in time order.</span></span>

<span data-ttu-id="80be5-605">Vous pouvez aussi utiliser `plot.lm()` pour générer une série de graphiques de diagnostic :</span><span class="sxs-lookup"><span data-stu-id="80be5-605">You can also use `plot.lm()` to produce a series of diagnostic plots.</span></span>

    ## Show the diagnostic plots for the model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="80be5-606">Ce code génère une série de graphiques de diagnostic représentés dans la figure 26.</span><span class="sxs-lookup"><span data-stu-id="80be5-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![premier graphique de diagnostic pour le modèle saisonnier](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![deuxième graphique de diagnostic pour le modèle saisonnier](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![troisième graphique de diagnostic pour le modèle saisonnier](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![quatrième graphique de diagnostic pour le modèle saisonnier](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="80be5-611">*Figure 26 : graphiques de diagnostic pour le modèle saisonnier.*</span><span class="sxs-lookup"><span data-stu-id="80be5-611">*Figure 26. Diagnostic plots for the seasonal model.*</span></span>

<span data-ttu-id="80be5-612">Même si nous parvenons à identifier quelques points saillants dans ces graphiques, il n'en ressort rien d'extraordinaire.</span><span class="sxs-lookup"><span data-stu-id="80be5-612">There are a few highly influential points identified in these plots, but nothing to cause great concern.</span></span> <span data-ttu-id="80be5-613">De plus, nous pouvons constater dans le graphique Normal Q-Q que les résidus sont répartis assez normalement, postulat important pour les modèles linéaires.</span><span class="sxs-lookup"><span data-stu-id="80be5-613">Further, we can see from the Normal Q-Q plot that the residuals are close to normally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="80be5-614">Prévision et évaluation des modèles</span><span class="sxs-lookup"><span data-stu-id="80be5-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="80be5-615">Il ne nous reste plus qu'une étape à effectuer pour terminer notre exemple.</span><span class="sxs-lookup"><span data-stu-id="80be5-615">There is just one more thing to do to complete our example.</span></span> <span data-ttu-id="80be5-616">Nous devons calculer les prévisions et mesurer les erreurs par rapport aux données réelles.</span><span class="sxs-lookup"><span data-stu-id="80be5-616">We need to compute forecasts and measure the error against the actual data.</span></span> <span data-ttu-id="80be5-617">Notre prévision concernera les 12 mois de l'année 2013.</span><span class="sxs-lookup"><span data-stu-id="80be5-617">Our forecast will be for the 12 months of 2013.</span></span> <span data-ttu-id="80be5-618">Nous pouvons calculer une mesure d’erreur pour cette prévision par rapport aux données réelles qui ne font pas partie de notre jeu de données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="80be5-618">We can compute an error measure for this forecast to the actual data that is not part of our training dataset.</span></span> <span data-ttu-id="80be5-619">De plus, nous pouvons comparer les performances réalisées sur les 18 années des données d'apprentissage à celles enregistrées au cours des 12 mois des données de test.</span><span class="sxs-lookup"><span data-stu-id="80be5-619">Additionally, we can compare performance on the 18 years of training data to the 12 months of test data.</span></span>  

<span data-ttu-id="80be5-620">Un certain nombre de mesures permettent de mesurer les performances des modèles chronologiques.</span><span class="sxs-lookup"><span data-stu-id="80be5-620">A number of metrics are used to measure the performance of time series models.</span></span> <span data-ttu-id="80be5-621">En l’occurrence, nous utiliserons l’erreur quadratique moyenne (ou RMS).</span><span class="sxs-lookup"><span data-stu-id="80be5-621">In our case we will use the root mean square (RMS) error.</span></span> <span data-ttu-id="80be5-622">La fonction suivante calcule l’erreur RMS entre deux séries :</span><span class="sxs-lookup"><span data-stu-id="80be5-622">The following function computes the RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function to compute the RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments to function RMS.error of wrong type encountered",
                    "ERROR: Input vector to function RMS.error is too short",
                    "ERROR: Input vectors to function RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check the arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate the values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute the RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="80be5-623">À l’instar de la fonction `log.transform()` , dont nous avons parlé dans la section « Transformations de valeurs », cette fonction contient beaucoup de code de recherche d’erreurs et de récupération d’exceptions.</span><span class="sxs-lookup"><span data-stu-id="80be5-623">As with the `log.transform()` function we discussed in the "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="80be5-624">Les principes utilisés sont les mêmes.</span><span class="sxs-lookup"><span data-stu-id="80be5-624">The principles employed are the same.</span></span> <span data-ttu-id="80be5-625">Le travail est accompli à deux endroits circonscrits à `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="80be5-625">The work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="80be5-626">Dans un premier temps, les séries chronologiques sont élevées à une puissance, car nous travaillons avec les logarithmes des valeurs.</span><span class="sxs-lookup"><span data-stu-id="80be5-626">First, the time series are exponentiated, since we have been working with the logs of the values.</span></span> <span data-ttu-id="80be5-627">Dans un deuxième temps, l'erreur RMS réelle est calculée.</span><span class="sxs-lookup"><span data-stu-id="80be5-627">Second, the actual RMS error is computed.</span></span>  

<span data-ttu-id="80be5-628">Étant dotés d'une fonction de mesure de l'erreur RMS, nous allons générer et sortir un tableau de données contenant les erreurs RMS.</span><span class="sxs-lookup"><span data-stu-id="80be5-628">Equipped with a function to measure the RMS error, let's build and output a dataframe containing the RMS errors.</span></span> <span data-ttu-id="80be5-629">Nous inclurons des termes pour le modèle de tendance seul et le modèle complet avec des facteurs saisonniers.</span><span class="sxs-lookup"><span data-stu-id="80be5-629">We will include terms for the trend model alone and the complete model with seasonal factors.</span></span> <span data-ttu-id="80be5-630">Le code suivant accomplit la tâche en utilisant les deux modèles linéaires que nous avons construits :</span><span class="sxs-lookup"><span data-stu-id="80be5-630">The following code does the job by using the two linear models we have constructed.</span></span>

    ## Compute the RMS error in a dataframe
    ## Include the row names in the first column so they will
    ## appear in the output of the Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="80be5-631">L'exécution de ce code génère la sortie présentée dans la figure 27 au niveau du port de sortie du jeu de données de résultat.</span><span class="sxs-lookup"><span data-stu-id="80be5-631">Running this code produces the output shown in Figure 27 at the Result Dataset output port.</span></span>

![comparaison de l’erreur RMS pour les modèles][26]

<span data-ttu-id="80be5-633">*Figure 27 : comparaison de l’erreur RMS pour les modèles.*</span><span class="sxs-lookup"><span data-stu-id="80be5-633">*Figure 27. Comparison of RMS errors for the models.*</span></span>

<span data-ttu-id="80be5-634">Ces résultats nous montrent que l’ajout des facteurs saisonniers au modèle a pour effet de réduire sensiblement l’erreur RMS.</span><span class="sxs-lookup"><span data-stu-id="80be5-634">From these results, we see that adding the seasonal factors to the model reduces the RMS error significantly.</span></span> <span data-ttu-id="80be5-635">Fort logiquement, l'erreur RMS au niveau des données d'apprentissage est plus limitée qu'au niveau de la prévision.</span><span class="sxs-lookup"><span data-stu-id="80be5-635">Not too surprisingly, the RMS error for the training data is a bit less than for the forecast.</span></span>

## <span data-ttu-id="80be5-636"><a id="appendixa"></a>ANNEXE A : guide de RStudio</span><span class="sxs-lookup"><span data-stu-id="80be5-636"><a id="appendixa"></a>APPENDIX A: Guide to RStudio</span></span>
<span data-ttu-id="80be5-637">RStudio étant très bien documenté, vous trouverez dans cette annexe des liens vers les principales sections de la documentation RStudio, qui vous aideront dans la prise en main du produit.</span><span class="sxs-lookup"><span data-stu-id="80be5-637">RStudio is quite well documented, so in this appendix I will provide some links to the key sections of the RStudio documentation to get you started.</span></span>

1. <span data-ttu-id="80be5-638">Création de projets</span><span class="sxs-lookup"><span data-stu-id="80be5-638">Creating projects</span></span>
   
   <span data-ttu-id="80be5-639">Vous pouvez organiser et gérer votre code R dans les projets à l’aide de RStudio.</span><span class="sxs-lookup"><span data-stu-id="80be5-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="80be5-640">Vous trouverez la documentation utilisant des projets à l’adresse https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="80be5-640">The documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="80be5-641">Je vous recommande de suivre ces instructions et de créer un projet pour les exemples de code R présentés dans ce document.</span><span class="sxs-lookup"><span data-stu-id="80be5-641">I recommend that you follow these directions and create a project for the R code examples in this document.</span></span>  
2. <span data-ttu-id="80be5-642">Modification et exécution de code R</span><span class="sxs-lookup"><span data-stu-id="80be5-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="80be5-643">RStudio offre un environnement intégré qui permet de modifier et d'exécuter du code R.</span><span class="sxs-lookup"><span data-stu-id="80be5-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="80be5-644">Vous trouverez la documentation à l’adresse https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="80be5-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="80be5-645">Débogage</span><span class="sxs-lookup"><span data-stu-id="80be5-645">Debugging</span></span>
   
   <span data-ttu-id="80be5-646">RStudio intègre de puissantes fonctionnalités de débogage.</span><span class="sxs-lookup"><span data-stu-id="80be5-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="80be5-647">Vous trouverez la documentation relative à ces fonctionnalités à l’adresse https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="80be5-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="80be5-648">Les fonctionnalités de résolution des problèmes de point d’arrêt sont documentées à l’adresse https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="80be5-648">The breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="80be5-649"><a id="appendixb"></a>ANNEXE B : informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="80be5-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="80be5-650">Ce didacticiel sur la programmation R couvre les concepts de base de ce qu'il vous faut pour utiliser le langage R avec Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="80be5-650">This R programming tutorial covers the basics of what you need to use the R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="80be5-651">Si vous ne connaissez pas le langage R, deux présentations sont disponibles sur le site CRAN :</span><span class="sxs-lookup"><span data-stu-id="80be5-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="80be5-652">« R pour les débutants » d'Emmanuel Paradis constitue un bon point de départ, à l'adresse http://cran.r-project.org/doc/contrib/Paradis-rdebuts_fr.pdf.</span><span class="sxs-lookup"><span data-stu-id="80be5-652">R for Beginners by Emmanuel Paradis is a good place to start at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="80be5-653">Une introduction à R par W. N.</span><span class="sxs-lookup"><span data-stu-id="80be5-653">An Introduction to R by W. N.</span></span> <span data-ttu-id="80be5-654">Venables, et</span><span class="sxs-lookup"><span data-stu-id="80be5-654">Venables et.</span></span> <span data-ttu-id="80be5-655">al.</span><span class="sxs-lookup"><span data-stu-id="80be5-655">al.</span></span> <span data-ttu-id="80be5-656">approfondit un peu le sujet : http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="80be5-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="80be5-657">Il existe de nombreux livres sur le langage R qui peuvent vous aider à vous lancer.</span><span class="sxs-lookup"><span data-stu-id="80be5-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="80be5-658">En voici quelques-uns que j'ai trouvés utiles :</span><span class="sxs-lookup"><span data-stu-id="80be5-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="80be5-659">« The Art of R Programming: A Tour of Statistical Software Design » de Norman Matloff est une excellente introduction à la programmation en langage R.</span><span class="sxs-lookup"><span data-stu-id="80be5-659">The Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction to programming in R.</span></span>  
* <span data-ttu-id="80be5-660">L’ouvrage « R Cookbook » de Paul Teetor propose des solutions aux problèmes rencontrés lors de l’utilisation du langage R.</span><span class="sxs-lookup"><span data-stu-id="80be5-660">R Cookbook by Paul Teetor provides a problem and solution approach to using R.</span></span>  
* <span data-ttu-id="80be5-661">« R in Action » de Robert Kabacoff est un autre ouvrage introductif utile.</span><span class="sxs-lookup"><span data-stu-id="80be5-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="80be5-662">Le site web d’accompagnement Quick R est une ressource utile à l’adresse http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="80be5-662">The companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="80be5-663">R Inferno de Patrick Burns est un ouvrage qui aborde sur un ton étonnamment humoristique plusieurs thèmes complexes liés à la programmation en R. L’ouvrage est disponible gratuitement à l’adresse http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="80be5-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. The book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="80be5-664">Si vous souhaitez examiner plus en profondeur les aspects avancés du langage R, jetez un œil au livre « Advanced R » de Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="80be5-664">If you want a deep dive into advanced topics in R, have a look at the book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="80be5-665">La version en ligne de ce livre est disponible gratuitement à l'adresse http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="80be5-665">The online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="80be5-666">Vous trouverez dans la section Task Views du site CRAN un catalogue de packages R pour l’analyse des séries chronologiques : http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="80be5-666">A catalogue of R time series packages can be found in the CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="80be5-667">Pour plus d’informations sur les packages d’objets chronologiques spécifiques, reportez-vous à la documentation de ce package.</span><span class="sxs-lookup"><span data-stu-id="80be5-667">For information on specific time series object packages, you should refer to the documentation for that package.</span></span>

<span data-ttu-id="80be5-668">L’ouvrage « Introductory Time Series with R » de Paul Cowpertwait et Andrew Metcalfe propose une introduction à l’utilisation de R pour l’analyse des séries chronologiques.</span><span class="sxs-lookup"><span data-stu-id="80be5-668">The book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction to using R for time series analysis.</span></span> <span data-ttu-id="80be5-669">Divers textes théoriques proposent des exemples R.</span><span class="sxs-lookup"><span data-stu-id="80be5-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="80be5-670">Quelques ressources Internet particulièrement utiles :</span><span class="sxs-lookup"><span data-stu-id="80be5-670">Some great internet resources:</span></span>

* <span data-ttu-id="80be5-671">DataCamp : apprenez le langage R tout en restant confortablement installé devant votre navigateur, grâce à des leçons vidéo et des exercices de codage.</span><span class="sxs-lookup"><span data-stu-id="80be5-671">DataCamp: DataCamp teaches R in the comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="80be5-672">Il existe des didacticiels interactifs sur les dernières techniques et de langage R.</span><span class="sxs-lookup"><span data-stu-id="80be5-672">There are interactive tutorials on the latest R techniques and packages.</span></span> <span data-ttu-id="80be5-673">Suivez le didacticiel R interactif gratuit à l’adresse https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="80be5-673">Take the free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="80be5-674">Guide de prise en main de R à partir de Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="80be5-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="80be5-675">Un bref didacticiel sur le langage R par Kelly Black de l’Université de Clarkson : http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="80be5-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="80be5-676">Plus de 60 ressources sur le langage R : http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="80be5-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
